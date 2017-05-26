---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 查看仪表板和报告
{: #DRA_toolchain_reports}

{{site.data.keyword.DRA_short}} 为您提供大量有关项目的可操作信息。
{:shortdesc}

## {{site.data.keyword.DRA_short}} 仪表板    
{: #DI_toolchain_dashboards}

{{site.data.keyword.DRA_short}} 跨 Bluemix 组织提供用于显示性能信息的仪表板。要查看这些仪表板，请在打开 {{site.data.keyword.DRA_short}} 后，单击**构建验证**或**部署验证**。

仪表板中会自动填充管道 {{site.data.keyword.DRA_short}} 测试作业的最新信息。单击仪表板中的元素，可查看有关它们的更多信息。

### 构建中的关键性能指标    
{: #DI_key_performance_indicators}

**构建验证**页面包含三个图形，其中包含大量所选开发分支的相关信息：

<table>
<thead>
<tr>
<th>图形</th>
<th>描述</th>
</tr>
</thead>

<tbody>
<tr>
<td>最新构建</td>
<td>与最近构建总数相比较的已完成最近构建数。</td>
</tr>
<tr>
<td>测试</td>
<td>与测试总数相比较的已通过测试数。</td>
</tr>
<tr>
<td>代码覆盖</td>
<td>测试所调用的代码语句和函数的百分比。</td>
</tr>
</tbody></table>

## 查看决策报告    
{: #DI_decision_reports}

在管道运行后，{{site.data.keyword.DRA_short}} 会开始从管道收集并分析测试结果，以建立基线。它会收集每个后续运行所产生的数据并与之前的结果进行比较。决策检测点使用此数据来确定何时停止部署。 

要查看管道中某个检测点的决策报告，请完成以下步骤：

   1. 在包含要检查的检测点的阶段上，单击**查看日志和历史记录**。

   2. 从阶段的作业窗口，单击检测点的名称。

   3. 在日志视图中，找到“在此处检查 {{site.data.keyword.DRA_short}} 报告”消息并单击所提供的链接以打开报告。
