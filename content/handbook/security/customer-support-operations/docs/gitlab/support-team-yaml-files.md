---
title: Support team YAML files
description: Operations documentation page for the Support team YAML files
canonical_path: "/handbook/security/customer-support-operations/docs/gitlab/support-team-yaml-files"
---

<sup>*Introduced via [support-team-meta#2159](https://gitlab.com/gitlab-com/support/support-team-meta/-/issues/2159)*</sup>

{{% pageinfo color="warning" %}}

This is an information page for the Support team YAML files.

If you are looking for information about managing them, please see [workflows](../../workflows).

{{% /pageinfo %}}

## What are the Support team YAML files

The Support team YAML files are a group of YAML files that contain various data we utilize in other components at GitLab.

## Where are they stored

They are stored within the [Support Team project](https://gitlab.com/gitlab-support-readiness/support-team).

## How are they used

The data within is compiled into an array of hashes that is then stored in Redis. This is done via the [Support Team Redis Sync project](https://gitlab.com/gitlab-support-readiness/support-team-redis-sync).

## Anatomy of a YAML file

### name

The support team member's name

### email

{{% alert title="Note" color="warning" %}}
This should never be an alias
{{% /alert %}}

The support team member's official GitLab email.

### title

The support team member's job title

### entity

The GitLab entity the team member belongs to.

A list of available entities is:

- GitLab BV
- GitLab Canada Corp
- GitLab GmbH
- GitLab Inc
- GitLab IT BV
- GitLab Korea LTD
- GitLab PTY Ltd
- GitLab PTY Ltd NZ
- GitLab Singapore PTE. LTD
- GitLab UK Ltd

### working_hours

A String representing your working hours. You should specify the timezone to be safe. (examples being `0800-1600 Central time` or `0000-0800 UTC`).

### reports_to

The `name` of the person to whom the support team member reports

### region

The support team member's region

The current regions we have available are:

- AMER-W
- AMER-C
- AMER-E
- APAC
- EMEA

### location

The city/state in which the support team member resides

### tzdata_timezone

The support team member's  timezone

### country

The country in which the support team member resides

### start_date

The date the support team member started at GitLab

### calendly

The link to the support-team member's calendly. Should always be the link to their *main* page, not an event.

### languages

An array of languages the support team member knows

### pagerduty

A hash containing Pagerduty information

- Should consist of an attribute `id`, which is the support team member's Pagerduty user ID

### focuses

An array containing the support team member's focuses

Each focuses array contains a hash with the attribures of:

- `name`, which is the name of the focus
- `percentage`, which is the percentage of the focus

All percentages should add up to be 100.

A list of current focuses available are:

- `Onboarding` - focused on onboarding to their position
- `SaaS` - focused on working Global SaaS support tickets
- `License and Renewals` - focused on working Global L&R support tickets
- `Self-Managed` - focused on working Global Self-Managed support tickets
- `Operations` - focused on Support Operations responsibilities
- `Management` - focused on Support Leadership responsibilities
- `US Federal` - focused on working US Federal support tickets
- `ASE` - focused on Assigned Support Engineer work

#### Additional info about the ASE focus

When the name of the focus is `ASE`, additonal attributes can be added to the hash:

- `zendesk`, which species the instance the organizations are on
- `organizations`, which is an array of information about the specific organizations, having the attributes of:
  - `id`, which is the Zendesk ID for the organization
  - `percentage`, which specifies the percent of ASE time spent on that organization

As an example, if Bob spent 50% of his time as an ASE in the Global Zendesk instance, and managed two organizations (123 and 456) evenly, he would enter his ASE focus object like so:

```yaml
focuses:
- name: 'Self-managed'
  percentage: 50
- name: 'ASE'
  percentage: 50
  zendesk: global
  organizations:
  - id: 123
    percentage: 50
  - id: 456
    percentage: 50
```

This means Bob spends 50% of his time doing Self-Managed work, and 50% of his time doing ASE work. And of that ASE work, 50% of it is for org 123 and 50% is for org 456.

Another example, if Bob spent 60% of his time as an ASE in the US Government, and managed two organizations (123 and 456) with different percentages, he would enter his ASE focus object like so:

```yaml
focuses:
- name: 'Self-managed'
  percentage: 40
- name: 'ASE'
  percentage: 60
  zendesk: us-federal
  organizations:
  - id: 123
    percentage: 25
  - id: 456
    percentage: 75
```

This means Bob spends 40% of his time doing Self-Managed work, and 60% of his time doing ASE work. And of that ASE work, 25% of it is for org 123 and 75% is for org 456.

### zendesk

A hash containing Zendesk information.

The attribures are:

- `main`, which is a hash containing the information pertaining to Zendesk Global
- `us-federal`, which is a hash containing the information pertaining to Zendesk US Government

Each of those attributes have further child attributes within them:

- `id`, which is the support team member's Zendesk user ID
- `groups`, which is the groups the support team member's Zendesk user is in
- `role`, which is the role the support team member's Zendesk user has
- `show_in_signature`, which is a hash containing an attribute of:
  - `gitlab_handle`, which tells the agent sync to add a line to your signature including your GitLab.com handle
- `alias`, which is what display name to use in Zendesk. If left blank, your full name will be used as the default
- `salutations`, which is an array of salutations to use in a support team member's Zendesk user's signature
- `article_publisher`, which determines if you will have Zendesk article publisher rights or not

#### Additional info about the US Government round robin

For the `us-federal` attribute, there is an additional attribute:

- `round_robin`, which is a Hash cotnaining the attribures:
  - `active`:, which dictates whether you are part of the round robin or not
  - `modifier`, which is the modifier to multiply by when calculating your total workload weight. In the event this number is 0, the round robin will use 1

### gitlab

A hash containing GitLab.com information.

The attribures are:

- `id`, which is the support team member's GitLab.com user ID
- `username`, which is the support team member's GitLab.com username
- `works_accou, which nt_deletion`, which dictates whether the support team member works Account Deletion issues
- `notes_link`, which is a link the team member uses for notes

### slack

A hash containing Slack information.

The attribures are:

- `id`, which is the support team member's Slack user ID
- `username`, which is the support team member's Slack handle

### modules

An array of learning modules the support team member has completed

### knowledge_areas

An array of areas in which the support team member is knowledgeable.

Each item is a Hash containing information about the support team member's perceived knowledgeable on along with the corresponding skill level they have on it.

Each item's attribures are:

- `name`, which is the knowledge area's name
- `level`, which is the support team member's knowledge level of the area
  1. Learning - I'm still learning the basics and I'm not yet ready to take tickets.
  1. Ready to work tickets - I'm ready to work on tickets, or learn by working on tickets.
  1. Looking to help others - I want to help others with tickets or learning.

### hobbies

An array of the support team member's hobbies

### pronouns

The preferred pronouns of the support team member
