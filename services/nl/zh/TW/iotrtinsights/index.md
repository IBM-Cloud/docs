---

copyright:
  years: 2015,2016

---

{:new_window: target=_"blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 開始使用 {{site.data.keyword.iotrtinsights_full}}
{: #gettingstartedtemplate}
*前次更新：2016 年 2 月 11 日*

使用 {{site.data.keyword.iotrtinsights_full}} on Bluemix ({{site.data.keyword.iotrtinsights_short}})，您可以對來自 Internet of Things 裝置的即時資料執行分析，並深入了解其性能以及您的作業的整體狀態。
{:shortdesc}

您必須設定 {{site.data.keyword.iot_full}} 服務 ({{site.data.keyword.iot_short}}) 來將分析引擎連接至裝置，才能開始使用 {{site.data.keyword.iotrtinsights_short}}。您可以使用現有 {{site.data.keyword.iot_short}} 服務，或建立新的服務。若要快速開始進行，您可以將 Internet of Things 電話應用程式及其關聯的 {{site.data.keyword.iot_short}} 服務部署至組織。

若要快速開始使用此服務，請遵循下列步驟：
1. 將 {{site.data.keyword.iotrtinsights_short}} 服務部署至 Bluemix 組織。
  1. 從 Bluemix 帳戶儀表板中，按一下**使用服務或 API**。
  2. 找出服務型錄的 Internet of Things 區段，然後選取 **{{site.data.keyword.iotrtinsights_short}}**。
  3. 在 {{site.data.keyword.iotrtinsights_short}} 頁面上，驗證「新增服務」選項：  
    - 空間 - 驗證您是在已部署 {{site.data.keyword.iot_short}} 服務的相同空間中部署服務。
    - 應用程式 - 維持不連結。
    - 服務名稱 - 選擇性地將服務名稱變更為容易記住的名稱。此名稱會顯示在 Bluemix 儀表板的 IoT {{site.data.keyword.iotrtinsights_short}} 磚中。
    - 選取的方案 - 選取符合您需求的「免費」或購買方案。  
    > **重要事項：**使用免費 {{site.data.keyword.iotrtinsights_short}} 方案，每個組織只能部署一個服務實例。
  4. 按一下**使用**，以將 {{site.data.keyword.iotrtinsights_short}} 部署至 Bluemix 服務。
2. 選用項目：運用 IoT {{site.data.keyword.iotrtinsights_short}}，使用您的電話作為 IoT 裝置。
使用 Internet of Things 電話應用程式，可以快速地設定智慧型手機作為可用來驗證 {{site.data.keyword.iotrtinsights_short}} 環境的 IoT 裝置，以及開始定義對資料的即時分析。如需 Internet of Things 電話應用程式的相關資訊，請參閱 [Internet of Things 電話應用程式](https://github.com/ibm-messaging/IoT-html5-phone)專案。

  若要建立應用程式，並將電話連接至 {{site.data.keyword.iot_full}}，請執行下列動作：
  1. 按一下下面的按鈕，以啟動部署處理程序：
[![「部署至 Bluemix」圖示。](images/deploy_to_bluemix.png "「部署至 Bluemix」圖示")(https://bluemix.net/deploy?repository=https://github.com/ibm-messaging/iot-html5-phone "將 IoT 電話部署至 Bluemix")
  > **附註：**部署 Internet of Things 電話應用程式，也會部署自動連結至電話應用程式的 {{site.data.keyword.iot_short}} 服務 (*iot-phone-iotf-service*)。新增此 {{site.data.keyword.iot_short}} 作為資料來源，以測試 Internet of Things 電話應用程式。它也會建立應用程式所使用的 Cloudant NoSQL DB 服務 (*iot-phone-cloudant-cloudantNoSQLDB*)。

  2. 如果系統提示您自行核准「IBM Single Sign On 服務」的存取權（OAuth 同意），請按一下**核准**。  
  >**提示：**如果您沒有 Bluemix 帳戶，則可以註冊以啟動免費 Bluemix 試用。
  2. 將 APP NAME 欄位變更為容易記住的項目；在這些指示的其餘部分，我們將這稱為*電話應用程式*。此名稱將會顯示在 Bluemix 儀表板的應用程式磚中，並且是將電話連接至 {{site.data.keyword.iot_short}} 時使用的 URL 的一部分。
  2. 按一下**部署**。
  2. 部署處理程序完成並且看到「成功」訊息之後，請回到 Bluemix 儀表板。
  *電話應用程式*磚及 *iot-phone-iotf-service* 磚已新增至您的帳戶。
  1. 從 Bluemix 儀表板中，按一下*電話應用程式*磚。
  2. 透過您的電話開啟瀏覽器，並移至顯示在應用程式名稱下方的「路徑 URL」。系統提示時，在 {{site.data.keyword.iot_short}} 及 IoT {{site.data.keyword.iotrtinsights_short}} 儀表板中輸入所選擇的裝置 ID，以將電話識別為裝置。
  3. 按一下**連接**，以將電話連接至 {{site.data.keyword.iot_short}} *iot-phone-iotf-service*。
  視圖會重新整理，以顯示從電話傳送至 {{site.data.keyword.iot_short}} 的資料。
2. 建立及配置 Internet of Things 服務。  
> **提示：**如果您已部署 Internet of Things 電話應用程式，則已建立 *iot-phone-iotf-service*，因此可以跳過此步驟。  

  1. 登入 Bluemix 組織，然後選取您要在其中部署 IoT {{site.data.keyword.iotrtinsights_short}} 的空間。
  2. 從 Bluemix 儀表板中，按一下**使用服務或 API**。
  3. 找到服務型錄的「物聯網」區段，然後選取 **Internet of Things**。
  4. 在 {{site.data.keyword.iot_full}} 頁面上，驗證「新增服務」選項，然後按一下**使用**，以將 {{site.data.keyword.iot_short}} 新增至 Bluemix 服務。
  部署 {{site.data.keyword.iot_short}} 服務之後，會將您帶至服務管理頁面。
3. 找出連線 API 金鑰。
如果您已建立新的 {{site.data.keyword.iot_short}} 服務，則現在必須建立 API 金鑰，才能連接這兩個服務。如果您使用的是現有服務，則可以使用現有金鑰。  
  1. 從 Bluemix 儀表板中，按一下 Internet of Things 磚。  
  >**附註：**如果您使用的是 Internet of Things 電話應用程式，請按一下 *iot-phone-iotf-service* 磚。  

  1. 按一下**啟動儀表板**，以開啟 {{site.data.keyword.iot_full}} 儀表板。
  2. 導覽至**存取 > API 金鑰**。
  3. 按一下**產生 API 金鑰**。
  3. 記下「API 金鑰」、「鑑別記號」及 {{site.data.keyword.iot_short}} 儀表板頂端顯示的「組織 ID」。
  您可以在 IoT {{site.data.keyword.iotrtinsights_short}} 中使用此資訊來連接服務。
4. 連接 {{site.data.keyword.iot_short}} 服務及 IoT {{site.data.keyword.iotrtinsights_short}} 服務。
  1. 從 Bluemix 儀表板中，按一下 IoT {{site.data.keyword.iotrtinsights_short}} 磚。  
  2. 在服務頁面中，按一下**新增資料來源**。
  2. 在 {{site.data.keyword.iotrtinsights_short}} 主控台的「管理資料來源」頁面中，按一下**新增資料來源**。
  3. 提供資料來源的敘述性名稱，並提供下列您先前收集的資訊：
    - 組織 ID
    - API 金鑰
    - 鑑別記號
  4. 按一下 ![「建立」圖示](images/create.png "「建立」圖示")，以建立資料來源並進行連接。
4. 開始使用 {{site.data.keyword.iotrtinsights_short}}。
現在，透過新增使用者、連接您的裝置、配置儀表板來檢視相關的裝置資料，以及設定警示，即可開始使用 {{site.data.keyword.iotrtinsights_short}}。
>**選取 {{site.data.keyword.iotrtinsights_short}} 實例：**如果您已獲授權以操作員或管理者身分存取任何其他 {{site.data.keyword.iotrtinsights_short}} 實例，則可以快速切換這些實例。在 {{site.data.keyword.iotrtinsights_short}} 主控台中，按一下您的使用者名稱，然後選取您要存取的實例。   

# 相關鏈結
## 範例
* [Internet of Things 電話應用程式](https://github.com/ibm-messaging/IoT-html5-phone)
* [developerWorks Internet of Things 秘訣](https://developer.ibm.com/recipes/)
* [使用 Internet of Things 入門範本應用程式建立應用程式](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html#iot500)

## API
* [API 文件](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)

## 一般
* [關於](iotrtinsights_overview.html)   
* [Bluemix 服務的新增功能](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category)
* [開始使用 {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html)
* [IBM developerWorks 上的 dW 答案](https://developer.ibm.com/answers/topics/iot-real-time/)
