---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 将环境映射到报告
{: #uc_insights_mapping}

在 Delivery Insights 中显示的信息按*逻辑环境*分组，逻辑环境是 IBM UrbanCode Deploy 环境（也称为*物理环境*）的集合。您可以按适合组织需要的任意方式将环境分组成逻辑环境。
{:shortdesc}

## 逻辑环境

Delivery Insights 将 IBM UrbanCode Deploy 环境分组成一个或多个逻辑环境。通过这种方式，可以根据您及您组织的需要，按组收集环境。例如，如果针对多个应用程序有多个生产环境，那么可以将所有这些环境分组到单个逻辑环境中，并将所有这些环境的度量合并到单个生产环境仪表板中。映射通过搜索字符串执行，所以您可以按适合 IBM UrbanCode Deploy 服务器需要的任意方式对环境分组。

## 缺省逻辑环境

缺省情况下，报告使用字符串来包含与 IBM UrbanCode Deploy 环境匹配的逻辑环境。例如，名称中具有“dev”的所有环境都会映射到 DEV 逻辑环境，而名称中具有“prod”的所有环境都会映射到 PROD 逻辑环境。

![缺省逻辑环境](images/uc_insights_mapping.gif)

## 将环境映射到逻辑环境

您可以手动将物理环境映射到逻辑环境，也可以使用模式以动态方式将物理环境与逻辑环境相关联。

要使用模式将物理环境映射到逻辑环境，请执行以下步骤：

1. 在 {{site.data.keyword.DRA_short}} 中，单击 **Delivery Insights > 映射环境**。
1. 单击现有逻辑环境，或单击**添加逻辑环境**。
1. 在逻辑环境的设置中的**模式**下，单击**添加模式**。
1. 指定环境名称的模式。可以使用星号 (*) 作为通配符。例如，模式 `env` 与环境 `env1`、`env2` 和 `env` 相匹配。
1. 验证逻辑环境是否包含需要的环境。

要手动将环境映射到逻辑环境，请单击**手动添加**，然后选择要添加或除去的环境。

![在 DevOps Connect 中设置集成](images/uc_insights_mapping_manually.gif)

现在，您已将环境映射到逻辑环境，因此可以查看按这些逻辑环境聚集的报告信息。
