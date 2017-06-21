---

copyright:
 years: 2017
lastupdated: "2017-6-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# About releases
{: #releases_overview}

A release is a container for deployment plans, events, and tags.

{:shortdesc}

Typically, a release contains deployment plans and events that are related in some business-meaningful way. For example, the deployment plans might represent the phases in a software development lifecycle, such as development, QA, and production. An event might represent a blackout that affects the release.

If you add events to a release, you can use the calendar to filter the Releases page to display releases and deployment plans.

## Creating releases
{: #releases_create}

To create a release, complete the following steps:

1. On the Releases page, click **Create release**.

1. In the Create release window, in the **Name** field, enter a name for the release. A name is required.

3. In the **Team** list, select a team to manage the release. You can add deployment plans from other teams to the release event, not just the team owned by the team that manages the release. All the teams that you belong to are available. A team is required.

3. In the **Start Time** field, select a starting date and time. Starting times are required for all releases.

3. In the **End Time** field, select the ending date and time.

3. In the **Tags** list, select an event or tag. You can select multiple items.  If you want the event to appear on the calendar, [select an event that is created on the Configure Calendar page](UCCR_events.html#events_tagCreate).

1. Optionally, you can create a tag by typing the tag name in **Tags** field. Tags that you create with the Create release window are not displayed on the calendar, which can prevent calendar clutter.

5. Click **Save**.

To display the release in the Activities list, ensure that the date range includes dates within the release's start or end times. 

After the release is created, you can add deployment plans, events, and tags to it.

## Adding deployment plans to a release
{: #releases_planAdd}

You can add existing deployment plans to a release or create new ones.

To add existing deployment plans to a release, complete the following steps:

1. On the Releases page, select the release.

1. On the Release Detail page, click **Create deployment plan**.

1. In the Add Plan window, select the plans that you want to add to the release. Scheduled plans that belong to your teams are listed.

3. Click **Save**.

[To create a plan](UCCR_deployPlan.html#plan_create), click **Create Deployment Plan**. Plans created with the Release detail page are automatically assigned to the release. When you create a deployment plan independent of a release, you can select the release that you want to add the plan to.

## Managing releases
{: #releases_manage}

The Release Detail page displays the deployment plans that belong to the release. To manage a release or the deployment plans that belong to it, open the Release Detail page, and then complete one of the following tasks:
<ul>
<li>Click **Edit** to modify the release definition. With this option, you can add events and tags to the release event.
</li>
<li>Select **Edit this plan** to edit a deployment plan. The Edit Deployment Plan window is displayed.
</li>
<li>Select **Reschedule this plan** to change the scheduled start and end times.
</li>
<li>Select **Copy this plan** to copy a deployment plan. A copy of the selected plan is added to the release.</li>
<li>Select **Remove from release** to remove the deployment plan from the release. Plans that are removed a release are not deleted and can be added to another release.
</li>
</li>
<li>Select **Archive this plan** to move the deployment plan to the archive. Archived plans can be restored.
</li>
</ul>

To start a deployment, [see Running deployments.](UCCR_deployRun.html#deployment_run)

## Archiving and restoring releases
{: #releases_archiveRelease}

Although you cannot delete a release, you can store it in the archive. Archived releases are not displayed on the Releases page.

To archive a release, complete the following steps:

1. On the Releases page, select the **Archive** action for the release.

1. On the Archive release event window, determine which deployment plans to archive by selecting one of the following options:
<ul>
<li>Select **Archive all deployment plans** to archive the release and all deployment plans regardless of their status.</li>
<li>Select **Archive completed deployment plans only** to archive the release and only deployment plans that have the status of Complete. Deployment plans with other statuses are not archived and maintain their current status.</li>
</ul>

3. Click **Archive**.

To restore an archived release, compete these steps:

1. On the Releases page, click **Archived**.

2. In the list of archived releases, click the **Restore** action for the release.

A restored release retains all of its original deployment plans.
