---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 配置工具集成
{: #integrations}

上次更新时间：2016 年 10 月 18 日
{: .last-updated}

您可以在创建工具链时配置支持开发、部署和操作任务的工具集成，或者您可以添加并配置工具集成，以定制现有工具链。  
{:shortdesc}

**重要信息**：在 {{site.data.keyword.Bluemix_notm}} Public 中，工具链仅在美国南部区域可用。

根据您是在 {{site.data.keyword.Bluemix_notm}} Public 还是 {{site.data.keyword.Bluemix_notm}} Dedicated 中使用工具链，工具链可添加和配置的工具集成有所不同。如果要在 {{site.data.keyword.Bluemix_notm}} Dedicated 上使用工具链，那么哪些工具集成可用将取决于 {{site.data.keyword.jazzhub_title}} 在您的特定环境中如何设置。

*表 1. {{site.data.keyword.Bluemix_notm}} Public 和 Dedicated 中，工具链可使用的工具集成*

|工具集成 |在 {{site.data.keyword.Bluemix_notm}} Public 中可用	|在 {{site.data.keyword.Bluemix_notm}} Dedicated 中可用（具体取决于环境）|
|:----------|:------------------------------|:------------------|
|{{site.data.keyword.deliverypipeline}} 		|是	   	|是  		|
|{{site.data.keyword.DRA_short}} 		|是		|否			|
|Eclipse Orion {{site.data.keyword.webide}}		|是		|是			|
|GitHub		|是		|是		|
|Dedicated GitHub Enterprise			|否		|是		|
|Other Tool			|是		|是		|
|PagerDuty			|是		|是		|
|Sauce Labs		|是		|否		|
|Slack			|是		|是		|

**提示**：如果您想要在 {{site.data.keyword.Bluemix_notm}} Public 中开始使用源代码进行开发，请配置 GitHub 工具集成，然后再配置 {{site.data.keyword.deliverypipeline}}。如果要在 {{site.data.keyword.Bluemix_notm}} Dedicated 上开始使用您的代码进行开发，请先配置 {{site.data.keyword.ghe_short}} 工具集成或 GitHub 工具集成，然后再配置 {{site.data.keyword.deliverypipeline}}。 


## 配置 Delivery Pipeline
{: #deliverypipeline}

{{site.data.keyword.deliverypipeline}} 可通过检索输入和运行作业的阶段序列（如构建、测试和部署），自动持续部署项目。 

配置 {{site.data.keyword.deliverypipeline}} 以自动持续构建、测试和部署应用程序： 

1. 如果您在创建工具链时配置此工具集成，请在“可配置的集成”部分中，单击 **Delivery Pipeline**。根据您所使用的模板，可能会有不同的字段可用。请复查缺省字段值，如果必要，更改那些设置。
1. 如果您在 {{site.data.keyword.Bluemix_notm}} Public 中有工具链，并且要将此工具集成添加到该工具链，请在 DevOps 仪表板的**工具链**页面上单击该工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**。然后，单击**工具集成**。如果您在 {{site.data.keyword.Bluemix_notm}} Dedicated 中使用工具链，请在仪表板的 **DEVOPS** 选项卡上，单击该工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的右上角，单击**查看工具链**。然后，单击**工具集成**。 
1. 单击添加按钮 (+)。
1. 在“工具集成”部分中，单击 **Delivery Pipeline**。
1. 指定新管道的名称。
1. 如果您计划使用管道来部署用户界面，请选择**可查看的应用程序**复选框。管道所创建的所有应用程序都会显示在工具链“工具集成”页面上的**查看应用程序**列表中。
1. 单击**创建集成**，以向工具链添加 {{site.data.keyword.deliverypipeline}}。
1. 单击 {{site.data.keyword.deliverypipeline}} 的磁贴，以查看管道并对其进行配置。要了解配置管道的基础知识，请参阅[构建和部署管道（在新窗口中打开链接）](../services/DeliveryPipeline/build_deploy.html){: new_window}。

  **提示**：如果在向 GitHub 或 {{site.data.keyword.ghe_short}} 存储库推送更改时您想要触发管道，那么您必须先为工具链配置 GitHub 或 {{site.data.keyword.ghe_short}}，然后再为管道定义阶段。管道阶段需要存储库的 Git URL。每一个管道阶段仅可以参考与工具链相关联的其中一个 GitHub 或 {{site.data.keyword.ghe_short}} 存储库。有关配置 GitHub 的指示信息，请参阅 [GitHub](#github) 一节。有关配置 Dedicated GitHub Enterprise 的指示信息，请参阅 [{{site.data.keyword.ghe_long}} 入门（在新窗口中打开链接）](../services/ghededicated/index.html){: new_window}。
  
1. 可选：如果您在 {{site.data.keyword.Bluemix_notm}} Public 中使用工具链，并且想要 Sauce Labs 对您的应用程序运行测试，请配置 {{site.data.keyword.deliverypipeline}} 以添加 Sauce Labs 测试作业。有关配置测试作业的指示信息，请参阅[在管道中配置 Sauce Labs 测试作业](#config_saucelabs)一节。

### 在管道中配置 Sauce Labs 测试作业
{: #config_saucelabs}

在管道中配置 Sauce Labs 测试作业之前，您需要具有构建和部署应用程序阶段的工作管道，且您必须为工具链配置 Sauce Labs。有关配置 Sauce Labs 的指示信息，请参阅 [Sauce Labs](#saucelabs) 一节。

配置 {{site.data.keyword.deliverypipeline}} 以添加 Sauce Labs 测试作业：

1. 如果您没有部署应用程序测试版本的阶段，请创建一个。
1. 在该阶段中，在部署作业之后添加测试作业。通过将这些作业置于相同的阶段中，它们可以访问相同的环境属性集。
![测试作业](images/toolchain_test_job.png) 

1. 配置阶段： 

  a. 在**环境属性**选项卡，创建三个属性：CF_APP_NAME、SAUCE_USERNAME 和 SAUCE_ACCESS_KEY。
  
  b. 输入 Sauce Labs 用户名和访问密钥。这样做可外部化那些值，以便您可以在测试中使用它们。
  
1. 配置部署作业。在**部署脚本**字段中，包括以下命令：`export CF_APP_NAME="$CF_APP"`。该命令会将应用程序名称导出为环境属性。
1. 配置测试作业。以下图像中的值为示例。**服务实例**、**目标**、**组织**和**空间**字段中会填充您使用的 Sauce Labs 用户名、区域、组织和空间。
![配置作业](images/toolchain_configure_job.png)

  a. 对于测试器类型，请选择 **Sauce Labs**。
  
  b. 对于服务实例，请选择您为工具链配置 Sauce Labs 时所使用的 Sauce Labs 用户名。 
  
   **提示**：要查看您为工具链配置 Sauce Labs 时所使用的用户名和访问密钥，请单击**配置**。 
  
  c. 在**测试执行命令**字段中，输入安装测试所需依赖项的命令，然后运行测试。例如，对于 Node.js 应用程序，您可能会输入以下命令：
     ```
npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. 如果您想要在测试作业日志中查看测试报告，请选择**启用测试报告**复选框，然后将“测试结果文件模式”设置为 `test/*.xml`。
  
1. 单击**保存**。无论何时您的管道运行，Sauce Labs 测试都会运行。

要了解更多信息，请参阅 [Delivery Pipeline（在新窗口中打开链接）](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}。


## 添加 {{site.data.keyword.DRA_short}}
{: #dra}

{{site.data.keyword.DRA_full}} 会从单元测试、功能测试和代码覆盖工具收集和分析结果，以确定您的代码是否满足部署过程中指定保护门处的预定义条件。如果您的代码不满足或超出条件，那么会停止部署以防止释放风险。您可以使用 {{site.data.keyword.DRA_short}} 作为持续交付环境的安全网或作为实现和提高质量标准的方法。 

 **注**：此工具集成是预配置的。它不需要任何配置参数，您无法对其重新配置。
 
添加 {{site.data.keyword.DRA_short}}，以在发行部署之前，监视这些部署以识别风险，从而保持并提高 {{site.data.keyword.Bluemix_notm}} 中代码的质量。

1. 如果您有工具链，并且要将此工具集成添加到该工具链，请在 DevOps 仪表板的**工具链**页面上单击该工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**。然后，单击**工具集成**。 
1. 单击添加按钮 (+)。
1. 在“工具集成”部分中，单击 **Deployment Risk Analytics**。 
1. 单击**创建集成**。
1. 单击 {{site.data.keyword.DRA_short}} 的磁贴，然后完成入门步骤：创建条件、将条件连接到管道并运行管道。有关更多信息，请参阅 [{{site.data.keyword.DRA_short}}（在新窗口中打开链接）](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){: new_window}。


## 添加 Eclipse Orion {{site.data.keyword.webide}}
{: #webide}

Eclipse Orion {{site.data.keyword.webide}} 是基于 Web 的集成环境，您可以在其中创建、编辑、运行、调试和完成源代码控制任务。您可以无缝地从编辑移到运行到提交再到部署。 

 **注**：此工具集成是预配置的。它不需要任何配置参数，您无法对其重新配置。
 
要完成源代码控制任务，请添加 Eclipse Orion {{site.data.keyword.webide}} 工具集成：

1. 如果您在 {{site.data.keyword.Bluemix_notm}} Public 中有工具链，并且要将此工具集成添加到该工具链，请在 DevOps 仪表板的**工具链**页面上单击该工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**。然后，单击**工具集成**。如果您在 {{site.data.keyword.Bluemix_notm}} Dedicated 中使用工具链，请在仪表板的 **DEVOPS** 选项卡上，单击该工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的右上角，单击**查看工具链**。然后，单击**工具集成**。
1. 单击添加按钮 (+)。
1. 在“工具集成”部分中，单击 **Eclipse Orion Web IDE**。 
1. 单击**创建集成**。
1. 单击新 Eclipse Orion {{site.data.keyword.webide}} 的磁贴。此时，您的工作空间会预填充 GitHub 或 {{site.data.keyword.ghe_short}} 存储库。与您当前工具链相关联的存储库会突出显示。

要了解更多信息，请参阅[使用 Eclipse Orion {{site.data.keyword.webide}} 编辑代码（在新窗口中打开链接）](../toolchains/web_ide.html){: new_window}。


## 配置 GitHub
{: #github}

GitHub 是 Git 存储库基于 Web 的托管服务。您可以同时具有存储库的本地和远程副本，这使协作变得更加轻松。 

GitHub Issues 是一种跟踪工具，可将您的全部工作和计划保留在一个地方。它与您的开发存储库相集成，以便您可将重点放在重要的任务的上。

配置 GitHub，以在云中管理源代码：

1. 如果您在创建工具链时配置此工具集成，请遵循以下步骤：

 a. 在“可配置的集成”部分中，单击 **GitHub**。如果您要在 {{site.data.keyword.Bluemix_notm}} Public 上创建工具链，但尚未授权 {{site.data.keyword.Bluemix_notm}} 访问 GitHub，请单击**授权**以转至 GitHub Web 站点。如果您没有活动 GitHub 会话，那么系统会提示您登录。单击**授权应用程序**，以允许 {{site.data.keyword.Bluemix_notm}} 访问 GitHub 帐户。如果您具有活动 GitHub 会话但最近未输入过密码，那么系统可能会提示您输入 GitHub 密码以进行确认。
 
 b. 复查 GitHub 存储库的缺省目标存储库位置。那些存储库是从样本存储库克隆而来。如果需要，请更改目标存储库的名称。
![缺省目标存储库位置](images/toolchain_github_config.png)
   
1. 如果您有工具链，并且要将此工具集成添加到该工具链，请在 DevOps 仪表板的**工具链**页面上单击该工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**。然后，单击**工具集成**。 
1. 单击添加按钮 (+)。
1. 在“工具集成”部分中，单击 **GitHub**。
1. 如果您具有 GitHub 存储库且想要使用它，请输入 URL。对于存储库类型，请单击**链接**。
1. 如果您想要使用新的 GitHub 存储库，请输入 GitHub 存储库的名称，输入您要克隆或派生的存储库的 URL，然后选择存储库类型： 

 a. 要创建空的存储库，请单击**新建**。 
 
 b. 要创建 GitHub 存储库的副本，请单击**克隆**。
 
 c. 要派生 GitHub 存储库以便您可以通过拉出请求来促进更改，请单击**派生**。
 
1. 如果您想要使用 GitHub Issues 进行问题跟踪，请选中**启用 GitHub Issues** 复选框。
1. 单击**创建集成**。
1. 单击您要使用的 GitHub 存储库的磁贴。这将打开 GitHub Web 站点，您可在其中查看存储库的内容。
 
  **提示**：您可以在 Eclipse Orion {{site.data.keyword.webide}} 中使用集成的源代码管理工具，以编辑 GitHub 存储库，并从您的工作空间部署应用程序。

1. 如果您已启用 GitHub Issues，请单击 GitHub Issues 的磁贴，以将其打开。

有关更多信息，请参阅 [GitHub（在新窗口中打开链接）](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window}和 [GitHub Issues（在新窗口中打开链接）](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}。


## 配置 Dedicated GitHub Enterprise
{: #configghe}

{{site.data.keyword.ghe_long}} 是 Git 存储库基于 Web 的内部部署托管服务。Dedicated GitHub Enterprise 仅适用于 {{site.data.keyword.Bluemix_notm}} Dedicated 客户。GitHub Issues 是一种跟踪工具，可将您的工作和计划保留在一个地方。它与您的开发存储库相集成，以便您可将重点放在重要的任务的上。有关 Dedicated GitHub Enterprise 和 GitHub Issues 的更多信息，请参阅[使用 Dedicated GitHub Enterprise（在新窗口中打开链接）](../services/ghededicated/index.html){: new_window}和 [GitHub Issues（在新窗口中打开链接）](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}。

您可以将 {{site.data.keyword.ghe_short}} 配置为工具链中的工具集成，以便您可以管理公司 [{{site.data.keyword.Bluemix_notm}} Dedicated（在新窗口中打开链接）](../dedicated/index.html#dedicated){: new_window}实例中的源代码。

1. 如果您在创建工具链时配置此工具集成，请遵循以下步骤：

 a. 首次登录到 Dedicated GitHub Enterprise 之前，请要求公司的区域管理员使用 LDAP，在公司的用户注册表中，将您的用户标识添加到 {{site.data.keyword.Bluemix_notm}} Dedicated 实例。有关设置 {{site.data.keyword.ghe_short}} 帐户的信息，请参阅[使用 Dedicated GitHub Enterprise（在新窗口中打开链接）](../services/ghededicated/index.html){: new_window}。
 
 b. 在“可配置的集成”部分中，单击 **{{site.data.keyword.ghe_short}}**。    
 
 c. 复查新 {{site.data.keyword.ghe_short}} 存储库的缺省名称。如果需要，请更改新存储库的名称。下图显示了从样本存储库克隆的存储库示例。您可以使用现有存储库或新存储库。要使用新存储库，您可以创建空的存储库、克隆存储库或派生存储库。![缺省存储库位置](images/toolchain_ghe_config.png)
   
1. 如果您在 {{site.data.keyword.Bluemix_notm}} Public 中有工具链，并且要将此工具集成添加到该工具链，请在 DevOps 仪表板的**工具链**页面上单击该工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**。然后，单击**工具集成**。如果您在 {{site.data.keyword.Bluemix_notm}} Dedicated 中使用工具链，请在仪表板的 **DEVOPS** 选项卡上，单击该工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的右上角，单击**查看工具链**。然后，单击**工具集成**。
1. 单击添加按钮 (+)。
1. 在“工具集成”部分中，单击 **{{site.data.keyword.ghe_short}}**。
1. 如果您具有 {{site.data.keyword.ghe_short}} 存储库且想要使用，请输入该存储库的 URL。对于存储库类型，请单击**现有**。
1. 如果您想要使用新的 {{site.data.keyword.ghe_short}} 存储库，请输入存储库的名称，输入您要克隆或派生的存储库的 URL，然后选择存储库类型： 

 a. 要创建空的存储库，请单击**新建**。 
 
 b. 要创建存储库的副本，请单击**克隆**。
 
 c. 要派生存储库以便您可以通过拉出请求来促进更改，请单击**派生**。
 
1. 要使用 GitHub Issues 进行问题跟踪，请选中**启用 GitHub Issues** 复选框。
1. 单击**创建集成**。
1. 单击您要使用的 {{site.data.keyword.ghe_short}} 存储库的磁贴。这将打开您公司的 [{{site.data.keyword.Bluemix_notm}} Dedicated（在新窗口中打开链接）](../dedicated/index.html#dedicated){: new_window}实例，可在其中查看存储库的内容。
 
  **提示**：您可以在 Eclipse Orion {{site.data.keyword.webide}} 中使用集成的源代码管理工具，以编辑 {{site.data.keyword.ghe_short}} 存储库，并从您的工作空间部署应用程序。

1. 如果您已启用 GitHub Issues，请单击 GitHub Issues 的磁贴。

<!-- 8/23/2016: The GHE Dedicated content has been moved to docs-staging/services/ghededicated/index.md -->

## 配置定制工具 (Other Tool)
{: #othertool}

如果您的团队使用工具链集成列表中不包含的工具，那么您可以集成定制工具。 

配置定制工具，以便与工具链中的其他工具一起使用，并且可供您的团队使用：
1. 如果要在创建工具链时配置此工具集成，请在“可配置的集成”部分中，单击 **Other Tool**。

1. 如果您有工具链，并且要将此工具集成添加到该工具链，请在 DevOps 仪表板的**工具链**页面上单击该工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**。然后，单击**工具集成**。
1. 单击添加按钮 (+)。
1. 在“工具集成”部分中，单击 **Other Tool**。
1. 输入工具名称。
1. 选择与该工具关联最紧密的生命周期阶段。选择哪个生命周期阶段将决定在“工具链集成”页面中，您的工具列在哪个类别之下。
1. 添加图标 URL。该图标将显示在工具集成卡上。
1. 添加文档 URL。
1. 指定工具实例名称。例如：我的团队工具。
1. 添加工具实例 URL。单击工具集成卡可转至您为该工具实例所列出的 URL。
1. 添加工具的描述。
1. （高级）根据需要添加其他属性。例如，列出您的工具与工具链中其他工具集成所需的任何信息或属性。  
1. 单击**创建集成**。

## 配置 PagerDuty
{: #pagerduty}

PagerDuty 可将多个监视系统的数据集成到单一视图。发生问题时，PagerDuty 可确保及时通知当时最有能力修正该问题的团队成员。如果该团队成员未响应该问题，可以配置呈报，以将该问题传递给第二顺位的工程师或运作管理员。

配置 PagerDuty，以在发生管道阶段失败时发送通知，以便您可以更快速地修正问题，并缩短停机时间：

1. 如果您在创建工具链时配置此工具集成，请在“可配置的集成”部分中，单击 **PagerDuty**。
1. 如果您有工具链，并且要将此工具集成添加到该工具链，请在 DevOps 仪表板的**工具链**页面上单击该工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**。然后，单击**工具集成**。 
1. 单击添加按钮 (+)。
1. 在“工具集成”部分中，单击 **PagerDuty**
1. 输入与 PagerDuty 帐户相关联的 PagerDuty 站点名称。如果您没有 PagerDuty 帐户，请[注册帐户（在新窗口中打开链接）](https://signup.pagerduty.com/accounts/new){: new_window}。
1. 输入 PagerDuty 帐户的 API 访问密钥。有关查找密钥的指示信息，请参阅 [API 认证（在新窗口中打开链接）](https://signup.pagerduty.com/accounts/new){: new_window}。
1. 输入 PagerDuty 服务的名称。
1. 输入主要 PagerDuty 联系人的电子邮件地址。
1. 输入主要 PagerDuty 联系人的电话号码。
1. 单击**创建集成**。
1. 单击 PagerDuty 的磁贴，以转至 pagerduty.com。您可以查看与您在为工具链配置此工具集成时所指定的 PagerDuty 服务相关联的事件。 

要了解更多信息，请参阅 [PagerDuty（在新窗口中打开链接）](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}。


## 配置 Sauce Labs
{: #saucelabs}

Sauce Labs 运行功能单元测试。当 Sauce Labs 测试套件配置为 {{site.data.keyword.deliverypipeline}} 中的测试作业时，测试套件可以作为您持续交付过程的一部分，根据您的 Web 或移动应用程序，运行测试。这些测试可以为您的项目提供有价值的流程控制，充当防止部署错误代码的保护门。

配置 Sauce Labs，以在多个操作系统和浏览器上运行自动功能测试，以便您可以模拟用户可能使用 Web 站点或应用程序的方式。

1. 如果您在创建工具链时配置此工具集成，请在“可配置的集成”部分中，单击 **Sauce Labs**。
1. 如果您有工具链，并且要将此工具集成添加到该工具链，请在 DevOps 仪表板的**工具链**页面上单击该工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**。然后，单击**工具集成**。 
1. 单击添加按钮 (+)。
1. 在“工具集成”部分中，单击 **Sauce Labs**。
1. 输入与 Sauce Labs 帐户相关联的用户名。您可以[在 Sauce Labs 帐户页面顶部的欢迎消息中查找用户名（在新窗口中打开链接）](https://saucelabs.com/account){: new_window}。
1. 输入 Sauce Labs 帐户的访问密钥。您可以[在 Sauce Labs 帐户页面中查找密钥（在新窗口中打开链接）](https://saucelabs.com/account){: new_window}。
1. 单击**创建集成**。
1. 单击 Sauce Labs 的磁贴，以转至 saucelabs.com 并查看工具链的测试活动。

 **提示**：如果您将 Sauce Labs 测试作业添加到 {{site.data.keyword.deliverypipeline}}，那么您可以选择服务实例。

要了解更多信息，请参阅 [Sauce Labs（在新窗口中打开链接）](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}。


## 配置 Slack
{: #slack}

**重要信息**：团队中的每一个人都可以看到发布到公共 Slack 通道的通知。记住您要对发布的内容负责。

Slack 是基于云的实时消息传递和通知系统。Slack 提供持久交谈，可替代电子邮件用于团队协作，其互动性更高。您可以通过专用通道或与您工作直接相关的一组通道，与团队进行通信。您还可以通过通道或直接消息，在两人或多人之间共享文件和图像。直接消息和通道的通信会保留，以便您可以对它们进行搜索。 

配置 Slack，以从工具集成接收有关工具链的通知，如测试和部署活动：

1. 如果您在创建工具链时配置此工具集成，请在“可配置的集成”部分中，单击 **Slack**。
1. 如果您有工具链，并且要将此工具集成添加到该工具链，请在 DevOps 仪表板的**工具链**页面上单击该工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**。然后，单击**工具集成**。
1. 单击添加按钮 (+)。
1. 在“工具集成”部分中，单击 **Slack**。
1. 输入 Slack 帐户的 API 认证令牌。您必须使用生成的完全访问令牌，向 Slack 进行认证。有关查找令牌的指示信息，请参阅 [Slack 认证（在新窗口中打开链接）](https://api.slack.com/web#authentication){: new_window}。
1. 输入您想要发送通知的目标 Slack 通道的名称。如果指定的通道不存在，那么会创建该通道。如果通道已归档，那么会重新激活该通道。
1. 单击**创建集成**。
1. 单击 Slack 的磁贴。您可以在已配置的 Slack 通道中查看工具链的所有活动。

要了解更多信息，请参阅 [Slack（在新窗口中打开链接）](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}。








