---
title: "Tableau Admin Guide"
description: "Tableau at GitLab"
---

This page describes the processes used to administer the Tableau sites managed by GitLab.  Additional run books, scripts, tools and repositories related to the processes will be referenced throughout this guide.

## Tableau Administrator - Role and Objectives

As Tableau Administrators, we serve as the foundation of our organization's data visualization and analytics infrastructure. Our mission is to empower teams with a secure, reliable, and user-friendly analytics environment that fosters data-driven decision-making. We bridge the gap between complex data systems and actionable business insights while upholding high standards of governance and promoting self-service analytics.

### Our Five North Star Goals

1. **Performance & Reliability:** Ensure a highly available Tableau environment with optimized dashboards and stable data connections for a seamless user experience.
2. **Security & Governance:** Safeguard data integrity by maintaining security policies, ensuring appropriate access controls, and ensuring compliance with governance standards.
3. **User Enablement & Adoption:** Drive engagement through training, support, and resources that empower users to confidently analyze and interpret data.
4. **Standardization & Quality:** Establish and enforce best practices for data sources and visualizations to ensure consistency, accuracy, and trust in reporting.
5. **Business Impact:** Deliver measurable value by aligning analytics initiatives with business objectives, tracking key metrics, and demonstrating how data-driven insights enhance decision-making and efficiency.

## Sites

GitLab currently maintains three different Tableau sites for different purposes:

- **Main Site:** The main site is where all of the workbook and datasource development takes place and is the site team members can request a license to use.  

- **Public Site:** The public site is used to host the workbooks that are intended to be embedded in the public handbook and viewed by anyone visiting the handbook page.  Team members do not have direct access to the public site and no general workbook development takes place on this site.  

- **Sandbox Site:**  The sandbox site is used for testing of scripts and features in an environment that will not disrupt the main site. No general workbook development takes place on the sandbox site.

### **Additional Sites**

Tableau Cloud Manager is an administrative feature that enables the creation of up to three additional Tableau sites per account. These extra sites can be used for various purposes, including enhanced governance, staging for new content, feature testing, or secure data separation by project or team. With [Tableau Cloud Manager](https://help.tableau.com/current/online/en-us/cloud_manager_intro.htm), administrators can set up isolated and well-organized workspaces, helping to maintain data integrity and ensuring seamless management across different environments.

## Tools

The TableauConMan tool is developed in house to assist in automating several aspects of administering Tableau.  With orchestration in Airflow and a series of configuration files known as plans, it currently performers the following functions:

- Sync content to the public site
- Manage groups and group membership on the main site

## User Management

- **Main Site:** For the main site team members login using Okta. An Okta - Lumos integration manages Tableau Access Requests which includes review and approvals (performed automatically via Slack), and automated Provisioning and Deprovisioning. This also includes an automated deprovisioning due to inactivity for 90+ days.

- **Public Site:** For the public site users login directly and do not use Okta.  The number of non viewer licenses on this site is limited so any active administration on the site should be done with the Analytics Service Account.

- **Sandbox Site:** For the sandbox site users login directly and do not use Okta.  The number of non viewer licenses on this site is limited so any active administration on the site should be done with the Analytics Service Account.

## Group Management

- **Main Site:** For the main site groups and group membership is managed via Okta with an [Access Request](https://gitlab.com/gitlab-com/team-member-epics/access-requests/-/issues/new?issuable_template=Tableau_Request).

- **Public Site:** The groups for the public site are manually maintained.  The general instructions found in the groups [runbook](https://gitlab.com/gitlab-data/runbooks/-/tree/main/tableau?ref_type=heads) can be followed to modify groups or group membership.

- **Sandbox Site:** The groups for the sandbox site are manually maintained.  The general instructions found in the groups [runbook](https://gitlab.com/gitlab-data/runbooks/-/tree/main/tableau?ref_type=heads) can be followed to modify groups or group membership.

## Tableau Cloud Sites Project Structure

- **Main Site:** The project structure for the main site is maintained manually and should match the folder structure found in the Tableau repository.  This structure is used to enforce code reviews of changes in the production project and the MR with the requested changes should be approved before changes are made to the site.

- **Public Site:** The project structure for the public site is maintained manually.  Many processes such as content synchronization and shareable content reports are dependent on the project structure of the site. Changes to the project structure should be made with this in mind.

- **Sandbox Site:**  The project structure of the sandbox site does not need to be fixed to any specific structure.

## Content Permissions

- **Main Site**: The content permissions for the main site are maintained manually and should align with the Transparency value and only limit access to content when it is strictly needed.  Content permissions should only be granted to groups and not individual users.

- **Public Site:** The content permissions for the public site are maintained manually.  Many processes such as content synchronization and shareable content reports are dependent on the project structure of the site. Changes to the project structure should be made with this in mind.

- **Sandbox Site:** The content permissions of the sandbox site do not need to be fixed to any specific structure.

## Content Management

### Main Site

#### Stale and Unsued Content Management

#### 1. Purpose - Content Archival

Unsued workbooks and data sources are moved to the Archive folder to maintain a clean and efficient Tableau Cloud environment. This is an automated process which ensures that only quality, actively used content remains readily accessible, thereby minimizing clutter and enhancing the user experience. Users can quickly find and access high-quality, relevant content without sifting through outdated or unused items. Automating this process ensures consistency and accuracy, saving time and effort for the Tableau Admin team. Manual intervention is minimized, reducing the likelihood of errors.

#### 2. Prerequisites - Automation Script

A Python script is used for this automation which follows specific criteria to identify and archive stale content. Here is a detailed explanation of the stale contentent identification:

1. <b>Workbooks</b> - Stale Criteria: A workbook is considered stale if it has not been created, updated, or viewed in the last 90 days.

2. <b>Data Sources</b> - Stale Criteria: A data source is considered unused if it has no connected workbooks and has not been created or updated in the last 90 days.

    Exclusions and Uniquenss:

    - Exclusions: Workbooks and Data sources with the Tableau tag "Do NOT Archive" are excluded from archiving.

    - Renaming for Uniqueness: Before moving a workbook or data source to the "Archive" folder, its name is appended with the owner, parent project, and the current date/time to ensure uniqueness and avoid conflicts.

#### 3. Archival Schedule

This procedure is scheduled to run quarterly, specifically at the end of each quarter. The Tableau Admin team will manually kick off the process, ensuring that the automation runs at the most opportune time and any immediate concerns can be addressed.

#### 4. Exclusion Tag

To prevent critical content from being archived, the business can use the exclusion tag "Do NOT Archive". Any workbooks or data sources with this tag will be skipped during the archiving process. The Data team may periodically review the dashboards with this tag to ensure the exceptions are still warranted. It should be noted that workbooks tagged with "Public" should also be exlcuded.

#### 5. Archive Folder Access

The "Archive" folder has restricted access, meaning that the business cannot view or access its contents directly. This restriction helps in removing archived content from search results, thereby maintaining a clean and efficient environment. If users need access to any archived content, they can reach out to the BI Team via the #data-tableau Slack channel for assistance.

### Public Site

#### Stale and Unsued Content Management

Content archival and management is performed manually on an as need basis.

### Sandbox Site

Content archival and management is performed manually on an as need basis.

## Connected Applications

Only the public site has a connected application that is used for viewing content embedded in the public handbook.  There are keys, secrets, and ids from this connected app that must be updated and shared with the handbook team: specifically the [cloud function](https://console.cloud.google.com/functions/details/us-central1/tableau-connected-app?env=gen2&hl=en&project=mcottrell-8f2b9454&tab=details) that authenticates the viewer on page load.

## Tableau Cloud and Tableau Desktop Release Management

Our Data and Analytics team manages new releases for Tableau Cloud and Tableau Desktop to ensure that these updates meet company standards for stability and compatibility with our existing workflows and integrations. This process outlines our review, inspection, validation, and communication procedures for each release, along with instructions for updating Tableau Desktop.

### Release Review and Validation Process

- **New Release Noticifation:** The Tableau Admin team will monitor for new Tableau Cloud and Tableau Desktop [releases](https://www.tableau.com/products/coming-soon) as they are announced by Tableau.

- **Release Review and Inspection:** After release the team will take **two weeks** to review release notes, inspect new features, enhancements, and security updates to assess potential impacts on our Tableau Cloud environment, data connections, and Tableau Desktop compatibility. Release notes can be followed in the GitLab [Tableau Quarterly Update Review](https://gitlab.com/groups/gitlab-data/-/epics/1287) Epic.

- **Validation and Testing:** New releases will undergo a series of validation tests within a staging environment. This includes checking compatibility with our embedded data sources, dashboards, integrations, and any custom configurations.

- **Communication to the Business:** After a release is validated, a communication will be sent via the Slack Channel: `#data-tableau`. Items to be covered in the release will include:
  - Key features and enhancements in the new release
  - Any changes that may impact user workflows
  - Steps for updating Tableau Desktop
  