---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-11"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Assigning user access
{: #assignaccess}

You assign access for the users as you invite them, assigning roles, policies, and the accounts or organizations, or both, that they can access. Depending on the access options that you are authorized to manage, you can invite and provide access for users across the account, organization, space, and service instances. As an account owner, you can assign access options to your account for a user when you and the user are both members, regardless of the role. The following sections describe the three types of access that can be assigned to an invited user.
{:shortdesc}

## Identity and access enabled services

You can assign a single service policy when you invite a new user. Once the user has accepted the invitation, you can add additional service policies.

1. From the **Invite users** screen, expand the **Identity and Access enabled services** section.
2. Select **All Identity and Access enabled services**, or select an individual service. **Note**: If you select the **Automatically grant access when new services are added** option, you are not notified to deselect each new {{site.data.keyword.Bluemix_notm}} service for that user when services are added later.
3. Select **All current regions** or a specific region.
4. Select **All current service instances** or select a specific service instance.
5. Select a role to define the scope of access for the policy.
6. Optional: Select **Add role** to specify an additional role for the policy.

See [Identity and access management policies and roles](/docs/iam/users_roles.html#iamusermanpol) for more specific information about setting service policies.

## Cloud Foundry access

All users are granted the auditor organization role by default. You can update this role to billing manager, organization manager, or no organization role after the user accepts the invitation. During the invite process, you can add multiple space roles, one at a time.

1. From the **Invite users** screen, expand the **Cloud Foundry access** section.
2. Select an organization to add the user to.
3. Select **All current regions** or a specific region.
4. Select **All current spaces** or a specific space.
5. Select a role to define the scope of access.
6. Optional: Select **Add role** to specify an additional role for the policy.

See [Cloud Foundry roles](/docs/iam/users_roles.html#cfroles) for more specific information about these roles.

## Infrastructure access

If you have permission, you see the option to assign infrastructure permissions. The actual permissions assigned are automatically limited to the subset of permissions that you have. For more information about the permissions and what actions the user can perform with each, see [Infrastructure permissions](/docs/iam/users_roles.html#infrapermissions).

1. From the **Invite users** screen, expand the **Infrastructure access** section. 
2. Select a permission to define the scope of access.

For information about configuring access for users after they have been added to your account, see [Managing user accounts and access](/docs/iam/iamusermanage.html).
