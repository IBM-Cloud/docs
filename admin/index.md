---



copyright:

  years: 2015, 2016



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Managing {{site.data.keyword.Bluemix_notm}} Local and {{site.data.keyword.Bluemix_notm}} Dedicated
{: #mng}
*Last updated: 13 June 2016*

If you have administrator access for {{site.data.keyword.Bluemix_notm}} Local or {{site.data.keyword.Bluemix_notm}} Dedicated, go to the **Administration** page to manage resources, monitor quota usage, administer user permissions, schedule upgrade notifications, view security reports and logs, and more. You can manage your orgs by creating spaces and setting [user roles and permissions](index.html#oc_useradmin); see [Managing your organizations](../admin/orgs_spaces.html).
{:shortdesc}

*Table 1. Administrative tasks for managing your {{site.data.keyword.Bluemix_notm}} local or dedicated instance*

| What can I do? | Details |    
|----------------|---------|
|Monitor system usage | Click **ADMINISTRATION &gt; USAGE**. View your system information, monitor CPU usage, and plan usage to make the best decisions for your business. See [Viewing usage information](index.html#oc_resource).|
|Manage your catalog | Click **ADMINISTRATION &gt; CATALOG MANAGEMENT** to manage which services are visible to your users and orgs. See [Managing your catalog](index.html#oc_catalog).|
|Administer orgs | Click **ADMINISTRATION &gt; ORGANIZATION ADMINISTRATION** to create organizations, monitor quotas for organizations, and make needs-based decisions quickly. See [Administering organizations](index.html#oc_organizations).|
|Create spaces and assign user roles | Click the **Account and Support** icon ![Account and Support](../support/images/account_support.svg), then select **Manage Organizations** to create spaces within your orgs. Add users and assign org and space roles to users. See [Managing your organizations](../admin/orgs_spaces.html). |
|Manage administrative user permissions | Click **ADMINISTRATION &gt; USER ADMINISTRATION** to add users, remove users, and adjust user permissions. See [Managing users and permissions](index.html#oc_useradmin). |
|Review reports and logs | Click **ADMINISTRATION &gt; REPORTS AND LOGS** to view security reports and audit logs for you instance. See [Viewing reports](index.html#oc_report). |
|View system information | Click **ADMINISTRATION &gt; SYSTEM INFORMATION** to view system information such as pending updates, name and version of your instance, region, API URL, CLI URL, LDAP configuration details, group and user mappings, statistics, and shared domains. You can also access the calendar feed and event subscriptions for extending your notifications in the Pending Updates section. See [Viewing system information](index.html#oc_system). |
|Extend notifications and set up event subscriptions | Click **ADMINISTRATION &gt; SYSTEM INFORMATION &gt; *Number* updates pending**. You can use web hooks to integrate with a web service of your choice to set up an event notification subscription for an update or incident. See [Notifications and event subscriptions](index.html#oc_eventsubscription). |


## Notifications and event subscriptions
{: #oc_eventsubscription}

You can always know the status of your environment by checking the Status page. As they occur, incidents are reported on the Status page. {{site.data.keyword.Bluemix_notm}} also sends notifications to the Notifications area on the Administration page for events such as scheduled or pending maintenance updates.

### Notifications

You can view notifications for your local or dedicated environment to monitor the status of your environment. Review the following table for information about the different types of notifications and where each notification type is posted.

*Table 2. Event types and notifications methods*

| **Event Type** | **Notification method** |       
|-----------------|-------------------|
| Maintenance updates | You are alerted about upcoming maintenance updates in the Notifications area on the Administration page. Go to the **Administration** page, then select the **Notifications** icon ![Notifications](images/icon_announcement.svg). To see a full list and history of your pending and complete notifications, click **ADMINISTRATION &gt; SYSTEM INFORMATION** &gt; *Number* **pending**. You can extend the notification capability by setting up a subscription that sends an email to recipients of your choice. Or you can set up a subscription that uses webhooks to integrate the notifications from the Administration page with a web service of your choice. |
| Critical incidents | You are alerted about critical incidents on the Status page. Click the **Account and Support** icon ![Account and Support](../support/images/account_support.svg), and then select **Status**. You can extend the notification capability by setting up an event subscription that sends an email to a recipient of your choice. Or you can set up a subscription that uses webhooks to integrate the notifications from the Administration page with a web service of your choice.  |  
| {{site.data.keyword.Bluemix_notm}} Status | You can always view the latest status for the platform, services, and your {{site.data.keyword.Bluemix_notm}} instance on the Status page. Click the **Account and Support** icon ![Account and Support](../support/images/account_support.svg), and then select **Status**.  |

### Setting up event subscriptions

You can extend the functionality of the notifications that are sent to the Administration page and the Status page by using event subscriptions to set up a custom email or use webhooks to integrate with a tool of your choice. If you select the webhooks option, your notifications are routed directly to a destination of your choice, such as a phone number (by SMS message). You can customize the type of notification, specifically maintenance updates or critical incident alerts, and the information that is included in the body of each notification.

**Note**: Only users with the Admin permission (`ops.admin`) can set up event subscriptions.

To access the **Event Subscriptions** page, complete the following steps:

* For maintenance update notifications, go to **SYSTEM INFORMATION &gt; *Number* pending &gt; Subscriptions**.
* For incident notifications, click the **Account and Support** icon ![Account and Support](../support/images/account_support.svg) &gt; **Status**, and then click the **Subscribe** icon ![Subscribe](images/icon_subscribe.svg).

**Note**: You can access the event subscription page for both types of notifications by using either of the two methods described.

To create an email or webhook subscription from the **Event Subscriptions** page, complete the following steps:

1. Click **Add Subscription**.
2. Fill in the event subscription form. For information about the fields on the form and the values to use in the payload section and the message body of the email template, review the following tables.
3. After you complete the form, you can choose from the following options:

  * Click **Save** to save the subscription to your event subscription list. 
  * Click **Save and Test** to save and test the notification. 
  * Click **Save and Close** to save the subscription to your event subscription list, and return to the previous page.

*Table 3. Event subscription form fields for an email subscription*

| **Field** | **Description** |
|-----------------|-------------------|
| Type | Select **Email**. |
| Event | Select to be subscribed to notifications for an Update or Incident. |
| Enabled | Select the option to enable the email notifications. Clear the selection to disable the email notification. Subscriptions are enabled by default. |
| Subject | Enter the subject line for the email. This is a required field.  |
| Body | Enter the message body text to be sent in the email. You can use the IBM payload values to populate the email notification with pertinent information. See the [Payload section values](index.html#payload) table to identify which values you can use. Use basic HTML tags to structure your email. If you do not enter information in this section, you receive a notification that does not have any additional information. This is a required field. |
| To | Enter the email address or addresses using a comma-separated list for the recipients of the email notification. Expand the "cc" or "bcc" options to copy others on the email. This is a required field. |
| Description | Add a unique description for the subscription that you are creating. |


*Table 4. Event subscription form fields for a webhook subscription*

| **Field** | **Description** |
|-----------------|-------------------|
| Type | Select **Webhook** |
| Method | Select **GET** or **POST**. |
| Event | Select to be subscribed to notifications for an Update or Incident. |
| URL | Enter the URL to connect to your web service. |
| Description | Add a unique description for the subscription that you are creating. |
| User name | Enter your user name for your web service. If you don't want to use your personal credentials, you can set up a functional ID to use specifically with {{site.data.keyword.Bluemix_notm}}. |
| Password | Enter the password for your web service. |
| Payload | If you selected the POST method, enter the properties that are specific to the web service that you are using paired with the pyaload values used for the IBM notification. See the [Payload section values](index.html#payload) table to identify which values you can use. If you do not enter information in this section, you receive a notification that does not have any additional information. |

*Table 5. Payload section values*
{: #payload}

| **IBM value** | **Description** | **Event type** |
|----------------|----------------|------------------------|
| {{content.title}} | Message title |  Update and incident  |
| {{type}} | Update or incident | Update and incident | 
| {{region}} | Affected region | Update and incident |
| {{content.message}} | Message description |   Update and incident  |
| {{content.severity}} | Severity rating | Incident |
| {{content.category}} | Affected services | Incident |
| {{content.subCategoryName}} | Affected components | Incident |
| {{status}} | Status of the update | Update |
| {{content.scheduleWindow.start}} | The scheduled start date for the update | Update |
| {{content.scheduleWindow.end}} | The scheduled end time for the update | Update |
| {{content.disruption}} | Affected components | Update |

When your event subscription is saved, you receive notifications through the method that you set up. Notifications still post on the Status page for incidents and in the Notifications area of the Administration page for maintenance updates.

You can select any saved event subscription, view the recent activity, or edit as you need. Click to expand any recent activity entry to view the history details.

## Maintenance updates
{: #oc_schedulemaintenance}

You can view scheduled and pending maintenance updates by going to **ADMINISTRATION &gt; SYSTEM INFORMATION &gt; *Number* pending** to access the **System Updates** page. 

**Note**: See the following section for [Setting preapproved maintenance windows](index.html#preapprovedmaintenance) to get you started. These windows must be set in order for IBM to schedule maintenance for your environment.

<dl>
<dt>Non-disruptive updates</dt>
<dd>A non-disruptive update does not affect your environment, your running applications, or your users' access to your applications. This update type does not require case-by-case approval and will be applied during the preapproved, available maintenance windows that you set from the System Updates page.</dd>
<dt>Disruptive updates</dt>
<dd>A disruptive update might affect your environment, running applications, or your users' access to your applications. You must schedule and approve each of these maintenance updates within the allotted 21-day maintenance window. You can select the suggested deployment date and time, the option for any of your preapproved windows, or you can open the calendar to select three specific dates and times for IBM to choose from when scheduling the update.</dd>
</dl>


### Setting preapproved maintenance windows
{: #preapprovedmaintenance}

Before you start scheduling and approving updates, you must set your preapproved maintenance windows. Non-disruptive updates are scheduled during the preapproved window times. 

You are required to set a minimum of 24 available hours for a week for a minimum of three days during each week. For example, you can set three 8-hour windows across three separate days, or you can set 6-hour windows across four separate days. To ensure that the windows provide enough time for an update to be applied, each window must be a minimum of four hours in duration.

**Note**: Only users with the Admin permission (`ops.admin`) can schedule and approve maintenance updates.

1. Go to **ADMINISTRATION &gt; SYSTEM INFORMATION &gt; *Number* pending &gt; Manage Availability**.
2. Expand the **Manage Available Update Windows** section.
3. Click **Add new** ![Add new](images/add-new.png).
4. Set your first availability window by selecting the frequency, duration, and start time for the window.
5. Click **Submit**.
6. Repeat this process until you have met the minimum requirements for the weekly windows.

### Setting unavailable maintenance windows

After you set your preapproved available maintenance windows, you can choose to set specific dates and times that your environment is not available for updates. For example, you might choose a high traffic weekend or holiday when you do not want any maintenance applied to ensure that your applications are available for your users.

1. Go to **ADMINISTRATION &gt; SYSTEM INFORMATION &gt; *Number* pending &gt; Manage Availability**.
2. Expand the **Manage Unavailable Update Windows** section.
3. Click **Add new** ![Add new](images/add-new.png).
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
5. Choose from the following options: **Suggested date**, **Specific dates**, or **Any preapproved window**. If you select **Specific dates**, you can open the calendar to select three options for IBM to choose from.
6. Select **Submit** when you are finished. 

Based on your selection, the update is scheduled for deployment during the suggested date that you accepted, during one of your preapproved windows, or one of the specific dates and times that you selected. When the update is scheduled for deployment by IBM, you see the scheduled date reflected in the details for the update on the **System Updates** page.


## Viewing system information
{: #oc_system}

To view system information, click **ADMINISTRATION &gt; SYSTEM INFORMATION**.

You can expand and view various sections about pending maintenance updates, general system information, and
LDAP configuration details.

### Pending system updates

In the Updates section, you can see the number of pending
update notifications that require action on your part. There are two types of maintenance updates that you might see:

<dl>
<dt>Non-disruptive updates</dt>
<dd>A non-disruptive update does not affect your environment, your running applications, or your users' access to your applications. This update type does not require case-by-case approval. These updates are applied in the preapproved, available maintenance windows that you set from the System Updates page.</dd>
<dt>Disruptive updates</dt>
<dd>A disruptive update might affect your environment, running applications, or your users' access to your applications. You have the ability to schedule and approve each of these maintenance updates within the allotted 21-day maintenance window to ensure that the update is not applied during critical business hours. You can select the suggested deployment date and time that is based on your preapproved update windows, or you can select two additional times and dates for IBM to choose from when applying the update.</dd>
</dl>

For more information about setting preapproved maintenance windows, setting specific unavailable dates for maintenance, and setting up a calendar feed, see [Maintenance updates](index.html#oc_schedulemaintenance).

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
- Org memory quota usage, allocated app memory based on the total used memory quota, and a view of GB-hour usage per app for a specific org. You can also view quota usage for all orgs on the  Organization Administration page in the Quota monitoring section. See [Organization administration](../admin/index.html#orgusage).


### Resource usage
{: #resourceusage}

To view resource usage information, click **ADMINISTRATION &gt; USAGE**.

In the Resource Monitoring section, you can view the following
information:

- Resource usage information, such as how many GB of memory and how many GB of disk space are
used. You can view the CPU usage averaged across all droplet execution agents (DEAs). Click the
**CPU** tile, and you can see the CPU usage for each DEA. The DEA with the
highest usage is listed first, and each is identified by their job and IP address. The CPU usage is
separated into three categories that include amount of CPU spent in system processes, amount of CPU
spent in user processes, and amount of CPU spent in waiting processes.
- Network usage information for bandwidth in and bandwidth out, over the past day, week, or month.
The data that is displayed is based on the sum of in and out traffic for both public and private
networks.
- Average response time for {{site.data.keyword.Bluemix_notm}} over the past 10 minutes, hour, and day.
- Average transactions per second for
{{site.data.keyword.Bluemix_notm}} over the past 10
minutes, hour, and day.

### Account usage
{: #accountusage}

You can view the monthly usage for your account for your dedicated or local environment. You can use this data to identify how much to charge specific orgs based on their usage.

<ol>
<li>Click the <strong>Account and Support</strong> icon ![Account and Support](../support/images/account_support.svg) &gt; <strong>Account</strong> &gt; <strong>Usage details</strong>.</li>
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
<li>Click the <strong>Account and Support</strong> icon ![Account and Support](../support/images/account_support.svg) &gt; <strong>Account</strong> &gt; <strong>Usage details</strong>.</li>
<li>Click <strong>Public</strong>.</li>
<li>Select the org that you want to see data for, or select <strong>All Organizations</strong> to view the data for all orgs at once.</li>
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

You can view security reports and logs, such as DataPower&trade;, firewall, and login audit, for your {{site.data.keyword.Bluemix_notm}} instance. To view reports and logs, click **ADMINISTRATION &gt; REPORTS AND LOGS**.

Select from the following options:

- You can select start and end dates from the fields to filter which reports and logs are
displayed.
- You can expand and view various reports from the navigation pane.
- You can search within your collection of reports and logs. The search applies to report
names as well as text content that is contained within the reports and logs. You can also choose to
filter your search by **Administration Events**, **DataPower Reports**, **Firewall**, and **Login Audit**.
- When displaying a report or log, you can click the ![Download](images/icon_download.png)
icon to download the report.

The following table shows the list of security reports that are generated for {{site.data.keyword.Bluemix_notm}} Local and {{site.data.keyword.Bluemix_notm}} Dedicated.

*Table 6. Security report list*

| **Category** | **Report** | **Description** |      
|-----------------|-------------------|---------------------|
| Firewall | Firewall logins | Events related to administrator login to the Vyatta firewall devices. |
| Firewall | Firewall denies | Events generated by the Vyatta firewall devices when a request to access is denied according to the firewall rules that are in place. |
| {{site.data.keyword.Bluemix_notm}} administrator login events | {{site.data.keyword.Bluemix_notm}} administrators login | Events generated by the operating system when an administrator starts an SSH session on every {{site.data.keyword.Bluemix_notm}} system. |
| {{site.data.keyword.Bluemix_notm}} application developer login events | {{site.data.keyword.Bluemix_notm}} application developers login | Events generated by the {{site.data.keyword.Bluemix_notm}} platform login component when a {{site.data.keyword.Bluemix_notm}} platform user starts a session by using the command line, the REST APIs, or the {{site.data.keyword.Bluemix_notm}} user interface. |
| {{site.data.keyword.Bluemix_notm}} administrator administrative events | {{site.data.keyword.Bluemix_notm}} administrators operating system administrative events | Events generated by the operating system when an administrator performs action within a current working session. |
| {{site.data.keyword.Bluemix_notm}} application developer administrative events | {{site.data.keyword.Bluemix_notm}} (Cloud Foundry) administrative events | Events related to operations performed by the {{site.data.keyword.Bluemix_notm}} platform user by using the command line, the REST APIs, or the {{site.data.keyword.Bluemix_notm}} user interface. |
| {{site.data.keyword.Bluemix_notm}} administrator database administrative events | Database administrative events | Events related to operations performed by a database administrator on the {{site.data.keyword.Bluemix_notm}} internal databases. |
| Administration events | User management events | Events related to user management actions performed on the Administration page. |
| Administration events | Catalog | Events related to services Catalog changes. |
| Administration events | Security reports management events | Events related to security reports management actions performed on the Administration page. |
| Access reviews | Access reviews report | Reviews for privileged accesses. |
| Change management | Management of software changes | Change management activity. |
| Key management | Management of custom SSL certificates | Custom SSL certifications that were uploaded and stored. |
| Encryption | Data-in-transit encryption | Data-in-transit encryption that is configured. |
| Anti-virus | Anti-virus scan report | Anti-virus software that is in place. |
| Software fix management | Patch application report | Software fixes that were applied. |
| Security incident management | Security incident remediation report | Evidence of security incidents for security incident management. |

## Viewing status
{: #oc_status}

You can view status for the {{site.data.keyword.Bluemix_notm}} environment and for the administration console.

### {{site.data.keyword.Bluemix_notm}} environment status

You can monitor status for your {{site.data.keyword.Bluemix_notm}} instance by using the {{site.data.keyword.Bluemix_notm}} Status page. Click the **Account and Support** icon ![Account and Support](../support/images/account_support.svg), and then select **Status**.

The Status page is the central place to find notifications and announcements about key events that are affecting the {{site.data.keyword.Bluemix_notm}} platform and major services in {{site.data.keyword.Bluemix_notm}}. You can subscribe to an RSS feed for notifications so that you don't have to check for them. For more information about the Status page and setting up the RSS feed, see [Viewing {{site.data.keyword.Bluemix_notm}}](../support/index.html#viewing-bluemix-status).

### Administration console status

After the initial deployment of your {{site.data.keyword.Bluemix_notm}} environment, a verification check is completed automatically on the components that are used to administer your environment. You can go to the Admin Console Verification Check page to check the status of the components after the verification check has run. To access the page, go to <code>https://console.&lt;subdomain&gt;.bluemix.net/check</code>, where `<subdomain>` is the name of your local or dedicated instance.

You can run a verification at any time. You must be logged in to select the option to run the verification. If you encounter failures while you are adding a user, editing an org, or managing your services, run this check to identify whether any components are failing or disconnected. You can open a support ticket with the information from the check to get the issue resolved quickly.

## Managing your Catalog
{: #oc_catalog}

You can manage which {{site.data.keyword.Bluemix_notm}} services and starters are visible to users in the {{site.data.keyword.Bluemix_notm}} Catalog. Click **ADMINISTRATION &gt; CATALOG MANAGEMENT**.

Select a service or starter tile to edit the service or starter plan visibility. To edit the
visibility, select from the following options:

- To show the hidden service or starter so that it is visible to your users in the
Catalog, select **ENABLE ALL PLANS**.
- To hide the service or starter from your users in the {{site.data.keyword.Bluemix_notm}}
Catalog, select **DISABLE ALL PLANS**.
- To control the visibility of an individual plan, select the plan name, and then use the
drop-down menu to select **Enable for all organizations**, **Disable for all organizations**, or **Enable plan for specific organizations**.

You can also manage the priority order of available buildpacks to be chosen based on compatibility for your developers when they are creating apps.

1. Go to **ADMINISTRATION &gt; CATALOG MANAGEMENT**.
2. Go to the **Compute** section.
3. Select **Buildpack priority**.
4. Select the buildpack option that you want to prioritize within the list.
5. With the option selected, use the arrows to move the option within the list. Priority is set by listing the highest prioirty item first in the list.

### Registering a service broker
{: #servicebrokerui}

If you have a service that you want to display in your {{site.data.keyword.Bluemix_notm}} catalog, you must implement and register a service broker. After registering your broker, you can choose which orgs can access the service in your local or dedicated instance.

The methods for working with you service broker vary depending on how many services it manages, or whether it has already been registered with {{site.data.keyword.Bluemix_notm}}.

- If your service broker manages one service, you can use the user interface to register it after you have implemented the [Service Broker API](http://docs.cloudfoundry.org/services/api.html){: new_window}. See [Registering a service broker that manages one service](index.html#registerbrokerui).
- If your service broker manages multiple services, at this time, you can't register it after you have implemented the Service Broker API. Instead, use the cf CLI with the [{{site.data.keyword.Bluemix_notm}} admin CLI](../cli/plugins/bluemix_admin/index.html) plug-in (`ba` subcommand), or use the [Custom service API](index.html#servicebrokerapi).
- If your service broker is already registered, and you want to update or delete it, use the cf CLI with the [{{site.data.keyword.Bluemix_notm}} admin CLI](../cli/plugins/bluemix_admin/index.html) plug-in (`ba` subcommand), or use the [Custom service API](index.html#servicebrokerapi).

#### Registering a service broker that manages one service
{: #registerbrokerui}

Complete the following steps to register your service broker:

<ol>
<li><a href="http://docs.cloudfoundry.org/services/api.html" target="_blank">Implement the Cloud Foundry Service Broker API</a> to enable communication between your service and {{site.data.keyword.Bluemix_notm}}. The Service Broker API is a set of REST endpoints that are consumed by {{site.data.keyword.Bluemix_notm}}.<br />
<br />
<p>When you are implementing the service broker, in the JSON response of <code>GET /v2/catalog</code>, you must provide the definitions for your service and service plans, including the service information that you want to display. For example, review the following sample JSON of the Catalog (GET) response</p>
<p><pre>
"services":[
   {
      "bindable":true,
      "description":"Cool Service is a data warehousing and analytics solution.",
      "id":"cool-service-id",
      "name":"coolservice",
      "tags":[
         "customer_dedicated"
      ],
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
               "description":"Cool Service is built to let you connect easily and to all of your services and applications. You can start analyzing your data right away with familiar tools."
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
</pre></p>
<p><strong>Note</strong>: When you create a service broker for a local or dedicated environment, you must specify `customer_dedicated` in the "tags" field of your service definition JSON file.</p>
</li>
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

To create a new organization and add managers, complete the following steps:

1. Click <strong>CREATE ORGANIZATION</strong>.
2. Enter a name for the organization
3. Enter the name or email of the person that you want to add as a manager. You can add more than one manager by entering and
selecting multiple names.
4. Click <strong>CREATE ORGANIZATION</strong> to save your changes and
create the org.

### Creating spaces

You can create spaces in your organization; for example, a *dev* space as a development environment, a *test* space as a testing environment, and a *production* space as a production environment. Then, you can associate your apps with spaces. Complete the following steps to create a space:

1. Go to the **Account and Support** icon ![Account and Support icon](../admin/images/account_support.svg) &gt; **Manage Organizations** page.
2. Select the org that you want to add a space to.
3. Click **Create a Space**.
4. Enter a space name.
5. Click **Create**.

### Quota monitoring

In the Quota Monitoring section, you can expand the section and view the following information:

- Environment memory usage. This section details the memory usage for the full system environment.
	The chart provides information that includes used system memory, total system memory, quota that is
	used, and the total quota allocated. The following list of terms defines the types of memory usage
	that are displayed in the chart.

	<dl>
	<dt><strong>Used system memory</strong></dt>
	<dd>The physical memory that is used by your environment.</dd>
	<dt><strong>Total system memory</strong></dt>
	<dd>The total physical memory that is available to your environment.</dd>
	<dt><strong>Quota deployed</strong></dt>
	<dd>The sum of memory that is allocated for all deployed apps, across all organizations. The sum of
	the quota deployed can exceed the physical total system memory for your environment. For example, if
	you have a total system memory of 16 GB, and you allocate 4 GB of memory each for a total of five
	different organizations, the total quota exceeds the total system memory that has been allocated to
	you for all organizations. However, in many cases, the organizations might not use the total quota
	that is allocated individually to each organization. In addition, all organizations might not use
	their total quota allocation of memory all at the same time. </dd>
	<dt><strong>Total quota</strong></dt>
	<dd>The total memory that is allocated across all organizations.</dd>
	</dl>

- Organization memory usage. This section details the memory usage at an organization level. You
	can view the total quota allowance and the quota that is deployed for each organization. The chart
	provides information that is listed by highest memory usage per organization, and the organization
	that uses the largest amount of memory, by default, is listed first. You can sort by
	** Highest Memory Usage** and **Excess Memory Allocation**.

	<dl>
	<dt><strong>Highest Memory Usage</strong></dt>
	<dd>Use this option to identify the org using the greatest amount of memory. Sort by highest memory
	usage to identify the organizations that are using the most amount of memory. The list is sorted by
	quota deployed. </dd>
	<dt><strong>Excess Memory Allocation</strong></dt>
	<dd>Use this option to identify organizations that have a quota plan that is larger than needed.
	Sort by excess memory usage to identify organizations that are using the lowest amount of memory for
	the quota that has been allocated for the org. </dd>
	</dl>

### Adjusting quota plans

To change the quota plan for an organization, complete the following steps:

<ol>
<li>Click the bar in the chart for the
organization that you want to edit in the Organization memory usage section, or select the name of
the org from the Organization List section.</li>
<li>On the Manage Organization page, you can change the quota plan, change the name of the org, and add or
remove managers.<br />
<p><strong>Note</strong>: If you select a quota plan that is not sufficient for the current usage for the
organization, you receive a message.</p>
</li>
<li>To save any changes that you made on the Manage Organization page, click <strong>SAVE</strong>.</li>
</ol>

### Managing your orgs from the organization list

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

## Managing users and permissions
{: #oc_useradmin}

You can add users to your {{site.data.keyword.Bluemix_notm}} instance from your company's user registry through LDAP. You can add users singly or in
groups, and view user permissions. If you are assigned `admin` permission, you
can also set and manage permissions for other users. Click **ADMINISTRATION &gt; USER ADMINISTRATION**.

The User Administration page displays all users for the local or dedicated instance.
Permissions for each user are displayed. Permissions can be the following: None,
`Admin`, `Catalog`, `Login`,
`Reports`, and `Users`. Permissions can be enabled, or the
user can be given `view` or `write` access for that
permission, as represented by icons. See [Permissions](index.html#permissions) for descriptions
of each type and explanation of the icons.

### Working with users

You can search for existing users, remove users, and add users individually or by a group. Choose from the following options:

* Locate users.You can locate users in the table by using the **Search**
field.

* Add a single user. If you have `admin` permission or
`users` permission with `write` access, you can add users.

  1. To add a single user from your LDAP directory, click **Add User**.
  2. In the **Search** field, type the email address for the user, and then select the user from the populated list.
  3. Next, from the **Org** field, choose the org to which you want to add the user by entering the org name and selecting it from the populated list.
  4. To add the user to the selected org, click **Add User**.

  **Note**: When the add operation is successful, the user is added to the table for you to view and search. When users are added, they have no assigned permissions.

* Add a group of users from your LDAP directory.

  1. Click **Add User Group**.
  2. In the **Search** field, type a group name to search, and select the group name from the populated list.
  3. Next, from the **Org** field, choose the org to which you want to add the user group by entering the org name and selecting it from the populated list.
  4. To add the user group to the selected org, click **Add Users**.
  **Note**: Groups of more than 50 users are added through a background batch job. When the add operation is successful, the user or group is added to the table for you to view and search. When users are added, they have no assigned permissions.

* Add a group of users by importing a spreadsheet that includes user IDs, user email addresses, and the organization to which you plan to add the user.

  1. Click **Import users**.
  2. Click **Download Template (.CSV)** to download a spreadsheet with the required columns that you can fill in, or you can create your own by using a spreadsheet that includes the required column headers: **User ID**, **Email**, **Organization**.  There are two optional columns that are also included in the template: **First Name** and **Last Name**.
  3. Fill in the user values for the required columns. If you are not using an LDAP directory, use the required and optional column headers for your importing users.
  4. Save your file, and click **Upload file**.
 

  **Note**: Enter user IDs that match the values used in your user registry. The columns within your spreadsheet can be in any order as long as you have all of the required columns. You receive a confirmation message stating that all users were added, if the import was successful. If the import was successful for some users, but not others, review the error message to take action on the users that could not be added.

* Remove users. If you have `admin` permission or `users` permission with `write` access, you can remove users.

    1. Locate the user and click the ![Delete](images/icon_trash.svg) icon.
    2. Click **Remove**.

### Permissions
{: #permissions}

Users can be assigned the following permissions:

*Table 7. Permissions*

| **User permission** | **Description** |       
|-----------------|-------------------|
| Admin | Users with `admin` permission are allowed to edit permissions for other users. |
| Catalog | Users with `catalog` permission can be assigned the access to `view` or `write` (modify) which services are available in the local or dedicated instance. |  
| Login | Users with `login` permission are allowed to see the Administration page. Without this permission, users cannot see the Administration menu option. |
| Reports | Users with `reports` permission can be assigned the access to `view` or `write` (modify) security reports. |
| Users | Users with `users` permission can be assigned the access to `view` the list of users or `write` (add or remove) users. This permission doesn't allow you to set permissions for other users.|


Permissions can be enabled, or the user can be given `view` or
`write` access for that permission, as represented by the following icons:

* The ![Enabled, represented by a check mark](images/icon_enabled.svg) icon beside a permission means that it is enabled.
* The ![View, represented by an eye](images/icon_read.svg) icon means that the user has `view` (read-only) access for that permission.
* The ![Write, represented by a pencil](images/icon_write.svg) icon means that the user has `write` (edit, add, or remove) access for that permission.

Editing permissions and organizations for other users requires you to have `admin` permission. To edit permissions, locate the user and
click the user name. From the **Edit User** page, you can enable or disable permissions:

* Select **On** from the list to enable a permission.
* Select **Read** from the list to allow the user to have `view` (read-only) access for that permission, or select **Write**
to allow `write` (edit, or add and remove) access for that permission.
* Select **Off** to disable the permission.

To add or remove a user from an org, select from the following options:

* To add a user to an org, select the user name from the table to access the **Edit User** screen. Then, use the search field to locate an org, and select the org from the list, and then click **Save**.
* To remove a user from an org, select the user name from the table to access the **Edit User** screen. Then, click ![Remove](images/icon_remove.svg) for the org from which you want to remove the user, and click **Save**.


## Managing users with the Admin REST API
{: #usingadminapi}

You can use the `Admin` REST API to add and remove users for your
{{site.data.keyword.Bluemix_notm}} instance.
The `Admin` REST API endpoints and JSON responses are provided on an experimental
basis to enable basic operations from a command line. The endpoints and URLs in the examples in this
information might change or might be discontinued at short notice.

The following tools are prerequisites for using the examples that follow. You can choose to
use other tools as well.
* cURL, to enter REST API requests as commands. cURL is a free utility that you can use to send
HTTP requests to a server and receive the server responses through a command-line interface. You can
download cURL from the [cURL Download site](http://curl.haxx.se/download.html){: new_window}.
* Python, to use the Python pretty-print JSON tool. This optional tool takes the JSON text as
input and provides easy-to-read output. You can download Python from the [Python Downloads site](https://www.python.org/downloads){: new_window}.

### Logging in to the Admin Console

Before you can run any `Admin` API requests, you must log in to the
Admin Console. If you have `admin` permission or `users`
permission with `write` access, you can add or remove users. You must have
`admin` permission to edit other users' permissions.

To log in to the Admin Console, you can use basic access authentication on the
`https://<your_host>.ibm.com/login` endpoint. The server returns a cookie with your
session. You use that cookie for all operations with the Admin Console.

**Note:** The session becomes invalid if not used for a few hours.

To log in to the Admin Console, run the following command:

`curl --user <user_id>:<password> -c ./cookies.txt --header "Accept: application/json" https://<your_host>.ibm.com/login | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">--user <em>user_id</em>:<em>password</em></dt>
<dd class="pd">Accepts the user ID and password and sends a Basic Authorization header.</dd>


<dt class="pt dlterm">-c <em>filename</em></dt>
<dd class="pd">Stores the specified user ID and password as a cookie in the specified file.</dd>


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

### Listing organizations
{: #listingorg}

When you add a user, you must specify an organization. You can use the
`Admin` REST API to list all organizations. You must have
`users` permission with `read` access to list
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
`users` permission with `read` access to list registered
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
have `users` permission with `write` access to add
users.

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
have `users` permission with `write` access to remove users.

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


## Custom service API
{: #servicebrokerapi}

There are three APIs that you can use to register or create a new service, update a service, and delete a service.

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

*Table 8. Fields*

| **Name** | **Description** |
|-----------------|-------------------|
| name | Name of the service broker. |
| auth_username | User name used to connect with the service broker. |
| auth_password | Password used to connect with the service broker. |
| broker_url | URL used to connect to the service broker. |
| owningOrganization | Initial organization to whitelist the service with. |


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
  "entity": {
    "name": "Service broker's name",
    "broker_url": "https://provision-broker.comp.bluemix.net/bmx/provisioning/brokers/2063580064-8f23230c-7f36-4ce5-a298-2ab4108f1120",
    "auth_username": "username",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "49f3adcc-ecc2-46fa-83c1-03322f04b3b1",
    "created_at": "2015-12-07T19:51:50Z",
    "updated_at": null,
    "url": "/v2/service_brokers/49f3adcc-ecc2-46fa-83c1-03322f04b3b1"
  }
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

*Table 9. Fields*

| **Name** | **Description** |
|-----------------|-------------------|
| name | Name of the service broker. This name cannot be changed from the name that the service was created with. |
| auth_username | User name used to connect with the service broker. |
| auth_password | Password used to connect with the service broker. |
| broker_url | URL used to connect to the service broker. |
| owningOrganization | Initial organization to whitelist the service with. |


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
  "entity": {
    "name": "Service Broker's name",
    "broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-d11bdd84-7556-469f-858d-2098b531f7f2",
    "auth_username": "username",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "2cbdb812-d37f-443b-894a-a96de31e5c38",
    "created_at": "2015-12-07T20:11:08Z",
    "updated_at": "2015-12-07T20:11:19Z",
    "url": "/v2/service_brokers/2cbdb812-d37f-443b-894a-a96de31e5c38"
  }
}
```
{: screen}

## Deleting a service

Use the following API and code examples to delete a service.

*Table 10. Parameter*

| **Name** | **Description** |
|-----------------|-------------------|
| name | Name of the service broker. This name cannot be changed from the name that the service was created with. |


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

## Managing users with the cf CLI
{: #usingadmincli}

You can manage users for your
{{site.data.keyword.Bluemix_notm}} environment by
using the Cloud Foundry command line interface with the
{{site.data.keyword.Bluemix_notm}} Admin CLI plug-in. For
example, you can add users from an LDAP registry.

Before you begin, install the cf command line interface. The
{{site.data.keyword.Bluemix_notm}} Admin CLI plug-in
requires cf version 6.11.2 or later. [Download Cloud Foundry command line interface](https://github.com/cloudfoundry/cli/releases){: new_window}

**Restriction:** The Cloud Foundry command line interface is not supported by
Cygwin. Use the Cloud Foundry command line interface in a command line window other than the Cygwin
command line window.

### Adding the {{site.data.keyword.Bluemix_notm}} Admin CLI plug-in

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

To see a list of commands, run the following
command:

`cf plugins`
{: codeblock}

For additional help for a command, use the `-help` option.

For more information about how to work with the {{site.data.keyword.Bluemix_notm}} Admin CLI plug-in, see [{{site.data.keyword.Bluemix_notm}} admin](../cli/plugins/bluemix_admin/index.html).
