---

copyright:
  years: 2017
lastupdated: "2017-04-13"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 我的 API
{: #manage_api}

使用**查看受管 API** 选项卡可查看您管理的 API 以及您先前进行管理但当前未公开的 API 的总体状态。在**共享 API** 选项卡中，可以查看已经通过 API Management 或通过 {{site.data.keyword.apiconnect_short}} 服务与 {{site.data.keyword.Bluemix_notm}} 组织共享的所有 API。

可以使用 API 仪表板来查看通过 API Management 管理的所有 API。 

## 查看受管 API
{: #view_api}

在此可以查看为 {{site.data.keyword.openwhisk_short}} 操作和其他外部源创建的 API。

1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”中，选择**菜单**图标 > **服务** > **API**。
2. 要选择源，请单击**管理 API**。这将显示当前管理的 API 的列表。API 的类型包含以下类型：
    * 用户定义的端点 - 这些条目是 {{site.data.keyword.Bluemix_notm}} 环境外部的 API，由其 URL 端点进行跟踪。 
    * {{site.data.keyword.openwhisk_short}} 应用程序 - 这些条目是在 API 内部包装的 {{site.data.keyword.openwhisk_short}} 操作。

选择 API 的名称，以查看有关该 API 的更多详细信息。

## 创建受管 API
{: #create_mgd_api}

可以在不离开受管 API 列表的情况下，通过选择**创建受管 API** 向该列表添加 API。

选择要创建 {{site.data.keyword.openwhisk_short}} API 还是 API 代理（外部 API）后，输入新 API 的信息。  

这是唯一可以添加 API 代理（即外部 API）的位置。外部 API 是指不在 {{site.data.keyword.Bluemix_notm}} 组织空间中创建或存储的 API。可以通过指定外部 API 的外部端点的 URL 来管理该 API。在尝试使用 API Management 来查看它是否满足您的需求，或者已经具有使用现有 URL 运行的 API，而您并不想中断这些 API 时，此功能非常有用。 

有关用于创建 API 的必需设置的其他信息，请参阅[管理 API](manage_apis.html)。

## 使用共享 API
{: #share_api}

在**浏览共享 API** 选项卡中，可以查看其他人创建并与您共享的 API。您还可以为与 {{site.data.keyword.openwhisk_short}} 操作和 {{site.data.keyword.appconserviceshort}} 服务相关联的 API 创建 API 密钥。

1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”中，单击**菜单**图标 > **服务** > **API**。
2. 在导航中选择**浏览共享 API**。在此将显示您可以使用的所有 API。
3. 要使用 API，请选择该 API 以打开其开发者门户网站，在其中可以预订套餐以进行使用。 
4. 选择要管理的 API 后，请参阅[管理 API](manage_apis.html) 以获取有关如何完成以下任务的更多信息： 
    * 查看 API 使用情况
    * 创建 API 密钥
    * 使用 API Explorer 查看文档和测试 API。
