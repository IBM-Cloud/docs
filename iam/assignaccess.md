---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-30"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Assigning user access
{: #assignaccess}

You assign access for users as you invite them, assigning Cloud Foundry roles, policies, and infrastructure permissions. Depending on the access options that you are authorized to manage, you can invite and provide access for users across the account, organization, space, and service instances. The following sections describe the three types of access that can be assigned to an invited user.
{:shortdesc}

## Identity and access enabled services

You can assign a single service policy when you invite a new user. Once the user has accepted the invitation, you can add additional service policies.

1. From the **Invite users** screen, expand the **Identity and Access enabled services** section.
2. Select a service.
3. Select **All current regions** or a specific region.
4. Select **All current service instances** or select a specific service instance.
5. Select a role to define the scope of access for the policy.
6. Optional: Select **Add role** to specify an additional role for the policy.

See [Identity and access management policies and roles](/docs/iam/users_roles.html#iamusermanpol) for more specific information about the roles when setting service policies.

## Cloud Foundry access

When you invite new users, you can choose to add the user to an organization in the account. If you add the user to an organization, they are granted the auditor organization role by default. You can update this role later to billing manager, organization manager, or no organization role after the user accepts the invitation. In addition, you can choose to give the invited user access to any or all of the spaces in the selected organization.

1. From the **Invite users** screen, expand the **Cloud Foundry access** section.
2. Select an organization to add the user to.
3. Select **All current regions** or a specific region.
4. Select **All current spaces** or a specific space.
5. Select a space role to define the level of access to the selected spaces.
6. Optional: Select **Add role** to specify an additional role.

See [Cloud Foundry roles](/docs/iam/users_roles.html#cfroles) for more specific information about these roles.

**Note**: You can add a Cloud Foundry role using the [bluemix iam account-user-invite](https://console.stage1.bluemix.net/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_iam_account_user_invite) CLI command, but the UI must be used to assign other access or permissions.

## Infrastructure access

The actual permissions assigned are automatically limited to the subset of permissions that you have. For more information about the permissions and what actions the user can perform with each, see [Infrastructure permissions](/docs/iam/users_roles.html#infrapermissions).

1. From the **Invite users** screen, expand the **Infrastructure access** section. 
2. Select a permission to define the scope of access.

For information about configuring access for users after they have been added to your account, see [Managing users and access](/docs/iam/iamusermanage.html).
