---

copyright:
 years: 2017
lastupdated: "2017-5-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Managing releases
{: #releases_overview}

A release is a container for deployment plans and events.

{:shortdesc}

Releases can be scaled for any software development lifecycle. You can add multiple deployment plans and multiple teams to a release.

Typically, the deployment plans that belong to a release are related in some business-meaningful way. For example, the plans might represent the phases in a software development lifecycle, such as development, QA, and production.

If you add events to a release, you can use the Calendar to find events and filter the Releases page.

## Creating releases
{: #releases_create}

To create a release, complete the following steps:

1. On the Releases page, click **Create release event**. If this is the first time that you are creating a release, click **Define a release to coordinate work**.

1. In the Create Release Event window, in the **Name** field, enter a name for the release.

3. In the **Team** list, select a team to manage the release. All the teams that you belong to are available.

3. In the **Start Time** field, select a starting date and time. Starting times are required for all releases.

3. In the **End Time** field, select an ending date and time.

3. In the **Tags** list, select an event. You can select multiple events. To create a tag, type the tag name in list field. Tags that you create with the Create Release Event window are not displayed on the calendar, which can help prevent calendar clutter. If you want your tag to appear on the calendar, [select a tag that is created on the Configure Calendar page](UCCR_events.html#events_tagCreate).

5. Click **Save**.

The release is displayed in the Activities list. After the release is created, you can add deployment plans to it.

## Adding deployment plans to a release
{: #releases_planAdd}

You can add existing deployment plans to a release or create new ones.

To add existing deployment plans to a release, complete the following steps:

1. On the Releases page, select the release.

1. On the Release Detail page, click **Add Deployment Plan**.

1. In the Add Plan window, select the plans that you want to add to the release. Scheduled plans that belong to your teams are listed.

3. Click **Save**.

[To create a plan](UCCR_deployPlan.html#plan_create), click **Create Deployment Plan**. Plans created from the Release detail page are automatically assigned to the release. When you create a deployment plan independent of a release, you can select the release that you want to add the plan to.

## Managing releases
{: #releases_manage}

You manage a release with the Release Detail page. To manage a release, open the Release Detail page and then complete one of the following tasks:
<ul>
<li>To modify the release, click **Edit**.
</li>
<li>To edit a deployment plan, select **Edit this plan**. The Edit Deployment Plan window is displayed.
</li>
<li>To modify a deployment plan's schedule, select **Reschedule this plan**.
</li>
<li>To copy a deployment plan, select **Copy this plan**. A copy of the selected plan is added to the release.</li>
<li>To remove the deployment plan from the release, select **Remove from release**. Removed plans are not deleted.
</li>
</li>
<li>To remove a deployment plan and save it in the archive, select **Archive this plan**. Archived items can be restored.
</li>
</ul>
