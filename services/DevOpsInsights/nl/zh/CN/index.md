---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.DRA_short}} 入门（试验性）
{: #gettingstarted}

使用 {{site.data.keyword.DRA_full}} 识别构建和部署的风险。
{:shortdesc}

{{site.data.keyword.DRA_short}} 聚集和分析单元测试、功能测试和代码覆盖工具的结果，以确定在部署过程中，您的代码是否满足指定检测点的预定义策略。如果您的代码不满足或超出策略，那么会暂停部署以防止发布有风险的更改。您可以使用 {{site.data.keyword.DRA_short}} 作为持续交付环境的安全网、作为随时间实现和提高质量标准的方法，以及作为帮助您了解项目运行状况的数据可视化工具。

{{site.data.keyword.DRA_short}} 是试验性产品，按原样提供仅用于开发和试验。要使用 {{site.data.keyword.DRA_short}}，请将其添加到使用 {{site.data.keyword.deliverypipeline}} 的任何工具链中。

{: #catalog}
要访问 {{site.data.keyword.DRA_short}} UI，请从现有工具链完成以下步骤：

1. 单击**添加工具**按钮。

2. 单击 **{{site.data.keyword.DRA_short}}**
。

3. 单击**创建集成**。

4. 单击 **{{site.data.keyword.DRA_short}}** 磁贴。

5. 完成其余任务的设置：

	1. [配置 {{site.data.keyword.deliverypipeline}} 集成](./pipeline_integration.html)。
	2. 运行管道并[复查 {{site.data.keyword.deliverypipeline}} 仪表板](./pipeline_decision_reports.html)。
	3. 为要管理的 {{site.data.keyword.DRA_short}} [定义策略](./create_criteria.html)。
	4. 再次运行管道以验证项目通过策略。


# 相关链接
{: #rellinks}

## 教程和样本
{: #samples}

* [使用 Analytics 建议成功部署的可能性](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){:new_window}

## 相关链接
{: #general}

* [工具链入门](https://new-console.ng.bluemix.net/docs/toolchains/toolchains_overview.html){:new_window}
* [Delivery Pipeline 入门](https://new-console.ng.bluemix.net/docs/services/DeliveryPipeline/index.html){:new_window}
* [IBM Bluemix 价格表](https://new-console.ng.bluemix.net/pricing/){:new_window}
* [IBMBluemix 先决条件](https://developer.ibm.com/bluemix/support/?cm_mc_uid=96503159749414585876298&cm_mc_sid_50200000=1462802909#prereqs){:new_window}
