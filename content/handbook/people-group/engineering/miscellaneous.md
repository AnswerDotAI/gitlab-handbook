---
title: Miscellaneous
description: "Information on automations related to syncing to our team page, job families, and more."
---

## Team page entry daily sync

Once/day we run a pipeline that syncs the following fields for all team members:

- `name`, team members preferred name or nick name.
  - Will **not** sync name from Workday if **opted in**. This can be changed at any time in the YAML entry itself, to set a custom nickname or preferred name for the team page.
  - Only overwritten if **opted out** of syncs, in which we will replace with the team members current job title.
- `specialty`, included if the team member has a job specialty component.
- `departments`, A list of the team members Workday department and extra departments added to their team page entry.
  - We will only ever update the **first** entry of this list to their current Workday department.
- `division`, person's current division in Workday.
- `job_title`, person's current job title.
- `reports_to`, the `slug` reference of the team members manager team page entry.
- `gitlab` the `customGitLabUsername` value from Workday.
- `public` whether or not the team member has selected having their information exported or not.

This means that if team members edit that field in the file, this will result in the sync overwriting when it runs again. The reason for this is that we consider Workday as the single source of truth for this data. Thus team members and managers will need to make adjustments in Workday first and this will be automatically propagated in the team page entry.

Team members can edit their export preferences at any time by following [this job aid](https://docs.google.com/document/d/16_G0jQEjV3f08rGZ65g6RHTCSX5IfFalo9ZUdLEqH1s), which will reflect their export preferences the next time the sync runs.

### Diagram

<div style="width: 640px; height: 480px; margin: 10px; position: relative;"><iframe allowfullscreen frameborder="0" style="width:640px; height:480px" src="https://lucid.app/documents/embedded/236d061a-50b5-4917-a74d-29715ed035e1" id="ZwPRKLUTflmI"></iframe></div>

### Caveats

- In the event that a daily sync is not merged the same day, that is fine, we can close the outdated MR and merge the most recent as this will contain the latest changes only updating files currently included in the handbook.
- Pipelines may fail when adding to the merge train if a team member edited their team page entry after the MR was opened, most can be resolved by using the `/rebase` quick action, or by resolving conflicts manually. As above, these will usually resolve themselves on the next sync.

## Sensitive data compliant Time Off by Deel export

Every week, a scheduled job queries all PTO events occurring during a ±4 week time frame. Sensitive information (eg. the *type* of PTO taken) is then filtered out from these PTO events. The compliant data is then uploaded to a Google Cloud Storage bucket for the data analytics team to consume.

The data team then makes a subset of this information available via Sisense to allow team members to create more accurate charts for metrics like *number of merge requests per team member over a 30-day period*.

## Netherlands accrual adjustments

A scheduled job runs on January first and for each team member located in the Netherlands, if their `Employee Accruals` balance is negative, it is set back to 0 days.

A similar scheduled job also runs on July first, but in this case, for each team member located in the Netherlands, if their `Employee Accruals` balance exceeds 10 days, it is set back to 10 days.

## Set closed training issues to confidential

Once per day, closed issues in the [training project](https://gitlab.com/gitlab-com/people-group/Training) are automatically marked as confidential for compliance.

## Letter of employment

Every hour, a scheduled job checks the letter of employment requests spreadsheet for new entries. For each entry, a letter of employment will be generated using the team member's Workday data. The letter is then sent directly to the team member's work email address.

To retrieve your letter of employment, please use the process in the internal handbook [here](https://internal.gitlab.com/handbook/people-group/people-operations/people-connect/frequently_requested/#letter-of-employment).

## Entities sync

Once per week, Workday locations are synced to GitLab groups. Team members are then added to the correct group. The list of groups (entities) can be found in the [entities project](https://gitlab.com/gitlab-com/entities).

When creating a merge request or issue that affects all members of a given GitLab entity, all members with direct membership can be pinged using `@gitlab-com/entities/<entity-name>`.

eg. for Canada Corp, use `@gitlab-com/entities/canada-corp`.

## On-call scheduling spreadsheet

On the first day of each month, we populate a spreadsheet including information for team members who have been at GitLab for more than 3 months. The spreadsheet is used by engineering to plan for on-call availability.

Synced fields are sourced from Workday.

- Name
- Job title
- Start Date
- Division
- Department
- Role
- Weekend availability
- Email
- Manager

## GitLab Group

We utilize a GitLab.com group for internal communications ('pings') on GitLab.com. This helps ensure the appropriate team members from the team are alerted and reduces noise for others that may not need to be alerted.

This group is public https://gitlab.com/gl-people-engineering, and can be mentioned by tagging `@gl-people-engineering` within an issue, merge request, or epic on GitLab.com.

> Project creation for this group has been disabled, all People Group Engineering projects that can be public should be committed to https://gitlab.com/gitlab-com/people-group-public/engineering.

## Access Request issue closing

Access Requests open for longer than 30 days will be closed automatically by the Employment Bot.

We run this job once a week to check for any open issues older than 30 days, except for ones with the `AccessReview` label, and leave the following note closing the issue:

```text
This access request issue has been open for more than 30 days. It is being automatically closed to de-clutter this issue tracker.

If there are any tasks remaining or this was not supposed to be closed, reopen the issue and ping the DRIs to get them completed as soon as possible.

/close
````
