---
title: Zendesk Ticket Basics
category: Handling tickets
description: Information about various Zendesk ticket fields, behaviors and procedures
---

## Ticket status

Each ticket in Zendesk has a [status](https://support.zendesk.com/hc/en-us/articles/4408832151834-Updating-and-solving-tickets)
that indicates its current state.

### Ticket statuses and their descriptions

| Status   | State | Notes |
| -------- | ------- | ----- |
| New      | The ticket has just been submitted and has had no replies. |  |
| Open     | The ticket has had one or more replies, and the user is waiting on GitLab Support to provide the next reply. | |
| Pending  | Support has replied to the ticket and is waiting on the user to respond. | If the user does not respond for 20 days, Zendesk will change the status of the ticket to `Solved`. |
| On-Hold  | Support is working on the ticket or is awaiting information from another GitLab team | See [Behavior of `On-Hold` tickets](#behavior-of-on-hold-tickets) |
| Solved   | The ticket has been solved | When a user replies to a `Solved` ticket, Zendesk reopens it. We automatically change a Solved ticket's status to `Closed` after 7 days. |
| Closed   | The ticket is archived | When a user replies to a `Closed` ticket, Zendesk opens a new ticket with a note that relates it to the closed one. |

### Make sure to reply to the user

If a user's reply is the last one in the ticket, make sure to send a public
reply when changing the ticket status.

Changing a ticket's status (except for `Solved`) without replying will not stop
the ticket's breach clock. See [SLA clock](#sla-clock) for more details.

### Avoiding status change automations

By default, our Zendesk automations will do the following:

- After 7 days in `Pending`, it will send a notification to the user we are still awaiting a response from them.
- After 14 days in `Pending`, it will send another notification and mark the ticket as `Solved`.
- After 7 days in `Solved`, it will close the ticket.

While this is normally the right workflow, there might be situations
in which you need to prevent this from occurring. To do so, use the appropriate
Zendesk labels:

| Label | What it does |
|-------|--------------|
| skip_autosolve | This tells Zendesk to refrain from moving the ticket to `Solved` automatically |
| skip_autoclose | This tells Zendesk to refrain from moving the ticket to `Closed` automatically |

NOTE: If the ticket has been reopened after already auto-solving and we want to
prevent autosolve from happening again, the `autosolve` and `autosolve_message`
tags will be present. These do NOT need to be removed  when adding the
`skip_autosolve` tag.

### Behavior of `On-Hold` tickets

We have a number of automations around tickets in an `On-Hold` status:

- When a ticket is set to `On-Hold`, it will be automatically assigned to you by
  the trigger [`Automatically assign on-hold ticket to the engineer who put it to the on-hold status`](https://gitlab.zendesk.com/agent/admin/triggers/360033242313).
- Tickets without an assignee will be automatically reopened by the trigger
[`Automatically reopen on-hold tickets without assignee`](https://gitlab.zendesk.com/agent/admin/triggers/360028981853).
- Tickets with an assignee will be automatically reopened in 4 days by the
  automation [`Reopen on-hold tickets after 4 days`](https://gitlab.zendesk.com/agent/admin/automations/360028978393), unless the ticket is of type **Task**.

## SLA clock

If a customer's reply is the last one in the ticket, do not set it to any status
silently (except for `Solved`), because the SLA clock will continue to run
and the ticket may breach SLA silently. Instead, send a confirmation, greeting, or
other message, while also changing the status.

## Ticket subject

Ensure that the subject of a support ticket is both descriptive and accurate.
You can edit the Subject to fix typos or make the problem clearer. Some examples
include:

- gitlab error 500 on login -> gitlab error 500 on login due to no partition of
  relation "audit_events"
- My Account was Blockes -> My Account was Blocked
- git reconfigure with below errors -> git reconfigure with
  letsencrypt_certificate errors

## Other ticket fields

Ticket fields help us capture important data that will help us improve the user
experience.

Depending on the view in which you are working and the form that has been
selected for the ticket, you might need to fill out some ticket fields manually.
As a high percentage of our tickets are solved or closed automatically through
our workflows, it is important to begin your work on a ticket by setting
appropriate values in all of the required (*) fields and relevant non-required
fields.

## Adding CCs to a ticket

Do not try to add external contacts to the CCs of a ticket, even if the customer asks you to.
As a matter of security policy, customers have to add CCs themselves. Direct the customer to the
[corresponding instructions](https://about.gitlab.com/support/portal/#adding-additional-participants-ccs-to-your-ticket) on how to do so.

You can still add internal contacts (like other SEs, the customer's CSM, …) yourself.

## Handling Large Files

Zendesk has a [fixed maximum attachment size](https://support.zendesk.com/hc/en-us/articles/4408882848538-Can-I-change-the-attachment-size-limit-in-ticket-comments) of 50MB per file. If you need a user to share a larger file than this, then see [Provide Large Files to GitLab Support](https://about.gitlab.com/support/providing-large-files/) for information on how to do so.

## Merging tickets

**WARNING:** Any attached files in the to be merged tickets will be shared
across the tickets. Everyone in CC on both of these tickets will receive the
files.

When [Merging Tickets](https://support.zendesk.com/hc/en-us/articles/4408882445594-Merging-tickets),
leave `Requester can see this comment` **unchecked** in the ticket that's being
merged into (the second ticket from the top) in order to maintain the SLA. If
the merge comment is made public, Zendesk considers it a response and removes
the SLA. The ticket that was merged into another ticket is closed while the
status of the target ticket is unaffected.

**NOTE:** Any ticket merge is final -- there is no option to undo it.

## ZenGuard - Action Warning System

ZenGuard is a Zendesk application deployed on Global Zendesk only. The app provides warning dialogs and confirmation prompts for high-risk actions that could lead to unwanted results. It helps prevent common mistakes that require tickets to be reopened or recreated.

### What ZenGuard protects against

The app provides warnings and blocks certain actions:

- **Due date issues**: Setting due dates in the past, or too far in the future
- **External collaborator risks**: Adding end-users as collaborators/CC 
- **Status change without response**: Setting a ticket to pending with only an internal note
- **On-hold timer reset**: Sending a public reply on an on-hold ticket that will not reset the SLA timer
- **Missing public reply**: Setting ticket to on-hold without a public reply 
- **Form change closure**: Changing ticket form which will cause automatic closure 

### How ZenGuard works

When you attempt a potentially problematic action, ZenGuard will:

1. **Display a warning dialog** explaining the potential issue
2. **Block the action** if it cannot be bypassed (marked as "this cannot be bypassed")
3. **Allow bypass** for certain warnings by [refreshing](#how-to-refresh-zenguard) the app or proceeding after confirmation, the action blocked can be bypassed

### Common scenarios and solutions

#### Bypassing warnings

Some warnings can be bypassed by either of the following::

- [Refreshing](#how-to-refresh-zenguard) the ZenGuard app in your browser
- Clicking through the confirmation dialog (where permitted)

Note that critical safety checks (like setting pending without any response) cannot be bypassed.

#### How to refresh ZenGuard

1. Click in to the ZenGuard app using either the icon on your apps list (right side of Zendesk), or if you can't see it, click the + to pin a new app and select ZenGuard.
2. Click the reload button in the title of the app. 

![Browser plug-in](/images/support/workflows/assets/zenguard-reload.png)

#### Troubleshooting

If ZenGuard prevents a legitimate action:

1. Check if there's a bypass option in the warning dialog
2. Ensure all required fields are properly filled
3. For macro-related issues, wait a moment and resubmit
4. If the problem persists, open a new issue in the [Support Operations project](https://gitlab.com/gitlab-com/gl-security/corp/cust-support-ops/issue-tracker/-/issues/new?issuable_template=Bug)

### Related resources

- [RFC: What Zendesk "pitfalls" are we most worried about when working tickets](https://gitlab.com/gitlab-com/support/support-team-meta/-/issues/6683#top)
- Support Operations issue: [Feature Request: Zendesk Action Warning System](https://gitlab.com/gitlab-com/gl-security/corp/cust-support-ops/issue-tracker/-/issues/122)
- Support Deployment issue: [ZenGuard App Deployment - Zendesk Action Warning System](https://gitlab.com/gitlab-com/support/support-team-meta/-/issues/6898)
