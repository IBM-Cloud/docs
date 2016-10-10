---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-08"

---

# Instrumenting your application to use the {{site.data.keyword.mobileanalytics_short}} client SDKs
{: #mobileanalytics_sdk}

The {{site.data.keyword.mobileanalytics_full}} SDKs enable you to instrument your mobile application.
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}} enables you to collect two <!--three--> categories of data, and each requires a different degree of instrumentation:

1. Pre-defined data - This category includes generic usage and device information that applies to all applications. Within this category is device metadata (operating system and device model) and usage data (active users and application sessions) that indicates the volume, frequency, or duration of application use. Pre-defined data is collected automatically after you initialize the {{site.data.keyword.mobileanalytics_short}} SDK in your application.

2. Application log messages - This category enables the developer to add lines of code throughout the application that log custom messages to assist in development and debugging. The developer assigns a severity/verbosity level to each log message and can subsequently filter messages by assigned level or preserve storage space by configuring the application to ignore messages that are at a lower level of a given log level. To collect application log data, you must initialize the {{site.data.keyword.mobileanalytics_short}} SDK within your application, as well as add a line of code for each log message.

<!--2. Custom events - This category includes data that you define yourself and that is specific to your app. This data represents events that occur within your app, such as page views, button taps, or in-app purchases. In addition to initializing the {{site.data.keyword.mobileanalytics_short}} SDK in your app, you must add a line of code for each custom event that you want to track. -->

Currently SDKs are available for Android, iOS, and WatchOS.

## Identifying your Service Credentials API Key value
{: #analytics-clientkey}

Identify your **API Key** value before you set up the client SDK. The API Key is required for initializing the client SDK.

1. Open your {{site.data.keyword.mobileanalytics_short}} service dashboard.
2. Click the **Service Credentials** tab.
3. Expand **View Credentials** to reveal your API Key value. You will need the API Key value when you initialize the {{site.data.keyword.mobileanalytics_short}} Client SDK.


## Initializing your Android application to collect analytics
{: #initalize-ma-sdk-android}

Initialize your application to enable sending logs to the {{site.data.keyword.mobileanalytics_short}} service.

1. Import the Client SDK by adding the following `import` statement at the beginning of your project file:

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
  ```
  {: codeblock}

2. Initialize the {{site.data.keyword.mobileanalytics_short}} Client SDK in your Android application by adding the initialization code in the `onCreate` method of the main activity in your Android application, or in a location that works best for your project.

	```Java
	BMSClient.getInstance().initialize(this.getApplicationContext(), BMSClient.REGION_US_SOUTH); // Make sure that you point to your region
	```
  {: codeblock}

  To use the {{site.data.keyword.mobileanalytics_short}} Client SDK, you must initialize the `BMSClient` with the **bluemixRegion** parameter. In the initializer, the **bluemixRegion** value specifies which {{site.data.keyword.Bluemix_notm}} deployment you are using, for example, `BMSClient.REGION_US_SOUTH` and `BMSClient.REGION_UK`. 
    <!-- , or `BMSClient.REGION_SYDNEY`.-->  <!-- Set this value with a `BMSClient.REGION` static property. -->

  <!--You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. Initialize Analytics by using your Android application object and giving it your application’s name. You also need the [**API Key**](#analytics-clientkey) value.
	
	```Java
	// In this code example, Analytics is configured to record lifecycle events.
	Analytics.init(getApplication(), "your_app_name_here", apiKey, hasUserContext, Analytics.DeviceEvent.LIFECYCLE);
	```
  {: codeblock}
	
	The name that you select for your application (`your_app_name_here`) displays in the {{site.data.keyword.mobileanalytics_short}} console as the application name. The application name is used as a filter to search for application logs in the dashboard. When you use the same application name across platforms (for example, Android and iOS), you can see all logs from that application under the same name, regardless of which platform the logs were sent from.
	
	**Note:** Set the value for `hasUserContext` to **true** or **false**. If false (default value), each device is counted as an active user. The [`Analytics.setUserIdentity("username")`](sdk.html#android-tracking-users) method, which enables you to track the number of users per device who are actively using your application, will not work when `hasUserContext` is false. If true, each use of [`Analytics.setUserIdentity("username")`](sdk.html#android-tracking-users) counts as an active user. There is no default user identity when `hasUserContext` is true, and therefore must be set to populate the active user charts.
	
4. [Send analytics data](sdk.html#app-monitoring-gathering-analytics) to the (sdk.html#app-monitoring-gathering-analytics) service.

## Initializing your iOS application to collect analytics
{: #init-ma-sdk-ios}

Initialize your application to enable sending logs to the {{site.data.keyword.mobileanalytics_short}} service. The Swift SDK is available for iOS and watchOS.

1. Import the `BMSCore` and `BMSAnalytics` frameworks by adding the following `import` statements to the beginning of your `AppDelegate.swift` project file:

  ```Swift
  import BMSCore
  import BMSAnalytics
  ```
  {: codeblock}

2. To use the {{site.data.keyword.mobileanalytics_short}} Client SDK, you must first initialize the `BMSClient` class, using the following code.

  Place the initialization code in the `application(_:didFinishLaunchingWithOptions:)` method of your application delegate, or in a location that works best for your project.
	
    ```Swift 
    BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Make sure that you point to your region
    ```
    {: codeblock}

    To use the {{site.data.keyword.mobileanalytics_short}} Client SDK, you must initialize the `BMSClient` with the **bluemixRegion** parameter. In the initializer, the **bluemixRegion** value specifies which {{site.data.keyword.Bluemix_notm}} deployment you are using, for example, `BMSClient.REGION_US_SOUTH` or `BMSClient.REGION_UK`.
    <!-- , or `BMSClient.REGION_SYDNEY`. -->
   
   <!-- Set this value with a `BMSClient.REGION` static property. -->

   <!-- You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. Initialize Analytics by giving it your mobile application’s name. You also need the [**API Key**](#analytics-clientkey) value.

 The application name is used as a filter to search for application logs in your {{site.data.keyword.mobileanalytics_short}} Dashboard. By using the same application name across platforms (for example, Android and iOS), you can see all logs from that application under the same name, regardless of which platform the logs were sent from.

  An optional `deviceEvents` parameter automatically gathers analytics for device-level events.

 ### iOS
 {: #ios-initialize-analytics}
	
 ```Swift
 Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: DeviceEvent.lifecycle)
 ```
 {: codeblock}
  
 ### watchOS
 {: #watchos-initialize-analytics}
	
 ```Swift
 Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false)
  ```
 {: codeblock}
	
 The name that you select for your application (`your_app_name_here`) displays in the {{site.data.keyword.mobileanalytics_short}} console as the application name. The application name is used as a filter to search for application logs in the dashboard. When you use the same application name across platforms (for example, Android and iOS), you can see all logs from that application under the same name, regardless of which platform the logs were sent from.
	
 **Note:** Set the value for `hasUserContext` to **true** or **false**. If false (default value), each device is counted as an active user. The [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) method, which enables you to track the number of users per device who are actively using your application, will not work when `hasUserContext` is false. If `hasUserContext` is true, each use of [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) counts as an active user. There is no default user identity when `hasUserContext` is true, and therefore must be set to populate the active user charts.

 You can record device events on WatchOS by using the `Analytics.recordApplicationDidBecomeActive()` and `Analytics.recordApplicationWillResignActive()` methods.
  
 Add the following line to the `applicationDidBecomeActive()` method of the ExtensionDelegate class.

	```
	Analytics.recordApplicationDidBecomeActive()
	```
  {: codeblock}

 Add the following line to applicationWillResignActive() method of the ExtensionDelegate class:
	```
	Analytics.recordApplicationWillResignActive()
	```
  {: codeblock}
  
4. [Send analytics data](sdk.html#app-monitoring-gathering-analytics) to the {{site.data.keyword.mobileanalytics_short}} service.

## Gathering usage analytics
{: #app-monitoring-gathering-analytics}

  You can configure the {{site.data.keyword.mobileanalytics_short}} Client SDK to record usage analytics and send the recorded data to the {{site.data.keyword.mobileanalytics_short}} service.

  Use the following APIs to start recording and sending usage analytics:

#### Android
{: #android-usage-api}
	
```
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.disable();
	
// Enable recording of usage analytics
Analytics.enable();
		
// Send recorded usage analytics to the Mobile Analytics Service
Analytics.send(new ResponseListener() {
            @Override
            public void onSuccess(Response response) {
                // Handle Analytics send success here.
            }

            @Override
            public void onFailure(Response response, Throwable throwable, JSONObject jsonObject) {
                // Handle Analytics send failure here.
            }
        });
```
{: codeblock}

<!-- removed: Analytics.log(eventJSONObject); -->

<!--	
Sample usage analytics for logging an event:
	
```
// Log a custom analytics event for custom charts, which is represented by a JSON object:
JSONObject eventJSONObject = new JSONObject();
	
eventJSONObject.put("customProperty" , "propertyValue");
```
{: codeblock}
-->

#### iOS - Swift
{: #ios-usage-api}

```
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.isEnabled = false

// Enable recording of usage analytics
Analytics.isEnabled = true

// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service
Analytics.send(completionHandler: { (response: Response?, error: Error?) in
    
    if let response = response {
        logger.debug(message: "Status code: \(response.statusCode)")
        logger.debug(message: "Response: \(response.responseText)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
})
```
{: codeblock}

<!--
Sample usage analytics for logging an event:

#### Swift
{: customchartsswift}

```Swift
// Log a custom analytics event for custom charts
let eventObject = ["customProperty": "propertyValue"]
Analytics.log(eventObject)
```
{: codeblock}

-->

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
  
## Enabling, configuring, and using Logger
{: #app-monitoring-logger}

  The {{site.data.keyword.mobileanalytics_full}} Client SDK provides a logging framework that is similar to other log frameworks that you might be familiar with, such as `java.util.logging` or `log4j`. The logging framework supports multiple per-package logger instances, different log levels, capturing of stack traces for an application crash, and more.

  You can also configure the logged data to be stored on the device where the application is running and send these device logs to the {{site.data.keyword.mobileanalytics_short}} Service at a later time.

  <!-- Initialization has to happen first to be able to collect logs and send them to the {{site.data.keyword.mobileanalytics_short}} service. -->

  The {{site.data.keyword.mobileanalytics_short}} Client SDK logging framework supports the following log levels, which are listed from least to most verbose, with recommended use guidelines:

  * `FATAL` - Use for unrecoverable crashes or hangs. The `FATAL` level is reserved for logging unrecoverable errors, which appear to users as an application crash
  * `ERROR` - Use for unexpected exceptions or unexpected network protocol errors
  * `WARN` - Use to log usage warnings that are not considered critical errors, such as usage of deprecated APIs or slow network response
  * `INFO` - Use for reporting initialization events and other data that might be important, but not urgent
  * `DEBUG` - Use for reporting debug statements to help developers resolve application defects

    #### Log level scenario
    {: #log-level-scenario}

    When the logger level is configured to `FATAL`, the logger captures uncaught exceptions, but does not capture any logs that lead up to the crash event. You can set a more verbose logger level to ensure that logs that might lead to a `FATAL` logger entry, such as `WARN` and `ERROR`, are also captured.

  <!--**Note:** Find full Logger API references for each platform at [SDKs, samples, API reference](sdks-samples-apis.html). The Logger API is part of the--> <!--{{site.data.keyword.mobileanalytics_short}} Client SDK Core.-->

  <!--### Cordova-->


  <!--```JavaScript-->

  <!--var logger = MFPLogger.getInstance("myLogger");-->

  <!--logger.debug("debug info");-->
  <!--logger.info("info message");-->
  <!--logger.warn("warning message");-->
  <!--logger.fatal("fatal message");-->

  <!--```-->


### Sample Logger usage
{: #sample-logger-usage}

**Note:** Make sure that you have instrumented your application to use the {{site.data.keyword.mobileanalytics_short}} Client SDK before you use the logging framework.
 
  The following code snippets show sample Logger usage:

#### Android
{: #android-logger-sample}

```
// Configure Logger to save logs to the device so that they 
// can later be sent to the Mobile Analytics service
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

// Send logs to the Mobile Analytics Service
        Logger.send(new ResponseListener() {
                    @Override
                    public void onSuccess(Response response) {
                        // Handle Logger send success here.
                    }

                    @Override
                    public void onFailure(Response response, Throwable throwable, JSONObject jsonObject) {
                        // Handle Logger send failure here.
                    }
                });        
```
{: codeblock}

#### iOS - Swift
{: #ios-logger-sample-swift2}

```
// Configure Logger to save logs to the device so that they can later be sent to the Mobile Analytics service
// Disabled by default; set to true to enable
Logger.isLogStorageEnabled = true

// Change the minimum log level (optional)
// The default setting is LogLevel.debug
Logger.logLevelFilter = LogLevel.info

// Create two logger instances
// You can create multiple log instances to organize your logs
let logger1 = Logger.logger(name: “feature1Logger”)
let logger2 = Logger.logger(name: “feature2Logger”)

// Log messages with different levels
logger1.debug(message: "debug message for feature 1") 
//the logger1.debug message is not logged because the logLevelFilter is set to info
logger2.info(message: "info message for feature 2")

// Send logs to the Mobile Analytics Service
Logger.send(completionHandler: { (response: Response?, error: Error?) in
    
    if let response = response {
        logger.debug(message: "Status code: \(response.statusCode)")
        logger.debug(message: "Response: \(response.responseText)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
})
```
{: codeblock}

**Tip:** For privacy concerns, you can disable Logger output for applications that are built in release mode. By default, the Logger class prints logs to the Xcode console. In the build settings for your target, add a `-D RELEASE_BUILD` flag to the **Other Swift Flags** section of the release build configuration.
    

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
{: codeblock}
Logger.setSDKDebugLoggingEnabled(true);
```
{: codeblock}

#### iOS - Swift
{: #enable-logger-print-swift}

```
Logger.sdkDebugLoggingEnabled = true
```
{: codeblock}
-->

## Reporting crash analytics
{: #report-crash-analytics}

You can see [application crash data](app-monitoring.html#monitor-app-crash) by sending analytics and log information to {{site.data.keyword.mobileanalytics_short}}.

The `Analytics.send()` method populates the crash overview and crashes tables on the Crashes page. Charts in this section are enabled by using the initialization and sending process for analytics; no special configuration is necessary.

The `Logger.send()` method populates the the Crashes and Crash Details tables on the Troubleshooting page. You must enable your application to store and send logs to populate the charts in this section, by adding an additional statement in your application code:

#### Android
{: #android-crash-statement}

* `Logger.storeLogs(true);`
<!-- * `Logger.setLogLevel(Logger.LEVEL.FATAL); // or greater` -->

See [sample logger usage](sdk.html#android-logger-sample).

#### iOS
{: #ios-crash-statement}

* `Logger.isLogStorageEnabled = true`
<!-- * `Logger.logLevelFilter = LogLevel.Fatal // or greater` -->

See [sample logger usage](sdk.html##ios-logger-sample-swift2).

## Tracking active users
{: #trackingusers}
If your application can recognize unique users on a device, you can optionally track how many users are actively using your application by passing the user name of the active user to {{site.data.keyword.mobileanalytics_short}}. 

Enable user tracking by initializing {{site.data.keyword.mobileanalytics_short}} with `hasUserContext=true`. Otherwise, {{site.data.keyword.mobileanalytics_short}}  captures only one user per device. 

#### Android
{: #android-tracking-users}

Add the following code to track when the user logs in:

```
Analytics.setUserIdentity("username");
```
{: codeblock}

<!--Add the following code for when the user logs out:

```
Analytics.clearUserIdentity();
```
{: codeblock}
-->

#### iOS - Swift
{: #ios-tracking-users}

Add the following code to track when the user logs in:

```
Analytics.userIdentity = "username"
```
{: codeblock}

<!--
Add the following code for when the user logs out:

```
Analytics.userIdentity = nil
```
{: codeblock}
-->

<!--## Configuring MobileFirst Platform Foundation servers to use the {{site.data.keyword.mobileanalytics_short}} service (optional)
{: #configmfp}
  If you are using MobileFirst Platform Foundation Server V7 and higher, you can configure it to use the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} service to store analytics and logged data. 
  
  Configure MobileFirst Platform V7.0, V7.1, and V8.0 Beta servers to send analytics data to the {{site.data.keyword.mobileanalytics_short}} service on {{site.data.keyword.Bluemix_notm}}.

  1. Visit the dashboard for the {{site.data.keyword.mobileanalytics_short}} service where you want to send analytics data and note the browser URL for the dashboard.
  2. Determine the value for reporting analytics, as follows:
  	1. Get the {{site.data.keyword.mobileanalytics_short}} service route from the dashboard URL. The {{site.data.keyword.mobileanalytics_short}} service route is the part of the URL before ``/analytics/console/dashboard``.  

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

## What to do next
{: #what-to-do-next}

You can now go to the {{site.data.keyword.mobileanalytics_short}} **Console** to see usage analytics, such as new devices and total devices using your application. You can also monitor your application by <!--[creating custom charts](app-monitoring.html#custom-charts),-->[setting alerts](app-monitoring.html#alerts) and [monitoring app crashes](app-monitoring.html#monitor-app-crash).

# rellinks

## API Reference
{: #api}
* [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}