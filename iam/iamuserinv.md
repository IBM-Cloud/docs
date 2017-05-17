---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-17"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Inviting users
{: #iamuserinv}

You can invite users across {{site.data.keyword.Bluemix_notm}} services, applications, and {{site.data.keyword.Bluemix_notm}} infrastructure from a single location. To invite users and manage outstanding invitations, you must be either an account owner, an organization manager, or you must have infrastructure permissions to add users. You can invite users, cancel invitations, and resend a pending invitation to an invited user. You can invite a single user or, if you are providing the same access for all members in a group of users, you can invite multiple users at once.
{:shortdesc}

To invite users or manage user invitations in your account, complete the following steps:

1. From the menu bar, click **Manage** &gt; **Security** &gt; **Identity & Access** &gt; **Users**. The Users window displays a list of users with their email addresses and current status in the accounts that you manage. 
2. Click **Invite users**. 
3. Specify the email address or IBMid of the user. If you are providing multiple users the same access, you can select **Invite multiple users** to enter a list of users to invite. Separate the user ID entries with commas. 
4. Add one or more of the access options that you manage. You must assign at least one access option and configure the settings for the user in each access option that you assign. For any additional access options that you don't add and configure, the default value of *no access* is assigned. You might see one or all of the following access options, depending on the options that you are authorized to manage: **Identity and access enabled services**, **Cloud Foundry access**, **Infrastructure access**. See [Assigning user access](/docs/iam/assignaccess.html) for more information.

If you determine that a user does not need access, you can cancel an invitation for any users that are shown in a **Processing** or **Pending** state in the **Status** column. If an invited user did not receive an invitation, you can resend the invitation to any user in a **Pending** state.
