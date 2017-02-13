---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Cloudant Sync Code Starter 的完整指導教學
{: #tutorial}

下列完整指導教學逐步執行從 Cloudant Sync Code Starter 建立專案的步驟，包括您必須安裝的工具，以及在 Android Studio 中執行入門範本的步驟。


### 安裝開發人員工具
{: #dev_tools}

確定您已安裝[必備的開發人員工具 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](get_code.html#prereq-dev-tools "外部鏈結圖示"){: new_window}。


### 從 Cloudant Sync Code Starter 建立專案
{: #create_project}

1. 在 {{site.data.keyword.Bluemix}} 中建立行動儀表板專案。

   1. 從行動儀表板的**開始使用**頁面中，按一下**建立專案**。

      您也可以按一下**專案**頁面中的**建立專案**。

   2. 按一下**程式碼入門範本**。

   3. 選取 **Cloudant Sync**，然後按一下**建立專案**。

   4. 輸入專案名稱。對於此指導教學，使用 `CloudantSyncProject`。
   
   5. 按一下**建立**。

2. 新增「資料」功能。您可以建立新的 {{site.data.keyword.cloudant}} 服務實例或新增現有的服務實例。

   1. 在**專案概觀**頁面上按一下**資料**磚上的**檢視**。

      或者，您可以按一下**建立**或**新增現有項目**，然後在**資料**頁面上按一下 **Cloudant NoSQL DB**。
      
   2. 選用項目：如果您選擇建立新的服務實例，請輸入您的服務名稱然後按一下**建立**。

   3. 選用項目：如果您選擇新增現有的服務實例，請從清單選取您的服務實例，然後按一下**新增現有項目**。

   4. 按一下服務磚裡的**功能表**圖示，然後選取**啟動...** 來啟動服務實例。

      1. 按一下**啟動**以啟動您的 {{site.data.keyword.cloudant}} 主控台。

      2. 按一下**建立資料庫**、輸入您的資料庫名稱，然後按一下**建立**。

      3. 按一下**所有文件**旁邊的 **+** 圖示以新增文件。

3. 選用項目：新增 {{site.data.keyword.mobilepushshort}} 功能。

   1. 在**專案概觀**頁面中，對 **{{site.data.keyword.mobilepushshort}}** 按一下**新增**。

      或者，您可以從 **{{site.data.keyword.mobilepushshort}}** 頁面中按一下**建立**。

   2. 輸入服務名稱，然後按一下**建立**。

   3. 若為 Android，請[配置 Firebase Cloud Messaging ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/mobilepush/t_push_provider_android.html "外部鏈結圖示"){: new_window}。
   
4. 選用項目：新增 Analytics 功能。

   1. 在**專案概觀**頁面中，針對 **Analytics** 按一下**新增**。

      您也可以按一下 **Analytics** 頁面中的**建立**。

   2. 輸入服務名稱，然後按一下**建立**。
   
   3. 在您執行應用程式之後，即可關閉**展示模式**來查看分析資料。
   
   4. 如需配置 Analytics 的相關資訊，請參閱[開始使用 {{site.data.keyword.mobileanalytics_short}} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/mobileanalytics/index.html "外部鏈結圖示"){: new_window}。
  
5. 選用項目：新增「鑑別」功能。

   1. 在**專案概觀**頁面上，針對**鑑別**按一下**新增**。

      您也可以選取**鑑別**頁面上的**建立**。

   2. 輸入服務名稱，然後按一下**建立**。
   
   3. 開啟**鑑別**。
   
   4. 選取您的身分提供者，並且輸入必要資訊以進行配置。您只能啟用一個身分提供者。

   5. 如需配置「鑑別」的相關資訊，請參閱[開始使用 {{site.data.keyword.amashort}} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/mobileaccess/index.html "外部鏈結圖示"){: new_window}。

6. 產生專案程式碼。

   1. 按一下**專案概觀**頁面上的**取得程式碼**，以選取您的平台及語言。
   
      您也可以按一下**程式碼**頁面。
      
   2. 若為 Android，按一下 **Android**。
   
   3. 當專案程式碼生成完成時，請按一下**下載程式碼**來下載專案保存檔。


### 在 Android Studio 中執行 Android 專案
{: #run_android}

1. 解壓縮 `CloudantSyncProject-Android.zip` 檔案。

2. 在 Markdown 檢視器中開啟 `README.md` 檔案，以配置專案。

   1. 在 Android Studio 中開啟 `CloudantSyncProject-Android` 專案。

   2. 新增您的 Cloudant 認證。

      1. 從**資料**頁面按一下服務磚裡的**功能表**圖示，然後選取**啟動...** 來啟動服務實例。

         1. 按一下**啟動**以啟動您的 {{site.data.keyword.cloudant}} 主控台。

         2. 按一下您的資料庫名稱，然後按一下**許可權**。

         3. 在 `res/values/cloudant_credentials.xml` 檔的 `cloudant_dbname` 字串輸入您的資料庫名稱。

         4. 按一下**產生 API 金鑰**。

             1. 複製**金鑰**值，然後將值貼入 `res/values/cloudant_credentials.xml` 檔的 `cloudant_api_key` 字串。

             2. 複製**密碼**值，然後將值貼入 `res/values/cloudant_credentials.xml` 檔的 `cloudant_api_password` 字串。

             3. 選取 **_admin** 許可權。
      
3. 執行應用程式。


## 下一步
{: #what_next}

檢視其他指導教學。


### 使用者介面入門範本指導教學
{: #tutorials_UI}

* [指導教學 - Store Catalog](tutorial_store_catalog.html)


### 程式碼入門範本指導教學
{: #tutorials_Code}

* [指導教學 - Basic](tutorial.html)
* [指導教學 - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [指導教學 - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [指導教學 - Watson Language](tutorial_watson_language.html)
* [指導教學 - Weather](tutorial_weather.html)
