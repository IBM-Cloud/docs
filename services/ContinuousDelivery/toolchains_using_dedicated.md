---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Using toolchains on {{site.data.keyword.Bluemix_notm}} Dedicated
{: #toolchains-using_dedicated}

Last updated: 16 November 2016
{: .last-updated}

You can use a toolchain to be productive in your daily development, deployment, and operations work. After you set up a toolchain, you can add, delete, or configure tool integrations and manage access to the toolchain.
{: shortdesc}

## Configuring a tool integration
{: #configuring_a_tool_integration_dedicated}

If you deferred the configuration of a tool integration when you created a toolchain, a **Configure** button is shown on its tile. If you configured a tool integration when you created a toolchain, you can update the configuration settings.

1. On the Dashboard, on the **DEVOPS** tab, click the toolchain to open its Tool Integrations page. Alternatively, in the upper-right corner of the app's Overview page, click **View Toolchain**. Then, click **Tool Integrations**.
1. If you need to configure a tool integration for the first time, on its tile, click **Configure**.

  ![Configure button](images/toolchain_tile_configure.png)

 When you are finished configuring the tool integration, click **Save Integration**.
 
1. If you need to update a tool integration's configuration, on its tile, click the menu to access the configuration options.

  ![Configuration menu](images/toolchain_tile_menu.png)
 
 When you are finished updating the settings, click **Save Integration**.

## Adding a tool integration
{: #adding_a_tool_integration_dedicated}

You can add and configure tool integrations for your toolchain.

1. On the Dashboard, on the **DEVOPS** tab, click the toolchain to open its Tool Integrations page. Alternatively, in the upper-right corner of the app's Overview page, click **View Toolchain**. Then, click **Tool Integrations**.
1. To see a list of tool integrations to add, click the add button (+).
1. Click the tool integration to add.
1. Enter any required information to configure the tool integration. 
1. Click **Create Integration** to add the tool integration to your toolchain.

## Deleting a tool integration
{: #deleting_a_tool_integration}

If you delete a tool integration from your toolchain, the deletion cannot be undone. 

1. On the Dashboard, on the **DEVOPS** tab, click the toolchain to open its Tool Integrations page. Alternatively, in the upper-right corner of the app's Overview page, click **View Toolchain**. Then, click **Tool Integrations**.
1. On the tile for the tool integration to delete, click the menu to access the configuration options.
1. To delete the tool integration from your toolchain, click **Delete**.
1. Confirm by clicking **Delete**. 

## Managing access
{: #managing_access_dedicated}

You can grant users access to a toolchain by adding them to the organization (org) that the toolchain is associated with. Each toolchain is associated with a specific org, and any user that is a member of that org can access the associated toolchains. To view the org that you are currently working in, click the **{{site.data.keyword.avatar}}** icon ![Avatar icon](../icons/i-avatar-icon.svg) in the menu bar. To access a different set of toolchains, switch to a different org.

When you add users to your {{site.data.keyword.Bluemix}} org and spaces, the users can log in to GitHub Enterprise by using their {{site.data.keyword.Bluemix_notm}} ID and password. When the users log in, accounts are created for them. When you add users to your {{site.data.keyword.Bluemix_notm}} org and spaces, they are not automatically added to the GitHub Enterprise repo. Someone who has admin privileges for the repo must add them. For more information, see [Using Dedicated GitHub Enterprise](/docs/services/ghededicated/index.html){: new_window}.

To add a user, follow these steps: 

1. On the Dashboard, on the **DEVOPS** tab, click the toolchain to open its Tool Integrations page. Then, click **Manage**. Alternatively, in the upper-right corner of the app's Overview page, click **View Toolchain**. Then, click **Manage**.  
1. Click the link to your org. 
1. On the Manage Organizations page, click **Invite a User** and type the user's email address.
1. If you want to give advanced permissions to manage users in {{site.data.keyword.Bluemix_notm}} orgs, select one or more of the **Manager**, **Billing Manager**, or **Auditor** check boxes.
1. Click **INVITE**.
1. Click **SAVE**.

## Deleting a toolchain
{: #deleting_a_toolchain_dedicated}

You can delete a toolchain and specify which of its associated tool integrations you want to delete. When you delete a toolchain, the deletion cannot be undone.

1. On the Dashboard, on the **DEVOPS** tab, click the toolchain to open its Tool Integrations page. Then, click **Manage**. Alternatively, in the upper-right corner of the app's Overview page, click **View Toolchain**. Then, click **Manage**.
1. Click **Delete Toolchain** and review or adjust the tool integrations that you are deleting.
1. Confirm the deletion by typing the name of the toolchain and clicking **Delete**.

 **Tip**: When you delete a GitHub Enterprise tool integration, the associated GitHub Enterprise repo is not deleted from GitHub Enterprise. You must manually remove the repo from GitHub Enterprise.


# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}

* [Create and use your first toolchain (Link opens in a new window)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Create a custom toolchain (Link opens in a new window)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Create an application with three microservices (Link opens in a new window)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}
* [Create a toolchain from a template on {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) (Link opens in a new window)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Create a toolchain from an app on {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) (Link opens in a new window)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Related Links
{: #general}

* [Microservices toolchain (Link opens in a new window)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple toolchain (Link opens in a new window)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method (Link opens in a new window)](https://www.ibm.com/devops/method){:new_window}
