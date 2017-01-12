---

copyright:
  years: 2016
lastupdated: "2016-11-30"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 開始使用 {{site.data.keyword.mobileanalytics_short}}（測試版）

{: #gettingstartedtemplate}

{{site.data.keyword.mobileanalytics_full}} 可提供開發人員、IT 管理者及商業利害關係人，對其行動應用程式的效能及其使用情形的見解。請從桌面或平板電腦監視所有應用程式的效能及使用情形。可快速識別趨勢和異常、往下探查以解決這些問題，以及在重要度量值超過重大臨界值時觸發警示。
{: shortdesc}

若要快速啟動並執行 {{site.data.keyword.mobileanalytics_short}} 服務，請遵循下列步驟：

1. 為 {{site.data.keyword.mobileanalytics_short}} 服務建立實例<!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->之後，可以在「{{site.data.keyword.Bluemix}} 儀表板」的**服務**區段中按一下您的磚，以存取「{{site.data.keyword.mobileanalytics_short}} 主控台」。

 {{site.data.keyword.mobileanalytics_short}} 服務在啟動時已啟用**展示模式**。展示模式會在**應用程式資料**及**警示**頁面上移入圖表，讓您可以查看資料的顯示方式。當您有自己的資料時，即可關閉展示模式。處於展示模式時，{{site.data.keyword.mobileanalytics_short}} 主控台是唯讀的，因此您無法建立新的警示定義。

2. 安裝 {{site.data.keyword.mobileanalytics_short}} [Client SDK](/docs/services/mobileanalytics/install-client-sdk.html)。您可以選擇性地使用 {{site.data.keyword.mobileanalytics_short}} [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}。

3. 匯入 Client SDK，並使用下列程式碼 Snippet 起始設定它們，以記錄用量分析：

	#### Android
	{: #android-import}

	將下列 `import` 陳述式新增至專案檔開頭處：
	
    ```
import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
  ```
    {: codeblock}
  
 #### iOS
 {: #ios-import}
	
 **附註：**Swift SDK 適用於 iOS 及 watchOS。
	
 將下列 `import` 陳述式新增至 `AppDelegate.swift` 專案檔開頭處，以匯入 `BMSCore` 和 `BMSAnalytics` 架構：

   ```Swift
   import BMSCore
   import BMSAnalytics
   ```
   {: codeblock}  
   
 #### Cordova
 {: #cordova-import}
		
 從您的 Cordova 應用程式根目錄，執行下列指令以新增 Cordova 外掛程式：

 ```Javascript
 cordova plugin add bms-core
 ```
 {: codeblock}  

4. 使用 [API 金鑰](/docs/services/mobileanalytics/sdk.html#analytics-clientkey)值，以在應用程式碼內起始設定 {{site.data.keyword.mobileanalytics_short}} Client SDK，來記錄用量分析及應用程式階段作業。	
	
 #### Android
 {: #android-initialize}	

  ```
  BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // You can change the region
  Analytics.init(getApplication(), "your_app_name_here", "your_api_key_here", hasUserContext, Analytics.DeviceEvent.ALL);
  ```
  {: codeblock}
    
 **bluemixRegion** 參數指定您所使用的 {{site.data.keyword.Bluemix_notm}} 部署（例如，`BMSClient.REGION_US_SOUTH` 及 `BMSClient.REGION_UK`）。 
    <!-- , or `BMSClient.Region.Sydney`.-->

 #### iOS
 {: #ios-initialize}
  
  使用 [API 金鑰](/docs/services/mobileanalytics/sdk.html#analytics-clientkey)值，以在應用程式碼內起始設定 Client SDK，來記錄用量分析及應用程式階段作業。
	
  ```Swift
		BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // You can change the region
		Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: deviceEvents: .lifecycle, .network)
		```
  {: codeblock}
			
   **bluemixRegion** 參數指定您所使用的 Bluemix 部署（例如，`BMSClient.Region.usSouth` 或 `BMSClient.Region.unitedKingdom`）。
	<!-- , or `BMSClient.REGION_SYDNEY`. -->
	
 #### Cordova
 {: #cordova-initialize}
	
 使用 [API 金鑰](/docs/services/mobileanalytics/sdk.html#analytics-clientkey)值，以在應用程式碼內起始設定 Client SDK，來記錄用量分析及應用程式階段作業。
	
  ```
  var appName = "your_app_name_here";
  var apiKey = "your_api_key_here";
	
  BMSClient.initialize(BMSClient.REGION_US_SOUTH); // You can change the region
  BMSAnalytics.initialize(appName, apiKey, false, [BMSAnalytics.ALL])
  ```
  {: codeblock}
  
  **bluemixRegion** 參數指定您所使用的 {{site.data.keyword.Bluemix_notm}} 部署（例如，`BMSClient.REGION_US_SOUTH` 及 `BMSClient.REGION_UK`）。
  
 **附註：**您為應用程式所選取的名稱 (`your_app_name_here`) 會在 {{site.data.keyword.mobileanalytics_short}} 主控台中顯示為應用程式名稱。應用程式名稱是用來作為過濾器，以在儀表板中搜尋應用程式日誌。當您跨平台（例如，Android 及 iOS）使用相同的應用程式名稱時，不論是從哪個平台傳送日誌，都可以看到同名應用程式的所有日誌。

5. 將記錄的用量分析傳送至「Mobile Analytics 服務」。簡單的測試分析方式是在應用程式啟動時執行下列程式碼：

	#### Android
	{: #android-send}

	使用 `Analytics.send()` 方法，將分析資料傳送至伺服器。您可以將 `Analytics.send()` 方法放在 Android 應用程式中主要活動之 `onCreate` 方法的任意位置，或放在最適合您專案的位置。 
	
	您可以在任意位置插入 `Analytics.send()`。

	```
	Analytics.send();
	```
	{: codeblock}

	#### iOS
	{: #ios-send}

	使用 `Analytics.send` 方法，將分析資料傳送至伺服器。您可以將 `Analytics.send` 方法放在應用程式委派的 `application(_:didFinishLaunchingWithOptions:)` 方法的任意位置，或放在最適合您專案的位置。 

	```
	Analytics.send()
	```
	{: codeblock}
	
	#### Cordova
	{: #cordova-send}
	
	使用 `BMSAnalytics.send` 方法，將分析資料傳送至伺服器。將 `BMSAnalytics.send` 方法放在最適合您專案的位置中。
	
	```
	BMSAnalytics.send
	```
	{: codeblock}
	
	閱讀[檢測應用程式](/docs/services/mobileanalytics/sdk.html)主題，以瞭解其他 {{site.data.keyword.mobileanalytics_short}} 功能（例如[記載](/docs/services/mobileanalytics/sdk.html#app-monitoring-logger)、[網路要求](/docs/services/mobileanalytics/sdk.html#network-requests)及[損毀分析](/docs/services/mobileanalytics/sdk.html#report-crash-analytics)）。
	
6. 在模擬器或裝置上編譯並執行應用程式。

7. 移至「{{site.data.keyword.mobileanalytics_short}} 主控台」，以查看應用程式的用量分析。您也可以<!--[creating custom charts](app-monitoring.html#custom-charts),-->[設定警示](/docs/services/mobileanalytics/app-monitoring.html#alerts)及[監視應用程式損毀](/docs/services/mobileanalytics/app-monitoring.html#monitor-app-crash)來監視應用程式。


# 相關鏈結

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [Cordova 外掛程式核心 SDK](https://www.npmjs.com/package/bms-core){: new_window}

## API 參考資料
{: #api}
* [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
