---
title: Secure / Govern sub-department delineation
description: "Definition of what engineering group is responsible for features in the Secure and Govern stages of the GitLab product"
---

## Why does this page exist?

In the spirit of establishing a [DRI](/handbook/people-group/directly-responsible-individuals/) for each set of functionality where this may not be obvious, the purpose of this page is to explicitly define which engineering group has reponsibility for which portions of the product and for specific decisions.

## Page/Function responsibilities

| Page/Function | PM | Primary Group | Example |
| ---      | ---      | ---      | ---      |
| [Secure Partner Onboarding Docs](https://docs.gitlab.com/ee/development/integrations/secure_partner_integration.html) | {{< member-by-gitlab "abellucci" >}} | [Sec by their categories](/handbook/product/categories/#sec-section) |  |
| [Security Configuration](https://docs.gitlab.com/ee/user/application_security/configuration/) | | [Sec by their categories](/handbook/product/categories/#sec-section) |  |
| Vulnerability ingestion and DB storage | {{< member-by-gitlab "abellucci" >}} | [Govern:Threat Insights](/handbook/product/categories/#threat-insights-group) |  |
| Dependency ingestion and DB storage | {{< member-by-gitlab "abellucci" >}} | [Govern:Threat Insights](/handbook/product/categories/#threat-insights-group) |  |
| [Dependency List](https://docs.gitlab.com/ee/user/application_security/dependency_list/) | {{< member-by-gitlab "abellucci" >}} | [Govern:Threat Insights](/handbook/product/categories/#threat-insights-group) | [Example](https://gitlab.com/gitlab-examples/security/security-reports/-/licenses#licenses) |
| [License Compliance Page](https://docs.gitlab.com/ee/user/compliance/license_approval_policies.html) | {{< member-by-gitlab "abellucci" >}} | [Govern:Threat Insights](/handbook/product/categories/#threat-insights-group) |  |
| [Interact with findings and vulnerabilities](https://docs.gitlab.com/ee/user/application_security/index.html#interact-with-findings-and-vulnerabilities) | {{< member-by-gitlab "abellucci" >}} | [Govern:Threat Insights](/handbook/product/categories/#threat-insights-group) |  |
| [Merge Request Security Widget](https://docs.gitlab.com/ee/user/application_security/#view-security-scan-information-in-merge-requests) | {{< member-by-gitlab "abellucci" >}} | [Govern:Threat Insights](/handbook/product/categories/#threat-insights-group) | [Example](https://gitlab.com/gitlab-org/security-products/tests/webgoat/-/merge_requests/26) |
| [Merge Request License Compliance Widget](https://docs.gitlab.com/ee/user/application_security/dependency_list/index.html) | {{< member-by-gitlab "johncrowley" >}} | [Secure:Composition Analysis](/handbook/product/categories/#composition-analysis-group) | [Example](https://gitlab.com/gitlab-org/security-products/tests/webgoat/-/merge_requests/28) |
| [Pipeline Security Tab](https://docs.gitlab.com/ee/user/application_security/security_dashboard/#view-vulnerabilities-in-a-pipeline) | {{< member-by-gitlab "abellucci" >}} | [Govern:Threat Insights](/handbook/product/categories/#threat-insights-group) | [Example](https://gitlab.com/gitlab-org/security-products/tests/webgoat/-/pipelines/155052050/security) |
| [Security Dashboards](https://docs.gitlab.com/ee/user/application_security/security_dashboard/) | {{< member-by-gitlab "abellucci" >}} | [Govern:Threat Insights](/handbook/product/categories/#threat-insights-group) | [Example](https://gitlab.com/gitlab-examples/security/security-reports/-/security/dashboard) |
| [Security Scanner Integration Documentation](https://docs.gitlab.com/ee/development/integrations/secure.html) | {{< member-by-gitlab "abellucci" >}} | [Govern:Threat Insights](/handbook/product/categories/#threat-insights-group) |  |
| [Vulnerability Pages](https://docs.gitlab.com/ee/user/application_security/vulnerabilities/) | {{< member-by-gitlab "abellucci" >}} | [Govern:Threat Insights](/handbook/product/categories/#threat-insights-group) | [Example](https://gitlab.com/gitlab-examples/security/security-reports/-/security/vulnerability_report) |
| [Vulnerability Report](https://docs.gitlab.com/ee/user/application_security/vulnerability_report/) | {{< member-by-gitlab "abellucci" >}} | [Govern:Threat Insights](/handbook/product/categories/#threat-insights-group) | [Example](https://gitlab.com/gitlab-org/threat-management/webgoat/-/security/vulnerabilities) |
| [Policies](https://docs.gitlab.com/ee/user/application_security/policies/) | {{< member-by-gitlab "g.hickman" >}} | [Govern:Security Policies](/handbook/product/categories/#security-policies-group) | [Example](https://gitlab.com/gitlab-examples/wayne-enterprises/wayne-financial/customer-web-portal/-/security/policies) |
| Advisories ingestion and DB storage| {{< member-by-gitlab "johncrowley" >}} | [Secure:Composition Analysis](/handbook/product/categories/#composition-analysis-group) |  |
| External License ingestion and DB storage | {{< member-by-gitlab "johncrowley" >}} | [Secure:Composition Analysis](/handbook/product/categories/#composition-analysis-group) |  |
| Vulnerability Match Job | {{< member-by-gitlab "johncrowley" >}} | [Secure:Composition Analysis](/handbook/product/categories/#composition-analysis-group) |  |
| License Match Job | {{< member-by-gitlab "johncrowley" >}} | [Secure:Composition Analysis](/handbook/product/categories/#composition-analysis-group) |  |
| [CVE ID Request - Workflow and automation](https://docs.gitlab.com/ee/user/application_security/cve_id_request.html) | {{< member-by-gitlab "sarahwaldner" >}} | [Secure:Vulnerability Management](/handbook/product/categories/#secure-vulnerability-research-group) |  |
| [CVE ID Request - Platform UI](https://docs.gitlab.com/ee/user/application_security/cve_id_request.html) | {{< member-by-gitlab "abellucci" >}} | [Govern:Threat Insights](/handbook/product/categories/#threat-insights-group) |  |
| [User Invitation Flows](https://docs.gitlab.com/ee/user/project/members/#add-users-to-a-project) | {{< member-by-gitlab "hsutor" >}} | [Govern:Authentication](https://about.gitlab.com/direction/software_supply_chain_security/authentication/) |  |

## Technical Boundaries

Ownership of the end-to-end technical solution spans multiple groups. This section clarifies
cross-group maintainership of code artifacts between [Threat Insights](/handbook/product/categories/#threat-insights-group) and the remaining groups in
the [Sec Section](/handbook/product/categories/#sec-section).

Ownership means that the responsible group:

1. Is responsible for maintenance of the code.
1. Receives attribution in their error budget associated with the relevant code.
1. Must be consulted before changes are made, and should review them before being merged.
1. Receives priority when requesting maintenance and fixes to changes introduced by another group.

### Owners by project/function

This is not a comprehensive list, but includes the main projects and areas of functionality under the Sec Section umbrella.

#### Comparison and tracking logic

The logic to compare and track vulnerabilities is owned by Threat Insights.

Customisation of this logic that is not generic to all report types is owned by the corresponding group(s) (e.g. Static Analysis group would be the maintainer of any improvement to track SAST vulnerabilities).

It is not always possible to promptly identify the group that owns some code. In the absence of an attribution through error budget, `CODEOWNERS`, code comments or other means, Threat Insights will idenfity the owner and, if necessary, handover to the appropriate group.

#### Security Report Schema

The [schemas](https://gitlab.com/gitlab-org/security-products/security-report-schemas/) are owned by the backend team in the analyzer groups responsible for the corresponding categories.

Threat Insights owns the [base schema](https://gitlab.com/gitlab-org/security-products/security-report-schemas/-/blob/master/src/security-report-format.json) and the [generic details schema](https://gitlab.com/gitlab-org/security-products/security-report-schemas/-/blob/master/src/vulnerability-details-format.json).

For instance, the Static Analysis group is responsible for the SAST category, so its backend team is responsible for the [`sast` report JSON schema](https://gitlab.com/gitlab-org/security-products/security-report-schemas/-/blob/master/src/sast-report-format.json).

Regardless of ownership, Threat Insights must review all changes as they are the consumer of reports that conform to the schemas.

For more information on who to request a review from, see the project
[guidelines](https://gitlab.com/gitlab-org/security-products/security-report-schemas/-/blob/master/README.md#guidelines).

#### Vulnerability Management

This includes all items assigned to Threat Insights under [Page/Function responsibilities](#pagefunction-responsibilities), and also:

* Database Management System objects
* Object-relational mappings
* Integration points
  * APIs
  * Security report ingestion framework

#### AI Vulnerability Explanation and Vulnerability Resolution

These workflows are owned by Threat Insights as part of [Vulnerability Pages](https://docs.gitlab.com/ee/user/application_security/vulnerabilities/) (see above).
This includes integration into the monorepo, display in Vulnerability pages, the merge request interface for Vulnerability Resolution, and integration into Duo Chat for Vulnerability Explanation. Threat Insights collaborates with [AI Framework](/handbook/engineering/ai/ai-framework/) and [Duo Chat](/handbook/engineering/ai/duo-chat/) to support integration into areas these teams own.

Prompts, test data set curation, and verifying quality of responses for Vulnerability Explanation and Vulnerability Resolution are owned by the relevant groups in [Secure](/handbook/engineering/development/sec/secure/) based on the type of vulnerability. These groups communicate and collaborate with [Vulnerability Research](/handbook/engineering/development/sec/secure/vulnerability-research/) and [AI Framework](/handbook/engineering/ai/ai-framework/) for prompt engineering support, as needed. These features are currently available for [SAST](/handbook/engineering/development/sec/secure/#sast) only.

While prompts are owned by teams in Secure, prompt engineering is an important part of software development at GitLab, the AI-Powered DevSecOps platform. Teams within Govern - including Threat Insights - are expected to onboard and be able to support prompt engineering for these features, and assist as needed with updating the prompts in the monorepo through follow the sun coverage.

Metrics and usage monitoring within the application are owned by Govern: Threat Insights. [Related issue](https://gitlab.com/gitlab-org/gitlab/-/issues/464089).
