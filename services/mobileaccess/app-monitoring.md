---

copyright:
  years: 2015, 2016
lastupdated: "2016-09-22"

---

# Monitoring applications
{: #app-monitoring}

In addition to security features, the {{site.data.keyword.amafull}} also provides monitoring and analytics for your mobile applications. You can record client logs and monitor data with the {{site.data.keyword.amashort}} client SDK. Developers can control when to send this data to the {{site.data.keyword.amashort}} Service. All the security events, such as authentication success or failure, that occur in {{site.data.keyword.amashort}} Service are logged automatically.
<!--
**Note**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

When data is delivered to {{site.data.keyword.amashort}}, you can use the {{site.data.keyword.amashort}} Monitoring Dashboard to get analytics insights about your mobile applications, devices, and client logs. Information about requests that your application makes to resources that are protected by {{site.data.keyword.amashort}} are recorded by default.

The automatically recorded data includes information such as number of authentications, new devices, and new users. In addition you can configure the {{site.data.keyword.amashort}} client SDK to report the following information:

### Usage statistics of your mobile applications
{: #usage-stats}

You can configure your mobile applications to record application lifecycle events and send the recorded data to the {{site.data.keyword.amashort}} service with a few simple API calls. You can record the number of app opens, push notifications that are received, and so on.

### Client-side log capture
{: #client-side-logcapture}

Applications in the field occasionally experience problems that require a developer's attention to fix. It is often difficult to reproduce these problems. Developers who worked on the code might lack the environment or exact device with which to test. In these situations, it is helpful to be able to retrieve debug logs from the client devices as the problems occur in the environment in which they happen.

### Preserve captured data
{: #preserve-captureddata}

There is no way to guarantee that all captured data is preserved on the client side. Your users might be running the mobile application offline and simultaneously accumulating captured analytic and log data. Because the client is offline with limited file system space, older logged events must be purged in favor of preserving more recently logged events. It is up to the developer to decide when to send captured data to the {{site.data.keyword.amashort}} Service by using the supplied APIs.

## Using the {{site.data.keyword.amashort}} Monitoring Dashboard
{: #monitoring-dashboard}

1. Open the {{site.data.keyword.Bluemix}} Dashboard, and click your {{site.data.keyword.Bluemix_notm}} application.

2. When your {{site.data.keyword.Bluemix_notm}} application dashboard is open, click a {{site.data.keyword.amashort}} tile.

3. Click the **Monitoring** button in the {{site.data.keyword.amashort}} Dashboard navigation.


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

#### Log level scenario
{: #log-level-scenario}

When the logger level is configured to `FATAL`, the logger captures uncaught exceptions, but does not capture any logs that lead up to the crash event. You can set a more verbose logger level to ensure that logs that might lead to a `FATAL` logger entry, such as `WARN` and `ERROR`, are also captured.

Make sure that you have initialized the {{site.data.keyword.amashort}} client SDK prior to using the logging framework. The following samples demonstrate the basic usage of a {{site.data.keyword.amashort}} client SDK logging framework.

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

The **bluemixRegion** parameter specifies which Bluemix deployment you are using, for example, `BMSClient.REGION_US_SOUTH` and `BMSClient.REGION_UK`.

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

You can find the following additional methods in Logger classes:

* `setCapture` - Enables or disables persisting log information to be sent to {{site.data.keyword.amashort}} service later.
* `setLevel` - Sets the minimum log level to save log messages.
* `send` - Sends persisted logs to the {{site.data.keyword.amashort}} service.

For example, when capture is ON and the logger level is configured to FATAL, the logger captures uncaught exceptions. Uncaught exceptions often appear to users as application crashes, but do not capture any logs that lead up to the crash event. Alternatively, a more verbose logger level ensures that logs that lead to a FATAL logger entry, such as WARN and ERROR, are also captured.

**Note:** Find full Logger API references for each platform at [SDKs, samples, API reference](sdks-samples-apis.html). The Logger API is part of the {{site.data.keyword.amashort}} client SDK Core.


### Sample Logger usage
{: #sample-logger-usage}

The following code snippets show sample Logger usage:

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

### Enabling the {{site.data.keyword.amashort}} client SDK internal logs
{: #enable-logger-sdklogs}
This feature is currently available only in the Android version of the {{site.data.keyword.amashort}} client SDK.

The {{site.data.keyword.amashort}} client SDK provides a better development experience by not unnecessarily increasing the Logcat output with its internal debug messages. Therefore, by default, internal log messages that are produced by the {{site.data.keyword.amashort}} SDK with the DEBUG level are not printed. You can enable printing of all internal log messages of the {{site.data.keyword.amashort}} client SDK with the following API:


```
Logger.setSDKInternalLoggingEnabled(true);
```
{: codeblock}

## Gathering usage analytics
{: #usage-analytics}

You can configure the {{site.data.keyword.amashort}} client SDK to record usage analytics and send the recorded data to the {{site.data.keyword.amashort}} service.
<!--
**Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

**Note:** Ensure that you have enabled logging capture before you start recording usage analytics.

Use the following APIs to start recording and sending usage analytics:

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

**Note:** When you are developing Cordova applications, use the native API to enable application lifecycle event recording.
