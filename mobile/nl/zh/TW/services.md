---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-11"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# 服務
{: #services}

從 {{site.data.keyword.Bluemix}} 行動儀表板的**服務**視圖中，您可以檢視現有服務，或建立新服務。行動儀表板提供單一位置，來檢視專案所管理的所有 Bluemix 服務。  

如果您從**服務**視圖中刪除服務，則會中斷服務與相關聯專案的連線。如果您要將服務重新連接至專案，請建立新的服務實例。

## {{site.data.keyword.Bluemix_notm}} 行動服務概觀
{: #mobile_services_overview}

下表說明 {{site.data.keyword.Bluemix_notm}} 行動服務。您可以使用 {{site.data.keyword.Bluemix_notm}} 型錄中的個別服務，或者可以將它們整合至行動專案。

<table summary="此表格說明 {{site.data.keyword.Bluemix_notm}} 行動服務，並提供服務文件的鏈結">
<caption>表格 1. {{site.data.keyword.Bluemix_notm}} 行動服務</caption>
<th>{{site.data.keyword.Bluemix_notm}} 行動服務</th>
<th>說明</th>
<tr>
<td> <img src="images/mobile_analytics_icon.png" alt="{{site.data.keyword.mobileanalytics_short}} 圖示"><br/>{{site.data.keyword.mobileanalytics_short}}</td>
<td valign="top">使用 {{site.data.keyword.mobileanalytics_full}} 服務來瞭解行動應用程式的執行方式及其使用方式。<br/><br/>
深入閱讀 <a href="/docs/services/mobileanalytics/index.html" alt="{{site.data.keyword.mobileanalytics_short}} 文件鏈結">{{site.data.keyword.mobileanalytics_short}} 文件</a>中的操作此服務。
</td>
</tr>
<tr>
<td><img src="images/authentication_icon
.png" alt="{{site.data.keyword.amashort}} 服務圖示"><br/>{{site.data.keyword.amashort}}</td>
<td valign="top">請使用 {{site.data.keyword.amafull}} 服務，將安全功能新增至行動應用程式。您可以配置用戶端鑑別及身分提供者，讓使用者可以利用其現有的 Google 或 Facebook 帳戶登入應用程式。<br/><br/>
深入閱讀<a href="/docs/services/mobileaccess/index.html" alt="{{site.data.keyword.amashort}} 文件鏈結">{{site.data.keyword.amashort}}文件</a>中的操作此服務。</td>
</tr>
<tr>
<td><img src="images/MFPFoundation_icon.png" alt="{{site.data.keyword.mobilefoundation_short}} 服務圖示"><br/> {{site.data.keyword.mobilefoundation_short}}</td>
<td valign="top">請使用 {{site.data.keyword.mobilefoundation_long}} 服務來加快設定 {{site.data.keyword.mfp_full}} 環境，您可以從中開發、測試及操作企業行動應用程式。<br/><br/>
深入閱讀 <a href="/docs/services/mobilefoundation/index.html" alt="{{site.data.keyword.mobilefoundation_short}} 文件鏈結">{{site.data.keyword.mobilefoundation_short}}文件</a>中的操作此服務。</td>
</tr>
<tr>
<td><img src="images/mqa_icon.png" alt="{{site.data.keyword.mqa}} 服務圖示"><br/>{{site.data.keyword.mqa}}</td>
<td valign="top">請使用 {{site.data.keyword.mqafull}} 服務，來探索並設定應用程式的行動品質服務。您可以檢視行動應用程式的高階品質度量值，快速瞭解您正在處理的應用程式的問題。這些度量值包括當機、錯誤、使用者意見及使用者觀感等資訊。透過檢視這個應用程式資訊，您可以判定是否要進一步調查特定問題。<br/><br/>
深入閱讀 <a href="/docs/services/MobileQualityAssurance/index.html" alt="{{site.data.keyword.mqa}} 文件鏈結">{{site.data.keyword.mqa}}文件</a>中的操作此服務。</td>
</tr>
<tr>
<td><img src="images/push_icon.png" alt="{{site.data.keyword.mobilepushshort}} 服務圖示"><br/>{{site.data.keyword.mobilepushshort}}</td>
<td valign="top">{{site.data.keyword.mobilepushfull}} 服務服務提供一個統一平台，來傳送及管理目標設為各種平台的行動及 Web 推送通知。
<br/><br/>
{{site.data.keyword.mobilepushshort}} 可管理應用程式使用者與其裝置、裝置平台、Web 瀏覽器的對映，並處理如何將推送通知分派給他們。您可以將播送、單點播送（根據 userID、deviceID），以及標籤（或主題）當作推送通知傳送給行動及 Web 瀏覽器應用程式使用者。您也可以使用 SDK 及 REST API，進一步開發用戶端應用程式。
<br/><br/>
在 <a href="/docs/services/mobilepush/index.html" alt="{{site.data.keyword.mobilepushshort}} 文件鏈結">{{site.data.keyword.mobilepushshort}} 文件</a>中閱讀操作此服務的相關資訊。</td>
</table>

## 整合行動服務
{: #services_integration}
您可以將現有 {{site.data.keyword.Bluemix_notm}} 行動服務（例如 {{site.data.keyword.cloudant}}）整合至專案中。


#### 整合 {{site.data.keyword.cloudant}}
{: #cloudant_integration}

若要整合現有的 {{site.data.keyword.cloudant}} 服務，請遵循下列步驟：

1. 按一下 {{site.data.keyword.cloudant}} 服務實例。
2. 按一下**啟動**。
3. 在**資料庫**視圖中，按一下您的「資料庫」名稱。
4. 按一下 **API**，然後透過您的資料庫名稱複製 **API 金鑰**值。

   **附註**：不要複製超過您的資料庫名稱的內容。

5. 按一下**許可權** > **產生 API 金鑰**，然後複製**金鑰**及**密碼**值。
6. 導覽回到行動儀表板的**專案**視圖。
7. 按一下您的專案，以對其進行編輯。
8. 按一下**資料** > **+ 資料來源** > **Cloudant**，提供您的資料來源名稱，然後按一下**新增**。
9. 按一下 **Cloudant 配置**。
10. 提供您先前複製到 **API URL** 的 **API 金鑰**值。
11. 提供您先前複製到**使用者**的**金鑰**值。
12. 提供您先前複製到**密碼**的**密碼**值。
13. 按一下**確定**。
