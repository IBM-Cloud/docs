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

# 集成 {{site.data.keyword.DRA_short}} 与 Jenkins
{: #toolchain_configure_jenkins}

在您为要监视的 {{site.data.keyword.DRA_full}} 定义策略之后，下一步是向工具链添加 {{site.data.keyword.DRA_short}}，然后配置持续交付管道。
{:shortdesc}

<!--##Configuring a Jenkins project-->

您可以将 {{site.data.keyword.DRA_short}} 集成到一个 Jenkins 项目中或几个相关 Jenkins 项目中。这允许您设置质量检测点，以及在 {{site.data.keyword.DRA_short}} 仪表板上接收构建质量数据。

## 先决条件    
{: #DI_jenkins_prereqs}

* 您必须具有本地 Jenkins 项目的访问权，或者具有正在运行 Jenkins 项目的服务器的访问权。

## 安装 {{site.data.keyword.DRA_short}} 插件
{: #DI_jenkins_install}

要在 Jenkins 项目中安装 {{site.data.keyword.DRA_short}} 插件，请遵循以下步骤：

  1. 从插件的 GitHub 存储库[下载 IBM DevOps Insight 插件安装文件 (.hpi)](https://github.ibm.com/oneibmcloud/DRA-Jenkins/blob/hpi-release/target/dra.hpi)。
  2. 在您的 Jenkins 安装中，单击**管理 Jenkins**，选择**管理插件**，然后单击**高级**选项卡。
  3. 单击**选择文件**并选择 DevOps Insight 插件安装文件。
  4. 单击**上传**。
  5. 重新启动 Jenkins 并验证已安装插件。

## 集成 {{site.data.keyword.DRA_short}} 与 Jenkins    
{: #DI_jenkins_integrate}

安装插件之后，将 {{site.data.keyword.DRA_short}} 集成到 Jenkins 安装之前，先转至[控制中心](https://control-center.stage1.ng.bluemix.net/)并至少创建一个策略。

对于您已经具有且要在其中使用 {{site.data.keyword.DRA_short}} 的每个作业：

1. 添加类型为**将构建信息发布到 {{site.data.keyword.DRA_short}}**、**将部署信息发布到 {{site.data.keyword.DRA_short}}** 或**将测试结果发布到 {{site.data.keyword.DRA_short}}** 的构建后操作。特定类型应该匹配作业类型（构建、部署或测试）。填写必填字段。

  * 在“凭证”字段中，选择 Bluemix 标识和密码。如果未在 Jenkins 中保存它们，请单击**添加**按钮，以添加并保存它们。
  * 在“构建作业名”字段中，指定与 Jenkins 中完全一样的构建作业名。如果构建与测试作业同时发生，请将此字段保留为空。如果构建作业在 Jenkins 外发生，请选中**构建在 Jenkins 外完成**，并指定构建号和构建 URL。
  * 对于“结果文件位置”字段，请指定结果文件的位置。如果测试未生成结果文件，请将此字段保留为空。插件将基于当前测试作业的状态，上传缺省结果文件。
3. *可选*：如果您想要测试作业中的 DRA 策略检测点控制下游部署作业，可添加类型为 **DevOps Risk Analytics 检测点**的另一个构建后操作，并填写必填字段。如果测试作业不满足关联的策略，那么检测点将防止下游作业运行。
4. 单击**应用**，然后单击**保存**。

您可以单击项目页面上的**立即构建**以运行项目。

构建运行后，转至[控制中心](https://control-center.stage1.ng.bluemix.net/)以在仪表板中检查构建状态。如果已配置策略检测点，那么您还可以在当前构建的“状态”页面上查看 {{site.data.keyword.DRA_short}} 结果。
