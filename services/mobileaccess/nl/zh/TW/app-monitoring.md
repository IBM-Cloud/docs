---

copyright:
  years: 2015, 2016
  
---

# 監視應用程式
{: #app-monitoring}
前次更新：2016 年 9 月 22 日
{: .last-updated}

除了安全特性之外，{{site.data.keyword.amafull}} 還會提供行動應用程式的監視及分析。您可以使用 {{site.data.keyword.amashort}} 用戶端 SDK 來記錄用戶端日誌以及監視資料。開發人員可以控制何時將此資料傳送給「{{site.data.keyword.amashort}} 服務」。將自動記載「{{site.data.keyword.amashort}} 服務」中所發生的所有安全事件（例如鑑別成功或失敗）。
<!--
**Note**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

將資料遞送至 {{site.data.keyword.amashort}} 時，您可以使用 {{site.data.keyword.amashort}} 監視儀表板來取得行動應用程式、裝置及用戶端日誌的分析洞察。預設會記錄您的應用程式對 {{site.data.keyword.amashort}} 所保護資源提出之要求的相關資訊。

自動記錄的資料包括鑑別次數、新裝置數目和新使用者數目這類的資訊。此外，您還可以配置 {{site.data.keyword.amashort}} 用戶端 SDK 來報告下列資訊：

### 行動應用程式的用量統計資料
{: #usage-stats}

您可以配置行動應用程式，使用一些簡單的 API 呼叫來記錄應用程式生命週期事件，並將記錄的資料傳送給 {{site.data.keyword.amashort}} 服務。您可以記錄應用程式開啟次數、收到的推送通知數等等。

### 用戶端日誌擷取
{: #client-side-logcapture}

現場運作中的應用程式有時會遇到問題，需要開發人員注意並進行修正。通常很難重新產生這些問題。從事程式碼開發的開發人員可能缺乏用於測試的環境或確切裝置。在這些狀況下，能夠在環境中發生問題時從用戶端裝置中擷取除錯日誌就會非常有用。

### 保留擷取的資料
{: #preserve-captureddata}

沒有任何方式可保證所有擷取的資料都保留在用戶端上。您的使用者可能離線執行行動應用程式，並且同步累計擷取的分析和日誌資料。因為用戶端處於離線狀態且檔案系統空間有限，所以必須清除較舊的記載事件，以騰出空間來保留更新的記載事件。開發人員可以決定何時使用提供的 API 將擷取的資料傳送給「{{site.data.keyword.amashort}} 服務」。

## 使用 {{site.data.keyword.amashort}} 監視儀表板
{: #monitoring-dashboard}

1. 開啟 {{site.data.keyword.Bluemix}} 儀表板，然後按一下 {{site.data.keyword.Bluemix_notm}} 應用程式。

2. 開啟 {{site.data.keyword.Bluemix_notm}} 應用程式儀表板時，按一下 {{site.data.keyword.amashort}} 磚。

3. 按一下 {{site.data.keyword.amashort}}「儀表板」導覽中的**監視**按鈕。


## 啟用、配置及使用日誌程式
{: #enable-logger}

{{site.data.keyword.amashort}} 用戶端 SDK 所提供的記載架構與您可能熟悉的其他日誌架構（例如 `java.util.logging` 或 `log4j`）類似。記載架構支援多個個別套件日誌程式實例、不同的記載層次、擷取應用程式當機的堆疊追蹤資料等。

您還可以將記載的資料配置為持續保存至本端儲存庫，然後可以根據需求將其傳送給 {{site.data.keyword.amashort}} 服務。

{{site.data.keyword.amashort}} 用戶端 SDK 記載架構支援下列記載層次（按詳細程度從低到高列出），建議的使用準則如下：

* `FATAL` - 用於無法復原的當機或停滯。FATAL 層次保留用於記載無法復原的錯誤，這些錯誤對於使用者會顯示為應用程式當機。
* `ERROR` - 用於非預期的異常狀況或非預期的網路通訊協定錯誤。
* `WARN` - 記載未視為嚴重錯誤的使用警告（例如使用已淘汰的 API 或網路回應緩慢）。
* `INFO` - 用於報告起始設定事件以及其他可能有用的資料。
* `DEBUG` - 用於報告除錯陳述，以協助開發人員解決應用程式問題報告。

#### 記載層次情境
{: #log-level-scenario}

日誌程式層次配置為 `FATAL` 時，日誌程式會擷取未捕捉的異常狀況，但不會擷取任何導致當機事件的日誌。您可以設定更詳細的日誌程式層次，確保也會擷取可能導致 `FATAL` 日誌程式項目的日誌（例如 `WARN` 及 `ERROR`）。

請確定您已起始設定 {{site.data.keyword.amashort}} 用戶端 SDK，然後才使用記載架構。下列範例示範 {{site.data.keyword.amashort}} 用戶端 SDK 記載架構的基本用法。

<!-- **Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available.-->

#### Android
{: #enable-logger-android}

```Java
BMSClient.getInstance().initialize(this.getApplicationContext(), BMSClient.REGION_US_SOUTH); // Make sure that you point to your region

Logger logger = Logger.getLogger("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```
{: codeblock}

**bluemixRegion** 參數指定所使用的 Bluemix 部署（例如，`BMSClient.REGION_US_SOUTH` 及 `BMSClient.REGION_UK`）。 

#### iOS - Swift
{: #enable-logger-swift}

```Swift
BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.REGION_US_SOUTH) // You can change the region
Analytics.initializeWithAppName(your_app_name_here, apiKey: your_api_key_here, hasUserContext: false, deviceEvents: DeviceEvent.LIFECYCLE)

let logger = Logger.logger(forName: "myLogger")

logger.debug(“debug info")
logger.info(“info message")
logger.warn(“warning message")
logger.error(“error message")
logger.fatal(“fatal message")
```
{: codeblock}
<!--
**Note:** The {{site.data.keyword.amashort}} client SDK is implemented with Objective-C, therefore you might need to add the `IMFLoggerExtension.swift` file to your Swift project to use the previous logger API. You can find this file in the [{{site.data.keyword.amashort}} client SDK archive](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).
-->

#### Cordova
{: #enable-logger-android-cordova}

```JavaScript
BMSClient.initialize(BMSClient.REGION_US_SOUTH); // You can change the region

var logger = BMSLogger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```
{: codeblock}

您可以在 Logger 類別中找到下列其他方法：

* `setCapture` - 啟用或停用稍後要傳送給 {{site.data.keyword.amashort}} 服務之日誌資訊的持續保存。
* `setLevel` - 設定儲存日誌訊息的最低記載層次。
* `send` - 將持續保存的日誌傳送給 {{site.data.keyword.amashort}} 服務。

例如，當擷取為開啟狀態，並將日誌程式層次配置為 FATAL 時，日誌程式會擷取未捕捉的異常狀況。未捕捉的異常狀況通常對於使用者會顯示為應用程式當機，但並不會擷取任何導致當機事件的日誌。或者，更詳細的日誌程式層次可確保也會擷取導致 FATAL 日誌程式項目的日誌，例如 WARN 及 ERROR。

**附註：**在 [SDK、範例、API 參考資料](sdks-samples-apis.html)中，尋找每一個平台的完整「日誌程式 API」參考資料。「日誌程式 API」是「{{site.data.keyword.amashort}} 用戶端 SDK 核心」的一部分。


### 範例日誌程式用法
{: #sample-logger-usage}

下列程式碼 Snippet 顯示範例「日誌程式」用法：

#### Android
{: #enable-logger-sample-android}

```Java
// Configure Logger to save logs to the device so that they 
// can later be sent to the {{site.data.keyword.amashort}} service
// Disabled by default; set to true to enable
Logger.storeLogs(true);

// Change the minimum log level (optional)
// The default setting is Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);

// Create two logger instances
// You can create multiple log instances to organize your logs
Logger logger1 = Logger.getLogger("logger1");
Logger logger2 = Logger.getLogger("logger2");

// Log messages with different levels
// Debug message for feature 1
// Info message for feature 2
logger1.debug("debug message"); 
//the logger1.debug message is not logged because the logLevelFilter is set to Info
logger2.info("info message");

// Send logs to the {{site.data.keyword.amashort}} service
Logger.send();
```
{: codeblock}

#### iOS - Swift
{: #enable-logger-sample-swift}

```Swift
// Configure Logger to save logs to the device so that they can later be sent to the {{site.data.keyword.amashort}} service
// Disabled by default; set to true to enable
Logger.logStoreEnabled = true

// Change the minimum log level (optional)
// The default setting is LogLevel.Debug
Logger.logLevelFilter = LogLevel.Info

// Create two logger instances
// You can create multiple log instances to organize your logs
let logger1 = Logger.logger(forName: "feature1Logger")
let logger2 = Logger.logger(forName: "feature2Logger")

// Log messages with different levels
logger1.debug("debug message for feature 1") 
//the logger1.debug message is not logged because the logLevelFilter is set to Info
logger2.info("info message for feature 2")

// Send logs to the {{site.data.keyword.amashort}} service
Logger.send()
```
{: codeblock}

#### Cordova
{: #enable-logger-sample-cordova}

```JavaScript
// Enable persisting logs
BMSLogger.setCapture(true);

// Set the minimum log level to be printed and persisted
BMSLogger.setLevel(BMSLogger.INFO);

// Create two logger instances
var logger1 = BMSLogger.getInstance("logger1");
var logger2 = BMSLogger.getInstance("logger2");    

// Log messages with different levels
logger1.debug ("debug message");
logger2.info ("info message");

// Send persisted logs to the {{site.data.keyword.amashort}} service
BMSLogger.send(success, failure);
```
{: codeblock}

### 啟用 {{site.data.keyword.amashort}} 用戶端 SDK 內部日誌
{: #enable-logger-sdklogs}
目前只有 Android 版的 {{site.data.keyword.amashort}} 用戶端 SDK 才提供此特性。

{{site.data.keyword.amashort}} 用戶端 SDK 可提供較佳的開發體驗，原因是不會不必要地因為內部除錯訊息而增加 Logcat 輸出。因此，預設不會列印由 {{site.data.keyword.amashort}} SDK 所產生且層次為 DEBUG 的內部日誌訊息。您可以使用下列 API，來啟用 {{site.data.keyword.amashort}} 用戶端 SDK 之所有內部日誌訊息的列印：


```
Logger.setSDKInternalLoggingEnabled(true);
```
{: codeblock}

## 收集用量分析
{: #usage-analytics}

您可以配置 {{site.data.keyword.amashort}} 用戶端 SDK 來記錄用量分析，以及將記錄的資料傳送給 {{site.data.keyword.amashort}} 服務。
<!--
**Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

**附註：**請確定您已啟用記載擷取，再開始記錄用量分析。

使用下列 API 來開始記錄及傳送用量分析：

#### Android
{: #usage-analytics-android}

```Java
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.disable();
	
// Enable recording of usage analytics
Analytics.enable();
	
Analytics.log(eventJSONObject);
	
// Send recorded usage analytics to the Mobile Analytics Service
Analytics.send();
```
{: codeblock}

#### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.enabled = false

// Enable recording of usage analytics
Analytics.enabled = true

// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service
Analytics.send()
```
{: codeblock}

#### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Enable usage analytics recording
BMSAnalytics.enable();

// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
BMSAnalytics.send();
```
{: codeblock}

**附註：**當您開發 Cordova 應用程式時，請使用原生 API 來啟用應用程式生命週期事件記錄。
