---
title: Product sections, stages, groups, and categories
---

{{% include "includes/product-handbook-links.md" %}}

## Interfaces

We want intuitive interfaces both within the company and with the wider
community. This makes it more efficient for everyone to contribute or to get
a question answered. Therefore, the following interfaces are based on the
product categories defined on this page:

- [Home page](https://about.gitlab.com/)
- [Product page](https://about.gitlab.com/stages-devops-lifecycle/)
- [Product Features](https://about.gitlab.com/features/)
- [Pricing page](https://about.gitlab.com/pricing/)
- [DevOps Lifecycle](https://about.gitlab.com/stages-devops-lifecycle/)
- [DevOps Tools](https://about.gitlab.com/why-gitlab/)
- [Product Direction](https://about.gitlab.com/direction/)
- [Stage visions](https://about.gitlab.com/direction/#devops-stages)
- [Documentation](https://docs.gitlab.com/)
- [Engineering](/handbook/engineering/) Engineering Manager/Developer/Designer titles, their expertise, and department, and team names.
- [Product manager](/handbook/product/) responsibilities which are detailed on this page
- [Our pitch deck](https://gitlab.highspot.com/spots/615dd7e3911d70c4887812a7), the slides that we use to describe the company
- [Strategic marketing](/handbook/marketing/brand-and-product-marketing/product-and-solution-marketing/) specializations

## Hierarchy

The categories form a hierarchy:

1. **Sections**: Are a collection of stages. We attempt to align these logically along common workflows like Dev, Sec and Ops.
Sections are maintained in [`data/sections.yml`](https://gitlab.com/gitlab-com/www-gitlab-com/blob/master/data/sections.yml).
1. **Stages**: are maintained in [`data/stages.yml`](https://gitlab.com/gitlab-com/www-gitlab-com/blob/master/data/stages.yml).
Each stage has a corresponding [`devops::<stage>` label](https://docs.gitlab.com/development/labels/#stage-labels) under the `gitlab-org` group.
1. **Group**: A stage has one or more [groups](/handbook/company/structure/#product-groups).
Groups are maintained in [`data/stages.yml`](https://gitlab.com/gitlab-com/www-gitlab-com/blob/master/data/stages.yml).
Each group has a corresponding [`group::<group>` label](https://docs.gitlab.com/development/labels/#group-labels) under the `gitlab-org` group.
1. **Categories**: A group has one or more categories. Categories are high-level
capabilities that may be a standalone product at another company. e.g.
Portfolio Management. To the extent possible we should map categories to
vendor categories defined by [analysts](/handbook/marketing/brand-and-product-marketing/product-and-solution-marketing/analyst-relations/).
There are a maximum of 8 high-level categories per stage to ensure we can
display this on our website and pitch deck.
(Categories that do not show up on marketing pages
show up here in _italics_ and do not count toward this limit.) There may need
to be fewer categories, or shorter category names, if the aggregate number of
lines when rendered would exceed 13 lines, when accounting for category names
to word-wrap, which occurs at approximately 15 characters.
Categories are maintained in [`data/categories.yml`](https://gitlab.com/gitlab-com/www-gitlab-com/blob/master/data/categories.yml).
Each category has a corresponding [`Category:<Category>` label](https://docs.gitlab.com/development/labels/#category-labels) under the `gitlab-org` group. Category maturity is managed in the product [Category Maturity Change](/handbook/product/categories/#changing-category-maturity) process
1. **Features**: Small, discrete functionalities. e.g. Issue weights. Some
common features are listed within parentheses to facilitate finding
responsible PMs by keyword.
Features are maintained in [`data/features.yml`](https://gitlab.com/gitlab-com/www-gitlab-com/blob/master/data/features.yml).
It's recommended to associate [feature labels](https://docs.gitlab.com/development/labels/#feature-labels) to a category or a group with `feature_labels` in [`data/categories.yml`](https://gitlab.com/gitlab-com/www-gitlab-com/-/blob/master/data/categories.yml?ref_type=heads) or [`data/stages.yml`](https://gitlab.com/gitlab-com/www-gitlab-com/-/blob/master/data/stages.yml?ref_type=heads).

Notes:

- Groups may have scope as large as all categories in a stage, or as small as a single category within a stage, but most will form part of a stage and have a few categories in them.
- Stage, group, category, and feature labels are used by the automated triage
operation ["Stage and group labels inference from category labels"](/handbook/engineering/infrastructure/engineering-productivity/triage-operations/).
- We don't move categories based on capacity. We put the categories in the stages where they logically fit, from a customer perspective. If something is important and the right group doesn't have capacity for it, we adjust the hiring plan for that group, or do [global optimizations](/handbook/values/#efficiency-for-the-right-group) to get there faster.
- We don't have silos. If one group needs something in a category that is owned by another group, go ahead and contribute it.
- This hierarchy includes both paid and unpaid features.

### Naming

Anytime one hierarchy level's scope is the same as the one above or below it, they can share the same name.

For groups that have two or more categories, but not _all_ categories in a stage, the group name must be a [unique word](/handbook/communication/#mecefu-terms) or a summation of the categories they cover.

If you want to refer to a group in context of their stage you can write that as "Stage:Group". This can be useful in email signatures, job titles, and other communications. E.g. "Monitor:Health" rather than "Monitor Health" or "Monitor, Health."

When naming a new stage, group, or category, you should search the handbook and main marketing website to look for other naming conflicts which could confuse customers or employees. Uniqueness is preferred if possible to help drive clarity and reduce confusion. See additional [product feature naming guidelines](/handbook/product/categories/gitlab-the-product/#factors-in-picking-a-name) as well.

### More Details

Every category listed on this page must have a link to a direction page. Categories may also have documentation and marketing page links. When linking to a category using the category name as the anchor text (e.g. from the chart on the homepage) you should use the URLs in the following hierarchy:

Marketing product page > docs page > direction page

E.g Link the marketing page. If there's no marketing page, link to the docs. If there's no docs, link to the direction page.

### Solutions

[Solutions](/handbook/marketing/use-cases/) can consist of multiple categories and are typically used to align to a customer challenge (e.g. the need to reduce security and compliance risk) or to market segments defined by analysts such as Software Composition Analysis (SCA). Solutions are also often used to align to challenges unique to an industry vertical (e.g. financial services), or to a sales segment (e.g. SMB vs Enterprise).

Solutions typically represent a customer challenge, and we define how GitLab capabilities come together to meet that challenge, with business benefits of using our solution.

Market segments defined by analysts don't always align to GitLab stages and categories and often include multiple categories. Two most frequently encountered are:

1. Software Composition Analysis (SCA) = Dependency Scanning + License Compliance + Container Scanning
1. Enterprise Agile Planning (EAP) = Team Planning + Planning Analytics + Portfolio Management + Requirements Management

We are [intentional in not defining SCA as containing SAST and Code Quality](https://gitlab.com/gitlab-com/www-gitlab-com/merge_requests/26897#note_198503054) despite some analysts using the term to also include those categories.

### Capabilities

Capabilities can refer to stages, categories, or features, but not solutions.

### Layers

Adding more layers to the hierarchy would give it more fidelity but would hurt
usability in the following ways:

1. Harder to keep the [interfaces](#interfaces) up to date.
1. Harder to automatically update things.
1. Harder to train and test people.
1. Harder to display more levels.
1. Harder to reason, falsify, and talk about it.
1. Harder to define what level something should be in.
1. Harder to keep this page up to date.

We use this hierarchy to express our organizational structure within the Product and Engineering organizations.
Doing so serves the goals of:

- Making our groups externally recognizable as part of the DevOps lifecycle so that stakeholders can easily understand what teams might perform certain work
- Ensuring that internally we keep groups to a reasonable number of stable counterparts

As a result, it is considered an anti-pattern to how we've organized for categories to move between groups out
of concern for available capacity.

When designing the hierarchy, the number of sections should be kept small
and only grow as the company needs to re-organize for [span-of-control](/handbook/company/structure/#management-group)
reasons. i.e. each section corresponds to a Director of Engineering and a
Director of Product, so it's an expensive add. For stages, the DevOps loop
stages should not be changed at all, as they're determined from an [external](https://en.wikipedia.org/wiki/DevOps_toolchain)
source. At some point we may
change to a different established bucketing, or create our own, but that will
involve a serious cross-functional conversation. While the additional value
stages are our own construct, the loop and value stages combined are the primary
stages we talk about in our marketing, sales, etc. and they shouldn't be changed
lightly. The other stages have more flexibility as they're not currently
marketed in any way, however we should still strive to keep them as minimal as
possible. Proliferation of a large number of stages makes the product surface
area harder to reason about and communicate if/when we decide to market that
surface area. As such, they're tied 1:1 with sections so they're the
minimal number of stages that fit within our organizational structure. e.g.
Growth was a single group under Enablement until we decided to add a Director
layer for Growth; then it was promoted to a section with specialized
groups under it. The various buckets under each of the non-DevOps stages are
captured as different groups. Groups are also a non-marketing construct, so we
expand the number of groups as needed for organizational purposes. Each group
usually corresponds to a backend engineering manager and a product manager, so
it's also an expensive add and we don't create groups just for a cleaner
hierarchy; it has to be justified from a [span-of-control](/handbook/company/structure/#management-group)
perspective or limits to what one product manager can handle.

### Category Statuses

Categories can have varying level of investment and development work. There are four main investment statuses:

1. Accelerated - Top category for product strategy that has received additional investment in the next year
1. Sustained - Categories where new features will be added in the next year
1. Reduced - Categories where scope and ambition is decreased although, new features will still be added in the next year
1. Maintenance - Categories where no new features will added

Typically, product direction pages will transparently state the investment status of the category for the fiscal year based on annual product themes and investment levels.

## Changes

The impact of changes to sections, stages and groups is felt [across the company](/handbook/company/structure/#product-groups).

All new category creation needs to be specifically approved via our Opportunity Canvas review process. This is to avoid scope creep and breadth at the expense of depth and user experience.

Merge requests with
changes to sections, stages and groups and significant changes to categories
need to be created, approved, and/or merged by each of the below:

1. Chief Product Officer
1. PLT Leader relevant to the affected Section(s)
1. The Director of Product relevant to the affected Section(s)
1. The Director of Engineering relevant to the affected Section(s)
1. Director of Product Design

_**Note:** Chief Product Officer approval should be requested once all other approvals have been completed. To request approval, post the MR link in the #chief-product-officer channel tagging both the Chief Product Offcer and cc'ing the EBA to the Chief Product Officer.

The following people need to be on the merge request so they stay informed:

1. Chief Technology Officer
1. Development Leader relevant to the affected Section(s)
1. VP of Infrastructure & Quality Engineering
1. VP of UX
1. Director, Technical Writing
1. Engineering Productivity (by @ mentioning `@gl-quality/eng-prod`)
1. The Product Marketing Manager relevant to the stage group(s)

After approval and prior to merging, ping the Engineering Manager for Quality Engineering  in the MR, if there are changes that:

- Add a new category, group, stage or section
- Move an existing category to a new or existing group
- Move an existing group to a new or existing stage
- Move an existing stage to a new or existing section
- Rename a group, stage or section
- Delete a group, stage or section

This is to ensure that [GitLab Bot auto-labeling](/handbook/engineering/infrastructure/engineering-productivity/triage-operations/#auto-labelling-of-issues-and-merge-requests) can be updated prior to the change, which can be [disruptive if missed](https://gitlab.com/gitlab-org/quality/triage-ops/-/issues/467#note_337325686).

Upon approval, tag the group Technical Writer in the merge request to ensure [documentation metadata](https://docs.gitlab.com/development/documentation/#stage-and-group-metadata) is updated after the category change is merged.

Ensure that relevant slack channels are updated following our [slack channel naming convention](/handbook/communication/chat/#channel-categories), open an [access request](/handbook/security/corporate/end-user-services/onboarding-access-requests/access-requests/) to have slack channel names updated as they can no longer be updated by creators.

### Examples

Because it helps to be specific about what is a significant change and what should trigger the above
approval process, below are non-exhaustive lists of examples that would and would not, respectively, require full approvals as outlined above.

Changes that require the above approvers include:

- Changes to a section, stage, group, or category name or `marketing` attribute
- Removal or addition of a section, stage, group, or category

Changes that require approval only from the relevant [Product Leadership Team](/handbook/product/product-leaders/product-leadership/#product-leadership-team-structure) member include:

- Changing name or removing a non-marketing category, per the `marketing` attribute.

Changes that require approval only from the relevant Product Director include:

- Changing a category maturity date
- Changes to section or group member lists
- Changes to a category vision page

### Changing group name

When changing the name of a group, create a merge request to change the group name in [`data/stages.yml`](https://gitlab.com/gitlab-com/www-gitlab-com/blob/master/data/stages.yml)
using the [Group-Stage-Category-Change](https://gitlab.com/gitlab-com/www-gitlab-com/-/blob/master/.gitlab/merge_request_templates/Group-Stage-Category-Change.md) template,
and make sure to complete all the steps in the template.

When changing the team tags, such as `be_team_tag`, ensure that each team member's individual `data/team_members/person/` YAML has the relevant `departments` entry updated. Alternatively, if the team tag is missing, add the tag under the list of `departments` as the second or lower entry. The first `departments` entry is controlled by the Workday sync and will be overwritten.

When deciding on the naming, ensure that each team tag is unique. For example, `sre_team_tag` should have a different value compared to `be_team_tag`. If they are the same, then all team members with the tag with be displayed, duplicating the list for BE and SRE.

### Changing category name

When changing an existing category name, there are some considerations to the order of events:

- First, create a MR to change the name in [`data/stages.yml`](https://gitlab.com/gitlab-com/www-gitlab-com/blob/master/data/stages.yml) and `spec/homepage/category_spec.rb`.
- Get sign off from all required stakeholders listed in the instructions above.
- Merge the name change MR.
- Tag the category's technical writer so that they can update the documentation metadata
- Re-name the category [direction page](https://about.gitlab.com/direction/) with a new MR. Search for the old category name on the category direction page to ensure the name has been updated in all places.
- Use the `#it-help` Slack channel to request an update to Slack channel name for the re-named category

### Changing category maturity

We primarily use the [Category Maturity Scorecard](/handbook/product/ux/category-maturity/category-maturity-scorecards) process to determine category maturity.

Typically, category maturity moves up from planned to minimal to viable to complete to lovable. However, maturity can also be downgraded. For example, in cases where we discover a JTBD is not met (see [example](https://gitlab.com/gitlab-com/www-gitlab-com/-/merge_requests/74367)), or when we [change the definition of maturity](https://gitlab.com/gitlab-com/www-gitlab-com/-/merge_requests/92858), we may choose to move category maturity down.

When downgrading product maturity, we adjust our customer's current expectations about our product. This is particularly impactful to our go-to-market team members in customer success and product marketing. We need to do the following to enable alignment between all affected and interested parties:

- Raise an MR for the downgrade and clearly state the reasons for change in the description (see [example](https://gitlab.com/gitlab-com/www-gitlab-com/-/merge_requests/74367))
- Inform VP, Product Management by adding them as Reviewer on the MR
- Notify the product group counterparts in the MR; Product Marketing, Product Designer, Engineering Manager, and Technical Writer
- Post the MR in the [#customer-success slack channel](https://gitlab.slack.com/archives/C5D346V08) prior to merging, to allow the team to assess impact and adjust
- Post the MR in the [#product slack channel](https://gitlab.slack.com/archives/C0NFPSFA8) for awareness

## DevOps Stages

![Dev Ops Diagram](/images/product/categories/devops-diagram.svg)

{{% product/categories %}}

## Possible future Stages

We have boundless [ambition](/handbook/product/product-principles/#how-this-impacts-planning), and we expect GitLab to continue to add new stages to the DevOps lifecycle. Below is a list of future stages we are considering:

1. Data, maybe leveraging [Meltano product](https://meltano.com/)
1. Networking, maybe leveraging some of the [open source standards for networking](https://www.linux.com/news/5-open-source-software-defined-networking-projects-know/) and/or [Terraform networking providers](https://developer.hashicorp.com/terraform/language/providers)
1. Design, we already have [design management](https://gitlab.com/groups/gitlab-org/-/epics/1445) today

Stages are different from the [application types](https://about.gitlab.com/direction/#maturity) you can service with GitLab.

## Maturity

Not all categories are at the same level of maturity. Some are just minimal and
some are lovable. See the [category maturity page](https://about.gitlab.com/direction/#maturity) to see where each
category stands.

## Other functionality

This list of other functionality so you can easily find the team that owns it.
Maybe we should make our features easier to search to replace the section below.

### Other functionality in Plan stage

[Plan](/handbook/product/categories/#plan-stage) stage

#### Project Management group

[Project Management group](/handbook/product/categories/#project-management-group)

- assignees
- milestones
- due dates
- labels
- issue weights
- quick actions
- email notifications
- to-do list
- Real-time features

#### Knowledge group

[Knowledge group](/handbook/product/categories/#knowledge-group)

- markdown functionality
- rich text editor

### Other functionality in Create stage

[Create](/handbook/product/categories/#create-stage) stage

#### Code Review group

[Code Review group](/handbook/product/categories/#code-review-group)

- [Merge Requests](https://docs.gitlab.com/user/project/merge_requests/)
- [GitLab CLI](https://gitlab.com/gitlab-org/cli)

#### Remote Development group

[Remote Development group](/handbook/product/categories/#remote-development-group/)

- [GitLab Workflow extension for Visual Studio Code](https://docs.gitlab.com/editor_extensions/visual_studio_code/)

### Other functionality in Verify

#### CI Group

[CI Group](#ci-group)

- [CI Abuse Response](https://gitlab.com/gitlab-com/www-gitlab-com/-/issues/11678)

#### Pipeline Authoring Group

[Pipeline Authoring Group](#pipeline-authoring-group)

- [CI/CD Template Management and Contributions](https://docs.gitlab.com/development/cicd/templates/)

### Other functionality in Monitor stage

[Monitor stage](/handbook/product/categories/#monitor-stage)

### Other functionality in Engineering Productivity

[Engineering Productivity](/handbook/engineering/infrastructure/engineering-productivity/)

- [GDK](/handbook/engineering/infrastructure/engineering-productivity/gdk/)

### Other functionality in Developer Experience

[Developer Experience](/handbook/engineering/infrastructure-platforms/developer-experience/)

- [Reference Architectures](https://docs.gitlab.com/administration/reference_architectures/)
- [GitLab Environment Toolkit (GET)](https://gitlab.com/gitlab-org/gitlab-environment-toolkit)
- [GitLab Performance Tool (GPT)](https://gitlab.com/gitlab-org/quality/performance)
- [Performance Test Data](https://gitlab.com/gitlab-org/quality/performance-data)
- [Zero Downtime Testing Tool](https://gitlab.com/gitlab-org/quality/zero-downtime-testing-tool)

Internal Customers: [Gitaly](/handbook/engineering/infrastructure-platforms/data-access/gitaly/), [SaaS Platforms section](/handbook/engineering/infrastructure/platforms/), [Infrastructure Department](/handbook/engineering/infrastructure/), [Support Department](/handbook/support/), [Customer Success](/handbook/customer-success/)

### Other functionality in Analytics

[Analytics](/handbook/product/categories/#analytics-stage)

#### Product Analytics group

[Product Analytics group](/handbook/product/categories/#product-analytics-group)

- [Analytics Dashboards](https://docs.gitlab.com/user/product_analytics/#product-analytics-dashboards) - used by many groups to add visualizations or provide pre-configured dashboards to users

### Facilitated functionality

Some product areas are have a broad impact across multiple stages. Examples of this include, among others:

- Shared project views, like the [project](https://docs.gitlab.com/user/project/#projects) overview and settings page.
- Functionality specific to the [admin area](https://docs.gitlab.com/administration/settings/) and not tied to a feature belonging to a particular stage.
- UI components available through our design system, [Pajamas](https://design.gitlab.com/).
- Dashboards for displaying analytics, such as Product Analytics, Value Stream Analytics, and others.

While the mental models for these areas are maintained by specific stage groups, everyone is encouraged to contribute within the guidelines that those teams establish. For example, anyone can contribute a new setting following the established guidelines for Settings. When a contribution is submitted that does not conform to those guidelines, we merge it and "fix forward" to encourage innovation.

If you encounter an issue falling into a facilitated area:

- For issues that relate to updating the guidelines, apply the `group::category` label for the facilitating group.
- For issues that relate to adding content related to a facilitated area, apply the `group::category` label for the most closely related group. For example, when adding a new setting related to Merge Requests, apply the `group::source code` label.

### Shared responsibility functionality

There are certain product capabilities that are foundational in nature and affect or refer to horizontal components of the architecture that have an impact across functional groups and stages.

These capabilities may refer to "Facilitated Functionality" (see section above) where the mental models are owned by a particular group, while anyone can contribute. However, there may be others that will not have a clear owner because they don't fall squarely into any particular group's purview of product categories. Prime examples of this are issues related to the improvement or evolution of foundational components, frameworks and libraries that are used by several or all groups across the organization. Another example could be components created by special task groups in the past that have been since dissolved and that have not required continued development to justify the funding of a dedicated permanent group to maintain them.

Whatever the source of the functionality, rather than thinking of these components as "not having an owner", it is important to think of them as being owned by everyone through the lens of shared responsibility. "Shared responsibility" means that every group should be committed and responsible to **contribute** to their continued maintenance, improvement and innovation.

**Contribution**, in this context, may manifest in different ways:

- Triage by coordinating conversations with stakeholders from different functions and at different levels to find the right owner and/or set the right level of priority.
- Product feature scoping and UX design by fleshing out the details of implementation in requirements documents and/or mockups.
- Technical scoping and feasibility analysis for possible technical and architectural approaches to implementation
- Actual implementation and release activities

It does not mean, however, that a single group should necessarily be solely responsible for all of these activities. Multiple groups could end up collaborating in execution. This coordination however requires a careful triage of the shared responsibility issues in the issue tracker where a single [DRI](/handbook/people-group/directly-responsible-individuals/) coordinates these activities.

For more information please review [this section in the quality department handbook](/handbook/engineering/infrastructure/engineering-productivity/issue-triage/#shared-responsibility-issues) to learn more about a decentralized approach to triaging these types of issues.

### Categories A-Z

<!-- To edit the content of the Categories index, see: https://gitlab.com/gitlab-com/www-gitlab-com/-/blob/master/data/stages.yml -->

{{< product/categories-index >}}
