---

copyright:

  years: 2015, 2017
lastupdated: "2017-04-11"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Managing organizations
As an account owner or an organization manager, you can perform org management tasks, including renaming your org, deleting an org or space, updating org or space roles, and managing quota and domains.
{:shortdesc}

From the console menu bar, click **Manage > Account > Organizations** to manage your orgs. 

**Note:** You can view resources of only one organization at a time. If you are a member of multiple organizations, you can switch organizations from the user account preferences link in the console menu bar.

## Renaming orgs
{: #orgrename}

Complete the following steps to rename your organization:
1. Click **Manage** > **Account** > **Organizations**.
2. Identify the org that you want to rename, and click **View Details**.
3. Click **Edit Org**.
4. Click **Edit** next to the name of the org.
5. Type the new org name, and click **Save**.

## Deleting orgs and spaces
{: #deleteorgs}

As the account owner, contact [{{site.data.keyword.Bluemix_notm}} Support ![External link icon](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window} to delete an organization.

**Note**: Deleting operations cannot be reversed. You lose all your apps and services that are associated with the org.

Complete the following steps to delete an org or space:
1. Click **Manage** > **Account** > **Organizations**.
2. Identify the org that you want to edit, and click **View Details**.
3. Identify the space that you want to delete, and click **Edit Space**.
4. Click **Delete Space**.

## Editing user roles
{: #listmembers}

Complete the following steps to edit the users roles for a specific org:
1. Click **Manage** &gt; **Account** &gt; **Organizations**.
2. Identify the organization that you want to view the members for, and click **View Details**.
3. Click **Edit Org**.
4. You can see the members of your organization and their roles in the **USERS** tab.

Complete the following steps to edit the user roles for a specific space:
1. Click **Manage** &gt; **Account** &gt; **Organizations**.
2. Identify the organization that you want to view the members for, and click **View Details**.
3. Identify the space that you want to view the members for, and click **Edit Space**.
4. You can see the members of your space and their roles in the **USERS** tab.

## Managing quota
{: #managequota}

As a {{site.data.keyword.Bluemix_notm}} account owner or organization manager, you can view the used and allocated quota for an organization. The quota represents the resource limits for the organization, which is assigned when the organization is created. Depending on whether you have a trial account or a billable account, the resources that are available to an organization vary. Any application or service in a space within the organization contributes to the usage of the allocated quota.

To view the used and allocated quota for an org, complete the following steps:
1. Click **Manage** &gt; **Account** &gt; **Organizations**.
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
 * FILE SHARES
8. Click **Virtual Servers** to view the virtual machines.

**Note:** Containers are not available in the {{site.data.keyword.Bluemix_notm}} Sydney region. 

For more information about containers, see [Quota](/docs/containers/container_planning.html#container_planning_quota) in the Containers documentation.
To change the quota that is allocated to an organization, you must open a support ticket. For more information about opening a support ticket, see [Getting customer support](/docs/support/index.html#contacting-support). 

## Managing domains
{: #managedomains}

As an account owner or organization manager, you can view the system domain and add custom domains for applications that are built within an organization and its spaces. As a space manager, the **Domains** tab for a space is a read-only list of the domains that are assigned to the space.

1. Click **Manage** &gt; **Account** &gt; **Organizations**.
2. Identify the organization that you want to view or edits domains for.
3. Select **View Details** for that org.
4. Click **Edit Org**.
5. Click **DOMAINS**.

If you add a custom domain, you must configure your DNS server to resolve your custom domain to point to the {{site.data.keyword.Bluemix_notm}} system domain. In this way, when {{site.data.keyword.Bluemix_notm}} receives a request for your custom domain, it can properly route it to your app. The system domain is always available to a space, and custom domains might also be allocated to a space. Apps created in a space might use any of domains listed for that space. For more information about creating and using custom domains, see [Using a custom domain](/docs/manageapps/updapps.html#domain).
