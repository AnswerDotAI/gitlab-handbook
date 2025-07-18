---
title: "GitLab Dedicated Group"
---

![GitLab Dedicated Group logo](/images/engineering/infrastructure/team/gitlab-dedicated/dedicated_team_logo.png)

## Mission

The GitLab Dedicated team's mission is to create a fully managed, single-tenant GitLab environment, served through a GitLab Dedicated platform. It is developed to remove any manual interactions with customer tenant installations, and to ensure that the customer tenants are fully focused on unlocking the power of The One DevOps Platform.

## Vision

The GitLab Dedicated group is a customer facing team, with team members focused on a high level of infrastructure automation, and enabling customer interactions with the GitLab Dedicated platform.

Team mission is to:

- Develop a 100% automated system for provisioning a large number of single tenant GitLab sites
- Automate maintenance tasks without human interaction for the said sites
- Create and manage central observability stack, as well as observability stack per customer tenant
- Create customer portal (Switchboard), exposing administrative operations to customer tenants

## GitLab Dedicated Architecture

For GitLab Dedicated Architecture documentation please refer to the [Architecture Page](architecture/index.html)

## Performance Indicators

Team performance indicators are not fully defined. We are going to consider a **Provisioning SLO** to start with, possibly followed by [DORA 4 metrics](https://cloud.google.com/blog/products/devops-sre/using-the-four-keys-to-measure-your-devops-performance).

## Team Members

Engineering team members of GitLab Dedicated are publicly referenced with specialty for `Environment Automation`, `Switchboard` or `US Public Sector Services` team, based on their primary task.

The following people are members of the Dedicated:Environment Automation Team:

{{< team-by-manager-slug "o-lluch" >}}

{{< team-by-manager-slug "denhams" >}}

The following people are members of the Dedicated:US Public Sector Services Team:

{{< team-by-manager-slug "mckgl" >}}

The following people are members of the Dedicated:Switchboard Team:

{{< team-by-manager-slug "ashiel" >}}

## Working with us

To engage with the GitLab Dedicated teams:

- [Create an issue](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/team/-/issues/new) in the GitLab Dedicated team issue tracker
  - For feature requests, use the [feature requests issue template](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/team/-/blob/main/.gitlab/issue_templates/feature_request.md) and fill in the required information
- When creating an issue, it is not necessary to `@`mention anyone
- In case you want to get attention, use a specific team handle as defined in [group hierarchy below](#gitlab-group-hierarchy)
- Slack channels
  - For GitLab Dedicated specific questions, you can find us in [#f_gitlab_dedicated](https://gitlab.slack.com/archives/C01S0QNSYJ2)
  - The Dedicated Group internally leverages: [#g_dedicated-team](https://gitlab.slack.com/archives/C025LECQY0M)
  - Engineering teams within Dedicated have their own work channels for team work discussions:
    - [#g_dedicated-environment-automation-team](https://gitlab.enterprise.slack.com/archives/C074L0W77V0)
    - [#g_dedicated-switchboard-team](https://gitlab.slack.com/archives/C04DG7DR1LG)
    - [#g_dedicated-us-pubsec](https://gitlab.slack.com/archives/C03R5837WCV)
  - Our social channel, [#g_dedicated-team-social](https://gitlab.slack.com/archives/C03QBGQ3K5W) is accessible to everyone who wants to casually interact with the team

### Urgent Availability or Security Events

In the case of a [Sev-1 or Sev-2 Incident](/handbook/engineering/infrastructure/incident-management/#severities), please *Page* the GitLab Dedicated Engineer On Call. Further guidance on when to use this can be found [here](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/team/-/blob/main/runbooks/on-call.md#what-is-an-emergency).

#### Dedicated for Commercial

1. From any Slack channel, use `/inc escalate`:
   1. Under `On-Call Teams` select `dedicated EOC`
   1. Provide information on the report in the `Notification Message`
   1. *Urgency*, *Priority* and *Assign To* should not be set

#### Dedicated for Government

1. From any Slack channel, use `/pd trigger`:
   1. Impacted Service: `Dedicated US Public Sector Platform Service`
   1. Title: `GitLab Dedicated`
   1. Description: Provide information on the report, and how you can be contacted
   1. *Urgency*, *Priority* and *Assign To* should not be set

### Escalation Policy

When it comes to escalating customer support issues, we follow the same definitions of severity as [provided by support](https://about.gitlab.com/support/definitions/#definitions-of-support-impact) since Dedicated customers receive priority support. Only in cases where there is an [availability or security sev-1](/handbook/engineering/infrastructure/engineering-productivity/issue-triage/#severity) event it can be escalated to Sev-1 at the Support level. 'Business as usual' configuration changes cannot be escalated to sev-1. In sev-1 cases we will involve our on-call, as these incidents may affect our Availability SLA commitments to the customer. Sev-2 and below will be handled by the team during normal business hours. Any fixes identified as part of a support ticket that must go out immediately will be considered "emergency maintenance" and can be done outside the normal maintenance window. All other fixes will be done during the next available maintenance window.

### Handling Configuration Changes for Tenant Environments

Customers require the ability to customize the configuration of their Dedicated instance before they are able to use it in a production setting.
These customizations involve configuration changes to [functionality already supported in Dedicated](https://docs.gitlab.com/ee/subscriptions/gitlab_dedicated/#available-features) including infra-level settings like IP Allowlists and Cloud-Specific Private Networking configuration as well as GitLab application settings that cannot currently be self-served through the admin UI like SAML configuration changes.

To request functionality that is not currently supported within Dedicated, customers must open a feature request using the [feature request issue template](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/team/-/blob/main/.gitlab/issue_templates/feature_request.md). To request functionality for the broader GitLab Application, customers can use the [feature proposal](https://gitlab.com/gitlab-org/gitlab/-/blob/master/.gitlab/issue_templates/Feature%20Proposal%20-%20lean.md) template.

While in the long term, customer admins will be able to self-serve configuration changes using the Switchboard customer portal. In the short term, SREs will need to make the change and deploy it to the customer's environment. This process is documented below.

- During Onboarding (before instance handover)
  - We will make one SRE available to support a new customer as they are onboarding to the platform. The SRE will be available one week prior to the onboarding date (that is, the `start date` specified in the customer contract) and make any needed configuration changes to the environment.
  - To request a configuration change during onboarding, customers can open a new issue in their shared collaboration project. The PM will take the customer request, create an issue within the Dedicated team project, assign the labels per project workflow, and `@` mention the SRE in question. The SRE will assign the issue to themselves and perform the change.
  - Note, config changes during onboarding cannot be escalated to the Dedicated team as this is still before the contractual start date. See below for more information on our [escalation policy](#escalation-policy).
- Post-instance handover
  - Any configuration changes needed after the `start date` will be batched and handled in the next available weekly maintenance window. The cut off to get changes in is 2 business days before the maintenance window begins.
  - We cannot make any guarantees that a config change will make it into a specific maintenance window. In cases where there is a large amount of work that may stretch beyond the 4 hour maintenance window, configuration changes may be pushed out to the following window. In such cases, this will be communicated on the request issue.
  - To request a configuration change after the initial onboarding, customers must create a support ticket. The assigned support engineer will then open a new issue in the Dedicated issue tracker with the request. The requester must ensure there is link to the ZD ticket in the internal issue for change control purposes. The SRE tasked with performing the next round of maintenance for this customer will reply on the issue with a rough ETA and again once the change has been deployed. If this is a change that requires development work, the SRE will raise to PM/EM.
  - Post-onboarding, escalating a config change requests is only possible for configuration that ensures that the tenant instance is online. "Business as usual" changes can only be scheduled well in advance using the customer Project Plan provided during onboarding. See more details about our escalation policy below.

#### Production Change Lock (PCL)

While changes we make are rigorously tested and carefully deployed,
it is a good practice to temporarily halt production changes during certain events such as GitLab Summit,
major global holidays,
and other times where GitLab Team Member availability is substantially reduced.

Risks of making a production environment change during these periods includes immediate customer impact and/or reduced engineering team availability in case an incident occurs.
Therefore, we have introduced a mechanism called Production Change Lock (PCL) to GitLab Dedicated.

The GitLab Dedicated Production Change Lock is greatly inspired by the [PCL](/handbook/engineering/infrastructure-platforms/change-management/#production-change-lock-pcl) for GitLab.com,
but there are some differences worth noting.

A PCL is manually enforced once the following requirements are met:

1. A PCL [issue](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/team/-/issues/3946) describing the PCL period is created.
2. An MR updating the scheduled PCLs table is approved by the Infrastructure Platforms Engineering Director
3. Customer changes using Switchboard are prevented for the duration of the PCL.

The following dates are currently scheduled PCLs.

| Dates                                        | Type   | Reason                                            |
|----------------------------------------------|--------|---------------------------------------------------|
| 2024-12-23 03:00 UTC -> 2025-01-06 03:00 UTC | Hard   | Year End Holidays (Low team member availability)  |

Times for the dates without a time specified begin at 09:00 UTC and end the next day at 09:00 UTC.

As opposed to GitLab.com [PCL](/handbook/engineering/infrastructure-platforms/change-management/#production-change-lock-pcl), for GitLab Dedicated we only consider a Hard PCL type.

##### Hard PCL

Hard PCLs include:

- customer changes using Switchboard
- all code deploys and infrastructure changes
- including automated maintenance in UAT, PreProd and Production environments

New customers will not be onboarded during Hard PCLs.

In case of an active S1/S2 incident, it is at the EOC (Engineer on Call) discretion to make the decision to apply the changes necessary to mitigate or resolve the incident in order to keep service availability.
Any action during an incident while in a PCL must be associated to an issue and the EOC should inform the GitLab Dedicated engineering Leadership about the action taken.

Changes not associated to any incident must have an exemption approval by the GitLab Dedicated engineering Leadership.

### Requesting access to logs

GitLab Dedicated comes with strict [access controls for tenant environments](https://docs.gitlab.com/ee/subscriptions/gitlab_dedicated/#access-controls).
By default, GitLab Dedicated logs are only accessible by members of the GitLab
Dedicated and Support Engineering teams. In cases where GitLab Dedicated
customers are impacted by issues that require additional team members to review
logs, access can be granted on a case-by-case basis. Examples include, but are
not limited to: Backend Engineers or Security Engineers in other departments.

Access will only be provided to:

1. Individual team members
1. For a defined period of time (default: 2 work weeks)
1. All access requests require approval by the Dedicated Team Engineering Manager or Director and the direct manager of the requesting team member
1. Extensions will need to be approved by the Dedicated Team Engineering Manager or Director and the direct manager of the requesting team member

To gain access, please create:

1. [access request](https://gitlab.com/gitlab-com/team-member-epics/access-requests/-/issues/new?issuable_template=Individual_Bulk_Access_Request). Use `GitLab Dedicated Logs (Production)` as the system.
1. An issue in the [GitLab Dedicated tracker](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/team/-/issues/new?issuable_template=log_access_rotation) using the `Log rotation access` template.

## Working across GitLab

### Communicating with GitLab Dedicated customers

If you need to urgently contact one or more GitLab Dedicated customers, engage the
[GitLab Dedicated Communications Manager On-Call (CMOC)](/handbook/support/workflows/dedicated_cmoc/).

Non-urgent communication should be handled through the customer's Customer Success Manager (CSM).

### Getting product fixes into GitLab Dedicated quicker

{{% alert title="Note" color="info" %}}

This section should be moved into the GitLab Dedicated incident management process page when it
becomes available.
{{% /alert %}}

Sometimes, a product fix is introduced to resolve a GitLab Dedicated incident or
[customer escalation](#escalation-policy). There can be a significant delay between when the
product fix is merged and when it is deployed to GitLab Dedicated environments due to our
[upgrade policy](https://docs.gitlab.com/ee/subscriptions/gitlab_dedicated/#upgrades).

In such cases, we should evaluate the impact of the delay and, if justified, use the
[backport request process](/handbook/engineering/releases/backports/) to request that the product
fix be backported to a GitLab version that can be deployed to GitLab Dedicated environments in an
acceptable time frame.

## How we work

GitLab Dedicated is highly visible within GitLab and the broader market. It is also complex service offering. Consequently, the Dedicated team needs to manage its own work and stakeholder expectations - both external and internal. The following sections describe processes and tools that the team has adopted to work efficiently and effectively.

These processes matter because they provide a clear way to understand the state of the product and ongoing work as well as enable team members to fulfill their role.

A main goal in designing these processes is to make it possible for every team member working on any part of GitLab Dedicated to understand **why** their work matters and how it contributes to customer results.

It is critical that the following processes are understood by all team members and that we hold ourselves accountable.

### Meetings and Scheduled Calls

Our preference is to work asynchronously, within our project issue tracker as described in [the project management section](#project-management).

The team does have a set of regular synchronous calls:

- `Demo call` - This call is scheduled every two weeks, rotating across timezones. During this call, team members show off their progress, and engage with other team members on topics related to GitLab Dedicated platform. Demo calls are supposed to be rough around the edges and unpolished. In fact, if the demo looks polished, we will discuss whether we are being ambitious enough with our goals
- Teams within Dedicated may have their own `Team Sync`
- 1-1s between the Individual Contributors and Engineering Managers

The group has a set of regular synchronous calls for PMs and EMs to ensure alignment:

- `GitLab Dedicated Product <> Eng Sync` - This call is weekly on Mondays and Thursdays for PMs and EMs to align
- `Dedicated Managers Sync` - This call is every two weeks for Dedicated EMs to sync and ensure alignment

It is the organizer's responsibility to ensure these calls can be recorded regardless of whether the organizer is present by [enabling "Alternative Hosts" in Zoom](/handbook/tools-and-tips/zoom/#how-to-allow-recording-when-the-host-is-not-present).

Impromptu Zoom meetings for discussing GitLab Dedicated work between individuals are created as needed.
It is expected that these meetings are private streamed, or recorded(1*), and then uploaded to [GitLab Unfiltered playlist](https://www.youtube.com/playlist?list=PL05JrBw4t0KqC5FfUVPyndvLvTWifWbfB).
The outcome of the call is shared in a persistent location (Slack is not persistent). This is especially important as the team grows, because any decisions that are made in the early stage have will be questioned in the later stages when the team is larger.

`1*` Exceptions to the recording rule are: 1-1 calls, discussions around non-project work, and in cases where parties do not feel comfortable with recording. However, even with the exceptions, outcome of project related discussions need to be logged in a persistent location, such as the main issue tracker.

### Protecting Customer Identity

GitLab [confidentiality levels](/handbook/communication/confidentiality-levels/) require that we do not publicly identify customers without their express permission.

When it is necessary to refer to a specific customer we use the following guidelines:

| Use Case                               | Example                                                                    | Process                                                                                                                                                                                                                                                                                                                                                                     |
|----------------------------------------|----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Internal Communication & Collaboration | Slack conversations, RFH (Request for Help) issues | <ul><li>Use the customer name</li></ul> |
| Public Collaboration | Collaboration on issues, including SIRT issues, epics and recorded calls   | <ul><li>Avoid using the customer name publicly. Instead use internal notes, or provide an accessible internal link to aid the identification - remember that not everyone has access to Switchboard</li><li>If a customer name is mentioned on a recorded call the video should be set to Private and the reason included in the YouTube description</li></ul> |
| Implementation Level                   | We need the ability to map a codename to a tenant_id within the tech stack | <ul><li>Use internal codenames for this use case.</li><li> Switchboard is the SSOT for internal codenames. </ul></li>                                                                                                                                                                                                                                                     |

### GitLab Group Hierarchy

We use [GitLab Groups](https://docs.gitlab.com/ee/user/group/#groups) to logically organize team-members working on GitLab Dedicated projects.
The groups cover the following use-cases:

1. GitLab Dedicated group membership: `@gitlab-dedicated`
    - All permanent team-members in any of the GitLab Dedicated teams gain access to this GitLab group as part of onboarding
    - Group mention should only be used in circumstances where the information shared is pertinent for all team members of the GitLab Dedicated group
1. Individual team group membership: `@gitlab-dedicated/environment-automation`, `@gitlab-dedicated/switchboard`, `@gitlab-dedicated/uspubsec`, etc.
    - All permanent team-members of individual teams gain access to their respective GitLab group as part of onboarding
    - Group mention should be used when the information shared is pertinent to the respective team
1. Individual team GitLab Dedicated groups have two additional subgroups `maintainers` and `reviewers`, for example: `@gitlab-dedicated/switchboard/maintainers`
    - `reviewers` GitLab group access is granted to permanent team-members, external contractors, team-members on borrow, and similar. This GitLab group type is used to distinguish users without merge rights. Initial reviews should be requested from this group, using the quick action, for example `/assign_reviewer @gitlab-dedicated/switchboard/reviewers`
    - `maintainers` GitLab group is granted to permanent team-members only. This group has merge rights, and the group is granted access through [CODEOWNERS approval rules](https://docs.gitlab.com/ee/user/project/codeowners/#code-owners). Team members onboard into the `maintainer` subgroup after meeting the requirements defined in the [Dedicated Maintainer Training](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/team/-/blob/main/.gitlab/issue_templates/maintainer_training.md)(internal only)

### Project Management

We use epics, issues, and issue/epic boards to organize our work, as they complement each other.

Please see:

1. [Infrastructure Platforms Project Management](/handbook/engineering/infrastructure/platforms/project-management)
1. [Infrastructure Platforms Epic](https://gitlab.com/groups/gitlab-com/-/epics/2115)
1. [Environment Automation Epic](https://gitlab.com/groups/gitlab-com/gl-infra/-/epics/479)
1. [Switchboard Epic (scoped to current quarter)](https://gitlab.com/groups/gitlab-com/gl-infra/gitlab-dedicated/-/epics/405)
1. [US Public Sector Epic](https://gitlab.com/groups/gitlab-com/gl-infra/-/epics/876)

#### Epic Hierarchy

We use sub-epics to break larger epics into smaller portions.

1. Sub-epics group tasks required to deliver an item mentioned
1. Sub-epics represent an item from the roadmap and are delivered in a specific phase
1. Sub-epics can span multiple months, but their end date should match the 'anticipated completion date' of the roadmap phase they are added to.

The diagram below shows an example of traversing the complete hierarchy:

```mermaid
graph TD
A(GitLab Dedicated)
A --> D([Epic])
A --> E([Dedicated Runners on AWS - Beta])
A --> G([...])
D --> H([Sub-epic])
E --> I([Dedicated Runners - Operational requirements])
E --> J([Dedicated Runners - Go-live preparations])
E --> K([...])
H --> L([Issue 1])

click A "https://gitlab.com/groups/gitlab-com/gl-infra/-/epics/479"
click E "https://gitlab.com/groups/gitlab-com/gl-infra/gitlab-dedicated/-/epics/276"
click I "https://gitlab.com/groups/gitlab-com/gl-infra/gitlab-dedicated/-/epics/297"
click J "https://gitlab.com/groups/gitlab-com/gl-infra/gitlab-dedicated/-/epics/298"
```

*Note* If you are not seeing the diagram, make sure that you have accepted all cookies.

#### Epic Owners

Each epic has a single DRI who is responsible for delivering the project. DRIs for each epic are listed at the top of the description of each epic per Epic Structure. Epic DRI responsibilities are in [https://handbook.gitlab.com/handbook/engineering/infrastructure/team/gitlab-dedicated/#epic-owner-responsibilities](/handbook/engineering/infrastructure/team/gitlab-dedicated/#epic-ownership)

1. Engineering epic DRIs can be found within children epics of [GitLab Dedicated epic](https://gitlab.com/groups/gitlab-com/gl-infra/-/epics/479).

#### Epic Owner Responsibilities

The DRI needs to:

1. Work with others to move issues through the boards
1. Ensure epic meets criteria outlined in [Epic Structure](/handbook/engineering/infrastructure/team/gitlab-dedicated/#epic-structure)
1. Provide updates on DRI's epic in epic description according to process outlined in [Status Update Process](/handbook/engineering/infrastructure/team/gitlab-dedicated/#Status-Update-Process) below.

Throughout the project, the DRI should continue to adjust the epic description and structure to keep it current with the project status.

#### Epic structure

Each epic and child sub-epics must include the following:

**Description** (TBD make epic template)

1. **DRI** who is responsible for this epic.
1. **Background**, including a problem statement, to provide context for people looking to understand the epic.
1. **Exit criteria** for the specific goals of the epic.
1. **Status yyyy-mm-dd** should be the final heading in the description.
    1. This enables others who are interested in the epic to see the latest status without having to read through all comments or issues attached to the epic.
    1. This heading is used to auto-generate the status information on the top-level epic.

**Epic meta data**

1. **Start date** is set to the expected start date, and updated to be the actual start date when the project begins.
1. **Due date** is set to be the expected end date.
    1. The date that a project actually ended is taken from the date that the epic was closed.

Labels are described in the [epic label section](#epics-labels).

#### Epic boards

Epic boards are used to track the overall status of epics. DRI's are encouraged to created any project labels needed to allow a suitable project board to be created.

#### Planning feature rollouts

All significant changes must have a [rollout issue using the rollout_coordination template](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/team/-/issues/new?issuable_template=rollout_coordination). This issue should be used to review test coverage, rollout timings as well as plan customer communication where needed.

#### Project Stages

The project is generally following these stages:

- Beta
- Limited Availability
- General Availability (GA)
- Post-GA

#### Issues

Dedicated team projects use an agile-like methodology.

1. Team members should start Issues that are marked as ~"workflow-infra::Ready".
1. GitLab is an asynchronous working environment, and as such, code change reviews may take time as reviewers are in other timezones. Team members are encouraged to review pending code reviews and then possibly start on a second task even if a task is not fully completed -- but only if they feel they have capacity. For example, during a review process awaiting final approval, team members could pick up another task to start working on. Regular Agile synchronous ceremonies (stand ups, retros, etc) are not done, but there will be occasional short 'team sync' calls in a week and activities like live troubleshooting or pairing are not forbidden.
1. When starting a new task:
    - Assign yourself to the issue and apply the label ~"workflow-infra::In Progress".
    - Start off by collecting additional information that you may need, and ask questions on the issue to clarify the problem.
1. When the task is in progress:
    - Update the issue with your progress on a regular basis. Ideally daily.
    - If the issue scope changes, update the issue description to reflect the change. Review the issue weight.
    - Try to work iteratively.
    - If you get stuck, leave a comment on the issue and highlight your comment in [Slack](https://gitlab.enterprise.slack.com/archives/C025LECQY0M)
1. When the change goes into review:
    - Apply the ~"workflow-infra::Under Review" label to the issue
1. If the issue becomes blocked:
    - If one finds a task is blocked by another task, and work cannot continue, assign the ~"workflow-infra::Blocked" label to the task and consider picking up a different task while the task is blocked, such as the blocking task
    - Be sure to use GitLab Issue Relationship to mark upstream blocking issues as such, and add a comment on the blocking issue so that subscribers to that issue can be notified that it's blocking downstream work

#### New Issue Checklist

When creating a new issue:

1. Add the appropriate project label, example: ~"Hosted Runners for GitLab Dedicated".
1. Add the ~"workflow-infra::Triage" label.
1. Add the appropriate team label, example: ~"team::Environment Automation".
1. Ensure the issue is confidential.
1. Add the issue to the correct Epic.

```txt
# Ensure the correct parent epic.
/epic &XXX

# Label with a project label.
# /label ~"Hosted Runners for GitLab Dedicated"

/label ~"team::Environment Automation" ~"workflow-infra::Triage"
/confidential
```

### Issue boards

Issue boards track the progress of all ongoing work.

On a single board, the goal is to get issues from `workflow-infra::Triage` into the `workflow-infra::Done` state. Each of the workflow labels have a special meaning described in [the workflow labels](#workflow-labels) section.

### Status Updates

The status for all work relating to GitLab Dedicated is maintained in the description of the top-level [GitLab Dedicated epic](https://gitlab.com/groups/gitlab-com/gl-infra/-/epics/479) so that it is visible at a glance.

#### Status Update Process

Both Engineering Cross-Functional DRIs should provide weekly updates for the DRI's epics according to following process, which allows alignment with [Project Management in Platforms](/handbook/engineering/infrastructure/platforms/project-management/#project-management-in-platforms):

1. **By Wednesday at 21:00 UTC** the DRI for a project is expected to update the status block in the epic description to:
    1. Format for weekly update: **Date of Update** (YYYY-MM-DD)
    1. Brief update for each of these four areas:
        1. Indicate project [Health Status by label](/handbook/engineering/infrastructure/team/gitlab-dedicated/#workflow-labels).
        1. Briefly highlight project status.
        1. Indicate progress items since the last update.
        1. Indicate any project blockers.
        1. Indicate planned next steps, or mitigations required to progress. This enables other engineers and other managers to have good information about projects in an asynchronous fashion.
    1. If the DRI for a sub-epic is different than the epic DRI, the epic DRI is responsible for getting updates from the sub-epic DRI.
    1. **Update Workflow and Health label** - After each status update, the Workflow label and Health label should be updated. See [Epic labels criteria](/handbook/engineering/infrastructure/team/gitlab-dedicated/#workflow-labels)

1. **Top-Level Epic Status Update** [automation synthesizes updates from status section](/handbook/engineering/infrastructure/team/gitlab-dedicated/#status-update-automation) from description of active epics to provide initiative status in the status section in the description of the top-level initiative Epic.

1. **Weekly engineering/product sync at 16:30 UTC on Mondays** Dedicated engineering/product meeting is used to discuss status updates and potential mitigations as necessary.

1. Status updates will be incorporated into initiative status updates and any initiative reporting in the following week.

#### Status Update Automation

Status updates are auto-generated and added to description of [GitLab Dedicated top-level epic](https://gitlab.com/groups/gitlab-com/gl-infra/-/epics/479) using a bot running [the epic issues summary project](https://gitlab.com/gitlab-com/gl-infra/epic-issue-summaries).

If no update has been provided in an epic or issue for over a week, the issue will automatically receive workflow-infra::stalled label. Engineering managers are responsible for reviewing the status of the issue and helping it move along.

#### Reporting

We provide reports on status of GitLab Dedicated to meet Top Cross-Functional Initiative requirements.

### Backlog Refinement

Prior to the start of a new quarter, the team will spend time refining the Epic backlog. This process will be led by the EM + PM, who will go through the Epics targeted for the upcoming quarter (according to the [roadmap](https://about.gitlab.com/direction/gitlab_dedicated/#roadmap)) and ensure each Epic contains the following information (pulling in different stakeholders to help fill in the details as necessary):

- MVC Scope
- Business Case / Rationale
- Link to high-level design
- Estimated level of complexity

While the above information is being added, the Epic will move from ![Triage](/images/engineering/infrastructure/team/gitlab-dedicated/label-triage.png) to ![Proposal](/images/engineering/infrastructure/team/gitlab-dedicated/label-proposal.png).  Once the information has been finalized, the Epic will move to ![Ready](/images/engineering/infrastructure/team/gitlab-dedicated/label-ready.png).

Having this set of refined epics will help us plan for the upcoming quarter and allow engineers to quickly get started on an Epic once it's ready to be picked up during the quarter.

### Blueprints

All new services or significant changes to our existing architecture must have a [blueprint](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/team/-/tree/main/architecture/blueprints).

Blueprints are designed to help us think through all the critical parts of making a change and help to share knowledge across the team.

A blueprint should consider:

1. Scope and technical considerations
1. High-level implementation details, and project iterations
1. Deployment to new and existing customers
1. Ongoing operation and maintenance
1. Security and Compliance
1. Costs
1. Operational risks
1. Resources

Anyone can contribute a Dedicated blueprint. Please make sure there is always a Staff+ approval before merging.

### Merge Requests

GitLab Dedicated team respects the Company principle of [everything starting with a merge request](/handbook/communication/#start-with-a-merge-request).

1. All Merge Requests (MRs) must go through the review process.
1. Ensure that merge requests include in the description `Closes #<issue>` or `Related to #<issue>` so that the merge request change is linked to the appropriate issue within GitLab.
1. Use draft to indicate the readiness of the MR. In general, remove draft before going into the review process.
1. It is expected that MR author assigns reviewers once the MR is ready to go.
1. Reviewers should review the change and leave comments with questions or suggestions. Please follow the [merge request reviewer guidelines](/handbook/engineering/infrastructure/team/gitlab-dedicated/#merge-request-reviewers) and the [resolving threads guidelines](/handbook/engineering/infrastructure/team/gitlab-dedicated/#resolving-threads-on-a-merge-request) documented below.

The MR approval rule settings for all projects should be:

1. `Prevent approval by author` On ✔️
1. `Prevent approvals by users who add commits` On ✔️
1. `Prevent editing approval rules in merge requests` Off ❌ for emergencies allowing us to act in good faith when absolutely necessary
1. `Remove all approvals when commits are added to the source branch` Off ❌

#### Priorities

We are prioritising reviewing documentation merge requests above all other ones, until further notice. Every merge request documenting acquired knowledge (or concluded discussion) has an impact beyond only the people working on the project directly. In the early stages of building the product, many stakeholders have a need to find actual information quickly, and that means that every line documented increases efficiency of people working on the project as well as people contributing to the project indirectly as we enable more direct self-service.

#### Failed pipeline on the default branch

Having a passing pipeline (green build) on the default branch is very important. Failed pipeline (red build) causes delays in all MR's in progress targeting the default branch, and more importantly, it can cause significant regressions if new MR's are merged into it.

When a red build in the default branch is detected, the first course of action is to **revert** the MR that introduced failures. Reverting should be done **even if it is more work**. A couple of answers to the question "why?":

1. Ensuring that the build is green unblocks all other work in progress.
1. Reverts are safe and quick to do in most cases, and revert leaves a trail in project history. This makes future tracking simpler.
1. When fixing the problem that caused the red build, reviewing the fix in the context of the original change is easier for any reviewer.
1. It is not uncommon for a quick-fix to introduce more issues, thus creating a chain of quick-fixes that are hard to track in the context of the original change.
1. Fixing the problem that caused the red build is less stressful when other team members are not depending on the fix being available.

#### Merge request reviewers

GitLab Dedicated follows the same pattern for author/reviewer assignment as the standard GitLab practice, documented in the [Code Review Guidelines documentation](https://docs.gitlab.com/ee/development/code_review.html#dogfooding-the-reviewers-feature).

The process can be summarized as:

1. The MR author will assign a reviewer and a maintainer to an MR that is ready for review.
     - Check that pipelines are passing before requesting reviews.
     - The MR author can choose who to assign for review. To spread workload and knowledge it is recommended to use the [Environment Automation Reviewer Roulette](https://gitlab-org.gitlab.io/gitlab-roulette/?currentProject=environment-automation).
     - Unless otherwise explicitly noted in the MR description itself, Maintainers are expected to also merge the MR they just approved for efficiency. Add **This MR should be approved by all approvers, last approver should merge.** as the first line in MR description to state the intention clearly.
     - If the change is a significant one, considering mentioning the appropriate group such as `@gitlab-dedicated/environment-automation` or `@gitlab-dedicated/switchboard` in the MR description to help with knowledge sharing.
2. Reviewers will review the MR and leave comments with questions or comments.
    - To help us keep projects moving, please respond to review requests within one working day, and aim to complete the review within two working days.
    - If a reviewer is unable to meet the timelines, or has too many other review requests it's ok to ask someone else to take on the review.

#### Resolving threads on a merge-request

As the merge request author, please don't mark discussions resolved until the reviewer has had a chance to respond. In general, if the reviewer has not yet approved the MR, and the thread is non-trivial, don't mark their comments as resolved, let the reviewer review your response and resolve accordingly during the next round of view. If they have approved the MR, but comments remain unresolved, it's generally fine to resolve comments before merging.

#### Maintainer training

New Dedicated team members work with their manager to decide when to begin Maintainer training. Usually this will be around the third month in the team.

A [Maintainer training issue](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/team/-/issues/new?issuable_template=maintainer_training) will be created using the `maintainer_training` template and a training buddy will assigned to support the training.

After training is complete, the new Maintainer will be added to the Environment Automation Maintainers pool.

### Temporary workarounds

There are times when we are impacted by an upstream library bug. While waiting for the upstream library fix we need to apply a temporary workaround that fixes the bug or mitigates an incident.

To reduce the team's cognitive load on having to keep a mental record of all the applied temporary workarounds, we use the following process to track temporary workarounds:

1. Open an issue explaining the workaround and to which tenant instances it was applied. Apply the label `workaround::active` to the issue
1. If there's a long-term fix issue already created, apply the label `corrective action` and link it to the workaround issue
1. Add a comment in the code describing the workaround and a link to the follow-up issue. For example [workaround on `pyyaml` bug](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/instrumentor/-/merge_requests/1873/diffs)
1. If the temporary workaround involves running scripts by the SRE during maintenance windows, we add the actions in the triage-ops' [tooling-upgrade-toil](https://gitlab.com/gitlab-com/gl-infra/triage-ops/-/blob/master/policies/gitlab-dedicated/tooling-upgrade-toil.yml#L55) policy

### Labels

Commonly used labels are:

1. The team label, such as `team::Environment Automation`.
1. Scoped `workflow-infra` labels.
1. Scoped `component` labels.
1. Scoped `cloud-provider` labels.
1. Scoped `workaround` labels.

The `team::Environment Automation` label is used in order to allow for easier filtering of issues applicable to the team that have group level labels applied.

#### Epics labels

Epics and child epics should contain the following labels:

1. A label indicating the phase of the roadmap in which the epic is scheduled to be delivered epic, such as `FY25-Q2`
1. A scoped `workflow-infra` label
1. All relevant GitLab Dedicated team labels
1. If the epic is labeled `workflow-infra::In Progress`, then a health status label should be applied. (`health::on track`, `health::needs attention`, `health:at risk` by the epic DRI. This label is regularly updated as part of status updates.)

#### Workflow labels

We leverage scoped workflow labels to track different stages of work.

In general, we want to see issues move from `workflow-infra::Triage` to `workflow-infra::Ready` stage to indicate that the submitted issue will go through for implementation. Once the issue is marked with `workflow-infra::Ready`, we are ready to work on the issue until we get the issue marked with `workflow-infra::Done`.

The standard progression of workflow is from top to bottom in the table below:

| State Label | Description |
| ----------- | ----------- |
| ![Triage](/images/engineering/infrastructure/team/gitlab-dedicated/label-triage.png) | Default label added to issues created. Issues with this label need to be confirmed as work we would consider. If we don't want to consider the issue further, we mark it with `workflow-infra::Cancelled` and close it. If this issue does not need Product validation, and we are ready for implementation, issue is moved to `workflow-infra::Ready`. Otherwise, we move it to the next stage `workflow-infra::Proposal`. |
| ![Proposal](/images/engineering/infrastructure/team/gitlab-dedicated/label-proposal.png) | In this stage, proposal is being created and put forward for review with the rest of the team. Issues in this stage are also a part of Product validation workflow. If there are no further questions or blockers, the issue is supposed to be sufficiently refined and ready for implementation and can be moved into `workflow-infra::Ready`. The epics that encapsulate the implementation work for customer facing features must have a Product Manager sign-off before they can be moved to `workflow-infra::Ready` |
| ![Ready](/images/engineering/infrastructure/team/gitlab-dedicated/label-ready.png) | The issue is waiting to be picked up for work. |
| ![In Progress](/images/engineering/infrastructure/team/gitlab-dedicated/label-in_progress.png) | Issue is assigned to a DRI and work has started. |
| ![Done](/images/engineering/infrastructure/team/gitlab-dedicated/label-done.png) | Issue is updated with the outcome of the work that was done, and this label is applied and issue closed. |

There are three other workflow labels of importance:

| State Label | Description |
| ----------- | ----------- |
| ![Cancelled](/images/engineering/infrastructure/team/gitlab-dedicated/label-cancelled.png) | Work in the issue is being abandoned due to external factors or decision to not resolve the issue. After applying this label, issue will be closed. |
| ![Stalled](/images/engineering/infrastructure/team/gitlab-dedicated/label-stalled.png) | If no update has been provided in an issue for over a week, the issue will get this label. The team Engineering Manager is responsible for reviewing the status of the issue and helping it move along. |
| ![Blocked](/images/engineering/infrastructure/team/gitlab-dedicated/label-blocked.png) | Work is blocked due external dependencies or other external factors. Where possible, a [blocking issue](https://docs.gitlab.com/ee/user/project/issues/related_issues.html) should also be set. After applying this label, issue will be regularly triaged by the team until the label can be removed. |

#### Support labels

Scoped support labels are applied to the issues that are opened when a GitLab Support Engineer escalates a ticket for assistance using the ["request for help"](/handbook/support/workflows/how-to-get-help/#how-to-formally-request-help-from-the-gitlab-development-team) process. These requests are reviewed periodically by members of the GitLab Support team. The purpose of this review is to identify whether a request could have been deflected. These reviews primarily lead to updates to the [GitLab Dedicated Support workflows](/handbook/support/workflows/index/#gitlab-dedicated) and the [GitLab docs](https://docs.gitlab.com/).

| State Label | Description |
| ----------- | ----------- |
| `support::reviewed` | The `support::reviewed` label is applied when these issues have been reviewed and the review did not directly result in an issue or MR. |
| `support::reviewed-and-improvement-made` | The `support::reviewed-and-improvement-made` label is applied when an improvement has been made based on a review. Improvements include opened issues or MRs. |

#### Component labels

To denote different types of components and services we are working with, we leverage `component::` scoped labels. By using these labels, we are able to track the distribution of work across different components which also allows us to change focus where needed. These labels are created on [the GitLab Dedicated group level](https://gitlab.com/groups/gitlab-com/gl-infra/gitlab-dedicated), since they are focused on work required specifically for GitLab Dedicated.

**NOTE** We do not use `Service::` labels given that service labels are used by GitLab SaaS related projects.

Component labels with their description can be found [by searching prioritized labels](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/team/-/labels?subscribed=&search=component).

#### Cloud Provider labels

These scoped labels are intended to distinguish generic work to everything made for a specific cloud provider.

| Cloud Provider Label | Description |
| ----------- | ----------- |
| ![AWS](/images/engineering/infrastructure/team/gitlab-dedicated/cloud-provider-aws.png) | Amazon Cloud specific implementation |
| ![AWS](/images/engineering/infrastructure/team/gitlab-dedicated/cloud-provider-gcp.png) | Google Cloud specific implementation |

#### Workaround labels

Scoped workaround labels are intended to track temporary workarounds applied to GitLab Dedicated tenant instances that are supposed to be removed once a permanent fix is available. These labels need to be added to the follow-up issues that describe the implementation of the permanent fix.

| Workaround label | Description |
| ----------- | ----------- |
| ![workaround active](/images/engineering/infrastructure/team/gitlab-dedicated/workaround-active.png) | This label is applied to issues describing workarounds applied to tenant instances |

### Capacity Planning

We operate a Capacity Planning rotation,
which switches on a fortnightly basis amongst all on-call SRES,
with the schedule managed in [PagerDuty](https://gitlab.pagerduty.com/schedules#PAP8TMH).
While Capacity Planning should not require large effort most weeks,
in the event of a Capacity Planning shift overlapping with an on-call shift,
consider swapping your capacity planning shift with another engineer
to ensure both tasks receive the necessary attention.
The goal is to give ourselves the best chance of resolving impending saturation events
*before* they become a customer-impacting incident
It is based on statistical modeling and human interpretation,
and is not expected to be perfect in every situation.
Do your best,
and understand that the process is inherently imprecise and fuzzy at the edges.

The Dedicated capacity planning process is built on top of [Tamland](https://gitlab.com/gitlab-com/gl-infra/tamland).
More information about capacity planning is available in [documentation](https://gitlab-com.gitlab.io/gl-infra/observability/docs-hub/capacity-planning/introduction/).

The overall flow of work is to assess any new reported saturation risks,
and re-review any which are due to be looked at again.
If there is an apparent risk of saturation,
initiate further assessment for potential remediation action,
and actively manage any such ongoing issues that are assigned to you.

At the start of your shift review the
[handover issue](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/team/-/issues/?label_name%5B%5D=capacity-planning-handover)
from the prior shift and close it when you are up to speed.

At the start of each work week while you are on duty,
as a high priority task that is second only to active incidents:

1. Review the capacity planning issues that are:
   1. In the Open column of the [board](https://gitlab.com/gitlab-com/gl-infra/capacity-planning-trackers/gitlab-dedicated/-/boards/7536402).
   1. [Previously assessed](https://gitlab.com/gitlab-com/gl-infra/capacity-planning-trackers/gitlab-dedicated/-/issues/?label_name%5B%5D=violation%3Asaturation) but now and therefore in need of a new look.
   - Use the labels auto-populated on the issue to help prioritize if necessary.
     `violation:hard` is more important than `violation:soft`,
     and `severity::` provides additional signal.
1. For each saturation issue that is up for review,
   evaluate the prediction given in the issue:
   - Check the tips below for suggestions on quickly assessing predictions as false positives;
     this is a good way to quickly reduce the number of issues requiring more work
   - If evaluation requires non-trivial investigation over more than a day calendar time,
     label it `capacity-planning:investigate` and investigate when you have dealt with higher priority capacity planning issues
   - If you assess that it warrants active action in the near future and is not already `capacity-planning::in-progress`:
      1. Label it `~capacity-planning:in-progress`,
      1. Add or update the due date to next week, and
      1. Create a remediation [issue](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/team/-/issues/new?issuable_template=saturation_risk)
      - Take into consideration whether we have existing remediation options
        (for example: performance-based overlays, or entire reference architecture upsizing)
        or if we will need to add capabilities to handle the particular saturation problem.
        Err on the side of raising an issue for further discussion;
        we can always close it and return to monitoring status.
   - If it's in `capacity-planning::in-progress` check on the remediation issue and ensure it is making progress,
     and update the due-date to be 1 week in the future.
     If remediation has completed,
     move the issue to `capacity-planning::verification`
     or, if results are already clearly sufficient, close it.
   - If it is in `capacity-planning::verification`,
     check if the remediation results can be considered sufficient,
     and if so close the issue.
     If not, update the due date to next week for further review.
   - If the prediction has a wide-range and there is no indication that it will breach any time soon,
     or the lead time is sufficient that there is no urgency (for example 3+ months for Gitaly disk saturation),
     label the issue with `~capacity-planning::monitor`
     and update the due-date to just before the start of the next shift
     for review by the incoming duty engineer.
   - If a metric is of a nature (perhaps for reasons specific to Dedicated)
     that predictions are consistently unusable across all customers for that metric,
     or if the prediction is plausibly useful but needs tuning:
      1. Label it `capacity-planning::tune-model`,
      1. Update the due-date to 2 weeks in the future,
      1. Work on the tamland
         [manifest](https://gitlab.com/gitlab-com/runbooks/-/blob/master/reference-architectures/get-hybrid/config/tamland/manifest.json)
        to exclude or tweak the specific saturation signal.
         - The [Observability team](/handbook/engineering/infrastructure-platforms/production-engineering/observability/)
        can offer advice on the finer details of the tamland configuration.
1. Check that Tamland is [running](https://gitlab.com/gitlab-com/gl-infra/capacity-planning-trackers/gitlab-dedicated/-/pipeline_schedules).
   The pipeline should run successfuly every day.
   Investigate and fix any errors or failures.
1. Check if there are new production tenants not [listed](https://gitlab.com/gitlab-com/gl-infra/capacity-planning-trackers/gitlab-dedicated/-/blob/main/tenants.yaml).
   Update the list as necessary and create corresponding `tenant::` [labels](https://gitlab.com/gitlab-com/gl-infra/capacity-planning-trackers/gitlab-dedicated/-/labels?subscribed=&sort=relevance&search=tenant%3A%3A).

When your shift comes to an end,
create a [handover issue](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/team/-/issues/new?issuable_template=capacity_planning_handover&issue[title]=Capacity%20Planning%20Triage%20handover%20notes%20YYYY-MM-DD)
assign it to the incoming duty engineer and populate with any information that the incoming shift should know about.
Let comments/discussions on the specific issues speak for mundane and routine matters, to be reviewed on their due date, but consider noting:

1. Any metrics that were coming close to being a concern but didn't warrant remediation just yet,
   or that are in some way unusual
2. Brief comment on any ongoing remediations.
   Reassign the remediation implementation issues to the incoming duty engineer,
   unless you want to finish them up yourself or they are assigned to someone else for specific reasons.

Remember to record updates and status comments on each capacity-planning issue when necessary or useful,
just like you would on a team issue.

Some tips:

1. Forecasts may take several months to become predictable on new tenants.
   As long as the literal numbers aren't too high,
   do not be alarmed if the predicted range is wide and tamland is being overly cautious.
   Putting into `capacity-planning::monitor` state is a good course of action in this situation
1. Sometimes Tamland will generate alerts for services whose saturation forecast is generally trending downwards,
   but which Tamland's confidence interval (the light blue area in prediction graphs) still includes the possibility of saturation.
   Unless you have specific reasons to suspect a real saturation risk,
   strongly consider tagging the issue as `capacity-planning::monitor` and moving its due date out by 2+ weeks.
1. Try to get ahead of obvious gradual growth with enough time to take calm action.
   For example, 1 month of warning for something like Gitaly or Opensearch disk usage is sufficient to schedule an expansion of the storage volumes during upcoming maintenance windows,
   not in a hurry in response to a pager alert
1. For items that need to be monitored it is encouraged to attach the current forecast in the comment;
   the forecast will likely change in place over the following weeks, and the history can be useful.
1. Look for the component / alert name in the
   [Capacity Planning Issue Tracker](https://gitlab.com/gitlab-com/gl-infra/capacity-planning-trackers/gitlab-dedicated/-/issues) can be a good source of information,
   as some recurring saturation forecast share the same or similar causes,
   or just to gain some insight into how these issues have been investigated and resolved in the past.
1. Remember that some items may alert across multiple tenants.
   If possible, treat them as a unit rather than per-tenant,
   unless the causes and fixes are truly distinct.
   This is particularly important for false-positives or items needing tuning
1. Trust your instincts.
   If it looks concerning, raise a remediation issue; they are free, and can easily be closed again after additional input.
   If it looks fine it probably is,
   and even if it isn't then there's a rotating schedule of other engineers in the following weeks who can spot something you missed.
   This process is designed to get warning of things that are coming when possible,
   not to be a perfect predictor in all cases.

### Resources

Resources used by the team to conduct work are described on the [Development Resources Page](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/team/-/blob/main/engineering/Dev-resources.md).

## History and trivia

- Name for [`Switchboard` customer portal](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/team/-/issues/7#note_591358260) was suggested by @marin after he spent a day trying to figure out which mixing console (Also known as a switchboard/soundboard) to get for amateur music making. He didn't buy anything, but the suggestion was accepted.
- Name for [`Amp` management cluster](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/team/-/issues/31#note_609710775) was suggested by @ccasella, as it is the instance that is "powering" supply of other instances.
- [Dedicated Group - Year in Review 2023](https://gitlab.com/gitlab-com/gl-infra/gitlab-dedicated/team/-/issues/3681)
