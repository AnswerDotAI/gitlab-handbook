---
title: Pipelines Table Redesign and GraphQL Migration
status: proposed
creation-date: "2025-04-04"
authors: ["@bsandlin", "@pburdette"]
coaches: ["@jivanvl"]
dris: ["@bsandlin", "@pburdette", "@jivanvl"]
owning-stage: "~devops::verify"
participating-stages:
    ["~group::pipeline execution", "~group::pipeline authoring"]
toc_hide: true
---

{{< engineering/design-document-header >}}

## Summary

**Associated Epic: [#17330: Pipelines Table Redesign and GraphQL Migration](https://gitlab.com/groups/gitlab-org/-/epics/17330)**

The Pipelines Table is a critical component of GitLab's CI/CD experience, appearing in three key locations throughout the application:

1. The main Pipelines page
2. The Commit Pipelines tab
3. The Merge Request Pipelines tab

The current implementation uses REST API and displays all information at once, including pipeline mini graphs for each pipeline. This has led to significant performance issues and a suboptimal user experience.

As the migration from REST to GraphQL for the Pipelines Table is already planned, this design document proposes combining this migration with a comprehensive UI redesign. The redesign will separate essential pipeline information from detailed data (like mini graphs and job information) using a progressive disclosure pattern, while the GraphQL implementation will enable more efficient data fetching and establish the foundation for future real-time updates.

By tackling both efforts simultaneously, we can significantly reduce development costs by avoiding temporary solutions and rework. This approach will improve initial load performance by reducing payload size and rendering complexity, enhance the user experience through better information hierarchy, and establish the technical architecture needed for eventual real-time pipeline status updates—all while maintaining feature parity for critical pipeline information.

![pipelines_table](/images/engineering/architecture/design-documents/pipelines_table_redesign/pipelines_table.png)

## Business Impact

### User Impact

The proposed redesign and migration will significantly improve the GitLab CI/CD experience by:

- **Improving Performance**: Reducing initial load time by 50%+, translating directly to increased developer productivity
- **Enhancing Information Access**: Implementing progressive disclosure to show essential information first while making details available on demand
- **Streamlining Troubleshooting**: Prioritizing failed jobs and actionable items in the expanded view to reduce MTTR
- **Addressing Current Issues**: Resolving multiple open issues related to Pipelines Table functionality, addressing long-standing user pain points
- **Preparing for Real-time Updates**: Establishing the foundation for future instantaneous pipeline status updates

### Business Value

This initiative delivers substantial business value through:

- **Infrastructure Cost Savings**: 30-40% reduction in CI/CD-related server load by eliminating polling and reducing payload sizes
- **Developer Efficiency**: Significant time savings across millions of daily pipeline interactions through faster load times and improved information hierarchy
- **Competitive Positioning**: Reinforcing GitLab's market position by addressing key performance concerns
- **Technical Debt Elimination and Prevention**: Eliminating significant existing technical debt while avoiding future rework by proactively implementing modern patterns and technologies

### Risk Mitigation

The implementation strategy includes several elements to mitigate potential business risks:

- **Feature Flag Approach**: The phased rollout behind a feature flag allows for controlled testing and monitoring, reducing the risk of disruption to critical workflows.
- **User Preference Toggle**: Providing users with the ability to switch between implementations ensures that those who rely heavily on the current interface can continue their work without interruption while adapting to the new design.
- **Feature Parity**: Maintaining feature parity for all critical pipeline information ensures that users don't lose functionality during the transition.
- **Comprehensive Metrics**: Detailed performance and user satisfaction metrics will be collected to validate improvements and identify any areas requiring adjustment.

### ROI Calculation

Based on preliminary estimates:

| Investment                                                                                      | Return                                                    |
| ----------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| Engineering effort: Partial allocation over ~4-5 milestones (approx 30% of engineers' time)     | 30-40% reduction in CI/CD-related server resources        |
| Product design effort: Partial allocation over ~2 milestones                                    | Measurable improvement in pipeline interaction efficiency |
| QA and validation effort: Partial allocation over ~1-2 milestones                               | Reduction in CI/CD-related support tickets                |
|                                                                                                 | Improved user satisfaction scores                         |
|                                                                                                 | Foundation for future real-time capabilities              |

## Motivation

### GraphQL Migration

The primary motivation for migrating the Pipelines Table from REST to GraphQL is to enable real-time updates for pipeline status information:

- **Enable Real-time Updates**: GraphQL subscriptions will allow us to deliver instantaneous pipeline status changes to users without inefficient polling mechanisms.
- **Reduce Server Load**: The current polling approach requires frequent, full-payload requests that unnecessarily consume server resources, particularly in environments with active CI/CD usage.
- **Eliminate N+1 Query Issues**: The current REST implementation suffers from N+1 query patterns when retrieving pipeline data, creating database performance bottlenecks. GraphQL's ability to batch and optimize queries will significantly reduce these database inefficiencies.
- **Improve Filtering Performance**: The GraphQL implementation will enable more efficient pipeline filtering by moving filter operations closer to the data source, reducing unnecessary data transfer and processing.
- **Optimize Network Traffic**: GraphQL allows precise specification of required data, significantly reducing payload sizes compared to REST endpoints that return fixed data structures.
- **Technical Alignment**: Most new GitLab features are being built with GraphQL, making this migration strategically aligned with the platform's technical direction and architecture.
- **Future Scalability**: As GitLab continues expanding its CI/CD capabilities, GraphQL provides a more flexible and scalable query language for accessing increasingly complex pipeline data structures.

### UI Redesign

The primary motivation for redesigning the Pipelines Table UI is to address critical performance issues caused by including the pipeline mini graph in the parent API request.

- **Excessive Initial Payload**: The current implementation includes detailed stage and job data for the mini graph in the initial request, significantly increasing payload size and processing time for each pipeline.
- **Information Architecture Improvement**: The current approach presents too much information at once (Hick's Law), making it difficult for users to quickly identify pipeline status. A redesign allows us to prioritize the most important information.
- **Unnecessary Data Loading**: Most users only need to view detailed mini graph information for a small subset of pipelines, yet we currently load this data for all visible pipelines.
- **Progressive Disclosure Opportunity**: By moving the mini graph and other detailed information to an expandable view loaded with a secondary request, we can drastically improve initial load performance while still providing access to all pipeline details.
- **Enhanced Pipeline Details**: Moving detailed information to a secondary request enables us to build a more robust Pipeline Details component that can include richer visualizations, comprehensive failed jobs information, and more detailed metrics without impacting initial page performance.

### Previous Work and Issues Addressed

This initiative builds upon previous efforts while comprehensively addressing identified UX pain points. By combining the GraphQL migration with UI redesign, we can make progress on:

#### Previous Migration Attempts

Several attempts to address pipeline table performance through GraphQL migration have not gained sufficient traction as standalone initiatives. While these efforts targeted individual components, our proposal addresses all three instances of the pipeline table throughout the application:

- **[Epic #11080: Migrate MR pipelines tab to GraphQL](https://gitlab.com/groups/gitlab-org/-/epics/11080)**
- **[Epic #16831: Migrate pipelines table to GraphQL](https://gitlab.com/groups/gitlab-org/-/epics/16831)**
- **[Issue #223264: Move pipelines page to GraphQL](https://gitlab.com/gitlab-org/gitlab/-/issues/223264)**
- **[Issue #223267: Move pipelines table filter search to GraphQL](https://gitlab.com/gitlab-org/gitlab/-/issues/223267)**

These previous efforts highlighted the need for pipeline table improvements but faced challenges in prioritization when treated as separate initiatives.

#### UX Issues by Complexity

The redesign also provides an opportunity to address several long-standing UX issues in a coordinated effort:

| High (Weight 3) | Medium (Weight 2) | Low (Weight 1) |
|:---------------:|:-----------------:|:--------------:|
| [#321517](https://gitlab.com/gitlab-org/gitlab/-/issues/321517)<br>Improve table layout | [#432373](https://gitlab.com/gitlab-org/gitlab/-/issues/432373)<br>Add created-at time | [#435814](https://gitlab.com/gitlab-org/gitlab/-/issues/435814)<br>Add missing tooltips |
| [#327900](https://gitlab.com/gitlab-org/gitlab/-/issues/327900)<br>Improve mini-graph UX | [#329513](https://gitlab.com/gitlab-org/gitlab/-/issues/329513)<br>Reevaluate tab headings | [#354074](https://gitlab.com/gitlab-org/gitlab/-/issues/354074)<br>Add skeleton loader |
| | [#300256](https://gitlab.com/gitlab-org/gitlab/-/issues/300256)<br>Improve "Triggered by me" | [#365616](https://gitlab.com/gitlab-org/gitlab/-/issues/365616)<br>Align buttons with design system |
| | [#339651](https://gitlab.com/gitlab-org/gitlab/-/issues/339651)<br>Add configuration options | |

Our user research indicates that pipeline performance and usability issues are consistently reported as significant pain points by users, yet addressing them has been repeatedly deprioritized in favor of new feature development.

## Goals

The primary goals of this initiative are:

### Performance Improvement

- Reduce initial page load time for the Pipelines Table by at least 50%
- Decrease the size of the initial data payload by at least 60%
- Improve client-side rendering performance by reducing initial DOM element count
- Eliminate polling in favor of efficiently designed GraphQL queries and future subscription capability

### User Experience Enhancement

- Improve information hierarchy by separating essential pipeline information from detailed data
- Create a more intuitive interface that allows users to quickly scan pipeline statuses
- Maintain feature parity for all critical pipeline information
- Achieve at least 80% user satisfaction in usability testing

### Technical Architecture

- Complete migration from REST to GraphQL for all pipeline table functionality
- Design and implement a component architecture that supports future real-time updates
- Create a separation between list-level data and detailed pipeline information

### Development Efficiency

- Implement both the UI redesign and GraphQL migration in a single coordinated effort
- Avoid creating temporary solutions or technical debt
- Develop behind a feature flag to enable controlled testing and rollout

## Non-Goals

- Implementation of real-time updates (though laying groundwork is in scope)
- Redesign of the pipeline mini graph
- Changes to the underlying CI/CD execution engine
- Migration of other CI/CD features to GraphQL (job logs, runner management, etc.)
- Changes to pipeline creation or configuration workflows

## Proposal

The proposed solution involves a complete redesign of the Pipelines Table coupled with a migration from REST to GraphQL. The new design will adopt a progressive disclosure pattern, showing only essential information at the list level while providing users with the ability to expand individual pipeline entries to access detailed information.

This approach will utilize two separate GraphQL queries:

1. A lightweight initial query that loads only essential pipeline data for the list view
2. A second, more detailed query that is only triggered when a user expands a specific pipeline

By combining these two initiatives into a single coordinated effort, we can achieve significant performance improvements while enhancing usability and setting the stage for future real-time updates, all while minimizing development costs.

### Information Architecture

The new design will separate pipeline information into two levels:

1. **List View (Essential Information)**

   - Pipeline status and finished timestamp
   - Pipeline ID and name
   - Branch, commit, and MR information
   - Author information
   - Quick actions

2. **Expanded View (Detailed Information)**

   _Appears when user expands a pipeline row_

   - Possibly pipeline mini graph visualization (see [Pipeline Mini Graph Placement](#pipeline-mini-graph-placement) decision)
   - Failed jobs information
   - Job actions
   - Duration metrics
   - Available artifacts
   - Detailed commit information
   - Configuration details

## Design and Implementation Details

### Implementation Approach

The implementation will be phased as follows:

**Phase 1: Design and Infrastructure** (1-2 milestones)

- Conduct product design sessions to finalize UI/UX requirements [**Design**]
- Create designs for both list view and expanded details [**Design**]
- Define information hierarchy and user interactions [**Design**]
- Introduce feature flag infrastructure [**BE/FE**]
- Update user preference schema to add `usePipelinesListView` (see [User Preference Implementation](#user-preference-implementation)) [**BE**]

**Phase 2: Foundation and Architecture** (1 milestone)

- Update GraphQL schema based on finalized designs [**BE**]
- Stub out query resolvers [**BE**]
- Build and test the details query [**BE**]
- Base component structure for list view [**FE**]
- Base component structure for details view [**FE**]

**Phase 3: Implementation and Integration** (1-2 milestones)

- Implement query resolvers and logic [**BE**]
- Implement user preference toggle for all 3 locations [**FE**]
- Build UI child components [**FE**]
- Query integration [**FE**]
- Conduct performance testing [**BE/FE**]
- Conduct user testing [**Design/FE**]

**Phase 4: Rollout and Monitoring** (1 milestone)

- Gradually enable feature flag
- Monitor performance metrics and toggle usage patterns
- Gather user feedback through dedicated feedback channels
- Adjust default toggle settings based on feedback and metrics
- Complete rollout when adoption and satisfaction metrics meet targets

### Contributors

The implementation of this initiative will require:

- 3-4 Frontend engineers
- 1-2 Backend engineers
- 1-2 UX/UI designers

### Key Design Decisions

#### List View Format

<details>
<summary>Details</summary>

**Decision DRI**: Product Design

**Decision**: [DECISION PENDING] Selection of the optimal list view format for the redesigned Pipelines Table.

**Context**: The current Pipelines Table uses a traditional table format with fixed columns, which presents all information at once and becomes visually complex with the pipeline mini graphs. A redesigned list view needs to balance information density with readability and usability, focusing on the most essential information while providing access to details when needed.

**Options to consider**:

- Row-based list view
- Card-based view
- Other

</details>

#### Detail View Interaction

<details>
<summary>Details</summary>

**Decision DRI**: Product Design

**Decision**: [DECISION PENDING] Selection of the optimal interaction method for accessing detailed pipeline information.

**Context**: With the introduction of the progressive disclosure pattern in the redesigned Pipelines Table, we need an effective way to display detailed pipeline information on demand. The component should provide sufficient space for comprehensive details while maintaining context and not disrupting the overall workflow.

**Options to consider**:

- Expandable row revealing details panel beneath the row
- Side drawer showing related pipeline details
- Other

</details>

#### User Preference Implementation

<details>
<summary>Details</summary>

**Decision DRI**: Product Design, Engineering

**Decision**: [DECISION PENDING] Whether to implement a user preference toggle to allow users to switch between the current Pipelines Table and the new redesigned version.

**Context**: As we transition from the current REST-based implementation to the GraphQL redesign, we need to provide users with a smooth migration path that allows them to access both versions during the transition period.

**Implementation**:

The user preference will be controlled with a GraphQL mutation:

```graphql
mutation updateUsePipelinesListView($usePipelinesListView: Boolean) {
    userPreferencesUpdate(
        input: { usePipelinesListView: $usePipelinesListView }
    ) {
        userPreferences {
            usePipelinesListView
        }
    }
}
```

The frontend will include a toggle component similar to the Work Items toggle that will:

- Display a badge indicating whether the new design is enabled
- Provide a popover with toggle control to switch between views
- Include a link to a dedicated feedback issue
- Handle preference persistence through the GraphQL mutation

**Rollout Strategy**:

1. **Initial Phase**: The feature will be enabled for internal GitLab users only, with the toggle defaulting to "Off"
2. **Beta Phase**: As confidence grows, the feature flag will be enabled for a wider audience, still with the toggle defaulting to "Off"
3. **Gradual Rollout**: Based on feedback and performance metrics, the toggle will gradually default to "On" for new users
4. **Full Rollout**: Eventually, the toggle will be removed and the redesigned implementation will become the standard

This approach enables users to try the new design while maintaining access to the familiar interface, facilitates feedback collection, provides a fallback mechanism, and creates a smoother transition experience.

</details>

#### Pipeline Mini Graph Placement

<details>
<summary>Details</summary>

**Decision DRI**: Product Design, Engineering

**Decision**: [DECISION PENDING] Whether to include the pipeline mini graph in the details view or focus on failed jobs and actionable items instead.

**Context**: The mini graph requires fetching extensive job data (including dozens of passed jobs with names and statuses) that is often unnecessary for the user's workflow.

**Options**:

1. **Include Mini Graph in Details View**

   - Provides visual representation of pipeline stages
   - Maintains familiar visualization element
   - Requires fetching data for all jobs, including non-actionable ones

2. **Focus on Failed Jobs and Actionable Items**

   - Prioritizes information users need to take action
   - Reduces data requirements by focusing on relevant jobs
   - Shows stage summary without individual passed job details
   - Potentially more useful for troubleshooting workflows

**Next Steps**:

- Research user workflows to identify most frequently needed information
- Analyze query patterns to measure reduction in data requirements
- Test alternative presentations focusing on actionable information

**Initial Recommendation**: Focus primarily on failed jobs and actionable items in the details view, with a simplified stage summary that doesn't require fetching data for every passed job.

</details>

#### GraphQL Query Structure

<details>
<summary>Details</summary>

**Decision DRI**: Engineering

**Decision**: Implement two separate GraphQL queries and prepare for future subscription model

**Context**: GraphQL allows for precise data fetching and real-time updates through subscriptions.

**Benefits**:

- Optimized initial payload
- On-demand loading of detailed information
- Foundation for real-time updates
- Better separation of concerns in frontend code

**Alternatives Considered**:

- Single comprehensive query with all data - Rejected due to performance concerns
- Multiple fragmented queries - Rejected due to increased request overhead

</details>

#### Pipeline Details Schema

<details>
<summary>Details</summary>

**Decision DRI**: Engineering

**Decision**: [PENDING UI DESIGNS] Determine the optimal GraphQL schema for pipeline details based on finalized UI designs.

**Context**: The schema for the secondary query will be driven by UI requirements to ensure we only fetch data needed for the expanded details view.

**Process**:

- Complete UI designs for the expanded pipeline details view
- Identify all data elements required by the design
- Develop schema that efficiently retrieves only necessary information
- Validate schema against performance goals

**Considerations**:

- Balance between comprehensive information and query efficiency
- Prioritize data for troubleshooting and actionable items
- Structure for future extensibility and real-time updates
- Support for all three pipeline table contexts

**Next Steps**:

- Finalize expanded details UI mockups
- Map UI elements to required data fields
- Draft initial GraphQL schema
- Review with stakeholders

**Implementation Target**: A focused schema that retrieves exactly what the UI needs without unnecessary data fetching.

</details>

### GraphQL Queries

The migration from REST to GraphQL for the Pipelines Table will involve creating two primary query patterns:

1. Lightweight list queries that retrieve only essential pipeline information for each context
2. A detailed query that fetches comprehensive information for a specific pipeline

<details>
<summary><h4>List Queries</h4></summary>

The list queries will be optimized for performance, retrieving only the data necessary for the initial list views. This approach significantly reduces the payload size compared to the current REST implementation. We will implement pagination and basic filtering capabilities from the start to ensure users do not lose current functionality, with additional filters to be added iteratively as needed.

We'll define a common fragment for all list queries to ensure consistency:

```graphql
# fragments/pipeline_list_fields.fragment.graphql
fragment PipelineListFields on Pipeline {
    id
    iid
    detailedStatus {
        ...CiIcon
    }
    createdAt
    finishedAt
    user {
        id
        name
        avatarUrl
        webUrl
    }
    commit {
        id
        shortId
        webUrl
    }
    mergeRequest {
        id
        webUrl
        reference
    }
    retryable
    cancelable
}
```

Then we'll implement three specific queries for each context where the Pipelines Table appears:

**Project Pipelines Query**:

```graphql
# queries/project_pipelines.query.graphql
query getProjectPipelines(
    $projectPath: ID!
    $first: Int
    $after: String
    $filters: PipelineFilterInput
) {
    project(fullPath: $projectPath) {
        id
        pipelines(first: $first, after: $after, filters: $filters) {
            pageInfo {
                hasNextPage
                endCursor
            }
            nodes {
                ...PipelineListFields
                # Project-specific fields will be added here
            }
        }
    }
}
```

**Merge Request Pipelines Query**:

```graphql
# queries/merge_request_pipelines.query.graphql
query getMergeRequestPipelines(
    $projectPath: ID!
    $mergeRequestIid: ID!
    $first: Int
    $after: String
) {
    project(fullPath: $projectPath) {
        id
        mergeRequest(iid: $mergeRequestIid) {
            id
            pipelines(first: $first, after: $after) {
                pageInfo {
                    hasNextPage
                    endCursor
                }
                nodes {
                    ...PipelineListFields
                    # MR-specific fields will be added here
                }
            }
        }
    }
}
```

**Commit Pipelines Query**:

```graphql
# queries/commit_pipelines.query.graphql
query getCommitPipelines(
    $projectPath: ID!
    $sha: String!
    $first: Int
    $after: String
) {
    project(fullPath: $projectPath) {
        id
        commit(sha: $sha) {
            id
            pipelines(first: $first, after: $after) {
                pageInfo {
                    hasNextPage
                    endCursor
                }
                nodes {
                    ...PipelineListFields
                    # Commit-specific fields will be added here
                }
            }
        }
    }
}
```

</details>

#### Details Query

The details query will be established once the UI designs for the expanded view are complete, as noted in the [Pipeline Details Schema](#pipeline-details-schema) decision.

### UI Component Architecture

[This structure will evolve once designs are complete]

```shell
ci/pipelines_list/
├── components/
│ ├── PipelinesListView.vue # Container component
│ ├── PipelineListItem.vue # Individual pipeline row component
│ └── PipelineDetails.vue # Expandable details component
│ ├── renderless/
│ │ ├── ProjectPipelinesQuery.vue # Renderless component for project pipelines query
│ │ ├── MergeRequestPipelinesQuery.vue # Renderless component for merge request pipelines query
│ │ └── CommitPipelinesQuery.vue # Renderless component for commit pipelines query
├── graphql/
│ ├── fragments/
│ │ └── pipeline_list_fields.fragment.graphql
│ ├── queries/
│ │ ├── project_pipelines.query.graphql
│ │ ├── merge_request_pipelines.query.graphql
│ │ ├── commit_pipelines.query.graphql
│ │ └── pipeline_details.query.graphql
│ ├── subscriptions/ # For future real-time updates
│ ├──── pipeline_statuses.subscription.graphql
│ └──── pipeline_details.subscription.graphql
├── constants.js
└── utils.js
```

## Alternative Solutions

### GraphQL Migration Without UI Redesign

**Approach**: Migrating to GraphQL while maintaining the current UI design.

**Pros**:

- Provides some performance benefits
- Allows incremental improvements
- Lower risk of user experience disruption

**Cons**:

- Requires building GraphQL queries that match current REST payloads
- Creates technical debt when UI is eventually redesigned
- Doesn't address information hierarchy or cognitive load issues
- Misses opportunity for combined implementation efficiency

## Metrics

To establish baseline performance measurements and set clear targets for improvement, we've gathered the following metrics across the locations where the Pipelines Table appears:

### Current Performance Baselines

| Location                    | Metric                                                            | Current Value | Target |
| --------------------------- | ----------------------------------------------------------------- | ------------- | ------ |
| Main Pipelines Page         | Average network response time (no filtering)                      | 1.35 seconds  | TBD    |
| Main Pipelines Page         | Average network response time (with trigger author/status filter) | 2.38 seconds  | TBD    |
| Merge Request Pipelines Tab | Average network response time                                     | 1.64 ms       | TBD    |

We'll measure the success of this initiative by comparing pre and post-implementation metrics across these dimensions, with specific improvement targets as outlined in the Goals section.

### Query Performance Comparison

To thoroughly evaluate the performance improvements of our proposed changes, we've conducted a comparative analysis of three different query approaches using the same test dataset (project pipelines) in a controlled test environment:

#### Query Approach Comparison

| Approach                    | Description                                                                       | Query Complexity                                       | Server Response Time | Payload Size | Client Processing Time |
| --------------------------- | --------------------------------------------------------------------------------- | ------------------------------------------------------ | -------------------- | ------------ | ---------------------- |
| Current REST Implementation | Fetches all pipeline data including mini graphs in a single request               | High (N+1 queries for stages/jobs)                     | 1.35 seconds         | 256 KB       | 450 ms                 |
| GraphQL Without UI Redesign | GraphQL implementation that maintains the same data structure as current REST API | Medium (Optimized queries but still fetching all data) | TBD                  | TBD          | TBD                    |
| GraphQL With UI Redesign    | Two-tier GraphQL approach with separate list and details queries                  | Low (Optimized for essential data only)                | TBD                  | TBD          | TBD                    |

#### Detailed Query Analysis

##### Current REST Implementation

**Endpoint**: `GET /api/v4/projects/:id/pipelines?per_page=20`

- **Complexity**: Triggers multiple database queries per pipeline for stages and jobs
- **Data Returned**: Complete pipeline data including all stages and jobs
- **Drawbacks**: Significant overhead for information that may not be viewed

##### GraphQL Without UI Redesign

**Endpoint**: GraphQL API with comprehensive pipeline data query

- **Complexity**: Reduced database queries through batch loading
- **Data Returned**: Same comprehensive dataset as REST
- **Expected Improvement**: Some efficiency gains through GraphQL optimization

##### GraphQL With UI Redesign

**Primary Endpoint**: GraphQL API with lightweight pipeline list query
**Secondary Endpoint**: GraphQL API with detailed pipeline information query (on-demand only)

- **Complexity**: Minimal database queries for essential data only
- **Data Returned**: Only data required for initial list view, with details fetched separately
- **Expected Improvement**: Significant reduction in payload size and processing time

#### Testing Methodology

The performance metrics were gathered using the following methodology:

- Test environment: Production GitLab instance
- Test project: Mid-sized project with 20 pipelines (standard pagination size)
- Measurement tools: Browser Developer Tools, GitLab performance monitoring
- Metrics captured: Server processing time, payload size, client rendering time
- Sample size: Average of 20 requests per implementation

#### Expected Performance Improvements

Based on preliminary testing, we anticipate the following improvements with the GraphQL UI redesign approach:

| Metric                | Expected Improvement |
| --------------------- | -------------------- |
| Server Response Time  | 65-70% reduction     |
| Initial Payload Size  | 75-80% reduction     |
| Client Rendering Time | 50-60% reduction     |
| Time to Interactive   | 60-65% reduction     |

These expectations will be validated with comprehensive testing during implementation, with actual measurements to be added once available.
