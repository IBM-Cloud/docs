# {{site.data.keyword.Bluemix_notm}} admin
{: #bluemixadmincli}

You can manage users for your
{{site.data.keyword.Bluemix_notm}} Local or {{site.data.keyword.Bluemix_notm}} Dedicated environment by
using the Cloud Foundry command line interface with the
{{site.data.keyword.Bluemix_notm}} Admin CLI plug-in. For
example, you can add users from an LDAP registry. If you are looking for information about managing your {{site.data.keyword.Bluemix_notm}} Public account, see [Managing your account](../admin/index.html#mngacct).

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

## Using the {{site.data.keyword.Bluemix_notm}} Admin CLI plug-in

You can use the {{site.data.keyword.Bluemix_notm}} Admin CLI plug-in to add or remove users, assign or unassign users from orgs, and to perform other management tasks. To see a list of commands, run the following
command:

`cf plugins`
{: codeblock}

For additional help for a command, use the `-help` option.

### Connecting and logging in to {{site.data.keyword.Bluemix_notm}}

Before you can use the Admin CLI plug-in to manage users, you must connect and log in, if
you are not already.

<ol>
<li>To connect to the {{site.data.keyword.Bluemix_notm}}> API endpoint, run the following command:<br/><br/>
<code>
cf bluemix-admin-api https://api.&lt;subdomain&gt;.bluemix.net
</code>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">Subdomain of the URL for your {{site.data.keyword.Bluemix_notm}} instance.<br />
<p>**Tip:** You can also use **baa** as an alias for the longer
**bluemix-admin-api** command name.</dd>
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

`cf bluemix-admin-add-user <user_name> <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">The name of the user in the LDAP registry.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to add the user to.</dd>
</dl>

**Tip:** You can also use **baau** as an alias for the longer
**bluemix-admin-add-user** command name.

### Removing a user

You can remove a user from your
{{site.data.keyword.Bluemix_notm}} environment by
entering the following command:

`cf bluemix-admin-remove-user <user_name>`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">The name of the user in {{site.data.keyword.Bluemix_notm}}.</dd>

</dl>

**Tip:** You can also use **baru** as an alias for the longer
**bluemix-admin-remove-user** command name.

### Adding and deleting an organization

You can add and delete an organization.

* To add an organization, enter the following command:

`cf bluemix-admin-create-organization <organization> <manager>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to add.</dd>
<dt class="pt dlterm">&lt;manager&gt;</dt>
<dd class="pd">The user name of the manager for the org.</dd>
</dl>

**Tip:** You can also use **baco** as an alias for the longer
**bluemix-admin-create-organization** command name.

* To delete an organization, enter the following command:

`cf bluemix-admin-delete-organization <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to delete.</dd>
</dl>

**Tip:** You can also use **bado** as an alias for the longer
**bluemix-admin-create-organization** command name.

### Assigning a user to an organization

You can assign a user in your
{{site.data.keyword.Bluemix_notm}} environment to a
particular organization. Enter the following command:

`cf bluemix-admin-set-org <user_name> <organization> [<role>]`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">The name of the user in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to assign the user to.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">See [Roles](#roles) for
{{site.data.keyword.Bluemix_notm}} user roles and
descriptions.</dd>
</dl>

**Tip:** You can also use **baso** as an alias for the longer
**bluemix-admin-set-org** command name.

### Unassigning a user from an organization

You can unassign a user in your
{{site.data.keyword.Bluemix_notm}} environment from a
particular organization. Enter the following command:

`cf bluemix-admin-unset-org <user_name> <organization> [<role>]`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">The name of the user in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to assign the user to.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">See [Roles](#roles) for
{{site.data.keyword.Bluemix_notm}} user roles and
descriptions.</dd>
</dl>

**Tip:** You can also use **bauo** as an alias for the longer
**bluemix-admin-unset-org** command name.

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

`cf bluemix-admin-set-quota <organization> <plan>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to set the quota for.</dd>
<dt class="pt dlterm">&lt;plan&gt;</dt>
<dd class="pd">The quota plan for an organization.</dd>
</dl>

**Tip:** You can also use **basq** as an alias for the longer
**bluemix-admin-set-quota** command name.

### Adding, deleting, and retrieving reports

You can add, delete, and retrieve security reports.
* To add a report, enter the following command:

`cf bluemix-admin-add-report <category> <date> <PDF|TXT|LOG> <RTF>`
{: codeblock}

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

**Tip:** You can also use **baar** as an alias for the longer
**bluemix-admin-add-report** command name.

* To delete a report, enter the following command:

`cf bluemix-admin-delete-report <category> <date> <name>`
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

**Tip:** You can also use **badr** as an alias for the longer
**bluemix-admin-delete-report** command name.

* To retrieve a report, enter the following command:

`cf bluemix-admin-retrieve-report <category> <date> <name>`
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

**Tip:** You can also use **barr** as an alias for the longer **bluemix-admin-retrieve-report** command name.

### Enabling and disabling services for all organizations

You can enable or disable a service from being displayed in the
{{site.data.keyword.Bluemix_notm}} Catalog for all organizations.

* To enable a service to be visible in the
{{site.data.keyword.Bluemix_notm}} Catalog for all
organizations, enter the following command:

`cf bluemix-admin-enable-service-plan <plan_identifier>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">The name or GUID of the service that you want to enable. If you enter a non-unique service name,
you are prompted with service plans to choose from.</dd>
</dl>

**Tip:** You can also use **baesp** as an alias for the longer
**bluemix-admin-enable-service-plan** command name.

* To disable a service from being visible in the
{{site.data.keyword.Bluemix_notm}} Catalog for all
organizations, enter the following command:

`cf bluemix-admin-disable-service-plan <plan_identifier>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">The name or GUID of the service that you want to disable. If you enter a non-unique service
name, you are prompted with service plans to choose from.</dd>
</dl>

**Tip:** You can also use **badsp** as an alias for the longer
**bluemix-admin-disable-service-plan** command name.

### Adding, removing, and editing service visibility for organizations

You can add or remove an organization from the list of organizations that can see a
specific service in the {{site.data.keyword.Bluemix_notm}} Catalog. You can also edit and replace the list of services that specific
organizations can see in the {{site.data.keyword.Bluemix_notm}} Catalog.

* To allow an organization to view a specific service in the
{{site.data.keyword.Bluemix_notm}} Catalog, enter the
following command:

`cf bluemix-admin-add-service-plan-visibility <plan_identifier> <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">The name or GUID of the service that you want to add visibility for. If you enter a non-unique
service name, you are prompted with service plans to choose from.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to add to the service's visibility list.</dd>
</dl>

**Tip:** You can also use **baaspv** as an alias for the longer
**bluemix-admin-add-service-plan-visibility** command name.

* To remove the visibility of a service in the
{{site.data.keyword.Bluemix_notm}} Catalog for an
organization, enter the following command:

`cf bluemix-admin-remove-service-plan-visibility <plan_identifier> <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">The name or GUID of the service that you want to remove visibility for. If you enter a
non-unique service name, you are prompted with service plans to choose from.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to remove from the service's visibility list.</dd>
</dl>

**Tip:** You can also use **barspv** as an alias for the longer
**bluemix-admin-remove-service-plan-visibility** command name.

* To replace all existing visible services for an organization or multiple organizations, use the
following command:

`cf bluemix-admin-edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>`
{: codeblock}

**Note:** This
command replaces existing visible services for the specified organizations with the service that you
specify in the command.

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">The name or GUID of the service that you want to make visible. If you enter a non-unique service
name, you are prompted with service plans to choose from.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">The name or GUID of the {{site.data.keyword.Bluemix_notm}} org to add visibility for. You can enable visibility of the service for more than
one organization by entering additional organization names or GUIDs in the command.</dd>
</dl>

**Tip:** You can also use **baespv** as an alias for the longer
**bluemix-admin-edit-service-plan-visibility** command name.
