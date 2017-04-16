---

copyright:
  years: 2016, 2017
lastupdated: "2017-3-3"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# {{site.data.keyword.product-insights_short}} 入门
{: #product-insights}

{{site.data.keyword.product-insights_full}} 连接至内部部署 IBM 软件产品，以构建跨产品清单并洞察产品使用情况度量值。

{:shortdesc}

{{site.data.keyword.product-insights_short}} 服务在 IBM Bluemix 内运行并从已启用的内部部署 IBM 软件产品接收信息。此信息随后会显示在服务实例仪表板中。要使用该服务，您必须具有 Bluemix 帐户并在组织和空间中创建该服务。在该唯一服务的范围或上下文中，可安全地存储并查看已启用的内部部署产品的产品和使用情况信息。 

提示：为简单起见，您一开始就可以使用单个服务实例。

要开始使用 {{site.data.keyword.product-insights_short}}，请完成以下步骤：

1.  在**管理**选项卡中，单击**注册产品**按钮，以查看受支持产品和必要版本级别的列表。系统还提供了每个产品类型的指示信息，以便您可以将内部部署产品实例连接至 {{site.data.keyword.product-insights_short}} 服务。如果必要，请将已启用的内部部署 IBM 软件产品更新到最低必备软件级别。对于需要最低受支持级别的产品，请安装修订包或临时修订，以启用与 {{site.data.keyword.product-insights_short}} 的集成。 
2.  将已启用的内部部署 IBM 软件产品连接至 {{site.data.keyword.product-insights_short}} 服务。在对每个产品进行配置的过程中，您需要服务凭证（即 apikey 和 apihost）。您可以在服务仪表板的**服务凭证**选项卡中找到服务凭证。 
3.  在您启用并连接每个产品实例后，您可能需要针对它们启动或重新启动产品或产品实例，以向 {{site.data.keyword.product-insights_short}} 服务提供产品和使用情况信息。 

如需启用产品、每个产品所需的最低支持级别，以及如何启用每个产品以与 {{site.data.keyword.product-insights_short}} 集成的详细信息，请加入{{site.data.keyword.product-insights_full}}[技术社区](https://developer.ibm.com/product-insights/)。

通过在服务仪表板中选择**管理**，可以查看清单。  

* 在服务仪表板中，已连接的产品的名称会在**产品**窗格中列出。 
* 要显示所有产品实例，请选择**全部查看**。要显示某个产品的产品实例，请从**产品**窗格中选择该产品，该产品的实例即会显示在**实例**窗格中。
* 要显示单个产品实例的详细信息，请从**实例**窗格中选择产品实例。**详细信息**窗格中随后会填充信息。**详细信息**窗格显示产品实例的详细信息，以及已从该实例发送的使用情况信息。
* **使用情况**选项卡以图形形式显示产品使用情况信息。根据产品，您可以指定要查看的信息类型和采样周期。
* **详细信息**选项卡显示产品实例信息，包括产品信息、环境信息和组件信息。
* **顾问程序**选项卡中的**服务**选项卡提供其他服务的详细信息，这些服务可能对当前产品实例方面有所裨益。在**更新**选项卡中，它提供产品实例版本级别及其当前状态的相关信息。










