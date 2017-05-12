---

copyright:
 years: 2017
lastupdated: "2017-5-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Managing events
{: #events_overview}

An event represents a release-related activity managed with the calendar.

{:shortdesc}

There are several event types, including release events, holidays, and maintenance windows. You can also create your own event types.

[Events are assigned to releases](UCCR_releases.html#releases_overview). Once an event is assigned, it is represented on the calendar by an icon appropriate for the event type. You can use the icons to filter the Releases page and select releases for any affected date or range of dates.

## Using the calendar
{: #events_calendarManage}

The Releases page displays the releases and deployment plans created by you and your teams. From the Releases page, you can do most release-related activities, such as creating releases and deployment plans.

By default, the Releases page displays releases and deployments scheduled for the next seven days. You can filter the display by time and status. For example, you might restrict the display to releases that are scheduled for tomorrow. You can also use the calendar to filter the display by selecting a specific date or range of dates. The currently selected date range is displayed on the action bar.

To filter items by date, complete one of the following tasks:
<ul>
<li>Select a value from the **Dates** list on the action bar. For example, to display items scheduled for the upcoming week, select **Next 7 days**.</li>
<li>On the calendar, select a date or a range of dates. You can select a range of dates by clicking a date and then shift-clicking another date. When you select dates on the calendar, the **Dates** value on the action bar is set to **Custom**.</li>
</ul>

Releases and plans that are or were scheduled for the selected dates are displayed.

To filter items by status, complete one of the following tasks:
<ul>
<li>To display all releases and plans, select **All**. You can use this option to display unscheduled deployments.
</li>
<li>To display deployment plans that do not have a status of Complete or Failed, select **Draft**.
</li>
<li>To display releases and plans that are scheduled for the selected date range, select **Scheduled**.
</li>
<li>To display deployments that are currently in progress, select **In Progress**.
</li>
<li>To display deployments that failed, select **Failed**.</li>
<li>To display finished deployments, select **Complete**.
</li>
</li>
<li>To display releases and deployment plans saved to the archive, select **Archive**. Archived items can be restored.
</li>
<li>To display deployment plans that are saved as templates, select **Templates**. You can use templates to create plans. You can revert templates to deployment plans.  
</li>
</ul>

## Creating event tags
{: #events_tagCreate}

Events are represented by tags that you can apply to releases. Events assigned to a release are represented by icons on the calendar. You can select an event icons on the calendar to filter the displayed releases.

There are three event categories: releases, milestones, and holidays. The categories are suggestions. You can order events in any manner you like.

When you create an event tag, graphical styles are automatically applied to the associated icon. Icons are displayed on the calendar where you can select them to filter the items displayed on the releases page. You can change the icon style after you create a event.

To create an event, complete the following tasks:

1. On the Releases page, click **Calendar settings** <img class="inline" src="images/cal-set.png"  alt="Calendar settings">.

1. In the Configure calendar page, click **Add event type** <img class="inline" src="images/event-add.png"  alt="Add event type"> for the event type that you want to create.

3. In the text field, enter a name for the event.

3. Click **Save**.

You can edit and delete event tags.

## Managing event tags
{: #events_tagEdit}

By default, event icon styles are applied according to the event's category. Styles are applied automatically and randomly according to category.

In the following illustration, the styles on the top two rows are applied to events in the release events category; styles in the third row are applied to maintenance and blackout events; styles in the fourth row are applied to holidays.

![](images/event-styles.png "Typical deployment plan")

Figure 1. Event icon styles

To edit an event's style, complete the following steps:

1. On the Releases page, click **Calendar settings**.

2. On the Configure calendar page, click the Edit icon next to the event icon that you want to change, then click **More**.

3. Select a style. You can select any style regardless of category.

To edit an event name, click the Edit icon next to the event name that you want to change, and then edit the name.

To delete an event, click the Delete icon next to the event name.

## Importing events
{: #events_importing}

You can import your own events. Events are defined in a CSV-type file. To import events, complete these steps:

1. On the Releases page, click **Import** <img class="inline" src="images/import-events.png"  alt="Import events">.

2. On the Import from CSV dialog, select the CSV file that contains your events, and then click **Import Events**. The dialog provides a link to download a sample CSV event file.

If the import is successful, the events are displayed in the Calendar configuration page.

The CSV event file has the following format:

`name,description,start,end,team`

Each event must be on a separate row.
