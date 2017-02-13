---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# {{site.data.keyword.visualrecognitionshort}} 程式碼入門範本的完整指導教學
{: #tutorial_vr}

下列完整指導教學逐步執行從「{{site.data.keyword.visualrecognitionshort}} 程式碼入門範本」（包括必須已安裝的工具）建立專案的步驟，隨後則進行在 Xcode 及 Android Studio 中執行入門範本的步驟。


### 安裝開發人員工具
{: #dev_tools}

確定您已安裝[必備的開發人員工具 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](get_code.html#prereq-dev-tools "外部鏈結圖示"){: new_window}。


### 從 {{site.data.keyword.visualrecognitionshort}} 程式碼入門範本建立專案
{: #create_project}

1. 在 {{site.data.keyword.Bluemix}} 中建立行動儀表板專案。

   1. 從行動儀表板的**開始使用**頁面中，按一下**建立專案**。

      您也可以按一下**專案**頁面中的**建立專案**。

   2. 按一下**程式碼入門範本**。

   3. 選取 **Visual Recognition**，然後按一下**建立專案**。

   4. 輸入專案名稱。對於此指導教學，使用 `VisualRecognitionProject`。
   
   5. 按一下**建立**。

2. 選用項目：新增 {{site.data.keyword.mobilepushshort}} 功能。

   1. 在**專案概觀**頁面中，對 **{{site.data.keyword.mobilepushshort}}** 按一下**新增**。

      或者，您可以從 **{{site.data.keyword.mobilepushshort}}** 頁面中按一下**建立**。

   2. 輸入服務名稱，然後按一下**建立**。

   3. 若為 iOS，請[配置 Apple Push Notification Service ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/mobilepush/t_push_provider_ios.html "外部鏈結圖示"){: new_window}。

   4. 若為 Android，請[配置 Firebase Cloud Messaging ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/mobilepush/t_push_provider_android.html "外部鏈結圖示"){: new_window}。
   
3. 選用項目：新增 Analytics 功能。

   1. 在**專案概觀**頁面中，針對 **Analytics** 按一下**新增**。

      您也可以按一下 **Analytics** 頁面中的**建立**。

   2. 輸入服務名稱，然後按一下**建立**。
   
   3. 在您執行應用程式之後，即可關閉**展示模式**來查看分析資料。
   
   4. 如需配置 Analytics 的相關資訊，請參閱[開始使用 {{site.data.keyword.mobileanalytics_short}} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/mobileanalytics/index.html "外部鏈結圖示"){: new_window}。
  
4. 選用項目：新增「鑑別」功能。

   1. 在**專案概觀**頁面上，針對**鑑別**按一下**新增**。

      您也可以選取**鑑別**頁面上的**建立**。

   2. 輸入服務名稱，然後按一下**建立**。
   
   3. 開啟**鑑別**。
   
   4. 選取您的身分提供者，並且輸入必要資訊以進行配置。您只能啟用一個身分提供者。

   5. 如需配置「鑑別」的相關資訊，請參閱[開始使用 {{site.data.keyword.amashort}} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/mobileaccess/index.html "外部鏈結圖示"){: new_window}。

5. 產生專案程式碼。

   1. 按一下**專案概觀**頁面上的**取得程式碼**，以選取您的平台及語言。
   
      您也可以按一下**程式碼**頁面。
      
   2. 若為 iOS，按一下 **iOS Swift**。
   
   3. 若為 Android，按一下 **Android**。
   
   4. 當專案程式碼生成完成時，請按一下**下載程式碼**來下載專案保存檔。


### 在 Xcode 中執行專案
{: #run_xcode}

1. 解壓縮 `VisualRecognitionProject-Swift.zip` 檔案。

2. 在 Markdown 檢視器中開啟 `README.md` 檔案，以檢閱配置專案的步驟。

   1. 建立您的[{{site.data.keyword.visualrecognitionshort}} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://console.{DomainName}/catalog/services/visual-recognition/ "外部鏈結圖示"){: new_window} 服務實例。
   
   2. 開啟終端機，然後導覽至您的專案資料夾。
   
      1. 如果您需要設定 CocoaPods 儲存庫，請執行 `pod setup`。
      
      2. 如果您需要更新現有 Pods，請執行 `pod update`。
      
      3. 執行 `pod install`，以安裝您專案所需的 Pods。
      
      4. 執行 `carthage update --platform iOS`，以建置相依關係及架構來使用 {{site.data.keyword.ibmwatson}} Developer Cloud iOS SDK。
      
   3. 開啟 `VisualRecognitionProject.xcworkspace` Xcode 工作區。
   
   4. 新增 {{site.data.keyword.visualrecognitionshort}} 服務認證。
   
      1. 從 {{site.data.keyword.visualrecognition}} 服務認證中複製您的 `api_key`。
      
      2. 將 `api_key` 貼入 `WatsonCredentials.plist` 檔案中的 `VisualRecognitionAPIKey` 金鑰。
      
3. 執行應用程式。


### 在 Android Studio 中執行專案
{: #run_studio}

1. 解壓縮 `VisualRecognitionProject-Android.zip` 檔案。

2. 在 Markdown 檢視器中開啟 `README.md` 檔案，以配置專案。

   1. 建立您的[{{site.data.keyword.visualrecognitionshort}} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://console.{DomainName}/catalog/services/visual-recognition/ "外部鏈結圖示"){: new_window} 服務實例。
   
      如果您已具有 {{site.data.keyword.visualrecognitionshort}} 服務實例，請跳過此步驟。
   
   2. 在 Android Studio 中開啟 `VisualRecognitionProject-Android` 專案。
   
   4. 新增 {{site.data.keyword.visualrecognitionshort}} 服務認證。
   
      1. 從 {{site.data.keyword.visualrecognitionshort}} 服務認證中複製您的 `api_key`。
      
      2. 將 `api_key` 貼入 `res/values/watson_credentials.xml` 檔案中的 `watson_visual_recognition_api_key` 金鑰。
      
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
* [指導教學 - Cloudant Sync](tutorial_cloudant_synd.html)
* [指導教學 - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [指導教學 - Watson Language](tutorial_watson_language.html)
* [指導教學 - Weather](tutorial_weather.html)

