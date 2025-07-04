---
title: "Deployments"
---

## Overview and terminology

This page describes the individual steps involved in deploying application changes to GitLab.com. Guidance on how to follow the deployment process are also described. For a high-level view of the overall deployment and release approach please see the [Deployments and Releases handbook page](/handbook/engineering/deployments-and-releases/).

### A tour of auto-deploy with a Release Manager

{{< youtube "zdVzX5ZY7o4" >}}

### GitLab.com deployments process

GitLab.com receives updates multiple times a day.

Automated tasks in the [release-tools](https://gitlab.com/gitlab-org/release-tools) project are setup to build and deploy packages.

#### Building packages

- New branches for deployment are created every hour from Monday through Friday. The branches are created
  from the latest commit that has passed the CI tests ('green build'). This means that if specs are
  failing in [`gitlab-org/gitlab`](https://gitlab.com/gitlab-org/gitlab), deployments cannot
  progress further.
- Then a new version is tagged on the latest commit and a new package begins being built.
- When a branch is created, any merge requests labeled with `~"Pick into auto-deploy"` (See [Labels of importance](#labels-of-importance))
  are cherry-picked into the branch, before a package is tagged.
  In addition, every 15 minutes, a task runs to cherry-pick merge requests labeled with `~"Pick into auto-deploy"`
  into the latest deployment branch. If one or more MRs are cherry-picked, a new package is tagged.

![GitLab.com deployment process](/images/engineering/deployments-and-releases/deployments/gitlab-com-auto-deploy-build-process.png)

- [Source](https://docs.google.com/presentation/d/1YRjA1dYCXNXp06VltDYlik1MdFyzUvaeXKk69mMPcA4/edit?usp=sharing)

A package is created approximately every hour (with every new auto-deploy branch), if there are new commits with successful CI pipelines.

1. The package is tagged and the build process can start
1. 2a. From the tag the Omnibus package is built.

   2b. In parallel a Cloud Native GitLab package is built.

#### Deploying packages

- Every 15 minutes, an automated task selects the latest package that has completed building and starts the deployment process.

![GitLab.com deployment process](/images/engineering/deployments-and-releases/deployments/gitlab-com-deployment-pipeline.png)

- [Source](https://docs.google.com/presentation/d/1YRjA1dYCXNXp06VltDYlik1MdFyzUvaeXKk69mMPcA4/edit?usp=sharing)

A package is deployed to GitLab.com in the following steps:

1. At regular intervals, an automated task in release-tools searches for the latest available package that has completed building.

   1a. When a built package is found, it is automatically deployed to gstg-cny, [the canary stage of staging.gitlab.com](/handbook/engineering/infrastructure/environments/#staging-canary).

   1b. In parallel, the same package is deployed to the [Staging-ref environment, gstg-ref](/handbook/engineering/infrastructure/environments/#staging-ref)
1. A set of automated QA end-to-end/integration tests are run. Note that two sets of blocking QA tests are executed, one targeting gstg-cny and the other targeting staging (gstg). This is designed to assist with exposing issues arising in mixed deployment environments, where multiple versions of GitLab components are deployed that share services such as the database
1. After passing, the package is automatically deployed to gprd-cny, [the canary stage of gitlab.com](/handbook/engineering/infrastructure/environments/#production-canary), where [covering the canary stage and how to use it](/handbook/engineering/infrastructure/environments/canary-stage) can take place. This means that specific projects (like `gitlab-org/gitlab`) as well as a small amount of end user traffic will be using the new package.
1. Like with deployment to staging-canary above, two sets of automated QA end-to-end/integration tests are run. One targets the canary stage of production, the other targets the main stage (to ensure the new and old code are still functional). Note that the `smoke` and `reliable` tests targeting production canary (gprd-cny) are blocking.
1. After 30 minutes in the [canary stage of gitlab.com](/handbook/engineering/infrastructure/environments/#production-canary), and provided no new exceptions or alerts are reported, the package is considered to be ready for deployment to [gitlab.com](/handbook/engineering/infrastructure/environments/#production) and [staging.gitlab.com](/handbook/engineering/infrastructure/environments/#staging)
1. The promotion to [gitlab.com](/handbook/engineering/infrastructure/environments/#production) and [staging.gitlab.com](/handbook/engineering/infrastructure/environments/#staging) is triggered manually by the release
managers. Ongoing incidents or Change Requests with the `blocks deployments` label will prevent a package from being deployed to gstg (staging) and gprd (production). Note that deployments to canary (both gstg-cny and gprd-cny)
will not be blocked. Migrations will also not be blocked since they are executed during canary deployments. However, post deploy migrations will be blocked.
1. Deployment to the staging environment
1. Production checks are performed to asses the health of the environment. If considered to be healthy the pipeline will automatically continue
1. Deployment to the production environment runs delayed to staging
Each deployment will trigger a notification in the Slack channel [#announcements](https://gitlab.slack.com/archives/C8PKBH3M5).
As part of the deployments, a QA issue is created in [release/tasks](https://gitlab.com/gitlab-org/release/tasks/) issue tracker to inform the people who are
involved in the process that their change is going through environments

### Post-deploy migration (PDM) execution

To make GitLab.com packages rollbackable, the [post-deploy migrations](https://docs.gitlab.com/ee/development/database/post_deployment_migrations.html) are independent from the GitLab.com deployment process. These migrations
are run in staging and production environments through the post-deploy migration pipeline that is triggered on a daily basis at the discretion of
the release managers.

![Post deploy migration pipeline](/images/engineering/deployments-and-releases/deployments/post-deploy-migration-pipeline.png)

- [Source](https://docs.google.com/presentation/d/1YRjA1dYCXNXp06VltDYlik1MdFyzUvaeXKk69mMPcA4/edit?usp=sharing)

When a release manager executes the post-deploy migration pipeline:

1. Post-deploy migration scripts run on staging
1. QA tests execute against staging
1. Following a successful QA verification, post-deploy migration scripts run on production.

Details of this pipeline can be found in the [post-deploy migration pipeline documentation](https://gitlab.com/gitlab-org/release/docs/-/tree/master/general/post_deploy_migration).

To determine if a post-deploy migration has been executed [please see this guide](https://gitlab.com/gitlab-org/release/docs/-/blob/master/general/post_deploy_migration/readme.md) for more information.
If, after 48 hours from the merge of your MR, you already have determined with the guide above that your Post-deploy migration has not yet run, and you have questions, please reach out to Release Managers on the [#releases](https://gitlab.slack.com/archives/C0XM5UU6B) channel.

### Deployment Rollbacks

Rollbacks can be a fast and safe way to mitigate an incident. By rolling back to a previous package we remove the cause of the incident but we also block all further deployments until a fix has been merged, packaged and is ready to deploy. Because of the potential disruption to the release process only [Release Managers](/handbook/engineering/deployments-and-releases/#release-managers) have permissions to execute a rollback.

Factors to consider before deciding to rollback:

1. Is a rollback available? We can only rollback to the package of the last execution of [post-deploy migrations](/handbook/engineering/deployments-and-releases/deployments/#post-deploy-migration-pdm-execution). [A chatops command](https://gitlab.com/gitlab-org/release/docs/-/blob/master/runbooks/rollback-a-deployment.md#1-gather-package-information) is available to test for suitability.
1. Is the incident able to be mitigated with a feature flag? Many new changes include a feature flag. Identifying, and turning off is usually the fastest mitigation.
1. Be aware that a package may include several hundred changes, rolling back will remove them all and could impact multiple teams especially close to the monthly release deadline.

Because of the level of disruption a rollback causes we would normally only consider rollbacks an option for an S1 or S2 incident. More details about how to assess incident mitigation options are available in the [incidents runbook](https://gitlab.com/gitlab-org/release/docs/-/blob/master/runbooks/incident.md).

If we decide to go ahead with a rollback, Release Managers should follow the [rollbacks runbook](https://gitlab.com/gitlab-org/release/docs/-/blob/master/runbooks/rollback-a-deployment.md#overview).

#### Rollback Pipeline

A rollback is essentially a new deployment but of a previously deployed package. As a previously deployed package we already know it is stable and can safely reduce the amount of time spent testing throughout the rollout.

Gitaly and Praefect have a dependency on the GitLab Rails version which means we need to rollback in the reverse order to the one we deploy in. To achieve this we have a separate rollback pipeline rather than simply re-running the deployment pipeline.

Example of the Staging environment rollback pipeline:

![Example of the Staging environment rollback pipeline](/images/engineering/deployments-and-releases/deployments/rollback-pipeline.png)

### Deployment blockers

Anyone can **halt or block a deployment to Production** by:

1. [Declaring](https://gitlab.com/gitlab-com/runbooks/docs/incident-io-onboard/incident-management.md#how-to-raise-an-incident) an [incident](/handbook/engineering/infrastructure/incident-management/#reporting-an-incident):
   - Declaring a **severity1** or **severity2** incident will **default to blocking deployments**.
   - Declaring **severity3** and **severity4** will default *"Blocks Deployments"* to **"no"**.
   - Changing from a **severity3 or lower** to **severity2 or higher** will **set** the *"Blocks Deployments"* flag, unless it has been manually changed.
   - Lowering the severity **below severity2** will **unset** the flag and allow deployments, unless it has been manually changed.

2. From the incident Slack channel, run the `/incident field` command to update [custom fields](https://gitlab.com/gitlab-com/runbooks/docs/incident-io-onboard/oncall.md#on-call-alert-handling-process), then select **'Yes'** under *Block Deployments*.

3. Alert the Release Managers in the [#releases](https://gitlab.slack.com/archives/C0XM5UU6B) channel.

In addition, automated deployments to **any production environment** (including [canary]), are
halted during the change lock period. Currently, the change lock period is between every **Friday 23:00 UTC and Monday 06:00 UTC** as well as during any [scheduled Production Change periods](/handbook/engineering/infrastructure-platforms/change-management/#production-change-lock-pcl).

During the change lock period, manual deployment can be triggered through GitLab ChatOps if the deployment fixes **a severity::1 availability or security issue**.

Deployments to production will be blocked by the following events:

1. An [active incident with the `blocks deployment` label](/handbook/engineering/infrastructure/incident-management/#labeling).
1. Ongoing [change issues with the `blocks deployment` label](/handbook/engineering/infrastructure-platforms/change-management/#change-criticalities).
1. Failures in [blocking (`smoke` and `reliable`) automated end-to-end tests targeting staging canary (gstg-cny), staging (gstg), production canary (gprd-cny), and production (gprd)](/handbook/engineering/testing/end-to-end-pipeline-monitoring/).

Release Managers may decide, with input from the [EOC](/handbook/engineering/infrastructure/incident-management/#incident-response-roles) to override a block and continue with the deployment.

## Labels of importance

### GitLab.com pick label

For code that needs to be deployed to GitLab.com with higher priority than the
regular cadence, we have `~"Pick into auto-deploy"` label. Note that branches are regularly created throughout the day, inclusion in a scheduled deployment does not require this label.

The automated systems that create a new GitLab.com release will look for this label
specifically, and any merge request with this label and a severity::1/severity::2 severity label will be automatically cherry-picked
into the active auto-deploy branch. In case the merge request cannot be picked,
which can happen if there is a conflict in the files being picked, the message
will be posted in the merge request asking the author to create a new merge request
targeting the currently active release branch.

The label should be only used under the following circumstances, when the merge
request is especially urgent. For example:

- Resolves or mitigates a severity::1/severity::2 incident
- Resolves a regression that can lead to a severity::1/severity::2 problem
- Urgent performance or availability fix that can improve the stability of
GitLab.com

In case of high-severity bugs, please proceed to [report an incident](/handbook/engineering/infrastructure/incident-management/#reporting-an-incident) to track
events and response.

If this label is added because a merge request is blocking further deploys,
consider leaving a note in [#releases](https://gitlab.slack.com/archives/C0XM5UU6B) Slack channel to raise awareness of the status.

**For new features or non-urgent fixes**, the label **should not be used** because
the new release is only days or hours away.

Directions on how to know whether a MR is deployed to GitLab.com are in the [release/docs](https://gitlab.com/gitlab-org/release/docs/blob/master/general%2Fdeploy%2Fauto-deploy.md#auto-deploy-status).

## Frequently Asked Questions

### When will my merge request be deployed?

We currently create an auto-deployment branch at a [specific timeline](/handbook/engineering/deployments-and-releases/deployments/#gitlabcom-deployments-process). The current Mean Time To Production time and target can be seen on the [Infrastructure performance indicators page](/handbook/engineering/infrastructure/performance-indicators/#mean-time-to-production-mttp).

For a merge request with [the pick label](/handbook/engineering/deployments-and-releases/deployments/#gitlabcom-pick-label), the
process is different.

### How can I determine what environment my merge request is currently in?

The [release tools](https://gitlab.com/gitlab-org/release-tools/) makes use of `workflow::` labels
in MRs to indicate which stage of the [deployments process](#gitlabcom-deployments-process) a merge
request is in. For example, the presence of the `workflow::production` label in a merge request
indicates it has been deployed to production.

See [this](https://gitlab.com/gitlab-org/release/docs/-/blob/master/general/deploy/auto-deploy.md#status-of-a-merged-mr-or-a-commit)
guide for more information.

### I found a regression, what do I do next?

If you've found a regression with a potentially high [severity](/handbook/engineering/infrastructure/engineering-productivity/issue-triage/#severity), immediately follow the steps in [Deployment blockers](/handbook/engineering/deployments-and-releases/deployments/#deployment-blockers) to halt the deployment.

For high severity bugs found in the lead up to the [monthly release](/handbook/engineering/releases/) please also alert the Release Managers in [#releases](https://gitlab.slack.com/archives/C0XM5UU6B).

## Resources

| Description        | Location            |
|--------------------|---------------------|
| Deployment orchestration | [Link](https://gitlab.com/gitlab-org/release-tools/) |
| Deployment documentation | [Link](https://gitlab.com/gitlab-org/release/docs) |
| Release related tasks issue tracker | [Link](https://gitlab.com/gitlab-org/release/tasks/) |
| Delivery group issue tracker | [Link](https://gitlab.com/gitlab-com/gl-infra/delivery/issues) |
| Release manager schedule | [Link](https://about.gitlab.com/community/release-managers/) |
| Maintenance Policy | [Link](https://docs.gitlab.com/ee/policy/maintenance.html) |
