---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# DevOps Insights 入门 (Beta)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} 将开发者、团队和部署分析应用于您最繁忙的 DevOps 项目。使用 DevOps Insights 可了解团队在多大程度上遵循 DevOps 和开发者实践，也可管理代码库中的风险，以及在 Continuous Delivery 项目中自动强制实施质量标准。
{:shortdesc}

{{site.data.keyword.DRA_short}} 由多组功能构成：

   * Developer Insights 提供了一种探索项目开发成熟度的综合性方法。您可以识别易出错性高的文件，并可获取基于开发者实践的项目合规视图。


   * Team Dynamics 使用社交编码分析来帮助您了解团队的协作程度以及如何改进团队工作。

   * Deployment Risk 就像一张持续交付安全网。它分析单元测试、功能测试、应用程序扫描和代码覆盖工具在部署过程中指定检测点生成的结果，并阻止发布有风险的更改。

   * Delivery Insights 显示部署统计信息、度量以及有关 IBM UrbanCode Deploy 安装的其他信息。例如，可以显示部署持续时间、成功次数和失败次数的图表，所有数据均按以逻辑方式分组的环境排序。请参阅[集成 DevOps Insights 与 IBM UrbanCode Deploy](/docs/services/DevOpsInsights/uc_insights_overview.html)。

{{site.data.keyword.DRA_short}} 是 Bluemix 开放工具链目录中的一个集成。有关工具链的更多信息，请参阅[使用工具链](/docs/services/ContinuousDelivery/toolchains_working.html)。

要使用 {{site.data.keyword.DRA_short}}，必须将其添加到工具链。许多工具链模板已经包含 {{site.data.keyword.DRA_short}}。另外，确保[将 DevOps Insights 作为服务添加到 {{site.data.keyword.Bluemix_notm}} 组织](/docs/services/reqnsi.html)，这样才能在 {{site.data.keyword.Bluemix_notm}}“仪表板”中查看有关 {{site.data.keyword.DRA_short}} 的信息，并访问包含 DevOps Insight 的某些工具链模板。  

## 将 DevOps Insights 添加到工具链
{: #catalog}

{{site.data.keyword.DRA_short}} 是 {{site.data.keyword.contdelivery_short}} 的一部分。通过从工具集成目录中选择 {{site.data.keyword.DRA_short}}，可以将其添加到任何工具链。

{{site.data.keyword.DRA_short}} 也是许多工具链模板的一部分。如果要通过包含 {{site.data.keyword.DRA_short}} 的模板创建工具链，请确保 {{site.data.keyword.DRA_short}} 设置为**高级**。然后，创建工具链，并跳至[使用 Insights](/docs/services/DevOpsInsights/index.html#using)。

要将 {{site.data.keyword.DRA_short}} 添加到工具链，请执行以下操作：

1. 单击**添加工具**。

2. 单击 **{{site.data.keyword.DRA_short}}**。

3. 单击**创建集成**。

现在，{{site.data.keyword.DRA_short}} 在工具链的“概述”页面上可用。此时，将自动扫描存储库和问题跟踪系统，以获取相关数据。 

## 使用 DevOps Insights
{: #using}

如果工具链包含 GitHub、GitLab 或 JIRA，那么在一些初始数据收集和分析后，{{site.data.keyword.DRA_short}} 会自动提供有关您代码库和团队的信息。如果工具链不包含其中任何集成，请添加其中一个集成，然后执行以下步骤：

1. 在工具链的“概述”页面中，单击 **{{site.data.keyword.DRA_short}}**。

2. 单击 **Team Dynamics** 或 **Developer Insights**，然后选择数据类别。 

3. 通过查看该数据类别中的仪表板，探索项目数据。如果要了解有关图或可使用图中信息执行哪些操作的更多信息，请单击**信息**或**指导**。

探索 Team Dynamics 和 Developer Insights 后，请[配置 Deployment Risk](/docs/services/DevOpsInsights/insights_risk.html) 以帮助您强制实施代码质量。Deployment Risk 与 {{site.data.keyword.contdelivery_short}} Pipeline和 Jenkins 兼容。   
