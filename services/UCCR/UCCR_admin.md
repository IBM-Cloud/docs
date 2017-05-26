---

copyright:
 years: 2017
lastupdated: "2017-5-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Administering
{: #admin_overview}

A release event is a container for deployment plans.

{:shortdesc}

Release events can be scaled for any software development lifecycle. You can add multiple deployment plans, and calendar events to a release event.

Typically, the deployment plans and events that belong to a release event are related in some business-meaningful way. For example, the deployment plans might represent the phases in a software development lifecycle, such as development, QA, and production.

If you add calendar events to a release, you can use the Calendar to filter the Releases page to display release events and deployment plans.

# Security
{: #admin_security}

To create a release event, complete the following steps:

1. On the Releases page, click **Create release event**. If this is your first time creating a release event, click **Define a release to coordinate work**.

1. In the Create Release Event window, in the **Name** field, enter a name for the release.

3. In the **Team** list, select a team to manage the release. You can add deployment plans oowned by other teams to the release event, not just those owned by the team selected to manage the release. All the teams that you belong to are available.

3. In the **Start Time** field, select a starting date and time. Starting times are required for all releases.

3. In the **End Time** field, select an ending date and time.

3. In the **Tags** list, select a calendar event. You can select multiple calendar events. To create a tag instead, type the tag name in list field. Tags that you create with the Create Release Event window are not displayed on the calendar, which can help prevent calendar clutter. If you want your event to appear on the calendar, [select an event that is created on the Configure Calendar page](UCCR_events.html#events_tagCreate).

5. Click **Save**.

The release event is displayed in the Activities list. After the release is created, you can add deployment plans to it.
