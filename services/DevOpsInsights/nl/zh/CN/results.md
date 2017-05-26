---

copyright:
  years: 2016, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 查看结果

## Deployment Risk 评估

在管道运行后，{{site.data.keyword.DRA_short}} 会开始从管道收集并分析测试结果，以建立基线。它会收集每个后续运行所产生的数据并与之前的结果进行比较。决策检测点使用此数据来确定何时停止部署。 

可以在 Deployment Risk 仪表板中查看部署和检测点评估数据。要打开该仪表板，请打开 {{site.data.keyword.DRA_short}}，然后在侧边菜单中，单击 **Deployment Risk**。

如果使用的是 {{site.data.keyword.contdelivery_short}} Pipeline，那么可以在管道自身中查看各个检测点执行报告。要查看管道中某个检测点的决策报告，请执行以下步骤：

1. 在包含要检查的检测点的阶段上，单击**查看日志和历史记录**。

2. 在包含检测点的作业中，单击检测点的名称。

3. 在日志视图中，找到“`在此处检查 {{site.data.keyword.DRA_short}} 报告`”消息并单击链接以打开报告。

## Developer Insights 和 Team Dynamics 报告

在初始数据挖掘时间段后，可以查看有关团队和代码的仪表板。在服务导航菜单中，单击 **Developer Insights** 或 **Team Dynamics**，然后选择一种数据类别来查看相应信息。
