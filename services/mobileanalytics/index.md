---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-20"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Getting started with {{site.data.keyword.mobileanalytics_short}}

{: #gettingstartedtemplate}

{{site.data.keyword.mobileanalytics_full}} provides developers, IT administrators, and business stakeholders insight into how their mobile apps are performing and how they are being used. {{site.data.keyword.mobileanalytics_short}} enables you to:

* Monitor performance and usage of all your applications from your desktop or tablet. 
* Quickly identify trends and anomalies, drill down to resolve issues, and trigger alerts when key metrics cross critical thresholds. 
{: shortdesc}

To quickly get the {{site.data.keyword.mobileanalytics_short}} service up and running, follow these steps:

1. After you create an instance <!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->of the {{site.data.keyword.mobileanalytics_short}} service, you can access the {{site.data.keyword.mobileanalytics_short}} Console by clicking your tile in the **Services** section of the {{site.data.keyword.Bluemix}} Dashboard.

 To help you get an immediate feel of the various views and charts and the value they bring forth, we provide a **demo mode** option in the {{site.data.keyword.mobileanalytics_short}} console, whereby the views and charts display *demo data*. Demo mode is the default mode of the console when it initially launches after the service is instantiated. When you have your own applications and analytics data populated into the service, you can toggle *off* the demo mode to view your applications' data in the different charts. The {{site.data.keyword.mobileanalytics_short}} console is read-only when in demo mode, therefore you will not be able to create new alert definitions.

2. Install the {{site.data.keyword.mobileanalytics_short}} [Client SDKs](/docs/services/mobileanalytics/install-client-sdk.html). You can optionally use the {{site.data.keyword.mobileanalytics_short}} [REST API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}.

3. Import the Client SDKs and initialize them with the following code snippet to record usage analytics:

	## Android
	{: #android-import notoc}

	Add the following `import` statements to the beginning of your project file:
	
    ```
    import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
    import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
    import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
    ```
	{: codeblock}

	## iOS
	{: #ios-import notoc}
	
	**Note:** The Swift SDK is available for iOS and watchOS.
	
	Import the `BMSCore` and `BMSAnalytics` frameworks by adding the following `import` statements to the beginning of your `AppDelegate.swift` project file:

	```Swift
	import BMSCore
	import BMSAnalytics
	```
	{: codeblock}
   
	## Cordova
	{: #cordova-import notoc}
		
	Add the Cordova plugin by running the following command from your Cordova application root directory:

	```Javascript
	cordova plugin add bms-core
	```
	{: codeblock}  

4. Initialize the {{site.data.keyword.mobileanalytics_short}} Client SDK in your application code to record usage analytics and application sessions, using your [API Key](/docs/services/mobileanalytics/sdk.html#analytics-clientkey) value.	
	
	## Android
	{: #android-initialize notoc}	

	```
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // You can change the region
	Analytics.init(getApplication(), "your_app_name_here", "your_api_key_here", hasUserContext, Analytics.DeviceEvent.ALL);
	```
	{: codeblock}
    
	The **bluemixRegion** parameter specifies which {{site.data.keyword.Bluemix_notm}} deployment you are using, for example, `BMSClient.REGION_US_SOUTH` and `BMSClient.REGION_UK`. 
    <!-- , or `BMSClient.Region.Sydney`.-->
    
	Set the value for `hasUserContext` to **true** or **false**. If false (default value), each device is counted as an active user.

	## iOS
	{: #ios-initialize notoc}
  
	Initialize the Client SDK inside your application code to record usage analytics and application sessions, using your [API Key](/docs/services/mobileanalytics/sdk.html#analytics-clientkey) value.
	
	```Swift
	BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // You can change the region
	Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: deviceEvents: .lifecycle, .network)
	```
	{: codeblock}
			
	The **bluemixRegion** parameter specifies which Bluemix deployment you are using, for example, `BMSClient.Region.usSouth` or `BMSClient.Region.unitedKingdom`.
	<!-- , or `BMSClient.REGION_SYDNEY`. -->
 
	Set the value for `hasUserContext` to **true** or **false**. If false (default value), each device is counted as an active user.
	
	## Cordova
	{: #cordova-initialize notoc}
	
	Initialize the Client SDK inside your application code to record usage analytics and application sessions, using your [API Key](/docs/services/mobileanalytics/sdk.html#analytics-clientkey) value.
	
	```
	var appName = "your_app_name_here";
	var apiKey = "your_api_key_here";
	
	BMSClient.initialize(BMSClient.REGION_US_SOUTH); // You can change the region
	BMSAnalytics.initialize(appName, apiKey, false, [BMSAnalytics.ALL])
	```
	{: codeblock}
  
	The **bluemixRegion** parameter specifies which {{site.data.keyword.Bluemix_notm}} deployment you are using, for example, `BMSClient.REGION_US_SOUTH` and `BMSClient.REGION_UK`.
  
	**Note:** The name that you select for your application (`your_app_name_here`) displays in the {{site.data.keyword.mobileanalytics_short}} console as the application name. The application name is used as a filter to search for application logs in the dashboard. When you use the same application name across platforms (for example, Android and iOS), you can see all logs from that application under the same name, regardless of which platform the logs were sent from.

5. Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service. A simple way to test your analytics is to run the following code when your application starts:

	## Android
	{: #android-send notoc}

	Use the `Analytics.send()` method to send analytics data to the server. You can place the `Analytics.send()` method anywhere in the `onCreate` method of the main activity in your Android application, or in a location that works best for your project. 
	
	You can insert `Analytics.send()` anywhere.

	```
	Analytics.send();
	```
	{: codeblock}

	## iOS
	{: #ios-send notoc}

	Use the `Analytics.send` method to send analytics data to the server. You can place the `Analytics.send` method anywhere in the `application(_:didFinishLaunchingWithOptions:)` method of your application delegate, or in a location that works best for your project. 

	```
	Analytics.send()
	```
	{: codeblock}
	
	## Cordova
	{: #cordova-send notoc}
	
	Use the `BMSAnalytics.send` method to send analytics data to the server. Place the `BMSAnalytics.send` method in a location that works best for your project.
	
	```
	BMSAnalytics.send()
	```
	{: codeblock}
	
	Read the [Instrumenting your application](/docs/services/mobileanalytics/sdk.html) topic to learn about additional {{site.data.keyword.mobileanalytics_short}} capabilities, such as [logging](/docs/services/mobileanalytics/sdk.html#app-monitoring-logger), [network requests](/docs/services/mobileanalytics/sdk.html#network-requests), and [crash analytics](/docs/services/mobileanalytics/sdk.html#report-crash-analytics).
	
6. Compile and run the application on your emulator or device.

7. Go to the {{site.data.keyword.mobileanalytics_short}} Console to see usage analytics for your application. You can also monitor your application by <!--[creating custom charts](app-monitoring.html#custom-charts),-->[setting alerts](/docs/services/mobileanalytics/app-monitoring.html#alerts) and [monitoring app crashes](/docs/services/mobileanalytics/app-monitoring.html#monitor-app-crash).


# Related Links
{: #rellinks notoc}

## SDK
{: #sdk notoc}
* [Android SDK ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [Cordova Plugin Core SDK ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.npmjs.com/package/bms-core){: new_window}

## API Reference
{: #api notoc}
* [REST API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
