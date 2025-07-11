---
title: "Organization Users"
owning-stage: "~devops::tenant scale"
group: Organizations
toc_hide: true
---

Since its inception, GitLab has followed a single-server, global-user architecture. With GitLab.com scaling concerns and diverging product feature sets between platforms, this model is no longer sufficient. These limitations have prompted an evolution to a new era of multi-cell, multi-tenant architecture. We are now faced with bridging the gap between our current and intended architecture while maintaining a predictable customer experience.

Previously the architecture assumed a single GitLab instance, with a single Users table in a single database and all traffic was routed to this one instance. While Users could be segmented through private groups and projects, Users were always considered part of a global User pool.

Our destination will have multiple GitLab instances, each with a User table, having traffic routed between them as needed. A User could be managed entirely by an Organization with the ability to prevent the User from accessing other Organizations or even deleting the User account completely. Legacy Users will remain undisturbed and will have the option of moving to the new architecture.

## User belongs to Organization

Now that a User will belong to a single Organization, the `users` table will have a `NOT NULL` `organization_id` column. This `organization_id` column will also shard the `users` table such that the User and their associated data such as `user_statistics` is also scoped to the Organization.

A User will belong to a single Organization and can only be a member of a single Organization. In the case of GitLab Team Members on GitLab.com we will enable a facility for these Users to access multiple Organizations. Eventually, it's proposed all Users will be able to interact with other Organizations, likely through an authorization mechanism like OAuth.

## Usernames

The end goal is Organization-scoped user records, where usernames only need to be unique within an Organization rather than globally. This will enable Organizations to have full control over their user namespace, allowing username reuse across different Organizations. Achieving this state will happen in iterations over time.

## Dog fooding

We will make accommodations for a User to exist within multiple Organizations on the same Cell for dog fooding purposes. The User will still only belong to a single Organization through `users.organization_id` but they will have multiple `organization_users` entries. This makes it easy for the GitLab Team to create new Isolated Organizations. However, this comes with the caveat that these types of dog food Organizations can only exist on the same cell as the Default Organization which is the Legacy Cell.

Dog fooding will have the assurance that an Organization context is provided with every request.

## Global Bot Users

Now that Users belong to an Organization, Global Bot Users such as `@support-bot` and `@GitLabDuo` will be created per Organization. Duplicating bots across Organizations will create an issue with conflicting usernames.

To solve this problem we will introduce the concept of a per organization Bot identity and add an `organization_user_details` table. Specifically we will add a `username` column which will be unique per Organization. This `organization_user_details.username` will effectively become a kind of username alias to `users.username`.

## Organization Membership

Users can become an Organization member in the following way:

- Organization Owners create an account on behalf of a user, and then share it with the user.

Organization members can get access to Groups and Projects in an Organization as:

- A Group Member: this grants access to the Group and all its Projects,
  regardless of their visibility.
- A Project Member: this grants access to the Project, and limited access to
  parent Groups, regardless of their visibility.
- A Non-Member: this grants access to public and internal Groups and Projects of
  that Organization. To access a private Group or Project in an Organization, a
  user must become a member. Internal visibility will not be available for
  Organization in Cells 1.0.

Organization members can be managed in the following ways:

- As [Enterprise Users](https://docs.gitlab.com/ee/user/enterprise_user/index.html), managed by the
  Organization. This includes control over their User account and the ability to
  block the User. In the context of Cells 1.0, Organization members will
  essentially function like Enterprise Users.
- As Non-Enterprise Users, managed by the default Organization. Non-Enterprise Users
  can be removed from an Organization, but the User keeps ownership of
  their User account. This will only be considered post Cells 1.0.

Enterprise Users are only available to Organizations with a Premium or Ultimate
subscription. Organizations on the free tier will only be able to host
Non-Enterprise Users.

## How do Users join an Organization?

Users are visible across all Organizations. This allows Users to move between
Organizations. Users can join an Organization by:

1. Being invited by an Organization Owner. Because Organizations are private on
   Cells 1.0, only the Organization Owner can add new Users to an Organization
   by iniviting them to create an account.

1. Becoming a Member of a Namespace (Group, Subgroup, or Project) contained
   within an Organization. A User can become a Member of a Namespace by:

   - Being invited by username
   - Being invited by email address
   - Requesting access. This requires visibility of the Organization and
     Namespace and must be accepted by the owner of the Namespace. Access cannot
     be requested to private Groups or Projects.

1. Becoming an Enterprise User of an Organization. Bringing Enterprise Users to
   the Organization level is planned post MVC. For the Organization MVC
   Enterprise Users will remain at the top-level Group.

The creator of an Organization automatically becomes the Organization Owner. It
is not necessary to become a User of a specific Organization to comment on or
create public issues, for example. All existing Users can create and comment on
all public issues.

## How do Users sign in to an Organization?

TBD

## When can Users see an Organization?

For Cells 1.0, an Organization can only be private. Private Organizations can
only be seen by their Organization members. They can only contain private Groups
and Projects.

For Cells 2.0, Organizations can also be public. Public Organizations can be
seen by everyone. They can contain public and private Groups and Projects.

In the future, Organizations will get an additional internal visibility setting
for Groups and Projects. This will allow us to introduce internal Organizations
that can only be seen by the Users it contains. This would mean that only Users
that are part of the Organization will see:

- The Organization front page, instead of a 404 when navigating to the
  Organization URL
- Name of the Organization
- Description of the Organization
- Organization pages, such as the Activity page, Groups, Projects, and Users
  overview. Content of these pages will be determined by each User's access to
  specific Groups and Projects. For instance, private Projects would only be
  seen by the members of this Project in the Project overview.
- Internal Groups and Projects

As an end goal, we plan to offer the following scenarios:

| Organization visibility | Group/Project visibility | Who sees the Organization? | Who sees Groups/Projects? |
| ------ | ------ | ------ | ------ |
| public | public | Everyone | Everyone |
| public | internal | Everyone | Organization members |
| public | private | Everyone | Group/Project members |
| internal | internal | Organization members | Organization members |
| internal | private | Organization members | Group/Project members |
| private | private | Organization members | Group/Project members |

## What can Users see in an Organization?

Users can see the things that they have access to in an Organization. For
instance, an Organization member would be able to access only the private Groups
and Projects that they are a member of, but could see all public Groups and
Projects. Actionable items such as issues, merge requests and the to-do list are
seen in the context of the Organization. This means that a User might see
10 merge requests they created in `Organization A`, and 7 in `Organization B`, when
in total they have created 17 merge requests across both Organizations.

## What is a Billable Member?

How Billable Members are defined differs between GitLabs two main offerings:

- Self-managed (SM): [Billable Members are Users who consume seats against the SM License](https://docs.gitlab.com/ee/subscriptions/self_managed/index.html#subscription-seats).
  Custom roles elevated above the Guest role are consuming seats.
- GitLab.com (SaaS): [Billable Members are Users who are Members of a Namespace (Group or Project) that consume a seat against the SaaS subscription for the top-level Group](https://docs.gitlab.com/ee/subscriptions/gitlab_com/index.html#how-seat-usage-is-determined).
  Currently, [Users with Minimal Access](https://docs.gitlab.com/ee/user/permissions.html#users-with-minimal-access)
  and Users without a Group count towards a licensed seat, but [that's changing](https://gitlab.com/gitlab-org/gitlab/-/issues/330663#note_1133361094).

These differences and how they are calculated and displayed often cause
confusion. For both SM and SaaS, we evaluate whether a User consumes a seat
against the same core rule set:

1. They are active users
1. They are not bot users
1. For the Ultimate tier, they are not a Guest

For (1) this is determined differently per offering, in terms of both what
classifies as active and also due to the underlying model that we refer to
(User vs Member). To help demonstrate the various associations used in GitLab relating
to Billable Members, here is a relationship diagram:

```mermaid
graph TD
    User
    GroupMember
    ProjectMember
    Member
    Group
    Project
    ProjectGroupLink
    GroupGroupLink
    Namespace

    User -.->|has many| GroupMember
    User -.->|has many| ProjectMember

    GroupMember ---|type of| Member
    GroupMember -.->|belongs to| Group

    ProjectMember ---|type of| Member
    ProjectMember -.->|belongs to| Project

    ProjectGroupLink -.->|belongs to| Project
    ProjectGroupLink -.->|belongs to| Group

    GroupGroupLink -.->|belongs to| Group

    Project -.->|belongs to| Group

    Group ---|type of| Namespace
```

GroupGroupLink is the join table between two Group records, indicating that one
Group has invited the other. ProjectGroupLink is the join table between a Group
and a Project, indicating the Group has been invited to the Project.

SaaS has some additional complexity when it comes to the relationships that
determine whether or not a User is considered a Billable Member, particularly
relating to Group/Project membership that can often lead to confusion. An
example of that are Members of a Group that have been invited into another Group
or Project and therewith become billable.

There are two charts as the flow is different for each:

- [SaaS chart](#saas-chart)
- [SM chart](#sm-chart)

(These charts are placed at the bottom of the page, due to length.)

## How can Users switch between different Organizations?

For Organizations in the context of Cells 1.0, Users will only be able to be
part of a single Organization. If a user wants to be part of multiple
Organizations, they have to join every additional Organization with a new user
account.

Later, in the context of Cells 1.5, Users can utilize a
[context switcher](https://gitlab.com/gitlab-org/gitlab/-/issues/411637). This feature
allows easy navigation and access to different Organizations' content and
settings. By clicking on the context switcher and selecting a specific
Organization from the provided list, Users can seamlessly transition their view
and permissions, enabling them to interact with the resources and
functionalities of the chosen Organization.

## What happens when a User is deleted?

We've identified three different scenarios where a User can be removed from an Organization:

1. Removal: The User is removed from the organization_users table. This is
   similar to the User leaving a company, but the User can join the Organization
   again after access approval.
1. Banning: The User is banned. This can happen in case of misconduct but the
   User cannot be added again to the Organization until they are unbanned. In
   this case, we keep the organization_users entry and change the permission to
   none.
1. Deleting: The User is deleted. We assign everything the User has authored to
   the Ghost User and delete the entry from the organization_users table.

As part of the Organization MVC, Organization Owners can remove Organization
members. This means that the User's membership entries are deleted from all
Groups and Projects that are contained within the Organization. In addition, the
User entry is removed from the `organization_users` table.

Actions such as banning and deleting a User will be added to the Organization at a later point.

## Organization Non-Users

Non-Users are external to the Organization and can only access the public
resources of an Organization, such as public Projects.

## SaaS chart

```mermaid
flowchart TD
        root[SaaS User Billable Flow]-->UserActive{`User.state` is active?}
        UserActive -.Yes.-> IsMember[Check if User is a Member <br/>of the Root Group hierarchy]
        UserActive -.No.-> NotBillable[Not Billable]

        IsMember --> DM
        Member -.Yes.->IsBot{Is User a Bot? <br/>See note 2}
        NotMember -.No.->NotBillable

        IsBot -.Yes.->NotBillable
        IsBot -.No.->Active[Active `Member` state?]

        Active --> MemberStateIsActive
        ActiveMember-.Yes.-> MinAccess{Member has <br/>Minimal Access level?}
        NotActive-.No.-> NotBillable

        MinAccess -.Yes.-> NotBillable

        MinAccess -.No.-> HighestRoleGuest?{Member Highest Role<br/> is Guest?}
        HighestRoleGuest? -.Yes.-> LicenseType{Ultimate License?}
        LicenseType -.No.-> Billable
        HighestRoleGuest? -.No.-> Billable

        LicenseType -.Yes.-> NotBillable

        subgraph in_hierarchy[User Is a Member of the Root Group hierarchy]
            DM{Direct Member of the Root Group?} -.No.->DMSub{Direct Member of a sub-group?}
            DM -.Yes.->Member[Is a Member]
            DMSub -.Yes.->Member
            DMSub -.No.->DMProject{Member of a Project in the hierarchy?}
            DMProject -.Yes.->Member
            DMProject -.No.-> InvitedMember{Member of an invited Group?}

            InvitedMember -.Yes.-> Member
            InvitedMember -.No.-> NotMember[Not a Member<br/>See note 1]
        end

        subgraph activesub[Is Member Active?]
            MemberStateIsActive{`Member.state` is active?} -.Yes.-> RequestedInvite{User Requested Access?<br/>See note 3}
            MemberStateIsActive -.No.-> NotActive

            RequestedInvite -.Yes.-> AcceptedRequest{Request was accepted?}
            AcceptedRequest -.No.-> NotActive[Not an active member]
            AcceptedRequest -.Yes.-> ActiveMember[Active Member]

            RequestedInvite -.No.-> Invited{User was Invited?<br/>See note 4}

            Invited -.No.-> NotActive
            Invited -.Yes.-> AcceptedInvite{User accepted invite?}
            AcceptedInvite -.No.->NotActive
            AcceptedInvite -.Yes.->ActiveMember
        end
```

## SM chart

```mermaid
flowchart TD
        user[Is the User Billable?]
        user -->UserState{Active `User` State?}
        UserState -.Yes.-> H{Human?}
        UserState -.No.-> NotBillable

        H -.No.-> PB{Project Bot?}
        PB -.No.-> SU{Service User?}
        SU -.No.-> NotBillable[Not Billable]


        SU -.Yes.-> InGroupOrProject
        PB -.Yes.-> InGroupOrProject
        H -.Yes.-> InGroupOrProject{Member of a Group or Project?}

        InGroupOrProject -.No.-> LicenseType
        InGroupOrProject -.Yes.-> HighestRoleGuest?{Highest Role is Guest?}


        HighestRoleGuest? -.Yes.-> LicenseType{Ultimate License?}
        LicenseType -.No.-> Billable
        HighestRoleGuest? -.No.-> Billable

        LicenseType -.Yes.-> NotBillable
```
