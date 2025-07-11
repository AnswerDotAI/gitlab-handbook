---
title: "Data Team Data Management Page"
description: "The Data Management Page covers the content around managing, securing, and governing the Enterprise Data Platform and related activities."
---

## Purpose

Data Management covers practices and policies around managing, securing, and governing the [Enterprise Data Platform](/handbook/enterprise-data/platform/) and activities related to it. The technical components of the Enterprise Data Platform are listed in the [GitLab Tech Stack](/handbook/business-technology/tech-stack-applications/).

## Scope

### Data Security Practices

The Enterprise Data Platform captures, processes, and stores [data collected from many systems](/handbook/enterprise-data/platform/). Not all of this data is of the same importance and we use the [Critical System Tier](/handbook/security/security-assurance/security-risk/storm-program/critical-systems/) framework and [Data Classification Standard](/handbook/security/standards/data-classification-standard/) to help us determine what data is most important and how to best secure it.

## Roles & Responsibilities

| Role  | Responsibility |
| :-- | :-- |
| GitLab Team Members | Responsible for following the requirements in this procedure |
| Data Management Team | Responsible for implementing and executing this procedure |
| Data Management (Code Owners) | Responsible for approving significant changes and exceptions to this procedure |

## Standard

### Snowflake

We deploy a Role-Based Data Access Scheme in Snowflake:

* User Access is managed with Okta and [Access Requests are managed with GitLab](/handbook/enterprise-data/platform/#warehouse-access)
* Each user is assigned one more [Roles based on their job function](/handbook/enterprise-data/platform/#snowflake-permissions-paradigm) and this configuration is managed with [Permifrost](/handbook/enterprise-data/platform/permifrost/)

Additional controls include:

* Based on the Data Classification standard, [data is managed with Databases and Schemas](/handbook/enterprise-data/platform/#data-storage)
* Every query/user/process is assigned a [pre-defined Warehouse, or Compute Resource](/handbook/enterprise-data/platform/#compute-resources)
* [Passwords are rotated](/handbook/enterprise-data/platform/#passwords)

### Data Categorization

In the Data Platform at GitLab we have multiple categories. Its good to highlight that each category applies to all the data. This means that every Data Product (extracted source, table, row, field, dashboard, pump, etc..) is applicable to **each** of the data categories.

| Data category | Description | Possible values | How to handle | Access controls |
| ------------- | ----------- | --------------- | ------------- | --------------- |
| Data Classification | The type and level of data. | Red, Orange, Yellow, Green. | Red data is not allowed to be stored in the Data Platform. Follow the [general data security controls](/handbook/enterprise-data/data-governance/data-management/#general-data-security-controls). | No particular controls in place. |
| MNPI | This is material non public information. | MNPI or not MNPI. | Follow the [SAFE Data guide](/handbook/enterprise-data/platform/safe-data/). | Access is granted by Permifrost. GitLab Team Members will become a designated insider. |
| Sensitive data | Data that is considered to be kept sensitive and not be shared with all GitLab Team members by default. | Sensitive or not Sensitive. | Sensitive data is [masked](/handbook/enterprise-data/platform/dbt-guide/#sensitive-data) via DBT | Access is granted by Permifrost. |
| Personal data | Sometimes also referenced as PII. Any data that describes or is reasonably capable of being associated with or linked to an identifiable natural person. Full description on the [security handbook page](/handbook/security/standards/data-classification-standard/#data-classification-definitions). | Personal data or not personal data | Work with our Legal Privacy team to obtain approval for processing personal data | Depends on legal guidance. [Masking](/handbook/enterprise-data/platform/dbt-guide/#sensitive-data) could be used (static or dynamic) if needed. |
| Sensitive Personal data | Data related to race/ethnicity, health or medical details, biometric or genetic data, religion, political affiliation or philosophy, sexual orientation, criminal offenses, citizenship/immigraion, or trade unions. | Sensitive personal data or not sensitive personal data | Privacy legislation prohibits the processing of these types of data elements, except in limited circumstances. Work with our Legal Privacy team to obtain approval for processing personal data and include People Operations, if sensitive Personal Data is related to GitLab Team Members |  Depends on legal guidance.  [Masking](/handbook/enterprise-data/platform/dbt-guide/#sensitive-data) could be used (static or dynamic) if needed.  |

### General Data Security Controls

* For the purpose of defining Data Controls, the Enterprise Data Platform is a [Tier 1 system](/handbook/security/security-assurance/security-risk/storm-program/critical-systems/).
* `IMPORTANT`: [Customer Private RED data](/handbook/security/standards/data-classification-standard/#red) is prohibited from permanent storage in the Enterprise Data Platform.

| Control | RED | ORANGE | YELLOW |
| :-- | :-- | :-- | :-- |
| **General Data Controls** | | | |
| Data Registry Listing  | Required | Required | Recommended |
| Encryption At Rest | Required | Required | Required |
| Encryption In Transit | Required | Required | Required |
| Privacy Review | Required | Recommended | Not Required |
| Data Retention Procedures | Required | Recommended | Not Required |
| **Data Infrastructure Controls** | | | |
| Multi-Factor Authentication | Required | Required | Required |
| Role Based Access | Required | Required | Required |
| Access Logging | Required | Required | Recommended |
| **Data Warehouse Controls** | | | |
| Quarterly Snowflake User Audits | Required | Required | Required |
| Quarterly SiSense User Audits | Required  | Required | Required |
| Quarterly Change Management Review | Required  | Recommended | Not Required |
| Quarterly RED Data Scanner | Required | N/A | N/A |
| **Endpoint Devices** | | | |
| Anti-Malware | Required | Required | Required |
| Full-Disk Encryption | Required | Required | Required |
| Quarterly Data Purge | Required | Required | Required |

* **Data Infrastructure**: includes any systems with interact access or process data as part of a Data Warehouse and makes data available to end users.
* **Data Warehouse Controls**: The Enterprise Data Warehouse is a Tier 1 System.
* **Endpoint Devices**: All Endpoints Which Have Access To The Data Warehouse are Classified as Tier 1

### Quarterly Data Health and Security Audit

A **Quarterly Audit** is performed to validate system security, such as ensuring the right people have correct data access configuration and data pipelines are running correctly.

The process is supported by the [Quarterly Data Health and Security issue template](https://gitlab.com/gitlab-data/analytics/-/blob/master/.gitlab/issue_templates/Platform%3A%20Quarterly%20Data%20Health%20and%20Security%20Audit.md). The label `~"Quarterly Data Health and Security Audit"` is used for all issues and merge requests related to the Quarterly audit.

Here is a sample checklist of activities:

#### Snowflake

* Drop accounts from off-boarded employees from Snowflake
  * All Snowflake accounts from GitLab team members that are off-boarded, should be dropped from the day they are off-boarded. This activity checks for any active accounts for off-boarded GitLab team members within `roles.yml`. Once inactive users are removed from `roles.yml`, the weekly DAG `snowflake_cleanup` will then remove them from Snowflake. Any active account that is dropped will no longer maintain any data, scripts, or other artifacts.
* Validate all user accounts do not have password set.
* Drop orphaned tables
  * Tables managed through dbt should be manually dropped when they are no longer needed or managed by dbt. This activity compared tables to the tables managed by dbt for tables that have been orphaned. Identified orphaned tables are validated as not being in use and then dropped.
* Drop unused models
  * Models (tables and views) which are not being used will be dropped and the code which generates them will be removed from the Analytics repository. An unused model can be defined as:
    * It has not been queried in more than three months.
          OR
    * The Airflow account is the only user and no downstream models depend on it.
  * A review of tables flagged for removal will be done by the analytics community before being dropped. This will allow for any tables wrongly flagged to be kept.

#### Airflow

* Remove log files older than 90 days.
  * Following [this runbook](https://gitlab.com/gitlab-data/runbooks/-/blob/main/airflow_infrastructure/archival_pvc_volume/delete_pvc_volume.md) remove old Airflow logfiles to reduce PVC. If we run out of disk space Airflow stops working.

#### Monte Carlo

* Deactivate off-boarded employees from Monte Carlo
  * All Monte Carlo accounts from GitLab team members that are off-boarded, should be deactivated from the day they are off-boarded. This activity checks for any active accounts for off-boarded GitLab team members. Subsequently any active account will be deactivated.
* Deactivate any account, that has not logged-in within the past 90 days from the moment of performing an audit, from Monte Carlo.
  * Any named user Monte Carlo account that hasn't logged for more than 90 days will be deactivated. If a GitLab team member wants to have access provisioned back again, a regular AR needs to be created. After manager approval the account will be activated if there are licenses available

Note: The 90 days are subject to change. At this moment we have set a 90 days threshold because Monte Carlo is less frequently used by some team members (not needed as frequent as i.e. Snowflake or Tableau). We may change this in the future

#### Tableau

* Remove users of off-boarded employees from Tableau
* Remove users that have had Tableau access for >=90 days, but have not logged in during the past 90 days

## Exceptions

Exceptions to this procedure will be tracked as per the [Information Security Policy Exception Management Process](/handbook/security/controlled-document-procedure/#exceptions).

## References

* [Controlled Document Procedure](/handbook/security/controlled-document-procedure/)
