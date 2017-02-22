---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Instrumenting your application to use the {{site.data.keyword.mobileanalytics_short}} client SDKs
{: #mobileanalytics_sdk}

The {{site.data.keyword.mobileanalytics_full}} SDKs enable you to instrument your mobile application.
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}} enables you to collect two <!--three--> categories of data, and each requires a different degree of instrumentation:

1. Pre-defined data - This category includes generic usage and device information that applies to all applications. Within this category is device metadata (operating system and device model) and usage data (active users and application sessions) that indicates the volume, frequency, or duration of application use. Pre-defined data is collected automatically after you initialize the {{site.data.keyword.mobileanalytics_short}} SDK in your application.

2. Application log messages - This category enables the developer to add lines of code throughout the application that log custom messages to assist in development and debugging. The developer assigns a severity/verbosity level to each log message and can subsequently filter messages by assigned level or preserve storage space by configuring the application to ignore messages that are at a lower level of a given log level. To collect application log data, you must initialize the {{site.data.keyword.mobileanalytics_short}} SDK within your application, as well as add a line of code for each log message.

3. Custom events - This category includes data that you define yourself and that is specific to your app. This data represents events that occur within your app, such as page views, button taps, or in-app purchases. In addition to initializing the {{site.data.keyword.mobileanalytics_short}} SDK in your app, you must add a line of code for each custom event that you want to track. 

Currently SDKs are available for Android, iOS, WatchOS, and Cordova.

## Identifying your Service Credentials API Key value
{: #analytics-clientkey}

Identify your **API Key** value before you set up the client SDK. The API Key is required for initializing the client SDK.

1. Open your {{site.data.keyword.mobileanalytics_short}} service dashboard.
2. Expand **View Credentials** to reveal your API Key value. You will need the API Key value when you initialize the {{site.data.keyword.mobileanalytics_short}} Client SDK.


## Initializing your application to collect analytics
{: #initalize-ma-sdk}

Initialize your application to enable sending logs to the {{site.data.keyword.mobileanalytics_short}} service.

1. Import the Client SDK.

	### Android
	{: #android-import notoc}

	Add the following `import` statements to the beginning of your project file:
	
	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
	import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
	import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
	```
	{: codeblock}
  
	### iOS
	{: #ios-import notoc}
	
	**Note:** The Swift SDK is available for iOS and watchOS.
	
	Import the `BMSCore` and `BMSAnalytics` frameworks by adding the following `import` statements to the beginning of your `AppDelegate.swift` project file:

	```Swift
	import BMSCore
	import BMSAnalytics
	```
	{: codeblock}  
   
	### Cordova
	{: #cordova-import notoc}
		
	Add the Cordova plugin by running the following command from your Cordova application root directory:

	```Javascript
	cordova plugin add bms-core
	```
	{: codeblock}  

2. Initialize the {{site.data.keyword.mobileanalytics_short}} Client SDK in your application.

	### Android
	{: #android-init notoc}
	
	Initialize the {{site.data.keyword.mobileanalytics_short}} Client SDK in your Android application by adding the initialization code in the `onCreate` method of the main activity in your Android application, or in a location that works best for your project.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // Make sure that you point to your region
	```
	{: codeblock}

	You must initialize the `BMSClient` with the **bluemixRegion** parameter. In the initializer, the **bluemixRegion** value specifies which {{site.data.keyword.Bluemix_notm}} deployment you are using, for example, `BMSClient.REGION_US_SOUTH` and `BMSClient.REGION_UK`. 
    <!-- , or `BMSClient.REGION_SYDNEY`.--> 
    
	### iOS
	{: #ios-init notoc}
    
	First initialize the `BMSClient` class, using the following code. Place the initialization code in the `application(_:didFinishLaunchingWithOptions:)` method of your application delegate, or in a location that works best for your project.
	
	```Swift 
	BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Make sure that you point to your region
	```
	{: codeblock}

	You must initialize the `BMSClient` with the **bluemixRegion** parameter. In the initializer, the **bluemixRegion** value specifies which {{site.data.keyword.Bluemix_notm}} deployment you are using, for example, `BMSClient.Region.usSouth` or `BMSClient.Region.unitedKingdom`.
    <!-- , or `BMSClient.Region.Sydney`. -->
    
	### Cordova
	{: #cordova-init notoc}
    
	Initialize **BMSClient** and **BMSAnalytics**. You will need your [**API Key**](#analytics-clientkey) value.

	```Javascript
	var applicationName = "HelloWorld";
	var apiKey =  "your_api_key_here";
	var hasUserContext = true;
	var deviceEvents = [BMSAnalytics.ALL];

	BMSClient.initialize(BMSClient.REGION_US_SOUTH); //Make sure you point to your region	
	BMSAnalytics.initialize(applicationName, apiKey, hasUserContext, deviceEvents)
	```
	{: codeblock}

	To use the {{site.data.keyword.mobileanalytics_short}} Client SDK, you must initialize the `BMSClient` with the **bluemixRegion** parameter. In the initializer, the **bluemixRegion** value specifies which {{site.data.keyword.Bluemix_notm}} deployment you are using, for example, `BMSClient.REGION_US_SOUTH` or `BMSClient.REGION_UK`.
    <!-- , or `BMSClient.REGION_SYDNEY`. -->
    
3. Initialize Analytics by using your application object and giving it your application’s name. 

	The name that you select for your application (`your_app_name_here`) displays in the {{site.data.keyword.mobileanalytics_short}} console as the application name. The application name is used as a filter to search for application logs in the dashboard. When you use the same application name across platforms (for example, Android and iOS), you can see all logs from that application under the same name, regardless of which platform the logs were sent from.

	You also need the [**API Key**](#analytics-clientkey) value.

	### Android
	{: #android-init-analytics notoc}
	
	```Java
	
	// In this code example, Analytics is configured to record lifecycle events.
	Analytics.init(getApplication(), "your_app_name_here", apiKey, hasUserContext, Analytics.DeviceEvent.ALL);
	```
	{: codeblock}
	
	**Note:** Set the value for `hasUserContext` to **true** or **false**. If false (default value), each device is counted as an active user. The [`Analytics.setUserIdentity("username")`](sdk.html#android-tracking-users) method, which enables you to track the number of users per device who are actively using your application, will not work when `hasUserContext` is false. If true, each use of [`Analytics.setUserIdentity("username")`](sdk.html#android-tracking-users) counts as an active user. There is no default user identity when `hasUserContext` is true, and therefore must be set to populate the active user charts.
	
	### iOS
	{: #ios-initialize-analytics notoc}
	
	```Swift 
	Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: .lifecycle, .network)
	```
	{: codeblock}
 	
	### watchOS
	{: #watchos-initialize-analytics notoc}
	 	
	```Swift
	Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", deviceEvents: .network)
	```
	{: codeblock}
 	
	An optional `deviceEvents` parameter automatically gathers analytics for device-level events.
	
	**Note:** Set the value for `hasUserContext` to **true** or **false**. If false (default value), each device is counted as an active user. The [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) method, which enables you to track the number of users per device who are actively using your application, will not work when `hasUserContext` is false. If `hasUserContext` is true, each use of [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) counts as an active user. There is no default user identity when `hasUserContext` is true, and therefore must be set to populate the active user charts.

	#### watchOS
	{: #watchos-record-device notoc}

	You can record device events on WatchOS by using the `Analytics.recordApplicationDidBecomeActive()` and `Analytics.recordApplicationWillResignActive()` methods.
  
	Add the following line to the `applicationDidBecomeActive()` method of the ExtensionDelegate class:
 
	```
	Analytics.recordApplicationDidBecomeActive()
	```
	{: codeblock}

	Add the following line to the `applicationWillResignActive()` method of the ExtensionDelegate class:
 
	```
	Analytics.recordApplicationWillResignActive()
	```
	{: codeblock}	
		
4. You've now initialized your application to collect analytics. Next, you can [send analytics data](sdk.html#app-monitoring-gathering-analytics) to the {{site.data.keyword.mobileanalytics_short}} service.


## Gathering usage analytics
{: #app-monitoring-gathering-analytics}

You can configure the {{site.data.keyword.mobileanalytics_short}} Client SDK to record usage analytics and send the recorded data to the {{site.data.keyword.mobileanalytics_short}} service.

Use the following APIs to start recording and sending usage analytics:


### Android
{: #android-usage-api notoc}
	
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
	
Sample usage analytics for logging an event:
	
```
// Log a custom analytics event
JSONObject eventJSONObject = new JSONObject();
	
eventJSONObject.put("customProperty" , "propertyValue");

Analytics.log(eventJSONObject);
```
{: codeblock}


### iOS - Swift
{: #ios-usage-api notoc}

```
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.isEnabled = false

// Enable recording of usage analytics
Analytics.isEnabled = true

// Send recorded usage analytics to the Mobile Analytics Service
Analytics.send(completionHandler: { (response: Response?, error: Error?) in

    if let response = response {
        // Handle Analytics send success here.
    }
    if let error = error {
        // Handle Analytics send failure here.
    }
})
```
{: codeblock}

Sample usage analytics for logging an event:

```Swift
// Log a custom analytics event
let eventObject = ["customProperty": "propertyValue"]
Analytics.log(metadata: eventObject)
```
{: codeblock}

### Cordova
{: #usage-analytics-cordova notoc}

```JavaScript
// Enable usage analytics recording
BMSAnalytics.enable();
  
// Disable usage analytics recording
BMSAnalytics.disable();

// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service
BMSAnalytics.send(
	function(response) {
		console.log('success: ' + response);
	},
	function (err) {
		console.log('fail: ' + err);
	});
```
{: codeblock}

Sample usage analytics for logging an event:

```JavaScript
// Log a custom analytics event
var eventObject = {"customProperty": "propertyValue"}
BMSAnalytics.log(eventObject)
```
{: codeblock}

**Note:** When you are developing Cordova applications, use the native API to enable application lifecycle event recording.
  
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


### Log level scenario
{: #log-level-scenario notoc}

When the logger level is configured to `FATAL`, the logger captures uncaught exceptions, but does not capture any logs that lead up to the crash event. You can set a more verbose logger level to ensure that logs that might lead to a `FATAL` logger entry, such as `WARN` and `ERROR`, are also captured.

When the logger level is set `DEBUG`, you also get Mobile Analytics Client SDK logs, which are included when you send logs.

<!-- **Note:** Find full Logger API references for each platform at [SDKs, samples, API reference](sdks-samples-apis.html). The Logger API is part of the--> <!--{{site.data.keyword.mobileanalytics_short}} Client SDK Core. -->


### Sample Logger usage
{: #sample-logger-usage notoc}

**Note:** Make sure that you have instrumented your application to use the {{site.data.keyword.mobileanalytics_short}} Client SDK before you use the logging framework.
 
The following code snippets show sample Logger usage:


#### Android
{: #android-logger-sample notoc}

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
{: #ios-logger-sample-swift2 notoc}

```
// Configure Logger to save logs to the device so that they 
// can later be sent to the Mobile Analytics service
// Disabled by default; set to true to enable
Logger.isLogStorageEnabled = true

// Change the minimum log level (optional)
// The default setting is LogLevel.debug
Logger.logLevelFilter = LogLevel.info

// Create two logger instances
// You can create multiple log instances to organize your logs
let logger1 = Logger.logger(name: "feature1Logger")
let logger2 = Logger.logger(name: "feature2Logger")

// Log messages with different levels
logger1.debug(message: "debug message for feature 1") 
// The logger1.debug message is not logged because the 
// logLevelFilter is set to info
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
    

#### Cordova
{: #enable-logger-sample-cordova notoc}

```
// Enable persisting logs
BMSLogger.storeLogs(true);

// Set the minimum log level to be printed and persisted
BMSLogger.setLogLevel(BMSLogger.INFO);

var logger1 = BMSLogger.getLogger("logger1");
var logger2 = BMSLogger.getLogger("logger2");   

// Log messages with different levels
logger1.debug ("debug message");
logger2.info ("info message");

// Send persisted logs to the {{site.data.keyword.mobileanalytics_short}} Service
BMSLogger.send();
BMSAnalytics.send();
```
{: codeblock}


<!--## Enabling the {{site.data.keyword.mobileanalytics_short}} Client SDK internal logs
{: #enable-logger-sdklogs notoc}

The {{site.data.keyword.mobileanalytics_short}} Client SDK provides a better development experience by not unnecessarily increasing the console output with its internal debug messages. Therefore, by default, internal log messages that are produced by the {{site.data.keyword.mobileanalytics_short}} SDK with the DEBUG level are not printed. You can enable printing of all internal log messages of the {{site.data.keyword.mobileanalytics_short}} Client SDK with the following API:

#### Android
{: #enable-logger-print-android notoc}

```
{: codeblock}
Logger.setSDKDebugLoggingEnabled(true);
```
{: codeblock}

#### iOS - Swift
{: #enable-logger-print-swift notoc}

```
Logger.sdkDebugLoggingEnabled = true
```
{: codeblock}
-->

## Making a network request
{: #network-requests}

You can configure the {{site.data.keyword.mobileanalytics_short}} Client SDK to [make a network request](/docs/mobile/sdk_network_request.html). Be sure that you have already initialized `BMSClient` and `BMSAnalytics` and imported the Client SDKs.

<!--
#### Android
{: #android-network-requests notoc}

**Note:** This code snippet assumes that you have [imported the Client SDKs](#android-import).

```
public void makeGetCall(){
    Thread thread = new Thread(new Runnable() {
        @Override
        public void run() {
            try  {
                Request request = new Request("http://httpbin.org/get", "GET");
                    request.send(null, null);
            } catch (Exception e) {
                // Handle failure here.
            }
        }
    });
    thread.start();
}
```
{: codeblock}

-->

<!-- 
#### Swift 3.0
{: #ios-network-requests notoc}

 ```Swift
 	// Make a network request
	let customResourceURL = "<your resource URL>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
   	if error == nil {
       	    print ("response:\(response?.responseText), no error")
    	  } else {
       	    print ("error: \(error)")
    	}
	}
	request.send(completionHandler: callBack)
 ```
 {: codeblock}
 
 -->

<!-- Commenting out bmsurlsession
```
// Make a network request
let urlSession = BMSURLSession(configuration: .default, delegate: nil, delegateQueue: nil)
var request = URLRequest(url: URL(string: "http://httpbin.org/get")!)
request.httpMethod = "GET"
request.allHTTPHeaderFields = ["foo":"bar"]

urlSession.dataTask(with: request) { (data: Data?, response: URLResponse?, error: Error?) in
    if let httpResponse = response as? HTTPURLResponse {
        logger.info(message: "Status code: \(httpResponse.statusCode)")
    }
    if data != nil, let responseString = String(data: data!, encoding: .utf8) {
        logger.info(message: "Response data: \(responseString)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
}.resume()
```
{: codeblock}
-->

<!--
#### Swift 2.2
{: ios-swift22-network-requests}

```Swift
 	// Make a network request
	let customResourceURL = "<your resource URL>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: NSError?) in
   	if error == nil {
       	    print ("response:\(response?.responseText), no error")
    	  } else {
       	    print ("error: \(error)")
    	}
	}
	request.send(completionHandler: callBack)
 ```
 {: codeblock}
-->
<!--
```
// Make a network request
let urlSession = BMSURLSession(configuration: .defaultSessionConfiguration(), delegate: nil, delegateQueue: nil)
let request = NSMutableURLRequest(URL: NSURL(string: "http://httpbin.org/get")!)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = ["foo":"bar"]

urlSession.dataTaskWithRequest(request) { (data: NSData?, response: NSURLResponse?, error: NSError?) in
    if let httpResponse = response as? NSHTTPURLResponse {
        logger.info(message: "Status code: \(httpResponse.statusCode)")
    }
    if data != nil, let responseString = NSString(data: data!, encoding: NSUTF8StringEncoding) {
        logger.info(message: "Response data: \(responseString)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
}.resume()
```
{: codeblock}
-->
<!--
#### Cordova
{: #cordova-network-requests notoc}

```
var success = function(data){
     console.log("success", data);
 }
 var failure = function(error)
     {console.log("failure", error);
 }
 var request = new BMSRequest("<your application route>", BMSRequest.GET);
 request.send(success, failure);
```
{: codeblock}

-->


## Reporting crash analytics
{: #report-crash-analytics}

You can see [application crash data](app-monitoring.html#monitor-app-crash) by sending analytics and log information to {{site.data.keyword.mobileanalytics_short}}.

The `Analytics.send()` method populates the **Crash Overview** and **Crashes** tables on the **Crashes** page. Charts in this section are enabled by using the initialization and sending process for analytics; no special configuration is necessary.

The `Logger.send()` method populates the the **Crash Summary** and **Crash Details** tables on the **Troubleshooting** page. You must enable your application to store and send logs to populate the charts in this section, by adding an additional statement in your application code:


### Android
{: #android-crash-statement notoc}

* `Logger.storeLogs(true);`
<!-- * `Logger.setLogLevel(Logger.LEVEL.FATAL); // or greater` -->

See [sample logger usage](sdk.html#android-logger-sample).


### iOS
{: #ios-crash-statement notoc}

* `Logger.isLogStorageEnabled = true`
<!-- * `Logger.logLevelFilter = LogLevel.Fatal // or greater` -->

See [sample logger usage](sdk.html##ios-logger-sample-swift2).


### Cordova
{: #cordova-crash-statement notoc}

* `BMSLogger.storeLogs(true);`
<!-- * `Logger.logLevelFilter = LogLevel.Fatal // or greater` -->

See [sample logger usage](sdk.html##ios-logger-sample-swift2).


## Tracking active users
{: #trackingusers}

If your application can recognize unique users on a device, you can optionally track how many users are actively using your application by passing the user name of the active user to {{site.data.keyword.mobileanalytics_short}}. 

Enable user tracking by initializing {{site.data.keyword.mobileanalytics_short}} with `hasUserContext=true`. Otherwise, {{site.data.keyword.mobileanalytics_short}} captures only one user per device. 


### Android
{: #android-tracking-users notoc}

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

### iOS - Swift
{: #ios-tracking-users notoc}

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


### Cordova
{: #cordova-tracking-users notoc}

Add the following code to track when the user logs in:

```
BMSAnalytics.setUserIdentity("username");
```
{: codeblock}


<!--## Configuring MobileFirst Platform Foundation servers to use the {{site.data.keyword.mobileanalytics_short}} service (optional)
{: #configmfp notoc}
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
    {: #mfp70 notoc}

        The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/data?tenant=<Client API Key>`
        {: screen}

        The `wl.analytics.console.url` JNDI property is the Analytics service dashboard URL.

        #### Example of MobileFirst Platform V7.0 JNDI property values
        {: #example-mfp70-jndi-values notoc}

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
    {: #mfp71 notoc}

      The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`
      {: screen}

      #### Example of MobileFirst Platform JNDI V7.1 property values
      {: #example-mfp71-jndi-values notoc}

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
      {: #mfp80 notoc}

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
{: #ignored-events notoc}
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
{: #what-to-do-next notoc}

You can now go to the {{site.data.keyword.mobileanalytics_short}} Console to see usage analytics, such as new devices and total devices using your application. You can also monitor your application by <!--[creating custom charts](app-monitoring.html#custom-charts),-->[setting alerts](app-monitoring.html#alerts) and [monitoring app crashes](app-monitoring.html#monitor-app-crash).


# Related Links
{: #rellinks notoc}

## API Reference
{: #api notoc}

* [REST API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}