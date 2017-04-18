---

copyright:
  years: 2015, 2016
  
---

# 监视应用程序
{: #app-monitoring}
上次更新时间：2016 年 9 月 22 日
{: .last-updated}

除了安全功能外，{{site.data.keyword.amafull}} 还为移动应用程序提供了监视和分析功能。可以通过 {{site.data.keyword.amashort}} 客户端 SDK 来记录客户端日志并监视数据。开发者可以控制何时将这些数据发送到 {{site.data.keyword.amashort}} 服务。在 {{site.data.keyword.amashort}} 服务中发生的所有安全事件（例如，认证成功或失败）都会自动记录。
<!--
**Note**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

数据传递到 {{site.data.keyword.amashort}} 后，可以使用 {{site.data.keyword.amashort}}“监视仪表板”来获取有关移动应用程序、设备和客户端日志的分析洞察。缺省情况下会记录有关应用程序对 {{site.data.keyword.amashort}} 所保护资源提出的请求的信息。

自动记录的数据包括认证数、新设备数和新用户数等信息。此外，还可以配置 {{site.data.keyword.amashort}} 客户端 SDK 来报告以下信息：

### 移动应用程序的使用情况统计信息
{: #usage-stats}

可以将移动应用程序配置为通过一些简单的 API 调用，记录应用程序生命周期事件，并将记录的数据发送到 {{site.data.keyword.amashort}} 服务。您也可以记录应用程序打开次数、接收到的推送通知数等。

### 客户机端日志捕获
{: #client-side-logcapture}

现场的应用程序有时会遇到问题，需要引起开发者注意以进行修复。通常很难重现这些问题。处理代码的开发者可能缺乏测试所需的环境或必要设备。在这些情况下，能够在环境中发生问题时从客户机设备中检索调试日志就会非常有用。

### 保存捕获到的数据
{: #preserve-captureddata}

没有方法能保证在客户端保存所有捕获到的数据。您的用户可能正在脱机运行移动应用程序，并且同时在积累捕获到的分析和日志数据。由于客户机处于脱机状态且文件系统空间有限，因此必须清除较早的记录事件，以腾出空间来保存更新的记录事件。由开发者决定何时使用提供的 API 将捕获到的数据发送到 {{site.data.keyword.amashort}} 服务。

## 使用 {{site.data.keyword.amashort}}“监视仪表板”
{: #monitoring-dashboard}

1. 打开 {{site.data.keyword.Bluemix}}“仪表板”，然后单击 {{site.data.keyword.Bluemix_notm}} 应用程序。

2. {{site.data.keyword.Bluemix_notm}} 应用程序仪表板打开时，单击 {{site.data.keyword.amashort}} 磁贴。

3. 单击 {{site.data.keyword.amashort}} 仪表板导航中的**监视**按钮。


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

#### 日志级别场景
{: #log-level-scenario}

记录器级别配置为 `FATAL` 时，记录器会捕获未捕获的异常，但并不捕获导致崩溃事件的任何日志。您可以设置更详细的记录器级别以确保同时捕获导致 `FATAL` 记录器条目的日志，例如 `WARN` 和 `ERROR`。

在使用此日志记录框架之前，确保已初始化 {{site.data.keyword.amashort}} 客户端 SDK。以下样本演示了 {{site.data.keyword.amashort}} 客户端 SDK 日志记录框架的基本用法。

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

**bluemixRegion** 参数指定使用的是哪种 Bluemix 部署，例如 `BMSClient.REGION_US_SOUTH` 和 `BMSClient.REGION_UK`。 

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

您可以在 Logger 类中找到以下更多方法：

* `setCapture` - 启用或禁用以后要发送到 {{site.data.keyword.amashort}} 服务的日志信息的持久存储。
* `setLevel` - 设置要保存日志消息的最低日志级别。
* `send` - 将持久存储的日志发送到 {{site.data.keyword.amashort}} 服务。

例如，捕获已启用且记录器级别配置为 FATAL 时，记录器会捕获到未捕获的异常。未捕获的异常通常对于用户显示为应用程序崩溃，但并不捕获有关导致崩溃事件的任何日志。或者，更详细的记录器级别可确保同时捕获导致 FATAL 记录器条目的日志，例如 WARN 和 ERROR。

**注：**在 [SDK、样本和 API 参考](sdks-samples-apis.html)中可找到每个平台的完整记录器 API 参考。记录器 API 是 {{site.data.keyword.amashort}} 客户端 SDK 核心的组成部分。


### 样本记录器用法
{: #sample-logger-usage}

以下代码片段显示了样本记录器用法：

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

### 启用 {{site.data.keyword.amashort}} 客户端 SDK 内部日志
{: #enable-logger-sdklogs}
此功能目前只可用于 Android 版本的 {{site.data.keyword.amashort}} 客户端 SDK。

{{site.data.keyword.amashort}} 客户端 SDK 没有用其内部调试消息来不必要地增加 LogCat 输出，因此提供了更好的开发体验。所以，缺省情况下不会输出 {{site.data.keyword.amashort}} SDK 在 DEBUG 级别下生成的内部日志消息。可以使用以下 API 来启用 {{site.data.keyword.amashort}} 客户端 SDK 的所有内部日志消息的输出：


```
Logger.setSDKInternalLoggingEnabled(true);
```
{: codeblock}

## 收集使用情况分析信息
{: #usage-analytics}

您可以将 {{site.data.keyword.amashort}} 客户端 SDK 配置为记录使用情况分析信息，并将记录的数据发送到 {{site.data.keyword.amashort}} 服务。
<!--
**Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

**注：**开始记录使用情况分析信息之前，请确保您已启用日志记录捕获。

使用以下 API 来开始记录和发送使用情况分析信息：

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

**注：**开发 Cordova 应用程序时，请使用本机 API 来启用应用程序生命周期事件记录。

