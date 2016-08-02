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

*上次更新时间：2016 年 6 月 17 日*
{: .last-updated}

您可以在创建工具链时配置支持开发、部署和操作任务的工具集成，或者您可以添加并配置工具集成，以定制现有工具链。  
{:shortdesc}

**重要信息**：此功能是试验性的。工具链可能不稳定，并且可能会发生变化而与较低版本不兼容。建议不要在生产环境中使用工具链。要使用工具链，您必须进行一次性的[访问请求](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window}。工具链仅在美国南部区域可用。

**提示**：如果您想要开始使用源代码进行开发，请确保您已配置 GitHub 和 GitHub Issues 工具集成，然后再配置 {{site.data.keyword.deliverypipeline}}。

## 配置 Delivery Pipeline
{: #deliverypipeline}

{{site.data.keyword.deliverypipeline}} 可通过检索输入和运行作业的阶段序列（如构建、测试和部署），自动持续部署项目。 

配置 {{site.data.keyword.deliverypipeline}} 以自动持续构建、测试和部署应用程序： 

1. 如果您在创建工具链时配置此工具集成，请在“可配置的集成”部分中，单击 **Delivery Pipeline**。根据您所使用的模板，可能会有不同的字段可用。请复查缺省字段值，如果必要，更改那些设置。
1. 如果您具有工具链，且要将此工具集成添加到该工具链，请在 DevOps 仪表板的**工具链**选项卡上，单击该工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**。然后，单击**工具集成**。 
1. 单击添加按钮 (+)。
1. 在“工具集成”部分中，单击 **Delivery Pipeline**。
1. 指定新管道的名称。
1. 如果您计划使用管道来部署用户界面，请选择**可查看的应用程序**复选框。管道所创建的所有应用程序都会显示在工具链“工具集成”页面上的**查看应用程序**列表中。
1. 单击**创建集成**，以向工具链添加 {{site.data.keyword.deliverypipeline}}。
1. 单击 {{site.data.keyword.deliverypipeline}} 的磁贴，以查看管道并对其进行配置。要了解配置管道的基础知识，请参阅[构建和部署管道](../services/DeliveryPipeline/build_deploy.html){: new_window}。

  **提示**：如果在向 GitHub 存储库推送更改时您想要触发管道，那么您必须先为工具链配置 GitHub，然后再为管道定义阶段。管道阶段需要 GitHub 存储库的 Git URL。每一个管道阶段仅可以参考与工具链相关联的其中一个 GitHub 存储库。有关配置 GitHub 的指示信息，请参阅 [GitHub 和 GitHub Issues](#github) 一节。
  
1. 可选：如果您想要 Sauce Labs 对您的应用程序运行测试，请配置 {{site.data.keyword.deliverypipeline}} 以添加 Sauce Labs 测试作业。有关配置测试作业的指示信息，请参阅[在管道中配置 Sauce Labs 测试作业](#config_saucelabs)一节。

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
  
1. 配置部署作业。在**部署脚本**字段中，包括以下命令：export CF_APP_NAME="$CF_APP"。该命令会将应用程序名称导出为环境属性。
1. 配置测试作业。以下图像中的值为示例。**服务实例**、**目标**、**组织**和**空间**字段中会填充您目前使用的 Sauce Labs 用户名、区域、组织和空间。
![配置作业](images/toolchain_configure_job.png)

  a. 对于测试器类型，请选择 **Sauce Labs**。
  
  b. 对于服务实例，请选择您为工具链配置 Sauce Labs 时所使用的 Sauce Labs 用户名。 
  
   **提示**：要查看您为工具链配置 Sauce Labs 时所使用的用户名和访问密钥，请单击**配置**。 
  
  c. 在**测试执行命令**字段中，输入安装测试所需依赖项的命令，然后运行测试。例如，对于假设的 Node.js 应用程序，您可能会输入：
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. 如果您想要在测试作业日志中查看测试报告，请选择**启用测试报告**复选框，然后将“测试结果文件模式”设置为 `test/*.xml`。
  
1. 单击**保存**。现在，无论何时您的管道运行，Sauce Labs 测试都会运行。

要了解更多信息，请参阅 [Delivery Pipeline](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}。

## 添加 Deployment Risk Analytics
{: #dra}

{{site.data.keyword.DRA_full}} 会从单元测试、功能测试和代码覆盖工具收集和分析结果，以确定您的代码是否满足部署过程中指定保护门处的预定义条件。如果您的代码不满足或超出条件，那么会停止部署以防止释放风险。您可以使用 Deployment Risk Analytics 作为持续交付环境的安全网或作为实现和提高质量标准的方法。 

 **提示**：此工具集成是预配置的。它不需要任何配置参数，您无法对其重新配置。
 
添加 Deployment Risk Analytics，以在发行部署之前，监视这些部署以识别风险，从而保持并提高 Bluemix 中代码的质量：

1. 如果您具有工具链，且要将此工具集成添加到该工具链，请在 DevOps 仪表板的**工具链**选项卡上，单击该工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**。然后，单击**工具集成**。 
1. 单击添加按钮 (+)。
1. 在“工具集成”部分中，单击 **Deployment Risk Analytics**。 
1. 单击**创建集成**。
1. 单击 Deployment Risk Analytics 的磁贴，然后完成入门步骤：创建条件、将条件连接到管道并运行管道。有关更多信息，请参阅 [Deployment Risk Analytics](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){: new_window}。

## 添加 Eclipse Orion {{site.data.keyword.webide}}
{: #webide}

Eclipse Orion {{site.data.keyword.webide}} 是基于 Web 的集成环境，您可以在其中创建、编辑、运行、调试和完成源代码控制任务。您可以无缝地从编辑移到运行到提交再到部署。 

 **提示**：此工具集成是预配置的。它不需要任何配置参数，您无法对其重新配置。
 
添加 Eclipse Orion {{site.data.keyword.webide}} 工具集成，以完成源代码控制任务：

1. 如果您具有工具链，且要将此工具集成添加到该工具链，请在 DevOps 仪表板的**工具链**选项卡上，单击该工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**。然后，单击**工具集成**。 
1. 单击添加按钮 (+)。
1. 在“工具集成”部分中，单击 **Eclipse Orion Web IDE**。 
1. 单击**创建集成**。
1. 单击新 Eclipse Orion Web IDE 的磁贴。此时，您的工作空间会预填充 GitHub 存储库。与您当前工具链相关联的存储库会突出显示。

要了解更多信息，请参阅 [Web IDE](https://www.ibm.com/devops/method/content/code/tool_web_ide/){: new_window}。


## 配置 GitHub 和 GitHub Issues
{: #github}

GitHub 是 Git 存储库基于 Web 的托管服务。您可以同时具有存储库的本地和远程副本，这使协作变得更加轻松。 

GitHub Issues 是一种跟踪工具，可将您的全部工作和计划保留在一个地方。它与您的开发存储库相集成，以便您可将重点放在重要的任务的上。

配置 GitHub 和 GitHub Issues，以在云中管理源代码：

1. 如果您在创建工具链时配置此工具集成，请遵循以下步骤：

 a. 在“可配置的集成”部分中，单击 **GitHub**。如果您未授权 {{site.data.keyword.Bluemix}} 访问 GitHub，请单击**授权**，以转至 GitHub Web 站点。如果您没有活动 GitHub 会话，那么系统会提示您登录。单击**授权应用程序**，以允许 {{site.data.keyword.Bluemix}} 访问 GitHub 帐户。如果您具有活动 GitHub 会话但最近未输入过密码，那么系统可能会提示您输入 GitHub 密码以进行确认。
 
 b. 复查 GitHub 存储库的缺省目标存储库位置。那些存储库是从样本存储库克隆而来。如果需要，请更改目标存储库的名称。
![缺省目标存储库位置](images/toolchain_github_config.png)
   
1. 如果您具有工具链，且要将此工具集成添加到该工具链，请在 DevOps 仪表板的**工具链**选项卡上，单击该工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**。然后，单击**工具集成**。 
1. 单击添加按钮 (+)。
1. 在“工具集成”部分中，单击 **GitHub**。
1. 如果您具有 GitHub 存储库且想要使用它，请输入 URL。对于存储库类型，请单击**链接**。
1. 如果您想要使用新的 GitHub 存储库，请输入 GitHub 存储库的名称，输入您要克隆或派生的存储库的 URL，然后选择存储库类型： 

 a. 要创建空的存储库，请选择**新建**。 
 
 b. 要创建 GitHub 存储库的副本，请选择**克隆**。
 
 c. 要派生 GitHub 存储库以便您可以通过拉出请求来促进更改，请选择**派生**。
 
1. 如果您想要使用 GitHub Issues 进行问题跟踪，请选择**启用 GitHub Issues** 复选框。
1. 单击**创建集成**。
1. 单击您要使用的 GitHub 存储库的磁贴，以转至 github.com 并查看存储库的内容。
 
  **提示**：您可以在 Eclipse Orion Web IDE 中使用集成的源代码管理工具，以编辑 GitHub 存储库，并从您的工作空间部署应用程序。

1. 如果您已启用 GitHub Issues，请单击 GitHub Issues 的磁贴，以转至 GitHub Issues。

要了解更多信息，请参阅 [GitHub](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} 和 [GitHub Issues](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}。    

##使用 Dedicated {{site.data.keyword.ghe_short}}
{: #ghe}

{{site.data.keyword.ghe_long}} 是 IBM Cloud 托管和完全管理的 {{site.data.keyword.ghe_short}} 版本，可用于 Dedicated Bluemix 环境。GitHub 提供开发者喜闻乐见的社交编码经验。[{{site.data.keyword.Bluemix_notm}} Dedicated](../dedicated/index.html#dedicated){: new_window} 在以物理方式隔离的硬件上提供集成到网络的云计算环境。

Dedicated {{site.data.keyword.ghe_short}} 仅适用于 {{site.data.keyword.Bluemix_notm}} Dedicated 客户。

### 设置帐户 

{{site.data.keyword.ghe_short}} 在 {{site.data.keyword.Bluemix_notm}} Dedicated 中随附单点登录。要登录 {{site.data.keyword.ghe_short}}，请将从区域管理员或欢迎使用电子邮件获得的 URL 粘贴到浏览器。URL 将遵循以下模式：`github.your-company-dedicated-name.bluemix.net`。使用 {{site.data.keyword.Bluemix_notm}} Dedicated 用户标识和密码登录，此时将自动创建 {{site.data.keyword.ghe_short}} 帐户。

**注：**如果有消息指出用户标识不存在，请询问区域管理员，以将用户标识添加到 {{site.data.keyword.Bluemix_notm}} Dedicated 用户注册表。如果您是区域管理员，请参阅[管理 {{site.data.keyword.Bluemix_notm}} Dedicated 用户和许可权](https://new-console.stage1.ng.bluemix.net/docs/admin/index.html#oc_useradmin){: new_window}。

在大部分情况下，GitHub 用户名是电子邮件短名称，除非短名称包括 GitHub 不支持的字符，如句点。如果短名称包括 GitHub 不支持的字符，那么这些字符会替换为连字符。     

### 向帐户添加电子邮件地址

您必须向 {{site.data.keyword.ghe_short}} 帐户设置添加电子邮件地址，以接收通知。在添加电子邮件地址之后，您可以利用 {{site.data.keyword.ghe_short}} 的社交编码功能。    
 
要向 Dedicated {{site.data.keyword.ghe_short}} 帐户添加电子邮件地址，请完成以下步骤：    
1. 在任何 GitHub 页面的右上角，单击概要文件图标，然后单击**设置**。    
2. 在侧边栏上，单击**电子邮件**。    
3. 添加电子邮件地址，并单击**添加**。     

{: #ghe_auth}
### 创建个人访问令牌或 SSH 密钥以进行认证

要从本地 Git 存储库执行远程 Git 操作（如`克隆`或`推送`），您必须使用个人访问令牌或 SSH 密钥，以向 {{site.data.keyword.ghe_short}} 进行认证。支持仅使用访问令牌通过 HTTPS 进行认证；您无法使用用户标识和密码，从本地存储库进行克隆或推送。API 请求还需要个人访问令牌。

**注：**要使用个人访问令牌或 SSH 密钥进行认证，您必须在本地设置 Git。有关指示信息，请参阅[设置 Git](https://help.github.com/enterprise/2.6/user/articles/set-up-git/){: new_window}。    

要创建个人访问令牌，请完成以下步骤：    
   1. 在任何 GitHub 页面的右上角，单击概要文件图标，然后单击**设置**。    
   2. 在侧边栏上，单击**个人访问令牌**。   
   3. 单击**生成新令牌**。
   4. 添加令牌描述，然后单击**生成令牌**。
   5. 将令牌复制到安全位置或密码管理应用程序。
**注：**鉴于安全原因，在您离开页面之后，您无法再查看令牌。    

使用个人访问令牌而不是密码，来进行通过 HTTPS 的命令行访问。 


要创建 SSH 密钥，请完成以下步骤：
   1. 打开 Git Bash (Windows) 或新的终端窗口（Linux 和 Mac）。    
   2. 粘贴以下文本，替换您添加到 {{site.data.keyword.ghe_short}} 帐户的电子邮件地址：
   
     ````
     ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
     # 使用所提供的电子邮件作为标签，创建新的 SSH 密钥
     生成公用/专用 RSA 密钥对。
     ````

   3. 当系统提示您指定要保存密钥的文件时，请按 Enter 以接受缺省位置。
   4. 在提示旁，输入安全口令。有关更多信息，请参阅[使用 SSH 密钥口令](https://help.github.com/enterprise/2.6/user/articles/working-with-ssh-key-passphrases/){: new_window}。   

向 SSH 代理程序添加 SSH 密钥：    
   1. 确保已启用 SSH 代理程序。使用 Git Bash，输入以下命令以启用 SSH 代理程序：
      ````
      # 在后台启动 SSH 代理程序
      $ eval "$(ssh-agent -s)"
      Agent pid 59566
      ````    
  
   2. 通过输入以下命令，向 SSH 代理程序添加 SSH 密钥：
      ````
      $ ssh-add ~/.ssh/id_rsa
      ````   
   3. 向 GitHub 帐户添加 SSH 密钥。有关更多信息，请参阅[向 GitHub 帐户添加新 SSH 密钥](https://help.github.com/enterprise/2.6/user/articles/adding-a-new-ssh-key-to-your-github-account/){: new_window}。    
   

### 设置 GitHub 组织、团队和存储库    

设置 GitHub 组织非常有用，这是因为您创建的用户组与众不同，这些用户处理相似的项目或任务。在组织内组织团队具有额外的好处，可控制存储库的访问。有关更多信息，请参阅[组织和团队](https://help.github.com/enterprise/2.6/admin/guides/user-management/organizations-and-teams/){: new_window}。

**注：**GitHub 组织与 Bluemix 组织不同。

通过完成以下任务，来设置团队的项目：

   1. [创建组织](https://help.github.com/enterprise/2.6/user/articles/creating-a-new-organization-account/){: new_window}。
   2. [创建组织的存储库](https://help.github.com/enterprise/2.6/user/articles/create-a-repo/){: new_window}。
   3. [邀请用户加入组织](https://help.github.com/enterprise/2.6/user/articles/inviting-users-to-join-your-organization/){: new_window}。
   4. [仔细在组织中至少选择一个团队成员具有所有者许可权](https://help.github.com/enterprise/2.6/user/articles/changing-a-person-s-role-to-owner/){: new_window}。    
   
  **注：**在您邀请用户加入组织之前，这些用户必须至少登录过一次 {{site.data.keyword.ghe_short}}，否则他们的 {{site.data.keyword.ghe_short}} 帐户无法用于邀请。
   
### 获取支持
要立即获取答案，请提交问题到[堆栈溢出](http://stackoverflow.com/questions/ask?tags=ibm-bluemix_github-enterprise){: new_window}。 

要获取更多支持，请使用以下资源：    
   1. 完成 https://ibm.biz/bluemixsupport 的表单。   
   2. 通过 Client Success Portal，提交新凭单，网址为 https://support.ibmcloud.com/ics/support/mylogin.asp?login=bluemix。    


## 配置 PagerDuty
{: #pagerduty}

PagerDuty 可将多个监视系统的数据集成到单一视图。发生问题时，PagerDuty 可确保及时通知当时最有能力修正该问题的团队成员。如果该团队成员未响应该问题，可以配置呈报，以将该问题传递给第二顺位的工程师或运作管理员。

配置 PagerDuty，以在发生管道阶段失败时发送通知，以便您可以更快速地修正问题，并缩短停机时间：

1. 如果您在创建工具链时配置此工具集成，请在“可配置的集成”部分中，单击 **PagerDuty**。
1. 如果您具有工具链，且要将此工具集成添加到该工具链，请在 DevOps 仪表板的**工具链**选项卡上，单击该工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**。然后，单击**工具集成**。 
1. 单击添加按钮 (+)。
1. 在“工具集成”部分中，单击 **PagerDuty**
1. 输入与 PagerDuty 帐户相关联的 PagerDuty 站点名称。如果您没有 PagerDuty 帐户，请[注册帐户](https://signup.pagerduty.com/accounts/new){: new_window}。
1. 输入 PagerDuty 帐户的 API 访问密钥。有关查找密钥的指示信息，请参阅 [API 认证](https://signup.pagerduty.com/accounts/new){: new_window}。
1. 输入 PagerDuty 服务的名称。
1. 输入主要 PagerDuty 联系人的电子邮件地址。
1. 输入主要 PagerDuty 联系人的电话号码。
1. 单击**创建集成**。
1. 单击 PagerDuty 的磁贴，以转至 pagerduty.com。您可以查看与您在为工具链配置此工具集成时所指定的 PagerDuty 服务相关联的事件。 

要了解更多信息，请参阅 [PagerDuty](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}。


## 配置 Sauce Labs
{: #saucelabs}

Sauce Labs 运行功能单元测试。当 Sauce Labs 测试套件配置为 {{site.data.keyword.deliverypipeline}} 中的测试作业时，测试套件可以作为您持续交付过程的一部分，根据您的 Web 或移动应用程序，运行测试。这些测试可以为您的项目提供有价值的流程控制，充当防止部署错误代码的保护门。

配置 Sauce Labs，以在多个操作系统和浏览器上运行自动功能测试，以便您可以模拟用户可能使用 Web 站点或应用程序的方式。

1. 如果您在创建工具链时配置此工具集成，请在“可配置的集成”部分中，单击 **Sauce Labs**。
1. 如果您具有工具链，且要将此工具集成添加到该工具链，请在 DevOps 仪表板的**工具链**选项卡上，单击该工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**。然后，单击**工具集成**。 
1. 单击添加按钮 (+)。
1. 在“工具集成”部分中，单击 **Sauce Labs**。
1. 输入与 Sauce Labs 帐户相关联的用户名。您可以[在 Sauce Labs 帐户页面顶部的欢迎消息中查找用户名](https://saucelabs.com/account){: new_window}。
1. 输入 Sauce Labs 帐户的访问密钥。您可以[在 Sauce Labs 帐户页面的左下角查找密钥](https://saucelabs.com/account){: new_window}。
1. 单击**创建集成**。
1. 单击 Sauce Labs 的磁贴，以转至 saucelabs.com 并查看工具链的测试活动。

 **提示**：如果您将 Sauce Labs 测试作业添加到 {{site.data.keyword.deliverypipeline}}，那么您可以选择服务实例。

要了解更多信息，请参阅 [Sauce Labs](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}。


## 配置 Slack
{: #slack}

**重要信息**：团队中的每一个人都可以看到发布到公共 Slack 通道的通知。记住您要对发布的内容负责。

Slack 是基于云的实时消息传递和通知系统。Slack 提供持久交谈，可替代电子邮件用于团队协作，其互动性更高。您可以通过专用通道或与您工作直接相关的一组通道，与团队进行通信。您还可以通过通道或直接消息，在两人或多人之间共享文件和图像。直接消息和通道的通信会保留，以便您可以对它们进行搜索。 

配置 Slack，以从工具集成接收有关工具链的通知，如测试和部署活动：

1. 如果您在创建工具链时配置此工具集成，请在“可配置的集成”部分中，单击 **Slack**。
1. 如果您具有工具链，且要将此工具集成添加到该工具链，请在 DevOps 仪表板的**工具链**选项卡上，单击该工具链，以打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**。然后，单击**工具集成**。
1. 单击添加按钮 (+)。
1. 在“工具集成”部分中，单击 **Slack**。
1. 输入 Slack 帐户的 API 认证令牌。您必须使用生成的完全访问令牌，向 Slack 进行认证。有关查找令牌的指示信息，请参阅 [Slack 认证](https://api.slack.com/web#authentication){: new_window}。
1. 输入您想要发送通知的目标 Slack 通道的名称。如果指定的通道不存在，那么会创建该通道。如果通道已归档，那么会重新激活该通道。
1. 单击**创建集成**。
1. 单击 Slack 的磁贴。您可以在已配置的 Slack 通道中查看工具链的所有活动。

要了解更多信息，请参阅 [Slack](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}。
