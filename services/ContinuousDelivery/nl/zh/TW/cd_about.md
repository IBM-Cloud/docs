---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 關於 Continuous Delivery  
{: #cd_about}  

使用 {{site.data.keyword.contdelivery_full}} 時，您可以使用 DevOps 作法及業界領先工具來建置、測試及提供應用程式。
{:shortdesc}

{{site.data.keyword.contdelivery_short}} 服務支援 DevOps 工作流程：

 * 您可以建立整合式 DevOps 開放式[工具鏈](/docs/services/ContinuousDelivery/toolchains_about.html){: new_window}，來啟用支援開發、部署及操作作業的工具整合。

  工具鏈是一組整合式工具，可用來協同開發、建置、部署、測試及管理應用程式。您可以建立工具鏈，內含 {{site.data.keyword.Bluemix_notm}} 服務、開放程式碼工具，以及讓開發及作業可重複進行且更易於管理的協力廠商工具，例如 GitHub、PagerDuty 及 Slack。

 * 使用自動化[管線](/docs/services/ContinuousDelivery/pipeline_about.html){: new_window}進行持續交付。

  自動進行建置、單元測試、部署及其他作業。以最少人為介入的可重複方式進行建置、測試及部署。隨時準備好投入正式作業。

 * 使用 [Web 型 IDE](/docs/services/ContinuousDelivery/web_ide.html){: new_window}，從任何位置編輯及推送程式碼。

  在 GitHub 中，建立、編輯、執行、除錯及完成來源控制作業。平順地從編輯程式碼，移至將程式碼部署至正式作業。

 * 透過 [{{site.data.keyword.DRA_short}}](/docs/services/ContinuousDelivery/di_working.html){: new_window} 改善品質。

  瞭解團隊在開發及交付程式碼時的動態。瞭解使用者如何與應用程式互動。請檢閱資料，以協助您管理應用程式的作業。


## Bluemix 公用與 Bluemix 專用的工具鏈可用性比較
{: #public_and_dedicated}

「{{site.data.keyword.Bluemix_notm}} 公用」是一種開放式標準雲端型平台，您可以在其中建置、執行及管理 [http://bluemix.net ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://bluemix.net){:new_window} 所存取的應用程式。「{{site.data.keyword.Bluemix_notm}} 專用」在專用 SoftLayer 環境中提供 {{site.data.keyword.Bluemix_notm}} 功能，該環境可安全地連接至「{{site.data.keyword.Bluemix_notm}} 公用」環境及網路。您公司的「{{site.data.keyword.Bluemix_notm}} 專用」環境可能未包含與「{{site.data.keyword.Bluemix_notm}} 公用」網站相同的工具整合。

對於原始碼管理及問題追蹤，「{{site.data.keyword.Bluemix_notm}} 公用」一般會使用 github.com。「{{site.data.keyword.Bluemix_notm}} 專用」也可以使用 github.com，但一般會使用公司所安裝或 IBM 所管理的 {{site.data.keyword.ghe_short}}。

「{{site.data.keyword.Bluemix_notm}} 公用」及「{{site.data.keyword.Bluemix_notm}} 專用」上都提供 {{site.data.keyword.contdelivery_short}}。視您是在「{{site.data.keyword.Bluemix_notm}} 公用」還是「{{site.data.keyword.Bluemix_notm}} 專用」上使用 {{site.data.keyword.contdelivery_short}} 而定，工具鏈會有所不同。

**提示**：工具鏈是在美國南部地區進行管理。如果您的工具鏈已配置成將應用程式部署至不同地區，則仍會將應用程式部署至該地區。

|工具鏈 |{{site.data.keyword.Bluemix_notm}} 公用	|{{site.data.keyword.Bluemix_notm}} 專用 |
|:----------|:------------------------------|:------------------|
|工具整合 		|如需所支援工具整合的清單，請參閱[配置工具整合](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}。 		|可用的工具整合取決於 {{site.data.keyword.contdelivery_short}} 在您環境中的設定方式。			|
|從範本建立工具鏈		|登入 [{{site.data.keyword.Bluemix_notm}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://console.ng.bluemix.net/devops){:new_window}		|登入 {{site.data.keyword.Bluemix_notm}} 的「專用」環境。			|
|從應用程式建立工具鏈		|應用程式會配置成從已移入應用程式入門範本程式碼的新 GitHub 儲存庫進行持續交付。		|應用程式會配置成從已移入應用程式入門範本程式碼的新 GitHub 或 GitHub Enterprise 儲存庫進行持續交付。		|  
|交付管線部署地區		|Cloud Foundry 部署工作可以使用所有「{{site.data.keyword.Bluemix_notm}} 公用」地區。 		|「{{site.data.keyword.Bluemix_notm}} 專用」地區可供使用。視 {{site.data.keyword.contdelivery_short}} 在您特定環境中的設定方式而定，也可使用相同客戶帳戶內的其他「專用」或「本端」地區。		|
|交付管線部署工作		|所有[工作類型](/docs/services/ContinuousDelivery/pipeline_about.html#deliverypipeline_jobs)都可供使用。		|可能無法使用與「專用」環境中未安裝之 {{site.data.keyword.Bluemix_notm}} 服務相依的工作類型。例如，在沒有 {{site.data.keyword.Bluemix_notm}} Container 服務的環境中，可能無法使用容器建置及部署工作類型。	|
{: caption="表 1.「Bluemix 專用」及「Bluemix 公用」上的工具鏈差異" caption-side="top"}


## 工具鏈範本
{: #templates}

您可以使用範本作為起點來[建立工具鏈 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/devops/create){: new_window}。工具鏈範本包含可支援開發、部署及操作作業的特定工具整合集。

**提示**：您公司的「{{site.data.keyword.Bluemix_notm}} 專用」環境可能未包含與「{{site.data.keyword.Bluemix_notm}} 公用」網站相同的工具鏈範本。「{{site.data.keyword.Bluemix_notm}} 公用」及「{{site.data.keyword.Bluemix_notm}} 專用」上可用的工具鏈範本可能包含「{{site.data.keyword.Bluemix_notm}} 專用」上的不同工具整合集。

部分工具鏈範本包含 {{site.data.keyword.contdelivery_short}} 服務所屬的工具整合。如果組織中還沒有該服務的實例，則在按一下**建立**以建立工具鏈時，會自動新增服務，而且不需要支付任何費用。如需相關資訊及術語，請參閱 [Bluemix 型錄 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/catalog/services/continuous-delivery/){:new_window}。

微服務工具鏈範本會部署具有 Cloudant 儲存庫所支援之 Catalog 及 Orders API 的應用程式。部署應用程式時，會建立不需要成本的 Cloudant 服務實例。如需相關資訊及術語，請參閱 [Bluemix 型錄 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/catalog/services/cloudant-nosql-db/){:new_window}。

|範本 |說明	|
|:----------|:------------------------------|
|[Garage Method 雲端原生指導教學工具鏈 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fcloud-native-toolchain-tutorial){:new_window} 		|此工具鏈示範 Garage Method 中所具備的 DevOps 作法。已預先配置此工具鏈，以進行持續交付、來源控制、測試自動化，以及自動化監視和作業。它會隨附以 Node.js Express 4 撰寫的範例應用程式，而且您可以進一步予以擴充。 		|
|[搭配 {{site.data.keyword.DRA_short}} 的微服務工具鏈 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Ftoolchain-demo){:new_window} 		|使用此雲端原生工具鏈，您可以使用範例來建立包含三個微服務的線上商店：Catalog API、Orders API 以及呼叫這兩個 API 的使用者介面。已預先配置此工具鏈，以進行持續交付、來源控制、功能測試、問題追蹤、線上編輯及警示通知。 		|
|[搭配 {{site.data.keyword.DRA_short}} 的微服務工具鏈（第 2 版）![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fmicroservices-toolchain-hosted){:new_window} 		|使用此雲端原生工具鏈，您可以使用範例來建立包含三個微服務的線上商店：Catalog API、Orders API 以及呼叫這兩個 API 的使用者介面。已預先配置此工具鏈，以進行持續交付、來源控制、功能測試、問題追蹤、線上編輯及警示通知。 		|
|[安全的容器工具鏈 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsecure-container-toolchain){:new_window} 		|運用此工具鏈，您可以開發及部署安全 Docker 容器應用程式。根據預設值，此工具鏈會使用範例 Node.js "Hello World" 應用程式，但您可以改為鏈結至自己的 GitHub 儲存庫。已預先配置此工具鏈，以進行「漏洞警告器」的持續交付、來源控制、問題追蹤及線上編輯。 		|
|[簡式 Cloud Foundry 工具鏈 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain){:new_window}		|運用此工具鏈，您可以開發及部署 Cloud Foundry 應用程式。根據預設值，此工具鏈會使用範例 Node.js "Hello world" 應用程式，但您可以改為鏈結至自己的 GitHub 儲存庫。已預先配置此工具鏈，以進行持續交付、來源控制、問題追蹤及線上編輯。 		|
|[簡式 Cloud Foundry 工具鏈（第 2 版）![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain-hosted){:new_window}	|運用此工具鏈，您可以開發及部署 Cloud Foundry 應用程式。根據預設值，此工具鏈會將範例 Node.js "Hello world" 應用程式複製到 IBM 所管理的 Git 儲存庫，您之後可以進行修改。已預先配置此工具鏈，以進行持續交付、來源控制、問題追蹤及線上編輯。 		|
|[搭配 {{site.data.keyword.DRA_short}} 的簡式 Cloud Foundry 工具鏈 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdra-toolchain-demo){:new_window}		|運用此雲端原生工具鏈，您可以使用 {{site.data.keyword.DRA_short}} 來限制簡式 Cloud Foundry 應用程式的部署。根據預設值，此工具鏈會使用範例 Node.js Weather 應用程式，或者，您可以鏈結至自己的 GitHub 儲存庫。 		|
|[簡式容器工具鏈 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-container-toolchain){:new_window}		|運用此工具鏈，您可以開發及部署 Docker 容器應用程式。根據預設值，此工具鏈會使用範例 Node.js "Hello World" 應用程式，但您可以改為鏈結至自己的 GitHub 儲存庫。已預先配置此工具鏈，以進行持續交付、來源控制、問題追蹤及線上編輯。 		|
|[Delivery Insights with IBM UrbanCode Deploy ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdeliveryinsights-toolchain){:new_window}		|運用此工具鏈，您可以從 IBM UrbanCode Deploy 檢視部署度量。讓此工具鏈從 {{site.data.keyword.DRA_short}} 中的「設定」頁面下載及配置 DevOps Connect，以與 IBM UrbanCode Deploy 進行通訊。 		|
|[Deployment Risk Analytics with GitHub and Jenkins ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevopsinsights-toolchain){:new_window}		|運用此工具鏈，您可以瞭解進行持續整合及交付的 Jenkins 處理程序。在 Jenkins 執行工作時，您可以配置 Jenkins 伺服器以將資料傳送至 {{site.data.keyword.DRA_short}}。您也可以實作品質限制，以根據原則來封鎖部署。您可以在 {{site.data.keyword.DRA_short}} 的「部署風險」儀表板上檢視結果。如果您配置 GitHub 儲存庫以指出 Jenkins 所使用的來源儲存庫，則可以使用變更可追蹤性。  		|
|[Developer Insights and Team Dynamics with GitHub and JIRA ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevteaminsights-toolchain){:new_window}		|運用此工具鏈，您可以探索專案的開發風險，以及使用社交編碼分析來瞭解開發人員之間的互動型樣。您可以搭配使用 GitHub Issues、JIRA Issues 或兩者同時使用來分析 GitHub 原始碼。使用 Developer Insights 來識別很容易出錯的檔案，以及查看如何使用 DevOps 作法來編譯專案。Team Dynamics 中的社交編碼分析可識別團隊成員之間的互動層次，讓團隊可以修正不具生產力的作法。 		|
|[建置您專屬的工具鏈 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fempty-toolchain){:new_window}		|此工具鏈沒有預先配置的工具。如果您已熟悉工具鏈，則可以設定自己的工具鏈。 		|
{: caption="表 2. 工具鏈範本" caption-side="top"}
