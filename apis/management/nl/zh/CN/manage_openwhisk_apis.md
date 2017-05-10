---

copyright:
  years: 2017
lastupdated: "2017-04-12"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 通过 {{site.data.keyword.openwhisk_short}} 操作创建 API
{: #manage_openwhisk_apis}

OpenWhisk 操作可通过由 API Management 进行管理而受益。

使用 API Management，可以将 {{site.data.keyword.openwhisk_short}} 操作作为 API 公开。定义 API 后，可以应用安全性和速率限制策略，查看 API 使用情况和响应日志，以及定义 API 共享策略。  

要创建 {{site.data.keyword.openwhisk_short}} API，请完成以下步骤：

1. 在 {{site.data.keyword.openwhisk_short}}“仪表板”中，单击 **API** 选项卡。如果已经创建了 {{site.data.keyword.openwhisk_short}} API，那么会显示 {{site.data.keyword.openwhisk_short}} API 的列表。如果您还没有任何 {{site.data.keyword.openwhisk_short}} API，那么会显示“开始使用”屏幕。 
2. 单击**创建 {{site.data.keyword.openwhisk_short}} API**。这将显示“创建 {{site.data.keyword.openwhisk_short}} API”窗口。 
3. 填写“API 信息”部分中的字段，然后单击**创建操作**。这将显示“创建操作”窗口。可创建用于为 API 定义端点、HTTPS 路径和方法的操作。
4. 在“创建操作”窗口中，填写必填字段，然后选择**创建**。该操作将添加到用于调用 {{site.data.keyword.openwhisk_short}} 操作表的“操作”中。
5. 填写您希望填写的其余信息。也可以日后管理 API 时添加或更新其余信息。
6. 单击**保存**。这将打开 API 的“API Management 概述”页面，并且显示刚才定义的所有信息。
7. 继续使用[管理 API](manage_apis.html) 来管理 API。
