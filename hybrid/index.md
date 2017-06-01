---


copyright:
  years: 2015, 2017
lastupdated: "2017-05-30"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Managing {{site.data.keyword.Bluemix_notm}} Local and {{site.data.keyword.Bluemix_notm}} Dedicated
{: #mng}

If you have administrator access for {{site.data.keyword.Bluemix}} Local or {{site.data.keyword.Bluemix_notm}} Dedicated, go to the **Administration** page to manage resources, monitor quota usage, administer user permissions, schedule upgrade notifications, view security reports and logs, and more. You can manage your orgs by creating spaces and setting [user roles and permissions](/docs/admin/index.html#oc_useradmin); see [Managing your organizations](/docs/admin/orgs_spaces.html).
{:shortdesc}

{: #ld_table1}

| What can I do? | Details |    
|----------------|---------|
|Monitor system usage | Click **ADMINISTRATION &gt; USAGE**. View your system information, monitor CPU usage, and plan usage to make the best decisions for your business. See [Viewing usage information](/docs/admin/index.html#oc_resource).|
|Manage your catalog | Click **ADMINISTRATION &gt; CATALOG MANAGEMENT** to manage which services are visible to your users and orgs. See [Managing your catalog](/docs/admin/index.html#oc_catalog).|
|Administer orgs | Click **ADMINISTRATION &gt; ORGANIZATION ADMINISTRATION** to create organizations, monitor quotas for organizations, and make needs-based decisions quickly. See [Administering organizations](/docs/admin/index.html#oc_organizations).|
|Create spaces and assign user roles | Click **Account** &gt; **Manage Organizations** to create spaces within your orgs. Add users and assign org and space roles to users. See [Managing your organizations](/docs/admin/orgs_spaces.html). |
|Manage administrative user permissions | Click **ADMINISTRATION &gt; USER ADMINISTRATION** to add users, remove users, and adjust user permissions. See [Managing users and permissions](/docs/admin/index.html#oc_useradmin). |
|Review reports and logs | Click **ADMINISTRATION &gt; REPORTS AND LOGS** to view security reports and audit logs for you instance. See [Viewing reports](/docs/admin/index.html#oc_report). |
|View system information | Click **ADMINISTRATION &gt; SYSTEM INFORMATION** to view system information such as pending maintenance updates, name and version of your instance, region, API URL, CLI URL, LDAP configuration details, group and user mappings, statistics, and shared domains. See [Viewing system information](/docs/admin/index.html#oc_system). |
|Extend notifications and set up notification subscriptions | Click **ADMINISTRATION &gt; SYSTEM INFORMATION &gt; *Number* pending**. You can use webhooks to integrate with a web service of your choice to set up an event notification subscription for an update or incident. See [Notifications and notification subscriptions](/docs/admin/index.html#oc_eventsubscription). |
{: caption="Table 1. Administrative tasks for managing your {{site.data.keyword.Bluemix_notm}} local or dedicated instance" caption-side="top"}

<!-- staging only for WoW start -->

**Tip**: The Infrastructure dashboard in the {{site.data.keyword.Bluemix_notm}} console is available only in linked accounts in {{site.data.keyword.Bluemix_notm}} Public environments.


<!-- staging only for WoW end -->


## Notifications and notification subscriptions
{: #oc_eventsubscription}

You can always know the status of your environment by checking the Status page. As they occur, incidents and scheduled disruptive maintenance update events are reported on the Status page. {{site.data.keyword.Bluemix_notm}} also sends notifications to the Notifications area on the Administration page for events such as scheduled or pending maintenance updates.

### Notifications

You can view notifications for your local or dedicated environment to monitor the status of your environment. Review the following table for information about the different types of notifications and where each notification type is posted.

{: #ld_table2}

| **Event Type** | **Notification method** |       
|-----------------|-------------------|
| Maintenance updates | To see a full list and history of your pending and complete notifications, click **ADMINISTRATION &gt; SYSTEM INFORMATION** &gt; *Number* **pending**. You are also alerted about scheduled disruptive maintenance update events on the Status page. Click **Support** &gt; **Status**. You can extend the notification capability by setting up a subscription that sends an email to recipients of your choice. Or you can set up a subscription that uses webhooks to integrate the notifications from the Administration page with a web service of your choice.|
| Critical incidents | You are alerted about critical incidents on the Status page. Click **Support** &gt; **Status**. You can extend the notification capability by setting up a notification subscription that sends an email to a recipient of your choice. Or you can set up a subscription that uses webhooks to integrate the notifications from the Administration page with a web service of your choice.  |  
| Threshold events | You can set up a notification subscription that sends an email to a recipient of your choice when thresholds for organization quota, physical disk, physical memory, reserved disk, or reserved memory are reached in your environment. Or, you can set up a subscription that uses webhooks to integrate the notifications with a web service of your choice.  |  
| {{site.data.keyword.Bluemix_notm}} Status | You can always view the latest status for the platform, services, and your {{site.data.keyword.Bluemix_notm}} instance on the Status page. Click **Support** &gt; **Status**.  |
{: caption="Table 2. Event types and notifications methods" caption-side="top"}

### Setting up notification subscriptions
{: #seteventsub}

You can extend the functionality of the notifications that are sent to the Administration page and the Status page by using notification subscriptions. Use notification subscriptions to set up a custom email or use webhooks to integrate with a tool of your choice.
 * If you select the email option, your notifications are sent to the email addresses that you specify. You can select notifications of incidents, maintenance updates, or thresholds. An initial email notification is sent. Then, if the event has a change made to it, another notification with the change is sent each time a change is made.  
 * If you select the webhooks option, your notifications are routed directly to a destination of your choice, such as a phone number (by SMS message). You can customize the type of notification, specifically maintenance updates, critical incident alerts, or thresholds. You can customize whether to receive new notifications or notifications about changes to subscriptions, and what information is included in the body of each notification.

**Note**: Only users with the Superuser permission (`ops.admin`) can set up notification subscriptions.

To create an email or webhook subscription from the **Notification Subscriptions** page, complete the following steps:

1. Navigate to the **Notification Subscriptions** page.  Go to **SYSTEM INFORMATION &gt; Environment &gt; Subscriptions**.
2. Click **Add Subscription**.
3. Complete the notification subscription form.

  * To create email notification subscriptions about maintenance updates or incidents, see the information in [Table 3](index.html#emailnotmaintinc).
  * To create email notification subscriptions about thresholds, see the information in [Table 4](index.html#emailnottrhesh).
  * To create webhook notification subscriptions about maintenance updates or incidents, see the information in [Table 5](index.html#webhooknotsub).
  * To create webhook notification subscriptions about thresholds, see the information in [Table 6](index.html#webhooknotthresh).

4. After you complete the form, you can choose from the following options:

  * Click **Save** to save the subscription to your notification subscription list.
  * Click **Save and Test** to save and test the notification.
  * Click **Save and Close** to save the subscription to your notification subscription list, and return to the previous page.

{: #emailnotmaintinc}

| **Field** | **Description** |
|-----------------|-------------------|
| Enabled | Select the option to enable the email notifications. Clear the selection to disable the email notification. Subscriptions are enabled by default. |
| Type | Select **Email**. |
| Event | Select to be subscribed to notifications for a **Maintenance** or **Incident** event. |
| Combine notifications | Select the option to combine the incident notifications for all regions into a single notification. This option is available for incidents only. |
| Subject | Enter the subject line for the email. This is a required field.  |
| Body | Enter the message body text to be sent in the email. You can use the IBM payload values to populate the email notification with pertinent information. See the [Maintenance and incident payload section values](index.html#payload) table to identify which values you can use. Use basic HTML tags to structure your email. This is a required field. |
| To | Enter the email address or addresses using a comma-separated list for the recipients of the email notification. Expand the "cc" or "bcc" options to copy others on the email. This is a required field. |
| Description | Add a unique description for the subscription that you are creating. |
{: caption="Table 3. Fields for email notification subscriptions about thresholds" caption-side="top"}


{: #emailnottrhesh}

| **Field** | **Description** |
|-----------------|-------------------|
| Enabled | Select the option to enable the email notifications. Clear the selection to disable the email notification. Subscriptions are enabled by default. |
| Type | Select **Email**. |
| Event | Select **Threshold**. |
| Threshold | Select the type of threshold you want to be notified about: Organization Quota, Physical Disk, Physical Memory, Reserved Disk, or Reserved Memory. |
| Threshold Direction | Select the direction that you want the data to be moving in, either Ascending or Descending, when it passes the Notify When Crossing value that you set. For example, if the Notify When Crossing value is 50%, and the direction is descending, you are notified only if the usage percentage goes from 50% or more to less than 50%.  If you set the direction to ascending, you would be notified when the usage percentage goes from less than 50% to more than 50%.   |
| Notify When Crossing Above (%) | Enter the threshold percentage at which you want to be notified. If you chose the Ascending property in the Threshold Direction field, the email notification is sent when the threshold rises above this percentage. |
| Notify When Crossing Below (%) | Enter the threshold percentage at which you want to be notified. If you chose the Descending property in the Threshold Direction field, the email notification is sent when the threshold drops beneath this percentage. |
| Description | Add a unique description for the subscription that you are creating. |
| Subject | Enter the subject line for the email. This is a required field.  |
| Message Body | Enter the message body text to be sent in the email. You can use the IBM payload values to populate the email notification with pertinent information. See the [Threshold payload section values](index.html#threshpayload) table to identify which values you can use. Use basic HTML tags to structure your email. This is a required field. |
| To | Enter the email address or addresses using a comma-separated list for the recipients of the email notification. Expand the "cc" or "bcc" options to copy others on the email. This is a required field. |
{: caption="Table 4. Fields for email notification subscriptions about maintenance updates or incidents" caption-side="top"}

Threshold data is collected once every 6 hours. A notification is sent only once when the value crosses the threshold value you set. If you chose ascending, a new notification is not sent unless the value drops below the threshold and then increases above the threshold again. Likewise, if you chose descending, you are notified only if the value rises above the threshold you set and then drops below the threshold again.

If you don't want to wait 6 hours for the notification to be sent when the threshold is met, after completing the fields on the form you can click **Save and Test** to receive a test notification with sample data.  

An Organization Quota threshold notification includes only the organizations that have crossed the specified threshold percentage in the 6 hour time period corresponding to that notification. Organizations that have crossed a threshold during previous 6 hour time periods will not be included, even if they remain above or below the threshold.  The three resources that make up an organization's quota (reserved memory, services, and routes) are considered independently when determining if an organization quota notification should be sent. For example, if the amount of reserved memory used by an organization crosses 50% of the organization's quota, an Organization Quota threshold configured with a value of 50% would result in a notification being sent.  If the number of services used by the same organization crosses 50% of the organization's quota at a later point in time, even though the amount of memory used remains unchanged, the same Organization Quota threshold subscription would also result in a notification being sent.

{: #webhooknotsub}

| **Field** | **Description** |
|-----------------|-------------------|
| Enabled | Select the option to enable the notification. Clear the selection to disable the notification. Subscriptions are enabled by default. |
| Type | Select **Webhook** |
| Event | Select to be subscribed to notifications for a **Maintenance** or **Incident** event. |
| Authorization | Select whether to enable authorization.  The options are: **Basic** or **None**. |
| User name | If you chose **Basic** authorization, enter your user name for your web service. If you don't want to use your personal credentials, you can set up a functional ID to use specifically with {{site.data.keyword.Bluemix_notm}}. |
| Password | If you chose **Basic** authorization, enter the password for your web service. |
| Description | Add a unique description for the subscription that you are creating. |
| New Event | Select this option to enable the notification for new maintenance or incident events. Clear the selection to disable the notification. |
| Method | Select **GET**, **POST**, or **PUT**. |
| URL | Enter the URL to connect to your web service. |
| Response property | This optional field is the property name that identifies the resource which is created by your web service when a POST or PUT request is sent. If you provide a response property for a new event and you choose to create a subscription for a change to an event, then you must also provide it for the Change to Event subscription. Depending on the web service that you are using, you could specify it as part of the URL or as a payload value.  |
| Payload | If you selected the POST or PUT method, enter the properties that are specific to the web service that you are using paired with the payload values used for the IBM notification. See the [Maintenance and incident payload section values](index.html#payload) table to identify which values you can use. If you do not enter information in this section, you receive a notification that does not have any more information. |
| Change to Event | Select this option to create notification subscriptions about changes to maintenance or incident events that you have created subscriptions for. Clear the selection to disable the notification. |
| Use values and payload from New Event | Uses the content of the Method, URL, and Payload fields from the New Event section. Note that if this option is checked, these fields are not available for further editing in the Change to Event section. |
| Method | Select **GET**, **POST**, or **PUT**. |
| URL | Enter the URL to connect to your web service. |
| Payload | If you selected the POST or PUT method, enter the properties that are specific to the web service that you are using paired with the payload values used for the IBM notification. See the [Maintenance and incident payload section values](index.html#payload) table to identify which values you can use. If you do not enter information in this section, you receive a notification that does not have any more information. |
| Combine notifications | Select the option to combine the incident notifications for all regions into a single notification. This option is available for incidents only. |
{: caption="Table 5. Form fields for a webhook notification subscription about maintenance or incidents" caption-side="top"}


{: #webhooknotthresh}

| **Field** | **Description** |
|-----------------|-------------------|
| Enabled | Select the option to enable the notification. Clear the selection to disable the notification. Subscriptions are enabled by default. |
| Type | Select **Webhook**. |
| Event | Select **Threshold**. |
| Threshold | Select the type of threshold you want to be notified about: Organization Quota, Physical Disk,  Physical Memory, Reserved Disk, or Reserved Memory.|
| Threshold Direction | Select whether you want to see the threshold data in Ascending order or Descending order.  |
| Notify When Crossing Below (%) | If you selected the **Descending** **Threshold Direction**, enter the threshold percentage at which you want to be notified. When the threshold drops beneath this percentage, the webhook notification is sent. |
| Notify When Crossing Above (%) | If you selected the **Ascending** **Threshold Direction**, enter the threshold percentage at which you want to be notified. When the threshold rises above this percentage, the webhook notification is sent. |
| Description | Add a unique description for the subscription that you are creating. |
| Authorization | Select whether to enable authorization.  The options are: **Basic** or **None**. |
| User name | If you chose basic authorization, enter your user name for your web service. If you don't want to use your personal credentials, you can set up a functional ID to use specifically with {{site.data.keyword.Bluemix_notm}}. |
| Password | If you chose basic authorization, enter the password for your web service. |
| Method | Select **GET**, **POST**, or **PUT**. |
| URL | Enter the URL to connect to your web service. |
{: caption="Table 6. Form fields for a webhook notification subscription about thresholds" caption-side="top"}

Threshold data is collected once every 6 hours. A notification is sent only once when the value crosses the threshold value you set. A new notification is not sent unless the value drops below the threshold, if you chose ascending, and then increases above the threshold again. Likewise, if you chose descending, you are only notified again if the value rises above the threshold you set and then drops below the threshold again.

If you don't want to wait 6 hours for the notification to be sent when the threshold is met, after you complete the fields on the form, you can click **Save and Test** to save and test the notification with sample data.

An Organization Quota threshold notification includes only the organizations that have crossed the specified threshold percentage in the 6 hour time period corresponding to that notification. Organizations that have crossed a threshold during previous 6 hour time periods will not be included, even if they remain above/below threshold.  The three resources that make up an organization's quota, reserved memory, services, and routes, are considered independently when determining if an organization quota notification should be sent. For example, if the amount of reserved memory used by an organization crosses 50% of the organization's quota, an Organization Quota threshold configured with a value of 50% would result in a notification being sent.  If the number of services used by the same organization crosses 50% of the organization's quota at a later point in time, even though the amount of memory used remains unchanged, the same Organization Quota threshold subscription would also result in a notification being sent.

{: #payload}

| **IBM value** | **Description** | **Event type** |
|----------------|----------------|------------------------|
| {{content.category}} | Affected services | Incident |
| {{content.disruption}} | Affected components | Maintenance update |
| {{content.message}} | Message description |   Maintenance update and incident |
| {{content.scheduleWindow.start}} | Scheduled start date for the update | Maintenance update |
| {{content.scheduleWindow.end}} | Scheduled end time for the update | Maintenance Update |
| {{content.severity}} | Severity rating | Incident |
| {{content.subCategoryName}} | Affected components | Incident |
| {{content.title}} | Message title | Maintenance update and incident |
| {{region}} | Affected region | Maintenance update and incident |
| {{status}} | Status of the update | Maintenance update |
| {{type}} | Update or incident | Maintenance update and incident |
| {{workitem}} | Work item number | Maintenance update and incident |
{: caption="Table 7. Maintenance and incident payload section values" caption-side="top"}


{: #threshpayload}

| **IBM value** | **Description** | **Event type** |
|----------------|----------------|------------------------|
| {{content.org_quota}} | Organization quota threshold | Threshold |
| {{content.physical_disk}} | Physical disk threshold | Threshold |
| {{content.physical_memory}} | Physical memory threshold | Threshold |  
| {{content.reserved_disk}} | Reserved disk threshold | Threshold |
| {{content.reserved_memory}} | Reserved memory threshold | Threshold |
{: caption="Table 8. Threshold payload section values" caption-side="top"}

When your notification subscription is saved, you receive notifications through the method that you set up. Notifications still post in the following locations:  
 * On the Status page for incidents
 * On the Status page for the scheduled disruptive maintenance update events
 * In the Notifications area of the Administration page for maintenance updates

You can select any saved notification subscription, view the recent activity, or edit as you need. Click to expand any recent activity entry to view the history details.

## Maintenance updates
{: #oc_schedulemaintenance}

You can view scheduled and pending maintenance updates, if you have the superuser permission (`ops.admin`), by clicking **ADMINISTRATION &gt; SYSTEM INFORMATION &gt; *Number* pending** to access the **System Updates** page.  All users of your environment can view the scheduled disruptive maintenance update events by clicking **Support** &gt; **Status**.

**Note**: See the following section for [Setting preapproved maintenance windows](index.html#preapprovedmaintenance) to get you started. These windows must be set in order for IBM to schedule maintenance for your environment.

<dl>
<dt>Non-disruptive updates</dt>
<dd>A non-disruptive update does not affect your environment, your running applications, or your users' access to your applications. This update type does not require case-by-case approval and will be applied during the preapproved, available maintenance windows that you set from the System Updates page.</dd>
<dt>Disruptive updates</dt>
<dd>A disruptive update might affect your environment, running applications, or your users' access to your applications. You must schedule and approve each of these maintenance updates within the allotted 21-day maintenance window. You can select the suggested deployment date and time, the option for any of your preapproved windows, or you can open the calendar to select three specific dates and times for IBM to choose from when scheduling the update.</dd>
</dl>


### Setting preapproved maintenance windows
{: #preapprovedmaintenance}

Non-disruptive maintenance updates are scheduled to run during preapproved windows of time. By default, two weekly available update windows are created for your system. These windows are typically set to recur every Saturday and Sunday night. You can change the default settings in one of the following ways:
 * Edit the default update windows by choosing a different day or a different start time, or both
 * Create an update window and then delete the default update window

To save your changes, you must still meet the required minimum of time each week.

You are required to set a minimum of 12 available hours in a week for a minimum of two days during each week. For example, you can set six-hour windows across two separate days, or you can set four-hour windows across three separate days. To ensure that the windows provide enough time for an update to be applied, each window must be a minimum of 4 hours in duration.  

**Note**: Only users with the Superuser permission (`ops.admin`) can schedule and approve maintenance updates.

1. Go to **ADMINISTRATION &gt; SYSTEM INFORMATION &gt; *Number* pending &gt; Manage Availability**.
2. Expand the **Manage Available Update Windows** section.
3. Click **Add new**.
4. Set your first availability window by selecting the frequency, duration, and start time for the window.
5. Optional: Select **Mark as preferred**, if you'd like to set your recurring availability window as a preferred time for deployments to be scheduled. Preferred windows are given priority, when possible.
6. Click **Submit**.
7. Repeat this process until you have met the minimum requirements for the weekly windows.

### Setting unavailable maintenance windows
{: #blockpreapprovedmaintenance}

You can choose to set specific unavailable update windows of time in which your environment is not available for non-disruptive maintenance updates. For example, you might choose a high traffic weekend or holiday when you do not want to apply any maintenance to ensure that your applications are available for your users.

You are required to set a minimum of 12 available hours in a week for a minimum of two days during each week. If you attempt to create an unavailable update window, you might not be able to save your changes if this new window would cause your system to drop below the weekly required minimum. In this case, you must first either remove some of the existing unavailable update windows or add more available update windows before you can save the new unavailable update window. See [Setting preapproved maintenance windows](index.html#preapprovedmaintenance) for more information.

1. Go to **ADMINISTRATION &gt; SYSTEM INFORMATION &gt; *Number* pending &gt; Manage Availability**.
2. Expand the **Manage Unavailable Update Windows** section.
3. Click **Add new**.
4. Set your unavailable window by selecting the frequency, duration, and start time for the window.
5. Click **Submit**.

### Scheduling and approving updates
{: #scheduleandapprove}

After you set your preapproved maintenance windows, non-disruptive updates will be automatically scheduled during those times. Your explicit approval for these types of updates is not required. However, you can view the details for each maintenance update including what is being updated, how long the update will take, and when the update is scheduled.

To view the details for a non-disruptive update, complete the following steps:

1. Go to **ADMINISTRATION &gt; SYSTEM INFORMATION &gt; *Number* pending**.
2. Identify any rows that have **Customer Scheduling Required** set to **No**.
3. Select the row for that update to view the details.

A disruptive update might affect your environment, running applications, or your users' access to your applications. You must schedule and approve each of these maintenance updates within the alloted 21-day maintenance window. You can select the suggested deployment date and time, the option for any of your preapproved windows, or you can open the calendar to select three specific dates and times for IBM to choose from when scheduling the update.

For disruptive updates that do require your approval, complete the following steps:

1. Go to **ADMINISTRATION &gt; SYSTEM INFORMATION &gt; *Number* pending**.
2. Identify any rows that have **Customer Scheduling Required** set to **Yes**.
3. Select the row for that update to review the details for the update including the update description, suggested date and time for the update, the affected components, and duration for the update.
4. Select **Schedule and Approve**.
5. Choose from the following options: **Suggested date**, **Alternative dates**, or **Any preapproved window**. If you select **Alternative dates**, you can open the calendar to select three options for IBM to choose from.
6. Optional: From the list of selected alternative dates in the calendar, select the ones that you want to be set as preferred dates for deployment. Each selected date is noted as preferred for the deployer who is scheduling the deployment. IBM attempts to schedule maintenance during preferred update windows.
7. Select **Submit** when you are finished.

Based on your selection, the update is scheduled for deployment during the suggested date that you accepted, during one of your preapproved windows, or one of the specific dates and times that you selected. When the update is scheduled for deployment by IBM, you see the scheduled date reflected in the details for the update on the **System Updates** page. You can reschedule an already planned deployment only if a day (24 hours) before the scheduled start date and time remains. Once you have rescheduled a deployment, you can't reschedule it again.


## Viewing system information
{: #oc_system}

To view system information, click **ADMINISTRATION &gt; SYSTEM INFORMATION**.

You can view various sections including pending system updates, general system information, API and CLI information, and
LDAP configuration details.

### Pending system updates

In the Updates section, you can see the number of pending
update notifications that require action on your part. There are two types that you might see:

<dl>
<dt>Non-disruptive updates</dt>
<dd>A non-disruptive update does not affect your environment, your running applications, or your users' access to your applications. This update type does not require case-by-case approval. These updates are applied in the preapproved, available maintenance windows that you set from the System Updates page.</dd>
<dt>Disruptive updates</dt>
<dd>A disruptive update might affect your environment, running applications, or your users' access to your applications. You have the ability to schedule and approve each of these maintenance updates within the allotted 21-day maintenance window to ensure that the update is not applied during critical business hours. You can select the suggested deployment date and time that is based on your preapproved update windows, or you can select two more times and dates for IBM to choose from when applying the update.</dd>
</dl>

For more information about setting preapproved maintenance windows, and setting specific unavailable dates for maintenance, see [Maintenance updates](index.html#oc_schedulemaintenance).

### General system information

In the General Information section, you can view the following information:

- Basic information about the {{site.data.keyword.Bluemix_notm}} build.
- API information including the version, URL, region, and a link to the CLI documentation.
- Shared domain information about your system and service.
- Statistics about the total number of applications, users, and organizations.

### LDAP configuration details

In the LDAP Configuration Details section, you can select the LDAP
server, and view information about user and group mappings. If you are using {{site.data.keyword.IBM}} WebID, it is indicated in this section.

## Viewing usage and reports
{: #oc_resource}

You can view different types of usage information for your local or dedicated instance and {{site.data.keyword.Bluemix_notm}} account. You can also download and view security reports and logs for your {{site.data.keyword.Bluemix_notm}} instance.

- Resource information including disk space, CPU usage, network usage, and average response times. See [Resource usage](index.html#resourceusage).
- Account usage per org including number of runtime apps with usage, total number of runtime GB-hours, and the number of service instances with usage. See [Account usage](index.html#accountusage).
- Org memory quota usage, allocated app memory based on the total used memory quota, and a view of GB-hour usage per app for a specific org. You can also view quota usage for all orgs on the  Organization Administration page in the **Quota Monitoring** section. See [Organization administration](../admin/index.html#orgusage).


### Resource usage
{: #resourceusage}

To view resource usage information, click **ADMINISTRATION &gt; Resource Usage**.

In the **Resource Usage** section, you can view the following information:

- Resource usage information, such as how much memory and disk space can be reserved and how much is physically available, and how much memory and disk space is actually reserved and how much is physically used.  You can also see information about the CPU usage averaged across all droplet execution agents (DEAs). For more detailed information about memory, disk, and CPU usage, see [Memory, Disk, and CPU details](index.html#resourceusagedetails).
- Network usage information for bandwidth in and bandwidth out, over the past 6 hours or day. The data that is displayed is based on the sum of in and out traffic for both public and private networks.
- Average response time for {{site.data.keyword.Bluemix_notm}} over the past 10 minutes, 1 hour, and 1 day.
- Average transactions per second for
{{site.data.keyword.Bluemix_notm}} over the past 10
minutes, hour, and day.

#### System Memory, Disk, and CPU details
{: #resourceusagedetails}

In the **Resource Usage** section, you can see a summary of the **Reserved** and **Physical** amounts for your memory and disk.    
	<dl>
	<dt><strong>Physical</strong></dt>
	<dd>The amount of memory or disk space that was purchased for your environment.</dd>
	<dt><strong>Reserved</strong></dt>
	<dd>The total amount of memory or disk space that is available to be reserved by all deployed and running applications in your environment. Because applications rarely use all of the memory that is reserved by them, the physical value is usually less than the reserved value.</dd>
	</dl>

In addition to the graphical representation, you can see the percentage of memory and disk space that your environment is using. You can also see both the reserved and the physical amounts, in GB, of the actual usage compared to the amount that is available.

To see the usage of your memory, disk, or CPU by DEA, click **Breakdown**.  

To see more detailed information about your physical and reserved memory or disk usage over time, click **History.** You can specify the time frame to view as either weekly or monthly. The historical usage view shows a graph of memory or disk usage over the time you choose.  
	<dl>
	<dt><strong>Reserved Limit</strong></dt>
	<dd>Shown as a horizontal dotted line, the Reserved Limit is the total amount of memory or disk space that can be collectively reserved by all of the applications running in your environment.</dd>
	<dt><strong>Reserved</strong></dt>
	<dd>The Reserved area shows the memory or disk space that is currently collectively reserved by all of the applications running in your environment.
	<p>To see which organizations have reserved the most memory at a particular point in time, hover over the dot along the Reserved area that is associated with that point in time. You can then click an organization in the pie chart that is displayed to see more information about that organization.</p></dd>
	<dt><strong>Physical Limit</strong></dt>
	<dd>Shown as a horizontal dotted line, the Physical Limit shows the amount of physical memory or disk space that was purchased for your environment.</dd>
	<dt><strong>Physical</strong></dt>
	<dd>The Physical area shows the amount of memory or disk space that is actually being used.</dd>
	</dl>

#### Service usage details
{: #servicesresourceusage}

The **Service** tab shows the total service usage in relation to the maximum capacity that you have for a dedicated service. For example, if you have a dedicated Cloudant service, and you are using 500 GB of your 1000 GB capacity, then you see a graphic showing that you have used 50% of your total capacity. The color of the graphic changes based on how close you are to the capacity limit. Yellow is shown when you have used 70% to 84% of your capacity, and red is used when you have reached 85% or more of the available capacity.

**Note**: Service consumption information may not be available in all environments at this time. This feature is available for Cloudant, MessageHub, API Connect, and Session Cache.



### Account usage
{: #accountusage}

You can view the monthly usage for your account for your dedicated or local environment. You can use this data to identify how much to charge specific orgs based on their usage. All admin console users that are assigned the **Users** permission with **Read** access can view the account usage data. In addition, organization billing managers can view the account usage data for their organizations, even if the billing manager does not have the admin console **Users** permission assigned. As an admin console administrator (superuser permission), you can assign the billing manager role for organizations by clicking **Account** &gt; **Manage organizations**.

To view account usage data, complete these steps:

<ol>
<li>Click <strong>Account</strong> &gt; <strong>Usage Dashboard</strong>.</li>
<li>Select the org that you want to see data for.</li>
<li>You can see usage details for the following categories:
<ul>
<li>Runtime apps that have usage</li>
<li>Runtime apps total usage in GB-hours</li>
<li>Service instances that have usage</li>
</ul>
</li>
<li>Optional: View your data for a specific month by using the <strong>Your Cloud Activity</strong> menu to select a month of your choice.</li>
<li>Optional: Click <strong>EXPORT DATA</strong>, and select from <strong>CSV</strong> or <strong>JSON</strong> to export your data for the selected month to a <code>CSV</code> or <code>JSON</code> file.</li>
</ol>

You can also view the monthly usage and associated charges at the account level for your runtimes, apps, and services that are syndicated from {{site.data.keyword.Bluemix_notm}} Public. You can use this data to identify how much to charge specific orgs based on their usage.

<ol>
<li>Click <strong>Account</strong> &gt; <strong>Usage Dashboard</strong>.</li>
<li>Click <strong>Public</strong>.</li>
<li>Select the org that you want to see data for.</li>
<li>You can see usage details for the following categories:
<ul>
<li>Runtime apps that have usage</li>
<li>Runtime apps total usage in GB-hours</li>
<li>Service instances that have usage</li>
<li>A charge summary for all syndicated runtimes, services, and apps</li>
</ul>
</li>
<li>Optional: View your data for a specific month by selecting a month of your choice from the bar graph. The data for the current month displays by default.</li>
<li>Optional: Click <strong>EXPORT DATA</strong>, and select from <strong>CSV</strong> or <strong>JSON</strong> to export your data for the selected month to a <code>CSV</code> or <code>JSON</code> file.</li>
</ol>


### Org usage
{: #orgusage}

To view usage per org, click **ADMINISTRATION &gt; ORGANIZATION ADMINISTRATION**, and then select an org from the **Organization list**. On the **Manage Organizations** page for the org that you selected, you can view the following usage information:

- Number of services that are currently in use.
- Number of routes that are currently in use.
- Memory quota graph that shows how much of the quota is used and how much is not currently being used.
- Application allocation graph that shows which applications are included in the used memory quota.
- Metered application usage graph that shows a a three-month report of used GB-hours per deployed app. You can select the **List View** to see data for all apps, including the memory allocation per app and the metered GB-hour usage for the past three months.

For more information about viewing usage per org, adjusting quota plans, and managing your orgs, see [Administering organizations](../admin/index.html#oc_organizations).

### Reports
{: #oc_report}

You can view security reports and logs, such as DataPower&trade;, firewall, and login audit reports, for your {{site.data.keyword.Bluemix_notm}} instance. To view reports and logs, click **ADMINISTRATION &gt; REPORTS AND LOGS**.

You can do the following tasks from the Reports and Logs tile:

- Select start and end dates from the fields to filter which reports and logs are displayed.
- View your list of requested reports and currently available reports.
- Search within your collection of reports and logs. The search applies to report names as well as text content that is contained within the reports and logs. You can also choose to filter your search by the category.
- Download a report by clicking the ![Download](images/icon_download.png) icon to download the report.
- Request a report to be generated, if you have write access for the reports permission. You can choose from the following six categories for generating a report on demand: Admin Console User Management, {{site.data.keyword.Bluemix_notm}} Platform Administration, Firewall Denies, Firewall Logins, Login Server Login, and Operating System Login. You can request reports for data that is up to 90 days old.

**Note**: The request a report feature might not be available in all environments at this time.

The following table shows the list of security reports that are generated for {{site.data.keyword.Bluemix_notm}} Local and {{site.data.keyword.Bluemix_notm}} Dedicated. Most reports are generated on a daily basis. However, the encryption and key management events reports are generated monthly. All reports are retained for 90 days in the administration console for your retrieval. After that 90 days, the reports are available offline per request from {{site.data.keyword.Bluemix_notm}} for 9 months. In total, reports are available for retrieval for up to 1 year.


{: #ld_table9}

| **Report** | **Description** |      
|-------------------|---------------------|
| [Firewall logins](/docs/hybrid/reports.html#firewalllogins) | Events related to administrator login to the Vyatta firewall devices. |
| [Firewall denies](/docs/hybrid/reports.html#firewalldenies) | Events generated by the Vyatta firewall devices when a request to access is denied according to the firewall rules that are in place. |
| {{site.data.keyword.Bluemix_notm}} [administrators login](/docs/hybrid/reports.html#oslogin) | Events generated by the operating system when an administrator starts an SSH session on every {{site.data.keyword.Bluemix_notm}} system. |
| {{site.data.keyword.Bluemix_notm}} [application developers login](/docs/hybrid/reports.html#loginserverlogins) | Events generated by the {{site.data.keyword.Bluemix_notm}} platform login component when a {{site.data.keyword.Bluemix_notm}} platform user starts a session by using the command line, the REST APIs, or the {{site.data.keyword.Bluemix_notm}} user interface. |
| {{site.data.keyword.Bluemix_notm}} [operating system administration](/docs/hybrid/reports.html#osadmin)  | Events generated by the operating system when an administrator performs action within a current working session. |
| {{site.data.keyword.Bluemix_notm}} [(Cloud Foundry) platform administration](/docs/hybrid/reports.html#platformadmin) | Events related to operations performed by the {{site.data.keyword.Bluemix_notm}} platform user by using the command line, the REST APIs, or the {{site.data.keyword.Bluemix_notm}} user interface. |
| [Internal database administration](/docs/hybrid/reports.html#dbadmin) | Events related to operations performed by a database administrator on the {{site.data.keyword.Bluemix_notm}} internal databases. |
| [User management](/docs/hybrid/reports.html#acusermgmt) | Events related to user management actions performed on the Administration page. |
| [Catalog management](/docs/hybrid/reports.html#catalogmgmt) | Events related to services Catalog changes. |
| [Security reports management](/docs/hybrid/reports.html#securityreportsmgmt) | Events related to security reports management actions performed on the Administration page. |
| [Access reviews](/docs/hybrid/reports.html#securityreportsmgmt) | Reviews for privileged accesses. |
| Management of software changes | Change management activity. |
| [Key certificate management](/docs/hybrid/reports.html#keymgmt) | Key certificate management operations. |
| [System notifications](/docs/hybrid/reports.html#systemnotifications) | Events related to configure the software update deployment windows or notification subscriptions. |

{: caption="Table 9. Security report list" caption-side="top"}

## Viewing status
{: #oc_status}

You can view status for the {{site.data.keyword.Bluemix_notm}} environment and for the administration console.

### {{site.data.keyword.Bluemix_notm}} environment status

You can monitor status for your {{site.data.keyword.Bluemix_notm}} instance by using the {{site.data.keyword.Bluemix_notm}} Status page. Click **Support** &gt; **Status**.

The Status page is the central place to find notifications and announcements about key events that are affecting the {{site.data.keyword.Bluemix_notm}} platform and major services in {{site.data.keyword.Bluemix_notm}}. You can subscribe to an RSS feed for notifications so that you don't have to check for them. For more information about the Status page and setting up the RSS feed, see [Viewing {{site.data.keyword.Bluemix_notm}}](../support/index.html#viewing-bluemix-status).

### Administration console status

After the initial deployment of your {{site.data.keyword.Bluemix_notm}} environment, a verification check is completed automatically on the components that are used to administer your environment. You can go to the Admin Console Verification Check page to check the status of the components after the verification check has run. To access the page, go to <code>https://console.&lt;subdomain&gt;.bluemix.net/check</code>, where `<subdomain>` is the name of your local or dedicated instance.

You can run a verification at any time. You must be logged in to select the option to run the verification. If you encounter failures while you are adding a user, editing an org, or managing your services, run this check to identify whether any components are failing or disconnected. You can open a support ticket with the information from the check to get the issue resolved quickly.

## Managing your Catalog
{: #oc_catalog}

You can manage which {{site.data.keyword.Bluemix_notm}} services are visible to users in the {{site.data.keyword.Bluemix_notm}} Catalog. Click **ADMINISTRATION &gt; CATALOG MANAGEMENT**.

Select a service tile to edit the service plan visibility. To edit the
visibility, select from the following options:

- To show the hidden service so that it is visible to your users in the
Catalog, select **ENABLE ALL PLANS**.
- To hide the service from your users in the {{site.data.keyword.Bluemix_notm}}
Catalog, select **DISABLE ALL PLANS**.
- To control the visibility of an individual plan, select the plan name, and then use the
drop-down menu to select **Enable for all organizations**, **Disable for all organizations**, or **Enable plan for specific organizations**.

<!-- staging only start -->

You can also manage the priority order of available buildpacks to be chosen based on compatibility for your developers when they are creating apps.

1. Go to **ADMINISTRATION &gt; CATALOG MANAGEMENT**
2. Go to the **Compute** section.
3. Select **Buildpack priority**.
4. Select the buildpack option that you want to prioritize higher or lower within the list.
5. With the option selected, use the arrows to move the option within the list.

<!-- staging only end -->

### Registering a service broker
{: #servicebrokerui}

If you have a service that you want to display in your {{site.data.keyword.Bluemix_notm}} catalog, you must implement and register a [service broker ![External link icon](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/services/api.html){: new_window}. After registering your broker, you can choose which orgs can access the service in your local or dedicated instance.

The methods for working with your service broker vary depending on how many services it manages, or whether it has already been registered with {{site.data.keyword.Bluemix_notm}}.

- If your service broker manages one service, you can use the user interface to register it after you have implemented the [Service Broker API ![External link icon](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/services/api.html){: new_window}. See [Registering a service broker that manages one service](index.html#registerbrokerui).
- If your service broker manages multiple services, use the cf CLI with the [{{site.data.keyword.Bluemix_notm}} admin CLI](../cli/plugins/bluemix_admin/index.html) plug-in (`ba` subcommand), or use the [Custom service API](index.html#servicebrokerapi).
- If your service broker is already registered, and you want to update or delete it, use the cf CLI with the [{{site.data.keyword.Bluemix_notm}} admin CLI](../cli/plugins/bluemix_admin/index.html) plug-in (`ba` subcommand), or use the [Custom service API](index.html#servicebrokerapi).

#### Registering a service broker that manages one service
{: #registerbrokerui}

<!-- staging only start -->

Review the following information and complete the steps to register your service broker:

**Before you begin**: <a href="http://docs.cloudfoundry.org/services/api.html" target="_blank">Implement the Cloud Foundry Service Broker API <img src="../icons/launch-glyph.svg" alt="External link icon"></a> to enable communication between your service and {{site.data.keyword.Bluemix_notm}}. The Service Broker API is a set of REST endpoints that are consumed by {{site.data.keyword.Bluemix_notm}}.

When you are implementing the service broker, in the JSON response of <code>GET /v2/catalog</code>, you must provide the definitions for your service and service plans, including the service information that you want to display. For example, review the following sample JSON of the Catalog (GET) response:

```
{
"services":[
   {
      "bindable":true,
      "description":"Cool Service is an analytics and data warehousing solution.",
      "id":"cool-service-id",
      "name":"coolservice",
      "metadata":{
         "displayName":"Cool Service",
         "serviceMonitorApi":"https://myservicesstatus.mybluemix.net/healthcheck/",
         "providerDisplayName":"Cool company",
         "longDescription":"Cool Service is a data warehousing and analytics solution. You can quickly move your data into a next-generation columnar in-memory database and start running complex analytical queries.",
         "bullets":[
            {
               "title":"Fast and Simple",
               "description":"Cool Service uses dynamic in-memory columnar technology and innovations, such as parallel vector processing and actionable compression to rapidly scan and return relevant data."
            },
            {
               "title":"Connectivity",
               "description":"Cool Service is built to let you connect easily and to all of your services and applications. You can start analyzing your data immediately with familiar tools."
            }
         ],
         "featuredImageUrl":"http://path/to/icon_64x64.png",
         "imageUrl":"http://path/to/icon_50x50.png",
         "mediumImageUrl":"http://path/to/icon_32x32.png",
         "smallImageUrl":"http://path/to/icon_24x24.png",
         "documentationUrl":"http://path/to/documentation.html",
         "instructionsUrl":"http://path/to/servicesample.md",
         "termsUrl":"http://path/to/terms_of_agreement.pdf",
         "media":[
            {
               "type":"youtube",
               "thumbnailUrl":"http://path/to/thumbnail.png",
               "url":"http://path/to/youtube/video",
               "caption":"Using Cool Service in 60 Seconds"
            },
            {
               "type":"image",
               "thumbnailUrl":"http://path/to/thumbnail.png",
               "url":"http://path/to/image_file.png",
               "caption":"Cool Service connects applications"
            },
            {
               "type":"video",
               "thumbnailUrl":"http://path/to/thumb.png",
               "caption":"Cool Service works with tables",
               "source":[
                  {
                     "type":"video/mp4",
                     "url":"http://path/to/video_file.mp4"
                  },
                  {
                     "type":"video/ogg",
                     "url":"http://path/to/video_file.ogg"
                  }
               ]
            }
         ]
      },
      "plans":[
         {
            "name":"smallplan",
            "description":"Dedicated schema and tablespace per service instance on a shared server. 1GB and 10GB of compressed database storage can hold up to 5GB and 50GB of uncompressed data respectively based on typical compression ratios.",
            "free":false,
            "id":"cool-service-plan-id",
            "metadata":{
               "bullets":[
                  "1 GB Min per instance. 10 GB Max per instance."
               ],
               "costs":[
                  {
                     "unitId":"INSTANCES_PER_MONTH",
                     "unit":"MONTHLY",
                     "partNumber":"D15UTLL"
                  }
               ],
               "displayName":"Small"
            }
         }
      ]
   }
]
}
```
{: codeblock}

The following tables can help you fill in the JSON file.


{: #ld_table10}

| **JSON fields** | **Description** |
|-----------------|-----------------|
|bindable   | A Boolean value that indicates whether service instances can be bound to applications.  |
|description | The description of the service that is displayed when you use the cf marketplace command, or hover over the service icon in the catalog of the {{site.data.keyword.Bluemix_notm}} user interface. You can add a single sentence or phrase for the description. |
|name | The name of the service that is displayed in the cf command line interface. This name must be unique in {{site.data.keyword.Bluemix_notm}}, and it must use lowercase letters and must not contain spaces. You cannot change the name of the service after you register the service with {{site.data.keyword.Bluemix_notm}}. |
|id  | The ID of the service. This ID must be unique in {{site.data.keyword.Bluemix_notm}} and must be a GUID (Globally Unique Identifier). You cannot change the ID of the service after you register the service with {{site.data.keyword.Bluemix_notm}}. |
|metadata | The service plan metadata that is displayed in the {{site.data.keyword.Bluemix_notm}} catalog and in the pricing sheet. The metadata field is an optional field. You can specify more fields for the metadata. See the following table for [Metadata fields](index.html#metadatafields) for more information. |
|plans | An array of service plan definitions. See the following table for [Plan fields](index.html#planfields) for more information. |
{: caption="Table 10. JSON fields" caption-side="top"}


{: #metadatafields}

| **Metadata values** | **Description** |
|---------------------|-----------------|
|displayName          | The name of the plan that is displayed in the {{site.data.keyword.Bluemix_notm}} user interface. This name is displayed both on the service details page in the catalog and on the pricing sheet. Capitalize only the first letter of the plan name. Do not use "Default" as the default plan name; use "Standard" instead. |
|providerDisplayName | The name of the service provider |
|longDescription | The detailed description for the service. Consider using at least two sentences for a long description. |
|plans                | An array of service plan definitions. Each array entry of the plans field consists of the following fields: name, description, free, id, and metadata. See the following table for [Plan fields](index.html#planfields) for more information. |
|bullets | An array of strings that are displayed for a service. You can use bullets to provide information in addition to the long description. The bullets field must contain at least two bullet elements. Each bullet includes the title and description field. |
|imageUrl | The URL of a large PNG image (50 x 50 pixel). |
|smallImageUrl | The URL of a small PNG image (24 x 24 pixel). |
|mediumImageUrl | The URL of a PNG medium image (32 x 32 pixel). |
|featuredImageUrl | The URL of a featured image (64 x 64 pixel). |
|documentationUrl | the URL of documentation about the service. |
|termsUrl | The URL to PDF files that contain terms of agreement. |
|media (optional) | An array of elements to display the videos and the screen captures that introduce the service in the {{site.data.keyword.Bluemix_notm}} user interface. A media element can contain the following fields: type (image, youtube, video), thumbnailUrl (The URL of the preview image for the media element.), url (The URL of the screen capture or the YouTube video.), source (The sources of videos that are not hosted on YouTube. The "type" of the source of the video must be supported by HTML5. Include "type" and "url" for the video.), and caption (The caption for the media element. Captions help in accessibility for people with disabilities to understand your media elements.). |
|serviceKeysSupported | A boolean value that indicates whether the service keys API is supported. The service keys API is used for enabling a service to be used outside of {{site.data.keyword.Bluemix_notm}}. The default value is false. |
|plan_updateable | A boolean value that indicates whether the service supports plan changes. The default value is false. |
|embeddableDashboard (optional) | A field that indicates how the service dashboard is displayed in the {{site.data.keyword.Bluemix_notm}} user interface. If you do not specify this field, the dashboard is embedded but is restricted to a minimum width of 960px, and the dashboard has more horizontal padding around the iframe. You can use true, false, drilldown, or launch. You can use the following fields for this value: true, false, drilldown, and launch.  |
|notCreatable (optional) | A Boolean value that indicates whether instances for the service can be created from the {{site.data.keyword.Bluemix_notm}} user interface and from the cf command line interface. A value of true means that service instances cannot be created either from the {{site.data.keyword.Bluemix_notm}} user interface or from the cf command line interface. The default value is false. |
|notCreatableMessage (optional) | A message that is displayed in the {{site.data.keyword.Bluemix_notm}} user interface if service instances cannot be created. If you do not specify this field, the following default message will be displayed: To be notified when it is available, confirm your e-mail address, or enter a different email address. |
|notCreatableRobotMessage (optional) | A message that is displayed in the speech bubble of the service details page in the {{site.data.keyword.Bluemix_notm}} user interface. The message is used to indicate that a service might have a problem or other reason that is causing it to be unavailable. You can specify a message to explain the reason. If you do not specify this field, the following default message will be displayed: This service is currently unavailable. |
|apiReferenceUrl (optional) | The URL of the iframe in the API Reference area on the service details page in Catalog. If not used for the service details page in the Catalog, you can enter the numeric value assigned to your REST API Doc for your service when registering it in the {{site.data.keyword.Bluemix_notm}} REST API Doc microservice. This will display your REST API Doc in the service dashboard. |
|sdkDownloadUrl (optional) | The URL of the web page that is opened when you click the Download SDK button. The Download SDK button is on the service tile of the application overview page in the Dashboard. The web page is opened in a new browser tab. |
|serviceMonitorApi    | The URL to an API that returns the JSON data, as shown in the following example, that reports the service health. You must have serviceMonitorApi or serviceMonitorApp in your service metadata. See the following code sample for an example. |
|serviceMonitorApp    | The URL to an application that can be deployed to {{site.data.keyword.Bluemix_notm}} and bound to a service to provide the service status specific output. The application must return the same JSON data format as the serviceMonitorApi. You must have serviceMonitorApi or serviceMonitorApp in your service metadata. See the following code sample for an example. |
{: caption="Table 11. Metadata fields" caption-side="top"}


```
{
    "service": "servicename",
    "version": 1,
    "health": [
        {
            "plan": "starter",
            "status": 0,
            "serviceinput": "count(*) from healthcheck",
            "serviceoutput": "10…or error 1234 database not running",
            "responsetime": 4
        },
        {
            "plan": "enterprise",
            "status": 1,
            "serviceinput": "count(*)fromhealthcheck",
            "serviceoutput": "10…orerror1234databasenotrunning",
            "responsetime": 4
        }
    ]
}
```
{: pre}

The following example shows how the JSON response of GET /v2/catalog is mapped to the service details page in the {{site.data.keyword.Bluemix_notm}} catalog:

![Service details in the catalog.](images/metadata.png "Bluemix Catalog service details view")


{: #planfields}

| **Plan values** | **Description** |
|---------------------|-----------------|
|name       | The name of the service plan that is used in the cf command line interface. For example, the plan name is displayed in the output of the cf marketplace command. The plan name must be in lowercase letters and must not contain spaces, and it must be unique within the service.  |
|description       | The description of the service plan. The description is displayed after you select a plan on the service details page in the {{site.data.keyword.Bluemix_notm}} catalog. |
|free      | A Boolean value that indicates whether the service plan is free. The default value is true. |
|id       | The ID of the service plan. The ID must be unique and it must be a GUID.  |
|metadata (optional)    | The service plan metadata that is displayed in the {{site.data.keyword.Bluemix_notm}} catalog and in the pricing sheet. The metadata field is an optional field. You can specify the following fields within the metadata field: displayName, type (subscription, reservable, planDetails), bullets, costs (unitId, unit, partNumber), and paidOnly. See the following table for [Plan metadata fields](index.html#planmetadata) for more information. |
{: caption="Table 12. Plan fields" caption-side="top"}


{: #planmetadata}

| **Plan metadata values** | **Description** |
|------------------------|-----------------|
|displayName             | The name of the plan that is displayed in the {{site.data.keyword.Bluemix_notm}} user interface. This name is displayed both on the service details page in the catalog and on the pricing sheet.   |
|type                    | The type of the plan. You can use the following values for this field: subscription (A subscription plan. The default value is false.), reservable (A reservable plan. This value is used only when the plan is a subscription plan, that is, the value of plan.metadata.subscription is true. The default value is false.), planDetails (A detailed quantity and description of the resources that can be used with the plan. This value is used only when the plan is reservable, that is, the value of plan.metadata.reserveable is true.) |
|bullets                 | A description of the resources that can be used with the plan. The description is displayed in the **Features** column on the service details page of the catalog and on the pricing sheet. |
|costs                   | The cost information about the service that is displayed in the Price column on the service details page of the catalog and on the pricing.  sheet. Each array entry contains the following fields: unitId (The ID of the unit. Use the plural form and capitalize all letters. For free plans, this field is optional.), unit (The metric that is used for calculating the charges of the service. The value of this field is used in the {{site.data.keyword.Bluemix_notm}} user interface to represent the charge metric.), and partNumber (The `part_number` identifier that is used by the billing system. For free plans, this field is optional.).   |
|paidOnly (optional)     | A Boolean value that indicates whether this service plan is available for {{site.data.keyword.Bluemix_notm}} pay accounts only. A value of **true** means that the service plan is for pay accounts only and cannot be added to trial accounts. A value of **false** means that the service plan can be added to both pay accounts and trial accounts. The default value is **false**.	  |
{: caption="Table 13. Plan metadata fields" caption-side="top"}

The following example shows how the JSON response of GET /v2/catalog is mapped to the service details page in the {{site.data.keyword.Bluemix_notm}} catalog. Specifically, the how the plan metadata fields described in the previous table map to the user interface:

![Plan metadata details in the catalog.](images/plan_metadata.png "Bluemix Catalog plan metadata values view")


<!-- staging only end -->

<ol>
<li>After you have implement the Service Broker API, go to <strong>ADMINISTRATION</strong> &gt; <strong>CATALOG MANAGEMENT</strong>.</li>
<li>Click <strong>REGISTER A SERVICE BROKER</strong>.</li>
<li>Complete the form by entering values in the following fields:
<ul>
<li>Service broker name</li>
<li>Service broker URL</li>
<li>Service broker user name</li>
<li>Service broker password</li>
</ul>
</li>
<li>Click <strong>CONNECT</strong>.</li>
<li>Review the information for your service including the available plans, icon, and the service description.<br />
<p><strong>Note</strong>: If you need to change the catalog information for the service, update your service broker, and start the registration process again by filling in the form.</p>
</li>
<li>Click <strong>REGISTER</strong>.</li>
<li>Choose to enable all plans or only specific plans for the service. All plans are disabled by default.</li>
<li>Enable the service instance for all orgs or specific orgs.</li>
</ol>

You can now see your service in the Custom Services category in your {{site.data.keyword.Bluemix_notm}} Catalog. Go to **ADMINISTRATION &gt; CATALOG MANAGEMENT**, and select the tile in the catalog. You can enable different plans, and edit the plan visibility for your orgs at any time.


## Administering organizations
{: #oc_organizations}

You can manage your organizations by creating and deleting organizations, adding or removing managers for organizations, and monitoring quota usage to make the best decisions for your business.

Click **ADMINISTRATION &gt; ORGANIZATION ADMINISTRATION**.

You can expand and view various sections. You can also review and manage the quota plans for
your organizations.

### Creating orgs

To create an organization and add managers, complete the following steps:

1. Click <strong>CREATE ORGANIZATION</strong>.
2. Enter a name for the organization
3. Enter the name or email of the person that you want to add as a manager. You can add more than one manager by entering and
selecting multiple names.
4. Click <strong>CREATE ORGANIZATION</strong> to save your changes and
create the org.

### Creating spaces

You can create spaces in your organization; for example, a *dev* space as a development environment, a *test* space as a testing environment, and a *production* space as a production environment. Then, you can associate your apps with spaces. Complete the following steps to create a space:

1. From the menu bar, click **Account** &gt; **Manage Organizations**.
2. Select the org that you want to add a space to.
3. Click **Create a Space**.
4. Enter a space name.
5. Click **Create**.

### Quota monitoring

You can expand the **Quota Monitoring** section to view the following information:

- Environment memory usage details the memory usage for the full system environment. The chart shows the following information:
<ul>
<li>The physical memory that is in use and the limit of physical memory that is availble</li>
<li>The quota of memory that is currenctly reserved and the limit of memory that can be reserved</li>
<li>The total quota of memory for your organizations</li>
</ul>
The following types of memory usage are displayed in the chart.

	<dl>
	<dt><strong>Physical Used</strong></dt>
	<dd>The physical memory that is used by your environment.</dd>
	<dt><strong>Physical Limit</strong></dt>
	<dd>The total physical memory that is available to your environment.</dd>
	<dt><strong>Quota Reserved</strong></dt>
	<dd>The sum of memory that is reserved for all deployed applications, across all organizations. The sum of the quota that is reserved can exceed the physical limit of memory for your environment. For example, if you have a physical memory limit of 16 GB, you could reserve 4 GB of memory each for a total of five different applications. The quota that is reserved exceeds the physical limit of memory. However, in many cases, the applications might not use the total quota that is reserved individually to each application. In addition, all applications might not use
	their total quota of reserved memory all at the same time.</dd>
	<dt><strong>Reserve Limit</strong></dt>
	<dd>The total memory that can be reserved across all applications for your environment.</dd>
	<dt><strong>Total quota</strong></dt>
	<dd>The total memory quota across all organizations.</dd>
	</dl>
	**Note**: The data is automatically refreshed every 4 hours. Click **Recalculate** if you want to refresh the data on the page before it is automatically updated.

- Organization memory usage. This section details the memory usage at an organization level. You can view the total memory quota, the quota that is reserved, and the physical memory used by each organization. The chart provides information that is listed by highest memory reserved per organization, and the organization that reserves the largest amount of memory, by default, is listed first. You can sort by **Highest Memory Usage** and **Excess Memory Allocation**.

	<dl>
	<dt><strong>Highest Memory Usage</strong></dt>
	<dd>Use this option to identify the organization that has reserved the greatest amount of memory. Sort by highest memory usage to identify the organizations that have reserved the most amount of memory. The list is sorted by quota reserved. </dd>
	<dt><strong>Excess Memory Allocation</strong></dt>
	<dd>Use this option to identify organizations that have a total memory quota which is larger than needed. Sort by excess memory usage to identify organizations that are using the lowest amount of memory for the quota that has been allocated for the org. </dd>
	</dl>

### Managing quotas
{: #manageorgquota}

A quota represents the resource limits for the organizations in your environment, which is assigned when the organization is created. Any application or service in a space within the organization contributes to the usage of the allocated quota. Complete the following steps to manage the quota for an organization:

<ol>
<li>Click the bar in the chart for the organization that you want to edit in the Organization memory usage section, or select the name of the org from the Organization List section. From the Organization Information page, you can rename the organization and add or remove managers.
<p><strong>Note</strong>: If you select a quota plan that is not sufficient for the current usage for the organization, you receive a message.</p></li>
<li>Click <strong>Cloud Foundry</strong> or <strong>Containers</strong>.  By default, the Cloud Foundry quota page opens.
<ul>
<li>From the Cloud Foundry page, you can select a plan and view the quota details for the following resources:
<ul>
<li>Services</li>
<li>Routes</li>
<li>Memory quota</li>
<li>Application allocation</li>
</ul>
</li>
<li>From the <strong>Containers</strong> page, you can assign values, which must be integers, for the following fields:
<dl class="parml">
<dt class="pt dlterm">Image Limit</dt>
<dd class="pd">The maximum number of container images that you can have in your private registry. A container image is the basis for every container that you create. An image is created from a Dockerfile which is a read-only file that holds the operating system, the app and all of its dependencies, and describes how a container is configured. Images are shared across all members of an organization.</dd>
<dt class="pt dlterm">Memory Allocation Default</dt>
<dd>The amount of container memory that is automatically allocated when a new space is created. When creating a container, you must choose a container size. The size determines the amount of memory that the container can use on the compute host and counts toward your container memory limit. </dd>
<dt class="pt dlterm">Memory Allocation Maximum</dt>
<dd>The maximum amount of container memory that can be allocated across all spaces of an organization.</dd>
<dt class="pt dlterm">Floating IPs Default</dt>
<dd>The number of public IP addresses that is automatically allocated when a new space is created. You can bind public IP addresses to single containers and container groups to make them accessible from the internet.</dd>
<dt class="pt dlterm">Floating IPs Maximum</dt>
<dd>The maximum number of public IP addresses that you cal allocate across all spaces of an organization.</dd>
</dl>
<strong>Note</strong>: If you do not yet have containers in your environment or if you do not yet have the containers in your environment set up, you get an error message.
<p>For more information about containers, see [About IBM containers](/docs/containers/container_ov.html). For more information about container quotas, see [Quota and Bluemix accounts](/docs/containers/container_planning_org_ov.html#container_planning_quota).</p>
<strong>Note:</strong> Containers are not available in the {{site.data.keyword.Bluemix_notm}} Sydney region.</li>
</ul>
<li>To save any changes that you made on the Manage Organization page, click <strong>SAVE</strong>.</li>
</ol>


### Managing your orgs from the organization list
{: #manageorgfrolis}

In the Organization List section, you can view all organizations in the
{{site.data.keyword.Bluemix_notm}} environment, and you can take actions for individual orgs by clicking on the org name.

- To delete the organization, click the **Delete** icon ![Delete](images/icon_trash.svg) in the Actions column.
- To view the quota plan and usage for an organization, click the name for the organization in the
	list. On the **Manage Organizations** page for the org that you selected, you can view the following usage information:

  - Number of services that are currently in use.
  - Number of routes that are currently in use.
  - Memory quota graph that shows how much of the quota is used and how much is not currently being used.
  - Application allocation graph that shows which applications are included in the used memory quota.
  - Metered application usage graph that shows a a three-month report of used GB-hours per deployed app. You can select the **List View** to see data for all apps, including the memory allocation per app and the metered GB-hour usage for the past three months.

- To edit the name of the org and add or remove managers, click the name for the organization in
	the list and follow the prompts on the screen.
- To view information about a specific user of the organization you are viewing, click the user name to display User Information. You can then click the organization name to return to view Organization Information.

## Managing users and permissions
{: #oc_useradmin}

You can add users singly or in groups. Commonly, users are added to your {{site.data.keyword.Bluemix_notm}} instance from your company's user registry through Lightweight Directory Access Protocol (LDAP). You can also view user permissions. If you are assigned **Superuser** permission, you can also set and manage permissions for other users. Click **ADMINISTRATION &gt; USER ADMINISTRATION**.

The User Administration page displays all users for the local or dedicated instance. Permissions for each user are displayed using icons in the table. Permissions can be the following: None, **Superuser**, **Basic Access**, **Catalog**, **Reports**, and **Users**.
The **Superuser** and **Basic Access** permissions can be set to **On** or **Off**, while the remaining permissions are enabled or disabled with specific access types, including **Read** or **Write** access for that permission, as represented by icons. See [Permissions](#permissions) for descriptions of each type and explanation of the icons.

### Working with users
{: #workwithusers}

Depending on your **Read** or **Write** access for the users' permissions, you can search for existing users, remove users, and add users individually or by a group. If you have the **Superuser** permission, you have full access to complete any tasks for user management in the environment. Review the following user management tasks and the level of access needed to complete each task:

* Locate users. If have **Read** or **Write** access and you know all or part of the user name, you can locate users in the table by using the **Search** field. You can also filter the list of users by their organization and permissions. To filter a list of users, complete these steps:
  <ol>
  <li>Click <strong>Filter</strong>.</li>
  <li> Click <strong>Organizations</strong> or <strong>Permissions</strong>, depending on which you want to filter by.
  <dl>
	<dt><strong>Organization</strong></dt>
	<dd>To filter users by their organization, begin typing the organization name in the <strong>Organization</strong> field and select the organization from the list. Then select the role, or roles, assigned to the users within the organization.</dd>
	<dt><strong>Permissions</strong></dt>
	<dd>To filter users by their permissions, first select the type of user, or users. For example, you might want to see all of the Superusers. For permissions other than <strong>Superuser</strong> or <strong>Basic Access</strong>, you can also select the type of access, for example <strong>Read</strong> or <strong>Write</strong>.</dd>
	</dl></li>
  <li>Click <strong>Apply</strong>.</li>
   </ol>

   The User Administration window shows the filters that you set and the users that resulted from the specified filters. You can then search for a user in the filtered table. You can also modify the list of specified filters by removing a filter option from the list.

* Add a single user. If you have **Superuser** permission or
**Users** permission with **Write** access, you can add users.

  1. To add a single user from your LDAP directory, click **Add User**.
  2. In the **Search** field, type the email address for the user, and then select the user from the populated list.
  3. Next, from the **Org** field, choose the org to which you want to add the user by entering the org name and selecting it from the populated list.
  4. To add the user to the selected org, click **Add User**.

  **Note**: When the add operation is successful, the user is added to the table for you to view and search. When users are added, they have no assigned permissions.

* Add a group of users from your LDAP directory. If you have **Superuser** permission or
**Users** permission with **Write** access, you can add users.

  1. Click **Add User Group**.
  2. In the **Search** field, type a group name to search, and select the group name from the populated list.
  3. Next, from the **Org** field, choose the org to which you want to add the user group by entering the org name and selecting it from the populated list.
  4. To add the user group to the selected org, click **Add Users**.

  **Note**: Groups of more than 50 users are added through a background batch job. When the add operation is successful, the user or group is added to the table for you to view and search. When users are added, they have no assigned permissions.

* Add a group of users by importing a spreadsheet that includes user IDs, user email addresses, and the organization to which you plan to add the user. If you have **Superuser** permission or **Users** permission with **Write** access, you can add users.

**Note**: Enter user IDs that match the values used in your user registry.

  1. Click **Import users**.
  2. Click **Download Template (.CSV)** to download a spreadsheet with the required columns that you can fill in, or you can create your own by using a spreadsheet that includes the required column headers: **User ID**, **Email**, and **Organization**.  Two optional columns are also included in the template: **First Name** and **Last Name**.
  3. Fill in the user values for the required columns. If you are not using an LDAP directory, use the required and optional column headers for the users that you are importing.
  4. Save your file, and click **Upload file**.

  **Note**: The columns within your spreadsheet can be in any order as long as you have all of the required columns. If the import was successful, you receive a confirmation message that states that all users were added. If the import was successful for some users, but not others, review the error message to take action on the users that could not be added.

* Remove users. If you have **Superuser** permission or **Users** permission with **Write** access, you can remove users from the environment permanently.

    1. Locate the user and click the ![Delete](images/icon_trash.svg) icon.
    2. Click **Remove**.

* Editing permissions and organizations to which users belong requires you to have **Superuser** permission. To edit permissions for users, locate the user and click the user name. From the **Edit User** page, you can enable or disable permissions:

    * Select **On** from the list to enable the **Superuser** or **Basic Access** permission.
    * Select **Read** from the list to allow the user to have **Read** (read-only) access for that permission, or select **Write** to allow **Write** (edit, or add and remove) access for that permission.
    * Select **Off** to disable any of the permissions.

    **Note**: Setting the **Superuser** permission to **On** sets all other permissions with **Write** access.

* To add or remove a user from a specific org, you must have **Superuser** permission or **Users** permission with **Write** access.

    1. To add a user to an org, select the user name from the table to access the **Edit User** page. Then, use the search field to locate an org, select the org from the list, and click **Save**.
    2. To remove a user from an org, select the user name from the table to access the **Edit User** page. Then, click ![Remove](images/icon_remove.svg) for the org from which you want to remove the user, and click **Save**.

* To view information about the organization the user is assigned to, click the organization name to display Organization Information. You can then click the user name to return to view User Information.

### Permissions
{: #permissions}

Users can be assigned the following permissions with specific access levels (read or write) that enable the user to complete specific tasks within the admin console.


{: #ld_table14}

| **User permission** | **Description** |       
|-----------------|-------------------|
| Superuser | Users with **Superuser** permission set to **On** are allowed to edit permissions for other users. If you have the permission on, it automatically enables full access to all other permissions. In addition to the tasks outlined for each permission in this table, they can also set up notification subscriptions to get alerted directly about maintenance or incidents, schedule maintenance, run verification checks on console components, and create orgs and spaces for the environment. This permission is equivalent to the administrator (admin) role for the admin console.  |
| Basic Access | Users with **Basic Access** permission set to **On** are allowed to see the Administration page option in the {{site.data.keyword.Bluemix_notm}} user interface. Users with the permission enabled can access the [System Information](#oc_system) and [Resource Usage](#oc_resource) tiles. Without this permission, users cannot see or access the Administration menu option. This permission is equivalent to the administrator (admin) role for the admin console. This permission is equivalent to the previously used login permission for the admin console. |
| Catalog | Users with **Catalog** permission can be assigned the access to **Read** or **Write** (modify) which services are available in the local or dedicated instance. Read access allows the user to access the Catalog Management tile to view available services. Write access allows the user to access the [Catalog Management](#oc_catalog) tile to view services, edit the visibility of services, register custom services, and control the buildpack priority list. |  
| Reports | Users with **Reports** permission can be assigned the access to **Read** or **Write** (modify) security reports. Read access allows the user to access the Reports and Logs tile to download reports. Write access allows the user to view the [Reports and Logs](#oc_report) tile as well as use the CLI to upload new reports and create new categories for users to access. |
| Users | Users with **Users** permission can be assigned the access to **Read** (view) the list of users or **Write** (add or remove) users. This permission doesn't allow you to set permissions for other users. Write access allows the user to add new users to the environment, delete users from the environment, and add existing users to organizations that already exist within the environment. In addition, **Write** access allows the user to add new organizations, delete organizations, and edit the users within the organizations. |
{: caption="Table 14. Permissions" caption-side="top"}

## Using REST APIs
{: #auth_adminapi}

To use the REST API commands, you first need to autheticate. To generate and support sessions, you can use cURL commands to accomplish the following tasks:

* [Loggin in to the Admin Console](#auth_loginapi)
* [Storing your user ID and password](#auth_setuidpw)
* [Storing cookies](#auth_apistorecook)
* [Reusing cookies](#auth_apireusecook)

### Logging in to the Admin Console
{: #auth_loginapi}

Before you can run any `Admin` API requests, you must log in to the Admin Console.

To log in to the Admin Console, you can use basic access authentication on the
`https://console.<region>.bluemix.net/login` endpoint. The server returns a cookie with your
session. You use that cookie for all operations with the Admin Console.

**Note:** The session becomes invalid if not used for a few hours.

To log in to the Admin Console, run the following command:

`curl --user <user_id>:<password> -c ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/login | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">--user <em>user_id</em>:<em>password</em></dt>
<dd class="pd">Accepts the user ID and password and sends a Basic Authorization header.</dd>
<dt class="pt dlterm">-c <em>filename</em></dt>
<dd class="pd">Stores the specified user ID and password as a cookie in the specified file.</dd>
<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">Retrieves the specified user ID and password as a cookie in the specified file.</dd>
<dt class="pt dlterm">--header</dt>
<dd class="pd">Sends an Accept header.</dd>
</dl>

The following example shows output from this
command:
```
{
    "message": "Logged in",
    "name": {
        "familyName": "*last_name*",
        "givenName": "*first_name*"
    }
}
```
{: screen}

### Storing your user ID and password
{: #auth_setuidpw}

You can also store your user ID and password so that you don't have to enter it manually each time you log in.  To store your user ID and pasword for reuse, use the following cURL example:

`curl -X GET -H "Authorization: Basic <redacted>" -H "Accept: application/json" "http://localhost:3000/login"`
{: codeblock}

To set up your log in information in a separate file and then call the file so that you don't have to re-enter it for each authentication request, use the `--netrc` option provided by the cURL command.

To use the `--netrc` option with cURL first create a file in the home directory of the user in one of the following ways:
* On a Unix system, create a file named .netrc
* On a Windows system, create a file named _netrc.

In the file, enter the following information:

`machine console.<region>.bluemix.net
login <id>
password <password>`
{: codeblock}

When invoking a cURL command, add the following argument: `--netrc`.
<p>To use a netrc file located in a different directory, use the `--netrc-file [file]` option, where `[file]` is the location of the netrc file.</p>
</li>
</ol>


### Storing cookies
{: #auth_apistorecook}

When you log in to the Admin Console, the server returns a cookie with your session. That cookie is required as part of the login process for future API calls for all operations with the Admin Console. You can store cookies for later use.

To store cookies after you log in, use the `-c` option, as shown in the following CURL example:

`curl --user <user_id>:<password> -c ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/login | python -m json.tool`
{: codeblock}

### Reusing cookies
{: #auth_apireusecook}

To reuse cookies, use the `-b` option with the cookie file name that you assigned with the `-c` option, as shown in the following CURL example:

`curl --user <user_id>:<password> -b ./cookies.txt`
{: codeblock}

## Managing users with the Admin REST API

{: #usingadminapi}

You can use the `Admin` REST API to add and remove users for your
{{site.data.keyword.Bluemix_notm}} instance.
The `Admin` REST API endpoints and JSON responses are provided on an experimental
basis to enable basic operations from a command line. The endpoints and URLs in the examples in this
information might change or might be discontinued at short notice.

If you have **Superuser** permission or **Users**
permission with **Write** access, you can add or remove users. You must have
**Superuser** permission to edit other users' permissions.

Though you can choose to use other tools, the following tools are prerequisites for using the examples that follow:
use other tools as well.
* cURL, to enter REST API requests as commands. cURL is a free utility that you can use to send
HTTP requests to a server and receive the server responses through a command-line interface. You can
download cURL from the [cURL Download site ![External link icon](../icons/launch-glyph.svg)](http://curl.haxx.se/download.html){: new_window}.
* Python, to use the Python pretty-print JSON tool. This optional tool takes the JSON text as
input and provides easy-to-read output. You can download Python from the [Python Downloads site ![External link icon](../icons/launch-glyph.svg)](https://www.python.org/downloads){: new_window}.


### Listing organizations
{: #listingorg}

When you add a user, you must specify an organization. You can use the
`Admin` REST API to list all organizations. You must have
**Users** permission with **Read** access to list
organizations.To list all organizations, run the following command:

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/organizations | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">Passes the user ID and password that was previously stored with the <samp class="ph codeph">-c</samp>
option in the file to the HTTP server as a cookie.</dd>

</dl>

For each organization, the results include the following information:
* `"guid"`, GUID of the organization
* `"name"`, name of the organization

The following example shows output from this command:
```
{
     "resources": [
         {
             "guid": "05af098d-d476-4fb0-8b87-a84350e72af3",
             "name": "org-1"
         },
         {
             "guid": "5129a5a8-37c2-4ee4-a9b2-bebae3531db5",
             "name": "org-2"
         },

		 		 ....

		 ],
		 "total_results": 284
}
```
{: screen}

### Listing users
{: #listingusr}

You can determine whether a user was already added to your
{{site.data.keyword.Bluemix_notm}} environment by
using the `Admin` REST API to list registered users. You must have
**Users** permission with **Read** access to list registered
users.To list all users, run the following command:

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">Passes the user ID and password that was previously stored with the <samp class="ph codeph">-c</samp>
option in the file to the HTTP server as a cookie.</dd>
</dl>

For each registered user, the results include the following information:
* `"first_name"` (given name) and `"last_name"` (surname)
* `"user_id"`, user ID and email address
* `"guid"`, GUID of the organization.
* `"permissions"` that are assigned to the user for the Admin Console.

The following example shows output from this command:

```
{
    "next_url": "/codi/v1/users?results_per_page=100&amp;page=2",
    "prev_url": "",
    "resources": [
        {
            "active": true,
            "created_at": "2015-04-08T17:38:51.788Z",
            "created_by": "",
            "first_name": "some first name",
            "guid": "5d5268cf-39c0-48d3-96ae-7afe928e5dd7",
            "last_name": "some last name",
            "permissions": [
                {
                    "display": "ops.admin"
                },
                {
                    "display": "ops.catalog.write"
                },
                {
                    "display": "ops.reports.write"
                },
                {
                    "display": "ops.catalog.read"
                },
                {
                    "display": "ops.users.write"
                },
                {
                    "display": "ops.reports.read"
                },
                {
                    "display": "ops.login"
                },
                {
                    "display": "ops.users.read"
                }
            ],
            "user_id": "someid@us.ibm.com"
        },
		 		 ...


     }
    ],
    "total_pages": 395,
    "total_results": 39421
}

```
{: screen}

### Adding a user

You can use the `Admin` REST API to add users to the
{{site.data.keyword.Bluemix_notm}} instance. You must
have **Users** permission with **Write** access to add
users, or the **Superuser** permission (ops.admin) for the admin console. Additionally, as the Admin, you can allow organization members who do not have general admin console `user` or `superuser` permission the ability to add new users to their organization only. Use the following API command for this specific capability for organization managers:

```
PUT console.<subdomain>.bluemix.net/codi/env_config/allow_managers?flag=<TRUE or FALSE>
```
{: screen}

You can add one user or a list of users. You can add users to a single
organization, or to multiple organizations.To
add a user, you must provide the following information:

* First name (given name) and last name (surname) of the user. Provide the
`"first_name"` and `"last_name"` from [Listing users](index.html#listingusr).
* Email address and user ID: Provide the `"user_id"` from [Listing users](index.html#listingusr) for both the email address and the user ID.
* `"guid"`. Provide the GUID of the organization from [Listing organizations](index.html#listingorg).

You provide the information in a JSON file.

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">Passes the user ID and password that was previously stored with the <samp class="ph codeph">-c</samp>
option in the file to the HTTP server as a cookie.</dd>
</dl>

<ol>
<li>Create a JSON file that contains the information in a proper JSON format.
<p>For example, create a file that is named `user.json` that has the
following content:</p>
<pre>
{
    "members": [
        {
            "emails": [
                "some_user_id@domain.com"
            ],
            "first_name": "Some_first_name",
            "last_name": "Some_last_name",
            "user_id": "some_user_id@domain.com"
        }
    ],
    "organization_roles": [
        {
            "id": "7a891f9c-e4e7-46c7-8b4e-dffaa7eb3bcd"
        }
    ]
}
</pre>
</li>
<li>Post the content of the JSON file to the user's endpoint by running the following
command:<br/><br/>
<code>
curl -v -b ./cookies.txt -X POST -H "Content-Type: application/json" -d @./user.json https://<your_host>.ibm.com/codi/v1/users
</code>
</li>
</ol>

<dl class="parml">
<dt class="pt dlterm">-v </dt>
<dd class="pd">Specifies verbose output.</dd>
<dt class="pt dlterm">-X POST</dt>
<dd class="pd">Specifies a POST request, overriding the default GET request.</dd>
<dt class="pt dlterm">-H "Content-Type: application/json"</dt>
<dd class="pd">Specifies the content-type header, which in this case is JSON.</dd>
<dt class="pt dlterm">-d *data*</dt>
<dd class="pd">Specifies the data, in this case the file `user.json`, to be sent in POST
request to the HTTP server.</dd>
</dl>

The following example shows output from this
command:

```
* Connected to localhost (127.0.0.1) port 3000 (#0)
 > POST /codi/v1/users HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 > Content-Type: application/json
 > Content-Length: 333
 >
 * upload completely sent off: 333 out of 333 bytes
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < vary: X-HTTP-Method-Override
 < content-type: application/json
 < date: Wed, 22 Apr 2015 19:32:54 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 5612 msec
 ```
{: screen}

### Removing a user

You can use the `Admin` REST API to remove users from the
{{site.data.keyword.Bluemix_notm}} instance. You must
have **Users** permission with **Write** access to remove users.

To remove a user, you must provide the user ID of the user. Run the following command:

`curl -v -b ./cookies.txt -X DELETE https://<your_host>.ibm.com/codi/v1/users?user_id=<some_user_id@domain.com>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-X DELETE</dt>
<dd class="pd">Specifies a DELETE request.</dd>
</dl>

The following example shows output from this
command:

```
 * connect to ::1 port 3000 failed: Connection refused
 *   Trying 127.0.0.1...
 * Connected to localhost (127.0.0.1) port 3000 (#0)
 > DELETE /codi/v1/users?user_id=exampleuser@domain.com HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 >
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < content-type: application/json
 < date: Wed, 22 Apr 2015 21:01:09 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 1922 msec
 <
 ```
{: screen}

## API for metrics
{: #envappmetricsapi}

You can use three experimental APIs to gather metrics about your environment or applications. These APIs return an array of data points for the metrics that you requested over the time that you specified.

The Metrics APIs that are described in the following sections can be accessed from the region-specific endpoint, for example:

`https://console.<region>.bluemix.net/admin/metrics`
{: codeblock}

**Notes**:

1. A user can make up to 200 API requests for metrics an hour.
2. Each API request returns up to 200 data points per request. If more data is available, a URL is provided in the response for loading the next set of data.
3. Each API request requires a user to have at least Basic Access to the Administration Console.  Additional permissions might be required, as specified below.
4. Data are available up to 6 months back from the time the API request is made.

## Gathering metrics about your environment

You can use the experimental environment API to gather high-level environment information over a time period that you specify. Available data points within the time that you specify are returned. Data is recorded approximately every hour. If, for example, you requested six hours of CPU data for the environment, the response would include CPU data for each of the six requested hours.


### Environment endpoints

You can use the following endpoint to invoke this API command:  `/api/v1/env`

**Note**: One of the following permissions are required to access these endpoints: **Basic Access**, **User Read**, **User Write**, or **Superuser**

### Environment metrics query parameters

Using the following query parameters, you can gather metrics for your CPU, disk, memory, network, quota, and apps:

<dl class="parml">
<dt class="pt dlterm">metric</dt>
<dd class="pd">One or more of the following values, separated by commas: `memory`, `disk`, `cpu`, `network`, `quota`, and `apps`.</dd>
<dt class="pt dlterm">startTime</dt>
<dd class="pd">The earliest point in time from which data is returned. If no startTime is specified, the earliest available data point is included. For example, to gather data between 2 PM and 5 PM, specify a startTime of 2 PM.</dd>
<dt class="pt dlterm">endTime</dt>
<dd class="pd">The latest point in time from which data is returned. If no endTime is specified, the most recent data point is used. For example, to gather data between 2 PM and 5 PM, specify an endTime of 5 PM.</dd>
<dt class="pt dlterm">sort</dt>
<dd class="pd">The order in which the data is returned. Valid values are `asc` (ascending) and `desc` (descending). The default is descending, returning the most recent data first. </dd>
</dl>

The following example uses the query parameters to gather metrics about your environment:

```
curl -b ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/admin/metrics/api/v1/env?metric=cpu,network,disk,apps,memory
```
{: codeblock}


### Environment metrics data format

The following sections provide the data format.

 * To gather data records about your memory usage, use the following data format:

```
{
  "sample_time": 1477494000000,
  "memory": {
    "total": {
      "physical": {
        "total_gb": 1728,
        "used": {
          "value_gb": 673.68,
          "percent": 38.99
        }
      },
      "allocated": {
        "reserved_gb": 3456,
        "total_allocated": {
          "value_gb": 2575.18,
          "percent": 74.51
        }
      },
    },
  	"cell": {
      "physical": {
        "total_gb": 864,
        "used": {
          "value_gb": 336.84,
          "percent": 38.99
        }
      },
      "allocated": {
        "reserved_gb": 1728,
        "total_allocated": {
          "value_gb": 1287.59,
          "percent": 74.51
        }
      },
     },
    "dea": {
      "physical": {
      	"total_gb": 864,
        "used": {
          "value_gb": 336.84,
          "percent": 38.99
        }
      },
      "allocated": {
        "reserved_gb": 1728,
        "total_allocated": {
          "value_gb": 1287.59,
          "percent": 74.51
        }
      },
   },
    "memory_by_container": [
      {
        "name": "dea_next/0",
        "type": "dea",
        "ip": "169.53.225.93",
        "percent": "47"
      },
      {
        "name": "dea_next/1",
        "type": "dea",
        "ip": "169.53.225.89",
        "percent": "51"
      },
      {
        "name": "dea_next/2",
        "type": "dea",
        "ip": "169.53.230.49",
        "percent": "45"
      },
      {
        "name": "dea_next/3",
        "type": "dea",
        "ip": "169.44.109.231",
        "percent": "43"
      }
    ]
  }
}
```
{: screen}

 * To gather data records about your disk usage, use the following data format:

```
{
  "sample_time": 1477494000000,
  "disk": {
    "total": {
      "physical": {
        "total_gb": 16200,
        "used": {
          "value_gb": 1614,
          "percent": 9.96
        }
      },
      "allocated": {
        "reserved_gb": 32400,
        "total_allocated": {
          "value_gb": 3979,
          "percent": 12.28
        }
      },
    },
    "cell": {
      "physical": {
        "total_gb": 8100,
        "used": {
          "value_gb": 807,
          "percent": 9.96
        }
      },
      "allocated": {
        "reserved_gb": 16200,
        "total_allocated": {
          "value_gb": 1989.5,
          "percent": 12.28
        }
      },
    },
    "dea": {
      "physical": {
        "total_gb": 8100,
        "used": {
          "value_gb": 807,
          "percent": 9.96
        }
      },
      "allocated": {
        "reserved_gb": 16200,
        "total_allocated": {
          "value_gb": 1989.5,
          "percent": 12.28
        }
      },
    },
    "disk_by_container": [
      {
        "name": "dea_next/0",
        "type": "dea",
        "ip": "169.53.225.93",
        "percent": "13"
      },
      {
        "name": "dea_next/1",
        "type": "dea",
        "ip": "169.53.225.89",
        "percent": "14"
      },
      {
        "name": "dea_next/2",
        "type": "dea",
        "ip": "169.53.230.49",
        "percent": "13"
      },
      {
        "name": "dea_next/3",
        "type": "dea",
        "ip": "169.44.109.231",
        "percent": "12"
      }
    ]
  }
}
```
{: screen}

 * To gather data records about your CPU usage, use the following data format:

```
{
  "sample_time": 1477494000000,
  "cpu": {
    "total": {
      "average_percent_cpu_used": 14.725
    },
    "cell": {
      "average_percent_cpu_used": 19
    },
    "dea": {
      "average_percent_cpu_used": 10.45
    },
    "cpu_by_container": [
      {
        "name": "dea_next/0",
        "type": "dea",
        "ip": "169.53.225.93",
        "sys_percent": "8.4",
        "user_percent": "2.7",
        "wait_percent": "0.0"
      },
      {
        "name": "dea_next/1",
        "type": "dea",
        "ip": "169.53.225.89",
        "sys_percent": "7.4",
        "user_percent": "2.4",
        "wait_percent": "0.0"
      },
      {
        "name": "cell/1",
        "type": "cell",
        "ip": "169.53.230.49",
        "sys_percent": "5.3",
        "user_percent": "1.9",
        "wait_percent": "0.0"
      },
      {
        "name": "cell/2",
        "type": "cell",
        "ip": "169.44.109.231",
        "sys_percent": "8.2",
        "user_percent": "22.6",
        "wait_percent": "0.0"
      }
    ]
  }
}
```
{: screen}

 * To gather data records about your network, use the following data format:

```
{
  "sample_time": 1477494000000,
  "network": {
    "datapower": {
    "response_times": [
      {
        "proxy": "custom_certificates",
        "ten_seconds_ms": "0",
        "one_minute_ms": "0",
        "ten_minutes_ms": "0",
        "one_hour_ms": "0",
        "one_day_ms": "0"
      },
      {
        "proxy": "bluemix",
        "ten_seconds_ms": "90",
        "one_minute_ms": "89",
        "ten_minutes_ms": "83",
        "one_hour_ms": "85",
        "one_day_ms": "95"
      }
      ],
        "transactions": [
      {
        "proxy": "custom_domains",
        "ten_seconds_ms": "0",
        "one_minute_ms": "0",
        "ten_minutes_ms": "0",
        "one_hour_ms": "0",
        "one_day_ms": "0"
      },
      {
        "proxy": "bluemix",
        "ten_seconds_ms": "697",
        "one_minute_ms": "747",
        "ten_minutes_ms": "802",
        "one_hour_ms": "794",
        "one_day_ms": "730"
      }
      ],
        "bandwidth": {
        "in_kbps": 10855,
        "out_kbps": 38090
      }
  }
}
```
{: screen}

* To gather data records about your quota usage, use the following data format:

```
{
  "sample_time": 1477494000000,
  "quota": {
    "reserved_memory": {
      "total_bytes": 33176474877952
    },
    "services": {
      "total": 111650
    },
    "routes": {
      "total": 1675000
    }
  }
}
```
{: screen}

* To gather data records about your applications, use the following data format:

```
{
  "sample_time": 1477494000000,
  "apps": {
    "count": 1406,
    "allocation": {
      "memory_gb": 571.8,
      "disk_gb": 1204
    }
  }
}
```
{: screen}

### Environment metrics response format

```
{
   docs: [],
   next_url:
}
```
{: screen}

## Gathering metrics about your organizations

Data is recorded for all organizations approximately every hour. A request for a particular metric returns information for all organizations in each data sample in the time period you specify, which is sorted in descending order by the requested metric. For example, requesting all organizations by memory over a 6-hour time period in an environment that has 200 apps returns 1200 records, 200 at a time.

To reduce the amount of information that is returned for each data sample in the requested time period, you can specify a count option. Using the previous example and adding a count option of 5 returns 30 records that represent the top 5 organizations by memory for each data sample.

### Organizations endpoints

You can use the following endpoints to invoke this API command:
* `/api/v1/org/memory/physical`
* `/api/v1/org/memory/reserved`
* `/api/v1/org/disk/physical`
* `/api/v1/org/disk/reserved`

**Note**: One of the following permissions are required to access these endpoints: **User Read**, **User Write**, or **Superuser**

### Organizations query parameters

Use the following query parameters to gather metrics for your organizations:

<dl class="parml">
<dt class="pt dlterm">startTime</dt>
<dd class="pd">The earliest point in time from which data is returned. If no startTime is specified, the earliest available data point is included. For example, to gather data between 2 PM and 5 PM, specify a startTime of 2 PM.</dd>
<dt class="pt dlterm">endTime</dt>
<dd class="pd">The latest point in time from which data is returned. If no endTime is specified, the most recent data point is used. For example, to gather data between 2 PM and 5 PM, specify an endTime of 5 PM.</dd>
<dt class="pt dlterm">count</dt>
<dd class="pd">The number of records to return within each data sample.
</dd>
<dt class="pt dlterm">minValue</dt>
<dd class="pd">The smallest value to return for the specified metric.  If no minValue is specified, all values are returned.  For example, to gather organizations using at least 20000 bytes of physical memory, specify a minValue of 20000.
</dd>
</dl>

The following example gathers metrics about your organizations:

```
curl -b ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/admin/metrics/api/v1/org/memory/physical?count=5&startTime=2016-12-02T16:54:09.467Z
```
{: codeblock}

### Organizations response format

```
{
   docs: [],
   next_url:
}
```
{: screen}

Each document that is returned represents the requested metrics for an organization in each data sample, at the point in time of the request.

## Gathering metrics about your applications

Data is recorded for all applications approximately every hour. A request for a particular metric returns information for all apps in each data sample in the time period you specify, which is sorted in descending order by the requested metric. For example, requesting all apps by CPU over a 6-hour time period in an environment that has 200 apps returns 1200 records, 200 at a time.

To reduce the amount of information that is returned for each data sample in the requested time period, you can specify a count option. Using the previous example and adding a count option of 5 returns 30 records that represent the top 5 applications by CPU for each data sample.

### Applications endpoints

You can use the following endpoints to invoke this API command:
* `/api/v1/app/cpu/physical`
* `/api/v1/app/memory/physical`
* `/api/v1/app/memory/reserved`
* `/api/v1/app/disk/physical`
* `/api/v1/app/disk/reserved`

**Note**: One of the following permissions are required to access these endpoints: **User Read**, **User Write**, or **Superuser**

### Applications query parameters

Use the following query parameters to gather metrics for your applications:

<dl class="parml">
<dt class="pt dlterm">startTime</dt>
<dd class="pd">The earliest point in time from which data is returned. If no startTime is specified, the earliest available data point is included. For example, to gather data between 2 PM and 5 PM, specify a startTime of 2 PM.</dd>
<dt class="pt dlterm">endTime</dt>
<dd class="pd">The latest point in time from which data is returned. If no endTime is specified, the most recent data point is used. For example, to gather data between 2 PM and 5 PM, specify an endTime of 5 PM.</dd>
<dt class="pt dlterm">count</dt>
<dd class="pd">The number of records to return within each data sample.
</dd>
<dt class="pt dlterm">minValue</dt>
<dd class="pd">The smallest value to return for the specified metric. If no minValue is specified, all values are returned. For example, to gather applications using at least 20000 bytes of physical memory, specify a minValue of 20000.
</dd>
</dl>

The following example gathers metrics about your applications:

```
curl -b ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/admin/metrics/api/v1/app/cpu/physical?count=5&startTime=2016-12-02T16:54:09.467Z
```
{: codeblock}


### Applications response format

```
{
   docs: [],
   next_url:
}
```
{: screen}

Each document that is returned represents the requested metrics for an application in each data sample, at the point in time of the request.


## Custom service API
{: #servicebrokerapi}

There are three APIs that you can use to register or create a service, update a service, and delete a service.

All APIs are relative to <code>https://console.&lt;subdomain&gt;.bluemix.net/</code>.

<dl>
<dt><strong>&lt;subdomain&gt;</strong></dt>
<dd>This value is the name of your local or dedicated instance. The subdomain name for your {{site.data.keyword.Bluemix}} instance was
assigned during onboarding.</dd>
</dl>

## Registering a new service

Use the following API and code examples to register a new service.

### Route
{: #registerroute}

```
POST /codi/v1/serviceBrokers
```
{: screen}

### Request
{: #registerrequest}

{: #ld_table15}

| **Name** | **Description** |
|-----------------|-------------------|
| name | Name of the service broker. |
| auth_username | User name used to connect with the service broker. |
| auth_password | Password used to connect with the service broker. |
| broker_url | URL used to connect to the service broker. |
| owningOrganization | Initial organization to whitelist the service with. |
{: caption="Table 15. Fields" caption-side="top"}

#### Body
{: #registerbody}

```
{
  "name" : "Service broker's name",
  "auth_username" : "username",
  "auth_password" : "password",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

#### Headers
{: #registerheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### Response
{: #registerresponse}

#### Status
{: #registerstatus}

```
201 Created
```
{: screen}

#### Body
{: #registerbody2}

```
{
    "_id": "2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "name": "Service broker's name",
    "broker_url": "https://provision-broker.comp.bluemix.net/bmx/provisioning/brokers/2063580064-8f23230c-7f36-4ce5-a298-2ab4108f1120",
    "proxy_broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "auth_username": "username",
    "created_on": "2016-09-30T16:45:56.304Z"
}

```
{: screen}

## Updating a service

Use the following API and code examples to update a service.

### Route
{: #updateroute}

`PUT /codi/v1/serviceBrokers`
{: screen}

### Request
{: #updaterequest}

{: #ld_table16}

| **Name** | **Description** |
|-----------------|-------------------|
| name | Name of the service broker. This name cannot be changed from the name that the service was created with. |
| auth_username | User name used to connect with the service broker. |
| auth_password | Password used to connect with the service broker. |
| broker_url | URL used to connect to the service broker. |
| owningOrganization | Initial organization to whitelist the service with. |
{: caption="Table 16. Requests" caption-side="top"}

#### Body
{: #updatebody}

```
{
  "name" : "Service Broker's name",
  "auth_username" : "username",
  "auth_password" : "newPassword",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

#### Headers
{: #updateheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### Response
{: #updateresponse}

#### Status
{: #updatestatus}

```
201 Created
```
{: screen}

#### Body
{: #updatebody2}

```
{
    "_id": "2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "name": "Service Broker's name",
    "broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-d11bdd84-7556-469f-858d-2098b531f7f2",
    "proxy_broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "auth_username": "username",
    "created_on": "2016-09-30T16:45:56.304Z"
}
```
{: screen}

## Deleting a service

Use the following API and code examples to delete a service.


{: #ld_table17}

| **Name** | **Description** |
|-----------------|-------------------|
| name | Name of the service broker. This name cannot be changed from the name that the service was created with. |
{: caption="Table 17. Parameter" caption-side="top"}

### Route

```
DELETE /codi/v1/serviceBrokers?name=name of service broker
```
{: screen}

### Request
{: #deleterequest}

#### Headers
{: #deleteheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### Response
{: #deleteresponse}

#### Status
{: #deletestatus}

```
204 No Content
```
{: screen}

### Managing users with the cf CLI
{: #usingadmincli}

You can manage users for your
{{site.data.keyword.Bluemix_notm}} environment by
using the Cloud Foundry command line interface with the
{{site.data.keyword.Bluemix_notm}} Admin CLI plug-in. You must download this plug-in for your Cloud Foundry CLI.

Before you begin, install the cf command line interface. The
{{site.data.keyword.Bluemix_notm}} Admin CLI plug-in
requires cf version 6.11.2 or later. [Download Cloud Foundry command line interface ![External link icon](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}.

**Restriction:** The Cloud Foundry command line interface is not supported by
Cygwin. Use the Cloud Foundry command line interface in a command line window other than the Cygwin
command line window.

#### Adding the {{site.data.keyword.Bluemix_notm}} Admin CLI plug-in

After the cf command line interface is installed, you can add the
{{site.data.keyword.Bluemix_notm}} admin CLI
plug-in.

**Note**: If you have previously installed the {{site.data.keyword.Bluemix_notm}} Admin plug-in, you might need to uninstall the plug-in, delete the repository, and then re-install to get the latest updates.

Complete the following steps to add the repository and install the plug-in:

<ol>
<li>To add the {{site.data.keyword.Bluemix_notm}} admin plug-in repository, run the following command:<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://console.&lt;subdomain&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">Subdomain of the URL for your {{site.data.keyword.Bluemix_notm}} instance.</dd>
</dl>
</li>
<li>To install the {{site.data.keyword.Bluemix_notm}} Admin CLI plug-in, run the following command:<br/><br/>
<code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

To see a list of the sub-commands available from the plug-ins that you have installed, run the following
command:

```
cf plugins
```
{: codeblock}

To see a list of the available command groups for the {{site.data.keyword.Bluemix_notm}} Admin plug-in, run the following command:

```
cf ba
```
{: codeblock}

For more help for a command, use the `-help` option.

For more information about how to work with the {{site.data.keyword.Bluemix_notm}} Admin CLI plug-in, see [{{site.data.keyword.Bluemix_notm}} admin](../cli/plugins/bluemix_admin/index.html).
