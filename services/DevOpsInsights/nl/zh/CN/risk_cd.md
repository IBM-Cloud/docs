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

# 与 Continuous Delivery Pipeline 集成

将 {{site.data.keyword.DRA_short}} 添加到工具链并定义其监视的策略之后，请将其与 {{site.data.keyword.deliverypipeline}} 相集成。
有关管道的更多信息，请参阅[正式文档](/docs/services/ContinuousDelivery/pipeline_working.html)。

## 准备管道阶段
{: #integrate_pipeline}

要使 Deployment Risk 能够分析项目，必须在管道中定义编译打包阶段和生产阶段。您可使用文本环境属性来定义阶段，这些属性位于每个阶段的配置菜单 ![“管道阶段配置”图标](images/pipeline-stage-configuration-icon.png) 的**环境属性**下。

1. 在编译打包阶段，将 `LOGICAL_ENV_NAME` 属性设置为 `STAGING`。 

2. 在生产阶段，将 `LOGICAL_ENV_NAME` 属性设置为 `PRODUCTION`。 

您还可以将以下属性添加到用于构建或部署应用程序的阶段：

* `LOGICAL_APP_NAME`，用于定义应用程序在仪表板上的名称。
* `BUILD_PREFIX`，用于定义附加到阶段构建前面的文本。此文本还会在仪表板中显示。 

## 添加测试作业
{: #configure_pipeline_jobs}

您可使用两种测试作业将 {{site.data.keyword.DRA_short}} 集成到管道中：一种是将结果上传到 {{site.data.keyword.DRA_short}} 进行分析的作业，另一种是对该分析执行操作的检测点。 

首先，将“高级测试器”作业添加到管道以运行测试并上传结果。 

**注：**如果要更新测试作业以将结果上传到 {{site.data.keyword.DRA_short}}，请在继续之前，先将其配置保存在方便的位置。然后，打开其作业配置菜单，并跳至第 3 步。 

1. 在要添加用于上传结果的作业的阶段中，单击**阶段配置**图标 ![“管道阶段配置”图标](images/pipeline-stage-configuration-icon.png)。单击**配置阶段**。
2. 创建测试作业，然后输入其名称。 
3. 对于作业类型，选择**高级测试器**。
4. 填写**测试命令**和**工作目录**字段，就像对普通管道测试作业那样。 
5. 填写其余字段，以上传特定测试类型的测试结果。 

 1. 选择与要使用的 {{site.data.keyword.DRA_short}} 策略中所定义类型相匹配的度量类型。
 2. 输入结果文件位置。此位置是工作目录的相对位置。 

6. 如果要在同一作业中上传另一种测试类型的结果，请填写前缀为*其他*的字段。
7. 单击**保存**以返回管道。

**度量的类型**和**结果文件位置**字段的值必须匹配正确的格式：

<table><thead>
<tr>
<th>度量的类型</th>
<th>支持的格式</th>
</tr>
</thead><tbody>
<tr>
<td>功能验证测试</td>
<td>Mocha、xUnit</td>
</tr>
<tr>
<td>单元测试</td>
<td>Mocha、xUnit、Karma/Mocha</td>
</tr>
<tr>
<td>代码覆盖</td>
<td>Istanbul、Blanket.js</td>
</tr>
</tbody></table>

图 1 显示的测试作业配置为运行单元测试、以 Mocha 格式上传结果，以及以 Istanbul 格式上传代码覆盖结果。

![DevOps Insights 上传作业](images/insights_upload_job.png)
*图 1. 将结果上传到 DevOps Insights*

## 定义检测点
{: #configure_pipeline_gates}

{{site.data.keyword.DRA_short}} 检测点用于检查测试结果是否符合所定义的策略。如果不符合策略，那么缺省情况下 {{site.data.keyword.DRA_short}} 检测点将失败。您还可以将检测点配置为以建议角色执行操作，以允许管道在即便发生失败后仍继续运行。

Deployment Risk 仪表板依赖于编译打包部署作业后存在检测点。如果要使用该仪表板，请确保您在部署到编译打包环境后，但在部署到生产环境之前拥有检测点。

通常，检测点在管道中构建升级之前放置。这些位置非常适合根据策略检查构建的质量，以确保构建能够安全地从一个环境升级到另一个环境。但是，您可以将检测点放置在管道中您要检查特定条件的任何位置。在部署到编译打包环境之前放置的检测点仍将强制实施策略，但这些检测点不会在 Deployment Risk 仪表板上显示。

1. 在阶段上，单击**阶段配置**图标 ![管道阶段配置图标](images/pipeline-stage-configuration-icon.png)，并单击**配置阶段**。
2. 单击**添加作业**。对于作业类型，选择**测试**。
3. 对于测试器类型，选择 **{{site.data.keyword.DRA_short}} 检测点**。
4. 指定环境名称。确保此值匹配[环境属性](#toolchain_pipeline_props)中所定义的内容。
5. 输入要在此检测点检查的策略名称。

 此名称必须与所定义的其中一个策略名称完全匹配。在与工具链相同的 {{site.data.keyword.Bluemix_notm}} 组织中，您仅可以指定一个所定义的策略。

6. 可选：要使检测点在建议方式下发挥作用，请清除**此作业失败时停止运行此阶段**复选框。在建议方式下，{{site.data.keyword.DRA_short}} 会在该检测点完成相同的策略分析并生成报告，但是如果发生失败，却不会停止管道。
7. 单击**保存**以返回管道。
8. 重复以上步骤，为所有 {{site.data.keyword.DRA_short}} 策略设置检测点。

![Deployment Risk Mocha 作业](images/insights_gate_job.png)
*图 2. DevOps Insights 检测点*

配置管道之后，开始使用 {{site.data.keyword.DRA_short}}。 
