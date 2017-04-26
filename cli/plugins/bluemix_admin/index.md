---

copyright:

  years: 2015, 2017

lastupdated: "2017-02-20"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} admin CLI
{: #bluemixadmincli}


You can manage your {{site.data.keyword.Bluemix_notm}} Local or {{site.data.keyword.Bluemix_notm}} Dedicated environment by using the Cloud Foundry command line interface with the {{site.data.keyword.Bluemix_notm}} Admin CLI plug-in. For example, you can add users from an LDAP registry. If you are looking for information about managing your {{site.data.keyword.Bluemix_notm}} Public account, see [Administering](/docs/admin/adminpublic.html#administer).

Before you begin, install the cf command line interface. The {{site.data.keyword.Bluemix_notm}} Admin CLI plug-in
requires cf version 6.11.2 or later. [Download Cloud Foundry command line interface ![External link icon](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}

**Restriction:** The Cloud Foundry command line interface is not supported by
Cygwin. Use the Cloud Foundry command line interface in a command line window other than the Cygwin
command line window.

**Note**: {{site.data.keyword.Bluemix_notm}} admin CLI is only used for {{site.data.keyword.Bluemix_notm}} Local and {{site.data.keyword.Bluemix_notm}} Dedicated environment. It is not supported by {{site.data.keyword.Bluemix_notm}} Public.

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
</li>
<li>To install the {{site.data.keyword.Bluemix_notm}} Admin CLI plug-in, run the following command:<br/><br/>
<code>
cf install-plugin BluemixAdminCLI -r BluemixAdmin
</code>
</li>
</ol>

If you need to uninstall the plug-in, you can use the following commands, then you can add the updated repository and install the latest plug-in:

* Uninstall the plug-in: `cf uninstall-plugin BluemixAdminCLI`
* Remove the plugin repository: `cf remove-plugin-repo BluemixAdmin`


## Using the {{site.data.keyword.Bluemix_notm}} Admin CLI plug-in

You can use the {{site.data.keyword.Bluemix_notm}} Admin CLI plug-in to add or remove users, assign or unassign users from orgs, and to perform other management tasks.

To see a list of commands, run the following
command:

```
cf plugins
```
{: codeblock}

For additional help for a command, use the `-help` option.

### Connecting and logging in to {{site.data.keyword.Bluemix_notm}}

Before you can use the Admin CLI plug-in, you must connect and log in, if
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

## Administering users
{: #admin_users}

### Adding a user
{: #admin_add_user}

To add a user to your {{site.data.keyword.Bluemix_notm}} environment from the
user registry for your environment, use the following command:

```
cf ba add-user <user_name> <organization> <first_name> <last_name>
```
{: codeblock}

**Note**: To add a user to a specific organization, you must be an **Admin** with the **users.write** (or **Superuser**) permission. If you are an organization manager, you can also be provided with the capability to add users to your organization by a Superuser who runs the **enable-managers-add-users** command.  See [Enabling managers to add users](index.html#clius_emau) for more information.

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">The name of the user in the LDAP registry.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to add the user to.</dd>
<dt class="pt dlterm">&lt;first_name&gt;</dt>
<dd class="pd">The first name of the user to be added to the organization.</dd>
<dt class="pt dlterm">&lt;last_name&gt;</dt>
<dd class="pd">The last name of the user to be added to the organization.</dd>
</dl>

**Tip:** You can also use **ba au** as an alias for the longer
**ba add-user** command name.

<!-- staging-only commands start. Live for interconnect -->

### Searching for a user
{: #admin_search_user}

To search for a user, use the following command in conjunction with the optional search filter parameters
(name, permission, organization, and role):

```
cf ba search-users -name=<user_name_value> -permission=<permission_value> -organization=<organization_value> -role=<role_value>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name_value&gt;</dt>
<dd class="pd">The name of the user in {{site.data.keyword.Bluemix_notm}}. </dd>
<dt class="pt dlterm">&lt;permission_value&gt;</dt>
<dd class="pd">The permission assigned to the user. For example, superuser, basic, catalog, user, and reports. For more information about assigned user permissions, see [Permissions](/docs/admin/index.html#permissions). You cannot use this parameter with the organization parameter in the same query. </dd>
<dt class="pt dlterm">&lt;organization_value&gt;</dt>
<dd class="pd">The organization name that the user belongs to. You cannot use this parameter with the permission parameter in the same query.</dd>
<dt class="pt dlterm">&lt;role_value&gt;</dt>
<dd class="pd">The organization role assigned to the user. For example, manager, billing manager, or auditor for the organization. You must specify the organization with this parameter. For more information about roles, see [User roles](/docs/admin/users_roles.html#userrolesinfo).</dd>

</dl>

**Tip:** You can also use **ba su** as an alias for the longer
**ba search-users** command name.

### Setting permissions for a user
{: #admin_setperm_user}

To set permissions for a specified user, use the following command:

```
cf ba set-permissions <user_name> <permission> <access>
```
{: codeblock}

**Note**: You can set one permission at a time.

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">The name of the user in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;permission&gt;</dt>
<dd class="pd">Set the permissions for the user: Admin (available alternative is Superuser), Login (available alternative is Basic), Catalog (read or write access), Reports (read or write access), or Users (read or write access).</dd>
<dt class="pt dlterm">&lt;access&gt;</dt>
<dd class="pd">For Catalog, Reports, or Users permissions, you must also set the level of access as <code>read</code> or <code>write</code>.</dd>
</dl>

**Tip:** You can also use **ba sp** as an alias for the longer
**ba set-permissions** command name.

<!-- staging-only commands end -->

### Removing a user
{: #admin_remov_user}

To remove a user from your {{site.data.keyword.Bluemix_notm}} environment, use the following command:

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

### Enabling managers to add users
{: #clius_emau}

If you have the **Superuser** permission in your {{site.data.keyword.Bluemix_notm}} environment, you can enable organization managers to add users to the organizations they manage. To enable managers to add users, use the following command:

```
cf ba enable-managers-add-users
```
{: codeblock}

**Tip:** You can also use **ba emau** as an alias for the longer
**ba enable-managers-add-users** command name.

### Disabling managers from adding users
{: #clius_dmau}

If organization managers have been enabled to add users to the organizations they manage in your {{site.data.keyword.Bluemix_notm}} environment with the **enable-managers-add-users** command, and if you have the **Superuser** permission, you can remove this setting.  To disable managers from adding users, use the following  command:

```
cf ba disable-managers-add-users
```
{: codeblock}

**Tip:** You can also use **ba dmau** as an alias for the longer
**ba disable-managers-add-users** command name.

## Administering organizations
{: #admin_orgs}

### Adding an organization
{: #admin_add_org}

To add an organization, use the following command:

```
cf ba create-org <organization> <manager>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to add.</dd>
<dt class="pt dlterm">&lt;manager&gt;</dt>
<dd class="pd">The user name of the manager for the org.</dd>
</dl>

**Tip:** You can also use **ba co** as an alias for the longer
**ba create-org** command name.

### Deleting an organization
{: #admin_delete_org}

To delete an organization, use the following command:

```
cf ba delete-org <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to delete.</dd>
</dl>

**Tip:** You can also use **ba do** as an alias for the longer
**ba delete-org** command name.

### Assigning a user to an organization
{: #admin_ass_user_org}

To assign a user in your {{site.data.keyword.Bluemix_notm}} environment to a
particular organization, use the following command:

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
<dd class="pd">See [Roles](/docs/admin/users_roles.html) for
{{site.data.keyword.Bluemix_notm}} user roles and
descriptions.</dd>
</dl>

**Tip:** You can also use **ba so** as an alias for the longer
**ba set-org** command name.

### Unassigning a user from an organization
{: #admin_unass_user_org}

To unassign a user in your {{site.data.keyword.Bluemix_notm}} environment from a
particular organization, use the following command:

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
<dd class="pd">See [Assigning roles](/docs/admin/users_roles.html) for
{{site.data.keyword.Bluemix_notm}} user roles and
descriptions.</dd>
</dl>

**Tip:** You can also use **ba uo** as an alias for the longer
**ba unset-org** command name.

#### Assigning roles

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
{: #admin_set_org_quota}

To set the usage quota for a particular organization, use the following command:

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


### Finding container quotas for an organization
{: #admin_find_containquotas}

To find the quota for containers for an organization, use the following command:

```
cf bluemix-admin containers-quota <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or ID of the organization in Bluemix. This parameter is required.</dd>
</dl>

**Tip:** You can also use **ba cq** as an alias for the longer
**bluemix-admin containers-quota** command name.

### Setting container quotas for an organization
{: #admin_set_containquotas}

To set the quota for containers in an organization, use the following command with at least one of the options included:

```
cf bluemix-admin set-containers-quota <organization> <options>
```
{: codeblock}

**Note**: You can include multiple options, but you must include at least one.

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or ID of the organization in Bluemix. This parameter is required.</dd>
<dt class="pt dlterm">&lt;options&gt;</dt>
<dd class="pd">Include one or more of the following options in which the value must be an integer:
<ul>
<li>floating-ips-max &lt;value&gt;</li>
<li>floating-ips-space-default &lt;value&gt;</li>
<li>memory-max &lt;value&gt;</li>
<li>memory-space-default &lt;value&gt;</li>
<li>image-limit &lt;value&gt;</li>
</ul>
</dd>
</dl>

**Tip:** You can also use the following short names as an alias for the longer
options names:
<dl class="parml">
<dt class="pt dlterm">floating-ips-max &lt;value&gt;</dt>
<dd class="pd"><strong>fim</strong></dd>
<dt class="pt dlterm">floating-ips-space-default &lt;value&gt;</dt>
<dd class="pd"><strong>fisd</strong></dd>
<dt class="pt dlterm">memory-max &lt;value&gt;</dt>
<dd class="pd"><strong>mm</strong></dd>
<dt class="pt dlterm">memory-space-default &lt;value&gt;</dt>
<dd class="pd"><strong>msd</strong></dd>
<dt class="pt dlterm">image-limit &lt;value&gt;</dt>
<dd class="pd"><strong>il</strong></dd>
</dl>

Optionally, you can provide a file containing specific configuration parameters in a valid JSON object. If you use the **-file** option, it takes precedence and the other options are ignored. To provide a file instead of setting the options, use the following command:

```
cf bluemix-admin set-containers-quota <organization> <-file path_to_JSON_file>
```
{: codeblock}

The JSON file should have the format shown in the following example:

```
{
  "floating_ips_max": 10,
  "floating_ips_space_default": 0,
  "ram_max": 4096,
  "ram_space_default": 0,
  "image_limit": 10
}
```
{: codeblock}

**Tip:** You can also use **ba scq** as an alias for the longer
**bluemix-admin set-containers-quota** command name.

## Administering spaces
{: #admin_spaces}

### Adding a space to the organization

To add a space in the organization, use the following command:

```
cf bluemix-admin create-space <organization> <space_name>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the organization that the space is to be added to.</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">The name of the space that is to be created in the organization.</dd>
</dl>

**Tip:** You can also use **ba cs** as an alias for the longer
**ba create-space** command name.

### Deleting a space from the organization

To remove a space from the organization, use the following command:

```
cf bluemix-admin delete-space <organization> <space_name>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the organization that the space is to be removed from.</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">The name of the space that is to be removed from the organization.</dd>
</dl>

**Tip:** You can also use **ba cs** as an alias for the longer
**ba delete-space** command name.

### Adding a user to a space with a role

To create a user in a space with a specified role, use the following command:

```
cf bluemix-admin set-space <organization> <space_name> <user_name> <role>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the organization that the user is to be added to.</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">The name of the space that the user is to be added to.</dd>
<dt class="pt dlterm">&lt;user_anme&gt;</dt>
<dd class="pd">The name of the user that is to be added.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">The role of the user that is to be assigned. The value can be Manager, Developer, or Auditor. See [Assigning roles](/docs/admin/users_roles.html) for
{{site.data.keyword.Bluemix_notm}} user roles and
descriptions in a space.</dd>
</dl>

**Tip:** You can also use **ba ss** as an alias for the longer
**ba set-space** command name.


### Removing the role of a user in a space 

To remove the role of a user in a space, use the following command:

```
cf bluemix-admin unset-space <organization> <space_name> <user_name> <role>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the organization that the user is to be added to.</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">The name of the space that the user is to be added to.</dd>
<dt class="pt dlterm">&lt;user_anme&gt;</dt>
<dd class="pd">The name of the user that is to be added.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">The role of the user that is to be assigned. The value can be Manager, Developer, or Auditor. See [Assigning roles](/docs/admin/users_roles.html) for
{{site.data.keyword.Bluemix_notm}} user roles and
descriptions in a space.</dd>
</dl>

**Tip:** You can also use **ba us** as an alias for the longer
**ba unset-space** command name.

## Administering catalog
{: #admin_catalog}

### Enabling services for all organizations
{: #admin_ena_service_org}

To enable a service to be displayed in the
{{site.data.keyword.Bluemix_notm}} Catalog for all
organizations, use the following command:

```
cf ba enable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">The name or GUID of the service plan that you want to enable. If you enter a non-unique service plan name, for example "Standard" or "Basic," you are prompted with service plans that  to choose from. To identify a service plan name,  select the service category from the homepage, then select **Add** to view the services for that category. Click the service name to open the details view, then you can view the names of the service plans that are available for that service. </dd>
</dl>

**Tip:** You can also use **ba esp** as an alias for the longer
**ba enable-service-plan** command name.

### Disabling services for all organizations
{: #admin_dis_service_org}

To disable a service from being visible in the {{site.data.keyword.Bluemix_notm}} Catalog for all
organizations, use the following command:

```
cf ba disable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">The name or GUID of the service plan that you want to enable. If you enter a non-unique service plan name, for example "Standard" or "Basic," you are prompted with service plans that  to choose from. To identify a service plan name, select the service category from the homepage, then select **Add** to view the services for that category. Click the service name to open the details view, then you can view the names of the service plans that are available for that service.</dd>
</dl>

**Tip:** You can also use **ba dsp** as an alias for the longer
**ba disable-service-plan** command name.

### Adding service visibility for organizations
{: #admin_addvis_service_org}

You can add an organization from the list of organizations that can see a specific service in the {{site.data.keyword.Bluemix_notm}} Catalog. To allow an organization to view a specific service in the
{{site.data.keyword.Bluemix_notm}} Catalog, use the following command:

```
cf ba add-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">The name or GUID of the service plan that you want to enable. If you enter a non-unique service plan name, for example "Standard" or "Basic," you are prompted with service plans that  to choose from. To identify a service plan name, select the service category from the homepage, then select **Add** to view the services for that category. Click the service name to open the details view, then you can view the names of the service plans that are available for that service.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to add to the service's visibility list.</dd>
</dl>

**Tip:** You can also use **ba aspv** as an alias for the longer
**ba add-service-plan-visibility** command name.

### Removing service visibility for organizations
{: #admin_remvis_service_org}

You can remove an organization from the list of organizations that can see a
specific service in the {{site.data.keyword.Bluemix_notm}} Catalog. To remove the visibility of a service in the
{{site.data.keyword.Bluemix_notm}} Catalog for an
organization, use the following command:

```
cf ba remove-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">TThe name or GUID of the service plan that you want to enable. If you enter a non-unique service plan name, for example "Standard" or "Basic," you are prompted with service plans that  to choose from. To identify a service plan name, select the service category from the homepage, then select **Add** to view the services for that category. Click the service name to open the details view, then you can view the names of the service plans that are available for that service.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to remove from the service's visibility list.</dd>
</dl>

**Tip:** You can also use **ba rspv** as an alias for the longer
**ba remove-service-plan-visibility** command name.

### Editing service visibility for organizations
{: #admin_editvis_service_org}

You can edit and replace the list of services that specific
organizations can see in the {{site.data.keyword.Bluemix_notm}} Catalog. To replace all existing visible services for an organization or multiple organizations, use the
following command:

```
cf ba edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>
```
{: codeblock}

**Note:** This command replaces existing visible services for the specified organizations with the service that you specify in the command.

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">The name or GUID of the service plan that you want to enable. If you enter a non-unique service plan name, for example "Standard" or "Basic," you are prompted with service plans that  to choose from. To identify a service plan name, select the service category from the homepage, then select **Add** to view the services for that category. Click the service name to open the details view, then you can view the names of the service plans that are available for that service.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to add visibility for. You can enable visibility of the service for more than
one organization by entering additional organization names or GUIDs in the command.</dd>
</dl>

**Tip:** You can also use **ba espv** as an alias for the longer
**ba edit-service-plan-visibility** command name.

## Administering reports
{: #admin_add_report}

### Adding reports
{: #admin_add_report}

To add a security report, use the following command:

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

### Deleting reports
{: #admin_del_report}

To delete a security report, use the following command:

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

### Retrieving reports
{: #admin_retr_report}

To retrieve a security report, use the following command:

```
cf ba retrieve-report <search>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;search&gt;</dt>
<dd class="pd">The filename of the report. If there is a space in the name, use quotation marks around the
name.</dd>
</dl>

**Tip:** You can also use **ba rr** as an alias for the longer **ba retrieve-report** command name.

## Viewing resource metric information
{: #cliresourceusage}

You can view resource metric information, including memory, disk, and CPU usage. You can see a summary of the available physical and reserved resources as well as the usage of physical and reserved resources. You can also see droplet execution agents (DEAs) and cells (Diego architecture) usage data and historical memory and disk usage. Historical data for memory and disk usage is displayed, by default, weekly and in descending order. To view the resource metric information, use the following command:

```
cf ba resource-metrics <monthly> <weekly>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;monthly&gt;</dt>
<dd class="pd">View the historical data for memory and disk space a month at a time.</dd>
<dt class="pt dlterm">&lt;weekly&gt;</dt>
<dd class="pd">View the historical data for memory and disk space a week at a time. This is the default value.</dd>
</dl>

**Tip:** You can also use **ba rsm** as an alias for the longer
**ba resource-metrics** command name.


## Administering service brokers
{: #admin_servbro}

### Listing service brokers
{: #clilistservbro}

To list service all brokers, use the following command:

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

### Adding a service broker
{: #cliaddservbro}

To add a service broker, so that you can add a custom service to your
{{site.data.keyword.Bluemix_notm}} Catalog, use the following command:

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

### Deleting a service broker
{: #clidelservbro}

To delete a service broker, to remove the custom service from your
{{site.data.keyword.Bluemix_notm}} Catalog, use the following command:

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

### Updating a service broker
{: #cliupdservbro}

To update a service broker use the following command:

```
cf ba update-service-broker <broker_name> <user_name> <password> <broker_url>
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

**Tip:** You can also use **ba usb** as an alias for the longer
**ba update-service-broker** command name.


## Administering application security groups
{: #admin_secgro}

To work with application security groups (ASGs), you must be a full access administrator for the local or dedicated environment. All users of the environment can list the available ASGs for the organization that is being targeted with the command. However, to create, update, or bind ASGs, you must be an administrator for the {{site.data.keyword.Bluemix_notm}} environment.

ASGs function as virtual firewalls that control outbound traffic from the applications in your {{site.data.keyword.Bluemix_notm}} environment. Each ASG consists of a list of rules that allow specific traffic and communication to and from the outside network. You can bind one or more ASGs to a specific security group set, for example a group set that is used for applying global access, or you can bind to spaces within an organization in your {{site.data.keyword.Bluemix_notm}} environment.

{{site.data.keyword.Bluemix_notm}} is initially set up with all access to the outside network restricted. Two IBM-created  security groups, `public_networks` and `dns`, enable global access to the outside network when you bind these groups to default Cloud Foundry security group sets. The two security group sets in Cloud Foundry that are used to apply global access are the **Default Staging** and **Default Running** group sets. These group sets apply the rules for allowing traffic to all running apps or all staging apps. If you do not want to bind to these two security group sets, you can unbind from the Cloud Foundry group sets, and then bind the security group to a specific space. For more information, see [Binding Application Security Groups ![External link icon](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window}.

**Note**: The following commands that enable you to work with security groups are based on the Cloud Foundry 1.6 version. For more information, including required and optional fields, see the Cloud Foundry information about [Creating Application Security Groups ![External link icon](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#creating-groups){: new_window}.

### Listing security groups
{: #clilissecgro}

* To list all security groups, use the following command:

```
cf ba security-groups
```
{: codeblock}

**Tip:** You can also use **ba sgs** as an alias for the longer
**ba security-groups** command name.

* To display details for a specific security group, use the following command:

```
cf ba security-groups <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">Name of the security group</dd>
</dl>

**Tip:** You can also use **ba sg** as an alias for the longer
**ba security-groups** command name with the `security-group` parameter.


### Creating a security group
{: #clicreasecgro}

For more information about creating security groups and the rules that define outgoing traffic, see [Creating Application Security Groups ![External link icon](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#creating-groups){: new_window}.

To create a security group, use the following command:

```
cf ba create-security-group <security-group> <path-to-rules-file>
```
{: codeblock}

Each security group that you create has the prefix `adminconsole_` added to the name to distinguish it from the IBM-created security groups.

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">Name of your security group</dd>
<dt class="pt dlterm">&lt;Path to rules file&gt;</dt>
<dd class="pd">Absolute or relative path to a rules file</dd>
</dl>

**Tip:** You can also use **ba csg** as an alias for the longer
**ba create-security-group** command name.

### Updating a security group
{: #cliupdsecgro}

To update a security group, use the following command:

```
cf ba update-security-group <security-group> <path-to-rules-file>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">Name of your security group</dd>
<dt class="pt dlterm">&lt;Path to rules file&gt;</dt>
<dd class="pd">Absolute or relative path to a rules file</dd>
</dl>

**Tip:** You can also use **ba usg** as an alias for the longer
**ba update-security-group** command name.

### Deleting a security group
{: #clidelsecgro}

To delete a security group, use the following command:

```
cf ba delete-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">Name of your security group</dd>
</dl>

**Tip:** You can also use **ba dsg** as an alias for the longer
**ba delete-security-group** command name.


### Binding security groups
{: #clibindsecgro}

For more information about binding security groups, see [Binding Application Security Groups ![External link icon](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window}.

* To bind to the Default Staging security group set, use the following command:

```
cf ba bind-staging-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">Name of your security group</dd>
</dl>

**Tip:** You can also use **ba bssg** as an alias for the longer
**ba bind-staging-security-group** command name.

* To bind to the Default Running security group set, use the following command:

```
cf ba bind-running-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">Name of your security group</dd>
</dl>

**Tip:** You can also use **ba brsg** as an alias for the longer
**ba bind-running-security-group** command name.

* To bind a security group to a space, use the following command:

```
cf ba bind-security-group <security-group> <org> <space>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">Name of your security group</dd>
<dt class="pt dlterm">&lt;Org&gt;</dt>
<dd class="pd">Name of the organization to bind the security group to</dd>
<dt class="pt dlterm">&lt;Space&gt;</dt>
<dd class="pd">Name of the space within the organization to bind the security group to</dd>
</dl>

**Tip:** You can also use **ba bsg** as an alias for the longer
**ba bind-security-group** command name.

### Unbinding security groups
{: #cliunbindsecgro}

For more information about unbinding security groups, see [Unbinding Application Security Groups ![External link icon](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#unbinding-groups){: new_window}.

* To unbind from a Default Staging security group set, use the following command:

```
cf ba unbind-staging-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">Name of your security group</dd>
</dl>

**Tip:** You can also use **ba ussg** as an alias for the longer
**ba unbind-staging-security-group** command name.

* To unbind from a Default Running security group set, use the following command:

```
cf ba unbind-running-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">Name of your security group</dd>
</dl>

**Tip:** You can also use **ba brsg** as an alias for the longer
**ba bind-running-security-group** command name.

* To unbind a security group to a space, use the following command:

```
cf ba unbind-security-group <security-group> <org> <space>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">Name of your security group</dd>
<dt class="pt dlterm">&lt;Org&gt;</dt>
<dd class="pd">Name of the organization to bind the security group to</dd>
<dt class="pt dlterm">&lt;Space&gt;</dt>
<dd class="pd">Name of the space within the organization to bind the security group to</dd>
</dl>

**Tip:** You can also use **ba usg** as an alias for the longer
**ba unbind-staging-security-group** command name.

## Administering buildpacks
{: #admin_buildpack}

### Listing buildpacks
{: #clilistbuildpack}

If you have the apps catalog write permissions, you can list buildpacks. To list all buildpacks or view a specific buildpack, use the following command:

```
cf ba buildpacks <buildpack_name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">An optional parameter to specify a particular buildpack to view.</dd>
</dl>

**Tip:** You can also use **ba lb** as an alias for the longer
**ba buildpacks** command name.

### Creating and uploading a buildpack
{: #clicreupbuildpack}

If you have the apps catalog write permissions, you can create and upload a buildpack. You can upload any compressed file that has a .zip file type. To upload a buildpack, use the following command:

```
cf ba create-buildpack <buildpack_name> <file_path> <position>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">The name of the buildpack to upload.</dd>
<dt class="pt dlterm">&lt;file_path&gt;</dt>
<dd class="pd">The path to the buildpack compressed file.</dd>
<dt class="pt dlterm">&lt;position&gt;</dt>
<dd class="pd">The order in which the buildpacks are checked during buildpack auto-detection.</dd>
</dl>

**Tip:** You can also use **ba cb** as an alias for the longer
**ba create-buildpack** command name.

### Updating a buildpack
{: #cliupdabuildpack}

If you have the apps catalog write permissions, you can update an existing buildpack.  To update a buildpack, use the following command:

```
cf ba update-buildpack <buildpack_name> <position> <enabled> <locked>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">The name of the buildpack to update.</dd>
<dt class="pt dlterm">&lt;position&gt;</dt>
<dd class="pd">The order in which the buildpacks are checked during buildpack auto-detection.</dd>
<dt class="pt dlterm">&lt;enabled&gt;</dt>
<dd class="pd">Indicates whether the buildpack is used for staging.</dd>
<dt class="pt dlterm">&lt;locked&gt;</dt>
<dd class="pd">Indicates whether the buildpack is locked to prevent updates.</dd>
</dl>

**Tip:** You can also use **ba ub** as an alias for the longer
**ba update-buildpack** command name.

### Deleting a buildpack
{: #clidelbuildpack}

If you have the apps catalog write permissions, you can delete an existing buildpack.  To delete a buildpack, use the following command:

```
cf ba delete-buildpack <buildpack_name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">The name of the buildpack to delete.</dd>
</dl>

**Tip:** You can also use **ba db** as an alias for the longer
**ba delete-buildpack** command name.
