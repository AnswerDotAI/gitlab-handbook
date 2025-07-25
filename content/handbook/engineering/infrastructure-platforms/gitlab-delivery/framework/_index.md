---
title: GitLab Delivery:Framework
---

## Summary

Framework is a team within the [GitLab Delivery Stage](/handbook/engineering/infrastructure-platforms/gitlab-delivery/delivery/). This team takes ownership of the GitLab Environment Toolkit (GET) as instance lifecycle tool, Reference Architectures, tooling and frameworks related to upgrade path testing, and will ensure installation and upgrade paths are fully tested and reliable. We follow the same processes as listed on the [GitLab Delivery Stage](/handbook/engineering/infrastructure-platforms/gitlab-delivery/delivery/), unless otherwise stated on this page.

## Mission

The Framework team intends to make GitLab easy to operate at any scale. GitLab is critical to our end users (developers) and a necessity for organizations most important business operations and workflows. The Framework team functions with autonomy to drive good quality within our Reference Architectures and GET above all else.

### Some optimal success criteria include

1. A decrease in the cost of support per customer
1. Lower time to value for new installations
1. More instances on the recent version of GitLab
1. Fewer upgrade-related incidents
1. Instances on supported architecture

Seeing that many of these metrics are owned by multiple teams, the Framework Team will contribute here but does not have full agency to drive.

### What does it mean to Operate GitLab?

GitLab is a complex application. Organizations typically have a dedicated team to manage GitLab internally. This operation includes day-to-day maintenance, upgrades, backup and restore, and downtime. This team's goal is to make this operation easy for all organizations, including our own deployments.

It is not solely the responsibility of the Framework team to make GitLab easy to operate, but to provide guidance to the wider GitLab organization to develop in a way that is conducive to a good user experience for admins. Managing GitLab components in a tested and supported architecture significantly lowers the operational aptitude required.

### Delivery of Mission

1. Easy enablement materials to consume reference architectures for account teams and operators
2. Collaborate on structured guidance for operational excellence in feature development
3. Verify upgrade paths
4. Stewards of a good experience for managing GitLab with GET and the Reference Architectures

### Tools and Responsibilities

The Framework team owns and leads our GitLab Environment Toolkit and Reference Architectures initiatives, which are key programs with the aim assist and enable customers to deploy and maintain their GitLab environments. This includes external users as well as easing the operational requirements for our own SaaS offerings.

#### GitLab Environment Toolkit (GET)

GET is a set of opinionated Terraform and Ansible scripts to assist with deploying scaled self-managed GitLab environments following the Reference Architectures. A good experience with GET means users will more quickly have an environment (lower TTV) and long-term success (decreased need for support).

#### Reference Architectures

The reference architectures will provide the best user experience with the intent to decrease the amount of required support from GitLab. The Framework team will continue to ensure the RAs meet the needs of customers by improving architecture designs over time. The Framework team will also provide guidance for internal teams to review and add components as needed.

#### Upgrade Path Validation

Upgrading GitLab is one of the most challenging aspects of its operation and often requires dedicated attention to effectively plan the upgrade process. The Framework team continuously validates the upgrade paths between releases to ensure that only necessary, planned stops are introduced, thereby instilling confidence in the upgrade process for our Self-Managed and Dedicated customers.

#### Other Responsibilities

1. Architecture performance and non-functional testing
1. Enablement of GitLab account teams to provide appropriate recommendations
1. Self-serve experience for scaling GitLab

## Team Members

{{< team-by-manager-slug "lsogunle" >}}

Product Manager: [Martin Brümmer](/handbook/company/team/#mbruemmer)

## Roadmap

The team's primary roadmap is tracked within [the Roadmap epic](https://gitlab.com/groups/gitlab-com/gl-infra/-/epics/1454). Our roadmap is aligned with GitLab Delivery's overall strategic objectives and is reviewed and updated as needed.

## Working with Us

To engage with the Framework team, please refer to the following.

Please kindly note that as an engineering team our resources are finite. Direct asks to join customer calls or projects are not within the remit of this team and should instead be directed accordingly to Product Management, Support or Professional Services accordingly.

### Slack Channels

The following list includes Slack channels relevant to projects within the team's scope:

* [#g_software_delivery-framework](https://gitlab.enterprise.slack.com/archives/C080V5MNVMY) - This is the primary Slack channel for discussions related to the GitLab Delivery Framework team.
* [#gitlab_environment_toolkit](https://gitlab.enterprise.slack.com/archives/C01DE8TA545) - For discussions, questions, and requests specific to the GitLab Environment Toolkit (GET).
* [#reference-architectures](https://gitlab.enterprise.slack.com/archives/C015V8PDUSW) - For discussions, questions, and requests related to Reference Architectures.
* Our slack group handle is `@software-delivery-framework-team`.

### Reference Architecture Review requests

For any requests relating to customer environments, either proposed or existing, they must be raised in the [Reference Architectures project](https://gitlab.com/gitlab-org/quality/reference-architectures/-/issues/new) in the following circumstances only with the given templates:

* `environment-review-request` - Sanity checks of new environment designs, not already covered in the [Reference Architecture docs](https://docs.gitlab.com/ee/administration/reference_architectures/).
* `request-for-help` - Help requests from the Support Team for assistance when an issue is suspected to be due to the environmental design.

Requests should be opened two or more business days before action is needed to ensure the team has time to prepare and we kindly ask for this process to be followed for tracking and capacity reasons.

**It is important to note that only requests following the outlined process will be addressed. To ensure effectiveness and minimize disruption, we strongly discourage directly tagging team members in real-time on issues or customer requests.**

Reference Architecture consultations will not include the following:

1. No involvement in direct customer calls or communications.
1. All requested data stated in the template must be proactively supplied.

### Environment Build Requests

**The Framework team will not fulfill bespoke environment build requests due to capacity constraints.** Also, building large sandbox environments with GET should be generally discouraged due to cost implications unless strictly required. However, here are some options to self-serve in building these types of environments:

* Self-service using GET documentation
  * Teams can follow the comprehensive [GET documentation](https://gitlab.com/gitlab-org/gitlab-environment-toolkit#documentation) to build their own environments. This is the primary recommended approach for teams that need custom environments.
  * Using the automated [Sandbox Cloud](/handbook/company/infrastructure-standards/realms/sandbox/) offering is recommended for setting up a cloud account for testing and development purposes.
* Run GitLab locally: For simpler needs, running GDK or Docker locally is recommended instead of building large environments to reduce costs and complexity.
* Use shared environments from Infra: Utilizing existing shared environments provided by the Infrastructure team.

## Project Management

<!-- List of Trackers and scope -->
[Framework Issue Tracker](https://gitlab.com/groups/gitlab-com/gl-infra/software-delivery/framework/-/issues).
[GitLab Environment Toolkit (GET) issues](https://gitlab.com/gitlab-org/gitlab-environment-toolkit/-/issues) - Primary tracking system for the GitLab Environment Toolkit. This board encompasses requests, enhancements, technical debts items and customer reported issues.

[GitLab Upgrades Test Coverage](https://gitlab.com/groups/gitlab-org/-/epics/12458) - This epic encompasses issues related to testing upgrade paths.

[Reference Architecture issues](https://gitlab.com/gitlab-org/quality/reference-architectures/-/issues) - This is where we track work related to Reference Architectures and conduct reviews for customer environments upon request.

### Epics

<!-- Top level Epic(s) -->

This top-level [epic](https://gitlab.com/groups/gitlab-com/gl-infra/software-delivery/framework/-/epics/2) monitors the different initiatives and sub-epics within the team and their respective statuses. It is populated automatically through [epic automation](https://gitlab.com/gitlab-com/gl-infra/epic-issue-summaries).
Every sub-epic must

1. Epics must be created with the epic template linked below.
1. Have the top-level epic as the parent epic.
1. Have a completion date and a DRI for providing a weekly status update.
1. Have a relevant `workflow::` or `workflow-infra::` label.
1. Epic DRIs will be pinged on Tuesdays to leave a status update for the week in the epic.
1. These updates are collected into the team's top-level epic which feeds into the [Grand Review](/handbook/engineering/infrastructure/platforms/#grand-review).

We follow Platforms Project Management practices as [outlined](/handbook/engineering/infrastructure/platforms/project-management/).

### Labels

<!-- Labels explanations -->
The primary team label is `group::framework`. This label should be applied to issues and epics throughout the organization that require the team's attention.
The team tracks work using the `workflow` and `workflow-infra` labels across issues, epics, and MRs. Team members will ensure that their work items are updated with the correct workflow labels.

| `gitlab-org` issues | `gitlab-com/gl-infra` issues |
| ---------- | ------------------  |
| ~"workflow::refinement" | ~"workflow-infra::Triage" |
| ~"workflow::ready for development" | ~"workflow-infra::Ready" |
| ~"workflow::in dev" | ~"workflow-infra::In Progress" |
| ~"workflow::in review" | ~"workflow-infra::Under Review" |
| ~"workflow::blocked" | ~"workflow-infra::Blocked" |
| ~"workflow::verification" | ~"workflow-infra::Verify" |
| ~"workflow::complete" | ~"workflow-infra::Done" |

#### Epic Template

<details><summary>Epic Template</summary>

```markdown
### DRI :levitate:
- TBC

### Participants :busts_in_silhouette:


### Problem to solve :thinking:

### Why :results-for-customers:
<!-- Explain the importance of this epic and its contributions to delivering results for customer. -->

### Future Maintenance :construction:
<!-- If this involves building a new piece of tooling, pipelines, or artifacts, clearly identify and align on future maintenance responsibilities. -->

### Acceptance Criteria

### Documentation :book:

* Publicly Accessible Documentation:

### Links / references :books:

*

---

<!-- STATUS NOTE START -->

<!-- STATUS NOTE END -->

/label ~"group::framework" ~"workflow-infra::Triage"

```

</details>

## Team Impact

The following are records of the annual achievements of the Framework team.

1. [Team Impact Overview for 2024](https://gitlab.com/gitlab-com/gl-infra/software-delivery/framework/software-delivery-framework-issue-tracker/-/issues/15)
