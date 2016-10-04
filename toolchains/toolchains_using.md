---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Using toolchains on {{site.data.keyword.Bluemix_notm}} Public
{: #toolchains-using}

Last updated: 13 September 2016
{: .last-updated}

You can use a toolchain to be productive in your daily development, deployment, and operations work. After you set up a toolchain, you can add, delete, or configure tool integrations and manage access to the toolchain.
{: shortdesc}

**Important**: Toolchains are available in the US South region only.

## Configuring a tool integration
{: #configuring_a_tool_integration}

If you deferred the configuration of a tool integration when you created a toolchain, a **Configure** button is shown on its tile. If you configured a tool integration when you created a toolchain, you can update the configuration settings.

1. On the DevOps dashboard, on the **Toolchains** tab, click a toolchain to open its Tool Integrations page. Alternatively, on the app's Overview page, on the Continuous Delivery tile, click **View Toolchain**, and then click **Tool Integrations**.
1. If you need to configure a tool integration for the first time, on its tile, click **Configure**.

  ![Configure button](images/toolchain_tile_configure.png)

 When you are finished configuring the tool integration, click **Save Integration**.
 
1. If you need to update a tool integration's configuration, on its tile, click the menu to access the configuration options.

  ![Configuration menu](images/toolchain_tile_menu.png)
 
 When you are finished updating the settings, click **Save Integration**.

## Adding a tool integration
{: #adding_a_tool_integration}

You can add and configure tool integrations for your toolchain.

1. On the DevOps dashboard, on the **Toolchains** tab, click a toolchain to open its Tool Integrations page. Alternatively, on the app's Overview page, on the Continuous Delivery tile, click **View Toolchain**, and then click **Tool Integrations**.
1. To see a list of tool integrations to add, click the add button (+).
1. Click a tool integration that you want to add.
1. Enter any required information to configure the tool integration. 
1. Click **Create Integration** to add the tool integration to your toolchain.

## Deleting a tool integration
{: #deleting_a_tool_integration}

If you delete a tool integration from your toolchain, the deletion cannot be undone. 

1. On the DevOps dashboard, on the **Toolchains** tab, click a toolchain to open its Tool Integrations page. Alternatively, on the app's Overview page, on the Continuous Delivery tile, click **View Toolchain**, and then click **Tool Integrations**.
1. On the tile for the tool integration that you want to delete, click the menu to access the configuration options.
1. To delete the tool integration from your toolchain, click **Delete**.
1. Confirm by clicking **Delete**.  

## Managing access
{: #managing_access}

You can grant users access to a toolchain by adding them to the organization (org) that the toolchain is associated with. Each toolchain is associated with a specific org, and any user that is a member of that org can access the associated toolchains. Click the **{{site.data.keyword.avatar}}** icon ![Avatar icon](../icons/i-avatar-icon.svg) in the menu bar to open the Account and Support widget and view the org that you are currently working in. Switch to a different org to access a different set of toolchains.

<!--CA: Commenting out the content on authentication for Interconnect since it applies to GitHub Enterprise. This content can be exposed again when GHE is supported for the Dedicated Beta 2.-->

<!--You have three authentication options for your Bluemix dedicated environment: LDAP, SAML, or Web ID. 

**Important:** For this beta, Web ID authentication requires additional user management on GitHub Enterprise.

If you use LDAP or SAML authentication in your Bluemix dedicated environment, when you add users to your Bluemix org and spaces, the users can log in to GitHub Enterprise by using their Bluemix ID and password, and accounts are created for them. When you add users to your Bluemix org and spaces, they are not automatically added to the GitHub Enterprise repo. Someone who has admin privileges for the repo must add them.  

If you use Web ID authentication, when you add users to your Bluemix org and spaces, a GitHub Enterprise site administrator must set up a GitHub Enterprise account for those users. Alternatively, new users can create a toolchain, in which case a GitHub Enterprise account is created for them. However, if those users want to access repos that are associated with toolchains besides their own, they must be granted access to those repos.

To add a user: -->

1. On the DevOps dashboard, on the **Toolchains** tab, click the toolchain to manage, and then click **Manage**. Alternatively, on the app's Overview page, on the Continuous Delivery tile, click **View Toolchain**, and then click **Manage**.  
1. Click the link to your organization. 
1. On the Manage Organizations page, click **Invite a User** and type the user's email address.
1. If you want to give advanced permissions to manage users in {{site.data.keyword.Bluemix_notm}} orgs, select one or more of the **Manager**, **Billing Manager**, or **Auditor** check boxes.
1. Click **INVITE**.
1. Click **SAVE**.

## Deleting a toolchain
{: #deleting_a_toolchain}

You can delete a toolchain and specify which of the associated tool integrations you want to delete. When you delete a toolchain, the deletion cannot be undone.

1. On the DevOps dashboard, on the **Toolchains** tab, click the toolchain to delete, and then click **Manage**. Alternatively, on the app's Overview page, on the Continuous Delivery tile, click **View Toolchain**, and then click **Manage**.
1. Click **Delete Toolchain** and review or adjust the tool integrations that you are deleting.
1. Confirm the deletion by typing the name of the toolchain and clicking **Delete**.  

 **Tip**: When you delete a GitHub tool integration, the associated GitHub repo is not deleted from GitHub. You must manually remove the repo from GitHub.h
