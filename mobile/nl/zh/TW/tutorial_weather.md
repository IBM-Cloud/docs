---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# 指導教學 - Weather 程式碼入門範本
{: #tutorial_weather}

「{{site.data.keyword.Bluemix}} Mobile for Weather 程式碼入門範本」展示使用 Swift 來開始使用 Weather 的臨時專案，並且包括 Push 及 Analytics 整合點。


## 需求
{: #tutorial_requirements}

* 一個 [Bluemix ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://bluemix.net "外部鏈結圖示") 帳戶
* [Weather Company 資料 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://console.{DomainName}/catalog/services/weather-company-data/ "外部鏈結圖示") 服務實例（取自於 [Bluemix 型錄 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://console.{DomainName}/catalog/ "外部鏈結圖示")）


## 開始使用
{: #tutorial_gs}

若要快速開始進行「Weather 程式碼入門範本」，請遵循下列步驟：

1. 在 {{site.data.keyword.Bluemix_notm}} 中建立行動儀表板專案。

   1. 從行動儀表板的**開始使用**頁面中，按一下**建立專案**。

      您也可以按一下**專案**頁面中的**新建專案**。

   2. 按一下**程式碼入門範本**。

   3. 選取 **Weather**，然後按一下**建立專案**。

   4. 輸入專案名稱，然後按一下**建立**。

2. 選用項目：新增 {{site.data.keyword.mobilepushshort}} 功能。

   1. 在**專案概觀**頁面中，對 **{{site.data.keyword.mobilepushshort}}** 按一下**新增**。

      或者，您可以從 **{{site.data.keyword.mobilepushshort}}** 頁面中按一下**建立**。

   2. 輸入服務名稱，然後按一下**建立**。

   3. 若為 iOS，請[配置 Apple Push Notification Service ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/mobilepush/t_push_provider_ios.html "外部鏈結圖示"){: new_window}。

   4. 若為 Android，請[配置 Google Cloud Messaging ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/mobilepush/t_push_provider_android.html "外部鏈結圖示"){: new_window}。
   
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

   5. 如需配置鑑別的相關資訊，請參閱[開始使用 Mobile Client Access ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/mobileaccess/index.html "外部鏈結圖示"){: new_window}。

5. 下載專案。

   1. 按一下**程式碼**，然後選取偏好的語言。

   2. 按一下**下載程式碼**。

5. 解壓縮保存檔，並且遵循 `README.md` 檔案中的指示。


## 下一步
{: #tutorial_next}

[試用看看吧！![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://console.{DomainName}/mobile/create-project?starter=fad1d49e-f7b6-3aff-9b53-14673fca4399 "外部鏈結圖示"){: new_window}


### 使用者介面入門範本指導教學
{: #tutorials_UI}

* [指導教學 - Store Catalog](tutorial_store_catalog.html)


### 程式碼入門範本指導教學
{: #tutorials_Code}

* [指導教學 - Basic](tutorial.html)
* [指導教學 - Cloudant Sync](tutorial_cloudant_synd.html)
* [指導教學 - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [指導教學 - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [指導教學 - Watson Language](tutorial_watson_language.html)
