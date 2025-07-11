---
title: Global Search Group
description: "The Global Search team is focused on bringing world class search functionality to GitLab.com and self-managed instances."
---

## Vision

The Global Search Group focuses on bringing world class search functionality to GitLab.com and self-managed instances.

This page covers processes and information specific to the Global Search group. See also the [Global Search](https://about.gitlab.com/direction/global-search/) and [Code Search](https://about.gitlab.com/direction/global-search/code-search/) direction pages.

## Mission

The group is responsible for improving and expanding upon our current global search implementations using Elasticsearch, PostgreSQL, Zoekt, and Gitaly. Areas of responsibility will include global search functionality, UI, ingestion mechanisms, optimal indexing, administrative tools, and installation mechanisms for self-managed installations.

Additionally, we build and maintain critical AI context infrastructure, including:

- **AI Context Abstraction Layer**: A unified interface for Retrieval Augmented Generation (RAG) across multiple vector databases (Elasticsearch, OpenSearch, PostgreSQL with pgvector), enabling AI features to work regardless of underlying storage
- **GitLab Zoekt**: GitLab's scalable exact code search service and file-based database system, with flexible architecture supporting various AI context use cases beyond traditional search. It's built on top of open-source code search engine Zoekt.

These systems will be fundamental to providing high-quality context for AI features via Retrieval Augmented Generation work, which includes:

- Identifying and preparing new useful data for our AI-powered features in collaboration with feature teams and the AI Framework team
- Storing vector embeddings of epics, issues, MRs, source code, and more
- Providing retrieval APIs for those vector embeddings, metadata filtering, and ensuring permissions are enforced
- Enabling fast, precise code search and context retrieval essential for AI context

This team doesn't own custom searches for specific features, such as the "filter bar" on issues which is part of the [Issue Tracking](https://about.gitlab.com/direction/plan/project_management/team_planning/) category owned by the [Project Management group](/handbook/product/categories/#project-management-group).

## Team Members

The following team members are permanent members of the Global Search Group:

{{< team-by-manager-slug manager="cliu" role="Global Search|Core Platform" >}}

## Stable Counterparts

The following members of other functional teams are our stable counterparts:

| **Name**                                                 | **Role** |
| ---------------------------------------------------------| ------------------------------------------------------------------------------- |
| [Ben Venker](/handbook/company/team#bvenker)             | [Senior Product Manager, Global Search](/job-families/product/product-manager/) |
| [Ashraf Khamis](/handbook/company/team#ashrafkhamis)     | [Senior Technical Writer](/job-families/product/technical-writer/) |
| [Cleveland Bledsoe Jr](/handbook/company/team#cleveland) | [Senior Support Engineer](/job-families/engineering/support-engineer/) |
| [Brenda Nyaringita](/handbook/company/team#bnyaringita)  | [Support Engineer(EMEA)](/job-families/engineering/support-engineer/) |

## Shared Responsibilities

The Global Search team shares responsibilites with the AI Framework team in the area of ![Retrieval Augmented Generation](/images/handbook/engineering/ai/search/rag_ownership_framwework.png) (RAG). Specifically, we will collaborate in the data preparation stage and information retrieval stage of the RAG process.

## AI Context Infrastructure and Advanced Search data stores

![Global Search data stores and interfaces diagram](/images/global_search_interfaces.png)

The Global Search team maintains several key systems that power both traditional search and AI context capabilities:

### Core Infrastructure Components

- **Elasticsearch**: Powers Advanced Search functionality with full-text search, aggregations, and vector similarity search capabilities
- **GitLab Zoekt**: GitLab's scalable file-based database system providing exact code search with enterprise-scale performance (48+ TiB indexed on GitLab.com). Beyond code search, Zoekt's flexible architecture serves as a foundation for various AI context use cases
- **AI Context Abstraction Layer**: A unified Ruby gem interface enabling RAG across multiple vector databases (Elasticsearch, OpenSearch, PostgreSQL with pgvector), ensuring AI features work regardless of underlying storage solution

These systems work together to provide comprehensive search and AI context capabilities, from traditional keyword search to sophisticated vector similarity matching for AI features.

### Advanced Search as an Enabling Framework

Beyond powering GitLab's global search functionality, Advanced Search serves as a critical framework that enables other teams across GitLab to overcome the inherent limitations of PostgreSQL for complex search and analytics use cases. Teams leverage Advanced Search infrastructure to:

- **Scale beyond PostgreSQL constraints**: Handle large-scale text search, aggregations, and analytics that would be prohibitively expensive or slow in PostgreSQL
- **Enable sophisticated filtering**: Support complex multi-field queries, faceted search, and advanced filtering capabilities
- **Power analytics and insights**: Generate aggregations, statistics, and insights from large datasets without impacting primary database performance
- **Support AI and ML workflows**: Provide vector similarity search, embeddings storage, and retrieval capabilities essential for AI features

This framework approach allows feature teams to focus on their domain expertise while leveraging battle-tested, scalable search infrastructure maintained by the Global Search team.

### A note on basic search

Basic search utilizes Postgres for text searching and Gitaly for code searching. Both functionalities are significantly limited compared to with Advanced search.

## Current state of Advanced Search scopes

There are many data types and search scopes already available via the Advanced Search interfaces. Below is a table that outlines the various available data types and the status of various functional elements, such as permissions, cross-group searching, and embeddings.

| Data type / scope | Privacy / Permissions | Cross-namespace / cross-group searching | Keyword search | Similarity search & Embeddings | Metadata filtering |
|-------------------|-----------------------|-----------------------------------------|----------------|--------------------------------|--------------------|
| **Code** | Yes | Yes | Yes | In progress | Group, Project, Include/exclude archived, include/exclude forks, Language, Filename, Path, Extension |
| **Issues** | Yes | Yes | Yes | Yes | Group, Project, Status, Confidentiality, Labels, Include/exclude archived |
| **Merge requests** | Yes | Yes | Yes | No | Group, Project, Status, Include/exclude archived |
| **Epics** | Yes | Yes | Yes | No | Group, Project |
| **Comments** | Yes | Yes | Yes | No | Group, Project, Include/exclude archived |
| **Users** | Yes | Yes | Yes | No | Group, Project |
| **Commits** | Yes | Yes | Yes | No | Include/exclude archived |
| **Milestones** | Yes | Yes | Yes | No | Group, Project, Include/exclude archived |
| **Project** | Yes | Yes | Yes | No | Group |
| **Wiki** | Yes | Yes | Yes | No | Group, Project |

## Meetings

Whenever possible, we prefer to communicate asynchronously using issues, merge requests, and Slack. However, face-to-face meetings are useful for establishing a personal connection and addressing items that would be more efficiently discussed synchronously, such as blockers.

- The Global Search Group meets weekly on Tuesdays at 14:00 UTC.
- The Global Search Group also has an Open Discussion Hour on Thursdays at 12:30 UTC

## Work

We follow the general workflow and principles defined in [Product Development Flow](/handbook/product-development/product-development-flow/) and [Engineering Workflow](/handbook/engineering/workflow/). To bring an issue to our attention, please create an issue in the relevant project. Add the `~"group::global search"` label and any other suitable labels. If it is an urgent issue, please reach out to the Product Manager or Engineering Manager listed in the [Stable Counterparts](/handbook/engineering/ai/search/#stable-counterparts) section above.

Below are a few guidelines the team follows in the day-to-day work.

- We use asynchronous communication with each other and with other GitLab teams via GitLab, Slack, Google Docs, etc.
- We have weekly team meetings, 1-on-1 meetings, and virtual happy hours via Zoom to discuss various topics and create team bonding.
- We encourage all backend engineers in our team to have their changes reviewed by someone else in our group. It's great for knowledge sharing.
- We organize our tasks under Epics and Issues. The Product Manager and Engineering Manager go through the backlog at the planning phase of each release and put issues into the next one or two milestones. The issues on the [milestone board](https://gitlab.com/groups/gitlab-org/-/boards/1339901?label_name[]=group%3A%3Aglobal%20search) are sorted based on priority. The higher priority issues are placed on the top.
- We apply the Deliverable label to the issues that we intend to close in a milestone before the milestone starts. Issues added during a milestone should not have the Deliverable label applied. We review these issues in the middle of the milestone, usually the first week of each month. We will remove the Deliverable label from the issues that are not likely to make it into the release.
- We apply the Stretch label to the issues that we intend to start during a milestone but are not committing to closing.
- We work with the UX team for features that need their design input by labeling the issues with a UX workflow label and adding the corresponding UX team counterpart as the assignee. We use `workflow::problem validation` and `workflow::solution` validation for user research and `workflow::design` for UI design and prototyping. Once the design is finished, `workflow::ready for development` label will be added as an indicator that development can start. For minor UX/UI changes, we contact our UX counterpart or the Product Design Manager to request a review for fast iterations.
- We work with the Quality team for issues that require input from a testing perspective by labeling the issues with `workflow::planning breakdown` and adding the SET counterpart as an assignee. Once SET reviews the issue, they acknowledge back with the label [`quad-planning::complete-action` or `quad-planning::complete-no-action`](/handbook/product-development/product-development-flow/#build-phase-1-plan)
- We work with the Technical Writing team for issues that need documentation change by labeling the issues with <code>documentation</code> and adding our counterpart in the Technical Writing team as assignee. Our technical writer helps us update the corresponding document. The documentation change normally happens together with the code change.
- We work with our stable counterpart in the Security team for issues that need input from a security perspective. We suggest using team planning issues, for example, [this one](https://gitlab.com/gitlab-org/search-team/team-tasks/-/issues/17), for communication.
- We work with the Support Engineering team by collaborating on issues directly. We invite our counterpart in the Support Engineering team to our team meeting every month to have direct communication.
- When team members are ready for their next tasks, they will pick an issue from the milestone board and become the issue owner by assigning the issue to themselves. Team members should prioritize issues with the Deliverable label. The issue owner will be responsible for finding the solution to the issue. They can propose a solution by opening a Merge Request. They can also break down the issue into smaller sub-issues if it makes sense to take an iterative approach.
- Before going out of office for an extended time, assign items still in review to the Engineering Manager. The Engineering Manager can reassign as needed.
- Whenever a team member reviews an author's work that is out of office for an extended time, they are welcome to complete the changes requested if they deem themselves comfortable with the remainder of the work.
- We review and prioritize bugs every week. It is common for bugs to represent the problem without identifying the impact. Because the Product Management and QA share the responsibility of assessing every bug for priority, severity, and details. Severity uses an approximation of the Risk Matrix to identify potential risk and frequency. Priority is based on total impact over time. Occasionally, something of a lower priority/ severity will be added to a milestone when it relates to work currently scheduled.
    1. Review all new bugs for content, priority, severity, and milestones
    1. Review any bugs missing priority or severity
    1. Prioritize bugs for the current milestone. 10% of scheduled work should be focused on bugs
    1. Schedule bugs for future milestones based on capacity, severity, priority, and relationship to any scheduled work

### Breaking changes process

Before a major milestone starts, we prepare an epic with all the breaking change issues linked. As usual, we work to get approvals but keep the MR in draft to prevent it from merging before the major milestone. If an MR is independent, we can have the `master` as a target branch. If not, we can have a sequence of MRs with target branches set to each other. As soon as the first one merges, the next will automatically target `master`.

Every MR that was created before the breaking change milestone should have this or a similar warning in the description: `:warning: This MR must be kept as a draft and cannot be merged until **DATE** :warning:`

### Bugfix backport process

We review the bugfix merge requests every week. To facilitate this process, we have created scoped labels: `backport::required`, `backport::skip`, and `backport::complete`.

- The `backport::skip` label will be added to merge requests if no backport is needed.
- The `backport::required` label will be added to the merge requests that need to be backported to a previous release in the initial review. The DRI will follow the [patch release process](/handbook/engineering/releases/#patch-releases-overview) to backport the fix to a previous release. Once the backport is done, the `backport::complete` label will be added to indicate the whole process is complete.

### Advanced Global Search Rollout on GitLab.com

The team has been actively working on enabling Elasticsearch powered Advanced Search on GitLab.com. [Based on our analysis](https://gitlab.com/groups/gitlab-org/-/epics/1736), we set our first target to roll this feature out for all the paid groups on GitLab.com. You can find more details about the timeline and progress in the links below.

- [Plan of Advanced. Search Rollout on GitLab.com](https://gitlab.com/groups/gitlab-com/-/epics/649)
- [Steps and Enhancements of Advanced Search Rollout on GitLab.com](/handbook/engineering/ai/search/es-rollout-timeline/)

### Severity Labels for Search Issues (`~advanced search`, `~global search`)

| Type of Operation | `~severity::1` - Blocker | `~severity::2` - Critical | `~severity::3` - Major  | `~severity::4` - Low |
| ------------------|--------------------------|---------------------------|-------------------------|----------------------|
| Recall Record, Global | Above 10 seconds to timing out | Between 7 and 10 seconds | Between 4 and 7 seconds | Between 2 and 4 seconds |
| Time until inserted record is recallable | Above 15 minutes | Between 15 and 10 minutes | Between 10 and 5 minutes | Between 3 and 5 minutes|

The two types of operations we detail severity metrics for above are:

- Recall Record, Global: This is the time it takes to recall a record using a globally scoped search of GitLab.com. Records could be entities such as projects, users, groups, etc.
- Time until inserted record is recallable: This is the elapsed time between adding a new record and having that new record be recallable via a search. This process depends on many underlying technologies such as the [Go indexer](https://gitlab.com/gitlab-org/gitlab-elasticsearch-indexer), [Sidekiq queues](https://docs.gitlab.com/ee/development/advanced_search.html#how-does-it-work), and the Elasticsearch database.

### Weighting for Search Issues

We use the Fibonacci rating system to assign weights to Search issues. Below are a few guidelines when setting issue weight:

- Issues that include `~backend` and `~frontend` work should have the weights added for a total weight representative of the work effort.
- Spike issues are assigned a weight to help timebox the effort.
- Bugs will not be given a weight.
- Any issue weighted over 5 should be broken down into smaller iterative steps if the issue does not contain `~backend` and `~frontend` work.

| Weight | Description |
|--------|--------|
| 0      | No effort or trivial effort (example: Documentation typo or Feature Flag Rollout) |
| 1      | Low effort (No Database migrations or Advanced Search migrations) |
| 2      | Low-Medium effort |
| 3      | Medium effort |
| 5      | High effort |

### MR reviews

We have the following guidelines for doing reviews on Global Search Team MRs:

- The MR author is responsible for deciding if the initial or maintainer reviews should be done by a Global Search Team member and can indicate that in a comment or by assigning the reviewers.
- Draft status indicates that the MR is not ready to be merged, but the author could decide to assign a reviewer while in draft mode. Unless a review is urgent, the author should wait for the pipeline to pass before assigning a reviewer.
- We use [Conventional Comments](https://conventionalcomments.org/) to communicate effectively in review comments.
- The merge request author resolves only the threads they feel they have fully addressed and all discussions have been closed, anything else is resolved by the reviewer. When a merge request has many threads, it is helpful for the reviewer to go back to open threads to pick up where the previous discussions were left off.

### Oncall escalation coverage

As the Global Search Team requires special domain knowledge, such as Elasticsearch, we borrow team members with this domain knowledge from other groups to cover the on-call escalation when we are understaffing, especially during the holiday seasons. In general, we will follow the [dev](/handbook/engineering/development/processes/infra-dev-escalation/process/#escalation-process) on-call process. The Elasticsearch domain experts, identified by domain_expertise on their profile, may be contacted when SRE and dev on-call engineers cannot resolve the production incidents. We don't expect the domain experts to work outside their normal working hours. In case of emergency, we will follow the rules and best practices outlined in our [Incident Management](/handbook/engineering/infrastructure/incident-management/) handbook. To assist team members in catching up on the latest development status and resolving potential incidents, we have created a [Global Search Incident Management document](https://gitlab.com/gitlab-org/search-team/training-materials/-/tree/main/2021-12-14-production-incident-management) as a reference.

#### Onboard domain experts from other groups to cover production incident escalation

When onboarding domain experts from other groups to help cover production incident escalation, we may consider the following actions:

- Suggest the team member add `elasticsearch` as their `domain_expertise` in their team member profile
- Add the team member to the Slack group global-search-team which can be used by SREs and other on-call engineers to contact in case of emergency
- Create the access request for the team member to grant them access permissions to Elasticsearch cluster
- Schedule [walk-through sessions](https://youtu.be/dK-G-pLVRfE) with the team member to go over the latest architecture and development status

#### Offboard domain experts from production incident escalation coverage

- Remove the team member from the Slack group global-search-team
- Revoke the team member's access permission of Elasticsearch cluster

### Common Links

- [Global Search Team Milestone Board](https://gitlab.com/groups/gitlab-org/-/boards/1339901?label_name[]=group%3A%3Aglobal%20search)
- [Global Search Team Workflow Board](https://gitlab.com/groups/gitlab-org/-/boards/4440461?not[label_name][]=UX%20Paper%20Cuts&label_name[]=group%3A%3Aglobal%20search&milestone_title=Started)
- [Global Search Team Epics](https://gitlab.com/groups/gitlab-org/-/epics?scope=all&utf8=%E2%9C%93&state=opened&label_name[]=group%3A%3Aglobal%20search)
- Global Search team slack channel (internal) [#g_global_search](https://gitlab.slack.com/app_redirect?channel=g_global_search)
- [Global Search Roadmap](https://gitlab.com/groups/gitlab-org/-/roadmap?state=all&sort=start_date_asc&layout=MONTHS&timeframe_range_type=CURRENT_YEAR&label_name%5B%5D=group%3A%3Aglobal+search&label_name%5B%5D=Roadmap&progress=COUNT&show_progress=true&show_milestones=false&milestones_type=ALL)
- [Bug Review Board](https://gitlab.com/groups/gitlab-org/-/boards/2118530?label_name[]=type::bug&label_name[]=group%3A%3Aglobal%20search)

### JTBD

We utilize the [Jobs to be Done](/handbook/product/ux/jobs-to-be-done/) (JTBD) framework to better understand our customers' and users' needs. You can view the current list of our JTBD [here](/handbook/engineering/ai/search/jtbd/#jobs-to-be-done).

### Performance Testing

We are exploring [Rally](https://esrally.readthedocs.io/en/stable/) for performance testing the Elasticsearch cluster. Workload data is determined using Kibana and stored in a [Google Sheet](https://docs.google.com/spreadsheets/d/1K_MteuTEX0spu0jOiRt9BqDLZXywUhQ9NUw7PbU8odw/edit?usp=sharing) (internal)

## Resources

### Documentations

#### Search and Advanced Search

- [GitLab Elasticsearch Integration](https://docs.gitlab.com/ee/integration/advanced_search/elasticsearch.html)
- [GitLab Advanced Search Development Guidelines](https://docs.gitlab.com/ee/development/advanced_search.html)
- [GDK Elasticsearch Setup Instructions](https://gitlab.com/gitlab-org/gitlab-development-kit/-/blob/main/doc/howto/elasticsearch.md)

#### AI Context Infrastructure

- [Zoekt Design Document](/handbook/engineering/architecture/design-documents/code_search_with_zoekt/) - Comprehensive architecture and implementation details
- [GDK Zoekt Setup Instructions](https://gitlab.com/gitlab-org/gitlab-development-kit/-/blob/main/doc/howto/zoekt.md)
- [AI Context Abstraction Layer Design Document](/handbook/engineering/architecture/design-documents/ai_context_abstraction_layer/) - Unified RAG interface architecture
- [AI Context Abstraction Layer Source Code](https://gitlab.com/gitlab-org/gitlab/-/tree/master/gems/gitlab-active-context) - Ruby gem implementation

### Blog Posts

- [Lessons from our journey to enable global code search with Elasticsearch on GitLab.com](https://about.gitlab.com/blog/2019/03/20/enabling-global-search-elasticsearch-gitlab-com/)
- [Update: The challenge of enabling Elasticsearch on GitLab.com](https://about.gitlab.com/blog/2019/07/16/elasticsearch-update/)
- [Update: Elasticsearch lessons learnt for Advanced Global Search 2020-04-28](https://about.gitlab.com/blog/2020/04/28/elasticsearch-update/)
- [How the Search Team at GitLab Implemented a Risk Map to Direct Automated Testing Efforts](https://about.gitlab.com/blog/2020/09/03/risk-mapping/)
- [GitLab's data migration process for Advanced Search](https://about.gitlab.com/blog/2021/06/01/advanced-search-data-migrations/)

### Product Demos

- [GitLab search with Custom Search Engines](https://www.youtube.com/watch?v=YESlLDxHH4o)
- [Use the GitLab search bar to navigate](https://www.youtube.com/watch?v=OE9b0Qc6KaI)
- [Search suggestions for recently viewed issues and merge requests](https://www.youtube.com/watch?v=_5s4ZjnDZPo)
- [How to search for epics in GitLab](https://www.youtube.com/watch?v=bu6kaBqcYFc)
- [Elasticsearch Migrating Issues To Separate Index Technical Overview](https://youtu.be/1znFvPH_wjU)
