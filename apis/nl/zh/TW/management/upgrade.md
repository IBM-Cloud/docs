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

# 存取其他 API Management 特性
{: #upgrade}

API Management 可讓您控制呼叫率、OAuth 以及檢視分析。升級為 {{site.data.keyword.apiconnect_full}} 服務，就可以具有 API 的更高管理控制權。{{site.data.keyword.apiconnect_short}} 服務提供更多安全原則選項，並且具有比率限制的更高控制權。除此之外，您可以配置可完全自訂的「開發人員入口網站」以將 API 社交化，並吸引開發人員社群的參與。其他好處包括：
* 生命週期管理
* 複合 API
* Web 服務整合
* 通訊協定調解
* 從綱目產生 API
* 微服務開發

移轉至 {{site.data.keyword.apiconnect_short}} 服務十分簡單，而且您不需要重建任何目前使用 API Management 管理的 API。

## 將 API 移轉至 {{site.data.keyword.apiconnect_short}}
{: #migrate_api}

如果您決定升級至 {{site.data.keyword.apiconnect_full}}，則需要將 API 從 API Management 移轉至 {{site.data.keyword.apiconnect_short}} 服務，方法為針對每一個 API 完成下列步驟： 

1. 從 API Management，下載 API 的 Swagger 文件。
    1. 開啟應用程式，然後選取 **API Management**。
	2. 選取 **API 瀏覽器**標籤。即會顯示與該專案相關的 API 清單。
    2. 選取 API 名稱旁的圖示，以下載 API 的 Swagger 文件。
2. 建立及準備 {{site.data.keyword.apiconnect_short}} 實例。 
    1. 從 {{site.data.keyword.Bluemix_notm}} 型錄中，建立 {{site.data.keyword.apiconnect_short}} 服務的實例。
	2. 選取方案。
	3. 選取 **+新增**，以建立型錄。
	4. 輸入型錄的「顯示名稱」及名稱，然後選取**新增**。
	5. 選取您已建立的型錄。
3. 完成下列步驟，以將 Swagger 文件匯入至 {{site.data.keyword.apiconnect_short}} 實例：
	1. 從 {{site.data.keyword.apiconnect_short}} 服務儀表板中，選取功能表中的**導覽至... (>>)** > **草稿**。
	2. 選取 API 標籤。
	3. 選取 **+新增** > **從檔案或 URL 匯入 API**。
	4. 尋找並選取您已從 API Management 下載的 Swagger 檔案。選取**開啟**。
	5. 選取**匯入**，以將 API 匯入至 {{site.data.keyword.apiconnect_short}} 服務。
4. 指定 API 的設定。
    1. 選取**建立產品**。
	2. 選取您已建立用來檢視其設定的產品。
	3. 設定 API 的比率限制。
	4. 設定 API 的層級。
5. 新增 API 的端點（必要的話）。
    1. 選取 API。
	2. 選取「組合」標籤。
	3. 新增端點（如果尚未指定）。
	
 在您移轉 API 之後，即可存取所有 API Management 特性，方法是開啟 {{site.data.keyword.apiconnect_short}} 服務磚，也可以透過「{{site.data.keyword.Bluemix_notm}} 儀表板」進行。 

 
