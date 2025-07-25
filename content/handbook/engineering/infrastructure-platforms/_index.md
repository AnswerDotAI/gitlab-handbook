---
title: "Infrastructure Platforms"
description: "The Infrastructure Platforms department is responsible for the availability, reliability, performance, and scalability of GitLab SaaS Platforms and supporting services"
---

## Mission

As Infrastructure Platforms, our mission is to enable GitLab to deliver a single DevSecOps platform across SaaS and self-managed platforms by building highly available, reliable, performant, and scalable infrastructure solutions while maintaining the lowest total cost of ownership.

## Vision

Deliver the industry leading SaaS solutions, empowering organizations worldwide with the most innovative and efficient DevSecOps platform.

## Getting Assistance

If you're a GitLab team member and are looking to alert the Infrastructure Platforms teams about an availability issue with GitLab.com, please find quick instructions to report an incident here: [Reporting an Incident](/handbook/engineering/infrastructure/incident-management/#reporting-an-incident).

For all other queries, please see the [getting assistance](/handbook/engineering/infrastructure/getting-assistance/) page.

## Direction

Initiatives driven within the Platforms section, often spanning multiple quarters, are represented on the [SaaS Platforms section epic](https://gitlab.com/groups/gitlab-com/-/epics/2115) (GitLab team member).

{{% include "includes/we-are-also-product-development.md" %}}

## Organization structure

(click the boxes for more details)

```mermaid
flowchart LR
    I[Infrastructure Platforms]
    click I "/handbook/engineering/infrastructure-platforms/"

    I --> DA[Data Access]
    click DA "/handbook/engineering/infrastructure-platforms/data-access/"
    I --> DE[Developer Experience]
    click DE "/handbook/engineering/infrastructure-platforms/developer-experience/"

    I --> GD[GitLab Dedicated]
    click GD "/handbook/engineering/infrastructure/team/gitlab-dedicated/"
    I --> PRODENG[Production Engineering]
    click PRODEND "/handbook/engineering/infrastructure/team/production-engineering/"
    I --> SD[GitLab Delivery]
    click SD "/handbook/engineering/infrastructure-platforms/gitlab-delivery/"
    I --> TS[Tenant Scale]
    click TS "/handbook/engineering/infrastructure-platforms/tenant-scale/"

    DA --> DF[Database Framework]
    click DF "/handbook/engineering/infrastructure-platforms/data-access/database-framework/"
    DA --> DO[Database Operations]
    click DO "/handbook/engineering/infrastructure-platforms/data-access/database-operations/"
    DA --> Durability
    click Durability "/handbook/engineering/infrastructure-platforms/data-access/durability/"
    DA --> Git
    click Git "/handbook/engineering/infrastructure-platforms/data-access/git/"
    DA --> Gitaly
    click Gitaly "/handbook/engineering/infrastructure-platforms/data-access/gitaly/"

    PRODENG --> Ops
    click Ops "/handbook/engineering/infrastructure/team/ops/"
    PRODENG --> Foundations
    click Foundations "/handbook/engineering/infrastructure-platforms/production-engineering/foundations/"
    PRODENG --> Runners[Runners Platform]
    click Runners "/handbook/engineering/infrastructure-platforms/production-engineering/runners-platform/"
    PRODENG --> Observability
    click Observability "/handbook/engineering/infrastructure-platforms/production-engineering/observability/"
    PRODENG --> Runway
    click Runway "/handbook/engineering/infrastructure/team/runway/"
    PRODENG --> CC[Cloud Connector]
    click CC "/handbook/engineering/infrastructure/team/cloud-connector/"
    PRODENG --> FO[FinOps]
    click FO "/handbook/engineering/infrastructure/team/finops/"

    DE --> DevA[Development Analytics]
    click DevA "/handbook/engineering/infrastructure-platforms/developer-experience/development-analytics/"

    DE --> DT[Developer Tooling]
    click DT "/handbook/engineering/infrastructure-platforms/developer-experience/developer-tooling/"
    DE --> FR[Feature Readiness]
    click FR "/handbook/engineering/infrastructure-platforms/developer-experience/feature-readiness/"
    DE --> PER[Performance Enablement]
    click PER "/handbook/engineering/infrastructure-platforms/developer-experience/performance-enablement/"
    DE --> TG[Test Governance]
    click TG "/handbook/engineering/infrastructure-platforms/developer-experience/test-governance/"

    GD --> E[Environment Automation]
    click E "/handbook/engineering/infrastructure/team/gitlab-dedicated/environment-automation/"
    GD --> PSS[Public Sector Services]
    click PSS "/handbook/engineering/infrastructure/team/gitlab-dedicated/us-public-sector-services/"
    GD --> Switchboard
    click Switchboard "/handbook/engineering/infrastructure/team/gitlab-dedicated/switchboard/"

    SD --> B[Build]
    click B "/handbook/engineering/infrastructure-platforms/gitlab-delivery/distribution/"
    SD --> Framework
    click Framework "/handbook/engineering/infrastructure-platforms/gitlab-delivery/framework/"
    SD --> R[Release]
    click R "/handbook/engineering/infrastructure-platforms/gitlab-delivery/delivery/"
    SD --> D[Deploy]
    click D "/handbook/engineering/infrastructure-platforms/gitlab-delivery/delivery/"

    TS --> Organizations
    click Organizations "/handbook/engineering/infrastructure-platforms/tenant-scale/organizations/"
    TS --> CI[Cells Infrastructure]
    click CI "/handbook/engineering/infrastructure-platforms/tenant-scale/cells-infrastructure/"
    TS --> Geo
    click Geo "/handbook/engineering/infrastructure-platforms/tenant-scale/geo/"
```

## Dogfooding

The Infrastructure Platforms department uses GitLab and GitLab features extensively as the main tool for operating many [environments](/handbook/engineering/infrastructure/environments/), including GitLab.com.

We follow the same [dogfooding process](/handbook/engineering/development/principles/#dogfooding) as part of the Engineering function, while keeping the [department mission statement](#mission) as the primary prioritization driver. The prioritization process is aligned to [the Engineering function level prioritization process](/handbook/engineering/#prioritizing-technical-decisions) which defines where the priority of dogfooding lies with regards to other technical decisions the Infrastructure Platforms department makes.

When we consider building tools to help us operate GitLab.com, we follow the [`5x rule`](/handbook/product/product-processes/dogfooding-for-r-d/#dogfooding-process) to determine whether to build the tool as a feature in GitLab or outside of GitLab. To track Infrastructure's contributions back into the GitLab product, we tag those issues with the appropriate [Dogfooding](https://gitlab.com/groups/gitlab-org/-/labels?utf8=%E2%9C%93&subscribed=&search=dogfooding) label.

## Handbook use at the Infrastructure Platforms department

At GitLab, we have a [handbook first policy](/handbook/about/handbook-usage/#why-handbook-first). It is how we communicate process changes, and how we build up a single source of truth for work that is being delivered every day.

The [handbook usage page guide](/handbook/about/handbook-usage/) lists a number of general tips. Highlighting the ones that can be encountered most frequently in the Infrastructure Platforms department:

1. The wider community can benefit from training materials, architectural diagrams, technical documentation, and how-to documentation. A good place for this detailed information is in the related project documentation. A handbook page can contain a high level overview, and link to more in-depth information placed in the project documentation.
1. Think about the audience consuming the material in the handbook. A detailed run through of a GitLab.com operational runbook in the handbook might provide information that is not applicable to self-managed users, potentially causing confusion. Additionally, the handbook is not a go-to place for operational information, and grouping operational information together in a single place while explaining the general context with links as a reference will increase visibility.
1. Ensure that the handbook pages are easy to consume. Checklists, onboarding, repeatable tasks should be either automated or created in a form of template that can be linked from the handbook.
1. The handbook is the process. The handbook describes our principles, and our epics and issues are our principles put into practice.

## Projects

Classification of the Infrastructure Platforms department projects is described on the [infrastructure department projects page](/handbook/engineering/infrastructure-platforms/projects).

The [infrastructure issue tracker](https://gitlab.com/gitlab-com/gl-infra/production-engineering/-/issues) is the backlog and a catch-all project for the infrastructure teams and tracks the work our teams are doing–unrelated to an ongoing change or incident.

In addition to tracking the backlog, Infrastructure Platforms department projects are captured in our [Infrastructure Platforms department Epic](https://gitlab.com/groups/gitlab-com/-/epics/1049) as well as in our [Quarterly Objectives & Key Results](https://gitlab.com/groups/gitlab-com/-/epics/1420)

## Supporting Product Features

We have a model that we use to help us support product features. [This model](/handbook/engineering/infrastructure-platforms/feature-support/) provides details on how we collaborate to ship new features to Production.

## How we work

### Communication

#### Slack

Our main method of communication is Slack.

If you need assistance with a production issue or incident, please see the section on [getting assistance](/handbook/engineering/infrastructure/getting-assistance/).

**SaaS Platforms**

| **Channel** | **Purpose** |
|-----------|-----------|
| [#infrastructure_-_platforms](https://gitlab.slack.com/archives/C02D1HQRTKQ) | We collaborate on department level items here. This channel is used to share important information with the wider team, but also serves to align all teams in Platfroms with the common topic. |
| [#g_infrastructure_platforms_leads](https://gitlab.slack.com/archives/C010QV6RRB3) | Communication for managers. Everyone interested is welcome to join this channel if they find the topics interesting. |
| [confidential managers channel](https://gitlab.enterprise.slack.com/archives/C0808MLEXL1) | Used to discuss staffing issues affecting all teams that require additional coordination. We default to using the public channel as much as possible.|
| [#infrastructure_platforms_social](https://gitlab.enterprise.slack.com/archives/C062T669RFD) | Our social channel. |

**Dedicated**

| **Channel** | **Purpose** |
|-----------|-----------|
| [#g_dedicated-team](https://gitlab.enterprise.slack.com/archives/C025LECQY0M)| Dedicated Group discussion channel. Please use this channel for discussions relevant to engineers across the Dedicated group |
| [#f_gitlab_dedicated](https://gitlab.enterprise.slack.com/archives/C01S0QNSYJ2)| Dedicated function channel. Please use this channel to ask questions about features or ways of using the Dedicated product. Dedicated group will use this channel to make announcements relevant to wider groups |
| [#g_dedicated-us-pubsec](https://gitlab.enterprise.slack.com/archives/C03R5837WCV)| Dedicated USPubSec team channel. Used to discuss topics that affect PubSec team only. For broader engineering discussions please use [#g_dedicated-team](https://gitlab.enterprise.slack.com/archives/C025LECQY0M) |
| [#g_dedicated-switchboard-team](https://gitlab.enterprise.slack.com/archives/C04DG7DR1LG)| Dedicated Switchboard team channel. Used to discuss topics that affect Switchboard team only. For broader engineering discussions please use [#g_dedicated-team](https://gitlab.enterprise.slack.com/archives/C025LECQY0M)|
| [#g_dedicated-environment-automation-team](https://gitlab.enterprise.slack.com/archives/C074L0W77V0)|Dedicated Environment Automation team channel. Used to discuss topics that affect Switchboard team only. For broader engineering discussions please use [#g_dedicated-team](https://gitlab.enterprise.slack.com/archives/C025LECQY0M)|
| [#g_dedicated-team-social](https://gitlab.enterprise.slack.com/archives/C03QBGQ3K5W)| Dedicated social channel|
| [#dedicated-mr-review-stream](https://gitlab.enterprise.slack.com/archives/C065DDKPL21)| Visibility of new merge requests on Dedicated repos |

**Delivery**

| **Channel** | **Purpose** |
|-----------|-----------|
|[#g_delivery](https://gitlab.enterprise.slack.com/archives/CCFV016SV)| Delivery Group channel|
|[#g_delivery_standups](https://gitlab.enterprise.slack.com/archives/C05KS71438B)| |
|[#delivery_social](https://gitlab.enterprise.slack.com/archives/C01QX84J6UR)| Social channel for the group. |
|[#releases](https://gitlab.enterprise.slack.com/archives/C0XM5UU6B)| General communication about the current Release/Patch|
|[#f_upcoming_release](https://gitlab.enterprise.slack.com/archives/C0139MAV672)| Detailed Release status / Release Manager channel |
|[#announcements](https://gitlab.enterprise.slack.com/archives/C8PKBH3M5)|Release-Tools automation posts related to deployment activity|

**Production Engineering**

| **Channel** | **Purpose** |
|-----------|-----------|
| [#s_production_engineering](https://gitlab.enterprise.slack.com/archives/C07U6SAKS4D)| General conversation for Production Engineering teams and requests coming in from other team members. |
| [#g_production_engineering_leads](https://gitlab.enterprise.slack.com/archives/C06LDGA7Z9S)| Channel for Production Engineering leads (staff+ and management) |
| [#g_infra_ops](https://gitlab.enterprise.slack.com/archives/C04MH2L07JS)| Team channel for Production Engineering Ops  |
| [#g_infra_social](https://gitlab.enterprise.slack.com/archives/CQYDEJE13)| Social channel for Production Engineering |
| [#g_foundations](https://gitlab.enterprise.slack.com/archives/C0313V3L5T6)| Team channel for Production Engineering Foundations |
| [#g_foundations_social](https://gitlab.enterprise.slack.com/archives/C04QVEXBVL3)| Social channel for the Foundations team |
| [#g_foundations_alerts](https://gitlab.enterprise.slack.com/archives/C04Q7RQC7FF) | Non-urgent service alerts for Foundations owned services |
| [#g_foundations_notifications](https://gitlab.enterprise.slack.com/archives/C04RZC5TPPD) | Renovate notifications for Foundations owned projects |
| [#infra-terraform-alerts](https://gitlab.enterprise.slack.com/archives/C06PZQCRUJH) | Terraform state drift alerts for SaaS infrastructure |
| [#g_runners_platform](https://gitlab.slack.com/archives/g_runners_platform)| Team channel for Production Engineering Runners Platform |
| [#g_observability](https://gitlab.enterprise.slack.com/archives/C065RLJB8HK)| Team channel for general work in Observability. |
| [#g_runway](https://gitlab.enterprise.slack.com/archives/C07UED5CGR2)| Team channel for general work and discussion. |
| [#r_runway](https://gitlab.enterprise.slack.com/archives/C05G970PHSA)| External channel used for support, requestions, and help with Runway. |

**Tenant Scale**

| **Channel** | **Purpose** |
| ----------- | ----------- |
|[#s_tenant_scale](https://gitlab.enterprise.slack.com/archives/C07TWC3QX47) | General conversation for Tenant Scale and requests coming from other teams. |
|[#g_organizations](https://gitlab.enterprise.slack.com/archives/C01TQ838Y3T) | Discussions and requests specific to the Organizations team. |
|[#g_geo](https://gitlab.enterprise.slack.com/archives/C32LCGC1H) | Discussions and requests specific to the Geo team. |
|[#g_cells_infrastructure](https://gitlab.enterprise.slack.com/archives/C07URAK4J59) | Discussions and requests specific to the Cells Infrastructure team. |
|[#f_cells_and_organizations](https://gitlab.enterprise.slack.com/archives/C0609EXHX6F) | Channel for cross-functional discussion and coordination on Cells and Organizations. |

The SaaS Platforms group is gradually directing requests for help to the [#saas-platforms-help](https://gitlab.enterprise.slack.com/archives/C07DU5Z7V6V) Slack channel.
This channel can be used if it is unclear which Infrastructure team the question should be directed to.
For more information, refer to the [landing page for getting assistance](/handbook/engineering/infrastructure/getting-assistance/).

The [#saas-platforms-help](https://gitlab.enterprise.slack.com/archives/C07DU5Z7V6V) channel is monitored by SaaS Platforms Engineering Managers and Staff+ engineers who triage any inbound requests. When triaging this channel, one should locate the team who can best answer this question and instruct the requestor to contact that team using the team's preferred contact method. When the requestor is connected to the right team, add a green check emoji to the message. Finally, if needed, update the [getting assistance](/handbook/engineering/infrastructure/getting-assistance/) page with any changes.

#### Meetings

Once per week, we hold a `Platforms leads call` to align on action items related to career development, general direction or answer any ongoing questions that have not been addressed async. The call is cancelled when there are no topics added on the morning of the call.

In addition to the `Platforms leads call`, we have some recurring events and reminders that can be viewed in the [SaaS Platforms Leadership Calendar](https://calendar.google.com/calendar/embed?src=c_8a81f7acc76d72b8e4189a61f7a259b9d722e3fe1e05693236f592e7dd52e83b%40group.calendar.google.com). Please add this to your Calendars to stay up-to-date with the various events.

Sr. Director of Infrastructure Marin Jankovski, likes to meet with new team members that join the organization. Marin sets up informal 1:1 coffee chats a few times a month with newer team members to get to know one another and see how they are doing. This process is organized by his EBA who will reach out to team members once he has the availability to meet. As this is a large team, it may take a while to get through everyone.
If someone needs to meet with Marin sooner than when the coffee chat is scheduled, you can reach out to his EBA Liki Simonot to set something up.

##### Grand Review

The Engineering Leads for each Stage, along with their Product Managers, hold weekly progress reviews to assess their groups’ progress, share project updates, resolve blockers, and celebrate wins. Additionally, the Director of Product and the Senior Director of Infrastructure Platforms conduct a higher-level leadership review, where they go over summaries from these group-level meetings.

**Weekly Schedule**

- Wednesday: each Epic DRI updates the status section of their epics with the progress. It is important to surface:
  - risks and blockers impacting the project
  - projects that are completed, including a closing summary highlight. These epics will be closed during the Grand Reviews
- Thursday: Group Level Reviews conducted and added as threads in [Infrastructure Platforms Top Level epic](https://gitlab.com/groups/gitlab-com/-/epics/2115) (see [example](https://gitlab.com/groups/gitlab-com/-/epics/2115#note_2197983622))
  - Data Access: run by the Data Access Acting Sr. EM and the Group PM
  - Tenant Scale: run by the Tenant Scale Sr. EM and Group PM
  - Production Engineering: run by the Production Engineering Sr. EM and Group PM
  - Software Delivery: run by the Software Delivery Acting Sr. EM and Group PM
  - Developer Experience: run by the Developer Experience Director and a rotation of Product Managers
  - Dedicated: run by the Dedicated Sr. EM and a rotation of of Product Managers
- Friday: Leadership Review, run by the Sr. Director of Infrastructure Platforms and the Director of Product Infrastructure Platforms. Review the group-level summaries added as threads in the [Infrastructure Platforms Top Level epic](https://gitlab.com/groups/gitlab-com/-/epics/2115), then conduct a deep dive into one specific group to ensure comprehensive project coverage.
- Friday: Group level and the leadership level reviews are released together in #infrastructure_platforms

The review is private streamed to the GitLab Unfiltered channel because the review covers confidential issues. All recordings are made available in the [Platforms Grand Review YouTube Playlist](https://www.youtube.com/playlist?list=PL05JrBw4t0KqDXSHdlUvPWHOj_Hw8JdQ1)

##### Infrastructure Platforms Leads Demo

The Infrastructure Platforms Leads Demo is an opportunity for sync discussions between Staff+ IC across the Infrastructure Platforms Group to highlight current ongoing efforts underway in the teams they support.
All team members are welcome to join the call, but the emphasis is on Staff+ ICs to present and discuss the work they're focused on, the problems they're experiencing, and solutions they're considering.

The call is recorded to the [Infrastructure Platforms Leads Demo Unfiltered Playlist](https://www.youtube.com/playlist?list=PL05JrBw4t0KpI98ZtrhYrA_gJgYJjnOgl). The agenda can be found in [Google Docs](https://docs.google.com/document/d/1MX__hMUcxEUv2JlRiXySNvFnOPHv7-Uul1_VbzImbKw/edit).

While the intention is for the call to be made public on GitLab Unfiltered, the default is for it to be published as private.
At the end of the call, a quick vote is held between the attendees and if all agree that the content is #SAFE, it can be published as public.

### Requests for Help

On the [landing page for getting assistance](/handbook/engineering/infrastructure/getting-assistance/), we ask team-members who need assistance to raise Requests for Help using standard templates.

These issues are raised in the [request for help issue tracker](https://gitlab.com/gitlab-com/saas-platforms/saas-platforms-request-for-help/-/issues) and are automatically assigned to the Engineering Manager of the relevant SaaS Platforms team.

The Engineering Manager is expected to:

1. Confirm that the question is not a duplicate and that the answer to the question is not already discoverable in the handbook or the tracker itself.
2. Confirm the urgency of the request.
3. Respond to the help request or assign to an engineer to help with the request.

### Slack to GitLab Issue Tracker Integration

In an effort to enhance the tracking and resolution of requests directed to the Infrastructure team, we are evaluating a bot that converts Slack messages in [#infrastructure_lounge](https://gitlab.slack.com/archives/CB3LSMEJV) channel into GitLab issues.

#### Workflow Overview

- **Acknowledgement**: An agent responds with the `acknowledged_emoji` (👀 in our case) to acknowledge a Slack message in the Infrastructure Lounge channel.
- **Issue Creation**: The Slack bot then creates an issue with the acknowledging agent assigned to it.
- **Thread Attachment**: The Slack thread corresponding to the message is also posted on the created GitLab issue.
- **Label Assignment**: Agents can further categorize issues by adding label emojis (`ops`, `foundations`, `observability`) in the Slack message. This action automatically assigns the issue to the respective team: Ops, Foundations, Observability.
- **Project Tracking**: These converted issues are tracked under a dedicated project hosted at [Infrastructure Lounge Slack Issue Tracker](https://gitlab.com/gitlab-com/gl-infra/infrastructure-lounge-slack-issue-tracker).
- **Issue Closure**: Agents/Requester can close the issue when resolved by adding any of the `resolved_emojis` (`green-circle-check`,`white_check_mark`or `checked`in our case)

#### Configuration

Agents responsible for handling these issues are defined in a JSON file, which serves as a [CI/CD variable](https://ops.gitlab.net/gitlab-com/gl-infra/infrastructure-lounge-slack-issue-creator/-/settings/ci_cd). Currently, this file contains a static list of all members of the infrastructure department.

### Project and Backlog Management

We use epics and issues to manage our work. [Our project management process](/handbook/engineering/infrastructure/platforms/project-management/) is shared between all teams in SaaS Plaforms.

### Tools

The Platforms section builds and maintains various tools to help deploy, operate and monitor our SaaS platforms. You can view a list of these tools in the [Platforms Tools Index](/handbook/engineering/infrastructure/platforms/tools/).

### OKR

We use objective and key results to set goals in alignment with [OKRs at GitLab](/handbook/company/okrs/).
[Our OKR process](/handbook/engineering/infrastructure/platforms/okrs/) is shared between all teams in Saas Platforms.

### Hiring and Interviewing

[Our hiring process](/handbook/engineering/infrastructure/platforms/hiring/) is shared between all teams in Infrastructure Plaforms.

This [Infrastructure Platforms Interviewing Guide](/handbook/hiring/interviewing/infrastructure-interview/) offers more detail on some of our regular openings, interview process and other useful information related to applying to jobs with us. More information on our current openings can be found on the [careers page](https://about.gitlab.com/jobs/).

## Platforms Learning Path

All team members are encouraged to schedule time for personal development. The following links may help you get started with Platforms-relevant learning. Please add your own contributions to this list to help others with their personal development.

### Learn about Infrastructure Platforms, and its groups

| Group | Topic |
|-------|-------|
| SaaS Platforms | [Product direction](https://about.gitlab.com/direction/saas-platforms/) |
| Delivery Group | [Delivery Group](/handbook/engineering/infrastructure-platforms/gitlab-delivery/delivery/) |
| Production Engineering Group| [Production Engineering](/handbook/engineering/infrastructure-platforms/production-engineering/) |
| Dedicated Group | [Dedicated Group](/handbook/engineering/infrastructure/team/gitlab-dedicated/) |
| Tenant Scale | [Group Page](/handbook/engineering/infrastructure-platforms/tenant-scale/) |

### Learn about tools and technologies used within Platforms

1. [Jsonnet tutorial](https://jsonnet.org/learning/tutorial.html)

## Common Links

- [How we do Incident Management for GitLab.com](/handbook/engineering/infrastructure/incident-management/)
- [GitLab.com status information](https://status.gitlab.com)

### Other Slack Channels

- [#production](https://gitlab.slack.com/archives/production)
- [#infrastructure-lounge](https://gitlab.slack.com/archives/infrastructure-lounge)
- [#incidents](https://gitlab.slack.com/archives/incidents)
- [#announcements](https://gitlab.slack.com/archives/announcements)
- [#feed_alerts-general](https://gitlab.slack.com/archives/feed_alerts-general)

### General Issue Trackers

- [Production Engineering issue queue](https://gitlab.com/gitlab-com/gl-infra/production-engineering/-/issues)
- [Production incidents, and changes](https://gitlab.com/gitlab-com/gl-infra/production/issues/)
- [Delivery](https://gitlab.com/gitlab-com/gl-infra/delivery/issues/)
- [Observability](https://gitlab.com/gitlab-com/gl-infra/observability/team/-/issues/)
- [Tenant Scale](https://gitlab.com/gitlab-com/gl-infra/tenant-scale/)
- [Runway](https://gitlab.com/groups/gitlab-com/gl-infra/platform/runway/-/issues)

### Resources

- [Production Architecture](/handbook/engineering/infrastructure/production/architecture/)
- [Operational Runbooks](https://gitlab.com/gitlab-com/runbooks)
- [Environments](/handbook/engineering/infrastructure/environments/)
- [Monitoring](/handbook/engineering/monitoring/)
- [Readiness Reviews](/handbook/engineering/infrastructure/production/readiness/)
- [Infrastructure Platforms Standards](/handbook/company/infrastructure-standards/)
- [Career development and Internships in Infrastructure Platforms](/handbook/engineering/infrastructure-platforms/careers)

## Other Pages

- [On-call Handover](/handbook/engineering/infrastructure-platforms/production-engineering/ops/on-call-handover/)
- [SRE Onboarding](/handbook/engineering/infrastructure-platforms/production-engineering/ops/sre-onboarding/)
- [GitLab.com data breach notification policy](https://about.gitlab.com/security/#data-breach-notification-policy)
- [Coding at scale](/handbook/engineering/infrastructure/team/scalability/#regarding-coding-at-scale)
