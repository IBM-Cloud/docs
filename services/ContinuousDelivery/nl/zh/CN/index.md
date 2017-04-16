---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.contdelivery_short}} 入门
{: #cd_getting_started}

上次更新时间：2016 年 11 月 18 日
{: .last-updated}  

使用 {{site.data.keyword.contdelivery_full}} 以采用 DevOps 方法，这包括自动构建和部署应用程序的工具链。首先，可以创建简单部署工具链来支持开发、部署和操作任务。
{: shortdesc}

通过从 {{site.data.keyword.Bluemix_notm}}“目录”中选择 {{site.data.keyword.contdelivery_short}} 的服务磁贴来创建该服务的实例后，可以选择希望如何开始使用该服务。![Continuous Delivery 欢迎页面](images/cd_landing_page.png)

 * 要使用自动化管道迅速着手使用应用程序并部署应用程序，请在“开始使用管道”部署中，单击**[从这里开始](#starting_with_a_pipeline)**。您可以日后添加更多工具。 
 * 要从模板创建并配置持续交付工具链，请单击**[从这里开始](#starting_from_a_toolchain_template)**。工具链将集成用于规划、开发、部署管道和管理应用程序的工具。您可以随时在工具链中添加或除去工具。
 * 如果已经具有工具链，请在“从工具链模板开始”部分中，单击**查看工具链**。有关使用工具链的更多信息，请参阅[在 Bluemix Public 上使用工具链](/docs/services/ContinuousDelivery/toolchains_using.html){: new_window}。

## 开始使用管道
{: #starting_with_a_pipeline}

管道可自动执行构建、部署等操作。要开始使用自动化管道，请选择模板，并提供 GitHub 存储库的位置。

要[创建管道（在新窗口中打开链接）](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window}（管道已配置为部署 Cloud Foundry 应用程序），请执行以下步骤：

1. 单击 **Cloud Foundry**。
1. 如果要对管道使用其他名称，请更改其缺省名称。管道名称使其可在 {{site.data.keyword.Bluemix_notm}} 中进行识别。 
1. 如果要对应用程序使用其他名称，请更改其缺省名称。应用程序名称使其可在 {{site.data.keyword.Bluemix_notm}} 中进行识别。这是管道部署到的应用程序的名称。 
1. 如果没有工具链，那么将为您创建具有缺省名称的工具链。如果要对工具链使用其他名称，请更改其名称。管道由工具链进行管理。使用工具链，您可以通过与其他工具和服务相集成来扩展管道的功能。 

 **提示**：管道和工具链属于组织。如果您属于具有工具链的组织，那么即便这些工具链不是您创建的，您也仍可以使用。
 
1. 选择要使用的工具链，或输入要创建的新工具链的名称。
1. 提供 GitHub 存储库的位置。

 **提示**：如果您未授权 {{site.data.keyword.Bluemix_notm}} 访问 GitHub，那么系统将提示您单击**授权**，以转至 GitHub Web 站点。如果您没有活动 GitHub 会话，那么系统会提示您登录。单击**授权应用程序**，以允许 {{site.data.keyword.Bluemix_notm}} 访问 GitHub 帐户。如果您具有活动 GitHub 会话但最近未输入过密码，那么系统可能会提示您输入 GitHub 密码以进行确认。

   * 如果您具有 GitHub 存储库且想要使用该存储库，那么对于存储库类型，请选择**链接**。搜索该存储库的位置，或者从可用存储库列表中选择该存储库。
   
   * 如果要创建空的 GitHub 存储库，那么对于存储库类型，请选择**新建**。输入存储库的名称。
   
   * 如果要创建 GitHub 存储库的克隆，那么对于存储库类型，请选择**复制**。搜索该存储库的位置，或者从可用存储库列表中选择该存储库。
   
   * 如果要派生 GitHub 存储库以便您可以通过拉出请求来提供更改，请选择**派生**。搜索该存储库的位置，或者从可用存储库列表中选择该存储库。
 
1. 单击**创建**。这将创建和配置管道，并将其显示在工具链的“概述”页面上。
 ![“管道”磁贴](images/cd_pipeline.png)
 
要创建不包含任何预配置阶段的[空管道（在新窗口中打开链接）](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window}，请执行以下操作：

1. 单击**定制**。
1. 如果要对管道使用其他名称，请更改其缺省名称。管道名称使其可在 {{site.data.keyword.Bluemix_notm}} 中进行识别。 
1. 如果没有工具链，那么将为您创建具有缺省名称的工具链。如果要对工具链使用其他名称，请更改其名称。管道由工具链进行管理。使用工具链，您可以通过与其他工具和服务相集成来扩展管道的功能。
1. 选择要使用的工具链，或输入要创建的新工具链的名称。
1. 单击**创建**。这将创建空管道，并将其表示为工具链“概述”页面上的磁贴。

## 从工具链模板开始
{: #starting_from_a_toolchain_template}

要从[模板（在新窗口中打开链接）](https://console.ng.bluemix.net/devops/create){: new_window}创建并配置持续交付工具链，请执行以下操作：

1. 在**创建工具链**页面上，单击工具链模板。  
1. 复查您要创建的工具链的图。该图显示工具链中处于其生命周期阶段的每一个工具集成。以下图像中的图是示例。创建工具链时，该图显示属于工具链的每一个工具集成。
![Toolchain_diagram](images/toolchain_diagram.png)
1. 复查工具链设置的缺省信息。工具链名称使其可在 {{site.data.keyword.Bluemix_notm}} 中进行识别。如果要使用其他名称，请更改工具链的名称。
1. 在“可配置的集成”部分中，选择要为工具链配置的每一个工具集成。有些工具集成无需进行配置。有关配置工具集成的信息，请参阅[配置工具集成](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}。
1. 单击**创建**。此时将自动运行数个步骤，以设置工具链：

 * 创建工具链。
 * 如果已配置 Delivery Pipeline 工具集成，那么会创建并触发管道。
 * 如果已配置 Sauce Labs 工具集成，那么 Sauce Labs 会设置为向管道添加作业，并运行测试。
 * 如果已配置 PagerDuty 工具集成，那么 PagerDuty 会设置为向指定的服务发送警报通知。 
 * 如果已配置 Slack 工具集成，那么 Slack 会设置为向指定的通道发送有关部署状态的通知。 
 * 如果已配置 GitHub 工具集成，那么样本 GitHub 存储库会克隆到 GitHub 帐户。 

# 相关链接
{: #rellinks}

## 教程和样本
{: #samples}

* [Create and use your first toolchain（在新窗口中打开链接）](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Create a custom toolchain（在新窗口中打开链接）](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Create an application with three microservices（在新窗口中打开链接）](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}

## 相关链接
{: #general}

* [Microservices toolchain（在新窗口中打开链接）](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple toolchain（在新窗口中打开链接）](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method（在新窗口中打开链接）](https://www.ibm.com/devops/method){:new_window}
