---
title: "AI Model Selection"
status: ongoing
creation-date: "2024-09-11"
authors: [ "@shekharpatnaik" ]
coaches: []
dris: [ "@sean_carroll" ]
approvers: [ "@jordanjanes", "@sean_carroll" ]
owning-stage: "~devops::ai-powered"
participating-stages: []
toc_hide: true
---

<!-- Design Documents often contain forward-looking statements -->

<!-- This renders the design document header on the detail page, so don't remove it-->
{{< engineering/design-document-header >}}

## Background

A growing number of AI models—both open-source and proprietary—are continually emerging, each with distinct characteristics such as latency, maximum token length, training approach, and output quality. Today, GitLab Duo relies on a fixed set of models for features like Code Suggestions, Chat, Duo Code Review, and Vulnerability Analysis. This rigidity limits administrators, operations teams, and end users in selecting the model that best suits their needs.

Additionally, whenever we introduce a new sub-processor or model, customers must undertake a thorough review and threat assessment process. These procedures that can span several months. This review is crucial for compliance and governance but also slows our ability to adopt new and potentially better-performing models.

In light of these challenges, we need an end-to-end solution that spans multiple feature groups to allow flexible model selection. This blueprint outlines the technical architecture required to integrate model selection options throughout GitLab Duo, providing administrators, operators, and end users with fine-grained control over which models can be used while also streamlining the governance and compliance workflow. For further background, please see [Issue #513430](https://gitlab.com/gitlab-org/gitlab/-/issues/513430).

## Current State

**Model Switching with Feature Flags:**

On gitlab.com and Self-Managed instances, model selection is currently controlled by feature flags. These flags are typically toggled on or off by an administrator or operations user. Because these flags apply at the instance level rather than at a user or group level, individual users and enterprises do not have the freedom to switch between different models based on their specific tasks.

**Self-Hosted Model Configuration:**

For Self-Managed installations, administrators can configure self-hosted models at an instance level. While this allows some flexibility in choosing or updating models, it still does not permit end users (developers) to select models on a per-feature basis in the UI or IDE. Furthermore, .com customers currently have no governance mechanism to specify which models their organization members can use.

## Phases

We can deliver this work in iterations so that we deliver value to the customer incrementally

**Iteration 1: Top-level Namespace Configuration**: In this phase, customers will be able to select a model for each feature at the root namespace level. This will allow .com customers to decide which models they want their namespace to use.
The model used for a given action will be the one set by the top-level namespace, depending on the context the user is in (project or namespace).
Related [epic](https://gitlab.com/groups/gitlab-org/-/epics/17570).

**Iteration 2: Consilidatating feature release**
Related [epic](https://gitlab.com/groups/gitlab-org/-/epics/18092).

**Future Iterations and considartion**
**Sub-level Namespace Cascading Configuration**:
Child namespaces will be able to assign a specific model for each feature as they did in the top-level iteration. In addition to that, they will be able to select a subset of available models for their downstream namespaces to choose from.
The model used for a given action will be the one set by the closest upstream namespace, including the current namespace, with a feature setting configured, depending on the context the user is in.
We will wait for further demand before considering planning this iteration. Related [Issue](https://gitlab.com/gitlab-org/gitlab/-/issues/514948).

**Oraganization-Level Configuration**: In this phase we enable managed model configuration for `.com`, `self-managed` and `dedicated` at the organiz level. Supported models are stored in the AI Gateway. These models will then be retrieved by gitlab.com, Self-managed instances and dedicated instances. _This is currently not planned as Organizations are not GA_

Future iterations will cover the ability to let users decide which model to use for a specific feature in both the IDE and the GitLab UI. Users would be able to select from a subset selected at the namespace level. Tracking of these features can be found in [this Epic](https://gitlab.com/groups/gitlab-org/-/epics/17720).

We will build out the capabilities for model switching in Duo Code Review, Vulnerability analysis and other features. In addition to this we also want to allow self hosted customers to bring their own models.

> Note: This design does not handle the scenario where we might want to pick from different `recommended_model`s based on the user query. For example we might want to pick `Google Gemini` when the context length becomes very large or `Claude Sonnet` when its a coding related question. Dynamic model switching would have to be covered in a separate blueprint.

## New Design (End State)

This represents the end state and is not broken down by phase. Every phase would deliver a section of this architecture.

### Data Model

The data model is designed to provide a structured way for organizations to manage AI feature settings at different levels. It allows **namespace administrators** to define default AI models for various features (e.g., Code Suggestions, Chat, etc.), while also enabling **individual users** to override these defaults with their preferred AI models.

The objective is to balance administrative control with user flexibility, ensuring that AI-powered features align with both organizational policies and personal preferences.

```mermaid
erDiagram
    NAMESPACES {
        bigint id PK
        bigint parent_id FK
        bigint owner_id FK
        varchar name
        varchar path
        bigint organization_id FK
    }

    NAMESPACE_FEATURE_SETTINGS {
        bigint id PK
        bigint namespace_id FK
        timestamp created_at
        timestamp updated_at
        smallint feature
        varchar offered_model_ref
        varchar offered_model_name
    }

    NAMESPACES ||--o{ NAMESPACE_FEATURE_SETTINGS : "has many"

    USERS {
        bigint id PK
        varchar username UNIQUE
        varchar email UNIQUE
    }

    USER_AI_MODEL_PREFERENCES["USER_AI_MODEL_PREFERENCES (Future Iteration)"] {
        bigint id PK
        bigint user_id FK
        varchar feature
        varchar favourite_model
    }

    USERS ||--o{ USER_AI_MODEL_PREFERENCES : "has many"
```

#### **Entities and Relationships**

##### **1. NAMESPACES**

- Represents groups/subgroups in GitLab.
- **Existing**

##### **2. NAMESPACE_FEATURE_SETTINGS**

- A set of features enabled for the namespace.
- This table consists of a feature category (such as Duo Chat) and a feature (such Code Completion)
- This also stores the Namespace level recommended model
- **New**
- **Why?**
  - We need to enable group admins to optionally set the models they want to use for each of the features.

##### **5. NAMESPACE_AI_FEATURE_MODELS**

- Stores a list of allowed models for each feature. If this list if empty then we will show all the GitLab supported models to the user
- **Future**

##### **6. USERS**

- Represents individual users who can interact with AI features.
- **Existing**

##### **7. USER_AI_MODEL_PREFERENCES**

- Allows users to select their **preferred AI model** per feature, overriding the namespace default.
- **Future**
- **Why?**
  - Empowers users with flexibility while maintaining organizational defaults.
  - Allows for personalization of AI-assisted workflows.

> **Note**: An `organization_id` field will be added to AI_SELF_HOSTED_MODELS, AI_FEATURE_SETTINGS and USER_AI_SETTINGS so that those work with cells.

#### **Key Design Considerations**

##### **1. Default & Override Mechanism**

- **Namespace Admins** define default AI models for each feature.
- **Users** can override these defaults for personal preferences (in the future).
- **Fallback Logic:**
  1. Check `USER_AI_SETTINGS` for user preference.
  2. If no user preference, check namespace in `NAMESPACE_FEATURE_SETTINGS`.
  Currently we just check the top-level namespace default.
  In future iteration we might check for namespace selection cascadingly (from the closest parent to the root ancestor).
  3. If no namespace default, revert to a system-wide default.
- **Why?**
  - Ensures a structured decision-making process.
  - Gives users autonomy without breaking organizational policies.

##### **2. Scalability & Performance**

- We need to be able to hierarchically look up the list of models across
  the namespace hierarchy.

##### **3. Incident management** 

- When the default model is selected or when model selection is disabled, an incident management mechanism is being put in place. The mechanism that will be implemented in AI Gateway will re-route the call to another model when the default model can't respond. Related [issue](https://gitlab.com/gitlab-org/gitlab/-/issues/478067).

- When a model has been selected for a feature by the user, we can't perform any incident management due to the fact that the user's choice needs to be respected. The user needs to be aware of this behavior.

##### **4. Flexibility for Deprecation**

- We need to be able to think about how administrators can deprecate models
  and what the process would be to cascade that down to other levels and the database performance implications of that.

### Changes to GitLab rails

1. The list of instance-level models is fetched from AI Gateway when a user is interacting with the model selection settings page and cached in the instance for an hour.

1. We need a way to sync models to all cells in `.com` and all self managed instances. This could be done using a separate sidekiq job that will sync GitLab Managed models with each cell and the self-managed instance.

```mermaid
sequenceDiagram
    Self Managed->>Cloud Connector: Scheduled Sidekiq job calls API
    Cloud Connector->>AI Gateway: Fetch Model List
    AI Gateway->>AI Gateway: Fetch Model List
    AI Gateway-->>Cloud Connector: Return list of models
    Cloud Connector-->>Self Managed: Return list of models
    Self Managed->>Self Managed: Insert model records and set defaults
    Self Managed->>Administrator: Send email about new model availability
```

1. We built the rails models, controllers and views as described in the `Data Model` section for the first itiration.

1. Every feature when making an API call to AI Gateway needs to be able to pick a model from the list of models allowed for a specific namespace, group, etc. Every feature also needs to be able to look at the default model for the feature.

1. We built the Group Settings page to be able to select namespace defaults from the set offered at the top level namspace. Selecting a list of models for the child namespace if for future considaration.

1. When a model is depreciated / inactivated then we need a way to cascade the deprecations down to the namespace level. We will need to build a Sidekiq job that can do that.

1. In rails when the user is picking a recommended_model / default_model at a namespace level they would be able to choose between the GitLab managed models (from the AI gateway config) and from the list of models configured in the self-hosted models screen.

**Future changes when we allow users to pick a model:**

1. Every feature (chat, code suggestions, code review) needs to be able to display a list of available models on the UI. When the customer selects a model that should be set as the default model.

> For some features such as `Duo Code Review` where the customer is not actively interacting with the UI, we may only allow the selection of a single model.

1. We will need to build a new API to fetch the list of models that user is allowed to use

```gql
query {
  aiFeatureSettings {
    nodes {
      feature,
      defaultModel,
      validModels {
        nodes {
          name
        }
      }
    }
  }
}
```

### AI Gateway Changes

The AI Gateway will have to support a new API that will allow rails to fetch the allowed list of models.

The configuration is done with this pair of files:

- [The model details configuration file](https://gitlab.com/gitlab-org/modelops/applied-ml/code-suggestions/ai-assist/-/blob/main/ai_gateway/model_selection/models.yml) where the model metadata will be configured.

- [The unit primitive configuration file](https://gitlab.com/gitlab-org/modelops/applied-ml/code-suggestions/ai-assist/-/blob/main/ai_gateway/model_selection/unit_primitives.yml) where the models are assigned to feature settings.

Both files need to be updated when we need to release or deprecate a model.

The AI Gateway already supports model passing for various APIs such as `/v2/chat` and `/v4/suggestions`.

The AI Gateway also already supports prompt versioning for different providers so we can tune the prompt in certain cases.

We will need to test our prompt changes across different model families and versions to ensure that we are backwards compatible with what customers are running.
We should collect metrics across different features to figure out the most popular models so that we can focus our model tuning efforts to those.

**Important note:** There is currently no way with model selection to roll out a model incrementally in the AI Gateway. Once a model is configured, it will be sent to customers. Keep that in mind when adding a new model and commit changes to these files at the end of your development cycle.

### Changes to Duo Workflow

In order to allow Model Switching for Duo Workflow we will need to have to create a new field showing the list of models that are available for the GitLab project. Since GitLab project is required for starting a Duo Workflow, we can use the project to determine the group / sub group information to fetch the list of allowed models. When the user selects a model that model information will need to be added to the parameters passed to Duo Workflow Executor which in turn will pass the model name to Duo Workflow Service. The [protobuf contract](https://gitlab.com/gitlab-org/duo-workflow/duo-workflow-service/-/blob/main/contract/contract.proto?ref_type=heads) between the Duo Workflow Service and Executor will need to have a new field called model.

```proto
message StartWorkflowRequest {
    string clientVersion = 1;
    string workflowID = 2;
    string workflowDefinition = 3;
    string goal = 4;
    string workflowMetadata = 5;
    repeated string clientCapabilities = 6;
    string model = 7;
}
```

In addition to this we will be need to be able to update the model [factory](https://gitlab.com/gitlab-org/duo-workflow/duo-workflow-service/-/blob/main/duo_workflow_service/llm_factory.py?ref_type=heads) in Duo Workflow to support different models.

### IDE Changes

The IDE must call GitLab to retrieve the list of allowed models for each feature and pass the selected model in the request to AI Gateway or Rails.
Related [issue](https://gitlab.com/gitlab-org/gitlab/-/issues/541382).

**1. Model List Update**

- The IDE periodically fetches the updated list of available models or listens for a specific GitLab: Update Model List command.
- Changes could also be triggered when the user switches GitLab accounts or when an admin updates model availability.

**2. User Preferences**

- A settings screen in the IDE lets users select their default model per feature.
- The IDE continues to pass the chosen model in chat and code suggestion requests.

**Important note**

Currently, when a user is assigned a seat to at least one project with a model selected for completion. The IDE disables [the direct connection to AI Gateway](https://docs.gitlab.com/user/gitlab_duo/gateway/#region-support) [code completion](https://docs.gitlab.com/user/project/repository/code_suggestions/) calls and goes through the GitLab monolith, which ultimately selects the model to be used according to the user's preferences. The customers should be made aware of this through documentation.

```mermaid
sequenceDiagram
    alt Model Switching
        User->>IDE: Opens VSCode
        IDE->>Rails: Fetch List of Models
        Rails->>Rails: Lookup namespace of project for model list
        loop Every namespace with parent
            Rails->>Rails: Lookup parent namespace of project for model list
        end
        Rails->>Rails: Lookup instance for model list
        Rails->>IDE: Return List of models per feature and default
        IDE->>IDE: Set default models if not set
        IDE->>User: Show list of settings options in IDE
        User->>IDE: Pick model to be used for each feature
    end
    alt Code Suggestions
        User->>IDE: User performs code suggestions request
        IDE->>AIGateway: Send Model in suggestions Request
        AIGateway->>AIGateway: Check whether model is allowed from JWT claims
        AIGateway->>LLM: Get suggestions from model
        LLM-->>AIGateway: Suggestions response
        AIGateway->>AIGateway: Post processing
        AIGateway-->>IDE: Send suggestions response
        IDE->>User: Show suggestions
    end
    alt Chat
        User->>IDE: User interacts with Chat widget
        IDE->>Rails: Start Chat session
        Rails-->>IDE: Chat Session ID
        IDE->>Rails: Send user message
        Rails->>Rails: Use model in request (check model is allowed)
        Rails->>AIGateway: Make chat request with model
        AIGateway->>LLM: Send chat request
        LLM-->>AIGateway: Chat response
        LLM-->>IDE: Send chat response
        IDE->>User: Show response
    end
```

> **Note:** This is a simplified diagram and does not contain all details such as Authentication/Authorization of the requests

## Open Questions / Risks

**Conflict Resolution**

What happens if multiple namespace admins set conflicting default models at different levels of the hierarchy. Which default should we choose?
> **Decision**: Configurations on a child namespace to take precedence over the parent namespace.

**Future Model Feature Parity**

Some models have different capabilities (e.g., Google Gemini 2.0 supports internet search and o1 supports `thinking`). How do we handle enable such sub-features?

**Deprecation & Enforcement**

Should we force a hard switch if an AI model is marked as deprecated, or provide a grace period?
