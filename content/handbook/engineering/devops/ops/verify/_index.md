---
title: "Verify Stage"
description: "The verify development group handbook page."
---

## Vision

We enable global software organizations and teams to make great decisions with [smart feedback loops](https://about.gitlab.com/direction/ops/#smart-feedback-loop) by delivering [speedy, reliable pipelines](https://about.gitlab.com/direction/ops/#speedy-reliable-pipelines) in a [comprehensive CI platform](https://about.gitlab.com/direction/ops/#verify) that embodies [Operations for All](https://about.gitlab.com/direction/ops/#operations-for-all).

## Technical Roadmap

### FY25 to FY26

There are 3 Core Themes that continue to be a focus for GitLab CI:

1. Scalability
1. Availability
1. Sustainability & Maintainability

We aim to drive enhancements that benefit GitLab.com, Self-Managed and Dedicated customers.

1. With [accelerated efforts](https://gitlab.com/gitlab-org/verify-stage/-/issues/508), we aim to complete [CI Data Partitioning](https://gitlab.com/gitlab-org/gitlab/-/blob/master/doc/architecture/blueprints/ci_data_decay/pipeline_partitioning.md) for our top 6 tables in the CI Database in FY25. Not only does this impact CI, this addresses a critical availability need impacting all of gitlab.com.  This is a cross-stage effort with backend engineers across Verify in order to parallelize the ongoing effort. (ETA: Q3)
1. [CI Data Retention](https://gitlab.com/gitlab-org/verify-stage/-/issues/440): with the continued growth in our CI database tables, Verify and Infrastructure teams will work on removing data upon analysis of disk usage. This includes removal of both table records and indexes.  Engineering will also collaborate with Product to implement features that allow Self-Managed and Dedicated customers to configure their own CI data retention policies. (ETA: Analysis in Q3, Implementation in Q4 until FY26-Q1/Q2)
1. CI Data Management (TBD): Determine the data management tools that provide the greatest flexibility to our customers to manage their own CI data. (For example, removal of old CI builds or artifacts that consume their disk usage). We will consult with Product and UX to understand the tools/feature set that are most requested. (ETA: FY26-Q3)
1. [CI Minutes / Compute Units support](https://gitlab.com/gitlab-org/gitlab/-/issues/490681): Build better tooling for our Support and SRE teams when responding to incidents that require us to restore CI Minutes for customer namespaces on GitLab.com, and ensure domain knowledge is shared across the Verify and Fulfillment teams. (ETA: Q4)
1. [Pipeline creation speed improvements](https://gitlab.com/groups/gitlab-org/-/epics/7290): benchmarking and instrumentation will be our focus in order to identify the bottlenecks and improve pipeline creation speeds. This will be critical for driving [Error Budget](/handbook/engineering/error-budgets/) improvements. (ETA: Ongoing efforts to FY26)
1. [Cells 1.0 Database Support](https://gitlab.com/groups/gitlab-org/-/epics/12323): the goal is to complete the Verify dependencies by Q4.

The [product roadmap](https://gitlab.com/gitlab-com/Product/-/issues/12911) outlines the expected deliverables for FY25.

#### 3 Year Vision

1. Continue to iterate on the Verify stage technical debt roadmap. How do we represent the highest priorities in a SSOT like an issue board?
1. Tracking **Unplanned Work** and making that more visible, to account for this during Engineering capacity or headcount planning. (For example, incident response, requests for help issues, triaging questions on Slack)
1. [Pipeline speed improvements](https://gitlab.com/groups/gitlab-org/-/epics/7290) - while benchmarking and instrumentation has been a focus, we have not:
   1. [Implemented distributed tracing on our CI workers](https://gitlab.com/groups/gitlab-org/-/epics/11040#note_1568112854)
   1. Prioritized further work in [CI/CD Build Speed working group](/handbook/company/working-groups/ci-build-speed/)
   1. Built more observability related to Pipeline speed improvements.
1. [CI Events](https://docs.gitlab.com/ee/architecture/blueprints/gitlab_ci_events/) - this is deferred from FY25 due to capacity constraints in Verify.
1. Better onboarding for contributors who are not CI subject domain experts - this includes improvements to code readability and accessibility, or better documentation and onboarding material.

### FY24

The Verify Pipeline teams focused on the following Engineering-led initiatives, in addition to our deliverables for the FY24 Yearlies:

1. [CI Data Partitioning](https://gitlab.com/gitlab-org/gitlab/-/blob/master/doc/architecture/blueprints/ci_data_decay/pipeline_partitioning.md)
1. Pipeline speed improvements - including analysis of pipeline performance
1. Review of the [data retention strategy of CI data on gitlab.com](https://gitlab.com/gitlab-org/verify-stage/-/issues/440)
1. Security vulnerabilities and infradev issues related to SaaS availability
1. S1/S2 bug burndown of Categories that do not have planned feature development for FY24.
    1. Note that this also includes the `Continuous Integration` category, which has the biggest backlog of bugs in Verify.  While it may be considered to be "Maintenance" (no new feature development planned), this work remains critical in ensuring we keep GitLab CI performant and reliable.
    1. [Pipeline Execution](/handbook/engineering/devops/ops/verify/pipeline-execution/) owns the `Continuous Integration` category. The team is also the DRI for CI Data Partitioning and Pipeline speed improvement efforts.

### FY23

The Verify stage focused on reliability and scalability of GitLab CI, which was critical for the availability of gitlab.com.  This included addressing database performance, security vulnerabilities, performance improvements and relevant technical debt.
This ensured GitLab remained secure, compliant and performant, with our SaaS offering that was able to maintain [SLAs of gitlab.com](/handbook/engineering/monitoring/#gitlabcom-service-availability).

## Mission

As engineers in Verify we know our customers because we _are_ our customers, and we are constantly striving to make our platform better for everyone. We do this through [iteration](/handbook/values/#iteration), [dogfooding](/handbook/values/#dogfooding), and being involved in our open source community. We innovate, we collaborate, and we challenge assumptions to arrive at great results.

We take ownership of the things we build, with a focus on stability and availability. We do this by having a deep technical understanding of the operation and performance characteristics of our platform, and a proactive perspective to future growth.

## Who we are

The Verify stage is made up of 5 groups:

1. [Verify:Pipeline Authoring](/handbook/engineering/devops/ops/verify/pipeline-authoring/)

1. [Verify:Pipeline Execution](/handbook/engineering/devops/ops/verify/pipeline-execution/)

1. [Verify:Runner](/handbook/engineering/devops/ops/verify/runner/)

1. [Verify:CI Platform](/handbook/engineering/devops/ops/verify/ci-platform/)

### Verify:Pipeline Authoring

{{< team-by-manager-role "Engineering Manager(.+)Pipeline Authoring" >}}

### Verify:Pipeline Execution

{{< team-by-manager-role "Engineering Manager(.+)Pipeline Execution" >}}

### Verify:Runner

{{< team-by-manager-role "Engineering Manager(.+)Runner" >}}

### Verify:CI Platform

{{< team-by-manager-role role="Senior Manager(.+)Verify" team="CI Platform" >}}

### Verify Engineering Leaders

{{< team-by-manager-role role="Senior(.+)Manager(.+)(Verify)" team="(Principal|Pipeline)">}}

### Stable Counterparts

{{< engineering/stable-counterparts role="Verify" other-manager-roles="Engineering Manager(.+)(Pipeline Authoring|Pipeline Execution|Runners)|Senior Manager(.+)Verify" >}}

## How we work

### Jobs to be done (JTBD)

A [Job to be Done (JTBD)](/handbook/product/ux/jobs-to-be-done/) is a framework, or lens, for viewing products and solutions in terms of the jobs customers are trying to achieve.

* [Verify:Pipeline Execution JTBD](/handbook/engineering/devops/ops/verify/pipeline-execution/jtbd/)
* [Verify:Pipeline Authoring JTBD](/handbook/engineering/devops/ops/verify/pipeline-authoring/jtbd/)
* [Verify:Runner JTBD](/handbook/engineering/devops/ops/verify/runner/jtbd/)

### Developer Onboarding in Verify

Welcome to the team! Whether you're joining GitLab as a new hire, transferring internally, or ramping up on the CI domain knowledge to tackle issues in our area, you'll be assigned an [onboarding/shadowing buddy](/handbook/company/culture/all-remote/onboarding) so you can have someone to work with as you're getting familiarized with our codebase, our tech stack and general development processes on your Verify team.

Read over this page as a starting point and feel free to set up regular sync or async conversations with your buddy. We recommend setting up weekly touch points, at a minimum, and joining our regular team syncs to learn more about how we work. (Reach out to our Engineering Managers for an invite to those recurring meetings). Please also schedule a few coffee chats to meet some members of our team. You will be assigned a team specific developer onboarding issue (For example, [Pipeline Execution Developer onboarding checklist](https://gitlab.com/gitlab-org/ci-cd/onboarding/-/blob/master/.gitlab/issue_templates/verify-pipeline-execution_developer-onboarding.md)) for you to go through. It contains admin tasks to complete (as a new team member, if relevant), and also links to technical documentation, meeting agendas, and recordings.

Issues labeled with `~onboarding` are smaller issues to help you get onboarded into the CI feature area. We typically work Kanban, so if there aren't [any `~onboarding` issues in the current milestone](https://gitlab.com/groups/gitlab-org/-/boards/1372896?milestone_title=%23started&label_name[]=onboarding), reach out to the Product Manager and/or Engineering Managers to see which issues you can start on as part of your onboarding period.

In May 2021, we introduced the [CI Shadow Program](https://gitlab.com/gitlab-com/Product/-/issues/2542), which we are trialing as a way to onboard existing GitLab team members from other Engineering teams to the CI domain and contribute to CI features.

#### Onboarding Buddies

Onboarding buddies are assigned to new hires to ensure their first few months of onboarding go smoothly. It's recommended that onboarding buddies set up weekly check-ins, whether that's async (such as a Slack DM) or sync (such as recurring coffee chats).

**Reviewing Merge Requests**

In addition to helping those _new hire/transfer_ through any issues with their set up or assigned tasks, it's recommended that their onboarding buddies add the _new hire/transfer_ as an additional reviewer on any MRs the onboarding buddy has been requested to review. Ideally this takes place after they've been working in Verify for at least 3 months, and as mutually agreed upon between both parties. This step further builds the _new hire/transfer's_ CI knowledge and allows for CI domain expertise to be shared amongst all engineers in Verify.

Similar to our [reviewer mentorship programs](/handbook/engineering/workflow/code-review/#reviewer-mentorship-program), the _new hire/transfer_ will review the merge request as if they're being asked to perform the code review. Once complete, they'll assign the MR back to their onboarding buddy.  It is expected that the onboarding buddy will also complete the code review, then provide the _new hire/transfer_ feedback about their code review. Ideally this takes place at their next check-in, where notes are captured in a shared Google Doc or a GitLab issue for ease-of-collaboration.

### API development

Our API exists in two formats ([REST](https://docs.gitlab.com/ee/api/#rest-api) and [GraphQL](https://docs.gitlab.com/ee/api/#graphql-api)) which should allow the same degree of querying.
In Verify, we are **`GraphQL` first** which means that we will develop new user facing features using `GraphQL` by default.
We will refactor older `REST` user facing features to support `GraphQL` wherever possible.
In some instances, it might make more sense to keep or even develop a new feature using `REST`.
For example, `REST` is better at handling files than `GraphQL` so it might be better to preserve this functionality in `REST`.
We allow each team to decide when they think they should go with `REST`, but eventually the goal is to have everything in `GraphQL`.

### Shared issues

In the Verify team we lean in to the GitLab mission, "[everyone can contribute](/handbook/company/mission/#mission)"!
To help balance this workload out across the groups, we use the [`Verify candidate`](https://gitlab.com/groups/gitlab-org/-/issues?label_name%5B%5D=Verify+candidate) label.
Every issue with this label is a good candidate to be worked on by any group in the Verify stage.
This applies to both frontend and backend issues.
Prioritization is still determined by the Product Manager, such as ensuring any deliverables in the engineer's own group still take priority, but engineers are encouraged to pick work up from [this board](https://gitlab.com/gitlab-org/gitlab/-/boards/1339417?scope=all&utf8=%E2%9C%93&state=opened&label_name[]=Verify%20candidate).
This helps us break down silos, balance the workload, and prevent disruptive re-allocations.

To help with prioritizing within the list of available `Verify candidate` issues, it's recommended to reference the issue types in the [Product Priorities](/handbook/product/product-processes/#prioritization) list, noting any severities applied on the issues as well.

### Shared technical debt

In the Verify stage, prioritizing our technical debt so that we can move faster is a top priority. Starting in August 2024, the Pipeline teams in the Verify stage have created a [board](https://gitlab.com/groups/gitlab-org/-/boards/1438885?not%5Blabel_name%5D%5B%5D=group%3A%3Ahosted%20runners&not%5Blabel_name%5D%5B%5D=group%3A%3Arunner&label_name%5B%5D=devops%3A%3Averify&label_name%5B%5D=type%3A%3Amaintenance) for Pipeline teams in the Verify stage that is intended to help us prioritize technical debt and bring alignment across team members of what is the most critical technical debt work to be focusing on. An engineer DRI from each team will work closely with their EM to align on which issues should be advocated for the most at a given time.

### Issue Health Status Definitions & Async Issue Updates

Across Verify we value [Transparency](/handbook/values/#transparency), we live our values of [Inclusion](/handbook/values/#bias-towards-asynchronous-communication), and we expect [Efficiency](/handbook/values/#write-things-down) by dogfooding using Issue Health Statuses and providing regular updates on active issues. Each team in the Verify Stage will define the cadence of updates and specific definition of the statuses, but generally the expectation is a weekly update on in progress issues with the following Health Statuses:

* On Track
* Needs Attention
* At Risk

These updates are an opportunity for the engineer to add detail to the status and are not expected to provide a justification for why something is behind or will miss a milestone. We encourage [blameless problem solving](/handbook/values/#blameless-problem-solving) and [kindness](/handbook/values/#kindness) at all times.

### Merge Requests in Verify

In the Verify stage, we value [MR Rate](/handbook/product/groups/product-analysis/engineering/metrics/#merge-request-rates-mr-rates) as a shared performance indicator for team collaboration, iteration, customer results. The entire team is responsible for iterative scope in issues. This starts with product management creating a clear problem statement connected to user insights. UX then adds interaction specifications and acceptance criteria to then be considered and weighed by the engineering team. Teams are encouraged to iterate on scope so as to delivery the [smallest thing possible](/handbook/values/#iteration).

By considering MR Rate as a measure of throughput, product management is focused on creating decomposed pieces of scope to improve the user experience. This encourages the UX and engineering teammates to provide simpler ways to solve the same problem, ultimately improving the throughput of the entire team.

Since April 2023, code changes to Verify code require approval from a Verify maintainer since Continuous Integration platform overall is a critical GitLab feature.
In order to [track quality of the approval process](https://gitlab.com/gitlab-org/gitlab/-/issues/411559)
we ask Verify maintainers to apply one of the following labels to a merge request changing Verify code:

* `~"verify-review::impacted"` for merge requests where the maintainer was able to identify near miss bugs, inefficiencies and tech debt.
* `~"verify-review::not impacted"` for merge requests where the change was trivial
or no issues were found by the Verify maintainer.

### Pipeline Authoring and Pipeline Execution Collaboration

Pipeline Authoring and Pipeline Execution are closely related but they also represent different stages in the cycle of a user's interaction with a pipeline. At a very high-level, this image illustrates the main focus of each group and how they can both support a better pipeline experience.

![Verify Groups](/images/product/groups/verify_groups_banner.jpg)

### Async Work Week

We have [quarterly async work weeks](https://gitlab.com/gitlab-org/verify-stage/-/issues/412) in Verify that start on the first Monday of the quarter.

Some of the noted benefits include reduced time spent in sync meetings, allowing for more focus that aligns with our async-first communication and our Diversity and Inclusion value to bias towards more async communication. However, this doesn't preclude us from having any meetings; it's up to the respective meeting attendees to decide accordingly. Exceptions might include: high priority issues and initiatives, social calls, coffee catch-ups. This also does not mean that you should not default to async-first at other times. Having regularly scheduled async weeks ensures that our processes do not become dependent on synchronous meetings.

## Verify Engineering - Async Updates

### Current (2022 onward)

As of June 2022, async issue updates are created weekly at the stage level and for each of the groups within the stage, following the [Ops section process of async updates](/handbook/engineering/devops/ops#async-updates-no-status-in-meetings).  Contributions will be added by Principal+ Engineers, Engineering Managers, and the Senior Engineering Manager of the Verify stage.

### 2020-2021

Every two weeks the Verify Engineering Update Newsletter is set out to an opt-in subscriber list. The purpose of the email is to share recent highlights from the Verify stage so folks will have a better idea of what is happening on other teams, and provide new opportunities for learning and collaboration.

Everyone is welcome to sign up or view previous issue on the newsletter page (link no longer available).

Each issue of the newsletter is planned using individual issues linked in the [newsletter epic](https://gitlab.com/groups/gitlab-com/-/epics/1148). Content is generally contributed by managers, but everyone is encouraged to contribute topics for the newsletter.

## Verify Technical Discussions

Verify Technical Discussions is a Zoom meeting hosted monthly by the team members in the Verify stage. Everyone is invited, however participation from the Verify stage members is especially encouraged.

During the meeting we discuss a variety of technical aspects related to the Verify stage roadmap. Folks are also encouraged to challenges they're facing working on problems in the CI domain.

Everyone can add their points to the [agenda document](https://docs.google.com/document/d/1SEydi30hYjqZ5ellZgwcijUesRnWjQVd___h3J9SSKY).

Below you can find a table with links to recordings of Verify Technical Discussions and Technical Deep Dives.

### Current Inventory of Recordings

The Verify Technical Discussions are automatically recorded and added to [Google Drive (internal)](https://drive.google.com/drive/folders/1Kk3RAfiOeHyny2OTSjGNVEjcO4Wb60oV).

### Uploaded Recordings to YouTube

| Date       | Title                                                          | Recording                                 |
|------------|----------------------------------------------------------------|-------------------------------------------|
| 2021-01-21 | Technical Discussions - Pipeline Editor and database storage   | [Recording](https://youtu.be/KsOR3lIz_4w) |
| 2021-01-07 | Technical Discussions - Next iteration of CI/CD Pipeline DAG   | [Recording](https://youtu.be/CvYEqSwd-UE) |
| 2020-12-10 | Technical Deep Dive - Observability at GitLab with demos       | [Recording](https://youtu.be/DVNyH3zQWBo) |
| 2020-11-19 | Technical Deep Dive - Cloud Native Build Logs feature overview | [Recording](https://youtu.be/Fq1ecmb_zk0) |
| 2020-05-08 | Technical Deep Dive - Using Prometheus with GitLab Compose Kit | [Recording](https://youtu.be/y9NW7A_XJrU) |

## Weekly Triage Reports

The Product Manager, Engineering Manager(s), and Designer for each group are responsible for triaging and scheduling [feature proposals and bugs as part of the Weekly Triage Report](/handbook/engineering/infrastructure/engineering-productivity/triage-operations/#group-level-bugs-features-and-deferred-ux). Product Managers schedule issues by assigning them to a Milestone or the Backlog.  For bug triage, Engineering Managers and Product Managers work together to ensure that the correct `severity` and `priority` labels have been applied.  Since [Product Managers are the DRIs for prioritization](/handbook/engineering/infrastructure/engineering-productivity/issue-triage/#priority), they will validate and/or apply the initial `priority` label to bugs.  Engineering Managers are responsible for adding or updating the `severity` labels for bugs listed in the triage report, and to help Product Management with understanding the criticality and technical feasibility of the bug, as needed.

While SLOs for resolving bugs are tied to severities, it is up to Product Management to set priorities for the group with an appropriate target resolution time. For example, criteria such as the volume of `severity::2` level bugs may make it appropriate for the Product Manager to adjust the priority accordingly to reflect the expected time to resolution.

### Availability, security, performance, and bug triage process

In the Verify Stage, we aim to solve new availability, security, performance issues within the SLO of the assigned severity. These types of issues are the top priority followed by bugs and technical debt according to our [severity SLO chart](/handbook/engineering/infrastructure/engineering-productivity/issue-triage/#severity-slos).

Availability and performance issues (commonly referred to as infradev) are also triaged in the [Infra/Dev Triage Board](https://gitlab.com/groups/gitlab-org/-/boards/1193197?label_name[]=gitlab.com&label_name[]=infradev).

## Supporting Community Contributions

We believe in supporting our open source community. We aim to support two main measure of success:

1. [Merged MRs from community contributions](https://gitlab.com/groups/gitlab-org/-/merge_requests?scope=all&utf8=%E2%9C%93&state=merged&label_name[]=Community%20contribution&label_name[]=devops%3A%3Averify)
1. [MRARR](/handbook/engineering/infrastructure/performance-indicators/#mrarr)

Each team in the Verify Stage follows roughly the same process to ensure the community is effectively supported and free to add features or fixes to the product. How we manage the Community Contribution MRs is spread across three main areas: processing the contributions, reviewing the contributions, and merging the contributions.

### Process

Code contributions to Verify typically occur in three flavors:

1. Free users, open source contributions from already scoped issues
1. Paid users, open source contributions not from scoped issues
1. Paid users, proprietary contributions not from scoped issues

Contributions from both free and paid users are equally important and will follow our [GitLab Contribution Guidelines](https://about.gitlab.com/community/contribute/). We strive to make this process as frictionless as possible between our users and the Engineering teams in Verify, especially during the reviewing of contributions.

### Reviewing contributions

Once a contribution has been created, the Engineering Manager assigns an engineer to manage and review with the Community Contributor. Reviewing contributions will follow the definition of done, style guidelines, and other practices of development. As the DRI of the review, the assigned Verify engineer will work with Community Contributor to resolve any outstanding items. The MR is then passed to a Maintainer with relevant domain expertise for final review prior to being merged.

#### Contributions from Partners

Our partners are an important part of our ecosystem at GitLab. These contributions should be reviewed with the same [GitLab Contribution Guidelines](https://about.gitlab.com/community/contribute/) as community MR contributions, and aligns with the [Verify contribution guidelines](https://docs.gitlab.com/ee/development/contributing/verify/) for working in the Verify areas of the codebase.

### Merging the Contribution

The Maintainer of the codebase will be the DRI of merging the contribution into the Verify product.

### SLOs for Community Contributions

For issues that are **refined**, they are considered priority for review and merging. Refined issues are defined as issues in `workflow::ready for development`, with `direction` labels, and either have technical proposals or are weighted. Issues that are not labeled with `workflow::ready for development` and `direction` labels are considered **non-refined** and are lower priority for review, and therefore have longer merge SLOs. SLOs for these two types of issues are defined in the table below:

| Types of issues & users  | Time Frame for Review SLO | Time frame for Merge SLO |
| --- | --- | --- |
| All users contributing to refined issues or bugs of severity S2 or S1  | 30 days | The next release (60 days) |
| Paying users from non-refined issues or bugs of severity S3 | 60 days | Within the next 3 releases (approx one quarter or 90 days) |
| Non-paying users from non-refined issues or bugs of severity S4 | 90 days | Anything outside the next 3 releases (more than one quarter or 120 days). |

In order to prevent the inflow of Community Contributions overwhelming engineers on the team and impacting their ability to work on planned issues, there is a WIP limit of 5 assigned Community Contribution MRs per reviewing engineer. This helps limit the amount of context switching a single engineer is doing and prevents them from being overwhelmed with reviews.

## Managing urgent priorities

In the event of escalations or high priority tasks that come up, we will adopt a [follow-the-sun rotation](https://www.lucidchart.com/blog/follow-the-sun-model) to ensure that the task is completed as quickly as possible. Examples of these urgent tasks include (but are not limited to): critical customer fixes, high severity security issues or corrective actions related to a high severity incident, with this level of urgency to be confirmed by the team's leadership (e.g. Engineering Manager and Product Manager). The follow-the-sun rotation requires an engineer to focus on that task within their working hours, then transitions to the next engineer once they come online, and engineers will arrange handoff of work to one another as needed (for example, when collaborating on an MR together as the contributor and reviewer, respectively).  This effort can also be a cross-stage effort, which involves collaboration amongst engineers across Verify stage groups.

As part of our GitLab values, we strive to be [inclusive to those in regions with fewer employees](/handbook/values/#inclusive-and-fair-policy-to-regions-with-fewer-employees). As a result, there is no expectation that people are expected to continuously work outside of their regular business hours. In the event we have limited people available in certain regions (such as APAC), we should look to escalate outside of the Verify stage to maintain focus on the escalated effort, by reaching out to engineers or other SMEs, and have managers help with this escalation path as needed.

## Common Links

### Slack Channels

* Verify [#s_verify](https://gitlab.slack.com/archives/C0SFP840G)
  * Verify:Pipeline Execution [#g_pipeline-execution](https://gitlab.slack.com/archives/CPCJ8CCCX)
  * Verify:Pipeline Authoring [#g_pipeline-authoring](https://gitlab.slack.com/archives/C019R5JD44E)
  * Verify:Runner [#g_runner](https://gitlab.slack.com/archives/CBQ76ND6W)
  * Verify:Pipeline Security [#g_pipeline-security](https://gitlab.slack.com/archives/CPANF553J)
* Verify Engineering Management [#s_verify-em](https://gitlab.slack.com/archives/C014UTH4W02)
* Verify Frontend Engineering [#s_verify_fe](https://gitlab.slack.com/archives/CUYH1MP0Q)
* CI/CD UX [#ux_ci-cd](https://gitlab.slack.com/archives/CL9STLJ06)
