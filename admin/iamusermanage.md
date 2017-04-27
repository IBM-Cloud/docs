---

copyright:

  years: 2015, 2017

lastupdated: "2017-04-26"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Managing user accounts and access
{: #iamusermanage}

Depending on the access options that you are authorized to manage, you can view and manage users across the account or organization. As an account owner, you can manage users in any of the access options that you administer and to which the user is assigned access, regardless of the role, in the current account. You can assign, edit, and remove access for users in any of the access options that you manage. 
{:shortdesc}

To manage users in your account, complete the following steps:

1. From the menu bar, click **Manage** &gt; **Account** &gt; **Users**. The Users window displays a list of users with their email addresses and current status in the accounts you manage. 
2. Select the user to manage, or click **Manage user** from the **Actions** menu. 
3. Then, depending on what access you can assign, update the access for the user in the Service policies or Cloud Foundry roles sections, or click the link to access the Assign Infrastructure Access page.

Review the following sections for additional information about managing each type of access.

## Cloud Foundry services access
{: #iammancfser}

If the user is assigned access to **Cloud Foundry**, you can see the organizations and spaces the user is assigned from the Manage user window. You can remove the user from an organization or you can change the role that is assigned for an organization or space. You can add a user to another organization by clicking **Assign Organization** if you are the manager of an organization that the user is not yet a member of. You can manage existing space and organization roles by clicking **Edit space role** or the **Edit organization role** in the row of the role you want to edit.

## Identity and access enabled services
{: #iammanidaccser}

If the user is assigned access to an **Identity and access enabled service**, you can see information about the policies assigned from the Manage user window. What is displayed for that user or group depends on the policies that have been assigned. If no policies are assigned, you see a message asking if you want to assign a policy. 

If policies are already assigned, then a list of the policies is shown with the role of the user or group and a description of the resource attributes for each policy. You can assign policies from the Assign policies page by clicking **Assign service policies**. The **Assign service policies** option is enabled if you are authorized to create policies. You can manage existing policies by clicking the policy in the list or by clicking **Edit policy** under **Actions** in the row of the policy you want to edit.

### About service policies
{: #iamusermanpol}

You can assign and manage policies for a user that has access to **Identity and access enabled services**. A policy assigns a user a role or roles to a set of resources by using a combination of attributes to define the applicable set of resources.

When you assign a policy to a user, you first specify the service to assign. The **Service** list provides the option for specific services, including an option to assign all available services. You also select a role, or roles, to assign.

Additional configuration options are available, depending on the service you select. You can select a service to see options for that service.

You can narrow the list of service options that are displayed. Click **Specify optional service context** to specify additional options like regions and service instances.  You might not want to specify all of the options that are displayed, but you can choose which to configure.

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
{: caption="Table 1. Administrative tasks for managing Identity and access enabled services policies" caption-side="top"}

### Service policy roles
{: #iamusermanrol}

Roles are a collection of actions; the actions that are mapped to these roles are service specific. 
Because actions are grouped as roles, you can use a small set of defined roles to support any actions for any services and any resource. For example, if you need an administrator for virtual machines, storage, and networking, you can set the user as the administrator for all three by changing the target of the policy. So you would set the policy to include the administrator of virtual machines, the administrator of storage, and the administrator of Networking.

Resources are not built into the roles so that new role names are not created for every type of resource that is introduced in the system. For example, you do not need a virtual machine administrator role, a storage administrator role, and a network administrator role to cover administration for resources of virtual machines, storage, and network.

In addition to the descriptions of the roles provided in the console, the following table provides examples of some of the tasks that users assigned each role might be able to do depending on the selected service. Refer to the documentation for the selected service for additional details about what types of actions each role provides.

{: #iamui_table2}

| Role | Description of actions | Example actions|
|:-----------------|:-----------------|:-----------------|
| Viewer | Performs actions that do not change state; read only actions | <ul><li>List devices</li><li>Read storage object</li><li>Run queries</li><li>Run searches</li></ul>|
| Editor | Performs actions that modify the state and create or delete sub-resources |<ul><li>Create or delete virtual machines</li><li>Attach storage</li><li>Reboot</li><li>Start or stop</li><li>Rename</li></ul> |
| Administrator | Performs all actions, including the ability to manage access control |<ul><li>Invite users</li><li>Create or delete virtual machines</li><li>Update user access policies</li><li>List devices</li><li>Attach storage</li><li>Reboot</li><li>Start or stop</li><li>Rename</li><li>Back up and restore</li></ul>|
{: caption="Table 2. Administrative tasks for managing Identity and access enabled services policies" caption-side="top"}

For more specific information about roles of users assigned access to Cloud Foundry, see [User roles](/docs/admin/users_roles.html#userrolesinfo).

## Infrastructure access

If you have access to assign infrastructure roles, you can set the following roles for the user: 

<dl>
<dt>View Only</dt>
<dd>Users with this permission can only view items within the system.</dd>
<dt>Basic User</dt>
<dd>Users with this permission can perform basic actions within the system, such as adding a ticket and managing devices.</dd>
<dt>Super User</dt>
<dd>Users with this permission can perform all actions available in the system.</dd>
</dl>
