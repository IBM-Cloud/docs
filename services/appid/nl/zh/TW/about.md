---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# 如何運作
{: #about}

您可以了解 {{site.data.keyword.appid_short_notm}} 使用的元件、架構及要求流程。
{:shortdesc}


您可以透過下列方式來使用服務：

* 新增對行動及 Web 應用程式的鑑別
* 授與對受保護後端資源及 Web 應用程式的存取權
* 保護 {{site.data.keyword.Bluemix_notm}} 上所裝載的 Node.js 及 Swift 應用程式
* 儲存使用者資料（例如其公用社交設定檔中的應用程式喜好設定或資訊）
* 使用已儲存的資料來建置個人化應用程式體驗
* 保護已鑑別及匿名使用者的資源

**附註**：實作的通訊協定完全符合 OpenID Connect (OIDC) 的標準。


## 元件
{: #components}

* 儀表板 - 下載上線範例、查看活動日誌、配置各種鑑別類型及身分提供者
* 用戶端 SDK - 建置行動及 Web 應用程式，以使用服務來實作使用者鑑別
    * Android 的必要條件：API 25 或更新版本、Java 8.x、Android SDK Tools 25.2.5 或更新版本、Android SDK Platform Tools 25.0.3 或更新版本、Android Build Tools 25.0.2 版
    * iOS 的必要條件：iOS9 或更新版本、MacOS 10.11.5、Xcode 8.2
* 伺服器 SDK - 保護 {{site.data.keyword.Bluemix_notm}} 上所裝載的資源
    * 支援的運行環境是 Node.js 及 Swift

## 架構概觀
{: #architecture}

使用 {{site.data.keyword.appid_short_notm}}，您可以藉由要求使用者登入，為您的應用程式增加一個安全等級。您也可以使用伺服器 SDK 來保護後端資源。

下圖顯示 {{site.data.keyword.appid_short_notm}} 服務運作方式的概觀。

![{{site.data.keyword.appid_short_notm}} 架構圖](/images/appid_architecture2.png)

圖 1. {{site.data.keyword.appid_short_notm}} 架構圖

<dl>
  <dt> 用戶端 SDK</dt>
    <dd> 用戶端 SDK 提供要求類別以便與您的雲端資源通訊。用戶端 SDK 會在偵測到授權盤查時自動開始鑑別處理程序。</dd>
  <dt> Bluemix</dt>
    <dd>  伺服器 SDK 從要求擷取存取記號，並向 {{site.data.keyword.appid_short_notm}} 驗證它。成功鑑別之後，{{site.data.keyword.appid_short_notm}} 會傳回授權及身分記號給您的應用程式。</dd>
  <dt> 身分提供者</dt>
    <dd> 您可以配置 Facebook 及（或）Google 來鑑別應用程式。</dd>
</dl>


## 要求流程
{: #request}

下圖說明要求如何從用戶端 SDK 流向後端應用程式及身分提供者。

![{{site.data.keyword.appid_short_notm}} 要求流程](/images/appidflow.png)


* 使用 {{site.data.keyword.appid_short_notm}} 用戶端 SDK，對使用 {{site.data.keyword.appid_short_notm}} 伺服器 SDK 保護的後端資源提出要求。
* {{site.data.keyword.appid_short_notm}} 伺服器 SDK 偵測到未獲授權的要求，並傳回 HTTP 401 及授權範圍。
* 用戶端 SDK 自動偵測到 HTTP 401，並啟動鑑別處理程序。
* 當用戶端 SDK 與服務聯絡時，如果已配置多個身分提供者，伺服器 SDK 會傳回登入小組件。{{site.data.keyword.appid_short_notm}} 呼叫身分提供者，並提出該提供者的登入表單，或是在沒有配置任何身分提供者的情況傳回一個授權碼，允許他們鑑別。
* {{site.data.keyword.appid_short_notm}} 提供鑑別盤查，以要求用戶端應用程式進行鑑別。
* 如果已配置 Facebook 或 Google，而使用者進行登入，則鑑別會有個別的身分提供者 OAuth 流程處理。
* 如果鑑別最後具有相同的授權碼，授權碼會傳送給記號端點。端點傳回兩個記號：存取記號，與身分記號。從此時起，使用用戶端 SDK 所提出的所有要求都會有新取得的授權標頭。
* 用戶端 SDK 自動重新傳送已觸發授權流程的原始要求。
* 伺服器 SDK 從要求擷取授權標頭、向服務驗證授權標頭，然後授與對後端資源的存取權。
