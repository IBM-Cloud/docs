---

copyright:

  years: 2015, 2017

lastupdated: "2017-05-02"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Managing user accounts and access
{: #iamusermanage}

Depending on the access options that you are authorized to manage, you can view and manage users across the account or organization. As an account owner, you can manage users in any of the access options that you administer and to which the user is assigned access, regardless of the role, in the current account.
{:shortdesc}

To manage users in your account, complete the following steps:

1. From the menu bar, click **Manage** &gt; **Account** &gt; **Users**. The Users window displays a list of users with their email addresses and current status in the accounts you manage. 
2. Select the user name, or click **Manage user** from the **Actions** menu. 
3. Then, depending on what access you can manage, update the access for the user in the Service policies or Cloud Foundry roles sections, or click the link to access the Assign Infrastructure Access page.

Review the following sections for additional information about managing each type of access and information about using the Team Directory.

## Cloud Foundry services 
{: #iammancfser}

If the user is assigned access to **Cloud Foundry**, you can see the organizations and spaces the user is assigned from the Manage user window. Use the **Actions** menu to remove the user from an organization or you can change the role that is assigned for an organization or space.

If you need to manage existing space and organization roles, select **Edit organization role** or the **Edit space role** options in the row of the role you want to edit. You can add a user to another organization by clicking **Assign Organization**, if you are the manager of an organization that the user is not yet a member of. 


## Identity and access enabled services
{: #iammanidaccser}

If the user is assigned access to an **Identity and access enabled service**, you can see information about the policies assigned from the Manage user window. What is displayed for that user or group depends on the policies that have been assigned. If no policies are assigned, you see a message asking if you want to assign a policy. 

You can assign policies from the Assign policies page by clicking **Assign service policies**. The **Assign service policies** option is enabled only if you are authorized to create policies. You can manage existing policies by clicking the policy in the list or by clicking **Edit policy** from the **Actions** column for the row of the policy you want to edit.

For more information about service policies and roles, see [Identity and access management policies and roles](/docs/admin/users_roles.html#iamusermanpol).

## Infrastructure services

If you have access to assign infrastructure permissions, you can set the following roles for the user: View Only, Basic User, or Super User. Click the **Assign Infrastructure Access** link to update or assign new permissions.

For more information about the permissions, see [Infrastructure permissions](/docs/admin/users_roles.html#infrapermissions).

## Managing Cloud Foundry roles in the Team Directory
{: #editinguserroles}

From the Team Directory page, account owners can manage platform-only users. However, if you can go to the **Manage** &gt; **Account** &gt; **Users** page, you can manage all platform and infratructure services users in one place.

Organization managers can edit organization and space roles for existing users on the Team Directory page.

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
