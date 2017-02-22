---

copyright:
  years: 2015, 2017
lastupdated: "2017-2-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Using toolchains
{: #toolchains-using}

Toolchains are available in the Public and Dedicated environments on {{site.data.keyword.Bluemix}}. You can use a toolchain to be productive in your daily development, deployment, and operations work. After you set up a toolchain, you can add, delete, or configure tool integrations and manage access to the toolchain. On {{site.data.keyword.Bluemix_notm}} Public, toolchains are available in the US South region only.
{: shortdesc}

## Configuring a tool integration
{: #configuring_a_tool_integration}

If you deferred the configuration of a tool integration when you created a toolchain, a **Configure** button is shown on its card. If you configured a tool integration when you created a toolchain, you can update the configuration settings.

1. On the DevOps dashboard, on the **Toolchains** page, click a toolchain to open its Overview page. Alternatively, on the app's Overview page, on the Continuous delivery card, click **View Toolchain**, and then click **Overview**.
1. If you need to configure a tool integration for the first time, on its card, click **Configure**.

  ![Configure button](images/toolchain_tile_configure.png)

 When you are finished configuring the tool integration, click **Save Integration**.
 
1. If you need to update a tool integration's configuration, on its card, click the menu to access the configuration options.

  ![Configuration menu](images/toolchain_tile_menu.png)
 
 **Tip**: A few of the tool integrations are preconfigured and don't require any configuration parameters. You can update the configuration settings for only the tool integrations that you configured.
 
 When you are finished updating the settings, click **Save Integration**.

## Adding a tool integration
{: #adding_a_tool_integration}

You can add and configure tool integrations for your toolchain. The available tool integrations differ depending on whether you use {{site.data.keyword.Bluemix_notm}} Public or {{site.data.keyword.Bluemix_notm}} Dedicated.

1. On the DevOps dashboard, on the **Toolchains** page, click a toolchain to open its Overview page. Alternatively, on the app's Overview page, on the Continuous delivery card, click **View Toolchain**, and then click **Overview**.
1. To see a list of tool integrations to add, click **Add a Tool**.
1. Click a tool integration that you want to add.
1. Enter any required information to configure the tool integration. 
1. Click **Create Integration** to add the tool integration to your toolchain.

## Deleting a tool integration
{: #deleting_a_tool_integration}

If you delete a tool integration from your toolchain, the deletion cannot be undone. 

1. On the DevOps dashboard, on the **Toolchains** page, click a toolchain to open its Overview page. Alternatively, on the app's Overview page, on the Continuous delivery card, click **View Toolchain**, and then click **Overview**.
1. On the card for the tool integration that you want to delete, click the menu to access the configuration options.
1. To delete the tool integration from your toolchain, click **Delete**.
1. Confirm by clicking **Delete**.  

## Managing access
{: #managing_access}

You can grant users access to a toolchain by adding them to the organization (org) that the toolchain is associated with. Each toolchain is associated with a specific org, and any user that is a member of that org can access the associated toolchains. The org that you are currently working in is displayed in the menu bar. Click the org and then switch to a different org to access a different set of toolchains.

If you are using {{site.data.keyword.Bluemix_notm}} Dedicated for {{site.data.keyword.ghe_short}}, when you add users to your {{site.data.keyword.Bluemix_notm}} org and spaces, the users can log in to {{site.data.keyword.ghe_short}} by using their {{site.data.keyword.Bluemix_notm}} ID and password. When the users log in, accounts are created for them. When you add users to your {{site.data.keyword.Bluemix_notm}} org and spaces, they are not automatically added to the {{site.data.keyword.ghe_short}} repo. Someone who has admin privileges for the repo must add them. For more information, see [Using Dedicated GitHub Enterprise](/docs/services/ghededicated/index.html){: new_window}. If you are using your own managed version of {{site.data.keyword.ghe_short}}, follow your internal procedures.

To add a user, follow these steps:

1. On the DevOps dashboard, on the **Toolchains** page, click the toolchain to manage, and then click **Manage**. Alternatively, on the app's Overview page, on the Continuous delivery card, click **View Toolchain**, and then click **Manage**.  
1. Click the link to your org. 
1. On the Manage Organizations page, click **Invite a User**, and type the user's email address.
1. If you want to give advanced permissions to manage users in {{site.data.keyword.Bluemix_notm}} orgs, select one or more of the **Manager**, **Billing Manager**, or **Auditor** check boxes. For more information, see [Managing team members and roles](/docs/admin/users_roles.html){: new_window}.
1. Click **INVITE**.
1. Click **SAVE**.

## Deleting a toolchain
{: #deleting_a_toolchain}

You can delete a toolchain and specify which of the associated tool integrations you want to delete. When you delete a toolchain, the deletion cannot be undone.

1. On the DevOps dashboard, on the **Toolchains** page, click the toolchain to delete, and then click **Manage**. Alternatively, on the app's Overview page, on the Continuous delivery card, click **View Toolchain**, and then click **Manage**.
1. Click **Delete Toolchain** and review or adjust the tool integrations that you are deleting.
1. Confirm the deletion by typing the name of the toolchain and clicking **Delete**.  

 **Tip**: When you delete a GitHub or {{site.data.keyword.ghe_short}} tool integration, the associated repo is not deleted from GitHub or {{site.data.keyword.ghe_short}}. You must manually remove the repo from GitHub or {{site.data.keyword.ghe_short}}.


# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}

* [Create and use your first toolchain![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Create a custom toolchain![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Create a toolchain that includes {{site.data.keyword.DRA_short}}![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_devops_insights){:new_window}
* [Create and use a microservices toolchain![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}
* [Create a toolchain from a template on {{site.data.keyword.Bluemix_notm}} Dedicated![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Create a toolchain from an app on {{site.data.keyword.Bluemix_notm}} Dedicated![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Related Links
{: #general}

* [{{site.data.keyword.contdelivery_full}}![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/deliver/tool_continuous_delivery/){:new_window}
* [Empty toolchain![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/toolchains/toolchain_empty){:new_window}
* [Microservices toolchain![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple Cloud Foundry toolchain![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [Simple Cloud Foundry toolchain with {{site.data.keyword.DRA_short}}![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/toolchains/toolchain_devops_insights){:new_window}
* [Simple container toolchain![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/toolchains/toolchain_simple_container){:new_window}
* [Simple secure container toolchain![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/toolchains/toolchain_simple_secure_container){:new_window}
* [IBM Bluemix Garage Method![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method){:new_window}
