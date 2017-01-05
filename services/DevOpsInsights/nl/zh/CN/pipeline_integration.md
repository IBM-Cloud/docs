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

# 集成 {{site.data.keyword.DRA_short}} 与 {{site.data.keyword.deliverypipeline}}
{: #toolchain_configure_pipeline}

在您将 {{site.data.keyword.DRA_full}} 添加到工具链并定义其监视的策略之后，您必须将 {{site.data.keyword.DRA_short}} 与管道相集成。
{:shortdesc}

<!--##Configuring the {{site.data.keyword.deliverypipeline}}

{: #toolchain_integration}
To use {{site.data.keyword.DRA_short}}, add it to any toolchain that uses the {{site.data.keyword.deliverypipeline}}.

1. In {{site.data.keyword.Bluemix_notm}}, on the **Toolchains** tab, open a toolchain.

2. On the toolchain's Overview page, click the add (+) button.

3. In the Tool Integrations section, select **{{site.data.keyword.DRA_short}}**.

4. Click **Create Integration**.

5. In your toolchain, click the {{site.data.keyword.deliverypipeline}} tile. You can configure {{site.data.keyword.DRA_short}} in any number of pipelines.-->

## 为 {{site.data.keyword.DRA_short}} 准备管道阶段
{: #toolchain_pipeline_props}

您必须在包含构建或部署作业的每个管道阶段中，创建几个环境属性：

1. 单击**阶段配置**，然后单击**配置阶段**。

2. 单击**环境属性**。

3. 添加以下三个文本属性，然后保存阶段的更改：

<table><thead>
<tr>
<th>环境属性</th>
<th>描述</th>
</tr>
</thead><tbody>
<tr>
<td><code>LOGICAL_APP_NAME</code></td>
<td>{{site.data.keyword.DRA_short}} 仪表板上显示的应用程序名称。</td>
</tr>
<tr>
<td><code>LOGICAL_ENV_NAME</code></td>
<td>应用程序运行所在的环境名称。此属性用于对 {{site.data.keyword.DRA_short}} 仪表板中的应用程序进行分类。</td>
</tr>
<tr>
<td><code>BUILD_PREFIX</code></td>
<td>在 {{site.data.keyword.DRA_short}} 仪表板上显示的添加到构建的前缀。</td>
</tr>
</tbody></table>


## 更新 {{site.data.keyword.DRA_short}} 的测试作业
{: #toolchain_pipeline_upload}

要开始使用，请从测试作业检索设置信息。

1. 在包含测试作业的阶段上，单击**阶段配置**图标 ![管道阶段配置图标](images/pipeline-stage-configuration-icon.png)。单击**配置阶段**。
2. 创建作业。对于作业类型，选择**测试**。
3. 选择使用“简单”测试器类型的测试作业，并将**测试命令**和**工作目录**字段中的信息复制到编辑器。您在以后会需要该信息。
4. 从相同的“简单”测试作业中，通过选择**高级测试器**，更改测试器类型。
5. 在**测试命令**字段中，粘贴从“简单”测试作业的**测试命令**字段中复制的命令。
6. 在**工作目录**字段中，粘贴从“简单”测试作业的**工作目录**字段中复制的路径。
7. 完成其余字段，以上传特定测试类型的测试结果。如果您想要在同一作业中，针对第二个测试类型上传结果，还请填写前缀为*其他*的字段。

 * 度量的类型
 * 格式
 * 结果文件位置
8. 单击**保存**以返回管道。

**度量的类型**和**结果文件位置**字段的值必须匹配正确的格式：

<table><thead>
<tr>
<th>度量的类型</th>
<th>支持的格式</th>
</tr>
</thead><tbody>
<tr>
<td>功能验证测试</td>
<td>Mocha、JUnit</td>
</tr>
<tr>
<td>单元测试</td>
<td>Mocha、JUnit、Karma/Mocha</td>
</tr>
<tr>
<td>代码覆盖</td>
<td>Istanbul、Blanket.js</td>
</tr>
</tbody></table>

*图 1* 显示的测试作业配置为运行单元测试、以 Mocha 格式上传结果，以及以 Istanbul 格式上传代码覆盖结果。

![Deployment Risk Analytics 上传作业](images/DRA_upload_job.png)
*图 1. 上传结果到 DevOps Analytics*

## 在管道中定义 {{site.data.keyword.DRA_short}} 检测点
{: #toolchain_pipeline_gates}

{{site.data.keyword.DRA_short}} 检测点用于检查测试结果是否符合所定义的策略。如果不符合策略，那么 {{site.data.keyword.DRA_short}} 检测点将失败。通常，检测点放置在管道每个阶段的结束位置。此位置非常适合根据策略检查构建的质量，以确保构建能够安全地从一个环境升级到另一个环境。但是，您可以将检测点放置在管道中您要检查特定条件的任何位置。

1. 在阶段上，单击**阶段配置**图标 ![管道阶段配置图标](images/pipeline-stage-configuration-icon.png)，并单击**配置阶段**。
2. 单击**添加作业**。对于作业类型，选择**测试**。
3. 输入新作业的名称，如 *Gate (Unit Test)*。
4. 对于测试器类型，选择 **{{site.data.keyword.DRA_short}} 检测点**。
5. 指定环境名称。确保此值匹配[环境属性](#toolchain_pipeline_props)中所定义的内容。
6. 定义要在此检测点检查的策略名称。

 此名称必须与所定义的其中一个策略名称完全匹配。在与工具链相同的 {{site.data.keyword.Bluemix_notm}} 组织中，您仅可以指定一个所定义的策略。

7. 可选：要使检测点在建议方式下发挥作用，请清除**此作业失败时停止运行此阶段**复选框。在建议方式下，{{site.data.keyword.DRA_short}} 会在该检测点完成相同的策略分析并生成报告，但是如果发生失败，却不会停止管道。
8. 单击**保存**以返回管道。
9. 重复以上步骤，为所有 {{site.data.keyword.DRA_short}} 策略设置检测点。

![Deployment Risk Analytics Mocha 作业](images/DRA_gate_job.png)
*图 2. DevOps Analytics 检测点*

配置管道之后，开始使用 {{site.data.keyword.DRA_short}}。有关指示信息，请参阅[运行 Delivery Pipeline](./pipeline_decision_reports.html#toolchain_reports)。
