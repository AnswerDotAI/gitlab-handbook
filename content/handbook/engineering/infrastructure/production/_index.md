---
title: "Production"
controlled_document: true
---

{{% alert color="warning" %}}
If you're a GitLab team member and are looking to alert Reliability Engineering about an availability issue with GitLab.com, please find quick instructions to report an incident here: [Reporting an Incident](/handbook/engineering/infrastructure/incident-management/#reporting-an-incident).
{{% /alert %}}

{{% alert color="warning" %}}
If you're a GitLab team member looking for help with a security problem, please see the [Engaging the Security On-Call](/handbook/security/security-operations/sirt/engaging-security-on-call/) section.
{{% /alert %}}

## The Production Environment

The GitLab.com production environment is comprised of services that operate–or support the operation of–gitlab.com.
For a complete list of production services see the [service catalog](https://gitlab.com/gitlab-com/runbooks/-/blob/master/services/service-catalog.yml)

## How to Get Help

See [how to get assistance](/handbook/engineering/infrastructure/team/).

## Why `infrastructure` and `production` queues?

### Premise

Long term, additional teams will perform work on the production environment:

- Release Engineering performs deployments on production
- Security performs scans against the production
- Google may perform work on the underlying production infrastructure

We cannot keep track of **events** in production across a growing number of *functional* queues.

Furthermore, said teams will start to have on-call rotations for both their function (e.g., security) and their services.  For people on-call, having a centralized tracking point to keep track of said events is more effective than perusing various queues. Timely information (in terms of when an event is happening and how long it takes for an on-call person to understand what's happening) about the production environment is critical. The `production` queue centralizes production event information.

### Implementation

Functional queues track team workloads (`infrastructure`, `security`, etc) and are the source of the work that has to get done. Some of this work clearly impacts production (build and deploy new storage nodes); some of it will not (develop a tool to do x, y, z) until it is deployed to production.

The `production` queue tracks events in production, namely:

- [changes](/handbook/engineering/infrastructure-platforms/change-management/)
- [incidents](/handbook/engineering/infrastructure/incident-management/)
- deltas (exceptions) -- still need to do handbook write up

Over time, we will implement hooks into our automation to *automagically* inject change audit data into the `production` queue.

This also leads to a single source of data. Today, for instance, incident reports for the week get transcribed to both the On-call Handoff and Infra Call documents (we also show exceptions in the latter). These meetings serve different purposes but have overlapping data. The input for this data should be queries against the `production` queue versus the manual build in documents.

Additionally, we need to keep track of error budgets, which should also be derived from the `production` queue.

We will also be collapsing the `database` queue into the `infrastructure` queue. The database is a special piece of the infrastructure for sure, but so are the storage nodes, for example.

For the on-call SRE, every event that pages (where an event may be a group of related pages) *should* have an issue created for it in the `production` queue.  Per the severity definitions, if there is at least *visible* impact (functional inconvenience to users), then it is by definition an incident, and the Incident template should be used for the issue.  This is likely to be the majority of pager events; exceptions are typically obvious, i.e. they impact only us and customers won't even be aware, or they're alerts that are pre-incident level which by acting on we avoid incidents.

### Security Related Changes

All direct or indirect changes to authentication and authorization mechanisms used by GitLab Inc. by customers or employees require additional review and approval by a member of at least one of following teams:

- [production team](/handbook/engineering/infrastructure/production/) member
- [security team](https://about.gitlab.com/security/)  member
- developer from a different team that is staff level or higher

This process is enforced for the following repositories where the approval is mandatory using
[MR approvals](https://docs.gitlab.com/ee/user/project/merge_requests/approvals/):

- [gitlab-oauth2-proxy](https://gitlab.com/gitlab-cookbooks/gitlab-oauth2-proxy)
- [gitlab_users](https://gitlab.com/gitlab-cookbooks/gitlab_users)

Additional repositories may also require this approval and can be evaluated on a
case-by-case basis.

When should we loop the security team in on changes? If we are making major changes to any of the following areas:

1. Processing credentials/tokens
1. Storing credentials/tokens
1. Logic for privilege escalation
1. Authorization logic
1. User/account access controls
1. Authentication mechanisms
1. Abuse-related activities

#### Type Labels

Type labels are very important. They define what kind of issue this is. Every issue should have one or more.

|       Label        | Description                                                                                                             |
|--------------------|-------------------------------------------------------------------------------------------------------------------------|
|      `~Change`     | Represents a Change on infrastructure please check details on : [Change](/handbook/engineering/infrastructure-platforms/change-management/)                             |
|     `~Incident`    | Represents a Incident on infrastructure please check details on : [Incident](/handbook/engineering/infrastructure/incident-management/)                           |
|     `~Database`    | Label for problems related to database                                                                                  |
|     `~Security`    | Label for problems related to security                                                                                  |

#### Services

The services list is mentioned here : https://gitlab.com/gitlab-com/runbooks/blob/master/services/service-catalog.yml

### Always Help Others

We should never stop helping and unblocking team members. To this end, data should always be gathered to assist in highlighting areas for automation and the creation of self-service processes. Creating an issue from the request with the proper labels is the first step. The default should be that the person requesting help makes the issue; but we can help with that step too if needed.

If this issue is urgent for whatever reason, we should label them following the instructions above and add them to the ongoing Milestone.

## On-Call Support

For details about managing schedules, workflows, and documentation, see the [on-call documentation](/handbook/engineering/on-call/).

### On-Call escalation

Given the number of systems and service that we use, it's very hard if not impossible to reach an expert level in all of them. What makes it even harder is the rate of changes made to our infrastructure. For this reason, the person on-call is not expected to know everything about all of our systems. In addition, incidents are often complex and vague in their nature requiring different perspectives and ideas for solutions.

Reaching out for help is considered good practice and should not be mistaken for incompetence. Asking for help while following the escalation guidelines and checklists can expose information and result in faster resolution of problems. It also improves the knowledge of the team as a whole when for example an undocumented problem is covered in runbooks after an incident or when questions are asked in Slack channels where others can read it. This is true for on-call emergencies as well as project work. You will not be judged on the questions you ask, regardless of how elemental they might be.

The SRE team's primary responsibility is availability of gitlab.com. For this reason, helping the person on-call should take priority over project work. It doesn't mean that for every single incident, the entire SRE team should drop everything and get involved. However, it does mean that as knowledge and experience in a field that is relevant to a problem, they should feel entitled to prioritize that over project work. Previous experiences have shown that as the incident's severity increased or potential causes were ruled out, more and more people from across the company were getting involved.

## Production Events Logging

All configuration, deploys and feature flag events are recorded in Elastic Search using the events index.
To access events and for more information about how they are logged see the [events runbook](https://gitlab.com/gitlab-com/runbooks/-/blob/master/docs/events/README.md).

These events include deploys, feature-flags, configuration (Chef, Terraform), and all Kubernetes changes.
Events are recorded separately for the staging and production environment.

### Incident Subtype - Abuse

For some incidents, we may figure out that the usage patterns that led to the issues were abuse.  There is a process for how we define and handle abuse.

1. The definition of abuse can be found on the [security abuse operations section of the handbook](/handbook/security/)
1. In the event of an incident affecting GitLab.com availability, the SRE team may take actions immediately to keep the system available.  However, the team must also immediately involve our security abuse team.  A new [security on call rotation](/handbook/security/security-operations/sirt/engaging-security-on-call/) has been established in PagerDuty - There is a Security Responder rotation which can be alerted along with a Security Manager rotation.

## Backup and Restore

See policies for [Backup and Restore](/handbook/engineering/gitlab-com/policies/backup).

## Patching

### Policy

All servers in the production environment managed and maintained by the GitLab infrustructure team will be proactively maintained and patched with the latest security patches.

### Summary of Patching Strategy

All production servers managed by chef have a base role that configures each server to install and use [`unattended-upgrades`](https://gitlab.com/gitlab-com/gl-infra/chef-repo/blob/8c522363bde0248f6d66adae0d1b6c233d31d261/roles/gprd-base.json#L31-42) for automatically installing important security packages from the configured apt sources.
`Unattended-upgrades` check for updates everyday between 6 and 7 am UTC. The time is randomized to avoid hitting the mirrors at the same time. All output is logged
to `/var/log/unattended-upgrades/*.log`.

Unattended upgrades is configured to automatically patch all security upgrades for packages with the exception of the GitLab omnibus package.

The critical change process is described in the [emergency change process](/handbook/engineering/infrastructure-platforms/emergency-change-processes) overview.

### Patching Validation

Patch validation can be performed in 3 ways.

- Manually by cross examining the logs of the host with the vulnerability finding in [wiz.io](https://www.wiz.io/).
- Reviewing vulnerability & tracking issue raised into GitLab by [Vulnerability Management teams automation] (/handbook/security/product-security/vulnerability-management/automation/)
- Reach out to Vulnerability Management in slack `#g_vulnerability_management`

### General OS (Ubuntu or other Linux) Version updates

Infrastructure will look to begin OS upgrades for Ubuntu LTS releases 6 months after their release and attempt to maintain all GCP compute instances on an LTS within the last 5 years of release.  We leverage [Ubuntu Pro](https://ubuntu.com/pro) to gain an extension on security updates for older OS releases using their [ESM](https://ubuntu.com/security/esm) service, and [Ubuntu Livepatch](https://ubuntu.com/security/livepatch) to automatically apply Kernel security updates to running systems.

## Penetration Testing

Infrastructure will provide support to the [security team](../../security) for issues found during
penetration testing. For coordinating a pen test or to coordinate any procedures to address and remidiate
vulnerabilities, should be communicated to the infrastructure team through an issue in the [infrastructure issue tracker](https://gitlab.com/gitlab-com/infrastructure/issues/).

In the issue please provide the following:

- scope of the testing
- a suggested time frame
- the depth of testing
- which services will be tested
- the procedures being done
- any possible teams that may be affected (such as support, security, etc)

Please tag issues with the `~security` label and `/cc` infrastructure managers.
