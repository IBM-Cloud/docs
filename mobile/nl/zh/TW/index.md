---

copyright:
  years: 2016

---
{:new_window: target="_blank"}

# 從 Mobile 儀表板建立行動專案
{: #mobile}
*前次更新：2016 年 7 月 18 日*
{: .last-updated}

有了 {{site.data.keyword.Bluemix}} Mobile 服務，您可以將預先建置、受管理且可延展的雲端服務納入行動應用程式中，而不必仰賴 IT 參與。您可以聚焦在建置行動應用程式，而不是管理後端基礎架構的複雜情況。

Mobile 儀表板提供 {{site.data.keyword.Bluemix_notm}} 的整合體驗。您可以從儀表板內輕鬆地建立新的行動專案。有了**專案**視圖，您可以在某個工作區管理所有專案。**服務**視圖顯示現有的行動服務實例。

若要檢視 Mobile 儀表板，請從 {{site.data.keyword.Bluemix_notm}} 首頁按一下**行動**種類。
<img src="images/mobile_dashboard.jpg" alt="{{site.data.keyword.Bluemix_notm}} 首頁">

若要開始，請從 Mobile 儀表板的**專案**視圖中按一下**新建專案**。

## {{site.data.keyword.Bluemix_notm}} Mobile 服務概觀
{: #mobile_services_overview}

下表說明可用的 {{site.data.keyword.Bluemix_notm}} Mobile 服務。您可以使用 {{site.data.keyword.Bluemix_notm}} 型錄中的個別服務，或者可以將它們整合至行動專案。

<table summary="此表格說明 {{site.data.keyword.Bluemix_notm}} Mobile 服務，並提供服務文件的鏈結">
<caption>表格 1. {{site.data.keyword.Bluemix_notm}} Mobile 服務</caption>
<th>{{site.data.keyword.Bluemix_notm}} Mobile 服務</th>
<th>說明</th>
<tr>
<td> <img src="images/mobile_analytics_icon.png" alt="{{site.data.keyword.mobileanalytics_short}}圖示"><br/><b>{{site.data.keyword.mobileanalytics_short}}（實驗性）</b></td>
<td valign="top">請使用 {{site.data.keyword.mobileanalytics_full}} 服務來測量行動應用程式、行動使用者及行動裝置的狀態、行為及環境定義。<br/><br/>
深入閱讀 <a href="../services/mobileanalytics/index.html" alt="{{site.data.keyword.mobileanalytics_short}} 文件鏈結">{{site.data.keyword.mobileanalytics_short}}文件</a>中的操作此服務。
</td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="{{site.data.keyword.amashort}} 服務圖示"><br/><b>{{site.data.keyword.amashort}}</b></td>
<td valign="top">請使用 {{site.data.keyword.amafull}} 服務，將安全功能新增至行動應用程式。您可以配置用戶端鑑別及身分提供者，讓使用者可以利用其現有的 Google 或 Facebook 帳戶登入應用程式。<br/><br/>
深入閱讀<a href="../services/mobileaccess/index.html" alt="{{site.data.keyword.amashort}} 文件鏈結">{{site.data.keyword.amashort}}文件</a>中的操作此服務。</td>
</tr>
<tr>
<td><img src="images/MFPFoundation_icon.png" alt="{{site.data.keyword.mobilefoundation_short}} 服務圖示"><br/> <b>{{site.data.keyword.mobilefoundation_short}}</b></td>
<td valign="top">請使用 {{site.data.keyword.mobilefoundation_long}} 服務來加快設定 {{site.data.keyword.mfp_full}} 環境，您可以從中開發、測試及操作企業行動應用程式。<br/><br/>
深入閱讀 <a href="../services/mobilefoundation/index.html" alt="{{site.data.keyword.mobilefoundation_short}} 文件鏈結">{{site.data.keyword.mobilefoundation_short}}文件</a>中的操作此服務。</td>
</tr>
<tr>
<td><img src="images/mqa_icon.png" alt="{{site.data.keyword.mqa}} 服務圖示"><br/><b>{{site.data.keyword.mqa}}</b></td>
<td valign="top">請使用 {{site.data.keyword.mqafull}} 服務，來探索並設定應用程式的行動品質服務。您可以檢視行動應用程式的高階品質度量值，快速瞭解您正在處理的應用程式的問題。這些度量值包括當機、錯誤、使用者意見及使用者觀感等資訊。透過檢視這個應用程式資訊，您可以判定是否要進一步調查特定問題。<br/><br/>
深入閱讀 <a href="../services/MobileQualityAssurance/index.html" alt="{{site.data.keyword.mqa}} 文件鏈結">{{site.data.keyword.mqa}}文件</a>中的操作此服務。</td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="「推送通知」服務圖示"><br/><b>{{site.data.keyword.mobilepushshort}}</b></td>
<td valign="top">請使用 {{site.data.keyword.mobilepushfull}} 服務，來傳送及管理目標設為 iOS 及 Android 平台的行動推送通知。此服務可管理應用程式使用者與其裝置、裝置平台的對映，並處理如何將推送通知分派給裝置。使用此服務，您可以將播送、單點播送（根據 userID、deviceID）以及根據推送通知的標籤（或主題）傳送至行動應用程式使用者。<br/><br/>
深入閱讀 <a href="../services/mobilepush/index.html" alt="{{site.data.keyword.mobilepushshort}} 文件鏈結">{{site.data.keyword.mobilepushshort}}文件</a>中的操作此服務。</td>
</table>

## 整合行動服務
{: #services_integration}
您可以將現有的 {{site.data.keyword.Bluemix_notm}} Mobile 服務（例如 {{site.data.keyword.mobilepushshort}} 及 {{site.data.keyword.cloudant}}）整合至您的專案。

#### 整合 {{site.data.keyword.mobilepushshort}}
{: #push_integration}

若要整合現有的 {{site.data.keyword.mobilepushshort}} 服務，請遵循下列步驟：

1. 按一下 {{site.data.keyword.mobilepushshort}} 服務實例。
2. 按一下**行動選項**，然後複製**路徑** 及 **AppGuid** 值。

   **附註**：您的 {{site.data.keyword.mobilepushshort}} 服務必須連結至應用程式，才能看到**行動選項**。

3. 導覽回到 Mobile 儀表板的**專案**視圖。
4. 按一下您的專案，以對其進行編輯。
5. 按一下**推送**並啟用通知。
6. 提供您先前複製到**應用程式 ID** 的 **AppGuid** 值。
7. 提供您先前複製到**應用程式路徑 URL** 的**路徑**值。

#### 整合 {{site.data.keyword.cloudant}}
{: #cloudant_integration}

若要整合現有的 {{site.data.keyword.cloudant}} 服務，請遵循下列步驟：

1. 按一下 {{site.data.keyword.cloudant}} 服務實例。
2. 按一下**啟動**。
3. 在**資料庫**視圖中，按一下您的「資料庫」名稱。
4. 按一下 **API**，然後透過您的資料庫名稱複製 **API 金鑰**值。

   **附註**：不要複製超過您的資料庫名稱的內容。

5. 按一下**許可權** > **產生 API 金鑰**，然後複製**金鑰**及**密碼**值。
6. 導覽回到 Mobile 儀表板的**專案**視圖。
7. 按一下您的專案，以對其進行編輯。
8. 按一下**資料** > **+ 資料來源** > **Cloudant**，提供您的資料來源名稱，然後按一下**新增**。
9. 按一下 **Cloudant 配置**。
10. 提供您先前複製到 **API URL** 的 **API 金鑰**值。
11. 提供您先前複製到**使用者**的**金鑰**值。
12. 提供您先前複製到**密碼**的**密碼**值。
13. 按一下**確定**。


# 相關鏈結
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Experimental)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## 部落格文章
{: #general}
* [部落格文章：Introducing the Bluemix Mobile dashboard](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [部落格文章：Bluemix Mobile, Part 1: Creating a Store Catalog application](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [部落格文章：Bluemix Mobile, Part 2: Integrating custom Bluemix backend into the Store Catalog app](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}

## 指導教學與範例
{: #samples}
* [Mobile Backend for Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
