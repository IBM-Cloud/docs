---

copyright:
  years: 2015, 2016
  
---

# 监视应用程序
{: #app-monitoring}
上次更新时间：2016 年 6 月 28 日
{: .last-updated}

除了安全功能外，{{site.data.keyword.amafull}} 还为移动应用程序提供了监视和分析功能。可以通过 {{site.data.keyword.amashort}} 客户端 SDK 来记录客户端日志并监视数据。开发者可以控制何时将这些数据发送到 {{site.data.keyword.amashort}} 服务。在 {{site.data.keyword.amashort}} 服务中发生的所有安全事件（例如，认证成功或失败）都会自动记录。

**注**：{{site.data.keyword.amashort}} 服务的监视功能计划迁移到新 [{{site.data.keyword.mobileanalytics_short}} 服务](https://console.ng.bluemix.net/catalog/services/mobile-analytics)。新 Swift SDK 将使用新的 {{site.data.keyword.mobileanalytics_short}} 服务，该服务提供了更加丰富的分析体验。{{site.data.keyword.mobileanalytics_short}} 服务目前在试验阶段，计划在今年晚些时候正式发布。我们建议您着手对迁移应用程序以使用新的 {{site.data.keyword.mobileanalytics_short}} 服务和 Swift SDK 进行调查，因为我们计划在 {{site.data.keyword.mobileanalytics_short}} 正式发布时，停止使用 {{site.data.keyword.amashort}} 服务的监视功能。

数据传递到 {{site.data.keyword.amashort}} 后，可以使用 {{site.data.keyword.amashort}}“监视仪表板”来获取有关移动应用程序、设备和客户端日志的分析洞察。缺省情况下会记录有关应用程序对 {{site.data.keyword.amashort}} 所保护资源提出的请求的信息。

自动记录的数据包括认证数、新设备数和新用户数等信息。此外，还可以配置 {{site.data.keyword.amashort}} 客户端 SDK 来报告以下信息：

### 移动应用程序的使用情况统计信息
{: #usage-stats}

可以将移动应用程序配置为通过一些简单的 API 调用，记录应用程序生命周期事件，并将记录的数据发送到 {{site.data.keyword.amashort}} 服务。您也可以记录应用程序打开次数、接收到的推送通知数等。

### 客户机端日志捕获
{: #client-side-logcapture}

现场的应用程序有时会遇到问题，需要引起开发者注意以进行修复。通常很难重现这些问题。<!--in R&D.--> 处理代码的开发者可能缺乏测试所需的环境或必要设备。在这些情况下，能够在环境中发生问题时从客户机设备中检索调试日志就会非常有用。

### 保存捕获到的数据
{: #preserve-captureddata}

没有方法能保证在客户端保存所有捕获到的数据。您的用户可能正在脱机运行移动应用程序，并且同时在积累捕获到的分析和日志数据。由于客户机处于脱机状态且文件系统空间有限，因此必须清除较早的记录事件，以腾出空间来保存更新的记录事件。由开发者决定何时使用提供的 API 将捕获到的数据发送到 {{site.data.keyword.amashort}} 服务。

## 使用 {{site.data.keyword.amashort}}“监视仪表板”
{: #monitoring-dashboard}

1. 打开 {{site.data.keyword.Bluemix}}“仪表板”，然后单击 {{site.data.keyword.Bluemix_notm}} 应用程序。

2. {{site.data.keyword.Bluemix_notm}} 应用程序仪表板打开时，单击 {{site.data.keyword.amashort}} 磁贴。

3. 在左侧的 {{site.data.keyword.amashort}}“仪表板”导航栏中，单击**监视**。


## 启用、配置和使用记录器
{: #enable-logger}

{{site.data.keyword.amashort}} 客户端 SDK 提供了一种日志记录框架，与您可能熟悉的其他日志框架（如 `java.util.logging` 或 `log4j`）类似。此日志记录框架支持每个数据包多个记录器实例，支持不同的日志级别，支持捕获对应用程序崩溃的堆栈跟踪，等等。

您还可以将记录的数据配置为持久存储在本地存储器中，然后可以根据需要将这些数据发送到 {{site.data.keyword.amashort}} 服务。

{{site.data.keyword.amashort}} 客户端 SDK 日志记录框架支持以下日志级别，按详细程度从低到高的顺序与其建议的使用准则一起列出：

* `FATAL` - 用于不可恢复的崩溃或挂起。FATAL 级别保留用于记录不可恢复的错误，这些错误对于用户显示为应用程序崩溃。
* `ERROR` - 用于意外异常或意外网络协议错误。
* `WARN` - 用于记录不视为严重错误的使用情况警告，例如使用了不推荐的 API 或网络响应速度慢。
* `INFO` - 用于报告初始化事件以及其他可能有用的数据。
* `DEBUG` - 用于报告调试语句，以帮助开发者解决应用程序缺陷。

在使用此日志记录框架之前，确保已初始化 {{site.data.keyword.amashort}} 客户端 SDK。以下样本演示了 {{site.data.keyword.amashort}} 客户端 SDK 日志记录框架的基本用法。

**重要信息**：{{site.data.keyword.amashort}} 服务的监视功能计划迁移到新的 [{{site.data.keyword.mobileanalytics_short}} 服务](https://console.ng.bluemix.net/catalog/services/mobile-analytics)。新 Swift SDK 将使用新的 {{site.data.keyword.mobileanalytics_short}} 服务，该服务提供了更加丰富的分析体验。{{site.data.keyword.mobileanalytics_short}} 服务目前在试验阶段，计划在今年晚些时候正式发布。我们建议您着手对迁移应用程序以使用新的 {{site.data.keyword.mobileanalytics_short}} 服务和 Swift SDK 进行调查，因为我们计划在 {{site.data.keyword.mobileanalytics_short}} 正式发布时，停止使用 {{site.data.keyword.amashort}} 服务的监视功能。

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

**重要信息：**虽然 Objective-C SDK 仍受到完全支持，且仍视为 {{site.data.keyword.Bluemix}} Mobile Services 的主 SDK，但是有计划要在今年晚些时候停止使用此 SDK，以支持新的 Swift SDK。

Objective-C SDK 会将监视数据报告给 {{site.data.keyword.amashort}} 服务的监视控制台。如果您依赖于 {{site.data.keyword.amashort}} 服务的监视功能，请继续使用 Objective-C SDK。

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

**注：**{{site.data.keyword.amashort}} 客户端 SDK 是使用 Objective-C 实现的，因此您可能需要向 Swift 项目添加 `IMFLoggerExtension.swift` 文件，以使用先前的记录器 API。可以在 [{{site.data.keyword.amashort}} 客户端 SDK 归档](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)中找到此文件。


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

您可以在 Logger 类中找到以下更多方法：

* `setCapture` - 启用或禁用以后要发送到 {{site.data.keyword.amashort}} 服务的日志信息的持久存储。
* `setLevel` - 设置要保存日志消息的最低日志级别。
* `send` - 将持久存储的日志发送到 {{site.data.keyword.amashort}} 服务。

例如，捕获已启用且记录器级别配置为 FATAL 时，记录器会捕获到未捕获的异常。未捕获的异常通常对于用户显示为应用程序崩溃，但并不捕获有关导致崩溃事件的任何日志。或者，更详细的记录器级别可确保同时捕获导致 FATAL 记录器条目的日志，例如 WARN 和 ERROR。

**注：**在 [SDK、样本和 API 参考](sdks-samples-apis.html)中可找到每个平台的完整记录器 API 参考。记录器 API 是 {{site.data.keyword.amashort}} 客户端 SDK 核心的组成部分。


### 样本用法
{: #sample-logger-usage}

以下代码片段显示了样本记录器用法：

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
var logger2 = MFPLogger.getInstance("logger2");

// Log messages with different levels
logger1.debug ("debug message");
logger2.info ("info message");

// Send persisted logs to the {{site.data.keyword.amashort}} service
MFPLogger.send(success, failure);
```

### 启用 {{site.data.keyword.amashort}} 客户端 SDK 内部日志
{: #enable-logger-sdklogs}
此功能目前只可用于 Android 版本的 {{site.data.keyword.amashort}} 客户端 SDK。

{{site.data.keyword.amashort}} 客户端 SDK 没有用其内部调试消息来不必要地增加 LogCat 输出，因此提供了更好的开发体验。所以，缺省情况下不会输出 {{site.data.keyword.amashort}} SDK 在 DEBUG 级别下生成的内部日志消息。可以使用以下 API 来启用 {{site.data.keyword.amashort}} 客户端 SDK 的所有内部日志消息的输出：


```
Logger.setSDKInternalLoggingEnabled(true);
```

## 收集使用情况分析信息
{: #usage-analytics}

您可以将 {{site.data.keyword.amashort}} 客户端 SDK 配置为记录使用情况分析信息，并将记录的数据发送到 {{site.data.keyword.amashort}} 服务。

**重要信息**：{{site.data.keyword.amashort}} 服务的监视功能计划迁移到新的 [{{site.data.keyword.mobileanalytics_short}} 服务](https://console.ng.bluemix.net/catalog/services/mobile-analytics)。新 Swift SDK 将使用新的 {{site.data.keyword.mobileanalytics_short}} 服务，该服务提供了更加丰富的分析体验。{{site.data.keyword.mobileanalytics_short}} 服务目前在试验阶段，计划在今年晚些时候正式发布。我们建议您着手对迁移应用程序以使用新的 {{site.data.keyword.mobileanalytics_short}} 服务和 Swift SDK 进行调查，因为我们计划在 {{site.data.keyword.mobileanalytics_short}} 正式发布时，停止使用 {{site.data.keyword.amashort}} 服务的监视功能。

**注：**开始记录使用情况分析信息之前，请确保您已启用日志记录捕获。

使用以下 API 来开始记录和发送使用情况分析信息：

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

**重要信息：**虽然 Objective-C SDK 仍受到完全支持，且仍视为 {{site.data.keyword.Bluemix}} Mobile Services 的主 SDK，但是有计划要在今年晚些时候停止使用此 SDK，以支持新的 Swift SDK。

Objective-C SDK 会将监视数据报告给 {{site.data.keyword.amashort}} 服务的监视控制台。如果您依赖于 {{site.data.keyword.amashort}} 服务的监视功能，请继续使用 Objective-C SDK。

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
**注：**开发 Cordova 应用程序时，请使用本机 API 来启用应用程序生命周期事件记录。
