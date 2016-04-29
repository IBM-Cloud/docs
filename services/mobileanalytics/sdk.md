---

copyright:
  years: 2015, 2016

---

# Instrumenting your application to use the {{site.data.keyword.mobileanalytics_short}} client SDKs
{: #mobileanalytics_sdk}
*Last updated: 27 April 2016*

The {{site.data.keyword.mobileanalytics_full}} SDKs enable you to instrument your mobile application.
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}} enables you to collect three categories of data, and each requires a different degree of instrumentation:

1.  Pre-defined data - This category includes generic usage and device information that applies to all apps. Within this category is device metadata (operating system and device model) and usage data (active users and app sessions) that indicates the volume, frequency, or duration of app use. Pre-defined data is collected automatically after you initialize the {{site.data.keyword.mobileanalytics_short}} SDK in your app.
2. Custom events - This category includes data that you define yourself and that is specific to your app. This data represents events that occur within your app, such as page views, button taps, or in-app purchases. In addition to initializing the {{site.data.keyword.mobileanalytics_short}} SDK in your app, you must add a line of code for each custom event that you want to track.
3. Client log messages - This category enables the developer to add lines of code throughout the app that log custom messages to assist in development and debugging. The developer assigns a severity/verbosity level to each log message and can subsequently filter messages by assigned level or preserve storage space by configuring the app ignore messages below a given level. To collect client log data, you must initialize the {{site.data.keyword.mobileanalytics_short}} SDK within your app, as well as add a line of code for each log message.

Currently SDKs are available for Android, iOS and WatchOS (Swift).

## Identifying your Client Key value
{: #analytics-clientkey}

Identify your **Client Key** value before you set up the client SDK. The Client Key is required for initializing the client SDK.
1. Open your {{site.data.keyword.mobileanalytics_short}} service dashboard.
2. Click the wrench icon to open the API Keys tab.
3. In the API Keys tab, note the Client Key value.


## Initializing your Android app to collect analytics
{: #initalize-ma-sdk-android}

Initialize your application to enable sending logs to the {{site.data.keyword.mobileanalytics_short}} service.

1. Import the Client SDK by adding the following `import` statement to the top of your project file:

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
  ```
  {: codeblock}

2. Initialize the {{site.data.keyword.mobileanalytics_short}} Client SDK in your Android application by adding the initialization code in the `onCreate` method of the main activity in your Android application, or in a location that works best for your project.

	```Java
	try {
            BMSClient.getInstance().initialize(this.getApplicationContext(), "", "", BMSClient.REGION_US_SOUTH); // Make sure you are pointing to your region
            BMSClient.getInstance().setDefaultProtocol(BMSClient.HTTP_SCHEME);
        } catch (MalformedURLException e) {
            Log.e("your_app_name","URL should not be malformed:  " + e.getLocalizedMessage());
        } 
  ```
  {: codeblock}

  To use the {{site.data.keyword.mobileanalytics_short}} Client SDK, you must initialize the `BMSClient` with the **bluemixRegionSuffix** parameter. In the initializer, the **bluemixRegionSuffix** value specifies which {{site.data.keyword.Bluemix_notm}} deployment you are using, for example, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK`, or `BMSClient.REGION_SYDNEY`.
  <!-- Set this value with a `BMSClient.REGION` static property. -->

  <!--You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. Initialize Analytics by using your Android application object and giving it your application’s name. You also need the [**Client Key**](#analytics-clientkey) value.
	
	```Java
	Analytics.init(getApplication(), "my_app", apiKey, Analytics.DeviceEvent.LIFECYCLE);
	// In this code example, Analytics is configured to record lifecycle events.
	```
  {: codeblock}

	**Tip:** The application name is used as a filter to search for client logs in the dashboard. When you use the same application name across platforms (for example, Android and iOS), you can see all logs from that application under the same name, regardless of which platform the logs were sent from.

## Initializing your iOS app to collect analytics
{: #init-ma-sdk-ios}

Initialize your application to enable sending logs to the {{site.data.keyword.mobileanalytics_short}} service. The Swift SDK is available for iOS and watchOS.

1. Import the `BMSCore` and `BMSAnalytics` frameworks by adding the following `import` statements to the top of your `AppDelegate.swift` project file:

  ```Swift
  import BMSCore
  import BMSAnalytics
  ```
  {: screen}

2. To use the {{site.data.keyword.mobileanalytics_short}} Client SDK, you must first initialize the `BMSClient` class, using the following code.

  Place the initialization code in the `application(_:didFinishLaunchingWithOptions:)` method of your application delegate, or in a location that works best for your project.

    ```Swift
    BMSClient.sharedInstance.initializeWithBluemixAppRoute(nil, bluemixAppGUID: nil, bluemixRegion: BMSClient.REGION_US_SOUTH)`
    ```
    {: codeblock}

    To use the {{site.data.keyword.mobileanalytics_short}} Client SDK, you must initialize the `BMSClient` with the **bluemixRegionSuffix** parameter. In the initializer, the **bluemixRegionSuffix** value specifies which {{site.data.keyword.Bluemix_notm}} deployment you are using, for example, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK`, or `BMSClient.REGION_SYDNEY`.
   
   <!-- Set this value with a `BMSClient.REGION` static property. -->

   <!-- You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. Initialize Analytics by giving it your mobile application’s name. You also need the [**Client Key**](#analytics-clientkey) value.

  The application name is used as a filter to search for client logs in your {{site.data.keyword.mobileanalytics_short}} Dashboard. By using the same application name across platforms (for example, Android and iOS), you can see all logs from that application under the same name, regardless of which platform the logs were sent from.

  An optional `deviceEvents` parameter automatically gathers analytics for device-level events. The `deviceEvents` parameter is available for **iOS only**.

  ### iOS
    {: #ios-initialize-analytics}

      ```
      Analytics.initializeWithAppName("AppName", apiKey: "your_client_key",
      deviceEvents: DeviceEvent.LIFECYCLE)
      ```

  ### watchOS
  {: #watchos-initialize-analytics}

	```
	  Analytics.initializeWithAppName("AppName", apiKey: "your_api_key")
	```

  Add the following line to the `applicationDidBecomeActive()` method of the ExtensionDelegate class.

  **Attention:** The `deviceEvents` parameter equivalent on watchOS is `ExtensionDelegate`.

	```
	Analytics.recordApplicationDidBecomeActive()
	```
  {: codeblock}

  Add the following line to applicationWillResignActive() method of the ExtensionDelegate class:
	```
	Analytics.recordApplicationWillResignActive()
	```
  {: codeblock}

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
	
Analytics.log(eventJSONObject);
	
// Send recorded usage analytics to the Mobile Analytics Service
Analytics.send();
```
	
Sample usage analytics for logging an event:
	
```
// Log a custom analytics event for custom charts, which is represented by a JSON object:
JSONObject eventJSONObject = new JSONObject();
	
eventJSONObject.put("customProperty" , "propertyValue");
```

#### iOS - Swift
{: #ios-usage-api}

```
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.enabled = false

// Enable recording of usage analytics
Analytics.enabled = true

// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service
Analytics.send()
```

Sample usage analytics for logging an event:

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

**Note:** Make sure that you have instrumented your app to use the [{{site.data.keyword.mobileanalytics_short}} Client SDK](sdk.html) before using the logging framework.
 
  The following code snippets show sample Logger usage:

#### Android
{: #android-logger-sample}

```
// Configure Logger to save logs to the device so that they 
// can later be sent to the {{site.data.keyword.mobileanalytics_short}} service
// Disabled by default; set to true to enable
Logger.storeLogs(true);

// Change the minimum log level (optional)
// The default setting is Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);

// Send logs to the {{site.data.keyword.mobileanalytics_short}} Service
Logger.send();
```

Logger scenarios:

```
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
```

#### iOS - Swift
{: ios-logger-sample}

```
// Configure Logger to save logs to the device so that they can later be sent to the {{site.data.keyword.mobileanalytics_short}} service
// Disabled by default; set to true to enable
Logger.logStoreEnabled = true

// Change the minimum log level (optional)
// The default setting is LogLevel.Debug
Logger.logLevelFilter = LogLevel.Info

// Send logs to the {{site.data.keyword.mobileanalytics_short}} Service
Logger.send()
```

Logger scenarios:
    
```
// Create two logger instances
// You can create multiple log instances to organize your logs
let logger1 = Logger.logger(forName: "feature1Logger")
let logger2 = Logger.logger(forName: "feature2Logger")
	
// Log messages with different levels
logger1.debug("debug message for feature 1") 
//the logger1.debug message is not logged because the logLevelFilter is set to Info
logger2.info("info message for feature 2")
```

**Tip**: For privacy concerns, you can disable Logger output for applications that are built in release mode. By default, the Logger class prints logs to the Xcode console. In the build settings for your target, add a `-D RELEASE_BUILD` flag to the **Other Swift Flags** section of the release build configuration.
    

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

## Tracking active users
{: #trackingusers}
You can optionally track how many users are actively using your application by passing the user name of the active user to {{site.data.keyword.mobileanalytics_short}}.

#### Android
{: #android-tracking-users}

Add the following code for when the user logs in:

```
Analytics.setUserIdentity("username");
```

Add the following code for when the user logs out:

```
Analytics.clearUserIdentity();
```

#### iOS - Swift
{: #ios-tracking-users}

Add the following code for when the user logs in:

```
Analytics.userIdentity = "username"
```

Add the following code for when the user logs out:

```
Analytics.userIdentity = nil
```

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