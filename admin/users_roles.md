---



copyright:

  years: 2015, 2016
lastupdated: "2016-12-05"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Identity and Access Management
{: #iamuserman}

You can view and manage users across the account or organization, depending on the access options that you are authorized to manage.  You can perform all operations for users including inviting and managting users, their assigned roles, and the accounts or organizations, or both, that they can access. As an account owner, you can manage the orgs of which you and the users are both members, regardless of role, in the current account.
{:shortdesc}

To access the users for your account, click **Identity and access** &gt; **Users**. The **Account users** window displays a list of users with their email addresses and current status in the accounts you manage.  If you manage multiple accounts, you can also filter to select the account in which to display users.  From the **Account users** window, you can navigate to manage the following tasks:

* [Administer user invitations](#iamuserinvite)
* Manage users (from the **Actions** menu)
*	Assign infrastructure access (from the **Actions** menu)
*	Assign Platform policies (from the **Actions** menu)
*	View user logs (from the **Actions** menu)
*	Remove users (from the **Actions** menu)

## Administering user invitations
{: #iamuserinvite}

If you are an account owner, you can invite users, cancel invitations for invited users who have not yet accepted the invitation to create their access, and resend a pending invitation to an invited user. You can invite a single user or, if you are providing the same access for a all members in a group of users, you can invite mutliple users at once.

(Do we need to mention that users can sign up on their own?)

To invite users, click **Invite users**, specify the email address or IBMid of the user, and then add them to one or more of the access options that you manage. You must grant access to at least one access option. You then configure the user's settings in each access option.  If you don't configure the settings, a default value of *no access* is assigned in that access option and the user, therefore, has no access.  You might see one or all of the following access options, dependind on the options that you are authorized to manage:
<dl>
<dt>Bluemix Access Enabled Services</dt>
<dd>Select to assign the services, regions, service instances, and roles for the users you invite. Selecting the **Automatically grant access when new services are added** option adds the user to all services that are added to **Bluemix Access Enabled Services** in the future and you are not notified with the option to deselect the new service for that user.</dd>
<dt>Bluemix Legacy Platform Access</dt>
<dd>Select to assign the services, regions, spaces, and space roles for the users you invite.</dd>
<dt>Bluemix Infrastructure Access</dt>
<dd>Select the permission set to assign the users you invite.</dd>
</dl>

You can also cancel an invitation for any users that are shown in the Status column in a Pending state if you determine that the user does not need access.  If a user in a Pending state does not recieve an invitation after you added the user, you can also resend pending invitation.

## Managing users
{: #iamusermanage}

(Do we need to mention users might have signed up on their own & gotten default settings?  If so, what would those be?)

Select the user or group to manage (discuss fields available to edit on select).

You can assign, edit, and remove access for users in any of the access options that you manage.  If the user has different access, you only see policy tables for the access options that you manage:
(explain what can be edited and why for each)
<dl>
<dt>Bluemix Access Enabled Services</dt>
<dd>Action menu to edit or remove policy.</dd>
<dt>Bluemix Legacy Platform Access</dt>
<dd>Table displays orgs & org roles
Add, change, or remove Space roles or Organization roles.</dd>
<dt>Bluemix Infrastructure Access</dt>
<dd></dd>
</dl>

Links to the following configuration options not directly tied to a specific chosen user are available from the modified **Actions** menu:
* Anchor Links to API Keys
* Group policies
* Unique policies

You can manage the following functions if no spaces are assigned:
* View user logs
* Remove user from account
* Assign infrastructure access

## Assigning Policies
{: #iamuserasspol}

You can assign policies to users, groups, or service IDs.  This option is enabled for users who are authorized to create policies.  You can select a service, and region, to see options for that service:
* All Bluemix Access Enabled Services
* Kubernetes
* Cloud Foundry

Additional configuration options available depend on the selection.  So “Cloud Foundry” options are different than “Kubernetes”

You can narrow service choices by specifying regions and service instances, and selecting roles.

Roles are defined when selected, can add multiples (give example) and new roles can be added

## Managing API keys
{: #iamusermanapikey}

Discuss purpose (such as logging in with an API key)

Change API keys (Edit name, edit description, delete)

Create API key (pop up provide name and description) -> input (paste) key (only time user sees key) to download (text file of API key)

### Managing platform team members and roles
{: #userroles}

From the **Team Directory** page for your account, you can manage existing team members and their roles in your organization and spaces, as well as invite new team members. To access the team directory for your account, click the **Team Directory** link from the Account Users page.
{:shortdesc}

Account owners perform all operations on organizations and spaces including managing team members and their assigned roles. Organization managers  have access to invite team members and manage roles. Space managers can use the **Manage Organizations** page to add existing account members to the space and adjust their roles. Check out the following information to learn more about roles.

#### Roles
{: #userrolesinfo}

At the account level, there are two roles that enable access to different account management features:

| Account role | Permissions |
|----------------|---------|
|Owner | An owner for the account has access to their profile, team directory, billing information, spending notifications, and usage dashboard. From the team directory page, the owner can invite new team members and adjust roles. The owner can also add promotional credits, set or change the billing limit, set service access, and manage organizations and spaces. |
|Member | A member has access to their profile, team directory, and account credits and billing limits in the {{site.data.keyword.Bluemix_notm}} header. However, on the team directory page, a member can only view the team members within the account. |
{:caption="Table 1. Account roles and permissions" caption-side="top"}

 All new team members are added as a member of the account. You can assign organization and space roles to invitees to enable specific views and permissions in {{site.data.keyword.Bluemix_notm}}. New team members added to an organization, except in a local or dedicated environment, are assigned the auditor organization role by default. For a specific space, you can choose to assign the developer or auditor role to invitees. Once your invitees accept the invitation and join {{site.data.keyword.Bluemix_notm}}, you can edit their roles on the **Team Directory** page.

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

#### Adjusting visibility of the team directory
{: #teamdirectoryvisibility}

Depending on how you have your {{site.data.keyword.Bluemix_notm}} accounts and organizations set up, you might want to change the visibility of the team directory page. By default, all team members within your account can see the full list of account team members, including all members of all organizations within the account. You might have privacy concerns or security reasons that prompt you to adjust the visibility of the team directory page. You have two options for setting the visibility of the team directory page: all team members or just you as the account owner.

To change the visibility of the team directory page complete the following steps:

1. Click **Account** &gt; **Team Directory**.
2. For the **Visibility to** option, click the current selection to view the options.
3. Then, select **All** or **Just me** based on the current needs for your account.
4. Then, click **Save**.

#### Inviting team members
{: #inviteteammembers}

Account owners and organization managers can invite team members to orgs from the Invite Team Members page. When you add new team members, except in a local or dedicated environment, they are assigned the auditor roles automatically. You can change the roles later on the Team Directory page. To invite a team member, complete these steps:

<ol>
<li>Click **Account** &gt; **Invite Team Members**.</li>
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

#### Editing roles
{: #editinguserroles}

Account owners and organization managers can edit organization and space roles for existing team members on the **Team Directory** page.

1. Click **Account** &gt; **Team Directory**.
2. Locate the team member whose roles you want to edit.
3. Click **View Roles**.
4. Select or clear the org role selections to modify the org access for the team member.
5. Click **View Spaces** to add or remove space roles.
6. Select or clear the space role selections to modify the space access for the team member.
7. Click **Close Spaces**.
8. Click **Save** at the end of the page.

Space managers can edit roles for the team members in their space on the **Manage Organizations** page.

1. Click **Account** &gt; **Manage Organizations**.
2. Locate the org that your space is in.
3. Click **View Details**.
4. Locate your space, and click **Edit space**.
5. Select the **Users** tab.
6. Select or clear the space role option for the role that you want to add or remove for the team member.
7. Then, click **Save**.

#### Removing team members
{: #removingteammembers}

Account owners and organization managers can remove team members from an account by using the **Team Directory** page. To remove a team member, complete the following steps:

1. Click **Account** &gt; **Team Directory**.
3. Locate the user that you want to remove from the account and click the **Remove** icon ![Remove icon](../icons/icon_remove_teamuser.svg).
4. In the **Remove User** window, click **Remove** to confirm that you want to remove the specified user from the account.

The user is removed from the displayed list of team members for the account.
