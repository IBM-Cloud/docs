---

copyright:

  years: 2015, 2016
lastupdated: "2017-05-02"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# User roles and permissions
{: #userroles}

You can manage users across the {{site.data.keyword.Bluemix_notm}} Platform and Infrastructure services from the **Users** page for your account. A link to the Team Directory page is also available from the Users page, if you want to manage only the platform users' Cloud Foundry access to organizations and spaces. However, you do not have to leave the Users page to manage Cloud Foundry access.
{:shortdesc}

To access the Users page, from the {{site.data.keyword.Bluemix_notm}} menu, click **Manage** &gt; **Account** &gt; **Users**. Account owners perform all operations on organizations and spaces, including managing users and their assigned roles. Organization managers and space managers also have access to manage roles. 

## Account roles
{: #userrolesinfo}

At the account level, there are two roles that enable access to different account management features:

| Account role | Permissions |
|----------------|---------|
|Owner | An owner for the account has access to their profile, team directory, billing information, spending notifications, and usage dashboard. From the team directory or users page, the owner can invite new team members and adjust roles. The owner can also add promotional credits, set or change the billing limit, set service access, and manage organizations and spaces. |
|Member | A member has access to their profile, team directory, and account credits and billing limits in the {{site.data.keyword.Bluemix_notm}} header. However, on the team directory page, a member can only view the team members within the account. |
{:caption="Table 1. Account roles and permissions" caption-side="top"}

All new users are added as a member of the account. You can assign organization and space roles to invitees to enable specific views and permissions in {{site.data.keyword.Bluemix_notm}}. New team members added to an organization, except in a local or dedicated environment, are assigned the auditor organization role by default. For a specific space, you can choose to assign the developer or auditor role to invitees. Once your invitees accept the invitation and join {{site.data.keyword.Bluemix_notm}}, you can edit their roles on the Users or Team Directory page.

## Cloud Foundry roles
{: #cfroles}

Cloud Foundry roles include the access permissions for organizations and spaces defined within the account. The following roles can be assigned at the organization level:

| Organization role | Permissions |
|-------------------|-------------|
|Manager | Organization managers can create, view, edit, or delete spaces within the organization, view the organization's usage and quota, invite team members to the organization, manage who has access to the organization and their roles in the organization, and manage custom domains for the organization. |
|Billing manager | Billing managers can view runtime and service usage information for the organization on the Usage Dashboard page.  |
|Auditor | Organization auditors can view application and service content in the organization. Auditors can also view the users in the organization and their assigned roles, and the quota for the organization. This role is assigned to all invitees, except in local or dedicated environments, by default. |
{:caption="Table 2. Organization roles and permissions" caption-side="top"}

The following roles can be assigned at the space level:

| Space role | Permissions |
|------------|-------------|
|Manager | Space managers can add existing users and manage roles within the space. The space manager can also view the number of instances, service bindings, and resource use for each application in the space. |
|Developer | Space developers can create, delete, and manage applications and services within the space. Some of the managing tasks include deploying apps, starting or stopping apps, renaming an app, deleting an app, renaming a space, binding or unbinding a service to an application, view the number or instances, service bindings, and resource use for each application in the space. In addition, the space developer can associate an internal or external URL with an application in the space.   |
|Auditor | Space auditors have read-only access to all information about the space, such as information about the number of instances, service bindings, and resource use for each application in the space. |
{:caption="Table 3. Space roles and permissions" caption-side="top"}

**Note**: Users that are assigned the manager or developer space role can access the VCAP_SERVICES environment variable. However, a user that is assigned the auditor role can't access VCAP_SERVICES.

## Identity and access management policies and roles
{: #iamusermanpol}

Account owners are automatically assigned the administrator role for Identity and access managemement which enables you to assign and manage service policies. This type of access control enables the assignment of policies per service or service instance to allow levels of access for managing resources and users within the assigned context.

A policy assigns a user a role or roles to a set of resources by using a combination of attributes to define the applicable set of resources. When you assign a policy to a user, you first specify the service to assign, including an option to assign all available services. Then, you can also select a role, or roles, to assign. Additional configuration options might be available, depending on the service you select.

You can assign and manage policies if you have the proper role. The following table shows policy management tasks and the role required for each one.

{: #iamui_table1}

| Action | Role required |
|----------|---------|
| Create a policy on an account | Account access administrator |
| Create a policy on all services in an account | Account access administrator |
| Create a policy on all service instances in an account | Account access administrator |
| Create a policy on a service in an account | Account access administrator or administrator on the service in the account |
| Create a service instance | Account access administrator or editor or administrator or editor on the service in the account |
| Create a policy on a service instance | Account access administrator or administrator on the service in the account or administrator on the service instance |
{: caption="Table 4. Administrative tasks for managing Identity and access enabled services policies" caption-side="top"}

### Service policy roles
{: #iamusermanrol}

Roles are a collection of actions; the actions that are mapped to these roles are service specific. 
Because actions are grouped as roles, you can use a small set of defined roles to support any actions for any services and any resource. For example, if you need an administrator for virtual machines, storage, and networking, you can set the user as the administrator for all three by changing the target of the policy. So you would set the policy to include the administrator of virtual machines, the administrator of storage, and the administrator of networking.

Resources are not built into the roles so that new role names are not created for every type of resource that is introduced in the system. For example, you do not need a virtual machine administrator role, a storage administrator role, and a network administrator role to cover administration for resources of virtual machines, storage, and network.

In addition to the descriptions of the roles provided in the console, the following table provides examples of some of the tasks that users assigned each role might be able to do depending on the selected service. Refer to the documentation for the selected service for additional details about what types of actions each role allows.

{: #iamui_table2}

| Role | Description of actions | Example actions|
|:-----------------|:-----------------|:-----------------|
| Viewer | Performs actions that do not change state; read only actions | <ul><li>List devices</li><li>Read storage object</li><li>Run queries</li><li>Run searches</li></ul>|
| Editor | Performs actions that modify the state and create or delete sub-resources |<ul><li>Create or delete virtual machines</li><li>Attach storage</li><li>Reboot</li><li>Start or stop</li><li>Rename</li></ul> |
| Administrator | Performs all actions, including the ability to manage access control |<ul><li>Invite users</li><li>Create or delete virtual machines</li><li>Update user access policies</li><li>List devices</li><li>Attach storage</li><li>Reboot</li><li>Start or stop</li><li>Rename</li><li>Back up and restore</li></ul>|
{: caption="Table 5. Administrative tasks for managing Identity and access enabled services policies" caption-side="top"}

## Infrastructure permissions
{: #infrapermissions}

If you have access to assign infrastructure roles, you can set the following permissions for the user: 

<dl>
<dt>View Only</dt>
<dd>Users with this permission can only view items within the system.</dd>
<dt>Basic User</dt>
<dd>Users with this permission can perform basic actions within the system, such as adding a ticket and managing devices.</dd>
<dt>Super User</dt>
<dd>Users with this permission can perform all actions available in the system.</dd>
</dl>
