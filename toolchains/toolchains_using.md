---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Using toolchains (Experimental)
{: #toolchains-using}

*Last updated: 18 April 2016*

Use an existing toolchain to help with your day-to-day work. You can add or delete tool integrations from a toolchain, configure existing or new tool integrations, and manage access to the toolchain.  
{: shortdesc}

**Important**: This capability is experimental. Toolchains might not be stable and might change in ways that are not compatible with earlier versions. They are not recommended for use in production environments. To use toolchains, you must make a one-time [request for access](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window}.  Toolchains are available in the Dallas region only.

## Configuring a tool integration
{: #configuring_a_tool_integration}

You can configure a new tool integration or update the configuration settings for a tool integration that was configured for your toolchain.

1. On the app's Overview page, on the Continuous Delivery tile, click **View Toolchain**, and then click **Tool Integrations**. Alternatively, on the DevOps dashboard, on the **Toolchains** tab, click the toolchain that you want to work with to open the Tool Integrations page.
2. Locate the tile for the tool integration that you want to configure for the toolchain. 
3. If you need to configure the tool integration for the first time, click **Configure**. Enter the required configuration settings, and click **Save Integration**.
4. If you need to update the tool integration's configuration, click the menu to access the configuration options for the tool integration. Update the settings, and click **Save Integration**.

 **Note**: You cannot update the repo for a GitHub tool integration after it is configured. To use a different repo, you must delete the current GitHub tool integration from your toolchain, add a GitHub tool integration to your toolchain, and configure the tool integration to use the new repo.

## Adding a tool integration
{: #adding_a_tool_integration}

Add and configure a tool integration for your toolchain.

1. On the app's Overview page, on the Continuous Delivery tile, click **View Toolchain**, and then click **Tool Integrations**. Alternatively, on the DevOps dashboard, on the **Toolchains** tab, click the toolchain that you want to work with to open the Tool Integrations page.
2. To see a list of tools to add, click the add button (+).
3. Click the tool integration that you want to add to your toolchain.
4. Enter any required information to configure the tool integration. 
5. Click **Create Integration** to add the tool integration to your toolchain.

## Deleting a tool integration
{: #deleting_a_tool_integration}

You can remove a tool integration from your toolchain or delete the tool integration from your app. 

1. On the app's Overview page, on the Continuous Delivery tile, click **View Toolchain**, and then click **Tool Integrations**. Alternatively, on the DevOps dashboard, on the **Toolchains** tab, click the toolchain that you want to work with to open the Tool Integrations page.
2. Locate the tile for the tool integration that you want to delete from the toolchain. 
3. Click the menu to access the configuration options for the tool integration.
4. If you want to remove the tool integration from your toolchain, click **Delete**.
5. If you want to also delete the tool integration from your app, select the **Delete this tool in addition to removing it from the toolchain** check box.
5. Confirm by clicking **DELETE**.

## Managing access
{: #managing_access}

You can grant a user access to a toolchain by adding them to the organization (org) that the toolchain is associated with. Each toolchain is associated with a specific org and any user that is a member of that org can access the associated toolchains. If you switch to a different org, you can access a different set of toolchains.

<!--CA: Commenting out the content on authentication for Interconnect since it applies to GitHub Enterprise. This content can be exposed again when GHE is supported for the Dedicated Beta 2.-->

<!--You have three authentication options for your Bluemix dedicated environment: LDAP, SAML, or Web ID. 

**Important:** For this beta, Web ID authentication requires additional user management on GitHub Enterprise.

If you use LDAP or SAML authentication in your Bluemix dedicated environment, when you add users to your Bluemix org and spaces, the users can log in to GitHub Enterprise by using their Bluemix ID and password, and accounts are created for them. When you add users to your Bluemix org and spaces, they are not automatically added to the GitHub Enterprise repo. Someone who has admin privileges for the repo must add them.  

If you use Web ID authentication, when you add users to your Bluemix org and spaces, a GitHub Enterprise site administrator must set up a GitHub Enterprise account for those users. Alternatively, new users can create a toolchain, in which case a GitHub Enterprise account is created for them. However, if those users want to access repos that are associated with toolchains besides their own, they must be granted access to those repos.

To add a user: -->

1. On the app's Overview page, on the Continuous Delivery tile, click **View Toolchain**, and then click **Manage**. Alternatively, on the DevOps dashboard, on the **Toolchains** tab, click the toolchain that you want to work with, and then click **Manage**.  

2. Click the link to your organization. 

3. On the Manage Organizations page, click **ADD USER**, type the user's name, and click **ADD**.

   **Note:** The user name might be an email address.
   
4. If you want to give advanced permissions to the user, select one or more of the **MANAGER**, **BILLING MANAGER**, or **AUDITOR** check boxes.

5. Click **SAVE**.

## Deleting a toolchain
{: #deleting_a_toolchain}

You can delete a toolchain and specify which of the associated tool integrations you want to delete.

1. On the app's Overview page, on the Continuous Delivery tile, click **View Toolchain**, and then click **Manage**. Alternatively, on the DevOps dashboard, on the **Toolchains** tab, click the toolchain that you want to work with, and then click **Manage**. 
2. Click **Delete Toolchain** and review the tool integrations that you are deleting.
3. Confirm the deletion by typing the name of the toolchain and clicking **DELETE**.

 **Tip**: When you delete a GitHub tool integration, the associated GitHub repo is not deleted from GitHub. You must manually remove the repo from GitHub by using the GitHub user interface.
