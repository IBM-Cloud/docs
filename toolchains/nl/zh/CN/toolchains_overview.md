---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 开始使用工具链（试验性）
{: #toolchains_getting_started}

*上次更新时间：2016 年 6 月 8 日*
{: .last-updated}  

工具链是支持开发、部署和操作任务的一组工具集成。这种集合起来的工具链的能力要远大于其个别工具集成的总和。
{: shortdesc}

您可以使用两种方法来创建工具链：使用模板创建工具链，或者通过应用程序创建工具链。根据您所使用的模板或工具链，工具链可能包括已经填充了应用程序入门模板代码的 GitHub 存储库和预配置的 Delivery Pipeline。当您将更改推送到工具链的 GitHub 存储库时，Delivery Pipeline 会自动构建应用程序，并将其部署到 {{site.data.keyword.Bluemix}}。

您可以使用工具链模板作为起始点，来创建具有一组特定工具集成的工具链，或者创建可以向其中添加工具集成的空工具链。

**重要信息**：此功能是试验性的。工具链可能不稳定，并且可能会发生变化而与较低版本不兼容。建议不要在生产环境中使用工具链。要使用工具链，您必须进行一次性的[访问请求](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window}。工具链仅在美国南部区域可用。


##通过模板创建工具链   
{: #creating_a_toolchain_from_a_template}

在访问工具链请求获得批准之后，您可以使用模板作为起始点，来创建包含一组特定工具集成的工具链。

1. 在 DevOps 仪表板的**工具链**选项卡上，单击**创建工具链**，以创建第一个工具链。如果您已经具有工具链，请单击添加按钮 (+)，以创建其他工具链。
1. 单击工具链模板。例如，要使用网上商店样本来创建工具链，请单击**微型服务工具链**。 
1. 在工具链创建页面上，复查您要创建的工具链的图。该图显示工具链中处于其生命周期阶段的每一个工具集成。以下图像中的图是示例。创建工具链时，该图显示属于工具链的每一个工具集成。
![工具链图](images/toolchain_diagram.png)

1. 复查工具链设置的缺省信息。工具链名称使其可在 {{site.data.keyword.Bluemix}} 中进行识别。如果您的工具链已经具有该名称，或者您想要使用不同的名称，请更改工具链的名称。  
1. 在“可配置的集成”部分中，选择要为工具链配置的每一个工具集成。有关配置工具集成的更多信息，请参阅[配置工具集成](../toolchains/toolchains_integrations.html){: new_window}。
1. 单击**创建**。此时将自动运行数个步骤，以设置工具链：

 * 创建工具链。
 * 如果已配置 Delivery Pipeline 工具集成，那么会触发管道。
 * 如果已配置 Sauce Labs 工具集成，那么 Sauce Labs 集成会配置为向管道添加作业，并运行测试。
 * 如果已配置 PagerDuty 工具集成，那么 PagerDuty 集成会配置为向您在 Slack 中配置的通道发送通知。这些通知指示何时发生问题。
 * 如果已配置 Slack 工具集成，那么 Slack 集成会配置为向您在 Slack 中配置的通道发送通知。这些通知指示部署的进度；例如，`已与项目 XYZ 连接`、`已配置管道`和`已启动“构建”阶段`。
 * 如果已配置 GitHub 工具集成，那么样本 GitHub 存储库会克隆到 GitHub 帐户。


##通过应用程序创建工具链
{: #creating_a_toolchain_from_an_app}

在访问工具链请求获得批准之后，您可以通过应用程序创建工具链。工具链可以支持持续开发、部署、监视等操作，且与应用程序相关联。每一个应用程序都可以与工具链相关联。当您将更改推送到工具链的 GitHub 存储库时，管道会自动构建和部署应用程序。  

1. 在应用程序“概述”页面的“持续交付”磁贴上，单击**添加工具链**。或者，在 Bluemix“典型经验”中，单击**添加 GIT**。此时，将会对您的应用程序进行配置，以便可通过填充应用程序入门模板代码的新 GitHub 存储库，进行持续交付。
1. 在工具链创建页面上，复查您要创建的工具链的图。该图显示工具链中处于其生命周期阶段的每一个工具集成。
1. 复查工具链设置的缺省信息。工具链名称使其可在 {{site.data.keyword.Bluemix}} 中进行识别。如果您的工具链已经具有该名称，或者您想要使用不同的名称，请更改工具链的名称。
1. 在“可配置的集成”部分中，选择要为工具链配置的每一个工具集成。有关配置工具集成的更多信息，请参阅[配置工具集成](../toolchains/toolchains_integrations.html){: new_window}。
1. 单击**创建**。此时将自动运行数个步骤，以设置工具链：

 * 创建工具链。
 * 如果已配置 Delivery Pipeline 工具集成，那么会触发管道。
 * 如果已配置 Sauce Labs 工具集成，那么 Sauce Labs 集成会配置为向管道添加作业，并运行测试。
 * 如果已配置 PagerDuty 工具集成，那么 PagerDuty 集成会配置为向您在 Slack 中配置的通道发送通知。这些通知指示何时发生问题。
 * 如果已配置 Slack 工具集成，那么 Slack 集成会配置为向您在 Slack 中配置的通道发送通知。这些通知指示部署的进度；例如，`已与项目 XYZ 连接`、`已配置管道`和`已启动“构建”阶段`。
 * 如果已配置 GitHub 工具集成，那么样本 GitHub 存储库会克隆到 GitHub 帐户。

 
##查看工具链
{: #viewing_a_toolchain}

配置完工具链和所有工具集成之后，您可以在“工具集成”页面中，查看工具链的可视化表示。

1. 在 DevOps 仪表板的**工具链**选项卡上，单击工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**，然后单击**工具集成**。
1. 复查页面，以查看工具链的可视化表示。
1. 要访问工具链中的工具集成，请单击工具磁贴。 
 
 **提示**：如果您具有多个 GitHub 存储库，那么相同的工具集成可能具有多个磁贴，因为每一个存储库需要其自己的管道。


 <!-- The toolchain in the following image is an example. When you create your own toolchain, the visual representation of the toolchain shows the tool integrations that you configure.
![Sample toolchain](images/toolchain.png) -->


# 相关连接
{: #rellinks}

## 教程与样本
{: #samples}

* [使用三个微型服务创建应用程序](https://www.ibm.com/devops/method/tutorials/tutorial_microservices_part1){:new_window}

## 相关连接
{: #general}

* [微型服务工具链（试验性）](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [简单工具链（试验性）](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM&reg; Bluemix&reg; Garage 方法](https://www.ibm.com/devops/method){:new_window}
