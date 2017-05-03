---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-03"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Assigning user access
{: #assignaccess}

You assign access for the users as you invite them, assigning roles, policies, and the accounts or organizations, or both, that they can access. Depending on the access options that you are authorized to manage, you can invite and provide access for users across the account or organization. As an account owner, you can assign access options to your account for a user when you and the user are both members, regardless of the role. The following sections describe the three types of access that can be assigned to an invited user.
{:shortdesc}

## Identity and access enabled services

When you assign a policy to a user, you first specify the service to assign, including an option to assign all available services. Then, you can also select all service instances, a single service instance, regions, and a role, or roles. You can assign a single service policy when you invite a new user. Once the user has accepted the invitation, you can add additional service policies.

**Note**:  If you select the **Automatically grant access when new services are added** option, you are not notified to deselect each new {{site.data.keyword.Bluemix_notm}} service for that user when services are added later.

## Cloud Foundry access

Select to assign the organization, regions, spaces, and space roles for the users you invite. See [Cloud Foundry roles](/docs/iam/users_roles.html#cfroles) for more specific information about these settings. You can add multiple space roles, one at a time. All users are granted the auditor organization role by default. You can update this role to billing manager or organization manager after the user accepts the invitation.

## Infrastructure access

If you have permission, you see the option to assign infrastructure permissions. For more information about the permissions and what actions the user can perform with each, see [Infrastructure permissions](/docs/iam/users_roles.html#infrapermissions).

**Note**: The actual permissions assigned are automatically limited to the subset of permissions that you have.

For information about configuring access for users after they have been added to your account, see [Managing user accounts and access](/docs/iam/iamusermanage.html).
