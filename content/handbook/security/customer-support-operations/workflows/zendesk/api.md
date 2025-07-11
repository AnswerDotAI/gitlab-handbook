---
title: API
description: Operations workflow page for Zendesk API
canonical_path: "/handbook/security/customer-support-operations/workflows/zendesk/api"
---

{{% alert title="Note" color="primary" %}}

Anything involving the Zendesk API is classified as ad-hoc.

{{% /alert %}}

{{% alert title="Note" color="danger" %}}

All Zendesk API tokens are admin level tokens. They are extremely dangerous and should only be issued when absolutely necessary.

{{% /alert %}}

## Token creation requests

{{% alert title="Note" color="primary" %}}

All token naming should be a link to the item the token was issued for.

{{% /alert %}}

All requests for an API token should be done via a [access request issue](https://gitlab.com/gitlab-com/team-member-epics/access-requests/-/issues/new?issuable_template=API_Token_Request).

There are two exceptions to this:

- API tokens for Support Operations team members' personal use
- API tokens for Support Operations scripts/automations/etc.

Once an access request is filed, the requester's manager must approve the request.

After that has been done, the provisioner for the instance (traditionally a Fullstack Engineer, Customer Support Operations) will review the request.

During this review, we carefully review the business reasons and use-case of each request due to the significant access level that an API token provides. 

If deemed acceptable, the Fullstack Engineer, Customer Support Operations will then create the API token. The name of the token in Zendesk should be a link to the access request.

The API token will then be DM'd in Slack to the requester.

See: [Zendesk API Tokens](/handbook/security/customer-support-operations/workflows/token-rotation/#for-zendesk-api-tokens)

## Integration requests

{{% alert title="Note" color="danger" %}}

These are significantly harder to revoke than API tokens. We should only ever create these via the `Integration bot` for the instance:

- [Zendesk Global](https://gitlab.zendesk.com/agent/users/370415907240)

Due to the security risk, we do not currently do integration requests for Zendesk US Government.

{{% /alert %}}

All requests for an integration token should be done via a [access request issue](https://gitlab.com/gitlab-com/team-member-epics/access-requests/-/issues/new?issuable_template=API_Token_Request).

Once an access request is filed, the requester's manager must approve the request.

After that has been done, the provisioner for the instance (traditionally a Fullstack Engineer, Customer Support Operations) will review the request.

During this review, we carefully analyze the business reasons and use-case due to the significant access level that an API token provides. Integrations pose even higher risks and should be avoided whenever possible. While API tokens can be quickly and easily revoked, integrations cannot.

If deemed acceptable, the Fullstack Engineer, Customer Support Operations will then create the integration. The exact means for this are going to vary from integration to integration, but the key point is it will be done by logging in as the `Integration bot` for the Zendesk instance.

See: [Zendesk OAuth Applications](/handbook/security/customer-support-operations/workflows/token-rotation/#integrating-a-new-oauth-application-into-zendesk)
