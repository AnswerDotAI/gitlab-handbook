---
title: KPIs
---

## What are KPIs

Every part of GitLab has Key Performance Indicators (KPIs).
Avoid the term metric where we can be more explicit.
Use KPI instead.
A function's KPIs are owned by the respective member of e-group.
A function may have many performance indicators (PIs) they track and not all of them will be KPIs.
KPIs should be a subset of PIs and used to indicate the most important PIs to be surfaced to leadership.

The KPI definition should be in the most relevant part of the handbook which is organized by [function and results](/handbook/about/handbook-usage/#organized-by-function-and-results).
In the definition, it should mention what the canonical source is for this indicator.
Where there are formulas, include those as well.
Goals related to KPIs should co-exist with the definition.
For example, "Wider community contributions per release" should be in the Developer Relations part of the handbook and "Average days to hire" should be in the Talent Acquisition part of the handbook.

## KPI Index

## Legend

The icons below are relevant for [Phase 1](/handbook/company/kpis/) and can be assigned by anyone at GitLab.

📊 KPI is operational, public, and embedded in the GitLab Handbook next to the definition.

🔗 KPI is operational, links to another system because the KPI is [internal](/handbook/communication/confidentiality-levels/#internal) or can't be embedded in the GitLab Handbook yet.

🔒 KPI is operational, links to a [limited access](/handbook/communication/confidentiality-levels/#limited-access) system.

🚧 KPI is `WIP: work in progress` and estimated to be operational within a month. Should include a link to an issue.

🐔 KPI is unlikely to be operationalized in the near term.

## GitLab KPIs

GitLab's **North Star metric** is run-rate revenue. In addition, there are other 10 other top KPIs.

GitLab KPIs are duplicates of goals of the reports further down this page.
GitLab KPIs are the 10 most important indicators of company performance, and the most important KPI is Net ARR.
We review these at each quarterly meeting of the Board of Directors.
These KPIs are determined by a combination of their stand alone importance to the company and the amount of management focus devoted to improving the metric.

1. [Revenue](/handbook/company/kpis/#sales-kpis) vs. plan (lagging)
1. [R&D Overall MR Rate](/handbook/engineering/performance-indicators/#rd-overall-mr-rate) (leading)
1. [Estimated Combined Monthly Active Users (CMAU)](https://internal.gitlab.com/handbook/company/performance-indicators/product/#estimated-combined-monthly-active-users) (leading)
1. [Net New Business Pipeline Created ($s)](/handbook/marketing/performance-indicators/#net-new-business-pipeline-created) 🐔 (leading)
1. [Pipeline coverage start of quarter stage 3+](/handbook/marketing/performance-indicators/#pipeline-coverage) (leading)
1. [Percent of Ramped Reps at or Above Quota](https://internal.gitlab.com/handbook/company/performance-indicators/sales/#percent-of-ramped-reps-at-or-above-quota) (lagging)
1. [Net Retention](/handbook/customer-success/customer-success-vision/#retention-and-reasons-for-churn) (lagging)
1. [Gross Retention](/handbook/customer-success/customer-success-vision/#retention-and-reasons-for-churn) (lagging)
1. [12 Month Team Member Voluntary Retention](/handbook/people-group/people-success-performance-indicators/#team-member-voluntary-retention-rolling-12-months) (lagging)
1. [Unique Wider Community Contributors per Month](/handbook/marketing/developer-relations/performance-indicators/#unique-wider-community-contributors-per-month) (lagging)

## Office of the CEO KPIs

{{< kpi "Office of the CEO" >}}

## Sales KPIs

[Sales KPIs](https://internal.gitlab.com/handbook/company/performance-indicators/sales/#kpi-summary) are [Not Public](/handbook/communication/confidentiality-levels/#not-public) and documented in [the Internal handbook](/handbook/about/handbook-usage/#the-internal-handbook).

{{< kpi "Sales" >}}

## Marketing KPIs

{{< kpi "Marketing" >}}

### Developer Relations Department KPIs

{{< kpi "Developer Relations Department" >}}

## People Group KPIs

### People Success KPIs

{{< kpi "People Success" >}}

## Finance KPIs

### Finance Team KPIs - Reported in Key Review

{{< kpi "Finance Team" >}}

## Product KPIs

GitLab team members can access and update all Product performance indicators within the internal handbook via `Okta > GitLab Internal Handbook`

## Engineering KPIs

{{< kpi "Engineering Function" >}}

### Customer Support Department KPIs

{{< kpi "Customer Support Department" >}}

### Development Department KPIs

{{< kpi "Development Department" >}}

### Infrastructure Department KPIs

{{< kpi "Infrastructure Department" >}}

### UX Department KPIs

{{< kpi "UX Department" >}}

## Satisfaction

We do satisfaction scope on a scale of 1 to 5 how satisfied people are with the experience.
We don't use NPS since that cuts off certain scores and we want to preserve fidelity.
We have the following abbreviation letter before SAT, please don't use SAT without letter before to specify it:

- C = unused since customer is ambiguous (can mean product or support, not all users are customers)
- E = unused since employee is used by other companies but not by us
- I = Interviewee (would you recommend applying here)
- L = Leadership (as an executive with dedicated administrative support, how is your executive administrative support received)
- O = [Onboarding](/handbook/people-group/people-success-performance-indicators/#onboarding-tsat) (how was your onboarding experience)
- P = [Product](https://internal.gitlab.com/handbook/company/performance-indicators/product/) (would you recommend GitLab the product)
- S = [Support](/handbook/support/performance-indicators/#support-satisfaction-ssat) (would you recommend our support followup)
- T = Team-members (would you recommend working here)

## Retention

Since we track retention in a lot of ways, we should never refer to just "Retention" without indicating what kind of retention.
We track:

- [Net Retention](/handbook/customer-success/customer-success-vision/#retention-and-reasons-for-churn)
- [Gross Retention](/handbook/customer-success/customer-success-vision/#retention-and-reasons-for-churn)
- User Retention
- [Team Member Retention](/handbook/people-group/people-success-performance-indicators/#team-member-retention)

## Layers of KPIs

We have KPIs at many different [layers](/handbook/company/structure/#layers).

KPIs can only exist at the Company (e.g. GitLab) layer if it exists at the functional layer.
In other words, GitLab KPIs are duplicates of KPIs of the executives.
Not all functional KPIs are GitLab KPIs but all GitLab KPIs are functional KPIs.

As GitLab grows, this will also be true throughout the layers.
Not all departmental KPIs will be functional KPIs but all functional KPIs will be department KPIs.
This will cascade throughout the organization, as all job families will have performance indicators associated with them.

The [KPI Index](#kpi-index) captures the company, functional, and departmental KPIs since these are the three highest layers.

The only exception to this is where the filter on a KPI may change.
For example, the GitLab KPI may be "Hires vs Plan" but the Engineering KPI may be "Engineering Hires vs Plan".
The logic is the same, but the filter changes.

## Parts of a KPI

A KPI or metric consists of multiple things:

1. Definition: What is the data source? How is it calculated? What fields are included? What caveats are considered? Why is it chosen?
    - Note: Please see [Infrastructure Hosting Cost per MAU](/handbook/engineering/infrastructure/performance-indicators/#infrastructure-hosting-cost-per-gitlab-com-monthly-active-users) as an example.
1. Target: What we strive to be above, e.g. ARR has a target
1. Cap: What we strive to be below, e.g. Turnover has a cap
1. [Job family](/handbook/hiring/job-families/): link to job families with this as a performance indicator
1. Plan: what we have in our yearly plan
1. Commit: the most negative it will be
1. 50/50: the median estimate, 50% chance of being lower and higher
1. Best case: the most positive it will be
1. Forecast: what we use in our rolling 4 quarter forecast
1. Actual: what the number is

## What is public?

In the doc 'GitLab Metrics at IPO' are the KPIs that we may share publicly.
All KPIs have a public definition, goal, and job family links.
The actual performance and various estimates can be:

1. Live reported
1. Quarterly reported
1. Private
