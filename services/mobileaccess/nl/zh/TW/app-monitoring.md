---

copyright:
  years: 2015, 2016
  
---

# 監視應用程式
{: #app-monitoring}
前次更新：2016 年 6 月 28 日
{: .last-updated}

除了安全特性之外，{{site.data.keyword.amafull}} 還會提供行動應用程式的監視及分析。您可以使用 {{site.data.keyword.amashort}} 用戶端 SDK 來記錄用戶端日誌以及監視資料。開發人員可以控制何時將此資料傳送給「{{site.data.keyword.amashort}} 服務」。將自動記載「{{site.data.keyword.amashort}} 服務」中所發生的所有安全事件（例如鑑別成功或失敗）。

**附註**：{{site.data.keyword.amashort}} 服務的監視功能，預計會移轉至新的 [{{site.data.keyword.mobileanalytics_short}} 服務](https://console.ng.bluemix.net/catalog/services/mobile-analytics)。新的 Swift SDK 會利用新的 {{site.data.keyword.mobileanalytics_short}} 服務，此服務提供更豐富的分析體驗。{{site.data.keyword.mobileanalytics_short}} 服務目前處於實驗階段，預計在今年稍晚正式上市。由於預計會在 {{site.data.keyword.mobileanalytics_short}} 正式上市時停止使用 {{site.data.keyword.amashort}} 服務的監視功能，因此建議您先研究移轉應用程式以使用新的 {{site.data.keyword.mobileanalytics_short}} 服務及 Swift SDK。

將資料遞送至 {{site.data.keyword.amashort}} 時，您可以使用 {{site.data.keyword.amashort}} 監視儀表板來取得行動應用程式、裝置及用戶端日誌的分析洞察。預設會記錄您的應用程式對 {{site.data.keyword.amashort}} 所保護資源提出之要求的相關資訊。

自動記錄的資料包括鑑別次數、新裝置數目和新使用者數目這類的資訊。此外，您還可以配置 {{site.data.keyword.amashort}} 用戶端 SDK 來報告下列資訊：

### 行動應用程式的用量統計資料
{: #usage-stats}

您可以配置行動應用程式，使用一些簡單的 API 呼叫來記錄應用程式生命週期事件，並將記錄的資料傳送給 {{site.data.keyword.amashort}} 服務。您可以記錄應用程式開啟次數、收到的推送通知數等等。

### 用戶端日誌擷取
{: #client-side-logcapture}

現場運作中的應用程式有時會遇到問題，需要開發人員注意並進行修正。通常很難重新產生這些問題。<!--in R&D.--> 從事程式碼開發的開發人員可能缺乏用於測試的環境或確切裝置。在這些狀況下，能夠在環境中發生問題時從用戶端裝置中擷取除錯日誌就會非常有用。

### 保留擷取的資料
{: #preserve-captureddata}

沒有任何方式可保證所有擷取的資料都保留在用戶端上。您的使用者可能離線執行行動應用程式，並且同步累計擷取的分析和日誌資料。因為用戶端處於離線狀態且檔案系統空間有限，所以必須清除較舊的記載事件，以騰出空間來保留更新的記載事件。開發人員可以決定何時使用提供的 API 將擷取的資料傳送給「{{site.data.keyword.amashort}} 服務」。

## 使用 {{site.data.keyword.amashort}} 監視儀表板
{: #monitoring-dashboard}

1. 開啟 {{site.data.keyword.Bluemix}} 儀表板，然後按一下 {{site.data.keyword.Bluemix_notm}} 應用程式。

2. 開啟 {{site.data.keyword.Bluemix_notm}} 應用程式儀表板時，按一下 {{site.data.keyword.amashort}} 磚。

3. 按一下「{{site.data.keyword.amashort}} 儀表板」左側導覽列中的**監視**鏈結。


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

請確定您已起始設定 {{site.data.keyword.amashort}} 用戶端 SDK，然後才使用記載架構。下列範例示範 {{site.data.keyword.amashort}} 用戶端 SDK 記載架構的基本用法。

**重要事項**：{{site.data.keyword.amashort}} 服務的監視功能，預計會移轉至新的 [{{site.data.keyword.mobileanalytics_short}} 服務](https://console.ng.bluemix.net/catalog/services/mobile-analytics)。新的 Swift SDK 會利用新的 {{site.data.keyword.mobileanalytics_short}} 服務，此服務提供更豐富的分析體驗。{{site.data.keyword.mobileanalytics_short}} 服務目前處於實驗階段，預計在今年稍晚正式上市。由於預計會在 {{site.data.keyword.mobileanalytics_short}} 正式上市時停止使用 {{site.data.keyword.amashort}} 服務的監視功能，因此建議您先研究移轉應用程式以使用新的 {{site.data.keyword.mobileanalytics_short}} 服務及 Swift SDK。

#### Android
{: #enable-logger-android}

```Java
BMSClient.getInstance().initialize(context, appRoute, appGUID);

Logger logger = Logger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```

#### iOS - Objective-C
{: #enable-logger-objectc}

**重要事項**：雖然仍然完全支援 Objective-C SDK 且將它視為 {{site.data.keyword.Bluemix}} Mobile Services 的主要 SDK，不過預計在今年稍晚停止使用，改用新的 Swift SDK。

Objective-C SDK 會向 {{site.data.keyword.amashort}} 服務的「監視主控台」報告監視資料。如果您依賴 {{site.data.keyword.amashort}} 服務的監視功能，請繼續使用 Objective-C SDK。

```Objective-C
[[IMFClient sharedInstance] initializeWithBackendRoute:appRoute backendGUID:appGUID];

IMFLogger *logger = [IMFLogger loggerForName:@"myLogger"];

[logger logDebugWithMessages:@"debug"];
[logger logInfoWithMessages:@"info"];
[logger logWarnWithMessages:@"warn"];
[logger logErrorWithMessages:@"error"];
[logger logFatalWithMessages:@"fatal"];

```

#### iOS - Swift
{: #enable-logger-swift}

```Swift
IMFClient.sharedInstance().initializeWithBackendRoute(appRoute, backendGUID: appGuid)

let logger = IMFLogger(forName: "myLogger");

logger.logDebugWithMessages("debug");
logger.logInfoWithMessages("info");
logger.logWarnWithMessages("warn");
logger.logErrorWithMessages("error");
logger.logFatalWithMessages("fatal");
```

**附註：**{{site.data.keyword.amashort}} 用戶端 SDK 是使用 Objective-C 進行實作，因此您可能需要將 `IMFLoggerExtension.swift` 檔案新增至 Swift 專案，才能使用先前的日誌程式 API。您可以在 [{{site.data.keyword.amashort}} 用戶端 SDK 保存檔](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)中找到此檔案。


#### Cordova
{: #enable-logger-android-cordova}

```JavaScript
BMSClient.initialize(appRoute , appGUID);

var logger = MFPLogger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");

```

您可以在 Logger 類別中找到下列其他方法：

* `setCapture` - 啟用或停用稍後要傳送給 {{site.data.keyword.amashort}} 服務之日誌資訊的持續保存。
* `setLevel` - 設定儲存日誌訊息的最低記載層次。
* `send` - 將持續保存的日誌傳送給 {{site.data.keyword.amashort}} 服務。

例如，當擷取為開啟狀態，並將日誌程式層次配置為 FATAL 時，日誌程式會擷取未捕捉的異常狀況。未捕捉的異常狀況通常對於使用者會顯示為應用程式當機，但並不會擷取任何導致當機事件的日誌。或者，更詳細的日誌程式層次可確保也會擷取導致 FATAL 日誌程式項目的日誌，例如 WARN 及 ERROR。

**附註：**在 [SDK、範例、API 參考資料](sdks-samples-apis.html)中，尋找每一個平台的完整「日誌程式 API」參考資料。「日誌程式 API」是「{{site.data.keyword.amashort}} 用戶端 SDK 核心」的一部分。


### 範例用法
{: #sample-logger-usage}

下列程式碼 Snippet 顯示範例「日誌程式」用法：

#### Android
{: #enable-logger-sample-android}

```Java
// Enable persisting logs
Logger.setCapture(true);

// Set the minimum log level to be printed and persisted
Logger.setLevel(Logger.LEVEL.INFO);

// Create two logger instances
Logger logger1 = Logger.getInstance("logger1");
Logger logger2 = Logger.getInstance("logger2");

// Log messages with different levels
logger1.debug("debug message");
logger2.info("info message");

// Send persisted logs to the {{site.data.keyword.amashort}} service
Logger.send();
```

#### iOS - Objective-C
{: #enable-logger-sample-objectc}

```Objective-C
// Enable persisting logs
[IMFLogger setCapture:YES];

// Start capturing uncaught exceptions
[IMFLogger captureUncaughtExceptions];

// Set the minimum log level to be printed and persisted
[IMFLogger setLogLevel:IMFLogLevelInfo];

// Create two logger instances
IMFLogger *logger1 = [IMFLogger loggerForName:@"logger1"];
IMFLogger *logger2 = [IMFLogger loggerForName:@"logger2"];

// Log messages with different levels
[logger1 logDebugWithMessages:@"debug message"];
[logger2 logInfoWithMessages:@"info message"];

// Send persisted logs to the {{site.data.keyword.amashort}} service
[IMFLogger send];
```

#### iOS - Swift
{: #enable-logger-sample-swift}

```Swift
// Enable persisting logs
IMFLogger.setCapture(true)

// Start capturing uncaught exceptions
IMFLogger.captureUncaughtExceptions()

// Set the minimum log level to be printed and persisted
IMFLogger.setLogLevel(IMFLogLevel.Info)

// Create two logger instances
let logger1 = IMFLogger(forName: "logger1");
let logger2 = IMFLogger(forName: "logger2");

// Log messages with different levels
logger1.logDebugWithMessages("debug message")
logger2.logInfoWithMessages("info message")

// Send persisted logs to the {{site.data.keyword.amashort}} service
IMFLogger.send()

```

#### Cordova
{: #enable-logger-sample-cordova}

```JavaScript
// Enable persisting logs
MFPLogger.setCapture(true);

// Set the minimum log level to be printed and persisted
MFPLogger.setLevel(MFPLogger.INFO);

// Create two logger instances
var logger1 = MFPLogger.getInstance("logger1");
var logger2 = MFPLogger.getInstance("logger2");// Log messages with different levels
logger1.debug ("debug message");
logger2.info ("info message");

// Send persisted logs to the {{site.data.keyword.amashort}} service
MFPLogger.send(success, failure);
```

### 啟用 {{site.data.keyword.amashort}} 用戶端 SDK 內部日誌
{: #enable-logger-sdklogs}
目前只有 Android 版的 {{site.data.keyword.amashort}} 用戶端 SDK 才提供此特性。

{{site.data.keyword.amashort}} 用戶端 SDK 可提供較佳的開發體驗，原因是不會不必要地因為內部除錯訊息而增加 Logcat 輸出。因此，預設不會列印由 {{site.data.keyword.amashort}} SDK 所產生且層次為 DEBUG 的內部日誌訊息。您可以使用下列 API，來啟用 {{site.data.keyword.amashort}} 用戶端 SDK 之所有內部日誌訊息的列印：


```
Logger.setSDKInternalLoggingEnabled(true);
```

## 收集用量分析
{: #usage-analytics}

您可以配置 {{site.data.keyword.amashort}} 用戶端 SDK 來記錄用量分析，以及將記錄的資料傳送給 {{site.data.keyword.amashort}} 服務。

**重要事項**：{{site.data.keyword.amashort}} 服務的監視功能，預計會移轉至新的 [{{site.data.keyword.mobileanalytics_short}} 服務](https://console.ng.bluemix.net/catalog/services/mobile-analytics)。新的 Swift SDK 會利用新的 {{site.data.keyword.mobileanalytics_short}} 服務，此服務提供更豐富的分析體驗。{{site.data.keyword.mobileanalytics_short}} 服務目前處於實驗階段，預計在今年稍晚正式上市。由於預計會在 {{site.data.keyword.mobileanalytics_short}} 正式上市時停止使用 {{site.data.keyword.amashort}} 服務的監視功能，因此建議您先研究移轉應用程式以使用新的 {{site.data.keyword.mobileanalytics_short}} 服務及 Swift SDK。

**附註：**請確定您已啟用記載擷取，再開始記錄用量分析。

使用下列 API 來開始記錄及傳送用量分析：

#### Android
{: #usage-analytics-android}

```Java
// Enable recording of usage analytics
MFPAnalytics.enable();

// Start recording application startup time
// Add this code in the onCreate method of your main Activity
MFPAnalytics.startLoggingApplicationStartup();

// Record the duration of application startup
// Add this code in the onStart method of your main Activity
MFPAnalytics.logApplicationStartup();

// Record application foreground and background events
// Add this code in the onPause and onResume methods of your main Activity
MFPAnalytics.logSessionStart();
MFPAnalytics.logSessionEnd();

// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
MFPAnalytics.send();
```

#### iOS - Objective-C
{: #usage-analytics-objectc}

**重要事項**：雖然仍然完全支援 Objective-C SDK 且將它視為 {{site.data.keyword.Bluemix}} Mobile Services 的主要 SDK，不過預計在今年稍晚停止使用，改用新的 Swift SDK。

Objective-C SDK 會向 {{site.data.keyword.amashort}} 服務的「監視主控台」報告監視資料。如果您依賴 {{site.data.keyword.amashort}} 服務的監視功能，請繼續使用 Objective-C SDK。

```Objective-C
// Enable usage analytics recording
[[IMFAnalytics sharedInstance] setEnabled:YES];

// Start recording application lifecycle events
[[IMFAnalytics sharedInstance] startRecordingApplicationLifecycleEvents];


// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
[[IMFAnalytics sharedInstance] sendPersistedLogs];
```

#### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Enable usage analytics recording
IMFAnalytics.sharedInstance().setEnabled(true)

// Start recording application lifecycle events
IMFAnalytics.sharedInstance().startRecordingApplicationLifecycleEvents()


// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
IMFAnalytics.sharedInstance().sendPersistedLogs()
```

#### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Enable usage analytics recording
MFPAnalytics.enable();

// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
MFPAnalytics.send();
```
**附註：**當您開發 Cordova 應用程式時，請使用原生 API 來啟用應用程式生命週期事件記錄。
