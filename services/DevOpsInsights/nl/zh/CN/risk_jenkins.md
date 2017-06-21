---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 与自由格式的 Jenkins 项目集成

将 {{site.data.keyword.DRA_full}} 添加到开放工具链并定义其监视的策略之后，可以将其与自由格式的 Jenkins 项目相集成。
自由格式的 Jenkins 项目可在 Jenkins Web 界面中进行配置和管理。 

IBM Cloud DevOps for Jenkins 插件可将 Jenkins 项目与工具链相集成。*工具链*是一组工具集成，用于支持开发、部署和操作任务。工具链的整体能力大于其各个单独工具集成的总和。开放工具链是 {{site.data.keyword.contdelivery_full}} 服务的组成部分。要了解有关 {{site.data.keyword.contdelivery_short}} 服务的更多信息，请参阅[其服务文档](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html)。

安装 IBM Cloud DevOps 插件后，可以将测试结果发布到 {{site.data.keyword.DRA_short}}，添加自动质量检测点以及跟踪部署风险。您还可以将作业通知发送给工具链中的其他工具，例如 Slack 和 PagerDuty。为了帮助您跟踪部署，工具链可以将部署消息添加到 Git 落实及其相关的 Git 或 JIRA 问题。此外，还可以在工具链的“连接”页面上查看部署。 

该插件提供了构建后操作和 CLI 以支持集成。{{site.data.keyword.DRA_short}} 聚集和分析单元测试、功能测试、代码覆盖工具、静态安全代码扫描和动态安全代码扫描的结果，以确定您的代码是否符合部署过程中检测点处的预定义策略。如果您的代码不满足或超出策略，那么会暂停部署以防止发布有风险的更改。您可以使用 {{site.data.keyword.DRA_short}} 作为持续交付环境的安全网、作为随时间实现和提高质量标准的方法，以及作为帮助您了解项目运行状况的数据可视化工具。

## 先决条件
{: #jenkins_prerequisites}

您必须有权访问正在运行 Jenkins 项目的服务器。

## 创建工具链
{: #jenkins_create}

必须创建工具链后，才能将 {{site.data.keyword.DRA_short}} 与 Jenkins 项目相集成。 

1. 要创建工具链，请转至[创建工具链页面](https://console.ng.bluemix.net/devops/create)并按照该页面上的指示信息进行操作。 

2. 创建工具链后，向其添加 {{site.data.keyword.DRA_short}}。有关指示信息，请参阅 [{{site.data.keyword.DRA_short}} 文档](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html)。 

## 安装插件
{: #jenkins_install}

首先，在 Jenkins 服务器上安装插件。打开服务器界面，然后：

1. 单击**管理 Jenkins**。
2. 单击**管理插件**。 
3. 单击**可用**选项卡。
4. 对 `IBM Cloud DevOps` 进行过滤。 
5. 选择 IBM Cloud DevOps。
6. 单击**立即下载并在重新启动后安装**。 

在服务器重新启动后即可使用该插件。  

## 为 Deployment Risk 仪表板配置 Jenkins 作业
{: #jenkins_configure}

安装插件之后，可以将 {{site.data.keyword.DRA_short}} 集成到 Jenkins 项目中。 

要将 Deployment Risk 的检测点和仪表板用于您的项目，请执行以下步骤。

1. 打开您拥有的任何作业（例如，构建、测试或部署）的配置。

2. 针对相应类型，添加构建后操作：

   * 对于构建作业，使用**将构建信息发布到 IBM Cloud DevOps**。
   
   * 对于测试作业，使用**将测试结果发布到 IBM Cloud DevOps**。
   
   * 对于部署作业，使用**将部署信息发布到 IBM Cloud DevOps**。
   
3. 填写必填字段。
这些字段将根据作业类型而变化。 

   * 从**凭证**列表中，选择您的 {{site.data.keyword.Bluemix_notm}} 标识和密码。如果它们未保存在 Jenkins 中，请单击**添加**按钮以添加并保存这些内容。通过单击**测试连接**，测试与 {{site.data.keyword.Bluemix_notm}} 的连接。
   
   * 在**构建作业名**字段中，指定与 Jenkins 中完全一样的构建作业名。如果构建与测试作业一起执行，请将此字段保留为空。如果构建作业在 Jenkins 外执行，请选中**构建在 Jenkins 外完成**复选框，并指定构建号和构建 URL。
   
   * 对于环境，如果测试正在构建阶段中运行，请仅选择构建环境。如果测试正在部署阶段中运行，请选择部署环境并指定环境名称。支持两个值：`STAGING` 和 `PRODUCTION`。
   
   * 对于**结果文件位置**字段，请指定结果文件的位置。如果测试未生成结果文件，请将此字段保留为空。插件将基于当前测试作业的状态，上传缺省结果文件。

   以下各图显示了示例配置：
   
   ![上传构建信息](images/Upload-Build-Info.png "将构建信息发布到 DRA")
   *发布构建信息*
   
   ![上传测试结果](images/Upload-Test-Result.png "将测试结果发布到 DRA")
   *发布测试结果*
   
   ![上传部署信息](images/Upload-Deployment-Info.png "将部署信息发布到 DRA")
   *发布部署信息*

4. 如果要使用 {{site.data.keyword.DRA_short}} 策略检测点来控制下游部署作业，请添加构建后操作 **IBM Cloud DevOps 检测点**。选择策略，并指定测试结果的作用域。要允许策略检测点阻止下游部署，请选中**基于策略规则阻止构建**复选框。下图显示了示例配置：

    ![DevOps Insights 检测点](images/DRA-Gate.png "DevOps Insights 检测点")

5. 运行 Jenkins 构建作业。

6. 通过转至 [IBM Bluemix DevOps](https://console.ng.bluemix.net/devops)，选择您的工具链并单击 **DevOps Insights** 来查看 Deployment Risk 仪表板。

Deployment Risk 仪表板依赖于编译打包部署作业后存在检测点。如果要使用该仪表板，请确保您在部署到编译打包环境后，但在部署到生产环境之前拥有检测点。
    
## 配置通知
{: #jenkins_notifications}

可以通过遵循 [Bluemix 文档](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins)中的指示信息来配置用于向 Slack 或 PagerDuty 之类的工具发送通知的 Jenkins 作业。
