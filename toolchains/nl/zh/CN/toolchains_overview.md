---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 工具链（试验版）入门
{: #toolchains_getting_started}

上次更新时间：2016 年 8 月 17 日
{: .last-updated}  

工具链可在 {{site.data.keyword.Bluemix}} 上的 Public 和 Dedicated 环境中使用。可以通过两种方式创建工具链：使用模板创建工具链或通过应用程序创建工具链。
{: shortdesc}

**重要信息**：此功能是试验性的。工具链可能不稳定，并且可能会发生变化而与较低版本不兼容。因此，不建议在生产环境中使用工具链。在 {{site.data.keyword.Bluemix_notm}} Public 上，工具链只能在美国（南部）区域中使用。


##工具链入门：Public
{: #getting_started_public}

每个工具链都与一个特定组织相关联，属于该组织的任何用户都可以访问其关联工具链。创建工具链之前，请确保是在要创建工具链的组织中工作。要切换到其他组织，请单击菜单栏中的 **{{site.data.keyword.avatar}}** 图标 ![Avatar 图标](../icons/i-avatar-icon.svg) 以打开“帐户和支持”窗口小部件。

###通过模板创建工具链   
{: #creating_a_toolchain_from_a_template}

可以将模板用作工具链创建的起点，以包含一组特定的工具集成。

1. 如果是第一次创建工具链，请确保组织中已启用工具链：
   1. 打开 DevOps 仪表板，然后单击**工具链**选项卡。
   2. 如果显示了**启用工具链**按钮，请单击此按钮，并按照提示创建工具链。
   3. 如果未显示**启用工具链**按钮，说明工具链已经启用。请转至步骤 2。
1. 在 DevOps 仪表板的**工具链**选项卡上，单击“添加”按钮 (+) 来创建工具链。
1. 单击工具链模板。例如，要使用联机存储样本来创建工具链，请单击**微型服务工具链**。 
1. 在“工具链创建”页面上，查看要创建的工具链的图。此图显示了每个工具集成在工具链中的生命周期阶段。下图是示例。创建工具链时，此图会显示属于工具链的每个工具集成。
![工具链图](images/toolchain_diagram.png)

1. 查看工具链设置的缺省信息。工具链的名称在 {{site.data.keyword.Bluemix_notm}} 中对其进行标识。如果已经具有该名称的工具链，或者如果要使用其他名称，请更改工具链的名称。  
1. 在“可配置集成”部分中，选择要为工具链配置的每个工具集成。某些工具集成无需任何配置。有关配置工具集成的信息，请参阅[配置工具集成](../toolchains/toolchains_integrations.html){: new_window}。
1. 单击**创建**。有多个步骤会自动运行来设置工具链：

 * 这将创建工具链。
 * 如果配置了 Delivery Pipeline 工具集成，那么会触发管道。
 * 如果配置了 Sauce Labs 工具集成，那么 Sauce Labs 集成会配置为将作业添加到管道并运行测试。
 * 如果配置了 PagerDuty 工具集成，那么 PagerDuty 集成会配置为向 Slack 中所配置的通道发送通知。这些通知会在发生问题时予以指示。
 * 如果配置了 Slack 工具集成，那么 Slack 集成会配置为向 Slack 中所配置的通道发送通知。这些通知会指示部署进度；例如，`已与项目 XYZ 连接`、`管道已配置`和`“构建”阶段已启动`。
 * 如果配置了 GitHub 工具集成，那么会将样本 GitHub 存储库克隆到 GitHub 帐户中。


###通过应用程序创建工具链
{: #creating_a_toolchain_from_an_app}

可以通过应用程序来创建工具链。工具链可以支持持续开发、部署、监视等操作，并且与应用程序相关联。每个应用程序可以与一个工具链相关联。将更改推送到工具链的 GitHub 存储库时，管道会自动构建和部署应用程序。  

1. 如果是第一次创建工具链，请确保组织中已启用工具链：
   1. 打开 DevOps 仪表板，然后单击**工具链**选项卡。
   2. 如果显示了**启用工具链**按钮，请单击此按钮，并按照提示创建工具链。
   3. 如果未显示**启用工具链**按钮，说明工具链已经启用。请转至步骤 2。
1. 在应用程序“概述”页面的“持续交付”磁贴上，单击**添加工具链**。或者，在 {{site.data.keyword.Bluemix_notm}}“典型经验”中，单击应用程序“概述”页面右上角的**添加工具链**。应用程序将配置为通过新的 GitHub 存储库进行持续交付，该存储库使用应用程序入门模板代码进行填充。
1. 在“工具链创建”页面上，查看要创建的工具链的图。此图显示了每个工具集成在工具链中的生命周期阶段。
1. 查看工具链设置的缺省信息。工具链的名称在 {{site.data.keyword.Bluemix_notm}} 中对其进行标识。如果已经具有该名称的工具链，或者如果要使用其他名称，请更改工具链的名称。
1. 在“可配置集成”部分中，选择要为工具链配置的每个工具集成。某些工具集成无需任何配置。有关配置工具集成的信息，请参阅[配置工具集成](../toolchains/toolchains_integrations.html){: new_window}。
1. 单击**创建**。有多个步骤会自动运行来设置工具链：

 * 这将创建工具链。
 * 如果配置了 Delivery Pipeline 工具集成，那么会触发管道。
 * 如果配置了 Sauce Labs 工具集成，那么 Sauce Labs 集成会配置为将作业添加到管道并运行测试。
 * 如果配置了 PagerDuty 工具集成，那么 PagerDuty 集成会配置为向 Slack 中所配置的通道发送通知。这些通知会在发生问题时予以指示。
 * 如果配置了 Slack 工具集成，那么 Slack 集成会配置为向 Slack 中所配置的通道发送通知。这些通知会指示部署进度；例如，`已与项目 XYZ 连接`、`管道已配置`和`“构建”阶段已启动`。
 * 如果配置了 GitHub 工具集成，那么会将样本 GitHub 存储库克隆到 GitHub 帐户中。


##工具链入门：Dedicated
{: #getting_started_dedicated}

每个工具链都与一个特定组织相关联，属于该组织的任何用户都可以访问其关联工具链。创建工具链之前，请单击菜单栏中的 **{{site.data.keyword.avatar}}** 图标 ![Avatar 图标](../icons/i-avatar-icon.svg) 以打开“帐户和支持”窗口小部件，并查看在其中工作的组织。如果该组织不是您要在其中创建工具链的组织，请切换到所需组织。

###通过模板创建工具链   
{: #creating_a_toolchain_from_a_template_dedicated}

可以将模板用作工具链创建的起点，以包含一组特定的工具集成。

1. 如果是第一次创建工具链，请确保组织中已启用工具链：
   1. 打开 DevOps 仪表板，然后单击**工具链**选项卡。
   2. 如果显示了**启用工具链**按钮，请单击此按钮，并按照提示创建工具链。
   3. 如果未显示**启用工具链**按钮，说明工具链已经启用。请转至步骤 2。
1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”的 **DEVOPS** 选项卡上，单击“添加”按钮 (+) 来创建工具链。
1. 单击工具链模板。例如，要创建简单工具链来部署新的 Cloud Foundry 应用程序，请单击**简单 Cloud Foundry 工具链**。 
1. 在“工具链创建”页面上，查看要创建的工具链的图。此图显示了每个工具集成在工具链中的生命周期阶段。下图是示例。创建工具链时，此图会显示属于工具链的每个工具集成。
![Dedicated 工具链图](images/toolchain_dedicated_diagram.png)

1. 查看工具链设置的缺省信息。工具链的名称在 {{site.data.keyword.Bluemix_notm}} 中对其进行标识。如果已经具有该名称的工具链，或者如果要使用其他名称，请更改工具链的名称。  
1. 在“可配置集成”部分中，选择要为工具链配置的每个工具集成。某些工具集成无需任何配置。有关配置工具集成的信息，请参阅[配置工具集成](../toolchains/toolchains_integrations.html){: new_window}。
1. 单击**创建**。有多个步骤会自动运行来设置工具链：

 * 这将创建工具链。
 * 如果配置了 Delivery Pipeline 工具集成，那么会触发管道。
 * 如果配置了 GitHub Enterprise 工具集成，那么会将样本 GitHub Enterprise 存储库克隆到 GitHub Enterprise 帐户中。


###通过应用程序创建工具链
{: #creating_a_toolchain_from_an_app_dedicated}

可以通过应用程序来创建工具链。工具链可以支持持续开发、部署、监视等操作，并且与应用程序相关联。每个应用程序可以与一个工具链相关联。将更改推送到工具链的 GitHub Enterprise 存储库时，管道会自动构建和部署应用程序。  

1. 如果是第一次创建工具链，请确保组织中已启用工具链：
   1. 打开 DevOps 仪表板，然后单击**工具链**选项卡。
   2. 如果显示了**启用工具链**按钮，请单击此按钮，并按照提示创建工具链。
   3. 如果未显示**启用工具链**按钮，说明工具链已经启用。请转至步骤 2。
1. 单击应用程序的“概述”页面右上角的**添加工具链**。应用程序将配置为通过新的 GitHub Enterprise 存储库进行持续交付，该存储库使用应用程序入门模板代码进行填充。
1. 在“工具链创建”页面上，查看要创建的工具链的图。此图显示了每个工具集成在工具链中的生命周期阶段。
1. 查看工具链设置的缺省信息。工具链的名称在 {{site.data.keyword.Bluemix_notm}} 中对其进行标识。如果已经具有该名称的工具链，或者如果要使用其他名称，请更改工具链的名称。
1. 在“可配置集成”部分中，选择要为工具链配置的每个工具集成。某些工具集成无需任何配置。有关配置工具集成的信息，请参阅[配置工具集成](../toolchains/toolchains_integrations.html){: new_window}。
1. 单击**创建**。有多个步骤会自动运行来设置工具链：

 * 这将创建工具链。
 * 如果配置了 Delivery Pipeline 工具集成，那么会触发管道。
 * 如果配置了 GitHub Enterprise 工具集成，那么会将样本 GitHub Enterprise 存储库克隆到 GitHub Enterprise 帐户中。


##查看工具链
{: #viewing_a_toolchain}

配置工具链及其工具集成后，可以在“工具集成”页面上查看工具链的可视表示。

* 如果使用的是 {{site.data.keyword.Bluemix_notm}} Public，请在 DevOps 仪表板的**工具链**选项卡上，单击工具链来打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**。然后，单击**工具集成**。 
   
* 如果使用的是 {{site.data.keyword.Bluemix_notm}} Dedicated，请在“仪表板”的 **DEVOPS** 选项卡上，单击工具链来打开其“工具集成”页面。或者，单击应用程序的“概述”页面右上角的**查看工具链**。

* 要访问位于工具链中的工具集成，请单击该工具的磁贴。 
 
 **提示**：如果有多个 GitHub 或 GitHub Enterprise 存储库，那么可能对于同一工具集成具有多个磁贴，因为每个存储库都会用其自己的磁贴来表示。


 <!-- The toolchain in the following image is an example. When you create your own toolchain, the visual representation of the toolchain shows the tool integrations that you configure.
![Sample toolchain](images/toolchain.png) -->


# 相关链接
{: #rellinks}

## 教程和样本
{: #samples}

* [Create an application with three microservices](https://www.ibm.com/devops/method/tutorials/tutorial_microservices_part1){:new_window}
* [Create a toolchain from a template on {{site.data.keyword.Bluemix_notm}} Dedicated (Experimental)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Create a toolchain from an app on {{site.data.keyword.Bluemix_notm}} Dedicated (Experimental)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## 相关链接
{: #general}

* [Microservices toolchain (Experimental)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple toolchain (Experimental)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method](https://www.ibm.com/devops/method){:new_window}
