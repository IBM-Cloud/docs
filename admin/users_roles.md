---

copyright:

  years: 2015, 2016
lastupdated: "2017-04-26"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Managing Cloud Foundry access in Team Directory
{: #userroles}

You can manage platform users assigned Cloud Foundry services access from the Team Directory page for your account. You can manage existing team members and their roles in your organization and spaces. 
{:shortdesc}

You can access the Team Directory for your account from a link at the top of the new Users page. To access the Users page, from the {{site.data.keyword.Bluemix_notm}} menu, click **Manage** &gt; **Account** &gt; **Users**.

Account owners perform all operations on organizations and spaces, including managing team members and their assigned roles. Organization managers have access to manage roles. Space managers can use the **Manage Organizations** page to add existing account members to the space and adjust their roles. Check out the following information to learn more about roles.

## User roles
{: #userrolesinfo}

At the account level, there are two roles that enable access to different account management features:

| Account role | Permissions |
|----------------|---------|
|Owner | An owner for the account has access to their profile, team directory, billing information, spending notifications, and usage dashboard. From the team directory page, the owner can invite new team members and adjust roles. The owner can also add promotional credits, set or change the billing limit, set service access, and manage organizations and spaces. |
|Member | A member has access to their profile, team directory, and account credits and billing limits in the {{site.data.keyword.Bluemix_notm}} header. However, on the team directory page, a member can only view the team members within the account. |
{:caption="Table 1. Account roles and permissions" caption-side="top"}

All new team members are added as a member of the account. You can assign organization and space roles to invitees to enable specific views and permissions in {{site.data.keyword.Bluemix_notm}}. New team members added to an organization, except in a local or dedicated environment, are assigned the auditor organization role by default. For a specific space, you can choose to assign the developer or auditor role to invitees. Once your invitees accept the invitation and join {{site.data.keyword.Bluemix_notm}}, you can edit their roles on the Team Directory page.

The following roles can be assigned at the organization level:

| Organization role | Permissions |
|-------------------|-------------|
|Manager | Organization managers can create, view, edit, or delete spaces within the organization, view the organization's usage and quota, invite team members to the organization, manage who has access to the organization and their roles in the organization, and manage custom domains for the organization. |
|Billing manager | Billing managers can view runtime and service usage information for the organization on the Usage Dashboard page.  |
|Auditor | Organization auditors can view application and service content in the organization. Auditors can also view the team members in the organization and their assigned roles, and the quota for the organization. This role is assigned to all invitees, except in local or dedicated environments, by default. |
{:caption="Table 2. Organization roles and permissions" caption-side="top"}

The following roles can be assigned at the space level:

| Space role | Permissions |
|------------|-------------|
|Manager | Space managers can add existing team members and manage roles within the space. The space manager can also view the number of instances, service bindings, and resource use for each application in the space. |
|Developer | Space developers can create, delete, and manage applications and services within the space. Some of the managing tasks include deploying apps, starting or stopping apps, renaming an app, deleting an app, renaming a space, binding or unbinding a service to an application, view the number or instances, service bindings, and resource use for each application in the space. In addition, the space developer can associate an internal or external URL with an application in the space.   |
|Auditor | Space auditors have read-only access to all information about the space, such as information about the number of instances, service bindings, and resource use for each application in the space. |
{:caption="Table 3. Space roles and permissions" caption-side="top"}

**Note**: Team members that are assigned the manager or developer space role can access the VCAP_SERVICES environment variable. However, a team member that is assigned the auditor role can't access VCAP_SERVICES.

## Editing roles
{: #editinguserroles}

Account owners and organization managers can edit organization and space roles for existing team members on the Team Directory page.

1. Locate and select the team member whose roles you want to edit.
2. Click **View roles**.
3. Select or clear the space role selections to modify the space access for the team member.
4. Click **Save**.

Space managers can edit roles for the team members in their space.

1. Locate and select the team member whose roles you want to edit.
2. Click **View roles**.
3. Click **View spaces**.
4. Select or clear the space role option for the role that you want to add or remove for the team member.
5. Then, click **Save**.

## Inviting team members
{: #inviteteammembers}

You can add a user by using the Team Directory window if the user ID is not a linked account and if you are an account owner or  an organization manager. When you add new team members, except in a local or dedicated environment, they are assigned the auditor roles automatically. You can change the roles later on the Team Directory page. To invite a team member, complete these steps:

<ol>
<li>Click **Invite a user**.</li>
<li>Enter the email address for the user to invite.</li>
<li>Select the role to be assigned for the organization.</li>
<li>Select the role to be assigned for a space or spaces in the organization.</li>
<li>Select the option to confirm that you take financial responsibility for all charges that are incurred on the account.</li>
<li>Click **Invite**.</li>
</ol>

The user is added to the displayed list of team members for the account.

## Removing team members
{: #removingteammembers}

If the user was added from the Team Directory and is not a linked account, account owners and organization managers can remove team members from an account from the Team Directory page. To remove a team member, complete the following steps:

1. Locate the user that you want to remove and click the **Remove user** icon ![Remove icon](../icons/icon_remove_teamuser.svg).
2. Click **Remove** to confirm that you want to remove the specified user from the account.

The user is removed from the displayed list of team members for the account.
