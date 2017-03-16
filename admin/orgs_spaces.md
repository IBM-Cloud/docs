---



copyright:

  years: 2015, 2016
lastupdated: "2016-12-05"  


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Managing organizations and spaces
{: #orgsspacesusers}

As an account owner, you can manage your organizations by going to the **Manage Organizations** page. Organization managers can also use the Manage Organizations page to manage any organizations where they are set as the manager.
{:shortdesc}

Management tasks include the following:

* Creating an organization or space
* Renaming an organization
* Deleting an existing organization or space
* Listing the team members added to your account or organization
* Managing or viewing the quota
* Managing custom domains

**Note**: You must be the account owner of a Pay-As-You-Go account to create an organization.

## Organizations
{: #orginfo}

Organizations can span multiple regions, and they are defined by the following items:

<dl>
<dt>Team members</dt>
<dd>The role with basic permission in organizations and spaces. You must be assigned to an organization before you can be granted other permissions to the spaces within the organization. For detailed information, see [Users and roles](users_roles.html#userrolesinfo).</dd>
<dt>Domains</dt>
<dd>Provide the route on the internet that is allocated to the organization. A route has a sub-domain and a domain. A sub-domain is typically the application name. A domain might be a system domain, or a custom domain that you registered for your application. See [Managing custom domains](orgs_spaces.html#managedomains).<br/>
<p>**Note**: If you add a custom domain, you must configure your DNS server to resolve your custom domain to point to the {{site.data.keyword.Bluemix_notm}} system domain. In this way, when {{site.data.keyword.Bluemix_notm}} receives a request for your custom domain, it can properly route it to your application.</p></dd>
<dt>Quota</dt>
<dd>Represents the resource limits for the organization, including the number of services and the amount of memory that can be allocated for use by the organization. Quotas are assigned when organizations are created. Any application or service in a space of the organization contributes to the usage of the quota. The quota is not an enforced cap. Instead, it is a trigger for spending notifications. With the Pay-As-You-Go or Subscription plans, you can adjust your quota for Cloud Foundry applications and containers as the needs of your organization change. See [Managing quota](orgs_spaces.html#managequota).</dd>
</dl>

In {{site.data.keyword.Bluemix_notm}}, you can use organizations to enable collaboration among team members and to facilitate the logical grouping of project resources in the following ways:

<ul>
<li>You can group a set of spaces, applications, services, domains, routes, and team members together in organizations.</li>
<li>You can manage the access to the spaces and organizations on a per-user basis.</li>
</ul>

When you create an organization, the organization name must be unique in {{site.data.keyword.Bluemix_notm}}. If the organization name is already in use by another {{site.data.keyword.Bluemix_notm}} Public, Dedicated, or Local user, then you must specify a new name. After you create the organization, you will be automatically assigned the *Organization Manager* permission, which enables you to edit the organization name, add team members, and create or delete spaces in the organization.

You must contact [{{site.data.keyword.Bluemix_notm}} Support ![External link icon](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window} to delete an organization. When you request for the support team to delete an organization, all the spaces, applications, and services within the organization are deleted.

The following [user roles](/docs/admin/users_roles.html#userrolesinfo) can be assigned to team members in an organization:

<ul>
<li>Organization manager</li>
<li>Organization billing manager</li>
<li>Organization auditor</li>
</ul>

<!-- Add info on Manage infrastructure option under a space -->

## Spaces
{: #spaceinfo}

Within an organization, you can use spaces to group a set of applications, services, and team members. Spaces are tied to a specific region in {{site.data.keyword.Bluemix_notm}}.

After you add team members to an organization, you can grant them permissions to the spaces. Similar to organizations, spaces also have a set of [user roles](/docs/admin/users_roles.html#userrolesinfo) with specific permissions that are assigned to team members:

<ul>
<li>Space manager</li>
<li>Space developer</li>
<li>Space auditor</li>
</ul>

**Note**: A team member must be assigned at least one of the permissions in the space.

## Creating orgs and spaces
{: #createorg}

Only account owners with Pay-As-You-Go accounts can create an organization. You can create an organization by completing the following steps:

1. Click **Account** &gt; **Manage Organizations** page.
2. Click **Add a New Org**.
3. Enter the org name.
4. Click **Add**.

You can create spaces in your organization; for example, a *dev* space as a development environment, a *test* space as a testing environment, and a *production* space as a production environment. Then, you can associate your apps with spaces. Complete the following steps to create a space:

1. Click **Account** &gt; **Manage Organizations** page.
2. Identify the org that you want to add a space to, and select **View Details**.
4. Click **Add a Space**.
5. Enter the space name.
6. Click **Add**.

## Renaming an organization
{: #orgrename}

Complete the following steps to rename your organization:

1. Click **Account** &gt; **Manage Organizations** page.
2. Identify the org that you want to edit, and select **View Details**.
3. Select **Edit Org**.
4. Select **Edit** for the title of the org.
5. Type the new org name.
6. Click **SAVE**.

## Deleting an existing org or space
{: #deleteorgs}

As the account owner, you can contact [{{site.data.keyword.Bluemix_notm}} Support ![External link icon](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window} to delete an organization. 

**Note**: Deleting operations cannot be reversed. You lose all your applications and services that are associated with the organization.

You can delete a space from the **Manage Organizations** page:

1. Click **Account** &gt; **Manage Organizations** page.
2. Identify the org that you want to edit, and select **View Details**.
3. Identify the space that you want to delete, and select **Edit Space**.
4. Click **Delete Space**.

## Listing members
{: #listmembers}

Complete the following steps to list the members for a specific organization:

1. Click **Account** &gt; **Manage Organizations** page.
2. Identify the organization that you want to view the members for, and click **View Details**.
3. Click **Edit Org**.
4. You can see the members of your organization and their roles in the **USERS** tab.

Complete the following steps to list the members for a specific space:

1. Click **Account** &gt; **Manage Organizations** page.
2. Identify the organization that you want to view the members for, and click **View Details**.
3. Identify the space that you want to view the members for, and click **Edit Space**.
4. You can see the members of your space and their roles in the **USERS** tab.

## Managing quota
{: #managequota}

As a {{site.data.keyword.Bluemix_notm}} account owner or organization manager, you can view the used and allocated quota for an  organization. The quota represents the resource limits for the organization, which is assigned when the organization is created. The limit is not a cap that is enforced against the org. Instead, it is a trigger for spending notifications. Depending on whether you have a trial account or a billable account, the resources that are available to an organization vary. Any application or service in a space within the organization contributes to the usage of the allocated quota.

To view the used and allocated quota for an organization, complete the following steps:

1. Click **Account** &gt; **Manage Organizations** page.
2. Identify the organization that you want to view the quota for, and click **View Details**.
3. Click **Edit Org**.
4. If you have spaces defined in more than one region, select the specific region that you want to view.
5. Click **QUOTA**. 
6. By default, the **Cloud Foundry** quota page opens. You can view the quota details for the following resources:
 * MEMORY
 * SERVICES
 * PLAN
 * PRICE
7. Click **Containers** to view the used and available container quota allocation. The container allocation varies depending on your pricing plan. You can view the quota details for the following resources:
 * MEMORY
 * PUBLIC IP

**Note:** Containers are not available in the {{site.data.keyword.Bluemix_notm}} Sydney region. 

For more information about containers, see [Quota](/docs/containers/container_planning_org_ov.html#container_planning_quota) in the Containers documentation.
To change the quota that is allocated to an organization, you must open a support ticket. For more information about opening a support ticket, see [Getting customer support](/docs/support/index.html#contacting-support). 

## Managing domains
{: #managedomains}

As an account owner or organization manager, you can view the system domain and add custom domains for applications that are built within an organization and its spaces. As a space manager, the **Domains** tab for a space is a read-only list of the domains that are assigned to the space. 

1. Click **Account** &gt; **Manage Organizations** page.
2. Identify the org that you want to view or edits domains for.
3. Select **View Details** for that org.
4. Click **Edit Org**.
5. Click **DOMAINS**.

If you add a custom domain, you must configure your DNS server to resolve your custom domain to point to the {{site.data.keyword.Bluemix_notm}} system domain. In this way, when {{site.data.keyword.Bluemix_notm}} receives a request for your custom domain, it can properly route it to your application. The system domain is always available to a space, and custom domains might also be allocated to a space. Applications created in a space might use any of domains listed for that space. For more information about creating and using custom domains, see [Using a custom domain](/docs/manageapps/updapps.html#domain).
