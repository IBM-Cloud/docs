---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-19"

---

# 從 {{site.data.keyword.mobilefirstbp}} Starter 樣板建立行動應用程式
{: #try_mobile}

您可以單獨使用每一個 {{site.data.keyword.Bluemix}} 行動服務。您也可以搭配 {{site.data.keyword.mobilefirstbp}} Starter 樣板一起使用它們來獲得最大優點。

若要開始使用，請使用 {{site.data.keyword.mobilefirstbp}} Starter 來建立應用程式。此樣板可讓您完成下列動作：

* 使用範本應用程式來建立 Node.js 運行環境。您可以使用此應用程式來提供伺服器端功能（例如 RESTful API 及靜態檔案）。<!-- You can read more about operating this application in the Developing Mobile Backend section.-->
* 佈建每一個 {{site.data.keyword.Bluemix_notm}} 行動服務的實例，並將服務連結至 Node.js 應用程式。

<!--
<img src="images/mf_boiler_icon.png" alt="Bluemix mobile services" width="500"> {{site.data.keyword.mobilefirstbp}} Starter boilerplate
-->

使用 {{site.data.keyword.mobilefirstbp}} Starter 樣板建立應用程式之後，即可取得每一個服務的 Hello Bluemix 範例，或開始檢測現有應用程式以使用 {{site.data.keyword.Bluemix_notm}} 服務。


## 服務概觀
{: #services-overview}
您可以透過使用 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobilefirstbp}} Starter 樣板以同時使用所有 {{site.data.keyword.Bluemix_notm}} 行動服務，也可以使用來自 {{site.data.keyword.Bluemix_notm}} 型錄的個別服務。下圖概述 {{site.data.keyword.Bluemix_notm}} 行動服務的元件。

![{{site.data.keyword.Bluemix_notm}} 行動服務架構](images/bms_architecture.jpg)

<table summary="此表格說明 {{site.data.keyword.Bluemix_notm}} 行動服務">
<caption>表格 1. {{site.data.keyword.Bluemix_notm}} 及企業系統</caption>
<th>{{site.data.keyword.Bluemix_notm}}</th>
<th>企業系統</th>
<tr>
<td> <img src="images/i_js_64.png" alt="Node.js 運行環境圖示"><b>Node.js</b> <br/>管理範本應用程式的 Node.js 運行環境是提供作為 {{site.data.keyword.mobilefirstbp}} Starter 樣板的一部分。您可以使用範本應用程式來提供伺服器端功能，例如 RESTful API 及靜態檔案。<br/>例如，您可能會擴充 Node.js 應用程式以進行自訂邏輯處理，或在公司的現有基礎架構中使用 REST API 進行連線。您在 {{site.data.keyword.Bluemix_notm}} 上建立的每一個應用程式都有唯一的應用程式 ID。您的行動應用程式搭配使用此 ID 與 SDK，來存取與該應用程式相關聯的服務。該平台使用此應用程式 ID 作為一般功能的環境定義（例如計量及記載）。
<!--You can read more about operating this application in the "Developing Mobile Backend" section.--></td>
<td valign="top"><b>資訊提供者</b> <br/>您可以使用在 {{site.data.keyword.Bluemix_notm}} 上管理的 Node.js 運行環境來連接至任何類型的資訊提供者：
<ul>
	<li>企業後端</li>
	<li>資料庫</li>
	<li>另一個所管理的協力廠商服務</li>
</ul>
</td>
</tr>
<tr>
<td><img src="images/authentication_icon.png" alt="{{site.data.keyword.amashort}} 服務圖示"> <b>{{site.data.keyword.amashort}}</b><br/>使用 {{site.data.keyword.amafull}} 服務來保護在 {{site.data.keyword.Bluemix_notm}} 上管理的 Node.js 及 Java for Liberty 應用程式。透過使用 {{site.data.keyword.amashort}} SDK 檢測行動應用程式，即可要求使用者登入以存取 Node.js 或 {{site.data.keyword.Bluemix_notm}} 行動服務。<!-- In addition to security capabilities, {{site.data.keyword.amashort}} also gathers analytics data, so that you can monitor your mobile application performance and collect client logs and usage statistics.--> </td>
<td valign="top"><b>使用者身分提供者</b> <br/>您可以使用下列身分提供者：<ul><li>Facebook</li><li>Google</li><li> 自訂</li></ul></td>
</tr>
<tr>
<td><img src="images/push_icon.png" alt="{{site.data.keyword.mobilepushshort}} 服務圖示"> <b>{{site.data.keyword.mobilepushshort}}</b><br/>{{site.data.keyword.mobilepushfull}} 服務提供一個統一平台，用來傳送及管理目標設為 Mobile（iOS 及 Android）平台及 Web 瀏覽器應用程式的推送通知。此服務可管理應用程式使用者與其裝置、裝置平台及瀏覽器的對映，並處理如何將推送通知分派給訂閱者。使用此服務，您可以將播送、單點播送（根據 userID、deviceID）以及根據推送通知的標籤（或主題）傳送給客戶。</td>
<td valign="top"><b>Push 服務提供者</b><ul><li>Apple Push Notifications Service</li><li>Firebase Cloud Messaging</li></ul></td>
</tr>
<tr>
<td><img src="images/cloudant64.png" alt="Cloudant 服務圖示"><b>Cloudant NoSQLDB</b><br/> Cloudant 是 NoSQL 資料庫即服務 (DBaaS)。它從基礎建置，擴充至全球，不間斷地執行，並且處理各式各樣的資料類型，如 JSON、全文和地理空間。</td>
<td>Cloudant.com</td>
</tr>
</table>
