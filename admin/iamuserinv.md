---

copyright:

  years: 2015, 2017
lastupdated: "2017-03-08"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Inviting users, assigning and managing access
{: #iamuserinv}

You can invite users across {{site.data.keyword.Bluemix_notm}} services, applications, and {{site.data.keyword.Bluemix_notm}} infrastructure from a single location. You assign access for the users as you invite them, assigning roles, policies, and the accounts or organizations, or both, that they can access. Depending on the access options that you are authorized to manage, you can invite and provide access for users across the account or organization. As an account owner, you can assign access options to your account for a user when you and the user are both members, regardless of the role. 
{:shortdesc}

To invite users or manage user invitations in your account, from the menu bar, click **Manage** &gt; **Account** &gt; **Users**. The Users window displays a list of users with their email addresses and current status in the accounts that you manage. 

To invite users and manage outstanding invitations, you must be either an account owner, an organization manager, or you must have infrastructure permissions to add users.  You can invite users, cancel invitations, and resend a pending invitation to an invited user. You can invite a single user or, if you are providing the same access for all members in a group of users, you can invite multiple users at once.

To invite users, click **Invite users**, specify the email address or IBMid of the user, and then add them to one or more of the access options that you manage. You must assign at least one access option and configure the settings for the user in each access option that you assign. For any additional access options that you don't add and configure, the default value of *no access* is assigned. You might see one or all of the following access options, depending on the options that you are authorized to manage:

**Identity and access enabled services**
Select to assign the services, regions, service instances, and roles for the users you invite.
**Note**:  If you select the **Automatically grant access when new services are added** option, you are not notified to deselect each new {{site.data.keyword.Bluemix_notm}}  service for that user when services are added later.

**Cloud Foundry access**
Select to assign the services, regions, spaces, and space roles for the users you invite. See [User roles](/docs/admin/users_roles.html#userrolesinfo) for more specific information about these settings. You can add multiple roles, one at a time.

**Infrastructure access**
Assign the following infrastructure permission to the user: 
<dl>
<dt>View Only</dt>
<dd>Users with this permission can only view items within the system.</dd>
<dt>Basic User</dt>
<dd>Users with this permission can perform basic actions within the system, such as adding a ticket and managing devices.</dd>
<dt>Super User</dt>
<dd>Users with this permission can perform all actions available in the system.</dd>
</dl>
**Note**: The actual permissions assigned are automatically limited to the subset of permissions that you have.

If you are providing multiple users the same access, you can select **Invite multiple users** to enter a list of users to invite. Separate the user ID entries with commas.  

If you determine that a user does not need access, you can also cancel an invitation for any users that are shown in a **Processing** or **Pending** state in the **Status** column. If an invited user did not receive an invitation, you can also resend the invitation to any user in a **Pending** state.  These options are available for users in the appropriate state from the **Actions** menu on the Users window.

For specific information about configuring access for users, including roles and policies, see [Managing user accounts and access](/docs/admin/iamusermanage.html).
