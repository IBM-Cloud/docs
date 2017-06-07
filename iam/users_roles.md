---

copyright:

  years: 2015, 2016
lastupdated: "2017-06-06"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# User roles and permissions
{: #userroles}

<!-- staging only content in the service policy roles table. Do not move entire topic to production -->

You can manage users across the {{site.data.keyword.Bluemix_notm}} Platform and Infrastructure services from the **Users** page for your account. To access the Users page, from the {{site.data.keyword.Bluemix_notm}} menu, click **Manage** &gt; **Account** &gt; **Users**. Account owners perform all operations on organizations and spaces, including managing users and their assigned roles. Organization managers and space managers also have access to manage roles. 
{:shortdesc}

If you are a user added to another person's account, and you want to view your assigned roles and permissions, go to **Manage** &gt; **Security** &gt; **Identity & Access** &gt; **Users**, and click on your name.

## Account roles
{: #userrolesinfo}

At the account level, there are two roles that enable access to different account management features:

| Account role | Permissions |
|----------------|---------|
|Owner | An owner for the account has access to their profile, users, billing information, spending notifications, and usage dashboard. From the Users page, the owner can invite new users and adjust roles. The owner can also add promotional credits, set or change the billing limit, set service access, and manage organizations and spaces. |
|Member | A member has access to their profile, the Users page displaying the active users in the account, and account credits and billing limits in the {{site.data.keyword.Bluemix_notm}} header.  |
{:caption="Table 1. Account roles and permissions" caption-side="top"}

All new users are added as a member of the account. You can assign organization and space roles to invitees to enable specific views and permissions in {{site.data.keyword.Bluemix_notm}}. Once your invitees accept the invitation and join {{site.data.keyword.Bluemix_notm}}, you can edit their roles on the Users page.

## Cloud Foundry roles
{: #cfroles}

Cloud Foundry roles include the access permissions for organizations and spaces defined within the account. Cloud Foundry roles do not enable user permissions for completing actions within the context of a service. The following roles can be assigned at the organization level:

| Organization role | Permissions |
|-------------------|-------------|
|Manager | Organization managers can create, view, edit, or delete spaces within the organization, view the organization's usage and quota, invite users to the organization, manage who has access to the organization and their roles in the organization, and manage custom domains for the organization. |
|Billing manager | Billing managers can view runtime and service usage information for the organization on the Usage Dashboard page.  |
|Auditor | Organization auditors can view application and service content in the organization. Auditors can also view the users in the organization and their assigned roles, and the quota for the organization. All users are given the auditor role by default upon invite. You can update this role to manager or billing manager after the user accepts the invitation. |
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

Account owners are automatically assigned the account access administrator role for Identity and access managemement which enables you to assign and manage service policies. This type of access control enables the assignment of policies per service or service instance to allow levels of access for managing resources and users within the assigned context.

### Service policies

A policy assigns a user a role or roles to a set of resources by using a combination of attributes to define the applicable set of resources. When you assign a policy to a user, you first specify the service. Then, you can select a role, or roles, to assign. Additional configuration options might be available, depending on the service you select.

You can assign and manage policies if you have the proper role. The following table shows policy management tasks and the role required for each.

| Action | Role required |
|----------|---------|
| Create policies on an account for all services and instances | Account access administrator |
| Create a policy on a service in an account | Account access administrator or administrator on the service in the account |
| Create a service instance | Account access administrator or the administrator or editor on the service in the account |
| Create a policy on a service instance | Account access administrator or administrator on the service in the account or administrator on the service instance |
{: caption="Table 4. Administrative tasks for managing Identity and access enabled services policies" caption-side="top"}

### Service policy roles
{: #iamusermanrol}

Roles are a collection of actions; the actions that are mapped to these roles are service specific. Refer to the documentation for the selected service for additional details about what types of actions each role allows.

In addition to the descriptions of the roles provided in the console, the following table provides examples of some of the tasks that users assigned each role might be able to do for the IBM Container service.  

**Note**: The operator role is not available for the IBM Container service at this time. The following example is included for informational purposes only.

| Role | Description of actions | Example actions|
|:-----------------|:-----------------|:-----------------|
| Viewer | Performs actions that do not change state; read only actions | <ul><li>List clusters</li><li>View details for a cluster</li></ul>|
| Editor | Performs actions that modify the state and create or delete sub-resources |<ul><li>Add or remove worker nodes</li><li>Reboot or reload worker nodes</li><li>Bind a service to a cluster</li></ul> |
| Operator | Performs actions required to configure and operate resources. | <ul><li>Add or remove worker nodes</li><li>Reboot or reload worker nodes</li><li>Bind a service to a cluster</li></ul> |
| Administrator | Performs all actions, including the ability to manage access control |<ul><li>Remove a cluster</li><li>Create a cluster</li><li>Update user access policies</li><li>All actions a viewer and editor can perform</li></ul>|
{: caption="Table 5. Administrative tasks for managing Identity and access enabled services policies" caption-side="top"}

## Infrastructure permissions
{: #infrapermissions}

You can set the following permissions when you invite a user: 

| Infrastructure permission | Description of actions |
|---------------------------|------------------------|
|View Only | Users with this permission can only view items within the system.|
|Basic User | Users with this permission can perform basic actions within the system, such as adding a ticket and managing devices. |
|Super User | Users with this permission can perform all actions available in the system. |
{:caption="Table 6. Infrastructure permissions" caption-side="top"}

Additional permissions can be set after the user has accepted the invite.
