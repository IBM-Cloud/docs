---

copyright:
  years: 2015, 2016

---

# 檢測應用程式以使用 {{site.data.keyword.mobileanalytics_short}} Client SDK
{: #mobileanalytics_sdk}
*前次更新：2016 年 4 月 27 日*
{: .last-updated}

{{site.data.keyword.mobileanalytics_full}} SDK 可讓您檢測行動應用程式。
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}} 可讓您收集三種種類的資料，而且各需要不同程度的檢測：

1.  預先定義的資料 - 此種類包括適用於所有應用程式的一般用法及裝置資訊。在此種類內，是指出應用程式使用數量、頻率或持續時間的裝置 meta 資料（作業系統及裝置模型）及用法資料（作用中使用者及應用程式階段作業）。在應用程式中起始設定 {{site.data.keyword.mobileanalytics_short}} SDK 之後，會自動收集預先定義的資料。
2. 自訂事件 - 此種類包括您自行定義及應用程式特有的資料。這個資料代表您應用程式內發生的事件，例如頁面檢視、按鈕點選或應用程式內採購。除了在應用程式中起始設定 {{site.data.keyword.mobileanalytics_short}} SDK 之外，您還必須為您要追蹤的每一個自訂事件新增一行程式碼。
3. 用戶端日誌訊息 - 此種類可讓開發人員在應用程式內新增程式碼行，以記載自訂訊息來協助開發和除錯。開發人員會將嚴重性/詳細層次指派給每一個日誌訊息，而且後續可以依指派的層次過濾訊息，或透過配置應用程式忽略低於給定記載層次的訊息來保留儲存空間。若要收集用戶端日誌資料，您必須在應用程式內起始設定 {{site.data.keyword.mobileanalytics_short}} SDK，以及為每一個日誌訊息新增一行程式碼。

SDK 目前適用於 Android、iOS 及 WatchOS。

## 識別用戶端金鑰值
{: #analytics-clientkey}

識別設定 Client SDK 之前的**用戶端金鑰**值。需要有「用戶端金鑰」，才能起始設定 Client SDK。
1. 開啟 {{site.data.keyword.mobileanalytics_short}} 服務儀表板。
2. 按一下扳手圖示來開啟「API 金鑰」標籤。
3. 在「API 金鑰」標籤中，記下「用戶端金鑰」值。


## 起始設定 Android 應用程式來收集分析
{: #initalize-ma-sdk-android}

起始設定應用程式，以啟用將日誌傳送至 {{site.data.keyword.mobileanalytics_short}} 服務。

1. 將下列 `import` 陳述式新增至專案檔頂端，以匯入 Client SDK：

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
  ```
  {: codeblock}

2. 在 Android 應用程式中主要活動的 `onCreate` 方法中或最適合您專案的位置中新增起始設定碼，以在 Android 應用程式中起始設定 {{site.data.keyword.mobileanalytics_short}} Client SDK。

	```Java
	try {
            BMSClient.getInstance().initialize(this.getApplicationContext(), "", "", BMSClient.REGION_US_SOUTH); // Make sure that you point to your region
        } catch (MalformedURLException e) {
            Log.e(your_app_name,"URL should not be malformed:  " + e.getLocalizedMessage());
        }
  ```
  {: codeblock}

  若要使用 {{site.data.keyword.mobileanalytics_short}} Client SDK，您必須起始設定 `BMSClient` 與 **bluemixRegion** 參數。在起始設定程式中，**bluemixRegion** 值指定您所使用的 {{site.data.keyword.Bluemix_notm}} 部署（例如，`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK` 或 `BMSClient.REGION_SYDNEY`）。
  <!-- Set this value with a `BMSClient.REGION` static property. -->

  <!--You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. 起始設定 Analytics，方法是使用 Android 應用程式物件，並將您的應用程式名稱提供給它。您也需要[**用戶端金鑰**](#analytics-clientkey)值。
	
	```Java
	Analytics.init(getApplication(), "my_app", apiKey, Analytics.DeviceEvent.LIFECYCLE);
	// In this code example, Analytics is configured to record lifecycle events.
	```
  {: codeblock}

	**提示：**應用程式名稱是用來作為過濾器，以在儀表板中搜尋用戶端日誌。當您跨平台（例如，Android 及 iOS）使用相同的應用程式名稱時，不論是從哪個平台傳送日誌，都可以看到同名應用程式的所有日誌。

## 起始設定 iOS 應用程式來收集分析
{: #init-ma-sdk-ios}

起始設定應用程式，以啟用將日誌傳送至 {{site.data.keyword.mobileanalytics_short}} 服務。Swift SDK 適用於 iOS 及 watchOS。

1. 將下列 `import` 陳述式新增至 `AppDelegate.swift` 專案檔頂端，以匯入 `BMSCore` 及 `BMSAnalytics` 架構：

  ```Swift
  import BMSCore
  import BMSAnalytics
  ```
  {: screen}

2. 若要使用 {{site.data.keyword.mobileanalytics_short}} Client SDK，您必須先使用下列程式碼來起始設定 `BMSClient` 類別。

  將起始設定碼放在應用程式委派的 `application(_:didFinishLaunchingWithOptions:)` 方法中或最適合您專案的位置中。

    ```Swift
    BMSClient.sharedInstance.initializeWithBluemixAppRoute(nil, bluemixAppGUID: nil, bluemixRegion: BMSClient.REGION_US_SOUTH)
```
    {: codeblock}

    若要使用 {{site.data.keyword.mobileanalytics_short}} Client SDK，您必須起始設定 `BMSClient` 與 **bluemixRegion** 參數。在起始設定程式中，**bluemixRegion** 值指定您所使用的 {{site.data.keyword.Bluemix_notm}} 部署（例如，`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK` 或 `BMSClient.REGION_SYDNEY`）。
   
   <!-- Set this value with a `BMSClient.REGION` static property. -->

   <!-- You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. 起始設定 Analytics，方法是將行動應用程式的名稱提供給它。您也需要[**用戶端金鑰**](#analytics-clientkey)值。

  應用程式名稱是用來作為過濾器，以在「{{site.data.keyword.mobileanalytics_short}} 儀表板」中搜尋用戶端日誌。跨平台（例如，Android 及 iOS）使用相同的應用程式名稱，不論是從哪個平台傳送日誌，都可以看到同名應用程式的所有日誌。

  選用 `deviceEvents` 參數會自動收集裝置層次事件的分析。

  ### iOS
    {: #ios-initialize-analytics}

      ```
      Analytics.initializeWithAppName("AppName", apiKey: your_client_key,
      deviceEvents: DeviceEvent.LIFECYCLE)
```

  ### watchOS
  {: #watchos-initialize-analytics}

	```
	  Analytics.initializeWithAppName("AppName", apiKey: your_api_key)
	```

  您可以使用 `Analytics.recordApplicationDidBecomeActive()` 及 `Analytics.recordApplicationWillResignActive()` 方法，來記錄 WatchOS 上的裝置事件。
  
  將下列這一行新增至 ExtensionDelegate 類別的 `applicationDidBecomeActive()` 方法。

	```
	Analytics.recordApplicationDidBecomeActive()
	```
  {: codeblock}

  將下列這一行新增至 ExtensionDelegate 類別的 applicationWillResignActive() 方法：
	```
	Analytics.recordApplicationWillResignActive()
```
  {: codeblock}

## 收集用法分析
{: #app-monitoring-gathering-analytics}

  您可以配置 {{site.data.keyword.mobileanalytics_short}} Client SDK 來記錄用法分析，並且將記錄的資料傳送至 {{site.data.keyword.mobileanalytics_short}} 服務。

  使用下列 API 開始記錄及傳送用法分析：

#### Android
{: #android-usage-api}
	
```
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.disable();// Enable recording of usage analytics
Analytics.enable();Analytics.log(eventJSONObject);// Send recorded usage analytics to the Mobile Analytics Service
Analytics.send();
```
	
用於記載事件的用法分析範例：
	
```
// Log a custom analytics event for custom charts, which is represented by a JSON object:
JSONObject eventJSONObject = new JSONObject();eventJSONObject.put("customProperty" , "propertyValue");
```

#### iOS - Swift
{: #ios-usage-api}

```
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.enabled = false// Enable recording of usage analytics
Analytics.enabled = true// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service
Analytics.send()
```

用於記載事件的用法分析範例：

```
// Log a custom analytics event for custom charts
let eventObject = ["customProperty": "propertyValue"]
Analytics.log(eventObject)
```

  <!--Removing Cordova for experimental-->
  <!--### Cordova-->
  <!--{: #usage-analytics-cordova}-->

  <!--```JavaScript-->
  <!--// Enable usage analytics recording-->
  <!--Analytics.enable();-->

  <!--// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service-->
  <!--Analytics.send();-->
  <!--```-->
  <!--**Note:** When you are developing Cordova applications, use the native API to enable application lifecycle event recording.-->

## 啟用、配置及使用日誌程式
{: #app-monitoring-logger}

  {{site.data.keyword.mobileanalytics_full}} Client SDK 提供的記載架構類似於您可能熟悉的其他記載架構，例如 `java.util.logging` 或 `log4j`。記載架構支援多個每一套件日誌程式實例、不同的記載層次、應用程式損毀的堆疊追蹤擷取等。

  您也可以配置將記載的資料儲存至應用程式執行所在的裝置，並且於稍後將這些裝置日誌傳送至「{{site.data.keyword.mobileanalytics_short}} 服務」。

  <!-- Initialization has to happen first to be able to collect logs and send them to the {{site.data.keyword.mobileanalytics_short}} service. -->

  {{site.data.keyword.mobileanalytics_short}} Client SDK 記載架構支援下列具有建議使用準則的記載層次（依最不詳細到最詳細程度列出）：

  * `FATAL` - 用於無法復原的損毀或停滯。`FATAL` 層次是保留用於記載無法復原的錯誤，這對使用者而言就像應用程式損毀
  * `ERROR` - 用於非預期的異常狀況或非預期的網路通訊協定錯誤
  * `WARN` - 用來記載非視為嚴重錯誤的用法警告（例如使用已淘汰的 API 或慢速網路回應）
  * `INFO` - 用於報告起始設定事件以及可能重要但不緊急的其他資料
  * `DEBUG` - 用於報告除錯陳述式，以協助開發人員解決應用程式問題報告

    #### 記載層次情境
    {: #log-level-scenario}

    日誌程式層次配置成 `FATAL` 時，日誌程式會擷取未捕捉的異常狀況，但不會擷取任何導致損毀事件的日誌。您可以設定更詳細的日誌程式層次，確保也一併擷取可能會導致 `FATAL` 日誌程式項目（例如 `WARN` 及 `ERROR`）的日誌。

  <!--**Note:** Find full Logger API references for each platform at [SDKs, samples, API reference](sdks-samples-apis.html). The Logger API is part of the--> <!--{{site.data.keyword.mobileanalytics_short}} Client SDK Core.-->

  <!--### Cordova-->


  <!--```JavaScript-->

  <!--var logger = MFPLogger.getInstance("myLogger");-->

  <!--logger.debug("debug info");-->
  <!--logger.info("info message");-->
  <!--logger.warn("warning message");-->
  <!--logger.fatal("fatal message");-->

  <!--```-->


### 日誌程式用法範例
{: #sample-logger-usage}

**附註：**請先確定已檢測過應用程式使用 [{{site.data.keyword.mobileanalytics_short}} Client SDK](sdk.html)，然後再使用記載架構。
 
  下列程式碼 Snippet 顯示「日誌程式」用法範例：

#### Android
{: #android-logger-sample}

```
// Configure Logger to save logs to the device so that they 
// can later be sent to the {{site.data.keyword.mobileanalytics_short}} service
// Disabled by default; set to true to enable
Logger.storeLogs(true);// Change the minimum log level (optional)
// The default setting is Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);// Send logs to the {{site.data.keyword.mobileanalytics_short}} Service
Logger.send();
```

日誌程式情境：

```
// Create two logger instances
// You can create multiple log instances to organize your logs
Logger logger1 = Logger.getLogger("logger1");
Logger logger2 = Logger.getLogger("logger2");// Log messages with different levels
// Debug message for feature 1
// Info message for feature 2
logger1.debug("debug message"); 
//the logger1.debug message is not logged because the logLevelFilter is set to Info
logger2.info("info message");
```

#### iOS - Swift
{: ios-logger-sample}

```
// Configure Logger to save logs to the device so that they can later be sent to the {{site.data.keyword.mobileanalytics_short}} service
// Disabled by default; set to true to enable
Logger.logStoreEnabled = true// Change the minimum log level (optional)
// The default setting is LogLevel.Debug
Logger.logLevelFilter = LogLevel.Info// Send logs to the {{site.data.keyword.mobileanalytics_short}} Service
Logger.send()
```

日誌程式情境：
    
```
// Create two logger instances
// You can create multiple log instances to organize your logs
let logger1 = Logger.logger(forName: "feature1Logger")
let logger2 = Logger.logger(forName: "feature2Logger")// Log messages with different levels
logger1.debug("debug message for feature 1") 
//the logger1.debug message is not logged because the logLevelFilter is set to Info
logger2.info("info message for feature 2")
```

**提示**：基於隱私權考量，您可以針對使用發行模式建置的應用程式停用「日誌程式」輸出。「日誌程式」類別預設會將日誌列印至 Xcode 主控台。在您目標的建置設定中，將 `-D RELEASE_BUILD` 旗標新增至發行建置配置的**其他 Swift 旗標**區段。
    

  <!-- ### Cordova-->
  <!--{: #enable-logger-sample-cordova}-->

  <!--// Enable persisting logs-->
  <!--MFPLogger.setCapture(true);-->

  <!--// Set the minimum log level to be printed and persisted-->
  <!--MFPLogger.setLevel(MFPLogger.INFO);-->

  <!--var logger1 = MFPLogger.getInstance("logger1");-->
  <!--var logger2 = MFPLogger.getInstance("logger2");   -->

  <!--// Log messages with different levels-->
  <!--logger1.debug ("debug message");-->
  <!--logger2.info ("info message");-->

  <!--// Send persisted logs to the {{site.data.keyword.mobileanalytics_short}} Service-->
  <!--```-->

<!--## Enabling the {{site.data.keyword.mobileanalytics_short}} Client SDK internal logs
{: #enable-logger-sdklogs}

  The {{site.data.keyword.mobileanalytics_short}} Client SDK provides a better development experience by not unnecessarily increasing the console output with its internal debug messages. Therefore, by default, internal log messages that are produced by the {{site.data.keyword.mobileanalytics_short}} SDK with the DEBUG level are not printed. You can enable printing of all internal log messages of the {{site.data.keyword.mobileanalytics_short}} Client SDK with the following API:

#### Android
{: #enable-logger-print-android}

```
Logger.setSDKDebugLoggingEnabled(true);
```

#### iOS - Swift
{: #enable-logger-print-swift}

```
Logger.sdkDebugLoggingEnabled = true
```
-->

## 追蹤作用中使用者
{: #trackingusers}
您可以選擇性地追蹤有多少位使用者正在活躍地使用您的應用程式，方法是將作用中使用者的使用者名稱傳遞至 {{site.data.keyword.mobileanalytics_short}}。

#### Android
{: #android-tracking-users}

對使用者登入時新增下列程式碼：

```
Analytics.setUserIdentity("username");
```

對使用者登出時新增下列程式碼：

```
Analytics.clearUserIdentity();
```

#### iOS - Swift
{: #ios-tracking-users}

對使用者登入時新增下列程式碼：

```
Analytics.userIdentity = "username"
```

對使用者登出時新增下列程式碼：

```
Analytics.userIdentity = nil
```

<!--## Configuring MobileFirst Platform Foundation servers to use the {{site.data.keyword.mobileanalytics_short}} service (optional)
{: #configmfp}
  If you are using MobileFirst Platform Foundation Server V7 and higher, you can configure it to use the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} service to store analytics and logged data. 
  
  Configure MobileFirst Platform V7.0, V7.1, and V8.0 Beta servers to send analytics data to the {{site.data.keyword.mobileanalytics_short}} service on {{site.data.keyword.Bluemix_notm}}.

  1. Visit the dashboard for the {{site.data.keyword.mobileanalytics_short}} service where you want to send analytics data and note the browser URL for the dashboard.
  2. Determine the value for reporting analytics, as follows:
  	1. Get the {{site.data.keyword.mobileanalytics_short}} service route from the dashboard URL. The {{site.data.keyword.mobileanalytics_short}} service route is the part of the URL before `/analytics/console/dashboard`.  

  		For example, if the dashboard URL is: `http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde`
      {: screen}

  		then the Analytics Service Route is
      `http://mobile-analytics-dashboard.ng.bluemix.net`
      {: screen}

  	2. Get the [Client API Key](#analytics-clientkey) value from the Analytics dashboard.

  	You will use the {{site.data.keyword.mobileanalytics_short}} service route and API Key to construct a URL to report analytics data, depending on the version of your MobileFirst Platform server. -->

<!--  3. Copy the URL for your {{site.data.keyword.mobileanalytics_short}} service dashboard. Include the `instanceId` query parameter, for example:
      `http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=1212345abcde`
      {: screen}

  4. Configure the values for the MobileFirst Platform server JNDI properties, as follows:-->

<!--    ### MobileFirst Platform V7.0
    {: #mfp70}

        The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/data?tenant=<Client API Key>`
        {: screen}

        The `wl.analytics.console.url` JNDI property is the Analytics service dashboard URL.

        #### Example of MobileFirst Platform V7.0 JNDI property values
        {: #example-mfp70-jndi-values}

        For a MobileFirst Platform project named `Myproj7000`, based on the examples in steps 2 and 3, replace the current JNDI property values in the `server.xml` file with:
        ```
        <jndiEntry jndiName="MyProj7000/wl.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data?tenant=12345abcde"'/>
        ```
        {: screen}
        ```
        <jndiEntry jndiName="MyProj7000/wl.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
        ```
        {: screen}

    ### MobileFirst Platform V7.1
    {: #mfp71}

      The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`
      {: screen}

      #### Example of MobileFirst Platform JNDI V7.1 property values
      {: #example-mfp71-jndi-values}

      For a MobileFirst Platform project named `MyProj7101`, replace the current JNDI property values in the `server.xml` file with:
      ```
      <jndiEntry jndiName="MyProj7101/wl.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/v2/data?tenant=12345abcde"'/>
      ```
      {: screen}
      ```
      <jndiEntry jndiName="MyProj7101/wl.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
      ```
      {: screen}

      ### MobileFirst Platform V8.0
      {: #mfp80}

      The format of the `mfp.analytics.url` JNDI property is:
      `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`  

    #### Example MobileFirst Platform V8.0 Beta JNDI property values
      {: example-mfp80b-jndi-values}

      For a MobileFirst Platform project named `mfp`, which is the default, replace the current JNDI property values in the `server.xml` file with:
      ```
      <jndiEntry jndiName="mfp/mfp.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data?tenant=12345abcde"'/>
      ```
      {: screen}
      ```
      <jndiEntry jndiName="mfp/mfp.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
      ```
      {: screen}
-->
<!-- #### Ignored events and event retention
{: #ignored-events}
The {{site.data.keyword.mobileanalytics_short}} service saves the following data for ignored events and event retention:
  
<dl>	
<dt>Ignored events</dt>
	<dd>`ANALYTICS_SDK_CFG_IGNORE_AppPushAction: true`
		  `ANALYTICS_SDK_CFG_IGNORE_ServerLog: true`
		  `ANALYTICS_SDK_CFG_IGNORE_NetworkTransaction: true`
		  `ANALYTICS_SDK_CFG_IGNORE_NetworkTransactionSummarizedHourly: true`
		  `ANALYTICS_SDK_CFG_IGNORE_PushNotification: true`
		  `ANALYTICS_SDK_CFG_IGNORE_PushSubscription: true`</dd>
</dt>
<dt>Event retention</dd>
<dd>
`ANALYTICS_TTL_AlertNotification: 14d`<br>
`ANALYTICS_TTL_CustomData: 7d`<br>
`ANALYTICS_TTL_Device: 90d`<br>
`ANALYTICS_TTL_AppLog: 3d`<br>
`ANALYTICS_TTL_AppSession: 7d`
</dd>
</dt>
</dl>
  
-->

# 相關鏈結

## API 參考資料
{: #api}
* [REST API](https://mobile-analytics-dashboard.eu-gb.bluemix.net/analytics-service/){:new_window}
