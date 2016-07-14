---

copyright:
  years: 2015, 2016
  
---

# Monitoring applications
{: #app-monitoring}
*Last updated: 28 June 2016*
{: .last-updated}

In addition to security features, the {{site.data.keyword.amafull}} also provides monitoring and analytics for your mobile applications. You can record client logs and monitor data with the {{site.data.keyword.amashort}} client SDK. Developers can control when to send this data to the {{site.data.keyword.amashort}} Service. All the security events, such as authentication success or failure, that occur in {{site.data.keyword.amashort}} Service are logged automatically.

**Note**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available.

When data is delivered to {{site.data.keyword.amashort}}, you can use the {{site.data.keyword.amashort}} Monitoring Dashboard to get analytics insights about your mobile applications, devices, and client logs. Information about requests that your application makes to resources that are protected by {{site.data.keyword.amashort}} are recorded by default.

The automatically recorded data includes information such as number of authentications, new devices, and new users. In addition you can configure the {{site.data.keyword.amashort}} client SDK to report the following information:

### Usage statistics of your mobile applications
{: #usage-stats}

You can configure your mobile applications to record application lifecycle events and send the recorded data to the {{site.data.keyword.amashort}} service with a few simple API calls. You can record the number of app opens, push notifications that are received, and so on.

### Client-side log capture
{: #client-side-logcapture}

Applications in the field occasionally experience problems that require a developer's attention to fix. It is often difficult to reproduce these problems. <!--in R&D.--> Developers who worked on the code might lack the environment or exact device with which to test. In these situations, it is helpful to be able to retrieve debug logs from the client devices as the problems occur in the environment in which they happen.

### Preserve captured data
{: #preserve-captureddata}

There is no way to guarantee that all captured data is preserved on the client side. Your users might be running the mobile application offline and simultaneously accumulating captured analytic and log data. Because the client is offline with limited file system space, older logged events must be purged in favor of preserving more recently logged events. It is up to the developer to decide when to send captured data to the {{site.data.keyword.amashort}} Service by using the supplied APIs.

## Using the {{site.data.keyword.amashort}} Monitoring Dashboard
{: #monitoring-dashboard}

1. Open the {{site.data.keyword.Bluemix}} Dashboard, and click your {{site.data.keyword.Bluemix_notm}} application.

2. When your {{site.data.keyword.Bluemix_notm}} application dashboard is open, click a {{site.data.keyword.amashort}} tile.

3. In the {{site.data.keyword.amashort}} Dashboard, click the **Monitoring** link in the left-hand menu.

## Enabling, configuring, and using Logger
{: #enable-logger}

The {{site.data.keyword.amashort}} client SDK provides a logging framework that is similar to other log frameworks that you might be familiar with, such as `java.util.logging` or `log4j`. The logging framework supports multiple per-package logger instances, different log levels, capturing of stack traces for an application crash and more.

You can also configure the logged data to be persisted to a local store, which can be sent to the {{site.data.keyword.amashort}} service on demand.

The {{site.data.keyword.amashort}} client SDK logging framework supports the following log levels, listed from least to most verbose, with recommended use guidelines:

* `FATAL` - Use for unrecoverable crashes or hangs. The FATAL level is reserved for logging unrecoverable errors, which appear to users as an application crash.
* `ERROR` - Use for unexpected exceptions or unexpected network protocol errors.
* `WARN` - To log usage warnings that are not considered critical errors, such as usage of deprecated APIs or slow network response.
* `INFO` - Use for reporting initialization events and other data that might be useful.
* `DEBUG` - Use for reporting debug statements to help developers resolve application defects.

Make sure that you have initialized the {{site.data.keyword.amashort}} client SDK prior to using the logging framework. The following samples demonstrate the basic usage of a {{site.data.keyword.amashort}} client SDK logging framework.

**Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available.

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

**Important**: While the Objective-C SDK remains fully supported, and is still considered the primary SDK for {{site.data.keyword.Bluemix}} Mobile Services, it is planned to be discontinued later this year in favor of the new Swift SDK.

The Objective-C SDK reports monitoring data to the Monitoring Console of the {{site.data.keyword.amashort}} service. If you rely on the monitoring functions of the {{site.data.keyword.amashort}} service, continue to use the Objective-C SDK.

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

**Note:** The {{site.data.keyword.amashort}} client SDK is implemented with Objective-C, therefore you might need to add the `IMFLoggerExtension.swift` file to your Swift project to use the previous logger API. You can find this file in the [{{site.data.keyword.amashort}} client SDK archive](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).


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

You can find the following additional methods in Logger classes:

* `setCapture` - Enables or disables persisting log information to be sent to {{site.data.keyword.amashort}} service later.
* `setLevel` - Sets the minimum log level to save log messages.
* `send` - Sends persisted logs to the {{site.data.keyword.amashort}} service.

For example, when capture is ON and the logger level is configured to FATAL, the logger captures uncaught exceptions. Uncaught exceptions often appear to users as application crashes, but do not capture any logs that lead up to the crash event. Alternatively, a more verbose logger level ensures that logs that lead to a FATAL logger entry, such as WARN and ERROR, are also captured.

**Note:** Find full Logger API references for each platform at [SDKs, samples, API reference](sdks-samples-apis.html). The Logger API is part of the {{site.data.keyword.amashort}} client SDK Core.


### Sample usage
{: #sample-logger-usage}

The following code snippets show sample Logger usage:

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

### Enabling the {{site.data.keyword.amashort}} client SDK internal logs
{: #enable-logger-sdklogs}
This feature is currently available only in the Android version of the {{site.data.keyword.amashort}} client SDK.

The {{site.data.keyword.amashort}} client SDK provides a better development experience by not unnecessarily increasing the Logcat output with its internal debug messages. Therefore, by default, internal log messages that are produced by the {{site.data.keyword.amashort}} SDK with the DEBUG level are not printed. You can enable printing of all internal log messages of the {{site.data.keyword.amashort}} client SDK with the following API:


```
Logger.setSDKInternalLoggingEnabled(true);
```

## Gathering usage analytics
{: #usage-analytics}

You can configure the {{site.data.keyword.amashort}} client SDK to record usage analytics and send the recorded data to the {{site.data.keyword.amashort}} service.

**Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available.

**Note:** Ensure that you have enabled logging capture before you start recording usage analytics.

Use the following APIs to start recording and sending usage analytics:

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

**Important**: While the Objective-C SDK remains fully supported, and is still considered the primary SDK for {{site.data.keyword.Bluemix}} Mobile Services, it is planned to be discontinued later this year in favor of the new Swift SDK.

The Objective-C SDK reports monitoring data to the Monitoring Console of the {{site.data.keyword.amashort}} service. If you rely on the monitoring functions of the {{site.data.keyword.amashort}} service, continue to use the Objective-C SDK.

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
**Note:** When you are developing Cordova applications, use the native API to enable application lifecycle event recording.
