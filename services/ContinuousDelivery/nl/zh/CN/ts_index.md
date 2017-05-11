---

copyright:
  years: 2015, 2017
lastupdated: "2017-2-9"

---
<!-- Common attributes used in the template are defined as follows: -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.contdelivery_short}} 故障诊断
{: #ts_cd}

获取使用 {{site.data.keyword.contdelivery_full}} 的常见故障诊断问题的答案。
{:shortdesc}


## 无法获取 GitHub 的授权
{: #cannot_authorize_github}

您无法从 GitHub 获取授权。
{:shortdesc}

如果您未授权 {{site.data.keyword.Bluemix_notm}} 访问您的 GitHub 帐户，那么可能会发生以下任何问题：
{: tsSymptoms}

 * 当您尝试向工具链添加 GitHub 工具集成时，不会添加该工具集成。
 * 当您将更改推送至 GitHub 或 GitHub Enterprise 存储库时，管道不会自动运行。

{{site.data.keyword.Bluemix_notm}} 未获授权访问 GitHub。  
{: tsCauses}
 
如果您在创建工具链时配置 GitHub 工具集成，请遵循以下步骤：
{: tsResolve}
 
  1. 在“可配置的集成”部分中，单击 **GitHub**。 
  1. 如果您要在 {{site.data.keyword.Bluemix_notm}} Public 上创建工具链，但尚未授权 {{site.data.keyword.Bluemix_notm}} 访问 GitHub，请单击**授权**以转至 GitHub Web 站点。 
  1. 如果您没有活动的 GitHub 会话，那么系统会提示您登录。单击**授权应用程序**，以允许 {{site.data.keyword.Bluemix_notm}} 访问 GitHub 帐户。如果您有活动的 GitHub 会话但最近未输入过密码，那么系统可能会提示您输入 GitHub 密码以进行确认。
  
如果已经具有工具链，请更新 GitHub 工具集成的配置：

 1. 在 DevOps 仪表板的**工具链**页面上，单击工具链，以打开其“概述”页面。或者，在应用程序“概述”页面的“持续交付”卡上，单击**查看工具链**，然后单击**概述**。
 1. 在 GitHub 卡上，单击菜单并单击**配置**。
 1. 更新配置设置以授权 {{site.data.keyword.Bluemix_notm}} 访问 GitHub。单击**授权**以转至 GitHub Web 站点。如果您没有活动的 GitHub 会话，那么系统会提示您登录。单击**授权应用程序**，以允许 {{site.data.keyword.Bluemix_notm}} 访问 GitHub 帐户。如果您有活动的 GitHub 会话但最近未输入过密码，那么系统可能会提示您输入 GitHub 密码以进行确认。
 1. 完成更新设置时，单击**保存集成**。


## 未配置工具集成
{: #tool_integration_error}

为工具链配置工具集成后，在其工具卡上会显示`设置失败`错误。
{:shortdesc}

在您配置工具集成后，您在工具链的“概述”页面上查看其工具卡，并注意到设置失败。
{: tsSymptoms}

 ![设置失败错误](images/tool_setup_failed.png)
 
当您添加工具集成时，工具链会与工具集成所代表的工具进行通信，以供应任何必要资源，并将它们与工具链相关联。如果在设置过程中发生错误，或者工具链与工具之间的通信没有正确完成，那么工具集成会置于错误状态。
{: tsCauses}

再次配置工具集成：
{: tsResolve}

1. 在其工具卡上，将鼠标悬停在`设置失败`消息上并单击**重新配置**。

 ![“重新配置”按钮](images/tool_reconfigure.png)
 
1. 请确保您使用有效的配置参数。如果错误由无效的配置引起，那么会显示错误消息；例如，`无法设置集成。请检查设置并重试。
原因：api_key:fakeKey 无效`。请更新工具集成的设置并单击**保存集成**。
1. 如果错误由通信问题引起，请单击**保存集成**，然后重试。
