---

copyright:
  years: 2016
lastupdated: "2016-10-31"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Getting started with {{site.data.keyword.mobileanalytics_short}} (Beta)

{: #gettingstartedtemplate}

{{site.data.keyword.mobileanalytics_full}} provides developers, IT administrators, and business stakeholders insight into how their mobile apps are performing and how they are being used. Monitor performance and usage of all your applications from your desktop or tablet. Quickly identify trends and anomalies, drill down to resolve issues, and trigger alerts when key metrics cross critical thresholds. 
{: shortdesc}

To get up and running quickly with the {{site.data.keyword.mobileanalytics_short}} service, follow these steps:

1. After you create an instance <!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->of the {{site.data.keyword.mobileanalytics_short}} service, you can access the {{site.data.keyword.mobileanalytics_short}} Console by clicking your tile in the **Services** section of the {{site.data.keyword.Bluemix}} Dashboard.

 The {{site.data.keyword.mobileanalytics_short}} service launches with **demo mode** enabled. Demo mode populates charts on the **APP DATA** and **ALERTS** pages, so you can see how your data will display. You can toggle demo mode off when you have your own data. The {{site.data.keyword.mobileanalytics_short}} console is read-only when in demo mode, therefore you will not be able to create new alert definitions.

2. Install the {{site.data.keyword.mobileanalytics_short}} [Client SDKs](/docs/services/mobileanalytics/install-client-sdk.html). You can optionally use the {{site.data.keyword.mobileanalytics_short}} [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}.

3. Import the Client SDKs and initialize them with the following code snippet to record usage analytics.

	#### Android
	{: #android-initialize}
	
	1. Import the Client SDK:

		```
		import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
		import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
		```
		{: codeblock}
	
	2. Initialize the Client SDK inside your application code to record usage analytics and application sessions, using your [API Key](/docs/services/mobileanalytics/sdk.html#analytics-clientkey) value.

		```Java
		BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // You can change the region
			
		Analytics.init(getApplication(), "your_app_name_here", "your_api_key_here", hasUserContext, Analytics.DeviceEvent.ALL);
		```
		{: codeblock}
		
    	The name that you select for your application (`your_app_name_here`) displays in the {{site.data.keyword.mobileanalytics_short}} console as the application name. The application name is used as a filter to search for application logs in the dashboard. When you use the same application name across platforms (for example, Android and iOS), you can see all logs from that application under the same name, regardless of which platform the logs were sent from.
    
    	The **bluemixRegion** parameter specifies which {{site.data.keyword.Bluemix_notm}} deployment you are using, for example, `BMSClient.REGION_US_SOUTH` and `BMSClient.REGION_UK`. 
    <!-- , or `BMSClient.Region.Sydney`.-->
    
    	**Note:** Set the value for `hasUserContext` to **true** or **false**. If false (default value), each device is counted as an active user. The [`Analytics.setUserIdentity("username");`](/docs/services/mobileanalytics/sdk.html#android-tracking-users) method will not work when `hasUserContext` is false. If true, each use of [`Analytics.setUserIdentity("username");`](/docs/services/mobileanalytics/sdk.html#android-tracking-users) counts as an active user. There is no default user identity when`hasUserContext` is true, and therefore must be set to populate the active user charts.

	#### iOS
	{: #ios-initialize}
  
	1. Import the `BMSCore` and `BMSAnalytics` frameworks:
	
		```
		import BMSCore
		import BMSAnalytics
		```
		{: codeblock}
    
	2. Initialize the Client SDK inside your application code to record usage analytics and application sessions, using your [API Key](/docs/services/mobileanalytics/sdk.html#analytics-clientkey) value.
	
		```Swift
		BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // You can change the region
		Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: deviceEvents: .lifecycle, .network)
		```
		{: codeblock}
		
		The name that you select for your application (`your_app_name_here`) displays in the {{site.data.keyword.mobileanalytics_short}} console as the application name. The application name is used as a filter to search for application logs in the dashboard. When you use the same application name across platforms (for example, Android and iOS), you can see all logs from that application under the same name, regardless of which platform the logs were sent from.
	
		The **bluemixRegion** parameter specifies which Bluemix deployment you are using, for example, `BMSClient.Region.usSouth` or `BMSClient.Region.unitedKingdom`.
	<!-- , or `BMSClient.REGION_SYDNEY`. -->
	
		**Note:** Set the value for `hasUserContext` to **true** or **false**. If false (default value), each device is counted as an active user. The [`Analytics.userIdentity = "username"`](/docs/services/mobileanalytics/sdk.html#ios-tracking-users) method will not work when `hasUserContext` is false. If true, each use of [`Analytics.userIdentity = "username"`](/docs/services/mobileanalytics/sdk.html#ios-tracking-users) counts as an active user. There is no default user identity when`hasUserContext` is true, and therefore must be set to populate the active user charts.
	
	#### Cordova
	{: #cordova-initialize}
	
	Initialize the Client SDK inside your application code to record usage analytics and application sessions, using your [API Key](/docs/services/mobileanalytics/sdk.html#analytics-clientkey) value.
	
		```Javascript
		var appName = "your_app_name_here";
		var apiKey = "your_api_key_here";
		
		BMSClient.initialize(BMSClient.REGION_US_SOUTH);
		BMSAnalytics.initialize(appName, apiKey, false, [BMSAnalytics.ALL])
		```

4. Send recorded usage analytics to the Mobile Analytics Service. A simple way to test your analytics is to run the following code when your application starts:

	#### Android
	{: #android-send}

	Use the `Analytics.send()` method to send analytics data to the server. You can place the `Analytics.send()` method anywhere in the `onCreate` method of the main activity in your Android application, or in a location that works best for your project. 
	
	You can insert `Analytics.send()` anywhere.

	```
	Analytics.send();
	```
	{: codeblock}

	#### iOS
	{: #ios-send}

	Use the `Analytics.send` method to send analytics data to the server. You can place the `Analytics.send` method anywhere in the `application(_:didFinishLaunchingWithOptions:)` method of your application delegate, or in a location that works best for your project. 

	```
	Analytics.send()
	```
	{: codeblock}
	
	#### Cordova
	{: #cordova-send}
	
	Use the `BMSAnalytics.send` method to send analytics data to the server. Place the `BMSAnalytics.send` method in a location that works best for your project.
	
	```
	BMSAnalytics.send
	```
	{: codeblock}
	
	Read the [Instrumenting your application](/docs/services/mobileanalytics/sdk.html) topic to learn about additional {{site.data.keyword.mobileanalytics_short}} capabilities, such as [logging](/docs/services/mobileanalytics/sdk.html#app-monitoring-logger), [network requests](/docs/services/mobileanalytics/sdk.html#network-requests), and [crash analytics](/docs/services/mobileanalytics/sdk.html#report-crash-analytics).
	
5. Compile and run the application on your emulator or device.

6. Go to the {{site.data.keyword.mobileanalytics_short}} Console to see usage analytics for your application. You can also monitor your application by <!--[creating custom charts](app-monitoring.html#custom-charts),-->[setting alerts](/docs/services/mobileanalytics/app-monitoring.html#alerts) and [monitoring app crashes](/docs/services/mobileanalytics/app-monitoring.html#monitor-app-crash).


# rellinks

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [Cordova Plugin Core SDK](https://www.npmjs.com/package/bms-core){: new_window}

## API Reference
{: #api}
* [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
