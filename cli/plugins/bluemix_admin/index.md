---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} admin CLI
{: #bluemixadmincli}

*Last updated: 2 June 2016*

You can manage users for your
{{site.data.keyword.Bluemix_notm}} Local or {{site.data.keyword.Bluemix_notm}} Dedicated environment by
using the Cloud Foundry command line interface with the
{{site.data.keyword.Bluemix_notm}} Admin CLI plug-in. For
example, you can add users from an LDAP registry. If you are looking for information about managing your {{site.data.keyword.Bluemix_notm}} Public account, see [Administering](../../../admin/adminpublic.html#administer).

Before you begin, install the cf command line interface. The
{{site.data.keyword.Bluemix_notm}} Admin CLI plug-in
requires cf version 6.11.2 or later. [Download Cloud Foundry command line interface](https://github.com/cloudfoundry/cli/releases){: new_window}

**Restriction:** The Cloud Foundry command line interface is not supported by
Cygwin. Use the Cloud Foundry command line interface in a command line window other than the Cygwin
command line window.

## Adding the {{site.data.keyword.Bluemix_notm}} Admin CLI plug-in

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

## Using the {{site.data.keyword.Bluemix_notm}} Admin CLI plug-in

You can use the {{site.data.keyword.Bluemix_notm}} Admin CLI plug-in to add or remove users, assign or unassign users from orgs, and to perform other management tasks. To see a list of commands, run the following
command:

```
cf plugins
```
{: codeblock}

For additional help for a command, use the `-help` option.

### Connecting and logging in to {{site.data.keyword.Bluemix_notm}}

Before you can use the Admin CLI plug-in to manage users, you must connect and log in, if
you are not already.

<ol>
<li>To connect to the {{site.data.keyword.Bluemix_notm}} API endpoint, run the following command:<br/><br/>
<code>
cf ba api https://console.&lt;subdomain&gt;.bluemix.net
</code>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">Subdomain of the URL for your {{site.data.keyword.Bluemix_notm}} instance.<br />
</dd>
</dl>
<p>You can check the Admin Console Resources and Information page for the
correct URL. The URL is shown in the API Information section in the **API URL**
field.</p>
</li>
<li>Log in to {{site.data.keyword.Bluemix_notm}} with the following command:<br/><br/>
<code>
cf login
</code>
</li>
</ol>

### Adding a user

You can add a user to your
{{site.data.keyword.Bluemix_notm}} environment from
an LDAP registry. Enter the following command:

```
cf ba add-user <user_name> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">The name of the user in the LDAP registry.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to add the user to.</dd>
</dl>

**Tip:** You can also use **ba au** as an alias for the longer
**ba add-user** command name.

<!-- staging-only commands start. Live for interconnect -->

### Search for a user

You can search for a user. Enter the following command:

```
cf ba search-users <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">The name of the user in {{site.data.keyword.Bluemix_notm}}.</dd>

</dl>

**Tip:** You can also use **ba su** as an alias for the longer
**ba search-users** command name.

### Set permissions for a user

You can set permissions for a specified user. Enter the following command:

```
cf ba set-permissions <user_name> <permission> <access>
```
{: codeblock}

**Note**: You can set one permission at a time.

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">The name of the user in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;permission&gt;</dt>
<dd class="pd">Set the permissions for the user: Admin, Login, Catalog (read or write access), Reports (read or write access), or Users (read or write access).</dd>
<dt class="pt dlterm">&lt;access&gt;</dt>
<dd class="pd">For Catalog, Reports, or Users permissions, you must also set the level of access as <code>read</code> or <code>write</code>.</dd>
</dl>

**Tip:** You can also use **ba sp** as an alias for the longer
**ba set-permissions** command name.

<!-- staging-only commands end -->

### Removing a user

You can remove a user from your
{{site.data.keyword.Bluemix_notm}} environment by
entering the following command:

```
cf ba remove-user <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">The name of the user in {{site.data.keyword.Bluemix_notm}}.</dd>

</dl>

**Tip:** You can also use **ba ru** as an alias for the longer
**ba remove-user** command name.

### Adding and deleting an organization

You can add and delete an organization.

* To add an organization, enter the following command:

```
cf ba create-organization <organization> <manager>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to add.</dd>
<dt class="pt dlterm">&lt;manager&gt;</dt>
<dd class="pd">The user name of the manager for the org.</dd>
</dl>

**Tip:** You can also use **ba co** as an alias for the longer
**ba create-organization** command name.

* To delete an organization, enter the following command:

```
cf ba delete-organization <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to delete.</dd>
</dl>

**Tip:** You can also use **ba do** as an alias for the longer
**ba delete-organization** command name.

### Assigning a user to an organization

You can assign a user in your
{{site.data.keyword.Bluemix_notm}} environment to a
particular organization. Enter the following command:

```
cf ba set-org <user_name> <organization> [<role>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">The name of the user in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to assign the user to.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">See [Roles](../../../admin/users_roles.html#userrolesinfo) for
{{site.data.keyword.Bluemix_notm}} user roles and
descriptions.</dd>
</dl>

**Tip:** You can also use **ba so** as an alias for the longer
**ba set-org** command name.

### Unassigning a user from an organization

You can unassign a user in your
{{site.data.keyword.Bluemix_notm}} environment from a
particular organization. Enter the following command:

```
cf ba unset-org <user_name> <organization> [<role>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">The name of the user in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to assign the user to.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">See [Roles](../../../admin/users_roles.html#userrolesinfo) for
{{site.data.keyword.Bluemix_notm}} user roles and
descriptions.</dd>
</dl>

**Tip:** You can also use **ba uo** as an alias for the longer
**ba unset-org** command name.

### Roles

<dl class="parml">
<dt class="pt dlterm">OrgManager</dt>
<dd class="pd">Organization manager. An org manager has authority to do the following actions:
<ul>
<li>Create or delete spaces within the organization.</li>
<li>Invite users to the organization and manage users.</li>
<li>Manage domains of the organization.</li>
</ul>
</dd>
<dt class="pt dlterm">BillingManager</dt>
<dd class="pd">Billing manager. A billing manager can view runtime and service usage information for the
organization.</dd>
<dt class="pt dlterm">OrgAuditor</dt>
<dd class="pd">Organization auditor. An organization auditor can view application and service content in the
space.</dd>
</dl>

### Setting a quota for an organization

You can set the usage quota for a particular organization.

```
cf ba set-quota <organization> <plan>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to set the quota for.</dd>
<dt class="pt dlterm">&lt;plan&gt;</dt>
<dd class="pd">The quota plan for an organization.</dd>
</dl>

**Tip:** You can also use **ba sq** as an alias for the longer
**ba set-quota** command name.

### Adding, deleting, and retrieving reports

You can add, delete, and retrieve security reports.
* To add a report, enter the following command:

```
cf ba add-report <category> <date> <PDF|TXT|LOG> <RTF>
```
{: codeblock}

**Note**: If you have write access for the reports permission, you can create a new category and add a report in any of the accepted formats for your users. Enter the new category name for the `category` parameter, or add your new report to an existing category.

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">The category for the report. If there is a space in the name, use quotation marks around the
name.</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">The report date in the format <samp class="ph codeph">YYYYMMDD</samp>.</dd>
<dt class="pt dlterm">&lt;PDF|TXT|LOG&gt;</dt>
<dd class="pd">The path for the report PDF, text file, or log file to upload.</dd>
<dt class="pt dlterm">&lt;RTF&gt;</dt>
<dd class="pd">An option to include a Rich Text Format (RTF) version of the PDF. This option applies only if
you included a path to the report PDF. The RTF version is used for indexing and searching.</dd>
</dl>

**Tip:** You can also use **ba ar** as an alias for the longer
**ba add-report** command name.

* To delete a report, enter the following command:

```
cf ba delete-report <category> <date> <name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">The category for the report. If there is a space in the name, use quotation marks around the
name.</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">The report date in the format <samp class="ph codeph">YYYYMMDD</samp>.</dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">The name of the report.</dd>
</dl>

**Tip:** You can also use **ba dr** as an alias for the longer
**ba delete-report** command name.

* To retrieve a report, enter the following command:

```
cf ba retrieve-report <category> <date> <name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">The category for the report. If there is a space in the name, use quotation marks around the
name.</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">The report date in the format <samp class="ph codeph">YYYYMMDD</samp>.</dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">The name of the report.</dd>
</dl>

**Tip:** You can also use **ba rr** as an alias for the longer **ba retrieve-report** command name.

### Enabling and disabling services for all organizations

You can enable or disable a service from being displayed in the
{{site.data.keyword.Bluemix_notm}} Catalog for all organizations.

* To enable a service to be visible in the
{{site.data.keyword.Bluemix_notm}} Catalog for all
organizations, enter the following command:

```
cf ba enable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">The name or GUID of the service plan that you want to enable. If you enter a non-unique service name,
you are prompted with service plans to choose from. To identify a service plan name, select the service category from the homepage, then select **Add** to view the services for that category. Click the service name to open the details view, then you can view which pricing plans are available for that service. </dd>
</dl>

**Tip:** You can also use **ba esp** as an alias for the longer
**ba enable-service-plan** command name.

* To disable a service from being visible in the
{{site.data.keyword.Bluemix_notm}} Catalog for all
organizations, enter the following command:

```
cf ba disable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">The name or GUID of the service plan that you want to enable. If you enter a non-unique service name,
you are prompted with service plans to choose from. To identify a service plan name, select the service category from the homepage, then select **Add** to view the services for that category. Click the service name to open the details view, then you can view which pricing plans are available for that service.</dd>
</dl>

**Tip:** You can also use **ba dsp** as an alias for the longer
**ba disable-service-plan** command name.

### Adding, removing, and editing service visibility for organizations

You can add or remove an organization from the list of organizations that can see a
specific service in the {{site.data.keyword.Bluemix_notm}} Catalog. You can also edit and replace the list of services that specific
organizations can see in the {{site.data.keyword.Bluemix_notm}} Catalog.

* To allow an organization to view a specific service in the
{{site.data.keyword.Bluemix_notm}} Catalog, enter the
following command:

```
cf ba add-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">The name or GUID of the service plan that you want to enable. If you enter a non-unique service name,
you are prompted with service plans to choose from. To identify a service plan name, select the service category from the homepage, then select **Add** to view the services for that category. Click the service name to open the details view, then you can view which pricing plans are available for that service.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to add to the service's visibility list.</dd>
</dl>

**Tip:** You can also use **ba aspv** as an alias for the longer
**ba add-service-plan-visibility** command name.

* To remove the visibility of a service in the
{{site.data.keyword.Bluemix_notm}} Catalog for an
organization, enter the following command:

```
cf ba remove-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">The name or GUID of the service plan that you want to enable. If you enter a non-unique service name,
you are prompted with service plans to choose from. To identify a service plan name, select the service category from the homepage, then select **Add** to view the services for that category. Click the service name to open the details view, then you can view which pricing plans are available for that service.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to remove from the service's visibility list.</dd>
</dl>

**Tip:** You can also use **ba rspv** as an alias for the longer
**ba remove-service-plan-visibility** command name.

* To replace all existing visible services for an organization or multiple organizations, use the
following command:

```
cf ba edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>
```
{: codeblock}

**Note:** This
command replaces existing visible services for the specified organizations with the service that you
specify in the command.

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">The name or GUID of the service plan that you want to enable. If you enter a non-unique service name,
you are prompted with service plans to choose from. To identify a service plan name, select the service category from the homepage, then select **Add** to view the services for that category. Click the service name to open the details view, then you can view which pricing plans are available for that service.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to add visibility for. You can enable visibility of the service for more than
one organization by entering additional organization names or GUIDs in the command.</dd>
</dl>

**Tip:** You can also use **ba espv** as an alias for the longer
**ba edit-service-plan-visibility** command name.

### Working with service brokers

Use the following commands to list all service brokers, add or delete a service broker, or to update a service broker.

* You can list a service brokers by
entering the following command:

```
cf ba service-brokers <broker_name>
```
{: codeblock}

**Note**: To list all service brokers, enter the command without the `broker_name` parameter.

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">Optional: The name of the custom service broker. Use this parameter, if you want to get information for a specific service broker.</dd>
</dl>

**Tip:** You can also use **ba sb** as an alias for the longer
**ba service-brokers** command name.

* You can add a service broker, so that you can add a custom service to your  
{{site.data.keyword.Bluemix_notm}} Catalog by
entering the following command:

```
cf ba add-service-broker <broker_name> <user_name> <password> <broker_url>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">The name of the custom service broker.</dd>
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">The user name for the account that has access to the service broker.</dd>
<dt class="pt dlterm">&lt;password&gt;</dt>
<dd class="pd">The password for the account that has access to the service broker.</dd>
<dt class="pt dlterm">&lt;broker_url&gt;</dt>
<dd class="pd">The URL for the service broker.</dd>
</dl>

**Tip:** You can also use **ba asb** as an alias for the longer
**ba add-service-broker** command name.

* You can delete a service broker, to remove the custom service from your   
{{site.data.keyword.Bluemix_notm}} Catalog by
entering the following command:

```
cf ba delete-service-broker <service_broker>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;service_broker&gt;</dt>
<dd class="pd">The name or guid of the custom service broker.</dd>
</dl>

**Tip:** You can also use **ba dsb** as an alias for the longer
**ba delete-service-broker** command name.

* You can update a service broker by
entering the following command:

`cf ba update-service-broker <broker_name> <user_name> <password> <broker_url>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">The name of the custom service broker.</dd>
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">The user name for the account that has access to the service broker.</dd>
<dt class="pt dlterm">&lt;password&gt;</dt>
<dd class="pd">The password for the account that has access to the service broker.</dd>
<dt class="pt dlterm">&lt;broker_url&gt;</dt>
<dd class="pd">The URL for the service broker.</dd>
</dl>

**Tip:** You can also use **ba usb** as an alias for the longer
**ba update-service-broker** command name.
