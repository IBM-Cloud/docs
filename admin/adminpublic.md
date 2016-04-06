---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Administering
{: #administer}
*Last updated: 29 February 2016*

Manage your orgs, spaces, and assigned users by clicking the **Account and Support** icon ![Account and Support](../support/images/account_support.svg), then select **Manage Organizations**. If you are a {{site.data.keyword.Bluemix_notm}} Local or {{site.data.keyword.Bluemix_notm}} Dedicated user, see [Managing {{site.data.keyword.Bluemix_notm}} Local and {{site.data.keyword.Bluemix_notm}} Dedicated](../admin/index.html#mng) for more information about administering your local or dedicated instance.
{:shortdesc}

## Managing {{site.data.keyword.Bluemix_notm}} Public
{: #mngacct}

In {{site.data.keyword.Bluemix}} Public, you can manage orgs and spaces, including user access all from the dashboard in the user interface. You can also monitor your usage and billing.
{:shortdesc}

### Organizations and spaces
{: #orgsandspaces}

As an organization manager or account owner, you can use the Manage Organizations page to view and manage the settings of the organization or space, including user access. To open the Manage Organizations page, click the **Account and Support** icon ![Account and Support](../support/images/account_support.svg), then select **Manage Organizations**.

#### Organizations

An organization is defined by the following items:

<dl>
<dt>Users</dt>
<dd>The role with basic permission in organizations and spaces. You must be assigned to an organization before you can be granted other permissions to the spaces within the organization. For detailed information, see [Users and roles](adminpublic.html#userroles).</dd>
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

#### Spaces

Within an organization, you can use spaces to group a set of applications, services, and users.

After you add users to an organization, you can grant them permissions to the spaces within the organization. Similar to organizations, spaces also have a set of permissions that can be assigned to users:

<ul>
<li>Space manager</li>
<li>Space developer</li>
<li>Space auditor</li>
</ul>

**Note**: A user must be assigned at least one of the permissions in the space.

The **Domains** tab for a space is a read-only list of the domains that are assigned to the space. The system domain is always available to a space, and custom domains might also be allocated to the space. Applications that were created in the space might use any of the listed domains for the space.

### Users and roles
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

#### User roles

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
<li>Add users to the space and manage users.</li>
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

**Note**: Users that are assigned the manager or developer role can access the VCAP_SERVICES environment variable. However, a user that is assigned the auditor role can't access VCAP_SERVICES.

### Managing your organizations
{: #orgmng}

As an organization manager or account owner, you can manage your organizations. Management tasks include creating an organization, renaming an organization, creating a space, inviting users to a space, changing user roles, and deleting an existing organization.

#### Creating an organization

Only users with pay accounts can create an organization. With a pay account, you can create an organization by taking the following steps:

<ol>
<li>Go to the {{site.data.keyword.Bluemix_notm}} Dashboard, click the **Account and Support** icon ![Account and Support](../support/images/account_support.svg), then select **Manage Organizations**.</li>
<li>Click **Create an Organization** and follow the prompts to create your organization.</li>
</ol>

#### Renaming an organization

Take the following steps to rename your organization:

<ol>
<li>Go to the {{site.data.keyword.Bluemix_notm}} Dashboard, click the **Account and Support** icon ![Account and Support](images/account_support.svg), and select **Manage Organizations**.</li>
<li>Select the organization that you want to rename.</li>
<li>Type a new name in the **Organization** field, and click **Save**.</li>
</ol>

#### Listing members 

Take the following steps to list the members of your organization or space:

<ol>
<li>Go to the {{site.data.keyword.Bluemix_notm}} Dashboard, click the **Account and Support** icon ![Account and Support](../support/images/account_support.svg), then select **Manage Organizations**. You can see the members of your organization and their roles in the **Users** tab.</li>
<li>Click the space name in your organization to see the members of this space and their roles.</li>
</ol>

#### Creating a space

You can create spaces in your organization; for example, a *dev* space as a development environment, a *test* space as a testing environment, and a *production* space as a production environment. Then, you an associate your apps with spaces. Take the following steps to create a space:

<ol>
<li>Go to the {{site.data.keyword.Bluemix_notm}} Dashboard, click the **Account and Support** icon ![Account and Support](images/account_support.svg), then select **Manage Organizations**.</li>
<li>Click **Create a Space** following your organization name, and follow the prompts to create your space.</li>
</ol>

#### Inviting users to a space

You can invite users to your orgs and spaces by email address. The users can access only the space that they were added to. 

Depending on whether the invitee has an IBM ID or not, that user is assigned as having a `member` or `collaborator` role for the account. The following table details how account roles are assigned by invitation type.

*Table 1. Account role assignments*

| **Invited email type** | **Assigned account role** | 
|----------------|------------------|
|User has IBM ID account linked to invited email address  | Member  | 
|User does not have an IBM ID | An IBM ID is created matching the submitted email address, and the user is added as a Member. | 
|An email address for a current {{site.data.keyword.Bluemix_notm}} user | Collaborator | 

Complete the following steps to add users with assigned roles to specific spaces for a chosen org:

<ol>
<li>Go to **Account and Support** &gt; **Account** &gt; **Manage Organizations**.</li>
<li>Select **Invite Users**.</li>
<li>Enter the email address for the person that you want to invite.</li>
<li>Select the role for the org to which you plan to invite the new user.</li>
<li>Select the role for the space to which you plan to invite the new user.</li>
<li>Select **Invite**.</li>
<li>View the confirmation that the invitation was sent in the **Pending** section. Select **Resend email** or **Cancel invitation** to take action on a pending invitation.</li>
</ol>

#### Changing user roles

Take the following steps to change user roles:

<ol>
<li>From the {{site.data.keyword.Bluemix_notm}} user interface, click the **Account and Support** icon ![Account and Support](images/account_support.svg), and then select **Manage Organizations**.</li>
<li>Select the **MANAGER**, **BILLING MANAGER**, or **AUDITOR** check box in the **USERS** tab to change roles of users in your organization. Or select a space from the navigation pane, and then select the **MANAGER**, **DEVELOPER**, or **AUDITOR** check box in the **USERS** tab to change roles of users in the space. </li>
<li>Click **SAVE**.</li>
</ol>

#### Deleting an existing organization

Contact {{site.data.keyword.Bluemix_notm}} registration and ID support to delete your organization.

**Note**: Deleting operations cannot be reversed. You lose all your applications and services that are associated with the organization.

