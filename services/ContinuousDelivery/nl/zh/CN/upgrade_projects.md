---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-21"

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 将 {{site.data.keyword.jazzhub_short}} 项目升级到工具链
{: #upgrade_projects}

{{site.data.keyword.jazzhub}} 逐步发展到 {{site.data.keyword.contdelivery_full}}。作为该变化的一部分，项目将升级到工具链。 

您可以升级项目或等待其自动升级。基于最佳经验，请尽快升级项目，以便您可以控制工具链的名称及其创建所在的组织。  
{: shortdesc}

## 工具链
{: #compare_toolchains}

工具链与项目类似，但有以下几个重要的不同之处：

- 项目只能具有一个储存库和管道。工具链可以具有您所需的任意多个存储库和管道。
- 工具链可以包括项目中不可用的工具，如 Slack、Sauce Labs、PagerDuty 和 {{site.data.keyword.DRA_full}}。
- 工具链的访问权通过标准 Bluemix 组织管理。成员资格在组织级别维护，这与项目不同，其成员资格在项目级别维护。

您可以在 [YouTube ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://youtu.be/2SIPE1e7NJ4){: new_window} 上或从 [{{site.data.keyword.contdelivery_short}} 入门](/docs/services/ContinuousDelivery/index.html)中了解工具链的相关信息。
[![指向 YouTube 的外部链接](images/CD_video.png)](https://youtu.be/2SIPE1e7NJ4){: new_window}    

## 先决条件
{: #upgrade_prereqs}    

- 要访问已升级的项目的工具链，您需要 Bluemix 标识。在升级之前，您必须验证您具有活动 Bluemix 标识。如果您没有，请进行[注册](https://console.ng.bluemix.net/registration/)。
- 请确保您的 DevOps Services 项目所有者正确。通过项目创建的工具链将成为该所有者 Bluemix 组织的一部分。

**重要信息：**工具链中的 Eclipse Orion {{site.data.keyword.webide}} 独立于与项目相关联的 {{site.data.keyword.webide}}。如果您使用 {{site.data.keyword.webide}} 且您具有未提交的更改，请在升级之前先提交它们。  


## 从项目升级到工具链
{: #project_to_toolchain}

当项目已就绪可以进行升级时，在项目的卡上和“概述”页面上会显示消息。

![具有“准备升级”标签的卡图像](images/card-project-to-upgrade.png)

![升级时间消息](images/banner-ready-to-upgrade.png)

**提示：**您可以在“我的项目”页面上，通过菜单查找准备升级的项目： 

![“要升级的项目”菜单项的图像](images/menu-projects-to-upgrade.png)

## 启动升级过程
{: #start_upgrade}

在启动升级过程之前，您可以在 [YouTube ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://youtu.be/oaZVGveVxBg){: new_window} 上观看其运行。
[![指向 YouTube 的外部链接](images/migration-video2.png)](https://youtu.be/oaZVGveVxBg){: new_window}    
要将项目升级到工具链，请遵循以下步骤：

1. 要启动升级过程，请在条幅消息上，单击**立即升级**。此时将打开“项目升级工具链”页面。 

   ![升级页面的示例](images/project-upgrade-toolchain.png)

   如需升级过程的概述，请阅读该页面上的描述。在此情况下，因为项目使用 GitHub.com 上的存储库，所以工具链将连接到相同的 GitHub 存储库。工具链将包含新的管道，其包含与项目管道相同的阶段和作业。此外，工具链还包含指向 {{site.data.keyword.contdelivery_short}} 中运行的 Eclipse Orion {{site.data.keyword.webide}} 的指针。

2. 要定制工具链，您可以配置一些设置：

   - 要更改工具链的名称，请编辑**名称**字段。

      ![名称字段](images/name-change.png)

   - 要更改要在其中创建工具链的 {{site.data.keyword.Bluemix_notm}} 组织，请从帐户菜单中选择组织：

      ![Bluemix 组织选择器](images/bluemix-organization-chooser.png)

   因为工具链在组织级别管理，所以请确保选择需要访问工具链的项目成员已经存在或者可以添加的组织。 
  
3. 单击**创建**。此时将创建新的工具链，同时显示其“概述”页面。

   ![已升级工具链的概述](images/new-toolchain-page.png)

   - 要访问 GitHub 存储库或相关联的问题跟踪程序，请单击 **GitHub** 或 **Issues**。
   
   - 要访问管道，请单击 **Delivery Pipeline**。  
   
   - 要访问 {{site.data.keyword.webide}}（其包含检出至工作空间的存储库内容），请单击 **Eclipse Orion {{site.data.keyword.webide}}**。 

## 重新访问项目
{: #revisit_projects}

您已准备好使用新的工具链。现在，您的项目标签为“已升级”，且在“概述”页面上，会显示确认消息。

![具有“已升级”标签的项目卡图像](images/card-upgraded-project.png)

![已升级的项目](images/banner-upgraded.png)

您可以在“我的项目”页面上，从菜单选择**已升级的项目**，来查看哪些项目已升级。

![“已升级的项目”菜单项的图像](images/menu-upgraded-projects.png)

如果您需要还原升级，请删除工具链。然后，当返回到项目的“概述”页面时，会再次显示升级消息，准备好后就可以再次升级。

## 后续步骤
{: #upgrade_next_steps}   

1. 通过检查项目“概述”页面上的消息来确认升级已完成：    

   ![已升级的项目](images/banner-upgraded.png)    

2. 为团队成员提供工具链的访问权。    
    - 每个团队成员都必须具有有效的 Bluemix 帐户。没有帐户的团队成员必须进行[注册 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/registration){:new_window}。
    - 向工具链所属的组织添加团队成员。
3. 从工具链使用工具而非从 {{site.data.keyword.jazzhub_short}} 项目使用工具。例如，要从浏览器编辑代码，请从工具链使用 Web IDE。    

## 故障诊断
{: #upgrade_troubleshoot}    

如果您有疑问或问题，请发送电子邮件至 [hub@jazz.net](mailto:hub@jazz.net)。在电子邮件中，请包含 {{site.data.keyword.jazzhub_short}} 项目和 {{site.data.keyword.contdelivery_short}} 工具链的 URL。

