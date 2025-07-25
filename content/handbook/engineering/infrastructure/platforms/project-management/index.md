---
title: "The Infrastructure Platforms Project Management"
---

## Project Management in Platforms

We use GitLab epics and issues to communicate the progress and status of our work.
The [Platforms epic](https://gitlab.com/groups/gitlab-com/-/epics/2115) is indexing the top level epic for each team, and links to active OKR's for a given quarter.
All teams in Infrastructure Platforms follow these guidelines so that it is easy for team-members to contribute to different projects if needed.

### Projects are reviewed weekly in the Grand Review

**Every Wednesday**, the DRI for a project is expected to update the status block in the epic description to:

1. Indicate any project blockers.
2. Briefly highlight progress since the last update.
3. Indicate planned next steps, or mitigations required to progress.

This enables other engineers and other managers to have good information about projects in an asynchronous fashion.

Completed epics should remain "Open" with the ~"workflow-infra::In Progress" label.
Update the status block in the epic description to summarize the project and share the completed status.

We use [automation](https://gitlab.com/gitlab-com/gl-infra/epic-issue-summaries/) to collect the status information into top-level epics for each group, and to gather status updates from epic notes.
This automation runs several times each day, and can be triggered by [running the pipeline listed on the project page](https://gitlab.com/gitlab-com/gl-infra/epic-issue-summaries/-/pipeline_schedules).

#### Status updates on project epics

Comments are automatically generated on project epics to report status.
To enable this functionality, please ensure the epic follows [these steps](https://gitlab.com/gitlab-com/gl-infra/epic-issue-summaries/-/blob/26295198fedcde8af09bf6b6abb22ed3acd52f07/README.md#child-epics).

#### When a project is finished

1. The epic should be left "Open" and retain the ~"workflow-infra::In Progress" label so that the project will still be listed for the next Platforms Grand Review.
1. The DRI is responsible for updating the epic description to ensure each section is up to date including the `Participants` section.
1. The DRI creates the closing status (final status update) which includes:
   1. The original problem
   1. A brief description of the changes made
   1. Information about the impact of the project now that it is completed
   1. A link to the demo / walkthrough video
   1. An instruction to direct the Grand Reviewers to close the epic
   1. Emojis and / or shout-outs are also welcome but not required

Completed epics will be reviewed, celebrated, updated to done, and closed in the next [`Platforms Grand Review`](https://www.youtube.com/playlist?list=PL05JrBw4t0KqDXSHdlUvPWHOj_Hw8JdQ1) (Playlist accessible using GitLab Unfiltered account).

Note that closing statuses are helpful when producing the end-of-year team summaries.

## Epics

Epics must always have the following sections:

- A Problem Statement
- Directly responsible individuals (DRI) responsible for the project completion
- Defined exit criteria
- Development Log, containing the previous Status Updates and any other relevant information to log
- Status Update, with the latest status update of the Epic
- Start date and estimated due date

### Sections format

The DRI of the epic should be the assignee, and there should only be one assignee for an epic.

Use the following headings and structure in the Epic description:

#### Participants Section

This section is dynamic and includes people who are currently contributing to the Epic work.
The DRI and the EM are responsible for updating the list of participants accordingly.

```markdown
### Participants

- @participant1
- @participant2
- @participantN
```

#### Status Section

The status section is generated automatically on sub-epics.
See the section on [status updates on project epics](#status-updates-on-project-epics) for more info.

### Should this be an issue or an epic?

We use epics to show that a set of work can be combined under one theme to meet a specific goal or lead to a specific impact.
Epics can cover any set of work that is likely to take longer than two weeks, or has already been running for longer than two weeks.
We can then report on our progress towards that goal regularly and clearly demonstrate the impact of our work when we are finished.

## Specific Issue Types

### Corrective Actions and Security issues

We also work on corrective actions and security issues labeled as `~"corrective action"` or `~"security"`.
For these issues, `severity::*` labels are set to meet specific SLOs.

- For security issue see the [Time to resolve table by severity](/handbook/security/#severity-and-priority-labels-on-security-issues)
- Corrective Actions SLOs are currently based on definitions from [Quality](/handbook/engineering/infrastructure/engineering-productivity/issue-triage/#severity-slos):

## Labels

The Infrastructure Platform teams uses the following set of labels:

| Description | Labels |
|-------------|--------|
| The section label | `devops::data_access` <br/>`group::GitLab Dedicated` <br/>`devops::gitlab-delivery`<br/> `devops::developer experience` <br/>`group::Production Engineering`<br/> `devops::tenant scale` <br/>  |
| The team label | `group::durability` <br/> `group::gitaly` <br/> `group::git` <br/> `group::database frameworks` <br/> `group::database operations` <br/> `team::Observability` <br/> `team::runway` <br/> `team::Foundations` <br/> `team::Ops`  <br/> `group::Self Managed` <br/> `group::build` <br/> `group::framework` <br/> `group::delivery-deploy` <br/> `group::delivery-release` <br/> `team::Environment Automation` <br/> `team::Switchboard` <br/> `team::US PubSec` <br/> `group::developer tooling` <br/> `group::development analytics` <br/> `group::feature readiness` <br/> `group::performance enablement` <br/> `group::test governance` <br/> `group::cells infrastructure` <br/> `group::organizations` <br/> `group::geo`|
| Scoped `workflow-infra::*` labels | (see below) |
| Optional Scoped `Service` labels | `Service::*` |

### Workflow labels

We leverage scoped workflow labels to track different stages of work.
They show the progression of work for each issue and allow us to remove blockers or change focus more easily.

While issues may not need to go through every state, the standard progression of workflow is from top to bottom in the table below:

| State Label | Description |
| ----------- | ----------- |
| ![Triage](/images/engineering/infrastructure/platforms/project-management/label-triage.png) | Default label. Task is raised and effort is needed to determine the correct action, work required or team ownership |
| ![Proposal](/images/engineering/infrastructure/platforms/project-management/label-proposal.png) | Proposal is created following triage and put forward for a review. <br/>If there are no further questions or blockers, the issue can be moved into "Ready". |
| ![Ready](/images/engineering/infrastructure/platforms/project-management/label-ready.png) | Proposal is complete and the issue is waiting to be picked up for work. |
| ![In Progress](/images/engineering/infrastructure/platforms/project-management/label-in_progress.png) | Issue is assigned and work has started. <br/>While in progress, the issue should be updated to include steps for verification that will be followed at a later stage.|
| ![Under Review](/images/engineering/infrastructure/platforms/project-management/label-under_review.png) | Issue has an MR in review. |
| ![Verify](/images/engineering/infrastructure/platforms/project-management/label-verify.png) | MR was merged and we are waiting to see the impact of the change to confirm that the initial problem is resolved. |
| ![Done](/images/engineering/infrastructure/platforms/project-management/label-done.png) | Issue is updated with the latest graphs and measurements, this label is applied and issue can be closed. |

There are three other workflow labels of importance:

| State Label | Description |
| ----------- | ----------- |
| ![Cancelled](/images/engineering/infrastructure/platforms/project-management/label-cancelled.png) | Work in the issue is being abandoned due to external factors or decision to not resolve the issue. After applying this label, issue will be closed. |
| ![Stalled](/images/engineering/infrastructure/platforms/project-management/label-stalled.png) | Work is not abandoned but other work has higher priority. After applying this label, team Engineering Manager is mentioned in the issue to either change the priority or find more help. |
| ![Blocked](/images/engineering/infrastructure/platforms/project-management/label-blocked.png) | Work is blocked due external dependencies or other external factors. Where possible, a [blocking issue](https://docs.gitlab.com/ee/user/project/issues/related_issues.html) should also be set. After applying this label, issue will be regularly triaged by the team until the label can be removed. |

### Labels in gitlab-org group

Stage groups use [type labels](/handbook/product/groups/product-analysis/engineering/metrics/#work-type-classification) to label merge requests in projects in the `gitlab-org` group.
If you need a stage group to perform work, it is best to apply the relevant stage group label when the issue is created.

## Issue Trackers

This is a list of the group issue trackers:

| Group | Tracker |
|-------|---------|
| Dedicated | [issue tracker](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/team/-/issues)|
| Delivery | [issue tracker](https://gitlab.com/gitlab-com/gl-infra/delivery/-/issues) |
| Production Engineering | [issue tracker](https://gitlab.com/gitlab-com/gl-infra/production-engineering/-/issues)|
| Scalability | [issue tracker](https://gitlab.com/gitlab-com/gl-infra/scalability/-/issues) |

### Triage Ops

For labeling and bot notifications under [gitlab-com/gl-infra](https://gitlab.com/gitlab-com/gl-infra) we use [gitlab-triage](https://gitlab.com/gitlab-org/ruby/gems/gitlab-triage) and the [triage-ops](https://gitlab.com/gitlab-com/gl-infra/triage-ops/) project.
For labeling, enforcing SLOs, and managing workflow labeling there are common policies that are set uniformly for projects in Infrastructure, Platform.
For more information and how to add additional policies see [the project README.md](https://gitlab.com/gitlab-com/gl-infra/triage-ops/-/blob/master/README.md?ref_type=heads).

## Retrospectives

At the end of the quarter, or the completion of a large deliverable, teams should perform a retrospective to capture learnings.
There is no set format for the retrospective though Engineering Managers should be aware of the [GitLab Retrospective Guidelines](/handbook/engineering/management/group-retrospectives/).
The retrospective DRI identifies a list of actions which they consolidate in the Summary of Actions section in the issue description.

Process to identify actions:

1. Add a comment on each thread with Actions as the title of the comment (H3 level)
1. Some threads may not require an action, you may want to state this explicitly at the end of the thread for transparency
1. Below the Actions comment, add a suggestion on an action the team can take
1. Ping the contributors to get a round of validation on the actions and potential refinement
1. Create an issue for each action and list them in the Summary of Actions section
