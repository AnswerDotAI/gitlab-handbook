---
title: "Patch Releases"
---

## Patch release overview

Patch releases are performed according to the [GitLab Maintenance Policy](https://docs.gitlab.com/ee/policy/maintenance.html)
in order to backport bug fixes and security fixes to the [maintained versions](https://docs.gitlab.com/policy/maintenance/#maintained-versions).

Patches that are outside of our maintenance policy must be requested and agreed upon by the release managers and the requester (see [backporting to versions outside the maintenance policy](https://docs.gitlab.com/ee/policy/maintenance.html#backporting-to-older-releases) for details). Refer to the [list of maintained versions](https://docs.gitlab.com/policy/maintenance/#maintained-versions).

Patch releases are prepared in parallel with regular GitLab.com deployments so that continuous deployment is not blocked. In this way we can apply security fixes to GitLab.com instances before the public release.

If you're a GitLab engineer looking to:

* Include a security fix in a patch release, please follow the steps on the [security runbook for GitLab engineers](https://gitlab.com/gitlab-org/release/docs/-/blob/master/general/security/readme.md#security-guides-by-role).
* Include a bug fix in a patch release, please follow the steps on the [patch release runbook for GitLab engineers](https://gitlab.com/gitlab-org/release/docs/-/blob/master/general/patch/engineers.md). Security vulnerabilities in GitLab and its dependencies are to be addressed following the [Security Remediation SLAs](/handbook/security/product-security/vulnerability-management/sla/).

Bug fixes are worked on in the GitLab canonical repositories, while security fixes are worked on in the mirrored GitLab
security repositories to avoid revealing vulnerabilities before the release.

## Patch release types

Patch releases have multiple touchpoints between many teams to prepare, validate and publish packages containing
bug and vulnerability fixes.

At GitLab, there are two types of patch releases processes:

1. **Planned (default)**: An SLO-driven patch to publish all available bug and vulnerability fixes per
   the [GitLab maintenance policy](https://docs.gitlab.com/ee/policy/maintenance.html). Scheduled twice a month on
   the Wednesday before and after the [monthly release week](https://about.gitlab.com/releases/), planned patches comply
   with the [bug SLO](/handbook/engineering/infrastructure/engineering-productivity/issue-triage/#severity-slos) and
   the [security remediation SLAs](/handbook/security/product-security/vulnerability-management/sla/). Patches that include
   [`critical` vulnerabilities](/handbook/security/product-security/vulnerability-management/sla/) will be considered critical patches.
1. **Unplanned**: An immediate patch required outside of the planned patch release cadence to mitigate a high-severity (critical) vulnerability. These ad-hoc patches
   are the result of an incident, they require a [security RCA](/handbook/security/root-cause-analysis/) done by the team that introduced the high-severity vulnerability and forced an unplanned release. The AppSec
   team is responsible for assessing the vulnerability, working with engineering to decide on the best approach to resolve it and coordinating with release managers
   on a timeline for the release.

## Patch release process

The process for a patch release is the same for all types with one important distinction: planned patches include all bug and security fixes ready at the time
of the patch release preparation, while unplanned patches will likely only include the security fix for high-severity vulnerability.

The end-to-end patch release process consists of the following stages:

![patch release overview](/images/engineering/releases/patch-releases/patch-release-overview.jpg)

* [Diagram source - internal](https://docs.google.com/presentation/d/12JXlLnZ8lQp7ATdaSoL4x_oCUv04rmqzYp6dQb8AXHE/edit#slide=id.g2d0bc50ab08_0_5)

At any given time, GitLab Engineers prepare bug fixes and vulnerability fixes to
the respective [maintained versions](https://docs.gitlab.com/policy/maintenance/#maintained-versions):

* **Step 1a: Bug fix prepared** - Merge requests backporting a bug fix to the
[maintained version](https://docs.gitlab.com/policy/maintenance/#maintained-versions) are prepared by GitLab engineers:
  * The merge requests execute end-to-end tests via test-on-omnibus pipeline to guarantee the bug fix meets the quality standards.
  * If the test-on-omnibus pipeline fails, a review from a Software Engineer in Test is required.
  * The merge requests are merged by a GitLab maintainer in the stable branch associated to the [maintained version](https://docs.gitlab.com/policy/maintenance/#maintained-versions).
* **Step 1b: Vulnerability fix prepared** - Engineers fix vulnerabilities in the relevant [Security repository](https://gitlab.com/gitlab-org/security). A fix is considered complete only when it has a [security implementation issue](https://gitlab.com/gitlab-org/release/docs/-/blob/master/general/security/terminology.md) with the following:
  * All checkboxes checked to show all steps have been completed.
  * An AppSec and Maintainer approved MR targeting the default branch.
  * A backport MR for each intended version. In most cases this will mean 4 MRs to cover each supported version. Each MR must have passing pipelines, required approvals and be assigned to the release bot for processing.
  * The `~"security-target"` label is applied. This will automatically review the issue and link it to the security tracking issue if it is ready.

Two days before the planned due date, release managers start the patch release process, they make sure that
all prepared bug and security fixes are safely released. Deployments to GitLab.com run in parallel.

A patch release has the following phases:

* **Step 2: First steps** Release preparation begins when release managers run the `prepare` chatops command to create the new release task issue to guide the patch release. From here they follow the checklist to complete the initial set up and communication issues needed to prepare the release.
* **Step 3: Early Merge Phase** - Release Managers deploy security fixes to GitLab.com. Fixes with the `~"security-target"` label that are linked to the security tracking issue will have the MR targeting the default branch merged. This allows fixes to be deployed to GitLab.com before they are released to self-managed users.
* **Step 4: Merge backports** - The day before the release due date, backports with security fixes targeting the supported versions are merged. At this point, everything included in the patch must be deployed to GitLab.com, and backports must apply to all stable branches.
* **Step 5: Release preparation*** -  When all fixes are deployed and merge, Release managers prepare and test the packages.
  * **Step 5a: Tag** - Release managers tag new patch release packages for the [maintained versions](https://docs.gitlab.com/policy/maintenance/#maintained-versions).
  * **Step 5b: Deploy** - The patch release package is deployed and tested to the GitLab release instance.
  * **Step 5c: Release** - Release managers publish the packages associated with the patch release.
* **Step 6: Final steps** - At this point patch release packages are available to all users. Release managers wrap up the final steps of the patch release.
  * **Step 6a**: Patch release blog post is published
  * **Step 6b**: Default branches, stable branches, and tags are synced from Security to Canonical to return to our default state of working in the open.

## Patch release FAQs

### How can I backport a bug fix to the next patch release?

If you're a GitLab engineer looking to include a bug fix in a patch release, please follow the steps on the [patch release runbook for GitLab engineers](https://gitlab.com/gitlab-org/release/docs/-/blob/master/general/patch/engineers.md).

### Where can I find the next patch release information?

Patch release information, including targeted versions, scheduled date and status can be found on the internal Grafana [release dashboard](https://dashboards.gitlab.net/d/delivery-release_info/delivery3a-release-information?orgId=1)

### A security issue was assigned to me, where should I start?

See the [Security process as Engineer](https://gitlab.com/gitlab-org/release/docs/-/blob/master/general/security/engineer.md) documentation for more information.

### Why wasn't my security fix included in the Patch Release?

Security issues created on [GitLab Security](https://gitlab.com/gitlab-org/security/) need to be associated with the Security Tracking issue for them to be included on the Security
Release. Make sure to use the [security issue template](https://gitlab.com/gitlab-org/gitlab/-/blob/master/.gitlab/issue_templates/Security%20developer%20workflow.md) and follow the listed steps.

### How many backports do I need when working on a security issue?

Besides the merge request targeting `master`, backports will be needed targeting the stable branches for the respective [maintained versions](https://docs.gitlab.com/policy/maintenance/#maintained-versions).
For more information, see [security backports](https://gitlab.com/gitlab-org/release/docs/-/blob/master/general/security/engineer.md#backports).

### How can I revert a security merge request?

Once a security merge request has been merged, it's not advisable to revert it for multiple reasons:

1. Reverting requires rolling back a security fix, compromising the integrity of GitLab.com and self-managed instances
1. Reverting without making another fix into the release risks disclosing the vulnerability to the public when we make the release.
   This is unacceptable
1. Patch releases are performed in a restricted time constraint, reverting a security merge request requires another fix to be
   prepared in time to avoid impacting the patch release timeframe

If a security vulnerability introduced a non-vulnerability bug, in most cases, the appropriate path forward is to fix the issue in the canonical repository (after the patch release has been published).

If a security vulnerability introduced a high severity non-vulnerability bug, engage with AppSec and release managers to coordinate next steps.

For more information, see [How to Mitigate Bugs Introduced by Security Merge Request](https://gitlab.com/gitlab-org/release/docs/-/blob/master/general/security/bugs_introduced_by_security_merge_request.md) runbook.
