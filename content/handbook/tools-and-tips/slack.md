---
title: "Slack"
description: "Slack usage and tips at GitLab"
---

## In general

*Slack is an important part of GitLab's strategy for communication between team members. As such, extra care needs to be given to ensure the safety and integrity of data.*

## Profile

Fill in your Slack profile, as we use Slack profiles as our Team Directory to stay in touch with other team members. Important fields include:

- Photo (unobscured photo of your face rather than an artificial avatar, for better human connection and easier recognition)
- Title (should be your GitLab job title, including your department and team name)
- GitLab.com profile (set the Display text to your @gitlabusername so that people don't need to click the link to identify your username)
- Time zone (useful for other GitLab team members to see when you're available)
- Working hours (can help others to identify the times you are generally available)
- GitLab Birthdays (opt in or out of the birthday celebrations in Slack by selecting yes or no)
- Location field for City / State / Province and Country (optional)
- You can add your personal phone number including country code (optional)
- Consider changing your "Display Name" if you prefer to be addressed by a nickname
- Consider adding your pronouns in the Pronouns field. By making it normal to set pronouns we create a more inclusive environment for people who use non-traditional pronouns.
- Consider adding a pronunciation guide in the "Name Pronunication" field to help others to pronounce your name correctly (e.g. sid see-brandy for Sid Sijbrandij).
- Consider adding a "Name recording" to help with name pronunciation.
- Do not enter anything in the G-Cal Booking! field unless you would like to set up and make use of a [Calendly Account](/handbook/tools-and-tips/other-apps/#calendly)

## Channels

Channels are a core feature of Slack. This section describes tools and tips for managing Slack channels. For a list of common GitLab Slack channels, please see the [GitLab Communication Chat](/handbook/communication/chat).

### Browse Channels

You can browse all available GitLab channels by clicking on "Channels" on the left pane in the Slack app.
From there, you can see every channel, who created it, and how many members there are.
Feel free to ask for recommendations from other team members for their favorite channels.
Every team member is automatically added to the `#company-fyi` and `#whats-happening-at-gitlab` channels, where announcements are made and information for the entire company is shared.
There are also a few default channels that every new hire is added to, such as: `#celebrations`, `#new_team_members`, `#questions`, `#random`, & `#thanks`; these channels are optional, but we think they are a great place for team members to interact and get to know each other.

### Organize Channels in Sidebar Sections

Slack now supports [organizing channels in sections](https://slack.com/intl/en-de/help/articles/360043207674-Organize-conversations-with-custom-sections). Previously this only was possible through "Starred" channels. Navigate into the Slack **preferences** and select the `Sidebar` navigation item. Click on `Create Section` to create a new section on the left sidebar. You can also do that from the settings menu of each existing section.

Feel free to organize this with your most frequent used channels, or specific team grouping. You can drag and drop and also hide sections. You can for example create the `info` section and add `#company-fyi` and `#whats-happening-at-gitlab` as channels. Additionally, add the `team` section and move all related channels there.

Consider using Slack's <b>[Starred channel](https://slack.com/help/articles/201331016-Star-channels-and-direct-messages)</b> function to spotlight three categories of channels, its <b>[Mute function](https://slack.com/help/articles/204411433-Mute-channels-and-direct-messages)</b> to quiet channels which are pulling your focus away too often, and most importantly, its **Mark all messages as read** function (easily toggled by pressing `Shift` and `Esc` simultaneously while on a desktop) to achieve an instantly clear slate.

An example of three spotlight channels approach is below. Slack allows you to organize your sidebar of starred channels with <b>[custom sections](https://slack.com/help/articles/360043207674-Organize-your-sidebar-with-custom-sections)</b> to visibly raise or lower their priority level, giving you control over what you see first.

1. Channels important to my job (e.g. a team member in Corporate Marketing may star `#marketing`, `#corp-mktg`, `#newswire`, `#external-comms`, `#website`, `#handbook`)
1. Channels important to GitLab (e.g. `#company-fyi`, `#whats-happening-at-gitlab`, `#team-member-updates`, `#e-group`, `#ceo`, `#new-vacancies`)
1. Channels important to my interests (e.g. `#travel`, `#remote`, `#daily-gratitude`, `#mental_health_aware`, `#intheparenthood`, `#women`, `#diversity_inclusion_and_belonging`)

### Sort channels and direct messages with stars

To sort direct messages and channels, open the direct message or channel and click on the star icon.
For details, see [Star channel or direct message](https://slack.com/intl/en-gb/help/articles/201331016-Star-channels-and-direct-messages#star-a-channel-or-dm).

### Channels Access

In addition to GitLab team-members, designated groups such as the [Core Team](https://about.gitlab.com/community/core-team/) members and advisors outside of GitLab may be granted access to our Slack channels.
However, internal channels that start with `#a_` will be restricted to GitLab team-members who have been invited to those channels only.
Any confidential conversations regarding our customers should be restricted only to `#a_` channels.
The rationale for internal channels is that it could be a breach of many of our contracts for third parties to have knowledge of GitLab customers.
This is especially the case when third parties could be customers' competitors.

### Invite

There are [multiple ways](https://slack.com/intl/en-gb/help/articles/201980108-Add-people-to-a-channel) to invite people into a Slack channel.
The easiest way is to use the invite command by typing `/invite @jenny`.
Avoid inviting people through a mention message.
E.g. `@jenny` as it can create a message that distracts others.

### Change Group DMs to Private Channels

If you are in a group direct message with multiple people, you can [change it to a private channel](https://slack.com/intl/en-gb/help/articles/217555437-Convert-a-group-direct-message-to-a-private-channel), in order to avoid extra pings and allow additional team members to be added or removed to the channel.  

In Slack Enterprise Grid, if you start a group DM and then it is converted to a channel, the channel ends up in "all workspaces". "All workspace" channels have [no retention limit](https://gitlab.com/gitlab-com/it/security/issue-tracker/-/issues/66), which contradicts our policy of [90 day retention](/handbook/communication/#slack). To remediate this, we have a script that will daily move the channels into our main GitLab workspace. If you are in an affected channel, you will receive a message from Slackbot that states:

`"Slack Owner has removed #<channel> from all other "GitLab" workspaces using the channel management tool. Only people from "GitLab" can access the channel now. Learn more."`

Do not convert group DMs to private channels within the "GitLab - Finance" workspace or any secondary workspace as they will be converted and end up in our main "GitLab" workspace. Instead, start a new private channel and add the participants to it.

### Change private channels to public channels

Only Slack administrators can change a private channel to a public channel.

To request that an existing private channel be made public, submit an [access request](/handbook/security/corporate/end-user-services/onboarding-access-requests/access-requests/).

## Managing noise and creating focus in Slack

Slack can be a disorderly place in its default state. Consider implementing the below to add structure and focus, but remember that there will likely be more useful information shared on Slack than you are able to ingest and process on a daily basis, regardless of your approach.

While an intentional effort to organize is important, remember that [it's impossible to know everything](/handbook/values/#its-impossible-to-know-everything). As a team, we may spot information that is missed by others, and we should surface that information when pertinent as we strive to [see others succeed](/handbook/values/#see-others-succeed). For managing Slack channels, consider blocking a set period of time to review certain channels that makes the most sense for you (i.e. multiple times a day, daily, weekly).

Below are helpful links to best practices and tips on managing your notifications and reducing noise in Slack. We encourage you to regularly check your notification settings to ensure you get more notifications of what *is* important/relevant to you, and less of what *isn't*.

- [Reduce noise in Slack](https://slack.com/intl/en-gb/help/articles/218551977-Reduce-noise-in-Slack)
- [Configure Your Notifications](https://slack.com/intl/en-gb/help/articles/201355156-Guide-to-desktop-notifications#configure-your-notifications)
- [Guide to Desktop Notifications](https://slack.com/intl/en-gb/help/articles/201355156-Guide-to-desktop-notifications#channel-specific-and-group-dm-notifications)
- [Channel-specific and group DM Notifications](https://slack.com/intl/en-gb/help/articles/201355156-Guide-to-desktop-notifications#channel-specific-and-group-dm-notifications)
- [Display only unread conversations](https://slack.com/help/articles/360043207674-Organize-your-sidebar-with-custom-sections-Organize-your-sidebar-with-custom-sections-Organize-your-sidebar-with-custom-sections#manage-conversation-display)
- [GitLab team member Brendan O'leary on how he uses Slack](https://blog.boleary.dev/how-i-slack/)

### Display only unread conversations

With lots of channels and direct messages, Slack can become overwhelming. To help
keep track of activity on Slack, and to simplify the interface, consider
[displaying only unread conversations](https://slack.com/intl/en-au/help/articles/360043207674-Organise-your-sidebar-with-customised-sections-Organise-your-sidebar-with-customised-sections-Organise-your-sidebar-with-customised-sections#manage-conversation-display).

### Slack Reminders

Slack reminders help you to remember things without having to keep it all in your head.
You can set reminders for yourself or other team members.
You will receive a notification at the specified time.

You can use natural language with the `/remind` command.
Type `/remind help` to get some tips.
For full information on Slack reminders [see the Slack help](https://slack.com/intl/en-gb/help/articles/208423427-Set-a-reminder).

### Set aside time to work through notifications

Building dedicated time into your day can help minimize the distractions that Slack can create. Consider using a 15 or 30 minute block in your morning or afternoon to enjoy a cup of coffee and catch up on messages you might have missed. When the time you set comes to an end, close out of the Slack app and move on to your next project. Having a set end time can help you feel more in control, and serves as a reminder that [it's impossible to know everything](/handbook/values/#its-impossible-to-know-everything)

### Scheduled Slack Messages

When working in an all-remote environment it can be sometimes difficult to draw the line between home and work, and it can be especially tempting to check Slack messages after hours. To foster a more inclusive environment at GitLab, we can avoid sending messages outside of the recipient's working hours by composing a message but not sending it until the recipient begins their working day. In Slack, you can schedule messages to be sent later, which helps reduce immediate disruptions. You can still edit, delete, or cancel scheduled messages before they are sent, making it a very family-friendly tool to use. This approach aligns with our [bias towards asynchronous communication](/handbook/values/#bias-towards-asynchronous-communication).

It's simple: when composing a message, click the arrow icon (next to the paper plane icon) to schedule it for a later time.

For more details on scheduling messages in Slack, please refer to [Slack help](https://slack.com/help/articles/201457107-Send-and-read-messages#:~:text=hide%20formatting%20tools-,Send%20or%20schedule%20messages,-You%20can%20send).

### Minimize Visual Distractions

Animated images and emoji can add meaning to conversation, but they can also be distracting.
If you would prefer to have static images and emoji, disable the animation.
For details, see [Manage animated images and emoji](https://slack.com/intl/en-gb/help/articles/228023907-Manage-animated-images-and-emoji).

## Slack Status

Slack allows you to set your [status](https://slack.com/blog/productivity/set-your-status-in-slack) for your fellow GitLab team members by using your choice of standard messages such as "Away" and "Lunch" or a custom message and your choice of emoji.

If you're off work for a holiday or vacation you can update your status by using [Time Off by Deel](/handbook/people-group/paid-time-off/#communicating-your-time-off).
This is a great way to let your team know whether you are available.

To have your Slack status automatically set to "In a meeting" based on your Google Calendar, add the [Google Calendar app](https://gitlab.slack.com/apps/ADZ494LHY-google-calendar?next_id=0) to your Slack account.

### Do Not Disturb Hours

Slack now supports "Do Not Disturb Hours" so you won't be pinged in the middle of the night or while you are dealing with family matters.
You can set your "Do Not Disturb Hours" by clicking on the bell at the top of the left pane in the Slack app.
You also have the option of snoozing for 20 minutes or up to 24 hours.
Note: Do Not Disturb can be overridden in the event of an emergency.
See Slack documentation for more information.

## Quick Switcher

Quick Switcher is a great feature to know about if you want to get productive with Slack.
As the name suggests, it allows you to switch between channels and direct messages quickly.
Invoke it with<kbd>Cmd</kbd>+<kbd>k</kbd>on Mac or<kbd>Ctrl</kbd>+<kbd>k</kbd>on Windows or Linux and start typing the name of the person to chat with or the channel you are interested in.
You can then navigate the suggestions with<kbd>↑</kbd>and<kbd>↓</kbd>keys and hit<kbd>enter</kbd>to select.

## Unfurling Links in Messages

Slack has a built-in feature to [Unfurl](https://api.slack.com/docs/message-link-unfurling) links included in messages posted to Slack.
This will post a preview of the link alongside the message.
You can remove the unfurled preview of the link by hitting the "x" in the top-left of the preview.
This will then prompt you to confirm removing the attachment, which you can hit "Yes, remove".

![Unfurl attachment removal](/images/tools-and-tips/unfurl-remove.png)

In the confirmation prompt you may also see a checkbox to *"Disable future attachments from this website"*.
As a workspace admin if you select the disable option **this will denylist the link/domain across the workspace and will impact every user**.
If you do happen to denylist a link or a domain, they can be modified in the Workspace admin portal under [Settings & Permissions](https://gitlab.slack.com/admin/attachments).

If you see a team member share posts with multiple link previews that you think are distracting, in channels like `#whats-happening-at-gitlab`, consider acting in the spirit of [Everyone is a moderator](/handbook/communication/#everyone-is-a-moderator) and either:

- [Letting them know in a DM](/handbook/communication/#communicate-directly) that it's adding noise to their message.
- Reacting to their message with the `:consider-removing-link-previews-to-keep-the-channel-tidy-please:` emoji.

## Custom theme

The interface colors can be customized in Slack.
This is especially useful when using multiple slack accounts, setting up different themes makes it really easy to differentiate them instantly.
The theme selector is available under Preferences > Themes.

In order to setup a GitLab theme, send yourself the following message: `#643685,#634489,#FC6D26,#ffffff,#71558f,#ffffff,#FCA326,#e24329`, and press the `Switch sidebar theme` button.

## Slack Apps

Many applications can integrate with Slack.
Recommended apps:

1. Google Calendar - By integrating your calendar with Slack, you'll get notifications about meetings directly in Slack.
Most important - 1 minute before a meeting begins, you'll receive a message with the meeting info, including a link to join meetings that are occurring in Zoom.
You can set up the integration by typing /gcal into any message field.

### Need to add a new app to Slack

GitLab has chosen to restrict the ability to install apps, and we have a process to approve or restrict certain apps for our workspace. In order to add a new app to Slack, you need to create a [vendor approval issue](https://gitlab.com/gitlab-com/Finance-Division/procurement-team/procurement/-/issues/new?issuable_template=app_integrations). Once that's approved by all parties, please request approval to add the app to Slack:

1. Make sure the app hasn't been pre-approved by our team by clicking on Apps in the left sidebar and find Available Apps. To find pre-approved apps in the App Directory, click Pre-Approved below Categories in the left column.
1. If the app isn't pre-approved, you can click on Add to Slack.
1. Add a custom message with more context about your request and also link the vendor approval issue.
1. Click Submit. You'll receive a direct message from Slackbot when your request has been reviewed by the team.

**Please note that this is only required for new apps that have not been reviewed or approved.** If your request is to add a new process or update an existing process for how an application works in slack, please refer to our [Business Technology Change Management](https://internal.gitlab.com/handbook/IT/it-change-management/) process.

## Slackbots

We have a few slackbots to help us with frequently asked questions and other slackbots that directly help us to remain inclusive in our language and align closely with our [Diversity, Inclusion and Belonging Value](/handbook/values/#diversity-inclusion).
The following list is reflective of the ones we use for Diversity, Inclusion and Belonging and the suggested changes to use. This list is representative, not complete; terms will be added and removed as we iterate on the list.
As a GitLab Team Member, you can view the active slackbots that we use in Slack, under: GitLab > Customize Your Workspace > Slackbot.

| `hey guys, hi guys, you guys, salesman, salesmen, businessman, businessmen` | Are you including people of multiple genders? Please consider using "everyone," "team," "y'all," or similar instead. You can read [more about inclusive language in our handbook](/handbook/values/#inclusive-language--pronouns) |
| `on your toes, on anybody's toes` | It's probably okay.<br><br>As companies grow, their speed of decision making goes down since there are more people involved. We should counteract that [by having short toes](/handbook/values/#short-toes), and feel comfortable letting others contribute to our domain. |
| `aggressive` | Did you mean ambitious? |
| `gitlabber, gitlabbers` | The term `gitlabber` is a commonly misused term. Please use "GitLab team member" instead. You can [read more about this in our handbook](/handbook/communication/top-misused-terms/) |

## Security

### Sign-in requirements

Every 90 days, all users will be logged out of Slack and will need to re-authenticate on each of their devices via Okta. This is to ensure that all BYOD devices are registered with a current Okta Verify client and are visible in the Okta Administration dashboard. It will also ensure that there are no indefinite sessions on devices temporarily exempted from [Okta Verify Device Trust](/handbook/security/corporate/systems/okta/verify/).

### Profile deletion

Beginning in December 2024, and going forward in June and December of each year, CorpSec will request from Slack support to delete profiles that have been deactivated for more than five years. For former team members who have left GitLab less than 5 years ago, we will use the API to remove all fields except for Name, GitLab Email, Title and GitLab.com username, which will remain for current team members to find historical context on earlier epics, merge requests and issues.
