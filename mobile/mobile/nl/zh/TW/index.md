# 建立行動式應用程式
{: #mobile}

有了 {{site.data.keyword.Bluemix_notm}} Mobile Services，您可以將預先建置、受管理且可延展的雲端服務納入行動式應用程式中，而不必仰賴 IT 參與。您可以聚焦在建置行動式應用程式，而不是管理後端基礎架構的複雜情況。

<table><caption>表 1. Bluemix Mobile Services 樣板</caption>
<tr>
	<td>每一個 Bluemix Mobile Services 都可以單獨使用。您也可以一起使用它們來獲得最大優點。若要開始使用，請使用「Bluemix Mobile Services 樣板」來建立應用程式。此樣板：
		<ul>
			<li>使用範本應用程式來建立 Node.js 執行時期。您可以使用此應用程式來提供伺服器端函數（例如 RESTful API 及靜態檔案）。您可以在「開發行動式後端」小節中深入閱讀如何操作此應用程式。</li>
			<li>
佈建每一個 Bluemix Mobile Services 的實例，並將服務連結至 Node.js 應用程式。</li>
		</ul>
	</td>
	<td> <img src="images/mf_boiler_icon.png" alt="Bluemix Mobile Services" width="500"> Bluemix Mobile Services 樣板</td>
</tr>
</table>

使用「Bluemix Mobile Services 樣板」建立應用程式之後，即可取得每一個服務的 HelloWorld 範例，或開始檢測現有應用程式以使用 Bluemix 服務。


## 服務概觀
{: #services-overview}
您可以使用「Bluemix Mobile Services 樣板」同時使用所有 Bluemix Mobile Services，也可以使用來自 Bluemix 型錄的個別服務。下圖概述 Bluemix Mobile Services 的所有元件。

![Bluemix Mobile Services 架構](images/bms_architecture.jpg)

<table>
<caption>表 2. Bluemix 及企業系統</caption>
<th>Bluemix</th>
<th>企業系統</th>
<tr>
<td> <img src="images/i_js_64.png" alt="Node.js 執行時期圖示"><b>Node.js</b> <br/> 管理範本應用程式的 Node.js 執行時期是提供作為 Bluemix Mobile Services 樣板的一部分。您可以使用範本應用程式來提供伺服器端函數（例如 RESTful API 及靜態檔案）。<br/>例如，您可能會擴充 Node.js 應用程式以進行自訂邏輯處理，或在公司的現有基礎架構中使用 REST API 進行連線。您在 Bluemix 上建立的每一個應用程式都有唯一的應用程式 ID。您的行動式應用程式搭配使用此 ID 與 SDK，來存取與該應用程式相關聯的服務。該平台使用此應用程式 ID 作為一般功能的環境定義（例如計量及記載）。您可以在「開發行動式後端」小節中深入閱讀如何操作此應用程式。</td>
<td valign="top"><b>資訊提供者</b> <br/>您可以使用在 Bluemix 上管理的 Node.js 執行時期來連接至任何類型的資訊提供者：
<ul>
	<li>企業後端</li>
	<li>資料庫</li>
	<li>另一個所管理的協力廠商服務</li>
</ul>
</td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="Mobile Client Access 服務圖示"> <b>Mobile Client Access</b><br/>使用 IBM Mobile Client Access for Bluemix 服務來保護在 Bluemix 上管理的 Node.js 及 Java for Liberty 應用程式。透過使用 Mobile Client Access SDK 檢測行動式應用程式，即可要求使用者登入以存取 Node.js 或 Bluemix Mobile Services。除了安全功能之外，Mobile Client Access 也會收集分析資料，因此，您可以監視行動式應用程式效能，以及收集用戶端日誌及使用統計資料。</td>
<td valign="top"><b>使用者身分提供者</b> <br/>您可以使用下列身分提供者：<ul><li>Facebook</li><li>Google</li></ul></td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="Push Notifications 服務圖示"> <b>Push Notifications</b><br/>IBM Push Notifications for Bluemix 服務提供一個統一平台，來傳送及管理目標設為 iOS 及 Android 平台的行動式推送通知。此服務可管理應用程式使用者與其裝置、裝置平台的對映，並處理如何將推送通知分派給裝置。使用此服務，您可以將播送、單點播送（根據 userID、deviceID）以及根據推送通知的標籤（或主題）傳送至行動式應用程式使用者。</td>
<td valign="top"><b>Push 服務提供者</b><ul><li>Apple Push Notifications Service</li><li>Google Cloud Messaging</li></ul></td>
</tr>
<tr>
<td><img src="images/cloudant64.png" alt="Cloudant 服務圖示"><b>Cloudant NoSQLDB</b><br/> Cloudant 是 NoSQL 資料庫即服務 (DBaaS)。它是從基礎建置，可以廣域擴充、不間斷地執行，並且處理廣泛的資料類型（例如 JSON、全文以及地理空間）。</td>
<td>Cloudant.com</td>
</tr>
</table>
