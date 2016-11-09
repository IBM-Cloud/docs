---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Getting started with toolchains (Beta)
{: #toolchains_getting_started}

Last updated: 2 November 2016
{: .last-updated}  

Toolchains are available in the Public and Dedicated environments on {{site.data.keyword.Bluemix}}. You can create a toolchain in two ways: use a template to create a toolchain or create a toolchain from an app. On {{site.data.keyword.Bluemix_notm}} Public, toolchains are available in the US South region only.
{: shortdesc}

##Getting started with toolchains: Public
{: #getting_started_public}

**Note:** Make sure that you are working in the New Bluemix experience by checking the top banner.

 * If you see a message about trying the new Bluemix, you are working in the Classic Bluemix experience. Click the link to open the New Bluemix experience.
 * If you don't see that message, you are working in the New Bluemix experience already.

Each toolchain is associated with a specific organization (org) and any user that is a member of that org can access its associated toolchains. Before you create a toolchain, make sure that you are working in the org where you want to create the toolchain. The org that you are currently working in is displayed in the menu bar. To switch to another org, click the org in the menu bar and then select the org that you want to switch to.

###Creating a toolchain from a template   
{: #creating_a_toolchain_from_a_template}

You can use a template as a starting point to [create a toolchain (Link opens in a new window)](https://console.ng.bluemix.net/devops/create){: new_window} that includes a specific set of tool integrations. Learn more about how to use the templates from the [IBM Bluemix Garage Method (Link opens in a new window)](https://www.ibm.com/devops/method/category/tools){:new_window}.

1. If you are creating your first toolchain, make sure that toolchains are enabled in your org:
   1. Open the DevOps dashboard and click the **Toolchains** page.
   2. If the **Enable Toolchains** button is shown, click it, and follow the prompts to create your toolchain.
   3. If the **Enable Toolchains** button isn't shown, toolchains are already enabled. Continue to step 2.
1. On the DevOps dashboard, on the **Toolchains** page, click **Create a Toolchain**.
1. Click a toolchain template. For example, to use an online store sample to create the toolchain, click **Microservices toolchain**. 
1. On the toolchain creation page, review the diagram of the toolchain that you are about to create. The diagram shows each tool integration in its lifecycle phase in the toolchain. The diagram in the following image is an example. When you create a toolchain, the diagram shows each tool integration that is part of the toolchain.
![Toolchain diagram](images/toolchain_diagram.png)

1. Review the default information for the toolchain settings. The toolchain's name identifies it in {{site.data.keyword.Bluemix_notm}}. If you already have a toolchain with that name, or if you want to use a different name, change the toolchain's name.  
1. In the Configurable Integrations section, select each tool integration that you want to configure for your toolchain. Some tool integrations do not require any configuration. For information about configuring the tool integrations, see [Configuring tool integrations (Link opens in a new window)](../toolchains/toolchains_integrations.html){: new_window}.
1. Click **Create**.  Several steps run automatically to set up your toolchain:

 * The toolchain is created.
 * If you configured the Delivery Pipeline tool integration, the pipelines are triggered.
 * If you configured the Sauce Labs tool integration, the Sauce Labs integration is configured to add jobs to the pipelines and run tests.
 * If you configured the PagerDuty tool integration, the PagerDuty integration is configured to send notifications to the channel that you configured in Slack. These notifications indicate when a problem occurs.
 * If you configured the Slack tool integration, the Slack integration is configured to send notifications to the channel that you configured in Slack. These notifications indicate the progress of the deployment; for example, `Connected with Project XYZ`, `Pipeline Configured`, and `Stage 'build' started`.
 * If you configured the GitHub tool integration, the sample GitHub repo is cloned into your GitHub account.


###Creating a toolchain from an app
{: #creating_a_toolchain_from_an_app}

You can create a toolchain from your app. The toolchain can support continuous development, deployment, monitoring, and more, and it is associated with your app. Each app can be associated with a toolchain. When you push changes to the toolchain's GitHub repo, the pipeline automatically builds and deploys the app.  

1. If you are creating your first toolchain, make sure that toolchains are enabled in your org:
   1. Open the DevOps dashboard and click the **Toolchains** page.
   2. If the **Enable Toolchains** button is shown, click it, and follow the prompts to create your toolchain.
   3. If the **Enable Toolchains** button isn't shown, toolchains are already enabled. Continue to step 2.
1. On your app's Overview page, on the Continuous Delivery tile, click **Enable**. Alternatively, in the {{site.data.keyword.Bluemix_notm}} Classic Experience, in the upper-right corner of your app's Overview page, click **Add Toolchain**. Your app is configured for continuous delivery from a new GitHub repo that is populated with the app starter code.
1. On the toolchain creation page, review the diagram of the toolchain that you are about to create. The diagram shows each tool integration in its lifecycle phase in the toolchain.
1. Review the default information for the toolchain settings. The toolchain's name identifies it in {{site.data.keyword.Bluemix_notm}}. If you already have a toolchain with that name, or if you want to use a different name, change the toolchain's name.
1. In the Configurable Integrations section, select each tool integration that you want to configure for your toolchain. Some tool integrations do not require any configuration. For information about configuring the tool integrations, see [Configuring tool integrations (Link opens in a new window)](../toolchains/toolchains_integrations.html){: new_window}.
1. Click **Create**.  Several steps run automatically to set up your toolchain:

 * The toolchain is created.
 * If you configured the Delivery Pipeline tool integration, the pipelines are triggered.
 * If you configured the Sauce Labs tool integration, the Sauce Labs integration is configured to add jobs to the pipelines and run tests.
 * If you configured the PagerDuty tool integration, the PagerDuty integration is configured to send notifications to the channel that you configured in Slack. These notifications indicate when a problem occurs.
 * If you configured the Slack tool integration, the Slack integration is configured to send notifications to the channel that you configured in Slack. These notifications indicate the progress of the deployment; for example, `Connected with Project XYZ`, `Pipeline Configured`, and `Stage 'build' started`.
 * If you configured the GitHub tool integration, the sample GitHub repo is cloned into your GitHub account.


##Getting started with toolchains: Dedicated
{: #getting_started_dedicated}

Each toolchain is associated with a specific organization (org) and any user that is a member of that org can access its associated toolchains. Before you create a toolchain, click the **{{site.data.keyword.avatar}}** icon ![Avatar icon](../icons/i-avatar-icon.svg) in the menu bar to open the Account and Support widget and view the org that you are working in. If that org is not the org where you want to create the toolchain, switch to another org.

###Creating a toolchain from a template   
{: #creating_a_toolchain_from_a_template_dedicated}

You can use a template as a starting point to create a toolchain that includes a specific set of tool integrations.

1. If you are creating your first toolchain, make sure that toolchains are enabled in your org:
   1. Open the DevOps dashboard and click the **Toolchains** tab.
   2. If the **Enable Toolchains** button is shown, click it, and follow the prompts to create your toolchain.
   3. If the **Enable Toolchains** button isn't shown, toolchains are already enabled. Continue to step 2.
1. On the {{site.data.keyword.Bluemix_notm}} Dashboard, on the **DEVOPS** tab, click the add button (+) to create a toolchain.
1. Click a toolchain template. For example, to create a simple toolchain to deploy a new Cloud Foundry app, click **Simple Cloud Foundry toolchain**. 
1. On the toolchain creation page, review the diagram of the toolchain that you are about to create. The diagram shows each tool integration in its lifecycle phase in the toolchain. The diagram in the following image is an example. When you create a toolchain, the diagram shows each tool integration that is part of the toolchain.
![Dedicated toolchain diagram](images/toolchain_dedicated_diagram.png)

1. Review the default information for the toolchain settings. The toolchain's name identifies it in {{site.data.keyword.Bluemix_notm}}. If you already have a toolchain with that name, or if you want to use a different name, change the toolchain's name.  
1. In the Configurable Integrations section, select each tool integration that you want to configure for your toolchain. Some tool integrations do not require any configuration. For information about configuring the tool integrations, see [Configuring tool integrations (Link opens in a new window)](../toolchains/toolchains_integrations.html){: new_window}.
1. Click **Create**.  Several steps run automatically to set up your toolchain:

 * The toolchain is created.
 * If you configured the Delivery Pipeline tool integration, the pipelines are triggered.
 * If you configured the GitHub Enterprise tool integration, the sample GitHub Enterprise repo is cloned into your GitHub Enterprise account.


###Creating a toolchain from an app
{: #creating_a_toolchain_from_an_app_dedicated}

You can create a toolchain from your app. The toolchain can support continuous development, deployment, monitoring, and more, and it is associated with your app. Each app can be associated with a toolchain. When you push changes to the toolchain's GitHub Enterprise repo, the pipeline automatically builds and deploys the app.  

1. If you are creating your first toolchain, make sure that toolchains are enabled in your org:
   1. Open the DevOps dashboard and click the **Toolchains** tab.
   2. If the **Enable Toolchains** button is shown, click it, and follow the prompts to create your toolchain.
   3. If the **Enable Toolchains** button isn't shown, toolchains are already enabled. Continue to step 2.
1. In the upper-right corner of your app's Overview page, click **Add Toolchain**. Your app is configured for continuous delivery from a new GitHub Enterprise repo that is populated with the app starter code.
1. On the toolchain creation page, review the diagram of the toolchain that you are about to create. The diagram shows each tool integration in its lifecycle phase in the toolchain.
1. Review the default information for the toolchain settings. The toolchain's name identifies it in {{site.data.keyword.Bluemix_notm}}. If you already have a toolchain with that name, or if you want to use a different name, change the toolchain's name.
1. In the Configurable Integrations section, select each tool integration that you want to configure for your toolchain. Some tool integrations do not require any configuration. For information about configuring the tool integrations, see [Configuring tool integrations (Link opens in a new window)](../toolchains/toolchains_integrations.html){: new_window}.
1. Click **Create**.  Several steps run automatically to set up your toolchain:

 * The toolchain is created.
 * If you configured the Delivery Pipeline tool integration, the pipelines are triggered.
 * If you configured the GitHub Enterprise tool integration, the sample GitHub Enterprise repo is cloned into your GitHub Enterprise account.


##Viewing a toolchain
{: #viewing_a_toolchain}

After you configure the toolchain and its tool integrations, you can view a visual representation of the toolchain.

* If you use {{site.data.keyword.Bluemix_notm}} Public, on the DevOps dashboard, on the **Toolchains** page, click a toolchain to open its Overview page. Alternatively, on the app's Overview page, on the Continuous Delivery tile, click **View Toolchain**. Then, click **Overview**. 
   
* If you use {{site.data.keyword.Bluemix_notm}} Dedicated, on the Dashboard, on the **DEVOPS** tab, click the toolchain to open its Tool Integrations page. Alternatively, in the upper-right corner of the app's Overview page, click **View Toolchain**.

* To access a tool integration that is in your toolchain, click the tool's tile. 
 
 **Tip**: If you have more than one GitHub or GitHub Enterprise repo, you might have multiple tiles for the same tool integration because each repo is represented by its own tile.


 <!-- The toolchain in the following image is an example. When you create your own toolchain, the visual representation of the toolchain shows the tool integrations that you configure.
![Sample toolchain](images/toolchain.png) -->


# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}

* [Create an application with three microservices (Beta) (Link opens in a new window)](https://www.ibm.com/devops/method/tutorials/tutorial_microservices_part1){:new_window}
* [Create a toolchain from a template on {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) (Link opens in a new window)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Create a toolchain from an app on {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) (Link opens in a new window)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Related Links
{: #general}

* [Microservices toolchain (Beta) (Link opens in a new window)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple toolchain (Beta) (Link opens in a new window)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method (Link opens in a new window)](https://www.ibm.com/devops/method){:new_window}
