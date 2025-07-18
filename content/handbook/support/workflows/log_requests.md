---
title: Log and audit requests
description: "Overview of aggregated information which GitLab Support may provide to customers, from the gitlab.com logs. Details beyond a summary require a Security request."
category: GitLab.com
subcategory: Security
---

## Log requests for GitLab.com

Users often ask for access to GitLab.com logs, typically, due to [IP blocks](/handbook/support/workflows/ip-blocks), a possible security issue, or for internal auditing purposes.

Always include a link to the log as an internal note, with additional information if needed.

A standard response is available in ZenDesk as a macro [`Support::SaaS::Gitlab.com::Audit logs access request`](https://gitlab.com/gitlab-com/support/zendesk-global/macros/-/blob/master/active/Support/SaaS/GitLab.com/Audit%20logs%20access%20request.md?ref_type=heads).

If required, you can escalate the ticket/issue by following our [escalation process](/handbook/support/internal-support/support-ticket-attention-requests).

You can consider using the [kibana workflow](/handbook/support/workflows/kibana/) page for tips on retrieving logs for requests within the last 7 days. Log requests beyond a summary (similar to the examples below) or where logs are not readily available on Kibana should be handled according to the process outlined in the handbook page dedicated to [providing assistance to GitLab.com customers during customer-based security incidents](/handbook/security/customer-requests/). GitLab's Security Incident Response Team handles complex, extensive requests according to an internal [runbook](https://internal.gitlab.com/handbook/security/cross_functional_runbooks/customer_security_incidents/) for customer response operations.

### Who can make a request

#### Paid Subscriptions

Requester must be a Group Owner of a pre-existing paid namespace.

- Must [verify](/handbook/support/workflows/account_verification/) that this is who is making the request and should be in alignment with support for [Enterprise Users](/handbook/support/workflows/gitlab-com_overview#enterprise-users)

> NOTE: A user cannot upgrade to a paid subscription to gain access to logging requests.

#### Free Users

Free users should reference [GitLab.com rate limits documentation](https://docs.gitlab.com/user/gitlab_com/#rate-limits-on-gitlabcom). Support will provide information [when GitLab initiates contact due to an incident](https://about.gitlab.com/support/statement-of-support/#free-users).

### What we can provide

We can provide the following information:

- Information found in the [Audit Events Features](https://docs.gitlab.com/administration/audit_event_reports/)
- Information about who has accessed the account/projects that the customers owns.  This can include:
  - number of users
  - number of times accessed
  - number of unique IPs
  - range of timestamp of occurrence
  - project path
- Provide the above excluding a known list. For example, number of IP addresses not originating from a user's "work office".

### What we cannot provide

We cannot provide the following information:

- Information about accounts or projects that the requester does not own.
- Any information considered [Personal Data](/handbook/support/workflows/personal_data_access_account_deletion/) that is not specifically about the individual requester. 
- Any information that would disclose GitLab confidential information or processes.

### Sending logs and other Personal Data

Any [Personal Data](/handbook/support/workflows/personal_data_access_account_deletion/) information that is pulled by the Security Incident Response Team (SIRT),
such as a log request, needs to be delivered compressed and password protected to the requestor with the following guidelines:

- The password should be a random string of at least 10+ characters including numbers, lower and upper case letters.
- The password protected file should be attached to the ZenDesk ticket, and the password needs to be sent separately through your email account directly to the customer's email address.
  - Use the command `zip -er [TicketNumber].zip filename` or other encryption tool to encrypt the file.
  - Use 1Password to generate the random secure password for the encryption.
- Once the customer had successfully received and opened the files you should delete the pulled data from your computer and the email from your mailbox.

If the log files are too large to attach to the ticket in ZenDesk, refer to the [Provide large files to GitLab support](https://about.gitlab.com/support/providing-large-files/) page.

In case you need to share the data pull results internally, such as in an internal issue, upload the files to Google Drive, such as the [Support Ticket Attachments folder](https://drive.google.com/drive/folders/1RpCb_li2RTYsE8GnVFExCux3QpZ2i0TD) (internal).

### Examples

The following are examples to provide a better idea of what responses we can provide.

#### Example 1: Who accessed a specific repo

A customer, who had accidentally set their project to the incorrect visibility setting, wanted to know if anyone outside the company accessed their project. Here is a modified excerpt of the response:

> Excluding users who have the company email domain, 2 users viewed the main project page a total of 4 times between 20:06 and 20:10 UTC 2019-08-15. However, I can confirm that all 4 instances originated from one of the IP addresses you provided as being from your office.

From ticket: [129594](https://gitlab.zendesk.com/agent/tickets/129594)

#### Example 2: IP block

User writes in to say their entire team is getting blocked and they want to know the source. When the user writing in has access to the projects in question, we can provide the specific path(s).

> It appears that the majority of requests that returned `401`, which likely caused the temporary block, involved `/project/path`.

Example ticket: [132652](https://gitlab.zendesk.com/agent/tickets/132652)

Also see ["Identifying the Cause of IP Blocks on GitLab.com"](/handbook/support/workflows/ip-blocks).

#### Example 3: GitLab requests action due to high load

GitLab reached out to the owners of a project that was causing concern for the production team, who asked Support to reach out. The user wanted to know where the requests were originating from.

> There are 3 different IPs showing in our logs, 2 of which are based in CountryA and 1 in CountryB (please note these locations may not be accurate as they are based purely on geolocation web searches). They also all have the same user agent.

Example ticket: [130153](https://gitlab.zendesk.com/agent/tickets/130153)
