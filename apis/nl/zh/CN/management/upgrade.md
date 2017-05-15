---

copyright:
  years: 2017
lastupdated: "2017-04-11"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 访问更多 API Management 功能
{: #upgrade}

通过 API Management，可控制调用速率、OAuth 以及查看分析结果。您可通过升级到 {{site.data.keyword.apiconnect_full}} 服务，掌握对 API 的更大管理控制权。{{site.data.keyword.apiconnect_short}} 服务提供了安全策略的更多选项，以及对速率限制的更大控制权。除此之外，您还能配置完全可定制的开发者门户网站，这样您就可以对 API 进行社交化，并参与开发者社区。其他优势包括：
* 生命周期管理
* 组合 API
* Web Service 集成
* 协议调解
* 通过模式生成 API
* 微服务开发

迁移到 {{site.data.keyword.apiconnect_short}} 服务非常容易，您不必重新创建通过 API Management 管理的任何 API。

## 将 API 迁移到 {{site.data.keyword.apiconnect_short}}
{: #migrate_api}

如果决定升级到 {{site.data.keyword.apiconnect_full}}，那么需要通过对 API Management 中的每个 API 完成以下步骤，将这些 API 从 API Management 迁移到 {{site.data.keyword.apiconnect_short}} 服务： 

1. 为 API Management 中的 API 下载 Swagger 文档。
    1. 打开应用程序，并选择 **API Management**。
	2. 选择 **API Explorer** 选项卡。这将显示与该项目相关的 API 的列表。
    2. 通过选择 API 名称旁的相应图标，下载该 API 的 Swagger 文档。
2. 创建并准备 {{site.data.keyword.apiconnect_short}} 实例。 
    1. 通过 {{site.data.keyword.Bluemix_notm}} 目录，创建 {{site.data.keyword.apiconnect_short}} 服务的实例。
	2. 选择套餐。
	3. 选择 **+添加**以创建目录。
	4. 输入目录的显示名称和名称，然后选择**添加**。
	5. 选择已创建的目录。
3. 通过完成以下步骤，将 Swagger 文档导入到 {{site.data.keyword.apiconnect_short}} 实例：
	1. 在 {{site.data.keyword.apiconnect_short}} 服务仪表板中，选择菜单中的**浏览至... (>>)** > **草稿**。
	2. 选择 API 选项卡。
	3. 选择 **+添加** > **从文件或 URL 导入 API**。
	4. 找到并选择从 API Management 下载的 Swagger 文件。选择**打开**。
	5. 选择**导入**以将 API 导入到 {{site.data.keyword.apiconnect_short}} 服务。
4. 指定 API 的设置。
    1. 选择**创建产品**。
	2. 选择已创建的产品以查看其设置。
	3. 为 API 设置速率限制。
	4. 为 API 设置层。
5. 根据需要，为 API 添加端点。
    1. 选择该 API。
	2. 选择“组合”选项卡。
	3. 添加端点（如果尚未指定）。
	
 迁移 API 后，您将能通过打开 {{site.data.keyword.apiconnect_short}} 服务磁贴以及通过 {{site.data.keyword.Bluemix_notm}}“仪表板”来访问所有 API Management 功能。 

 
