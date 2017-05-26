---

copyright:
 years: 2017
lastupdated: "2017-5-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Managing release events
{: #releases_overview}

A release event is a container for deployment plans, calendar events, and tags.

{:shortdesc}

Release events can be scaled for any software development lifecycle. You can add multiple deployment plans, tags, and calendar events to a release event.

Typically, the deployment plans and events that belong to a release event are related in some business-meaningful way. For example, the deployment plans might represent the phases in a software development lifecycle, such as development, QA, and production. A calendar event might represent a blackout that affects the release event.

If you add calendar events to a release, you can use the Calendar to filter the Releases page to display release events and deployment plans.

## Creating release events
{: #releases_create}

To create a release event, complete the following steps:

1. On the Releases page, click **Create release event**. If this is your first time creating a release event, click **Define a release to coordinate work**.

1. In the Create Release Event window, in the **Name** field, enter a name for the release.

3. In the **Team** list, select a team to manage the release. You can add deployment plans from other teams to the release event, not just those owned by the team that manages the release. All the teams that you belong to are available.

3. In the **Start Time** field, select a starting date and time. Starting times are required for all releases.

3. In the **End Time** field, select an ending date and time.

3. In the **Tags** list, select a calendar event or tag. You can select multiple items.  If you want your event to appear on the calendar, [select an event that is created on the Configure Calendar page](UCCR_events.html#events_tagCreate).

1. Optional. Create a tag by typing the tag name in **Tags** field. Tags that you create with the Create Release Event window are not displayed on the calendar, which can help prevent calendar clutter.

5. Click **Save**.

The release event is displayed in the Activities list. After the release is created, you can add deployment plans, calendar events, and tags to it.

## Adding deployment plans to a release events
{: #releases_planAdd}

You can add existing deployment plans to a release or create new ones.

To add existing deployment plans to a release event, complete the following steps:

1. On the Releases page, select the release event.

1. On the Release Detail page, click **Add Deployment Plan**.

1. In the Add Plan window, select the plans that you want to add to the release. Scheduled plans that belong to your teams are listed.

3. Click **Save**.

[To create a plan](UCCR_deployPlan.html#plan_create), click **Create Deployment Plan**. Plans created from the Release detail page are automatically assigned to the release. When you create a deployment plan independent of a release, you can select the release that you want to add the plan to.

## Managing release events
{: #releases_manage}

The Release Detail page displays the deployment plans that belong to the release event. To manage a release event or the deployment plans that belong to it, open the Release Detail page and then complete one of the following tasks:
<ul>
<li>Click **Edit** to modify the release event definition. With this option, you can add calendar events and tags to the release event.
</li>
<li>Select **Edit this plan** to edit a deployment plan. The Edit Deployment Plan window is displayed.
</li>
<li>Select **Reschedule this plan** to change a deployment plan's scheduled start and end times.
</li>
<li>Select **Copy this plan** to copy a deployment plan. A copy of the selected plan is added to the release.</li>
<li>Select **Remove from release** to remove the deployment plan from the release. Removed plans are not deleted and can be added to another release.
</li>
</li>
<li>Select **Archive this plan** to move the deployment plan to the archive. Archived items can be restored.
</li>
</ul>

To start a deployment, [see Running deployments.](UCCR_deployRun.html#deployment_run)

## Archiving and restoring release events
{: #releases_archiveRelease}

Although you cannot delete a release event, you can archive it. Archived release events are not displayed on the Releases page.

To archive a release event, complete the following steps:

1. On the Releases page, select the **Archive** action for the release event.

1. On the Archive release event window, determine which deployment plans to archive by selecting one of the following options:
<ul>
<li>Select **Archive all deployment plans** to archive the release event along with all its deployment plans regardless of their status.</li>
<li>Select **Archive completed deployment plans only** to archive the release event and all deployment plans with the status of Complete. Deployment plans with statuses other than Complete are not archived and maintain their current status.</li>
</ul>

3. Click **Archive**.

To restore an archived release event, compete these steps:

1. On the Releases page, click **Archived**.

2. Click the **Restore** action for the release event.

A restored release event retains all its original deployment plans.
