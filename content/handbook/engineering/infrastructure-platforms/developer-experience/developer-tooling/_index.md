---
title: "Developer Tooling team"
description: "The Developer Tooling team enables all GitLab contributors to efficiently deliver results for customers by providing stable and performant software development tools, such as the GitLab Development Kit."
---

## Mission

- Build state-of-the-art developer tools that are efficient and reliable, empowering developers to keep their development environments up-to-date painlessly.
- Enable contributors to contribute to our tools.
- Measure what matters: improvements in developer experience, efficiency, and toil reduction, using both quantitative and qualitative metrics.

## Vision

The Developer Tooling team's vision is to create tools that enable GitLab team members and the wider community to contribute to GitLab efficiently, without the friction and manual toil that often come with working on large, complex software projects like GitLab.

## Areas of responsibilities

```mermaid
flowchart LR
    DT[Developer Tooling] --focuses on--> GDK[GitLab Development Kit]
    click GDK "https://gitlab.com/gitlab-org/gitlab-development-kit"
    GDK --> GDKRemoteDev[GDK remote development workspace]

    DT --> CanonicalTooling[gitlab-org/gitlab tooling]

    CanonicalTooling --> StaticAnalysis[Static Analysis]

    DT --> AuxTooling[Auxiliary tooling<br><small>Useful tools for GitLab.com.</small>]
    AuxTooling --> civiz[Pipeline Visualizer]
    AuxTooling --> subparticle[Subparticle]

    click civiz "https://gitlab.com/gitlab-org/quality/engineering-productivity/pipeline-visualizer"
    click subparticle "https://gitlab.com/gitlab-org/quality/engineering-productivity/subparticle"
```

## Team structure

### Members

{{< team-by-manager-slug "mgamea" >}}

## Communication

| Description            | Link                                                                                                                                         |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| **GitLab Team Handle** | [`@gl-dx/developer-tooling`](https://gitlab.com/gl-dx/developer-tooling)                                                                     |
| **Slack Channel**      | [`#g_developer_tooling`](https://gitlab.enterprise.slack.com/archives/C07UW7F3FL2)                                                           |
| **Team Issue Board**   | [Team Issue Board](https://gitlab.com/groups/gitlab-org/-/boards/8974136?label_name%5B%5D=group%3A%3Adeveloper+tooling&iteration_id=Current) |
| **Issue Tracker**      | [`gitlab-org/dx/tooling/team`](https://gitlab.com/gitlab-org/quality/tooling/team/-/issues/)                                                 |
