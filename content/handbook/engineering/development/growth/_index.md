---
title: Growth Stage
description: "The Growth Stage consists of development teams working in the product delivering enhancements and running experiments"
---

## Vision

Grow an agile fullstack development capability to support our product goals through feature development and experiments
enabling GitLab to make informed product decisions and achieve results in line with our [product direction](/handbook/marketing/growth/).

## Mission

Working inline with our [values](/handbook/values/), we focus on [iteration](/handbook/values/#iteration) and [collaboration](/handbook/values/#collaboration),
working with and across areas of the product our development department counterparts maintain,
as well our own [areas of responsibility](/handbook/marketing/growth/#product-ownership).

## Direction

We work on the issues prioritized by our product teams including running [experiments](/handbook/engineering/development/growth/experimentation/) on GitLab.com.
More information on priorities can be found on the [Growth direction](/handbook/marketing/growth/) page.

Growth stage teams have Fullstack Engineers.
The reason for this is that the Growth stage has a need for both Frontend and Backend skill-sets,
but as a small team, has optimized for team member efficiency to adopt the Fullstack role.

Some useful links to see how and what we are working on include:

- [Growth direction](/handbook/marketing/growth/)
- [Growth Kanban board for development](https://gitlab.com/groups/gitlab-org/-/boards/1392106?&label_name%5B%5D=devops%3A%3Agrowth)
- [Experimentation](experimentation/)
- [GLEX](https://gitlab.com/gitlab-org/ruby/gems/gitlab-experiment)
- [Experiment rollout](https://gitlab.com/groups/gitlab-org/-/boards/1352542?label_name[]=experiment-rollout)
- [acquisition](acquisition/) group
- [activation](activation/) group

Growth teams contribute to a GitLab [experimentation](/handbook/engineering/development/growth/experimentation/) gem to make it easier to run experiments and make data driven product decisions on GitLab.com.

## Roadmap

Our current roadmap can be accessed through our quarterly OKR planning issues:

- [FY24 Q3](https://gitlab.com/gitlab-org/gitlab/-/issues/420650)
- [FY24 Q4](https://gitlab.com/gitlab-org/gitlab/-/issues/428640)

## Who Are We?

### People Leaders in Development

{{< members-by-role role="Growth and Govern" >}}

### All Team Members

The following people are permanent members of groups that belong to the Growth stage:

#### Acquisition

{{< team-by-departments department="Acquisition Team" >}}

#### Activation

{{< team-by-departments department="Activation Team" >}}

## Counterparts

We work closely with our [Product Team](/handbook/product/categories/#growth-stage) counterparts to design and implement
features and experiments that measure the impact of changes to our messaging, UX, and overall experience of using GitLab.

### Stable Counterparts

The following members of other functional teams are our stable counterparts:

{{< engineering/stable-counterparts role="Growth" manager-role="Director of Engineering for Secure, Govern, and Growth" other-manager-roles="Govern and Growth|Growth and Govern:Threat Insights|VP, Online Sales and Self Service" >}}

## How We Work

Our team follows the [Product Development Flow](/handbook/product-development/product-development-flow/#workflow-summary) utilizing all labels from `~workflow::start` to `~workflow::complete`.

We adhere to the **Completion Criteria** and **Who Transitions Out** outlined in the [Product Development Flow](/handbook/product-development/product-development-flow/#workflow-summary) to progress issues from one stage to the next.

### Labels and Workflow Boards

We use workflow boards to track issue progress throughout a milestone. Workflow boards should be viewed at the highest group level for visibility into all nested projects in a group.

The Growth stage uses the `~"devops::growth"` label and the following groups for tracking merge request rate and ownership of issues and merge requests.

| Name          | Label                   | gitlab-org | All Groups |
| ----------    | -----------             | ------     | ------     |
| Growth        | `~"devops::growth"`     | [Growth Workflow](https://gitlab.com/groups/gitlab-org/-/boards/4152639) | [-](https://gitlab.com/dashboard/issues?scope=all&utf8=%E2%9C%93&state=opened&label_name[]=devops%3A%3Agrowth) |
| Acquisition   | `~"group::acquisition"` | [Acquisition Workflow](https://gitlab.com/groups/gitlab-org/-/boards/4152639) | [-](https://gitlab.com/dashboard/issues?scope=all&utf8=%E2%9C%93&state=opened&label_name[]=devops%3A%3Agrowth&label_name[]=group%3A%3Aacquisition) |
| Activation    | `~"group::activation"`  | [Activation Workflow](https://gitlab.com/groups/gitlab-org/-/boards/4152639) | [-](https://gitlab.com/dashboard/issues?scope=all&utf8=%E2%9C%93&state=opened&label_name[]=devops%3A%3Agrowth&label_name[]=group%3A%3Aactivation) |
| Experiments   | `~"experiment-rollout"` | [Experiment tracking](https://gitlab.com/groups/gitlab-org/-/boards/1352542) | [-](https://gitlab.com/dashboard/issues?scope=all&utf8=%E2%9C%93&state=opened&label_name[]=experiment-rollout) |
| Feature Flags | `~"feature flag"`       | [Feature flags](https://gitlab.com/groups/gitlab-org/-/boards/1725470?&label_name[]=devops%3A%3Agrowth&label_name[]=feature%20flag) |  |

Growth teams work across the GitLab codebase on multiple groups and projects including:

- The [gitlab.com/gitlab-org](https://gitlab.com/gitlab-org/) group
- [gitlab](https://gitlab.com/gitlab-org/gitlab)
- [GLEX](https://gitlab.com/gitlab-org/ruby/gems/gitlab-experiment)
- [customers-gitlab-com](https://gitlab.com/gitlab-org/customers-gitlab-com)
- The [gitlab.com/gitlab-com](https://gitlab.com/gitlab-com/) group
- [www-gitlab-com](https://gitlab.com/gitlab-com/www-gitlab-com)

### Issue sequencing

In order to convey Issue implementation order and blocking concepts,
we leverage the [blocking issue linking feature](https://docs.gitlab.com/ee/user/project/issues/related_issues.html#blocking-issues).

More on the discussion can be seen in https://gitlab.com/gitlab-org/growth/team-tasks/-/issues/752.

### Issue Refinement And Estimation

Before the work can begin on an issue, we should refine and estimate it. We have a continuous process for this, leveraging additional workflow status,  `~"workflow::refinement"`, which indicates that the issue is being refined by the team. Once the issue refinement is completed, it can be moved to `~"workflow::scheduling"` stage.

The refinement process is driven by [triage bot automations and policies](https://gitlab.com/gitlab-org/quality/triage-ops/-/blob/master/policies/groups/gitlab-org/growth/refine-automations.yml) to ensure that it's smooth and consistent.

## Refinement Steps

1. Issues are moved from `~"workflow::planning breakdown"` to `~"workflow::refinement"` automatically by the triage bot in order of priority (from top to bottom). The bot will only move issues to refinement if there is room in refinement column, meaning there is less issues than maximum limit for this column. This is first chance for PMs to prioritize issues by moving them higher in the `planning breakdown` column. After the issue is moved to refinement, a dedicated `refinement thread` is created, which acts as a place for discussion and weight estimation.
     - 💡 Hint: In rare case when an issue has to be expedited, it's possible to move it to refinement manually. This will invoke a reaction from triage bot, which will add `refinement thread` for such issue instantly so the refinement can proceed the same way as with automated path.
2. During refinement the team ensures that the issue is well described and requirements are clear. They can use the `refinement thread` to discuss but they should make sure that any changes and decisions made there are also reflected in issue's description. Once each engineer is comfortable with the way the issue is described, they can vote their estimation of weight based on our [guidelines](/handbook/engineering/development/growth/#estimation-guidelines). The voting happens by reacting to the thread with one of few possible weight estimates: 1️⃣ 2️⃣ 3️⃣ 5️⃣ or 🚀.
3. Each day the triage bot checks all issues in `~"workflow::refinement"` column and if an issue has required minimum number of estimation votes (see `MIN_REACTIONS` constant [here](https://gitlab.com/gitlab-org/quality/triage-ops/-/blob/master/lib/growth_refine_automation_helper.rb?ref_type=heads#L16) for the current setting) it will be moved to `~"workflow::scheduling"`.
    - 💡 Hint: If there is some problem with the issue and it shouldn't be moved forward even if enough engineers estimate it, ❌ reaction can be added to the thread which will stop the bot from transitioning the issue to `~"workflow::scheduling"` as long as this reaction sticks to the thread. This means that whoever put it is also responsible for removing it once the problem is gone.
4. Once the issue is in `~"workflow::scheduling"`, it is awaiting final prioritization by PMs - it has to be manually moved to `~"workflow::ready for dev"` depending on the current priorities. This part of the process is PMs responsibility. This allows for additional fine-tuning of priorities and acts as a buffer for our ready for development column.

## Estimation guidelines

| Weight | Description (Engineering) |
| ------ | ------ |
| 1 | The simplest possible change. We are confident there will be no side effects. |
| 2 | A simple change (minimal code changes), where we understand all of the requirements. |
| 3 | A simple change, but the code footprint is bigger (e.g. lots of different files, or tests effected). The requirements are clear. |
| 5 | A more complex change that will impact multiple areas of the codebase, there may also be some refactoring involved. Requirements are understood but you feel there are likely to be some gaps along the way. |
| 8 | A complex change, that will involve much of the codebase or will require lots of input from others to determine the requirements. |
| 13| A significant change that may have dependencies (other teams or third-parties) and we likely still don't understand all of the requirements. It's unlikely we would commit to this in a milestone, and the preference would be to further clarify requirements and/or break in to smaller Issues. |

In planning and estimation, we value [velocity over predictability](/handbook/engineering/development/principles/#velocity-over-predictability). The main goal of our planning and estimation is to focus on the [MVC](/handbook/values/#minimal-valuable-change-mvc), uncover blind spots, and help us achieve a baseline level of predictability without over optimizing. We aim for 70% predictability instead of 90%. We believe that optimizing for velocity (merge request rate) enables our Growth teams to achieve a [weekly experimentation cadence](/handbook/product/groups/growth/#weekly-growth-meeting).

- If an issue has many unknowns where it's unclear if it's a 1 or a 5, we will be cautious and estimate high (5).
- If an issue has many unknowns, we can break it into two issues. The first issue is for research, also referred to as a [Spike](https://en.wikipedia.org/wiki/Spike_(software_development)), where we de-risk the unknowns and explore potential solutions. The second issue is for the implementation.
- If an initial estimate is incorrect and needs to be adjusted, we revise the estimate immediately and inform the Product Manager. The Product Manager and team will decide if a milestone commitment needs to be adjusted.

## Engineering DRI for Large-Scale Initiatives

For substantial epics or projects that require extensive coordination, we designate an Engineering Directly Responsible Individual (DRI). This role is pivotal in managing complex workstreams within our team.

The Engineering <abbr title="Directly Responsible Individual">DRI</abbr> is typically assigned in two scenarios:

1. When an epic reaches the development phase and requires detailed oversight.
1. When an issue grows in scope and complexity, necessitating its promotion to an epic.

Importantly, we appoint the <abbr title="Directly Responsible Individual">DRI</abbr> before breaking down the work into smaller, manageable tasks. This early assignment is crucial because one of the <abbr title="Directly Responsible Individual">DRI</abbr>'s primary responsibilities is to lead the planning process and facilitate the strategic breakdown of the epic or project into actionable deliverables.

By having a dedicated <abbr title="Directly Responsible Individual">DRI</abbr> for these large-scale initiatives, we ensure focused leadership, clear accountability, and effective coordination throughout the development lifecycle of complex engineering efforts.

### Role Responsibilities

*Communicating Progress and Managing Health Status*

The Engineering <abbr title="Directly Responsible Individual">DRI</abbr> oversees weekly updates on the epic, tracking overall health status, including progress, obstacles, and emerging risks.

- They continuously monitor and report on the epic's health status, indicating if it's on track, at risk, or blocked, providing context around any changes.
- Progress updates are reported via a top-level comment on the epic containing the development work (usually linked to our OKRs).
- Updates are due by End of Day on the <abbr title="Directly Responsible Individual">DRI</abbr>'s last workday of the week.

*Facilitating Breakdown of Work*

This role is crucial in breaking down epics into smaller, manageable deliverables, ensuring tasks are clearly defined and ready for development.

*Ensuring Steady Progress*

The responsible individual ensures work items progress smoothly through our Kanban flow, with enough work prepared for development to maintain consistent progress.

*Risk Management and Mitigation*

Early identification of potential risks and proactive collaboration with the team to develop mitigation strategies are key responsibilities. This enhances the role in not only communicating issues but actively managing and resolving them.

*Retrospective and Continuous Improvement*

Upon conclusion of each epic, a brief retrospective session should be facilitated to gather feedback on successes and areas for improvement. This practice helps refine processes and improves the handling of future epics.

*Collaboration with Product and Design*

Active collaboration with Product Managers and Designers during the planning phase is essential to ensure the epic's scope aligns with business goals and user experience standards.

*Resource Allocation and Escalation*

The appointed individual is empowered to identify when additional resources or support are needed and to escalate issues promptly. This helps ensure timelines are met and work progresses smoothly.

*Note:* While responsible for timely delivery, the <abbr title="Directly Responsible Individual">DRI</abbr> is not expected to execute every task personally.

### Standardized Status Update Template

To ensure consistency and clarity in our communication, we've implemented a standardized comment template for status updates across the Growth team.

**Template Details:**

- **Name:** "Growth - DRI Status Update"
- **Scope:** Available for the entire GitLab group
- **Location:** [GitLab.com Comment Templates](https://gitlab.com/groups/gitlab-org/-/comment_templates/1000452)

This template streamlines our reporting process, making it easier for <abbr title="Directly Responsible Individual">DRI</abbr>s to provide comprehensive and uniform updates. By using a consistent format, we enhance readability and facilitate quick information retrieval for all team members.

For guidance on using comment templates, please refer to our [Comment Templates Usage Guide](https://docs.gitlab.com/ee/user/project/description_templates.html#use-the-templates).

## Technical exploration ("Spike") guidelines

Occasionally, the team will be asked to dedicate time to exploring or "spiking" a technical solution to a problem or
opportunity area deemed a priority by Growth PM. Technical spikes are fundamentally different than our typical work items
as the result is more commonly a recommendation on a technical direction or solution rather than code, yet they still
require dedicated developer focus and should be accounted for in our development workflows. As such, we've determined
the following guidelines and responsibilities for individual Growth Engineers to follow when addressing a technical
spike in our workflow:

Note: Technical spikes will serve as the single source of truth for implementation and will have one of three outcomes:
conversion into a development implementation issue, promotion to an epic with additional implementation issues, or
closure if determined not technically feasible.

```mermaid
flowchart TD
A[Technical Spike Created] --> B[Engineer Assigns Self]
B --> C[Set Due Date with PM]
C --> D[Review & Clarify Requirements]
D --> E[Document Investigation Approach]
E --> F[Investigation Period]
F --> G[Document Progress & Findings]
G --> H[Provide Summary & Recommendations]
H --> I{Technical Feasibility?}
I -->|Not Feasible| J[Close Issue with Explanation]
I -->|Feasible| K{Scope Size?}
K -->|Small Scope| L[Convert to Implementation Issue]
K -->|Large Scope| M[Promote to Epic & Create Implementation Issues]
L --> N[Move to workflow::solution validation]
M --> O[Epic enters workflow process]
```

**Inputs**

As a technical spike is prioritized and available for pickup in `~workflow::ready for development`, complete the following steps:

- Assign yourself, apply ~spike label, set the milestone and set the workflow label to `~workflow::in dev`
- Connect with the responsible PM to align on a reasonable due date for the technical spike and assign it accordingly.
  Duration will be dependent on the subject matter and Growth's familiarity with the topic.
- Review the contents of the technical spike issue body.
  Add any comments to clarify outstanding questions with the responsible PM.
  Identify potential needs for cross-team collaboration, subject matter expertise, or other important inputs for the
  technical spike.
- Add with your proposed approach and note any desired PM checkpoints.

**During the technical spike investigation period**

- Document your progress with detailed notes to support our async collaboration model and maintain an inclusive environment.
- Share any discoveries that might impact the spike's duration or scope with the responsible PM.
- If approaching the due date and needing more time, proactively discuss next steps with the responsible PM.

**Outputs**

As the technical spike work comes to a completion, complete the following steps to close out the spike process:

- Provide a summary comment with detailed learnings of your investigation and recommended path(s) for the solution in the
  spike issue.
  Include an outline of the recommended next step issues and/or epics to be created for the next phase of work.
- Tag in the responsible PM, EM, and Growth Engineering team (`@gitlab-org/growth/engineering` team) for review.
- Confirm with the responsible PM that the spike requirements have been met within the allotted duration time.

Based on your findings, proceed with one of these three outcomes:

1. **For technically infeasible solutions:**
   Close the issue with a clear explanation of the technical limitations discovered.

2. **For single-issue implementations:**
   Refine the technical details in the current issue and move it back into `~workflow::solution validation` for PM guidance.

3. **For multi-issue implementations:**
   Promote the spike to an epic and create the necessary implementation issues to break down the work.
   As the engineer who performed the spike, you are responsible for creating these implementation issues.

For outcomes 2 and 3, ensure technical details are sufficiently documented to support implementation once it re-enters later
`workflow` stages.

### UX

Info on the Growth UX team and how they work can be found on the [Product/Growth page](/handbook/product/groups/growth/#ux).

### How We Use Issues

To help our team be [efficient](/handbook/values/#efficiency), we explicitly define how our team uses issues.

#### Issue Creation

We aim to create issues in the same project as where the future merge request will live. For example, if an experiment is being run in the [GitLab CustomersDot](https://customers.gitlab.com), both the issue and MR should be created in the [CustomersDot](https://gitlab.com/gitlab-org/customers-gitlab-com) project.

We emphasize creating the issue in the right project to avoid having to close and move issues later in the development process. If the location of the future merge request cannot be determined, we will create the issue in our catch-all [growth team-tasks project](https://gitlab.com/gitlab-org/growth/team-tasks/issues).

We use [issue templates](experimentation/#experiment-issue-templates) for common tasks.

#### Iteration

To support [Iteration](/handbook/values/#iteration) Growth engineering:

1. Separates refactoring from feature [MVCs](/handbook/values/#minimal-valuable-change-mvc). When refactoring is raised in review, the preference is to resolve in a follow up issue.
1. Addresses technical debt and follow up issues through prioritization and discussion by relevant stakeholders.
1. Issues with a weight of `5` and higher should be reassigned to the Product Manager to make sure they can be split into smaller [MVCs](/handbook/values/#minimal-valuable-change-mvc).
   When this is not possible, the Product Manager will create a spike or research issue so that engineering can break it down and close the original.
1. We make use of research issues and engineering spikes in the prior milestone, so estimations are more accurate.

#### Status Updates

The DRI (assignee) of an issue is encouraged to add an async issue update, particularly for issues labeled `~Deliverable` or `~Stretch`.
These updates can be added anytime and are useful to highlight when an issue is on track, blocked, or may need to be re-prioritized.
This helps us maintain [transparency](/handbook/values/#transparency) and our [bias towards asynchronous communication](/handbook/values/#bias-towards-asynchronous-communication).

```markdown
Async issue update

**YYYY-MM-DD Update**

#### Please provide a quick summary of the current status (one sentence)

#### When do you predict this feature to be ready for maintainer review?

#### Are there any opportunities to further break the issue or merge request into smaller pieces (if applicable)?

#### Were expectations met from a previous update? If not, please explain why

```

### Experimentation

The Growth groups regularly run experiments to test product hypothesis.

- Read about the [experimentation process](experimentation/).
- View the [developer documentation](https://docs.gitlab.com/ee/development/experiment_guide/)
- View slides for the [Experimentation Workshop](https://docs.google.com/presentation/d/1nmStWChWkYad9K-dced9wS4jS7XLIrHB-WKafc7jrMU/)

GitLab team members are welcome to attend the Growth Stage Engineering Weekly meetings
to connect with growth team members and find out more about running experiments at GitLab.

### Growth Metrics

The Growth stage tracks number of experiments deployed as a development metric. This is not an individual or team performance indicator. This allows teams to track their technical debt.

New experiments added to the codebase using [experiment feature flags](https://docs.gitlab.com/ee/development/feature_flags/#experiment-type) are tracked until removal.
Current experiments shows the total number of experiments in the codebase (pending, active, or concluded and ready to be removed).

{{< tableau height="600px" toolbar="hidden" src="https://us-west-2b.online.tableau.com/t/gitlabpublic/views/Experimentscadenceandcurrentexperimentsdeployed/Experimentscadenceandcurrentexperimentsdeployed" >}}
{{< /tableau >}}

#### Growth Section Metrics

Complete list of [Growth Section engineering metrics](/handbook/product/groups/product-analysis/engineering/dashboards/growth/).

{{< tableau height="600px" toolbar="hidden" src="https://us-west-2b.online.tableau.com/t/gitlabpublic/views/TopEngineeringMetrics/TopEngineeringMetricsDashboard" >}}
  {{< tableau/filters "SECTION_LABEL"="growth" >}}
{{< /tableau >}}

{{< tableau height="600px" src="https://us-west-2b.online.tableau.com/t/gitlabpublic/views/MergeRequestMetrics/OverallMRsbyType_1" >}}
  {{< tableau/filters "SECTION_LABEL"="growth" >}}
{{< /tableau >}}

## Team Days

On occasion we hold virtual team days or meetings to take a break and participate in fun, social activities with our Growth counterparts.

- [FY23-Q2 2022](https://gitlab.com/gitlab-org/growth/team-tasks/-/issues/625)
- [December 2021](https://gitlab.com/gitlab-org/growth/team-tasks/-/issues/522)
- [April 2021](https://gitlab.com/gitlab-org/growth/product/-/issues/1675)
- [September 2020](https://gitlab.com/gitlab-org/growth/team-tasks/-/issues/175)
- [May 2020](https://gitlab.com/gitlab-org/growth/team-tasks/-/issues/119)

## Common Links

- [Growth stage](/handbook/engineering/development/growth/)
- [Growth workflow board](https://gitlab.com/groups/gitlab-org/-/boards/4152639)
- `#s_growth` in [Slack](https://gitlab.slack.com/archives/s_growth) (GitLab internal)
- [Growth opportunities](https://gitlab.com/gitlab-org/growth/product/-/issues)
- [Growth meetings and agendas](https://drive.google.com/drive/search?q=type:document%20title:%22Growth%20Weekly%22) (GitLab internal)
- [GitLab values](/handbook/values/)
