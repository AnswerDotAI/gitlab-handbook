---
title: Help Center categories
description: Operations workflow page for Zendesk Help Center categories
canonical_path: "/handbook/security/customer-support-operations/workflows/zendesk/help-center-categories"
---

{{% alert title="Note" color="primary" %}}

All Help Center category changes are handled via a standard deployment.

{{% /alert %}}

## Creating a Help Center category

For these, you will need to create a corresponding Help Center category file in the sync repo.

You should also do this in a way that creates a MR. Said MR should always be peer reviewed before merging (the MR should enforce this).

The exact nature of what you need to put into the YAML file will vary based on the issue's request.

Be sure to read [Working with sync repo files](../../docs/sync-repo-files) for more information.

## Editing a Help Center category

For these, you will need to locate the corresponding Help Center category file in the sync repo and make changes to it.

You should also do this in a way that creates a MR. Said MR should always be peer reviewed before merging (the MR should enforce this).

The exact nature of what you need to put into the YAML file will vary based on the issue's request.

Be sure to read [Working with sync repo files](../../docs/sync-repo-files) for more information.

## Exception deployment

To perform an exception deployment for Help Center categories, navigate to the Help Center category project in question, go to the scheduled pipelines page, and click the play button. This will trigger a sync job for the Help Center categories.

## Repo links

- [Zendesk Global sync repo](https://gitlab.com/gitlab-support-readiness/zendesk-global/help-center-categories)
- [Zendesk US Government sync repo](https://gitlab.com/gitlab-support-readiness/zendesk-us-government/help-center-categories)
