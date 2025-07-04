---
title: How to Perform Customer Emergencies Duties
category: On-call
description: "Describes the role and responsibilities for Customer Emergencies rotation in Support Engineering"
---

## Introduction

Support Engineers in the Customer Emergencies rotation coordinate operational emergencies from GitLab customers.

The Customer Emergencies rotation is one of the rotations that make up [GitLab Support On-call](/handbook/support/on-call/).

## Things to Know

Before getting started, consider reviewing the following sections or to get straight into the workflow start at [Handling Self-managed Emergencies](#handling-self-managed-emergencies) section.

### How to be added to the Customer Emergencies PagerDuty rotation

To be added to the Customer Emergency On Call Rotation, you should have first completed the [Customer Emergency On-Call training module](https://gitlab.com/gitlab-com/support/support-training/-/issues/new) and then after agreement with your manager, you should raise a new [Pager Duty Issue](https://gitlab.com/gitlab-com/support/support-ops/other-software/pagerduty/-/issues) with the Support-Ops team requesting that you are added to the appropriate Pager Duty rotation.

#### Considerations in AMER

Customer Emergency shifts are 6-hour long overlapping shifts.

Due to an increase in concurrent emergencies, we have split the AMER shift into 3 overlapping schedules that are 6-hours in length to cover the 8 hour AMER on-call window. The schedules have been split to allow engineers to cover hours that align closest with their working hours.

- AMER 1 hours: 12:00 PM to 6:00 PM EDT (16:00 to 22:00 UTC)
- AMER 2 hours: 1:00 PM to 7:00 PM EDT (17:00 to 23:00 UTC)
- AMER 3 hours: 2:00 PM to 8:00 PM EDT (18:00 to 24:00 UTC)

This leaves the first and last hours of the AMER on-call window with a single engineer on-call. If multiple emergencies come in during these times, follow the [Handling multiple simultaneous emergencies](/handbook/support/workflows/customer_emergencies_workflows#handling-multiple-simultaneous-emergencies) workflow.

Each group is encouraged to coordinate a DRI role for the shift. The DRI will be responsible for taking assignment of the first emergency. The non-DRIs will take concurrent emergencies as they come in.

An example DRI schedule is below. Note that AMER 2 is DRI for 30 minutes longer since they will overlap with AMER 1 or AMER 3 across all of their shift hours.

- AMER 1 DRI: 12:00pm - 14:30pm EDT
- AMER 2 DRI: 14:30pm - 17:30pm EDT
- AMER 3 DRI: 17:30pm - 20:00 EDT

### Emergencies

Emergencies can be raised by GitLab customers by submitting reports on the [Emergency Support form](https://about.gitlab.com/support/#how-to-engage-emergency-support) for the following:

- [Self-managed Emergencies](#handling-self-managed-emergencies)
- [SaaS (GitLab.com) Emergencies](#saas-emergencies)
- [Advanced or Signature Success Tier Emergencies](#supporting-247-coverage-for-customers-on-the-advanced-or-signature-success-tier----phase-1)
- [License Emergencies](#license-emergencies)
- [GitLab Dedicated Emergencies](#gitlab-dedicated-emergencies)

### PagerDuty

We use PagerDuty to keep track of emergencies raised by GitLab customers. For any [customer emergency](#emergencies), you will receive a notification in the `#support_self-managed`.

### PagerDuty Status

- **Triggered** - "A customer has requested the attention of the on-call engineer"
- **Acknowledged** - "I have seen the page and am reviewing the ticket"
- **Resolved** - "I've engaged with the customer by sending a reply to the emergency ticket"

**Note:** "Resolved" in PagerDuty does not mean the underlying issue has been resolved.

## Key Responsibilities for Customer Emergency On-Call

When serving as the Customer Emergency On-Call (CEOC) engineer, follow these key principles to ensure clear ownership and accountability:

1. **Take Assignment**: Immediately assign yourself to any emergency ticket you acknowledge and begin working on. This establishes you as the Directly Responsible Individual (DRI) and ensures clear ownership throughout the emergency response process.

2. **Document Everything**: Keep thorough notes in both Slack threads and the ticket to maintain transparency, reproducibility, and enable asynchronous collaboration.

3. **Communicate Status**: Keep stakeholders informed of progress and any handoffs required at the end of your shift.

4. **Follow Through**: Remain the DRI until the emergency is resolved or properly handed off to the next CEOC.

These principles help maintain efficiency while ensuring every emergency has clear ownership and accountability. Being the DRI means you are the single person accountable for driving the emergency to resolution. While you may collaborate with others or need to hand off the ticket during shift changes, there should never be ambiguity about who is currently responsible for an emergency ticket.

### Expectations for Support Engineers in the Customer Emergencies Rotation

#### Before On-Call

- 🎫 Maintain your regular workload during the week prior.
- 📅 Toward the end of the week (Thursday-Friday), look through your queue:
  - Identify the tickets that will need to be [handed over](https://gitlab.com/gitlab-com/support/support-team-meta/-/issues/6371) (i.e. High priority tickets, high touch tickets, STAR’ed or escalated customers)
    - Leave the summary you would want to receive
    - Work with your network/peers/Support Pod to find an Assignee for each of those tickets
- During the week before you are on-call, discuss tickets that need to be handed over with your manager. Assign these tickets to them to ensure they have a DRI and chat through Next Steps as needed. (It's expected that your Manager will help with finding an Assignee to work on the ticket.)
  - 🔎 Identify tickets you can reasonably keep during on-call week
    - 📉Try to enter the on-call week with about ~20% less than the AQC baseline. (Current: 22)
NOTE: 💡Solving emergency tickets will count towards your AQC

#### During On-Call

- Be available as soon as your shift starts.
- Organize your physical surroundings to allow for customer calls at any time during your shift.
- Plan for an additional 15-30 minutes after your shift ends to allow for cross-region handovers.
- Start your day by checking for emergencies currently in progress from the previous shift. You will be expected to be the DRI for any emergency tickets (or find a replacement DRI) which have not yet been de-escalated/resolved. This ensures that all team members can leave as soon as possible after their shift ends.
- Emergencies are unpredictable, so remember that your main objective this week is to deliver results for customers who contact CEOC.
- You may sometimes be required to contact GitLab users on behalf of another GitLab team (such as the SIRT team). Please follow the [Sending Notices workflow](/handbook/support/workflows/sending_notices) to action these requests.
- 🔥 If one of your assigned tickets gets hot, you can [STAR the ticket](/handbook/support/internal-support/support-ticket-attention-requests.md), or raise attention to a Support Leader who can help.
- Help with the Global queue as you can
  - Take easy win tickets (i.e. 2FA, Low priority, free user tickets) as you are able
  - Leave internal notes with next steps on tickets if you cannot take assignment
  - Pair and participate in Support Pod sessions as you are able
- 🧠 Remember: your goal this week is to take care of customers who page CEOC

#### Week After On-Call

- Take time off as needed based on how things went that weekend or the previous week
  - If you plan to take time off, please ensure that you complete any extra steps so that your pending tickets are in good hands 🫶
- If you had to leave something for later while on-call — do it now
- Ramp up as quickly as you reasonably can to normal AQC

## Handling Self-managed Emergencies

As the CEOC you will work with the customer along with other Support Engineers to coordinate the resolution of the emergency through the following stages:

1. Stage 1: Acknowledge
1. Stage 2: Evaluate
1. Stage 3: Engage
1. Stage 4: Resolve
1. Stage 5: Close

### Stage 1: Acknowledge

1. When an emergency is triggered, you will receive an alert from PD. This could be a text, phone call, email, Slack message, or a combination of those (depending on your PagerDuty notification preferences).
1. Acknowledge the alert in PagerDuty or Slack. This means that you received the emergency page, and are starting the response process.
1. **OPTIONAL:** Create a new Issue to guide you through the emergency response process for Customer Emergency tickets. You can use either of these tools:
    1. [Emergency Runbook Issue Template](https://gitlab.com/gitlab-com/support/emergency-runbook/-/issues/new)
    1. [Fieldnote's emergency template](https://gitlab.com/gitlab-com/support/fieldnotes/-/issues/new?description_template=Emergency%20-%20Self-Managed)
1. Open the Zendesk ticket. Assign yourself as the ticket owner to establish yourself as the Directly Responsible Individual (DRI), which prevents confusion about emergency response, ensures consistent customer communication, and creates accountability for follow-through until resolution or proper handoff.
    1. Most PagerDuty notification formats provide a direct link to the ticket.
    1. Alternatively, use Zendesk search with the term `priority: urgent` to find the ticket.

### Stage 2: Evaluate

1. Verify that the requester has an active subscription at Premium level or
   above, and is therefore entitled to emergency support. If they are not,
   lower the priority of the ticket and inform the customer kindly that their
   subscription does not include emergency support.
1. Work with the on-call Support Manager to [determine if the situation qualifies as an emergency](#determine-if-the-situation-qualifies-as-an-emergency).
   1. Create a Public Comment in the ticket acknowledging receipt of the emergency request and communicating according to the qualification determination. Please note that the responding Support Engineer needs to add a Public Comment to ensure that the ticket SLA is "reset".
1. If the situation does not qualify as an emergency, work on [downgrading the emergency report](#handling-an-emergency-downgrade).

### Stage 3: Engage

1. Offer a [call](#taking-an-emergency-customer-call) to the customer if appropriate to the reported situation. A SaaS emergency related to a public incident published on the status page, for example, would not warrant a call.
   - Example of self-managed emergency ticket which was resolved without a call: <https://gitlab.zendesk.com/agent/tickets/148028>
1. Only Resolve the PagerDuty alert *after* you have contacted the customer. This means that you are actively handling the emergency now and will see it through.
1. Use the PagerDuty message in `#support_self-managed` or `#support_gitlab-com` to start a Slack thread. This ensures that everyone coming into the ensuing discussion can easily identify the corresponding emergency ticket.
1. Start taking notes in the Slack to help others follow along, and help you with your follow-ups after the call.
1. Try to communicate complete ideas rather than snippets of thought. Something like "that's not good" as a response to something happening within the call isn't as helpful as "gitaly timings are really high".
1. Take and share screenshots of useful info the customer is showing you. Make sure you're not sharing anything sensitive. Let the customer know you're taking screenshots: "Could you pause there? I want to screenshot this part to share with my team".
1. After 15 minutes, if the customer has not responded to our initial contact with them, send a follow up message covering the following points:
    - The bridge created to work on the emergency.
    - If the customer is not able to join immediately, we can make other arrangements.
    - After another 15 minutes without response the bridge will be closed and the ticket will be assigned a `HIGH` priority.
    - Feel free to open a new emergency request if the need arises.
1. In case another emergency comes in while you are still engaged with an ongoing emergency, follow [handling multiple simultaneous emergencies](#handling-multiple-simultaneous-emergencies).
1. If the emergency was raised due to a GitLab.com Incident, follow [customer emergencies are triggered by a GitLab incident](#customer-emergencies-are-triggered-by-a-gitlab-incident).

**NOTE:** If you need to reach the current on-call engineer and they're not accessible on Slack (e.g., it's a weekend, or the end of a shift), you can [manually trigger a PagerDuty incident](https://support.pagerduty.com/main/docs/incidents#section-manually-trigger-an-incident) to get their attention, selecting **Customer Support** as the Impacted Service and assigning it to the relevant Support Engineer.

### Stage 4: Resolve

1. Work with the customer on the call and identify the issue by:
    - Collecting logs and searching the errors.
    - Verifying configuration files.
    - Reviewing recent major changes.
    - Looking for potentially known issues affecting their environment configuration and version.
1. Help the customer handle the emergency by identifying a path forward which might look like:
    - Rolling back to their previous state by restoring a backup.
    - Rolling forward by applying patches or skipping stuck migrations.
    - Applying workarounds for known issues.
    - Fixing misconfigurations to restoring services.

### Stage 5: Close

1. After working with the customer, based on the progress you can:
    - Close the emergency if the issue is [resolved](#when-the-customer-incident-is-resolved).
    - Reconvene at a later point and ask customer to raise a [follow up emergency](#when-the-customer-incident-is-not-resolved) if the issue is not resolved and
      additional information or resources are needed.
    - [Ask help if you don't know what to do](#what-to-do-if-you-dont-know-what-to-do).
2. For some emergencies, it would be beneficial to conduct a [retrospective](/handbook/support/workflows/customer-emergency-retro) after the issue is resolved, 
   to help support engineers identify any areas that can be improved and iterate on it.

#### Determine if the situation qualifies as an emergency

According to our [definition of Severity 1](https://about.gitlab.com/support/definitions/#severity-1) an emergency exists when a "GitLab server or cluster in production is not available, or otherwise unusable". In the event that the situation does not clearly qualify under the strict definition of emergency, an exception may be granted.

We [assume positive intent](/handbook/values/#assume-positive-intent) and use our [criteria for exceptions](/handbook/support/workflows/emergency_exception_workflow#exception-criteria) in the [Emergency Exception Workflow](/handbook/support/workflows/emergency_exception_workflow) as a framework for understanding the business impact of situations customers raise. During any crisis, the customer may be stressed and have immense pressure on them. Later, after the crisis, if we've determined that the ticket didn't strictly qualify as an emergency, the CSM for the customer or a Support Manager can discuss that with the customer.

| When you decide the request... | Then apply the Zendesk macro... | and communicate to the customer... |
| ------------------------------ | ------------------------------- | ---------------------------------- |
| ...meets the [definition of Severity 1](https://about.gitlab.com/support/definitions/#severity-1), | `General::Emergency::Strict Definition` | ...your plan to work the emergency. |
| ...qualifies under one of our [exception criteria](/handbook/support/workflows/emergency_exception_workflow#exception-criteria), | `General::Emergency::Exception` | ...that the situation is being treated as an emergency as a courtesy. |
| ...needs more information to allow us to determine whether it qualifies as an emergency, | `General::Emergency::Needs more info` | ...that you [will proceed asynchronously](#communicating-that-you-need-more-info) until that determination can be made. |
| ...does not meet the criteria for an [emergency](https://about.gitlab.com/support/definitions/#severity-1) or an [exception](/handbook/support/workflows/emergency_exception_workflow#exception-criteria), | `General::Emergency::Not an Emergency` and `Downgrade emergency ticket` | ...that their situation does not qualify for emergency service. Follow the section [Handling an emergency downgrade](#handling-an-emergency-downgrade). |

#### Communicating that you need more info

When an emergency request ticket does not contain information sufficient to
allow you to determine whether the situation qualifies as an emergency or for
an exception, send the customer a message through the ticket:

1. explaining that in order to correctly categorise the situation, you would
   like to understand more about the effect it is having on their ability to
   work or to meet their business objectives (*i.e.* business impact)
1. asking for the specific additional context that you require in order to
   understand what problem they are facing and what help they need

Once you have enough information to make a determination, use one of the other macros to tag the ticket with the final qualification determination. Note that the `Needs more info` tag will intentionally remain attached.

#### Handling an emergency downgrade

##### Apply "Downgrade emergency ticket" macro

Applying the macro will lead to the following changes:

- Form will be set to Self-Managed.
- Priority will be set to High.
- Ticket stage will be set to NRT.

Adjust the form depending on the ticket type and set the priority based on our
[Definitions of support impact](https://about.gitlab.com/support/definitions/#definitions-of-support-impact).
If the customer submitted the emergency request related to an existing ticket,
close the emergency ticket when you deliver the downgrade message,
and be sure the existing ticket has the priority you selected.

##### Communicate the emergency downgrade

It's important that we deliver the downgrade message as carefully and
thoughtfully as possible. Customers who submit an emergency request are often
already in a static of panic, high stress, high pressure, or a combination of
those. If you feel comfortable in delivering the message to the customer, you
are encouraged to do so. If you prefer to have a manager's assistance, please
[contact the on-call Support Manager](#optional-contact-the-on-call-support-manager).

The important details to include in the message are:

1. How we define an [emergency situation](https://about.gitlab.com/support/definitions/#severity-1)
1. To what severity level we will be resetting their ticket, and why (see
   [Definitions of support impact](https://about.gitlab.com/support/definitions/#definitions-of-support-impact))
1. If there is an existing ticket, indicate that you will close the emergency
   ticket and continue work in the existing one
1. What kind of response they should then expect for starting work on
   the ticket
   - If the customer's situation is [not quite yet an emergency, but may quickly become one](#situations-that-might-or-might-not-be-emergencies),
     indicate that a support engineer will begin working on the ticket
     immediately as a high priority
   - Otherwise, indicate that a support engineer will respond according to
     normal, non-emergency SLA
1. In which ticket the non-emergency work will proceed

##### (Optional) Contact the on-call Support Manager

If at any point you would like advice or help finding additional support, [contact the on-call Support Manager](/handbook/support/on-call/#engaging-the-on-call-manager). The on-call manager is there to support you. They can locate additional Support Engineers if needed. This can make it easier to handle a complex emergency by having more than one person on the call, so you can share responsibilities (e.g., one person takes notes in Slack while the other communicates verbally on the call). Managers are on-call during weekends, so you can page for help at any time.

#### Handling multiple simultaneous emergencies

In rare cases, the on-call engineer may experience concurrent emergencies triggered by separate customers. If this happens to you, please remember that you are not alone; you need only take the first step in the following process to ensure proper engagement and resolution of each emergency:

1. **You**: [Contact the on-call Support Manager](/handbook/support/on-call/#paging-the-on-call-manager) to inform them of the new incoming emergency. The Support Manager is responsible for finding an engineer to own the new emergency page.
1. **Support Manager**: In Slack, ping the regional support group (*e.g.* `@support-team-americas`) and request assistance from anyone who is available to assist with the new incoming emergency case.
1. **Second Support Engineer**: Acknowledge and resolve the emergency page to indicate that you are assisting the customer with the case.

#### Customer emergencies are triggered by a GitLab incident

If a GitLab incident is the cause for customer emergencies, check in with the CMOC and the Support Manager On-Call about whether a [Support Response](/handbook/support/workflows/cmoc_workflows.md#about-coordinating-a-support-response) is relevant. A [Support Response issue](https://gitlab.com/gitlab-com/support/support-team-meta/-/blob/master/.gitlab/issue_templates/Support%20Response.md) will be created when the incident requires a non-standard workflow or communication from Support; use this issue as a guide when you work on the emergencies. You can also collaborate on the workflow and share any information you find that would help Support Engineers to handle related tickets.

#### Backup engineers on weekends in APAC

Concurrent emergencies are anticipated to become more frequent over weekends. There is active discussion with the APAC managers on
the next iteration of emergency coverage but as a stop gap solution, the APAC Support team have a backup pool of Support Engineers
that can be paged by the Manager on call to assist with simultaneous emergencies if needed.

Support Engineers participating in the backup pool are referred to as **backup engineers** and are strictly on a volunteer basis.

This pool is independent of the existing escalation policies in Pagerduty, as outlined:

```text
Pool 1: On call engineer -> Support Manager on call -> Directors
Pool 2: Backup engineers
```

Changes to the backup policy (including adding/removing members) can be made by Support Managers and Support Engineers by creating an issue within the PagerDuty project using the
[Edit an existing escalation policy](https://gitlab.com/gitlab-com/support/support-ops/other-software/pagerduty/-/blob/master/.gitlab/issue_templates/Edit%20an%20existing%20escalation%20policy.md?ref_type=heads) issue template.

*For further details, please refer to [STM#4583](https://gitlab.com/gitlab-com/support/support-team-meta/-/issues/4583).*

##### Escalate to initiate page to backup engineers

In the event that a concurrent emergency comes through while you are still working on the current emergency:

1. **You**: **Escalate** the page, instead of acknowledging/resolving it. The Support Manager is responsible for finding an engineer to own the new emergency page.
1. **Support Manager**: Assess the situation. It's possible to [initiate a page of the backup pool](/handbook/support/workflows/support_manager-on-call) to request assistance from backup engineers if the situation calls for it.
1. **Backup Support Engineer**: Acknowledge and resolve the emergency page to indicate that you are assisting the customer with the case.

### Situations that Might or Might not Be Emergencies

At times, an emergency page may come in for a situation that is not quite yet an emergency, but may quickly become one. In this situation, we want to assist the customer in preventing the situation from becoming an emergency.

If this situation arises during the week:

- Contact the on-call Support Manager to request assistance. They will work to find another Support Engineer to handle the ticket as a `high` priority that requires an immediate response.

If this situation arises during the weekend:

- Handle the page as a `high` priority ticket that requires an immediate response. Work with the customer to try to resolve or mitigate the issue before it becomes an emergency.
- If you are actively engaged with another emergency, [contact the on-call Support Manager](/handbook/support/on-call/#paging-the-on-call-manager) to request assistance. They will assist the customer or work to find another Support Engineer to handle the ticket as a `high` priority that requires an immediate response.

See more examples of [situations that might be emergencies](/handbook/support/workflows/emergency_exception_workflow#examples-of-situations-that-might-or-might-not-qualify-for-an-exception) and [situations that are not emergencies](/handbook/support/workflows/emergency_exception_workflow#situations-that-are-not-emergencies).

### Taking an emergency customer call

Taking an emergency call isn't significantly different from a normal call outside of two unique points:

- You (likely) won't have much forewarning about the subject of the call
- The desired end state is a functioning system

Try to find a colleague to join the call with you. A second person on the call can take notes, search for solutions, raise additional help in Slack, and take on the role of co-host in the event of system or network-related issues. They can also discuss and confirm ideas with you in Slack.

During the call, try to establish a rapport with the customer; empathize with their situation, and set a collaborative tone.

As early as possible, determine your options. In some cases, the best option may be rolling back a change or upgrade. The best option may also involve some loss of production data. If either of those is the case, it's okay to ask the customer if they see any other options before executing that plan.

### Post-call

Before ending an emergency customer call, let the customer know what to do if there is any follow-up, and who will be available if any follow-up is required.

For example:

> It seems like we've solved the root problem here, but if you need any help I'll be on-call for the next two hours. Feel free to **open a new emergency ticket** and I'll get back on a call with you right away. If it's after two hours, my colleague Francesca will be responding. I'll make sure that she has the background of the situation before I leave for the day.

When the call has ended:

1. Write post-call notes (using macro [`Support::Customer Calls::Call Completed - Summary`](https://gitlab.com/search?utf8=%E2%9C%93&group_id=2573624&project_id=17008590&scope=&search_code=true&snippets=false&repository_ref=master&nav_source=navbar&search=id%3A+360028010274)) relevant to the customer in a public reply on the ticket.
1. Add all relevant internal-only information as an internal note on the ticket.
1. Tag the next on-call engineer in the emergency's Slack thread.
1. Review the guidance in the general [On-call - Ending your on-call shift](/handbook/support/on-call/index#ending-your-on-call-shift) section and follow the relevant steps.

Remember that as the DRI, you maintain ownership of the ticket until one of these conditions is met:

- The emergency is resolved and the ticket is closed
- The customer confirms they no longer need emergency assistance
- You've properly handed off DRI responsibility to another engineer during your shift change
- A new emergency ticket is created for follow-up (in which case, link the tickets and ensure the new ticket has a DRI assigned)

#### When the customer incident is not resolved

Situations may arise where a customer incident has not been resolved, but they need to step away for an extended time period, such as overnight to get rest. Before ending the call in this situation, explain to the customer that they need to create a *new* emergency for follow-up. Creating a new emergency ensures that there is a DRI when the customer is available again.

For example:

> We were not able to get to a resolution today and I understand you will be away until tomorrow morning. If you come back to this and need any help, I'll be on-call for the next two hours. Feel free to **open a new emergency ticket** and I'll get back on a call with you right away. If it's after two hours, my colleague Francesca will be responding. I'll make sure that she has the background of the situation before I leave for the day.

When the call has ended:

1. Write post-call notes (using macro [`Support::Customer Calls::Call Completed - Summary`](https://gitlab.com/search?utf8=%E2%9C%93&group_id=2573624&project_id=17008590&scope=&search_code=true&snippets=false&repository_ref=master&nav_source=navbar&search=id%3A+360028010274)) relevant to the customer in a public reply on the ticket.
1. Add all relevant internal-only information as an internal note on the ticket.
1. Tag the next on-call engineer in the emergency's Slack thread.
1. Merge into non-emergency ticket to consolidate and link everything.

#### When the customer incident is resolved

As soon as the customer incident is resolved, mark the emergency ticket as solved. Consider whether an emergency summary is necessary to add in an internal comment. Any follow up work should be **in a separate ticket** – do **NOT** continue work within the emergency ticket.

- **Option 1: A related ticket already exists:**
   1. Add an internal comment linking to the (solved) emergency ticket.
   1. Add an internal comment in the emergency ticket, linking to this ticket as the follow-up ticket.
   1. Check that the priority of the follow-up ticket fits.
   1. Write post-call notes (using macro [`Support::Customer Calls::Call Completed - Summary`](https://gitlab.com/search?utf8=%E2%9C%93&group_id=2573624&project_id=17008590&scope=&search_code=true&snippets=false&repository_ref=master&nav_source=navbar&search=id%3A+360028010274)) relevant to the customer in a public reply on the follow-up ticket.
  - Be sure to let the customer know that follow up work will continue in this ticket.

- **Option 2: There is no related ticket:**
   1. Create a new ticket by following the steps provided in this doc [How can I open a new ticket on behalf of a customer?](/handbook/support/workflows/working-on-tickets/#how-can-i-open-a-new-ticket-on-behalf-of-a-customer).
   1. Let customer know in the ticket description that follow-up work will continue in this ticket.
   1. Add an internal comment linking to the (closed) emergency ticket.
   1. Add an internal comment in the emergency ticket, linking to this ticket as the follow-up ticket.
   1. Optionally, an engineer involved in the emergency can take ownership of the ticket.

Why do follow up work in another ticket?

- We are at risk of missing customer responses that may come in to the ticket after the original assignee's shift ends.
- Emergency tickets have a shorter internal NRT SLO to encourage us to respond very quickly.
- Emergency tickets count differently in our statistics.

#### Optional: create pairing issue

Another option to consider is creating a [pairing issue](https://gitlab.com/gitlab-com/support/support-pairing/-/issues/new?issue%5Btitle%5D=[Emergency%20collaboration]&issuable_template=Ticket%20Pairing%20-%20Emergencies) with the label `pairing-customer_emergency`, including the support engineer(s) who provided assistance during the emergency. If your capacity is limited, you can request any engineer who was involved in the emergency to create the pairing issue on your behalf. This way, we can ensure that the necessary collaboration efforts get tracked.

## What to do if you don't know what to do

First, remember that your primary role is incident management. You are not expected to have all the answers personally and immediately.

Your primary job is to coordinate the emergency response. That could mean:

- directing the customer to take specific actions
- finding relevant documentation or doing other research into the problem
- identifying a known bug or regression and providing a workaround
- analyzing log data

It could *equally* mean:

- [identifying other experts](/handbook/support/workflows/how-to-get-help#expand-to-support-pods-and-other-subject-matter-experts) on the Support team to help do the above
- [reaching out to development teams](/handbook/support/workflows/how-to-get-help#how-to-find-the-correct-development-section-and-group-to-reach-out-for-help) to find a subject matter expert (SME)
- suggesting that the customer reach out to additional experts on their side (for example, if the problem is slow storage, you might suggest getting someone from their storage team)

Remember to say only things that help the customer and that maintain their confidence in you as the person in charge of getting their problem resolved. When you're not sure what to do, you might also be unsure what to say. Here are some phrases that might help:

- *What have you done up until now to try to resolve this?*
- *Please give me a few minutes to check the documentation on that.*
- *I'm doing some research to find the answer to that; please give me a few minutes.*
- *I'm working on finding someone who has specific expertise in this area.*
- *I don't know the answer just yet, but I'm here for you and I will use all the resources at my disposal to get this resolved.*

If you encounter a SaaS emergency at the weekend that you are unable to progress, then consider checking if the [CMOC engineer on call](https://gitlab.pagerduty.com/escalation_policies#PNH1Z1L) is available to offer any help or guidance.

If you are still stuck *and* are having difficulty finding help, contact the [manager on-call](/handbook/support/on-call/#paging-the-on-call-manager).

### Triggering a Developer Escalation

On rare occasions, you and the manager on-call may decide it's necessary to initiate the [developer escalation process](/handbook/engineering/development/processes/infra-dev-escalation/process/#escalation-process) to get the needed developer input. Keep in mind that the developer who takes the escalation might not be familiar with the aspect of GitLab that is the focus of the emergency, and it can take them time to get up to speed.

To trigger a developer escalation, see [this process outline](/handbook/engineering/development/processes/infra-dev-escalation/process/#process-outline).

## Supporting 24/7 Coverage for Customers on the Advanced or Signature Success Tier  - Phase 1

Customer Support provides 24/7 coverage for customers subscribed to GitLab’s Advanced and Signature Success Tiers. These premium tiers, which include access to a [Customer Success Architect (CSA)](/handbook/customer-success/csm/segment/csa/), require continuous support and faster response times for Severity 2 issues (labeled as High Priority tickets in Zendesk).

| Success Tier | Coverage                                   |
| ------------ | ------------------------------------------ |
| Advanced     | - 24/7 High Priority coverage              |
| Signature    | - 24/7 High Priority coverage<br>- 2hr SLA |

### Weekend Coverage

Commencing May, 2025 `@ceoc`, managed by our existing on-call rotation schedule, will temporarily be responsible for weekend coverage for these tickets. This means we need to provide a first reply and ensure the customer doesn't get into a critical scenario during the weekend. A team of dedicated engineers hired for the permanent 24/7 roles will use this period for onboarding and training. This is Phase 1 of a 3-Phase approach detailed further in [STM#6743 24/7 Shift role and it's implementation](https://gitlab.com/gitlab-com/support/support-team-meta/-/issues/6743).

### PagerDuty Alerts

From 2025-05-01 PagerDuty Alerts for High Priority tickets received from customers with either of the two success tiers will be triggered over the weekend. The [CEOC](#key-responsibilities-for-customer-emergency-on-call) will need to action this ticket within the SLA stated above, dependent on the customer's entitlements, which will be clearly stated in Zendesk.

### Ticket Assignment and Handling

We as a company want to treat High Priority tickets, especially from customers with a Success Tier, with urgency and action.

1. When you start your shift take over any emergencies or High priority tickets from the leaving CEOC that needs attention. 
1. When you get paged on a High priority ticket work with the customer on Solving the pieces that are causing the ticket to be a high priority, by working towards reducing the ticket's priority. 
1. There is no need to Unassign tickets over the weekend. Ticket that needs ongoing attention should be handed over to the incoming CEOC by using the [PD alert](/handbook/support/on-call/#engaging-the-next-on-call-support-engineer) and tickets in safe state should stay assigned to the CEOC leaving shift. 

#### Customers with an Assigned Support Engineer (ASE)

In cases where:

- An [assigned support engineer](/handbook/support/enhanced-support-offerings/offering-assigned-support-engineer/) has opted to automatically assign their customer's tickets to themselves; and
- The customer creates a Sev 2 ticket on a weekend.

This will:

1. Generate a CEOC page for the ticket; and
1. Assign the ASE to the ticket.

CEOC will need to respond to such tickets, even though it may have been assigned to the ASE. You can view all Unsolved, High Priority tickets for Success Tier customers in the Report: *All Success Tier Customers' Unsolved Severity 2/High Tickets* on the [24-7 Success Tier Coverage](https://gitlab.zendesk.com/explore/studio#/dashboards/06E115D8E3D0A86B89012F8C2FF9C3713331EF2CA24A3B7677CB8B355D061ACE) Zendesk Explore dashboard.

Once the customer ticket has been de-ecalated and is no longer a Severity 2/High Priority issue, [reset the ticket priority](/handbook/support/workflows/setting_ticket_priority/#resetting-ticket-priority), and let the customer know we will continue working with them during standard operating hours. 

The Support Manager On-Call is always available to support you. Follow [these steps](/handbook/support/on-call/#engaging-the-on-call-manager) to engage the [Support Manager On-call](/handbook/support/workflows/support_manager-on-call) for assistance.

### Rollout and Monitoring

Estimated timeline for Phase 1: 1-2 months, depending on ticket volume and customer adoption.

**Zendesk Explore Dashboard:** [24-7 Success Tier Coverage](https://gitlab.zendesk.com/explore/studio#/dashboards/06E115D8E3D0A86B89012F8C2FF9C3713331EF2CA24A3B7677CB8B355D061ACE)

This is being closely monitored by Manager DRIs (@erikamiklos (EMEA), @ralfaro (AMER), @kslaats (APAC)) in the Zendesk Dashboard: [24-7 Success Tier Coverage](https://gitlab.zendesk.com/explore/studio#/dashboards/06E115D8E3D0A86B89012F8C2FF9C3713331EF2CA24A3B7677CB8B355D061ACE).

## License Emergencies

### During the week

For license emergencies during the week, reach out to [`#support_licensing-subscription`](https://gitlab.slack.com/archives/C018C623KBJ) and ask for an expert there to handle the case. Ping the current [Support Manager On-call](/handbook/support/workflows/support_manager-on-call) in your request so they can ensure it gets picked up. Once pinged, the Support Manager On-call is the DRI for ensuring the emergency gets handled.

In the event the customer's instance is unusable due to an expired license and you are unable to reach the L&R team or the on-call manager, [generate a trial license](/handbook/support/license-and-renewals/workflows/self-managed/license_for_weekend_emergencies/#step-2-generate-the-trial-license).

### On a weekend

#### Self-managed Subscription Emergencies

There may be times when a customer's subscription expires **over the weekend**, leaving their instance unusable until a new subscription is generated.

For non-trial subscriptions, you can remind the customer that subscriptions have [a 14-day grace period](https://about.gitlab.com/pricing/licensing-faq/#what-happens-when-my-subscription-is-about-to-expire-or-has-expired). If the grace period will still be active on the next business day, kindly let the user know that their request will be handled as a standard L&R case during normal business hours. You should close the emergency ticket and ask the customer to open a [new L&R ticket](https://support.gitlab.com/hc/en-us/requests/new?ticket_form_id=360000071293) in case one doesn't exist yet.

Otherwise, follow the [Self-Managed Weekend Emergencies - License Request](/handbook/support/license-and-renewals/workflows/self-managed/license_for_weekend_emergencies/) workflow.

#### SaaS Subscription Emergencies

##### Subscription expired and downgraded to Free

A customer may be blocked because of a license expiring or neglecting to apply a renewal. If this happens over the weekend:

1. Look up the namespace details using [chatops](/handbook/support/workflows/chatops#namespace) or a GitLab.com Admin account by using the namespaces API (https://gitlab.com/api/v4/namespaces/<NAMESPACE>)
1. Check the `Trial ends on` date.
   - If it has a date, you will not need to provide a `Subscription Name` in the next step. Proceed to step 3.
   - If it is empty or null **and the namespace is on a Free plan**, guide the customer to navigate to the Settings -> Billing page and click on `Start a Free Ultimate trial`.
1. In the ticket, apply the `Trial Subscription - Exclusions Sign Off` macro and send the generated message to the customer. Do not proceed further until the customer has provided a **written** response confirming they understand the trial subscription exclusions.
1. Access the `CustomersDot Support Admin Tools` use the `Trial changes (SaaS)` option to resolve the situation.
    - Search for the namespace ID.
    - Select the pencil icon to edit the trial.
    - Select the Plan the customer had initially purchased, or use `Ultimate` if you do not have this information.
    - Set the end date to 10 days later.
    - Add the relevant Zendesk ticket link to `Zendesk ticket link` field
    - Click `Save`.
1. When the customer confirms, close the emergency ticket.
1. Alert [`#support_licensing-subscription`](https://gitlab.slack.com/archives/C018C623KBJ) by linking to the ticket for follow-up.

##### Multi-year subscriptions

- **Note:** Refer to [Handling multi-year subscriptions](/handbook/support/license-and-renewals/workflows/self-managed/handling_multi-years_subscription/) for Self Managed licensing.

Some legacy-type subscriptions are called "multi-year" but are actually multiple, separate subscriptions sold up front to cover a multi-year period.  When a customer has a deal like this, each anniversary of the renewal requires that the next subscription be associated, or else the customer's namespace can fall back to `Free`. If this occurs, send the customer the following steps.

1. Ask the customer to login to the [Customers Portal](https://docs.gitlab.com/subscriptions/customers_portal/) located at https://customers.gitlab.com/customers/sign_in for subscription management.
1. Follow these [steps to ensure their GitLab.com account is linked](https://docs.gitlab.com/subscriptions/customers_portal/#change-the-linked-account).
1. Follow these [steps to update the linked namespace](https://docs.gitlab.com/subscriptions/gitlab_com/#change-the-linked-namespace).

If the customer's CustomersDot account is not linked to their GitLab.com account (`uid` and `Gitlab user` in the CustomersDot account is empty) and you need to act on their behalf, you can try [Force Association of the subscription](/handbook/support/license-and-renewals/workflows/customersdot/support_tools#force-associate) as a workaround.

If neither of the above resolves the issue for the customer, [contact the on-call Support Manager](#optional-contact-the-on-call-support-manager) requesting further guidance.

## SaaS Emergencies

The workflow for these calls is the same as with self-managed emergencies: success means that the customer is unblocked. In some cases,
you may even be able to fully resolve a customer's problem.

For any customer facing a SaaS Emergency you are empowered to perform any [two-way door](/handbook/values/#make-two-way-door-decisions) action required to unblock them without seeking approval first.

Some examples:

- manually setting a subscription level
- adding additional storage
- adding extra compute minutes
- toggling a feature flag

During a SaaS Emergency, you have additional visibility into problems that a customer may be facing.

Review:

- [Using Kibana](/handbook/support/workflows/kibana) - explore GitLab.com log files to find the errors customers are encountering.
- [Using Sentry](/handbook/support/workflows/sentry) - get access to the full stacktrace of errors a customer might encounter.

We're expecting, broadly that emergencies will fall into one of five categories:

- **broken functionality due to a regression being pushed to GitLab.com**
  - Success may mean: reproducing, identifying or creating a bug report and escalating to have a patch created and deployed.
- **broken functionality due to an inconsistency in data unique to the customer**, for example: a group name used to be able to have special characters in it, and now something broke because our group name has a special character in it.
  - Success may mean reproducing the error, identifying it Sentry/Kibana, escalating to have the specific data corrected (and creating a bug report so our code is better)
- **GitLab.com access or "performance" degradation to the level of unusability**, for example: no access in a geographical area, CI jobs aren't being dispatched. This is the hardest class, but will generally be operational emergencies.
  - Success here means making sure it's not actually one of the top two before [declaring an incident](/handbook/engineering/infrastructure/incident-management/#report-an-incident-via-slack) and letting the SRE team diagnose and correct the root cause.

- **License / Consumption issues are preventing access to the product**
  - Success here means getting the customer into a state where they're unblocked and making sure the license team is equipped to take the handover.
- **a widespread incident causes multiple, successive PagerDuty alerts**
  - Success here means tagging and bulk responding to the issues pointing to the [GitLab.com Status Page](https://status.gitlab.com) and production issue.

### Broken Functionality

If a customer is reporting that behaviour has recently changed, first check [GitLab.com Status](https://status.gitlab.com) and `#incidents` for any on-going incidents. If there's no known incident:

1. Initiate a call with the customer. You're specifically looking to:
   - observe broken behavior.
   - determine if there's a known issue, bug report, or other customers reporting similar behavior.
   - ascertain whether or not a feature flag that may have been recently turned on (see: [Enabling Feature Flags on GitLab.com](https://docs.gitlab.com/development/feature_flags/controls/#enabling-a-feature-for-gitlabcom))
   - find/build reproduction steps devoid of customer data to build a bug report if none exists.

#### Broken functionality due to a regression or feature flag

1. Create a `~"type::bug"` issue and have the customer review it.
1. Escalate the `~"type::bug"` issue
   - If it's a new bug, or a bug with [S1/S2 severity](/handbook/engineering/infrastructure/engineering-productivity/issue-triage/#severity) escalate using the [InfraDev Escalation Process](/handbook/engineering/development/processes/infra-dev-escalation/). In most cases we will generate a roll-back patch and apply it to GitLab.com.
   - If it's a feature flag, work with the who turned it on to [disable it through ChatOps](https://docs.gitlab.com/development/feature_flags/controls/#disabling-feature-flags). In some cases, you may need to use the [InfraDev Escalation Process](/handbook/engineering/development/processes/infra-dev-escalation/) to raise a developer.
1. If this is affecting multiple customers, [declare an incident](/handbook/engineering/infrastructure/incident-management/#report-an-incident-via-slack) to engage the incident response team who will update the status page.
1. Once the original functionality is restored, update the customer.

#### Broken functionality due to something specific to the customer

1. [Page the Support Manager on-call](/handbook/support/on-call/#engaging-the-on-call-manager) to review the best way to unblock the customer. It may be that you will need someone with .com console access to fully investigate / resolve.

#### Broken functionality due to an incident

If there is a known incident, it's acceptable to link to the public status page and related incident issue. Consider using [`Support::SaaS::Gitlab.com::Incident First Response`](https://gitlab.com/gitlab-com/support/zendesk-global/macros/-/blob/master/active/Support/SaaS/GitLab.com/Incident%20First%20Response.md?ref_type=heads).

#### Example tickets

- [Feature flag broke previously working behaviour](https://gitlab.zendesk.com/agent/tickets/204073): resolution was to turn off a feature-flag.
- [Regression on GitLab.com broke previously working pipeline](https://gitlab.zendesk.com/agent/tickets/147266): resolution was to revert a recently deployed MR.
- [Customer locked themselves out of their group by changing SAML settings](https://gitlab.zendesk.com/agent/tickets/146611)

### Consumption Issues

#### Quota of compute minutes is blocking a production deployment

A customer may be blocked because they have run out of compute minutes.

1. Advise them to purchase additional compute minutes or set up individual runners.
1. At your discretion, as a courtesy, [set an additional 1000 compute minutes on their namespace through ChatOps](/handbook/support/workflows/chatops#setting-minutes-quota-for-a-namespace)

#### Customer has exceeded their storage quota

A customer may be blocked because they've exceeded their storage quota.

1. Advise them to purchase additional storage
1. In cases where a customer is unable to complete a purchase because of a defect or outage, as a courtesy, someone with GitLab.com admin can override the storage limit on a group.

### A widespread incident causes multiple, successive PagerDuty alerts

If an incident occurs on GitLab.com and hasn't been posted on the status page, SaaS customers may raise emergencies in bulk.
Success in such a situation is two-fold:

1. Route customers reporting the incident to our status page, `@gitlabstatus` on Twitter and the production incident issue.
1. Sort through the alerts to ensure that there are no emergencies raised that are unrelated to the on-going incident.

If this occurs:

1. Don't panic! Slack and PD alerts may come quickly and frequently. Consider silencing both temporarily and focus on ZD.
1. Verify that an [incident has been declared](/handbook/support/workflows/cmoc_workflows/#how-incidents-are-declared) and that the incident is actively being worked.
1. If there is no update on the status page yet, advocate for urgency with the [CMOC](/handbook/support/workflows/cmoc_workflows/#how-incidents-are-declared).
1. Choose a unique tag that will help you identify tickets, using the incident number would be typical. For example: `incident-12345`
1. Create a bulk response that points to the incident on the status page, `@gitlabstatus` on Twitter and the production issue. If any of these aren't available yet, you can send a response without to keep customers informed. You can include them in a future update.
   - Share the response that you draft or otherwise coordinate with `#support_gitlab-com` and others fielding first responses. There are likely non-emergency tickets being raised about the incident. Using the same response increases the efficiency with which we can all respond to customer inquiries about the problem.
1. Create the tag by typing it into the tag field of at least **one** ticket and submitting it - if you don't, it won't show as available in the bulk edit view of Zendesk.
1. Use Zendesk search to identify customer-raised emergencies:
   - [`priority:urgent order_by:created_at sort:desc`](https://gitlab.zendesk.com/agent/search/1?type=ticket&q=priority%3Aurgent%20order_by%3Acreated_at%20sort%3Adesc) will show all emergency tickets, sorted by those opened most recently
   - [`priority:urgent order_by:created_at sort:desc status:new`](https://gitlab.zendesk.com/agent/search/1?type=ticket&q=priority%3Aurgent%20order_by%3Acreated_at%20sort%3Adesc%20status%3Anew) will show all **new** emergencies
   - **CAREFUL**: Verify that each ticket is related to the incident - if it is not, follow [handling multiple simultaneous emergencies](#handling-multiple-simultaneous-emergencies)
1. Use [Zendesk Bulk Update](#using-zendesk-bulk-update) to respond to all open tickets.

At any point, you may ack/resolve PD alerts. It may be faster to do so through the PagerDuty web interface.

During an incident:

- *If there is no production issue to link to yet*: let customers know we are actively working to address the problem and that we will follow-up with a link to a tracking issue as soon as one is created. Set the ticket to **Open**. Once the issue is available, send a follow-up note letting the customer know that they should follow along with the issue and that we are marking the ticket as **Solved**. Include a note that they should reply if they still have trouble once the production issue has been closed / the incident has been declared resolved.
- *If there is a production issue to link to*: let customers know we are actively working to address the problem, that they should follow along at the issue, that we are marking the ticket as **Solved** and they should reply if they still have trouble once the production issue has been closed / the incident has been declared resolved.

#### Using Zendesk Bulk Update

[Zendesk Bulk Update](https://support.zendesk.com/hc/en-us/articles/4408886890906-Managing-tickets-in-bulk#topic_oth_lkp_gk) is a way to mass edit and respond to tickets. During an incident, you can use it to:

- automatically tag tickets
- send a bulk response
- set status *en masse*

You can bulk edit tickets by:

1. From a Zendesk search click one or more checkboxes
1. Click "Edit `n` tickets" in the upper right-hand corner
1. Edit the properties of the ticket you'd like to update. During an incident that will probably be:

- A public reply
- A ticket tag

1. Click Submit with the appropriate status change

![ZD Bulk Update View](/images/support/zd-bulk-update.png)

## US Government On-call

US Government on-call support is provided 7 days a week between the hours of 0500 and 1700 Pacific Time for [severity one](https://about.gitlab.com/support/definitions/#severity-1) issues that arise with premium and ultimate customers who have purchased 12x5 US Gov support. Customers who have opted for the 24x7 ultimate for high and emergency coverage can page at any time.

The current on-call schedule can be viewed in [PagerDuty](https://gitlab.pagerduty.com/schedules#P89ZYHZ)(Internal Link). The schedule is currently split into three, 8 hour shifts which roughly correlate with the dayshift, evening, and overnight team member hours:

- Dayshift: 05:00 - 13:00 PT
- Evenings: 13:00 - 21:00 PT
- Overnight: 21:00 - 05:00 PT

Customers are permitted to submit emergencies via email or via the emergency form in the US Government support portal.

### On-call Shift Coverage in US Government

In the event that a Support Engineer needs coverage for a scheduled On-call shift, open an issue in Support Team Meta using the `us-gov-oncall-coverage` template.

Dayshift engineers needing coverage on a **non-holiday weekday** may give the shift to the Support Bot.  To do so, open an issue in Support Team Meta using the `us-gov-oncall-coverage` template and mention your manager for review. After ensuring that the shift(s) in question do not fall on a weekend or holiday remove the override for your shift in PagerDuty and ensure it falls back to the bot user.

### Emergencies outside on-call hours

If a non-24x7 eligible customer submits an emergency case outside the [working hours of Government Support](https://about.gitlab.com/support/us-government-support/#hours-of-operation) the following will occur:

- A slack notification will trigger in the #spt_us-government channel alerting the team to an off hours emergency and indicating follow-up is needed at the start of business hours
- The `Off hours emergency request` trigger will inform the ticket submitter that it is after hours and give them the option to either create an emergency case in Global support or wait for US Government support to follow-up at the next start of business hours.

#### Responding to after hours emergencies

Team members who are working after the 12x5 hours may opt to provide support for customers who are having a production incident at the engineer's own discretion. When addressing these it is important to ensure the following is clear with the customer:

- They are not entitled to 24x7 support based on their subscription
- Emergency support is being provided as a one off exception based on the engineer's availability and future after hours support is not guaranteed

The responding engineer should also add their manager as a follower and indicate in an internal note that after hours support is being provided. This will help ensure the appropriate follow-up occurs with the customer's account team.

### US Gov Emergencies in Global

US Government customers with 12x5 support packages are permitted to use the global support portal for after hours emergencies if their organization's policies permit interacting and sharing information with non-US citizens. The US Gov support team **cannot confirm or deny** whether a specific case belongs to a user or organization entitled to US Government support. There is no requirement or restriction on who can reply to emergencies filed in the global support portal. If a user asks for a US citizen please remind them they are using the global support portal where US citizenship is not guaranteed and let them know if that is a requirement they should use the US Government Support portal for future communication instead.

## GitLab Dedicated Emergencies

Emergencies from [GitLab Dedicated](https://docs.gitlab.com/subscriptions/gitlab_dedicated/) come through the Customer Emergency On Call rotation. The [GitLab Dedicated Handbook](/handbook/support/workflows/dedicated) has information about [working with logs](/handbook/support/workflows/dedicated_logs) and viewing [observability dashboards](/handbook/support/workflows/dedicated_instance_health/).

Consider using the `@spt_focus-dedicated` Slack handle to ping members of the GitLab Support team who focus on GitLab Dedicated for additional assistance.

As appropriate, you can use the section on [escalating emergency issues](/handbook/support/workflows/dedicated#raise-a-dedicated-incident) to engage the Engineer on Call for GitLab Dedicated.

## Special handling notes

There are a few cases that require special handling. If an emergency page falls in one of these categories please follow these special handling instructions. If you think an emergency is special and not called out below, connect with the Support Manager On-call for help as how best to approach it.

### Compromised instances

In the event that an emergency is raised about a compromised instance a call can quickly move well beyond the scope of support.

Use the Zendesk macro `Incident::Compromised Instance` which expands on the approach below.

The customer should:

1. Shut the instance down immediately.
1. Create a new instance at the exact same version and restore their most recent backup into it.
   - Avoid exposing the new instance to the Internet
   - If they do not have a copy of their `gitlab-secrets.json`, or if the only backups available are stored in `/var/opt/gitlab/backups`, mount the volume of the compromised instance to retrieve it.
1. Rotate secrets on the new instance:
   - All secrets contained within the `gitlab.rb` (such as LDAP/email passwords)
   - All secrets in CI jobs such as API keys or remote server credentials
   - GitLab Runner registration tokens and Runner environment variables
1. If the exploit used to compromise this instance is known, then upgrade **the new instance** to a version that contains a fix for it or apply any known patches/workarounds.
   - In the case that public access is required by the organization, remove network access restrictions once the new instance is appropriately secured.
1. Retain the compromised instance for forensics and additional data recovery.

Do not offer or join a call without engaging the Support Manager on-call to align and set expectations with the customer through the ticket.

### Single user, same day purchases

There have been a few documented cases of folks purchasing a single user GitLab license specifically to raise an emergency. If you
encounter such a case, engage the Support manager on-call before offering a call.

## Customer Emergency On-Call Training Resources

### Customer Emergency Shadow PagerDuty Schedule

The [Customer Emergency Shadow Schedule](https://gitlab.pagerduty.com/schedules#PLNQAAB) can be used by anyone who wishes to shadow customer emergencies to learn before being Customer Emergency On-Call. To add yourself to the shadow rotation, speak to your manager. To modify your rotation schedule, speak to your manager. To shadow for a short span of days, you can click *Schedule an Override*, then click *Custom duration* and then select the time zone and the start and end dates and times before clicking the *Create Override* button to save the changes. To remove overrides, click the **x** on the override to be removed in the list of **Upcoming Overrides** on the right side of the screen.
