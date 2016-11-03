---

copyright:
  years: 2015, 2016
lastupdated: "2016-05-06"

---

# Enabling, configuring, and using Logger
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

### Android
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

### iOS - Objective-C
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

### iOS - Swift
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


### Cordova
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


## Sample usage
{: #sample-logger-usage}

The following code snippets show sample Logger usage:

### Android
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

### iOS - Objective-C
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

### iOS - Swift
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

### Cordova
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

## Enabling the {{site.data.keyword.amashort}} client SDK internal logs
{: #enable-logger-sdklogs}
This feature is currently available only in the Android version of the {{site.data.keyword.amashort}} client SDK.

The {{site.data.keyword.amashort}} client SDK provides a better development experience by not unnecessarily increasing the Logcat output with its internal debug messages. Therefore, by default, internal log messages that are produced by the {{site.data.keyword.amashort}} SDK with the DEBUG level are not printed. You can enable printing of all internal log messages of the {{site.data.keyword.amashort}} client SDK with the following API:


```
Logger.setSDKInternalLoggingEnabled(true);
```
