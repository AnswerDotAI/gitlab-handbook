---
title: Apps
description: Operations documentation page for Zendesk apps
canonical_path: "/handbook/security/customer-support-operations/docs/zendesk/apps"
---

{{% alert title="Note" color="primary" %}}

This is an informational page for the Zendesk apps. It may not reflect the way we actually manage Zendesk apps.

If you are looking for information about maintaining apps (creating, editing, etc.), please see [Apps workflow](../../workflows/zendesk/apps)

{{% /alert %}}

## What is a Zendesk App

A Zendesk App is an application (written in HTML/CSS/JS) that runs in a location of Zendesk. What it does and how it does it varies greatly from application to application. Applications can be run in a great many places, but the traditional locations are:

- [Ticket sidebar](https://developer.zendesk.com/api-reference/apps/apps-support-api/ticket_sidebar/)
- [User sidebar](https://developer.zendesk.com/api-reference/apps/apps-support-api/user_sidebar/)
- [Organization sidebar](https://developer.zendesk.com/api-reference/apps/apps-support-api/organization_sidebar/)
- [Navbar](https://developer.zendesk.com/api-reference/apps/apps-support-api/nav_bar/)
- [Background](https://developer.zendesk.com/api-reference/apps/apps-support-api/background/)

You can see more resources on application locations via the [Zendesk Developer Manifest Reference](https://developer.zendesk.com/documentation/apps/app-developer-guide/manifest/#location) documentation.

Zendesk applications tend to come from one of two areas:

- [Zendesk Marketplace](https://www.zendesk.com/apps/)
- Developed in-house

## Installing a private app

https://developer.zendesk.com/documentation/ticketing/using-the-zendesk-api/creating-and-managing-private-apps/#creating-an-app

## Updating a private app

https://developer.zendesk.com/documentation/ticketing/using-the-zendesk-api/creating-and-managing-private-apps/#updating-an-app

## Zendesk Global apps

### Advanced SAST App

<sup>*Introduced via [support-team-meta#6652](https://gitlab.com/gitlab-com/support/support-team-meta/-/issues/6652)*</sup>

The Advanced SAST App is a ticket app that enables a quick working of User requests for source code of LGPL-licensed components in GitLab Advanced SAST.

App information:

- Located in the ticket sidebar
- Restricted by Group:
  - Support AMER
  - Support APAC
  - Support EMEA
- This application was developed in-house and can be found [Advanced SAST App project](https://gitlab.com/gitlab-support-readiness/zendesk-global/apps/advanced-sast-app).

### Advanced Search

Advanced Search is an app that provides a simple visual interface for constructing complex search queries against tickets, users, and organizations (orgs). It also enables you to export the search results in a CSV format.

App information:

- Located in the navbar
- This application was developed by [Zendesk](https://www.zendesk.com/marketplace/partners/zendesk/) and is available in the [Zendesk Marketplace](https://www.zendesk.com/marketplace/apps/support/198393/advanced-search/).

### GitLab Reminders App

<sup>*Introduced via [support-team-meta#3036](https://gitlab.com/gitlab-com/support/support-team-meta/-/issues/3036)*</sup>

The Reminders App appears in the navbar and allows the agent a more specialized view of tickets they are involved in. It currently shows:

- Tickets assigned to you with a pending/overdue task that are not in a Closed state
- Recent tickets you have viewed
- Tickets assigned to you that are not in a Closed state
- Tickets you are CC'd on that are not in a Closed state

It also allows you to quickly manage your tasks by seeing the notes you have left for said task, when it is due, and a button to quickly mark the task as done (remove the notes and due date).

App information:

- Located in the navbar
- This application was developed in-house and can be found [GitLab Reminders App project](https://gitlab.com/gitlab-support-readiness/zendesk-global/apps/reminders-app).

### GitLab Search

This app lets you use the gitlab.com API to search for issues/merge requests within Zendesk.

App information:

- Located in the topbar
- This application was developed in-house and can be found [GitLab Search project](https://gitlab.com/gitlab-support-readiness/zendesk-global/apps/gitlab-search).

### GitLab Super App

<sup>*Introduced via [support-ops-project#801](https://gitlab.com/gitlab-com/support/support-ops/support-ops-project/-/issues/801)*</sup>

A plugin controlled app that can do several things GitLab related

The current plugins are:

- **User Lookup**
  > This lets you search gitlab.com for a username or email. It then displays information based on the results.
- **Namespace Lookup**
  > This lets you search gitlab.com for a namespace. It then displays information based on the results.
- **Collaboration Project**
  > This checks the organization for a collaboration project ID. If one exists, it then provides a link to said project.
- **2FA Helper**
  > This creates a usable form to checking if a 2FA verification has passed. It calculates the Risk Factor from the Data Classification and modifies it to reflect the passed challenges.
- **Email Suppressions**
  > This searches mailgun for suppressions from bounces (note it does not do it on complaints or unsubscribes). It will display the results (with the message for the suppression).
  >
  > It also gives the option of removing the suppression (if one if found). Doing so deletes it from mailgun and adds an intenral comment on the ticket with the results of the suppression deletion.
- **Fieldnotes**
  > This app checks the [Fieldnotes project](https://gitlab.com/gitlab-com/support/fieldnotes/-/issues) for any existing Issues which reference the current Zendesk ticket ID. If no existing Issues are found, then agents are able to create a new Fieldnotes Issue from directly within the Zendesk ticket.
- **2FA Validator**
  > This app checks values entered by a support engineer and does a validation check. This effectively acts as the second layer of validation

App information:

- Located in the ticket sidebar
- Restricted by Group:
  - Support AMER
  - Support APAC
  - Support EMEA
- This application was developed in-house and can be found [GitLab Super App project](https://gitlab.com/gitlab-support-readiness/zendesk-global/apps/gitlab-super-app).

### GitLab Views

The GitLab Views appears in the navbar and allows the agent a more customizable set if Zendesk views.

App information:

- Located in the navbar
- Restricted by Group:
  - Support AMER
  - Support APAC
  - Support EMEA
  - Support Managers
  - Support Ops
- This application was developed in-house and can be found [GitLab Views App project](https://gitlab.com/gitlab-support-readiness/zendesk-global/apps/views-app).

### Mechanizer

Please use [CustomersDot Support Admin Tools](/handbook/support/license-and-renewals/workflows/customersdot/support_tools) instead of the app at this time.

<sup>*Introduced via [support-team-meta#4208](https://gitlab.com/gitlab-com/support/support-team-meta/-/issues/4208)*</sup>

This app incorporates Mechanizer into Zendesk.

App information:

- Located in the ticket sidebar
- Restricted by Group:
  - Support AMER
  - Support APAC
  - Support EMEA
- This application was developed in-house and can be found at [Mechanizer project](https://gitlab.com/gitlab-support-readiness/zendesk-global/apps/mechanizer)

### Notifications App

{{% alert title="Note" color="primary" %}}

This app is *opt-in*. This means nothing will happen unless you modify your user settings to receive notifications.

{{% /alert %}}

This app handles posting notifications at the top of the screen, depending on various conditions and user settings.

App information:

- Located in the Top Navigation of Zendesk Global
- Restricted by Group:
  - Support AMER
  - Support APAC
  - Support EMEA
  - Support Managers
  - Support Ops
- This applicate was developed in-house and can be found at [Notification app project](https://gitlab.com/gitlab-support-readiness/zendesk-global/apps/notification-app)

#### Current events that trigger the app

The following events will send data to the app for notification processing:

- Agent private comment made on ticket
- Agent public comment made on ticket
- Customer public comment made on ticket
- Emergency ticket created
- Escalated ticket created
- Tickets being STAR'd
- Tickets created by specific organizations

#### User settings

The current user settings, which will determine what notifications you will (and will not) recieve are:

- Play notification sound
  - Checking this box tells the app to play the notification sound.
- Notify me for
  - This tells the app what kind of tickets to notify you for
  - Values:
    - Assigned tickets only
    - CC'd tickets only
    - All tickets
- Notify me about
  - This tells the app what kind of events to notify you for
  - Values:
    - All public comments (agent and customer)
    - Only public comments from agents
    - Only public comments from customers
    - Only private comments
    - All types of comments
- Notify me only for tickets with priority
  - This tells the app which priorities to notify you on
  - Values:
    - at least Urgent
    - at least High
    - at least Medium
    - at least Low
  - **Note** A blank value is assumed to be "all priorities"
- Also notify me for escalated ticket creation
  - This dictates if you want to be notified via the app when an escalated organization creates a ticket.
  - **Note** This works *independently* of all other settings.
- Also notify me for emergency ticket creation
  - This dictates if you want to be notified via the app when an emergency ticket is created.
  - **Note** This works *independently* of all other settings.
- Also notify me for STARs
- Also notify me for soon to breach tickets on
  - This dictates if you want to be notified via the app when a ticket is about to breach (within 2 hours)
  - Values:
    - Assigned tickets only
    - CC'd tickets only
    - Tickets within my SGG only
    - All tickets
  - **Note** This works *independently* of all other settings.
- Also notify me for tickets created via specific orgs
  - This dictates if you want to be notified via the app when a ticket is created by a specific organization
  - The list should be comma separated
    - Example, if you want to be notified for organizations 123, 456, and 789, use the value `123,456,789` or `123, 456, 789`
  - **Note** This works *independently* of all other settings.

For information on editing your personal user settings, please see [Zendesk's documentation](https://support.zendesk.com/hc/en-us/articles/4408819930906-Editing-your-personal-settings-in-Zendesk-Chat-Support-accounts#topic_gfh_rqm_4fb).

### Out of Office

<sup>*Introduced via [support-team-meta#4303](https://gitlab.com/gitlab-com/support/support-team-meta/-/issues/4303)*</sup>

This will enable an agent to mark when they are out of office in Zendesk, which then updates tickets and makes it visible in the views.

Managers are also able to do this for their reports.

App information:

- Located in the navbar
- Restricted by Group:
  - Support AMER
  - Support APAC
  - Support EMEA
- This application was developed in-house and can be found [Out of Office project](https://gitlab.com/gitlab-support-readiness/zendesk-global/apps/out-of-office)

### Support Ops Super App

A plugin controlled app that can do several things Support Ops related

The current plugins are:

- **Namespace Lookup**
  > This lets you search gitlab.com for a namespace. It then displays information based on the results. This is related to the one in the GitLab Super App, but instead it shows less information and shows the SFDC IDs it is associated with.
- **Project Lookup**
  > This lets you search gitlab.com for a project. It then displays information based on the results.
- **Attempt Association**
  > On tickets where the product type is `GitLab.com`, clicking the button on the plugin will attempt to auto-associate the requester to an organizaiton. If that is not possible, it will detail why it was not possible.
- **Associate User**
  > On a Support Ops ticket, it will ask you for an email address. It will then use the organization on the current ticket to associate said email address to that organization.
- **CMP Developers**
  > Outputs a list of CMP developers (by email) for an organization (if it has a CMP)

App information:

- Located in the ticket sidebar
- Restricted by Role:
  - Admin
- This application was developed in-house and can be found [Support Ops Super App project](https://gitlab.com/gitlab-support-readiness/zendesk-global/apps/support-ops-super-app).

### Unbabel

<sup>*Introduced via [support-team-meta#1664](https://gitlab.com/gitlab-com/support/support-team-meta/-/issues/1664)*</sup>

Powered by state-of-the-art AI and a worldwide community of translators, Unbabel delivers translation at enterprise scale. We help you serve customers in any language, with fast, native-quality translations of your customer support tickets in Zendesk.

App information:

- Located in the ticket sidebar
- Restricted by Group:
  - Support AMER
  - Support APAC
  - Support EMEA
- This application was developed by Unbabel and is available in the [Zendesk Marketplace](https://www.zendesk.com/marketplace/apps/support/43875/unbabel-for-zendesk-support/).

#### Replying with a Translation

To request a translation automatically, simply reply as you normally would as an internal note with the #unbabel hashtag included at the top of your content.

Please also ensure that the `unbabel_en`, `unbabel_reply`, `unbabeled` tags are included, otherwise your response might not be translated automatically. Should this happen, you will need to add the missing tags, and create a new internal note with the #unbabel hashtag included at the top of your content.

Once you submit your response, it may take several seconds for Unbabel to automatically translate your internal comment, but it can take several minutes if a human is required to manually translate your internal comment. To view the status of the translation, you can open the Apps sidebar in the ticket, and scroll down to the **Unbabel for Zendesk Support** box.

After a translated response has been sent to the customer via Unbabel it is necessary to manually set the ticket status as **Pending** since Unbabel will incorrectly set the ticket status as **Open**. You must do this with an *empty comment* (remove any `#unbabel` added by the plugin, before you Submit as Pending).

#### Excluding Text from Translation

The highlighted code can be skipped for translation by adding 3 brackets around the text:

```string
<<< text/code >>>
```

The above can also be used to protect sensitive information from a human translator when sending a translation request.

#### Disabling Unbabel in a Specific Ticket

Sometimes Unbabel is triggered if a customer's signature was written in a language that requires translation but the customer replies in English, and the translation is not needed. In this case, there is a way to disable Unbabel in this specific ticket:

- Open the ticket in question.
- Click Apps > Unbabel for Zendesk Support.
- `Change` the `Customer language` to `English`.

From now on, Unbabel will not be triggered in this ticket.

#### Help with Translation

If for some reason you have difficulty in understanding the automated translation, an actual human intervention can actually be requested. Simply click the link `Can't understand the translation?` in the Unbabel app box and this will send your response for translation to Unbabel editors.

#### Best Practices for Unbabel

As indicated in the training session, please keep in mind of the following best practices when writing a response for translation.

- Respond in one language
  - It is likely that you can speak another language and understand what the customer is trying to say. Please ensure that you only use the English language when responding tickets as the system may not detect the language correctly.
- Copy only the body of the content that needs translation.
  - When referring to a quoted texts from our customers, please only use the content that requires translation. Including snippets/code/elements may take more time to translate and could result in a mistranslation.
- Mind the punctuation.
  - Punctuation can be sometimes tricky for Unbabel so please be sure there are no unnecessary periods/punctuations in between.
- Single Word Use
  - It is likely that the response you are sending may be lost in translation, for example the word `pass` would differ to a `boarding pass`.

### Zendesk Super App

<sup>*Introduced via [support-ops-project#801](https://gitlab.com/gitlab-com/support/support-ops/support-ops-project/-/issues/801)*</sup>

A plugin controlled app that can do several things Zendesk related

The current plugins are:

- **Create new ticket**
  > Allows an agent to create a new ticket using the same user as the ticket they are currently on.
- **Due date picker**
  > This allows you to customize what the Due Date for a Task ticket is set for. By default, Zendesk only allows setting the date. This enables you to set the date, time, and timezone.
  >
  > You can also set the Due Date Note and disable (or enable) task notifications using this app.
- **Escalated tickets**
  > This searches for tickets under the organization that have been escalated within the last 6 months.
- **Related tickets**
  > This looks for tickets related to the current one based off the category (or subcategory) the ticket is currently using. It then displays up to 5 of them (sorted by the update_at value of the ticket, descending).
- **Attachments**
  > Displays attachments present on the ticket.

App information:

- Located in the ticket sidebar
- Restricted by Group:
  - Support AMER
  - Support APAC
  - Support EMEA
- This application was developed in-house and can be found [Zendesk Super App project](https://gitlab.com/gitlab-support-readiness/zendesk-global/apps/zendesk-super-app).

### ZenDuo

<sup>*Introduced via [gitlab-com/support/support-team-meta#6689](https://gitlab.com/gitlab-com/support/support-team-meta/-/issues/6689)*</sup>

The ZenDuo application enables Duo Chat to work with Zendesk tickets.

You can choose from two pre-defined prompts:

- Summarize conversation
- Suggest KB article

or define up to two custom prompts.

For each custom prompt, you configure:

- Title: this is shown in the prompt dropdown list
- Button: the text shown on the action button
- Prompt: the actual prompt. Use the `<<ticket-content>>` placeholder, which will be replaced by the ticket content. 

When you run a prompt, the application will send the ticket content (excluding file attachments) to Duo Chat and show its reply.

Note that large tickets have to be sent in multiple parts, so it can take a while before Duo Chat replies.

Once you've received a reply, you can choose:

- Copy to clipboard: copy the complete conversation (prompts and replies) to the clipboard.
- Chat: continue the conversation with Duo Chat.
- Done: hide the conversation, and be ready to start a new one.

When you send the initial prompt, a fresh conversation is always started, so there is no need to instruct Duo Chat to forget previous conversations.

The conversations you have with Duo Chat also show up in the GitLab Duo Chat history on e.g. GitLab.com as `ZenDuo <ticket#> <prompt>`.
You can use this history to look up previous conversations, or continue on an old conversation.

App information:

- Located in the ticket sidebar
- This application was developed in-house and can be found [ZenDuo project](https://gitlab.com/gitlab-support-readiness/zendesk-global/apps/zenduo).

### ZenGuard

<sup>*Introduced via [gitlab-com/gl-security/corp/cust-support-ops/issue-tracker#122](https://gitlab.com/gitlab-com/gl-security/corp/cust-support-ops/issue-tracker/-/issues/122)*</sup>

Implements a warning system into Zendesk to warn (or block) potentially dangerous actions.

Current list of checks:

- Checks if due date is in the past, present, or too far in the future
- Checks if adding an end-user as a collaborator/CC
- Checks if setting to pending with an internal note
- Checks if trying to send a public reply on an on-hold ticket in a way that won't reset the timer
- Checks if trying to set it on-hold without a public reply (except for accepted situations)
- Checks if setting ticket to pending without a reply
- Checks if making unapproved form changes

App information:

- Located in the ticket sidebar
- This application was developed in-house and can be found in the [ZenGuard project](https://gitlab.com/gitlab-support-readiness/zendesk-global/apps/zenguard).

## Zendesk US Government apps

### Advanced SAST App

<sup>*Introduced via [support-team-meta#6652](https://gitlab.com/gitlab-com/support/support-team-meta/-/issues/6652)*</sup>

The Advanced SAST App is a ticket app that enables a quick working of User requests for source code of LGPL-licensed components in GitLab Advanced SAST.

App information:

- Located in the ticket sidebar
- Restricted by Group:
  - Support
  - Support Managers
  - Support Operations
- This application was developed in-house and can be found [Advanced SAST App project](https://gitlab.com/gitlab-support-readiness/zendesk-us-government/apps/advanced-sast-app).

### Advanced Search

Advanced Search is an app that provides a simple visual interface for constructing complex search queries against tickets, users, and organizations (orgs). It also enables you to export the search results in a CSV format.

App information:

- Located in the navbar
- This application was developed by [Zendesk](https://www.zendesk.com/marketplace/partners/zendesk/) and is available in the [Zendesk Marketplace](https://www.zendesk.com/marketplace/apps/support/198393/advanced-search/).

### Architecture Diagrams

<sup>*Introduced via [support-ops-project#801](https://gitlab.com/gitlab-com/support/support-ops/support-ops-project/-/issues/801)*</sup>

This app uses the Organization field `AM Project ID` to check for an existing Account Management project. If it finds it, it will then link to that project's Architecture Diagram.

App information:

- Located in the ticket sidebar
- This application was developed in-house and can be found [GitLab Architecture project](https://gitlab.com/gitlab-support-readiness/zendesk-us-government/apps/gitlab-architecture).

### GitLab Reminders App

<sup>*Introduced via [support-team-meta#3036](https://gitlab.com/gitlab-com/support/support-team-meta/-/issues/3036)*</sup>

The Reminders App appears in the navbar and allows the agent a more specialized view of tickets they are involved in. It currently shows:

- Tickets assigned to you with a pending/overdue task that are not in a Closed state
- Recent tickets you have viewed
- Tickets assigned to you that are not in a Closed state
- Tickets you are CC'd on that are not in a Closed state

It also allows you to quickly manage your tasks by seeing the notes you have left for said task, when it is due, and a button to quickly mark the task as done (remove the notes and due date).

App information:

- Located in the navbar
- This application was developed in-house and can be found [GitLab Reminders App project](https://gitlab.com/gitlab-support-readiness/zendesk-us-government/apps/reminders-app).

### GitLab Search

This app lets you use the gitlab.com API to search for issues/merge requests within Zendesk.

App information:

- Located in the topbar
- This application was developed in-house and can be found [GitLab Search project](https://gitlab.com/gitlab-support-readiness/zendesk-us-government/apps/gitlab-search).

### Show Related Tickets

This uses the ticket subject to search for other tickets with a similar subject. This helps to locate potentially related tickets you can check to see how they were solved.

App information:

- Located in the ticket sidebar
- This application was developed by [Zendesk](https://www.zendesk.com/marketplace/partners/zendesk/) and is available in the [Zendesk Marketplace](https://www.zendesk.com/marketplace/apps/support/5131/show-related-tickets/).

### Zendesk Super App

<sup>*Introduced via [support-ops-project#801](https://gitlab.com/gitlab-com/support/support-ops/support-ops-project/-/issues/801)*</sup>

A plugin controlled app that can do several things Zendesk related

The current plugins are:

- **Create new ticket**
  > Allows an agent to create a new ticket using the same user as the ticket they are currently on.
- **Due date picker**
  > This allows you to customize what the Due Date for a Task ticket is set for. By default, Zendesk only allows setting the date. This enables you to set the date, time, and timezone.
  >
  > You can also set the Due Date Note and disable (or enable) task notifications using this app.
- **Escalated tickets**
  > This searches for tickets under the organization that have been escalated within the last 6 months.
- **Related tickets**
  > This looks for tickets related to the current one based off the category (or subcategory) the ticket is currently using. It then displays up to 5 of them (sorted by the update_at value of the ticket, descending).
- **Attachments**
  > Displays attachments present on the ticket.

App information:

- Located in the ticket sidebar
- Restricted by Group:
  - Support
  - Support Managers
  - Support Operations
- This application was developed in-house and can be found [Zendesk Super App project](https://gitlab.com/gitlab-support-readiness/zendesk-us-government/apps/zendesk-super-app).

### ZenDuo

<sup>*Introduced via [gitlab-com/support/support-team-meta#6689](https://gitlab.com/gitlab-com/support/support-team-meta/-/issues/6689)*</sup>

The ZenDuo application enables Duo Chat to work with Zendesk tickets.

You can choose from two pre-defined prompts:

- Summarize conversation
- Suggest KB article

or define up to two custom prompts.

For each custom prompt, you configure:

- Title: this is shown in the prompt dropdown list
- Button: the text shown on the action button
- Prompt: the actual prompt. Use the `<<ticket-content>>` placeholder, which will be replaced by the ticket content. 

When you run a prompt, the application will send the ticket content (excluding file attachments) to Duo Chat and show its reply.

Note that large tickets have to be sent in multiple parts, so it can take a while before Duo Chat replies.

Once you've received a reply, you can choose:

- Copy to clipboard: copy the complete conversation (prompts and replies) to the clipboard.
- Chat: continue the conversation with Duo Chat.
- Done: hide the conversation, and be ready to start a new one.

When you send the initial prompt, a fresh conversation is always started, so there is no need to instruct Duo Chat to forget previous conversations.

The conversations you have with Duo Chat also show up in the GitLab Duo Chat history on e.g. GitLab.com as `ZenDuo <ticket#> <prompt>`.
You can use this history to look up previous conversations, or continue on an old conversation.

App information:

- Located in the ticket sidebar
- This application was developed in-house and can be found [ZenDuo project](https://gitlab.com/gitlab-support-readiness/zendesk-us-government/apps/zenduo).

### ZenGuard

<sup>*Introduced via [gitlab-com/gl-security/corp/cust-support-ops/issue-tracker#122](https://gitlab.com/gitlab-com/gl-security/corp/cust-support-ops/issue-tracker/-/issues/122)*</sup>

Implements a warning system into Zendesk to warn (or block) potentially dangerous actions.

Current list of checks:

- Checks if due date is in the past, present, or too far in the future
- Checks if adding an end-user as a collaborator/CC
- Checks if setting to pending with an internal note
- Checks if trying to send a public reply on an on-hold ticket in a way that won't reset the timer
- Checks if trying to set it on-hold without a public reply (except for accepted situations)
- Checks if setting ticket to pending without a reply
- Checks if making unapproved form changes

App information:

- Located in the ticket sidebar
- This application was developed in-house and can be found in the [ZenGuard project](https://gitlab.com/gitlab-support-readiness/zendesk-us-government/apps/zenguard).

## App development

{{% alert title="Note" color="primary" %}}

This is generalized information we have found helpful in the course of app development. It is not a single source of truth.

{{% /alert %}}

### Understanding Zendesk Apps

Before you can start creating and editing apps in Zendesk, it is important to understand the ins and outs of both Zendesk Apps and [Zendesk Apps framework](https://developer.zendesk.com/documentation/apps/app-developer-guide/using-the-apps-framework/).

There is a lot to this, so the Zendesk documentation is the best resource you have to learn the various ins and outs. This training documentation will cover what is viewed at "the most important" parts, but it is highly recommended you read and reference the [Zendesk developer documentation](https://developer.zendesk.com/documentation/apps/app-developer-guide/getting_started/) as often as possible.

#### ZAT

ZAT, or Zendesk App Tools, is a ruby gem that makes working with Zendesk Apps locally considerably easier. It is highly recommended you install it on your computer:

```bash
gem install rake
gem install zendesk_apps_tools
```

To update it:

```bash
gem update rake
gem update zendesk_apps_tools
```

Sometimes on Mac terminal, you will get write permission error. You may use:

```bash
sudo gem update rake
sudo gem update zendesk_apps_tools
```

Note: ZAT is having issues with Ruby version `3.0.0 and plus`. You'll likely need to use old stable versions like `2.6.3p62`

#### manifest.json

This file is used to configure you application. As such, it is very important and vital it is accurate.

The common configuration settings are:

| Setting | What it does | Required? |
|---------|--------------|:---------:|
| name | Specifies the name of the app | Y |
| author | Specifies the author of the app | Y |
| version | Specifies the app version | Y |
| frameworkVersion | Specifies the framework version to use | Y |
| location | Specifies where the app appears | Y |
| defaultLocale | Specifies the locale of the app | Y |
| parameters | The parameters to pass to the app during installation | N |
| domainWhitelist  | The domains to allow use of secure parameters | N |
| private | Specifies whether the app can be only be installed in the app developer's account or not | N |

#### Location

This setting determines where the app will appear and run. This is a very important setting. The first setting determines the product type location, and within that setting you can specify many other configurations, including the physical location the app will appear in. For the product type location, we always use `support`.

The physical locations are as follows:

| String | Location/Purpose |
|--------|------------------|
| `ticket_sidebar` | The right side of all ticket view pages |
| `new_ticket_sidebar` | The right side of all new ticket pages |
| `ticket_editor` | A button on the ticket editor box |
| `nav_bar` | An icon on the left-side navigation bar |
| `top_bar` | An icon on the right side of the top menu |
| `user_sidebar` | The right side of all user view pages |
| `organization_sidebar` | The right side of all organization view pages |
| `background` | The app runs in the background and does not display anywhere |
| `modal` | Used when the app creates modals |

Within the physical location settings, you can include more configuration settings, with the most common being:

| String | What it does | Variable type |
|--------|--------------|---------------|
| `autoHide` | Tells the app to auto-collapse on first load | Boolean |
| `autoLoad` | Tells the app to automaticall local (defaults to true) | Boolean |
| `signed` | Specifies whether or not to use signed URLs | Boolean |
| `url` | The URL of the page to display in the iframe of the app | String |
| `size` | The initial app size (configure this in the app instead) | JSON |

As an example, to have an app load "<https://google.com>" automatically in the ticket sidebar with a starting height of 200px, your configuration block would look like this:

```json
"location": {
  "support": {
    "ticket_sidebar": {
      "autoLoad": true,
      "url": "https://google.com/",
      "size": {
        "height": "200px"
      }
    }
  }
}
```

As another example, to have your app load in both the user and organization pages, rendering the locale `assets/iframe.html` file, you would do this:

```json
"location": {
  "support": {
    "user_sidebar": "assets/iframe.html",
    "organization_sidebar": "assets/iframe.html",
  }
}
```

#### Parameters

This is where you would define variables you want the app to use during installation.

#### Domain whitelists

If your app is using secure parameters and you plan to make requests outside of Zendesk, you must whitelist the domains in question. Each parameter is a hash that contains the following:

- `name`: the name of the parameter
- `type`: the type of parameter
- `secure`: ensures users cannot see the variable value when making HTTP requests (you should *always* use this)
- `require`: specifies if the parameter is required for installation

As an example, to use two required parameters (`param1` and `param2`), both of which are text parameters in a secure way, you would do the following:

```json
"parameters": [
  {
    "name": "param1",
    "type": "text",
    "secure": true,
    "required": true
  },
  {
    "name": "param2",
    "type": "text",
    "secure": true,
    "required": true
  }
]
```

During the installation of the app, Zendesk will ask you to give the values for these parameters. To utilize this in the code of your app, you will use this:

`{{setting.NAME_OF_PARAMETER}}`

Where `NAME_OF_PARAMETER` is the name you gave the parameter in the manifest.json file.

#### init

To create a client instance of the ZAF (Zendesk App Framework) client, you need to ensure the following is present in the javascript of your app:

```javascript
var client = ZAFClient.init();
```

#### App resizing

To resize the app during runtime, you would use the `invoke` class, specifying you wish to invoke the `resize` function. This is done like so:

```javascript
// First line shown to clarify you use the ZAF client object to do this
var zafclient = ZAFClient.init();
zafclient.invoke('resize', { width: '100%', height: '100px' });
```

### Required javascript library

To utilize the ZAT, you must include the following javascript in your app's HTML file(s):

```html
<script src="https://static.zdassets.com/zendesk_app_framework_sdk/2.0/zaf_sdk.min.js"></script>
```

#### Getting metadata

To get metadata and use it in your app, you need to use the ZAF client's `get` function. This takes an array of values to get from the ticket metadata, which you use in a function.

As an example, to get the ticket requester's name and the ticket's organization, and then log them to the console, you would do the following:

```javascript
// First line shown to clarify you use the ZAF client object to do this
var zafclient = ZAFClient.init();
zafclient.get(['ticket.requester.name', 'ticket.organization']).then(function(data) {
  console.log("Ticket requester name: " + data['ticket.requester.name']);
  console.log("Ticket organization: " + data['ticket.organization']);
});
```

As another example, to get the ticket's due date and the due date notes (a custom ticket field) and then log them to the console, you would do the following:

```javascript
// First line shown to clarify you use the ZAF client object to do this
var zafclient = ZAFClient.init();
zafclient.get(['ticket.customField:due_date', 'ticket.customField:custom_field_360017383799']).then(function(data) {
  console.log("Due date": + data['ticket.customField:due_date']);
  console.log("Due date notes:" + data['ticket.customField:custom_field_360017383799']);
});
```

#### Making requests

Your app might need to make requests, whether they be "internal" (i.e. within Zendesk itself) or external. To do this, we use the `request` function of the client object.

The format of this is *very* close to that of making [AJAX requests](https://api.jquery.com/jquery.ajax/) in jQuery. The format you will normally use is:

```javascript
// First line shown to clarify you use the ZAF client object to do this
var zafclient = ZAFClient.init();
zafclient.request({
  method: 'REQUEST_TYPE',
  url: 'URL_TO_USE',
  contentType: 'CONTENT_MEDIA_TO_SEND',
  data: DATA_OBJECT,
  secure: BOOLEAN,
  headers: HEADERS_OBJECT
}).then(function(data) {
  // do stuff
});
```

The exact parameters in the request will vary from request to request.

As an example, if you wanted to update the due date of a ticket, you might do:

```javascript
// First line shown to clarify you use the ZAF client object to do this
var zafclient = ZAFClient.init();
zafclient.request({
  method: 'PUT',
  url: '/api/v2/tickets/123456.json',
  contentType: 'application/json',
  data: JSON.stringify({
    due_at: new Date('2021-01-01').toISOString()
  }),
  secure: BOOLEAN,
  headers: HEADERS_OBJECT
}).then(function(data) {
  console.log('Due date updated to 2021-01-01');
});
```

As another example, if you wanted to make a GET request to gitlab.com to find information about user ID 987654, using a secure parameter from app installation, you might do:

```javascript
// First line shown to clarify you use the ZAF client object to do this
var zafclient = ZAFClient.init();
zafclient.request({
  method: "GET",
  url: 'https://gitlab.com/api/v4/users/987654?private_token={{setting.GitLab_token}}',
  secure: true
}).then(function(data) {
  console.log('User email: ' + data.email);
});
```

### Testing an app

There are two ways to test a Zendesk app before you put it into production:

#### Locally

{{% alert title="Note" color="primary" %}}

This cannot be done if your app is using secure parameters. Instead, you would need to install the app into the Sandbox and test from there.

{{% /alert %}}

To test your app locally, cd into the app directory on your local computer and then run the `zat server` command. This will start up a ZAT server on your computer. Once it has booted up, go to a Zendesk URL and put `?zat=true` at the end. This will now load the apps from your local computer, allowing you to test out the app locally.

#### Via the Sandbox

If your app is using secure parameters, you will need to test via the Sandbox instead.
