{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

#Administering {{site.data.keyword.Bluemix_notm}}
{: #administer}
*Last updated: 16 December 2015*

Manage your orgs, spaces, and assigned users by clicking **Account and Support** &gt; **Manage Organizations**. If you are a {{site.data.keyword.Bluemix_notm}} Local or {{site.data.keyword.Bluemix_notm}} Dedicated user, see [Managing {{site.data.keyword.Bluemix_notm}} Local and {{site.data.keyword.Bluemix_notm}} Dedicated](index.html#mng) for more information about administering your local or dedicated instance.
{:shortdesc}

##Managing your account
{: #mngacct}

In {{site.data.keyword.Bluemix}}, you can manage orgs and spaces, including user access all from the dashboard in the user interface. You can also monitor your usage and billing.
{:shortdesc}

###Organizations and spaces
{: #orgsandspaces}

As an organization manager or account owner, you can use the Manage Organizations page to view and manage the settings of the organization or space, including user access. To open the Manage Organizations page, on the menu go to *Account and Support* &gt; **Manage Organizations**.

####Organizations

An organization is defined by the following items:

<dl>
<dt>Users</dt>
<dd>The role with basic permission in organizations and spaces. You must be assigned to an organization before you can be granted other permissions to the spaces within the organization. For detailed information, see [Users and roles](index.html#userroles).</dd>
<dt>Domains</dt>
<dd>Provide the route on the internet that is allocated to the organization. A route has a sub-domain and a domain. A sub-domain is typically the application name. A domain might be a system domain, or a custom domain that you registered for your application.<br/>
<p>**Note**: If you add a custom domain, you must configure your DNS server to resolve your custom domain to point to the {{site.data.keyword.Bluemix_notm}} system domain. In this way, when {{site.data.keyword.Bluemix_notm}} receives a request for your custom domain, it can properly route it to your application.</p></dd>
<dt>Quota</dt>
<dd>Represents the resource limits for the organization, including the number of services and the amount of memory that can be allocated for use by the organization. Quotas are assigned when organizations are created. Any application or service in a space of the organization contributes to the usage of the quota. With the Pay as you go or Subscription plans, you can adjust your quota for Cloud Foundry applications and containers as the needs of your organization change.</dd>
</dl>

In {{site.data.keyword.Bluemix_notm}}, you can use organizations to enable collaboration among users, and to facilitate the logical grouping of project resources in the following ways:

<ul>
<li>You can group a set of spaces, applications, services, domains, routes, and users together in organizations.</li>
<li>You can manage the access to the spaces and organizations on a per-user basis.</li>
</ul>

When you create an organization, the organization name must be unique in {{site.data.keyword.Bluemix_notm}}. After you create the organization, you will be automatically assigned the *Organization Manager* permission, which enables you to edit the organization name, delete the organization, and create spaces in the organization.

When you delete an organization, all the spaces, applications, and services within the organization are deleted.

{{site.data.keyword.Bluemix_notm}} enables collaboration on projects by assigning users within an organization, and within the spaces in the organization. You can use the **Users** tab to display and manage users of the organization. You can also invite users to your organization by clicking the **Invite a New User** link on the **Users** tab. The following permissions can be assigned to users in an organization:

<ul>
<li>Organization user</li>
<li>Organization manager</li>
<li>Organization billing manager</li>
<li>Organization auditor</li>
</ul>

####Spaces

Within an organization, you can use spaces to group a set of applications, services, and users.

After you add users to an organization, you can grant them permissions to the spaces within the organization. Similar to organizations, spaces also have a set of permissions that can be assigned to users:

<ul>
<li>Space manager</li>
<li>Space developer</li>
<li>Space auditor</li>
</ul>

**Note**: A user must be assigned at least one of the permissions in the space.

The **Domains** tab for a space is a read-only list of the domains that are assigned to the space. The system domain is always available to a space, and custom domains might also be allocated to the space. Applications that were created in the space might use any of the listed domains for the space.

###Users and roles
{: #userroles}

Account owners perform all operations on organizations and spaces.

####User types

You can be either a member or a collaborator of an account.

<dl>
<dt>Member</dt>
<dd>You are a member of a {{site.data.keyword.Bluemix_notm}} account if you created the account, or you were invited to the account and then you signed up from the invitation, as your first experience with {{site.data.keyword.Bluemix_notm}}. </dd>
<dt>Collaborator</dt>
<dd>You are a collaborator of a {{site.data.keyword.Bluemix_notm}} account if you previously used {{site.data.keyword.Bluemix_notm}} with a different account, but then you were invited to this account and you accepted the invitation.</dd>
</dl>

####User roles

Users can be assigned the following permissions to take different user roles in an organization or space:

<dl>
<dt>Organization managers</dt>
<dd>Organization managers have the following permissions:
<ul>
<li>Create or delete spaces within the organization.</li>
<li>Invite users to the organization if you are also a member of the organization or the account owner.</li>
<li>Manage existing users who are already in the organization.</li>
<li>Manage domains of the organization.</li>
</ul>
<p>**Note**: If you have the user type of collaborator, and previously used {{site.data.keyword.Bluemix_notm}} with a different account, you cannot invite users to the organization even if you are assigned the organization manager role. You must have the user type of member to invite users. See <a href="../troubleshoot/index.html#ts_adduser">Unable to add users to an organization</a> for information about how to work around this problem.</p>
</dd>
<dt>Billing managers</dt>
<dd>Billing managers have permissions to view runtime and service usage information for the organization.</dd>
<dt>Organization auditors</dt>
<dd>Organization auditors have permissions to view application and service content in the space.</dd>
<dt>Space managers</dt>
<dd>Spacing managers have the following permissions:
<ul>
<li>Add users to the space and manager users.</li>
<li>Enable features for the space</li>
</ul>
</dd>
<dt>Space developers</dt>
<dd>Space developers have the following permissions:
<ul>
<li>Create, delete, and manage applications and services within the space.</li>
<li>Have access to logs within the space</li>
</ul>
</dd>
<dt>Space auditors</dt>
<dd>Space auditors have permissions for read-only access to all information about the space, such as information about applications and services, settings, reports, and logs.</dd>
</dl>

###Managing your organization
{: #orgmng}

As an organization manager or account owner, you can manage your organizations. Management tasks include creating an organization, renaming an organization, creating a space, inviting users to a space, and deleting an existing organization.

<ul>
<li>Creating an organization
<p>Only users with pay accounts can create an organization. With a pay account, you can create an organization by taking the following steps:</p>
<ol>
<li>Go to the {{site.data.keyword.Bluemix_notm}} Dashboard, click the icon in the upper right, and select **Manage Organizations**.</li>
<li>Click **Create an Organization** and follow the prompts to create your organization.</li>
</ol>
</li>
<li>Renaming an organization
<p>Take the following steps to rename your organization:</p>
<ol>
<li>Go to the {{site.data.keyword.Bluemix_notm}} Dashboard, click the icon in the upper right, and select **Manage Organizations**.</li>
<li>Select the organization that you want to rename.</li>
<li>Type a new name in the **Organization** field, and click **Save**.</li>
</ol>
</li>
<li>Listing members
<p>Take the following steps to list the members of your organization or space:</p>
<ol>
<li>Go to the {{site.data.keyword.Bluemix_notm}} Dashboard, click the icon in the upper right, and select **Manage Organizations**. You can see the members of your organization and their roles in the **Users** tab.</li>
<li>Click the space name in your organization to see the members of this space and their roles.</li>
</ol>
</li>
<li>Creating a space
<p>You can create spaces in your organization; for example, a *dev* space as a development environment, a *test* space as a testing environment, and a *production* space as a production environment. Then, you an associate your apps with spaces. Take the following steps to create a space:</p>
<ol>
<li>Go to the {{site.data.keyword.Bluemix_notm}} Dashboard, click the icon in the upper right, and select **Manage Organizations**.</li>
<li>Click **Create a Space** under your organization name, and follow the prompts to create your space.</li>
</ol>
</li>
<li>Inviting users to a space
<p>You can invite users to your organization as collaborators. You can also add users of your organization to different spaces. The users can access only the space that they were added to. Take the following steps to add a user to a space:</p>
<ol>
<li>Go to the {{site.data.keyword.Bluemix_notm}} Dashboard, click the icon in the upper right, and select **Manage Organizations**. Then, click **Add user** in your organization, and follow the prompts to add the user to your organization.</li>
<li>Add the user to a space. Select the space from the left navigation pane, click **Add User**, and follow the prompts to add the user to the space.</li>
</ol>
</li>
<li>Deleting an existing organization
<p>Contact {{site.data.keyword.Bluemix_notm}} registration and ID support to delete your organization.</p>
<p>**Note**: Deleting operations cannot be reversed. You lose all your applications and services that are associated with the organization.</p>
</li>
</ul>

## Managing {{site.data.keyword.Bluemix_notm}} Local and {{site.data.keyword.Bluemix_notm}} Dedicated
{: #mng}

Use the Admin Console to manage resources, monitor usage, administer user permissions, and view security reports, logs, status, and upgrade notifications for your {{site.data.keyword.Bluemix}} Local or Dedicated environment.
{:shortdesc}

### Accessing the Admin Console
{: #oc_access}

You can access the Admin Console by entering the following URL:

<code>https://opsconsole.&lt;subdomain&gt;.bluemix.net/</code>

<dl>
<dt><strong>&lt;subdomain&gt;</strong></dt>
<dd>This value is the name of your local or dedicated instance. The subdomain name for your {{site.data.keyword.Bluemix}} instance was
assigned during onboarding.</dd>
</dl>

### Viewing system information
{: #oc_system}

Use the Admin Console to monitor your system information.

To view system information, click **ADMINISTRATION &gt; SYSTEM INFORMATION**.

You can expand and view various sections about pending updates, general system information, and
LDAP configuration details.

* In the Updates section, you can view any pending
updates that require action on your part. You can also easily track your updates using the calendar
link to import your scheduled updates to a calendar app.

<ol>
<li>To take action for a specific update, complete the following steps:
<ol type="a">
<li>Click <strong><em>Number</em> updates pending</strong> to view all pending
updates.</li>
<li>Select an update to take action or view the details of the update, which include the update
window, scheduled date, or disruption status.</li>
<li>Click <strong>SET UNAVAILABLE DATES</strong> to set specific days in the update window
that are not convenient for the update to be applied. If you set unavailable dates, IBM approves and
schedules your update based on your selections. You receive a notification when the update is
approved and scheduled.</li>
<li>Click <strong>APPROVE</strong> to approve the update, if you do not have any unavailable
dates. If you approve, the update is applied during the scheduled update window. IBM sends a
notification when the update deployment starts and ends.</li>
</ol>
</li>
<li>To import your scheduled updates to a calendar app of your choice, complete the following steps:
<ol type="a">
<li>Open your calendar app.</li>
<li>Import the updates calendar by pasting the **Calendar URL** listed on the System Information page in your app. Or, download the calendar file by clicking the Calendar URL, and then import it to your calendar app by using the `.ics` file.</li>
<li>Enter your credentials.</li>
<li>View your scheduled updates.</li>
</ol>
</li>
</ol>

* In the General Information section, you can view the following information:
    * Basic information about the {{site.data.keyword.Bluemix_notm}} build.
    * API information including the version, URL, region, and a link to the CLI documentation.
    * Shared domain information about your system and service.
    * Statistics about the total number of applications, users, and organizations.
* In the LDAP Configuration Details section, you can select the LDAP
server, and view information about user and group mappings. If you are using {{site.data.keyword.IBM}} WebID, it is indicated in the LDAP Configuration
Details section.

### Viewing usage information
{: #oc_resource}

Use the Admin Console to monitor resource and network usage.

To view resource information, click **ADMINISTRATION &gt; USAGE**.

In the Resource Monitoring section, you can view the following
information:

* Resource usage information, such as how many GB of memory and how many GB of disk space are
used. You can view the CPU usage averaged across all droplet execution agents (DEAs). Click the
**CPU** tile, and you can see the CPU usage for each DEA. The DEA with the
highest usage is listed first, and each is identified by their job and IP address. The CPU usage is
separated into three categories that include amount of CPU spent in system processes, amount of CPU
spent in user processes, and amount of CPU spent in waiting processes.
* Network usage information for bandwidth in and bandwidth out, over the past day, week, or month.
The data that is displayed is based on the sum of in and out traffic for both public and private
networks.
* Average response time for {{site.data.keyword.Bluemix_notm}} over the past 10 minutes, hour, and day.
* Average transactions per second for
{{site.data.keyword.Bluemix_notm}} over the past 10
minutes, hour, and day.

### Viewing reports
{: #oc_report}

You can view security reports and logs, such as DataPower&trade;, firewall, and login audit, for
your {{site.data.keyword.Bluemix_notm}} instance.

To view reports and logs, click **ADMINISTRATION &gt; REPORTS AND LOGS**.

Select from the following options:

* You can select start and end dates from the fields to filter which reports and logs are
displayed.
* You can expand and view various reports from the left navigation pane.
* You can search within your collection of reports and logs. The search applies to report
names as well as text content that is contained within the reports and logs. You can also choose to
filter your search by **Administration Events**, **DataPower Reports**, **Firewall**, and **Login Audit**.
* When displaying a report or log, you can click the ![Download](images/icon_download.png)
icon at the upper right of the report to download it.

<!-- This content cannot go into production until the security reports have gone into production -->

For more information about the types of security reports, see [Security reports](../security/index.html#reports).

### Viewing status
{: #oc_status}

You can monitor status for your {{site.data.keyword.Bluemix_notm}} instance through the Admin
Console. You can also subscribe to an RSS feed for notifications so that you don't have to check for them.

To view status for your {{site.data.keyword.Bluemix_notm}} instance, complete the following steps:

1. In the Admin Console in the upper-right corner, click the
**Profile Settings** icon.

2. Then, click **Status**.

The System Status page displays. The left pane displays the status
of your runtimes and services across regions and your {{site.data.keyword.Bluemix_notm}} instance. The right pane shows notifications.

3. If you configured your browser for RSS feeds, you can subscribe to an RSS feed of the
notifications. Locate the ![RSS](images/icon_RSS.png) icon to the right of **UPDATES** at the top left of the notifications list, and select one of the following actions:

* Drag the ![RSS](images/icon_RSS.png) icon into your RSS reader.
* Right-click the RSS icon, select **Copy link address**, and paste the URL
into your RSS reader.

4. Filter which notifications are displayed. Click **FILTER** at the top right
of the notifications list. Then, you can search and narrow the list of notifications by typing a
word that you would expect to find in a notification, for example "maintenance". Or, you can
click to select which notifications to display by **Type**,
**Region**, **Category**, **Start date**, or **End date**.

### Managing your Catalog
{: #oc_catalog}

You can manage which {{site.data.keyword.Bluemix_notm}} services and starters are visible to users in the {{site.data.keyword.Bluemix_notm}} Catalog.

To use the Admin Console to manage the Catalog,
click **ADMINISTRATION &gt; CATALOG MANAGEMENT**.

Select a service or starter tile to edit the service or starter plan visibility. To edit the
visibility, select from the following options:
* To show the hidden service or starter so that it is visible to your users in the
Catalog, select **ENABLE ALL PLANS**.
* To hide the service or starter from your users in the {{site.data.keyword.Bluemix_notm}}
Catalog, select **DISABLE ALL PLANS**.
* To control the visibility of an individual plan, select the plan name, and then use the
drop-down menu to select **Enable for all organizations**, **Disable for
all organizations**, or **Enable plan for specific
organizations**.

### Administering organizations
{: #oc_organizations}

You can manage your organizations by creating and deleting organizations, adding managers to organizations, and monitoring quota usage.

To use the Admin Console to manage your organizations, click **ADMINISTRATION &gt; ORGANIZATION ADMINISTRATION**.

You can expand and view various sections. You can also review and manage the quota plans for
your organizations.

* To create a new organization and add managers, click <strong>CREATE ORGANIZATION</strong>.
Enter a name for the organization, and then enter the name or email of the
person that you want to add as a manager. You can add more than one manager by entering and
selecting multiple names. Click <strong>CREATE ORGANIZATION</strong> to save your changes and
create the org.
* In the Quota Monitoring section, you can expand the section and view
the following information:
    * Environment memory usage. This section details the memory usage for the full system environment.
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
	* Organization memory usage. This section details the memory usage at an organization level. You
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
* To change the quota plan for an organization, click the bar in the chart for the
organization that you want to edit in the Organization memory usage section, or select the name of
the org from the Organization List section. On the Edit
Organization page, you can change the quota plan, change the name of the org, and add or
remove managers. If you select a quota plan that is not sufficient for the current usage for the
organization, you receive a message. To save any changes that you made on the Edit
Organization page, click **SAVE**.
* In the Organization List section, you can view all organizations in the
{{site.data.keyword.Bluemix_notm}} environment.
	* To delete the organization, click ![Delete](images/icon_trash.png) in the Actions column.
	* To view and edit the quota plan for an organization, click the name for the organization in the
	list.
	* To edit the name of the org and add or remove managers, click the name for the organization in
	the list.

### Managing users and permissions
{: #oc_useradmin}
You can add users to your {{site.data.keyword.Bluemix_notm}} instance from your company's user registry through LDAP. You can add users singly or in
groups, and view user permissions. If you are assigned `admin` permission, you
can also set and manage permissions for other users.

To use the Admin Console to manage users, click **ADMINISTRATION &gt; USER ADMINISTRATION**.

The User Administration page displays all users for the local or dedicated instance.
Permissions for each user are displayed. Permissions can be the following: None,
`Admin`, `Catalog`, `Login`,
`Reports`, and `Users`. Permissions can be enabled, or the
user can be given `view` or `write` ability for that
permission, as represented by icons. See [Permissions](#permissions) for descriptions
of each type and explanation of the icons.

Choose from the following options:
* Locate users.You can locate users in the table by using the **Search**
field at the top.
* Add users. If you have `admin` permission or
`users` permission with `write` ability, you can add users. To
add a user or group of users, click **ADD SINGLE USER** or **ADD USER
GROUP**. In the **Search** field, type a user name or group name to
search, and select the organization to add the user or user group to from the
**Org** list. When you find the user or group that you want to add, click the
user name, then click **ADD USER** or **ADD USERS** to add.
Groups of more than 50 users are added through a background batch job. When the add operation
is successful, the user or group is added to the table for you to view and search. When users are
added, they have no assigned permissions.
* Edit permissions and organizations. If you have `admin` permission,
you can edit permissions and organizations for other users. To edit permissions, locate the user and
click the user name. To enable or disable permissions, select from the following options in the
window that opens:
	* Select **On** from the list to enable a permission.
	* Select **Read** from the list to allow the user to have `view` (read-only) ability for that permission, or **Write**
	to allow `write` (edit, or add and remove) ability for that permission.
	* Select **Off** to disable the permission.
To edit organizations, select from the following options:
	* Add the user to an organization by using the search field to locate an organization, clicking to
	select from the options, and clicking **ADD**.
	* Remove a user from an organization by clicking the ![Remove, represented by a minus sign](images/icon_remove.png) icon.
When finished, click **SAVE**.
* Remove users. If you have `admin` permission or
`users` permission with `write` ability, you can remove users.
To remove a user, locate the user and click the ![Delete](images/icon_trash.png) icon and then **Remove**.

#### Permissions
{: #permissions}

Users can be assigned the following permissions:

| **User permission** | **Description** |
|-----------------|-------------------|
| Admin | Users with `admin` permission are allowed to edit permissions for other users. |
| Catalog | Users with `catalog` permission can be assigned the ability to `view` or `write` (modify) which services are available in the local or dedicated instance. |
| Login | Users with `login` permission are allowed to log in to the Admin Console. Without this permission, users can't log in. |
| Reports | Users with `reports` permission can be assigned the ability to `view` or `write` (modify) security reports. |
| Users | Users with `users` permission can be assigned the ability to `view` the list of users or `write` (add or remove) users. This permission doesn't allow you to set permissions for other users.|

*Table 1. Permissions*

Permissions can be enabled, or the user can be given `view` or
`write` ability for that permission, as represented by the following icons:

* The ![Enabled, represented by a check mark](images/icon_enabled.png) icon beside a permission means that it is enabled.
* The ![View, represented by an eye](images/icon_read.png) icon means that the user has `view` (read-only) ability for that permission.
* The ![Write, represented by a pencil](images/icon_write.png) icon means that the user has `write` (edit, add, or remove) ability for that permission.

### Managing users with the Admin REST API
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

#### Logging in to the Admin Console

Before you can run any `Admin` API requests, you must log in to the
Admin Console. If you have `admin` permission or `users`
permission with `write` ability, you can add or remove users. You must have
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

#### Listing organizations
{: #listingorg}

When you add a user, you must specify an organization. You can use the
`Admin` REST API to list all organizations. You must have
`users` permission with `read` ability to list
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

#### Listing users
{: #listingusr}

You can determine whether a user was already added to your
{{site.data.keyword.Bluemix_notm}} environment by
using the `Admin` REST API to list registered users. You must have
`users` permission with `read` ability to list registered
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

#### Adding a user

You can use the `Admin` REST API to add users to the
{{site.data.keyword.Bluemix_notm}} instance. You must
have `users` permission with `write` ability to add
users.

You can add one user or a list of users. You can add users to a single
organization, or to multiple organizations.-->To
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

#### Removing a user

You can use the `Admin` REST API to remove users from the
{{site.data.keyword.Bluemix_notm}} instance. You must
have `users` permission with `write` ability to remove users.

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

### Custom service API
{: #servicebrokerapi}

There are three APIs that you can use to register or create a new service, update a service, and delete a service.

All APIs are relative to <code>https://opsconsole.&lt;subdomain&gt;.bluemix.net/</code>.

<dl>
<dt><strong>&lt;subdomain&gt;</strong></dt>
<dd>This value is the name of your local or dedicated instance. The subdomain name for your {{site.data.keyword.Bluemix}} instance was
assigned during onboarding.</dd>
</dl>

### Registering a new service

Use the following API and code examples to register a new service.

#### Route

```
POST /codi/v1/serviceBrokers
```
{: screen}

#### Request

*Table 3. Fields*

| **Name** | **Description** |
|-----------------|-------------------|
| name | Name of the service broker. |
| auth_username | User name used to connect with the service broker. |
| auth_password | Password used to connect with the service broker. |
| broker_url | URL used to connect to the service broker. |
| owningOrganization | Initial organization to whitelist the service with. |

##### Body

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

##### Headers

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### Response

##### Status

```
201 Created
```
{: screen}

##### Body

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

### Updating a service

Use the following API and code examples to update a service.

#### Route

`PUT /codi/v1/serviceBrokers`
{: screen}

#### Request

*Table 4. Fields*

| **Name** | **Description** |
|-----------------|-------------------|
| name | Name of the service broker. This name cannot be changed from the name that the service was created with. |
| auth_username | User name used to connect with the service broker. |
| auth_password | Password used to connect with the service broker. |
| broker_url | URL used to connect to the service broker. |
| owningOrganization | Initial organization to whitelist the service with. |

##### Body

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

##### Headers

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### Response

##### Status

```
201 Created
```
{: screen}

##### Body

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

### Deleting a service

Use the following API and code examples to delete a service.

*Table 5. Parameter*

| **Name** | **Description** |
|-----------------|-------------------|
| name | Name of the service broker. This name cannot be changed from the name that the service was created with. |

#### Route

```
DELETE /codi/v1/serviceBrokers?name=name of service broker
```
{: screen}

#### Request

##### Headers

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### Response

##### Status

```
204 No Content
```
{: screen}

### Managing users with the cf CLI
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

#### Adding the {{site.data.keyword.Bluemix_notm}} Admin CLI plug-in

After the cf command line interface is installed, you can add the
{{site.data.keyword.Bluemix_notm}} admin CLI
plug-in.

Complete the following steps to add the repository and install the plug-in:

<ol>
<li>To add the {{site.data.keyword.Bluemix_notm}} admin plug-in repository, run the following command:<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://opsconsole.&lt;subdomain&gt;.bluemix.net/cli
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
