---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Getting started with {{site.data.keyword.contdelivery_short}}
{: #cd_getting_started}

Last updated: 9 November 2016
{: .last-updated}  

{{site.data.keyword.contdelivery_full}} allows your team to adopt a DevOps approach by delivering continuously using toolchains and automated build and deploy. You can create a simple deployment toolchain or a toolchain with a set of tool integrations that support development, deployment, and operations tasks. If you already have toolchains, you can view them to start working with them.
{: shortdesc}

**Tip**: To learn more about how to continuously design, deliver, and validate new function, see the [IBM Bluemix Garage Method (Link opens in a new window)](https://www.ibm.com/devops/method){:new_window}. Walk through the practices, architectures, tools, and toolchains using hands on samples to start your transformation.

After you select the {{site.data.keyword.contdelivery_short}} service instance tile from the {{site.data.keyword.Bluemix_notm}} Catalog, you can choose how you want to get started using {{site.data.keyword.contdelivery_short}}:

 * To get started quickly and deploy your app with an automated build and delivery pipeline, in the Start with a pipeline section, click **Start here**. You can add more tools later. 
 * To create and configure a continuous delivery toolchain from a template, in the Start from a toolchain template section, click **Start here**. The toolchain integrates tools for planning, developing, deploying, and managing your apps. You can always add or remove tools from your toolchains.
 * If you already have toolchains, in the Start from a toolchain template section, click **View your toolchains**. You can view and work with an existing toolchain.

##Starting with a pipeline
{: #starting_with_a_pipeline}

Pipelines automate builds, deployments, and more. To get started with an automated build and delivery pipeline, select a template and provide the location of your GitHub repository (repo).

To [create a pipeline (Link opens in a new window)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} that is configured to deploy a Cloud Foundry application:

1. Click **Cloud Foundry**.
1. The pipeline's name identifies it in {{site.data.keyword.Bluemix_notm}}. If you want to use a different name, change the pipeline's default name.
1. The app's name identifies it in {{site.data.keyword.Bluemix_notm}}. If you want to use a different name, change the app's default name.
1. If you don't have any existing toolchains, we'll create a toolchain for you. The toolchain will allow you to extend the capabilities of your pipeline by integrating with other tools and services. A default toolchain name is provided. If you want to use a different name, change the toolchain's name.
1. If you already have toolchains, select the toolchain that you want to use, or enter a name for the new toolchain that you want to create.
1. Provide the location of your GitHub repo:

 a. If you already have a GitHub repo and want to use it, for the repository type, select **Link**. Search for the location of the repo or select the repo from the list of available repos.
 
 b. If you want to create an empty GitHub repo, for the repository type, select **New**. Type a name for the repo.
 
 c. If you want to create a copy of a GitHub repo, for the repository type, select **Copy**. Search for the location of the repo or select the repo from the list of available repos.
 
 d. If you want to fork a GitHub repo so that you can contribute changes through pull requests, select **Fork**. Search for the location of the repo or select the repo from the list of available repos.
 
1. Click **Create**. The pipeline is created, configured, and represented as a tile on the Toolchain's Overview page. 
 ![Pipeline tile](images/cd_pipeline.png)
 
To [create an empty pipeline (Link opens in a new window)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} without any pre-configured stages:

1. Click **Custom**.
1. The pipeline's name identifies it in {{site.data.keyword.Bluemix_notm}}. If you want to use a different name, change the pipeline's default name.
1. If you don't have any existing toolchains, we'll create a toolchain for you. The toolchain will allow you to extend the capabilities of your pipeline by integrating with other tools and services. A default toolchain name is provided. If you want to use a different name, change the toolchain's name.
1. If you already have toolchains, select the toolchain that you want to use, or enter a name for the new toolchain that you want to create.
1. Click **Create**. An empty pipeline is created and represented as a tile on the Toolchain's Overview page.

##Starting from a toolchain template
{: #starting_from_a_toolchain_template}

To [create and configure a continuous delivery toolchain from a template (Link opens in a new window)](https://console.ng.bluemix.net/devops/create){: new_window}:

1. On the **Create a Toolchain** page, click a toolchain template. For example, to use an online store sample to create the toolchain, click **Microservices toolchain**. 
1. On the toolchain creation page, review the diagram of the toolchain that you are about to create. The diagram shows each tool integration in its lifecycle phase in the toolchain. The diagram in the following image is an example. When you create a toolchain, the diagram shows each tool integration that is part of the toolchain.
 ![Toolchain_diagram](images/toolchain_diagram.png)
1. Review the default information for the toolchain settings. The toolchain's name identifies it in {{site.data.keyword.Bluemix}}. If you want to use a different name, change the toolchain's name.
1. In the Configurable Integrations section, select each tool integration that you want to configure for your toolchain. Some tool integrations do not require any configuration. For information about configuring the tool integrations, see [Configuring tool integrations (Link opens in a new window)](../../toolchains/toolchains_integrations.html){: new_window}.
1. Click **Create**.  Several steps run automatically to set up your toolchain:

 * The toolchain is created.
 * If you configured the Delivery Pipeline tool integration, the pipelines are triggered.
 * If you configured the Sauce Labs tool integration, the Sauce Labs integration is configured to add jobs to the pipelines and run tests.
 * If you configured the PagerDuty tool integration, the PagerDuty integration is configured to send notifications to the channel that you configured in Slack. These notifications indicate when a problem occurs.
 * If you configured the Slack tool integration, the Slack integration is configured to send notifications to the channel that you configured in Slack. These notifications indicate the progress of the deployment; for example, `Connected with Project XYZ`, `Pipeline Configured`, and `Stage 'build' started`.
 * If you configured the GitHub tool integration, the sample GitHub repo is cloned into your GitHub account. 

##Viewing your toolchains
{: #viewing_your_toolchains}

You can view and work with existing toolchains:

1. On the DevOps dashboard, on the **Toolchains** page, click a toolchain to open its Overview page.
1. You can add, delete, or configure tool integrations and manage access to the toolchain. For more information about working with toolchains, see [Using toolchains on Bluemix Public (Link opens in a new window)](../../toolchains/toolchains_using.html){: new_window}.
1. To access a tool integration that is in your toolchain, click the tool's tile.

# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}

* [Create and use your first toolchain (Link opens in a new window)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Create a custom toolchain (Link opens in a new window)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Create an application with three microservices (Link opens in a new window)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}

## Related Links
{: #general}

* [Microservices toolchain (Link opens in a new window)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple toolchain (Link opens in a new window)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method (Link opens in a new window)](https://www.ibm.com/devops/method){:new_window}
