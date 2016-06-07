---



copyright:

  years: 2015, 2016



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Managing team members and roles
{: #userroles}
*Last updated: 1 June 2016*

From the **Team Directory** page for your account, you can manage existing team members and their roles in your organization and spaces, as well as invite new team members. To access the team directory for your account, go to the **Account and Support** icon ![Account and Support icon](../admin/images/account_support.svg) &gt; **Account** &gt; *your_account_name* &gt; **Team Directory**. 
{:shortdesc}

Account owners perform all operations on organizations and spaces including managing team members and their assigned roles. Organization managers  have access to invite team members and manage roles. Space managers can use the **Manage Organizations** page to add existing account members to the space and adjust their roles. Check out the following information to learn more about roles.

## Roles
{: #userrolesinfo}

At the account level, there are two roles that enable access to different account management features:

*Table 1. Account roles and permissions*

| Account role | Permissions |    
|----------------|---------|
|Owner | An owner for the account has access to their profile, team directory, billing information, spending notifications, and usage dashboard. From the team directory page, the owner can invite new team members and adjust roles. The owner can also add promotional credits, set or change the billing limit, set service access, and manage organizations and spaces. |
|Member | A member has access to their profile, team directory, and account credits and billing limits in the {{site.data.keyword.Bluemix_notm}} header. However, on the team directory page, a member can only view the team members within the account. |

 All new team members are added as a member of the account. You can assign organization and space roles to invitees to enable specific views and permissions in {{site.data.keyword.Bluemix_notm}}. New team members added to an organization are assigned the auditor organization role by default. For a specific space, you can choose to assign the developer or auditor role to invitees. Once your invitees accept the invitation and join {{site.data.keyword.Bluemix_notm}}, you can edit their roles on the **Team Directory** page.

The following roles can be assigned at the organization level:

*Table 2. Organization roles and permissions*

| Organization role | Permissions |    
|-------------------|-------------|
|Manager | Organization managers can create, view, edit, or delete spaces within the organization, view the organization's usage and quota, invite team members to the organization, manage who has access to the organization and their roles in the organization, and manage custom domains for the organization. |
|Billing manager | Billing managers can view runtime and service usage information for the organization on the Usage Dashboard page.  |
|Auditor | Organization auditors can view application and service content in the organization. Auditors can also view the team members in the organization and their assigned roles, and the quota for the organization. This role is assigned to all invitees by default.|

The following roles can be assigned at the space level:

*Table 3. Space roles and permissions*

| Space role | Permissions |    
|------------|-------------|
|Manager | Space managers can add existing team members and manage roles within the space. The space manager can also view the number of instances, service bindings, and resource use for each application in the space. |
|Developer | Space developers can create, delete, and manage applications and services within the space. Some of the managing tasks include deploying apps, starting or stopping apps, renaming an app, deleting an app, renaming a space, binding or unbinding a service to an application, view the number or instances, service bindings, and resource use for each application in the space. In addition, the space developer can associate an internal or external URL with an application in the space.   |
|Auditor | Space auditors have read-only access to all information about the space, such as information about the number of instances, service bindings, and resource use for each application in the space. |

**Note**: Team members that are assigned the manager or developer space role can access the VCAP_SERVICES environment variable. However, a team member that is assigned the auditor role can't access VCAP_SERVICES.

## Inviting team members
{: #inviteteammembers}

Account owners and organization managers can invite team members to orgs from the Invite Team Members page. When you add new team members, they are assigned the auditor roles automatically. You can change the roles later on the Team Directory page. To invite a team member, complete these steps:

<ol>
<li>Go to the **Account and Support** icon ![Account and Support icon](../admin/images/account_support.svg) &gt; **Account** &gt; *your_account_name* &gt; **Invite Team Member**.</li>
<li>Select the org that you want to invite team members to.</li>
<li>Click **Next**.</li>
<li>Select the spaces that you want to allow access to for your team members.</li>
<li>Select the role to be assigned for the selected spaces in the org.</li>
<li>Select the option to confirm that you take financial responsibility for all charges that are incurred on the account.</li>
<li>Enter the email address for an individual team member, or email addresses for multiple team members:
<ul>
<li>To add a single team member, enter the email address, and click **Send**.</li>
<li>To add more than one team member, click **Invite them all at once**. Enter the email addresses using a comma-separated list, spaces, or line breaks. Then, click **Next** to verify the email addresses to send the invites to, and click **Send**.</li>
</ul>
</li>
</ol>

Click **View Pending** to check if invites are pending or accepted. You can choose to resend the invitation email or cancel the invitation for a pending invite at any time.

If you have a SoftLayer account linked with your {{site.data.keyword.Bluemix_notm}} account, you can add your SoftLayer team members. Go to the **Account and Support** icon ![Account and Support icon](../admin/images/account_support.svg) &gt; **Account** &gt; *your_account_name* &gt; **Invite Team Members** page. Then, click **Add** in the **Add SoftLayer Team Members** section to authenticate into your SoftLayer account and view a list of team members from your SoftLayer account. For more information about adding team members from your SoftLayer account, see [Inviting SoftLayer team members to {{site.data.keyword.Bluemix_notm}}](../admin/softlayerlink.html#invite_users).

## Editing roles
{: #editinguserroles}

Account owners and organization managers can edit organization and space roles for existing team members on the **Team Directory** page. 

1. Go to the **Account and Support** icon ![Account and Support icon](../admin/images/account_support.svg) &gt; **Account** &gt; *your_account_name* &gt; **Team Directory**.
2. Locate the team member whose roles you want to edit.
3. Click **View Roles**.
4. Select or clear the org role selections to modify the org access for the team member.
5. Click **View Spaces** to add or remove space roles.
6. Select or clear the space role selections to modify the space access for the team member.
7. Click **Close Spaces**.
8. Click **Save** at the end of the page.

Space managers can edit roles for the team members in their space on the **Manage Organizations** page.

1. Go to the **Account and Support** icon ![Account and Support icon](../admin/images/account_support.svg) &gt; **Account** &gt; *your_account_name* &gt; **Manage Organizations**.
2. Locate the org that your space is in.
3. Click **View Details**.
4. Locate your space, and click **Edit space**.
5. Select the **Users** tab.
6. Select or clear the space role option for the role that you want to add or remove for the team member.
7. Click **Save**.
