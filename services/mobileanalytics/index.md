---

copyright:
  years: 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Getting started with {{site.data.keyword.mobileanalytics_short}} (Beta)  

{: #gettingstartedtemplate}
Last updated: 12 September 2016
{: .last-updated}

{{site.data.keyword.mobileanalytics_full}} provides developers, IT administrators, and business stakeholders insight into how their mobile apps are performing and how they are being used. Monitor performance and usage of all your applications from your desktop or tablet. Quickly identify trends and anomalies, drill down to resolve issues, and trigger alerts when key metrics cross critical thresholds. 
{: shortdesc}

To get up and running quickly with the {{site.data.keyword.mobileanalytics_short}} service, follow these steps:

1. After you create an instance <!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->of the {{site.data.keyword.mobileanalytics_short}} service, you can access the {{site.data.keyword.mobileanalytics_short}} Console by clicking your tile in the **Services** section of the {{site.data.keyword.Bluemix}} Dashboard.

2. Install the {{site.data.keyword.mobileanalytics_short}} [Client SDKs](install-client-sdk.html). You can optionally use the {{site.data.keyword.mobileanalytics_short}} [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}.

3. Import the Client SDKs and initialize them with the following code snippet to record usage analytics.

	#### Android
	{: #android-initialize}
	1. Import the Client SDK:

		```
		import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
		import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
		```
		{: codeblock}
		
	2. Initialize the Client SDK inside your application code to record usage analytics and application sessions, using your [API Key](sdk.html#analytics-clientkey) value.

		```Java
			BMSClient.getInstance().initialize(this.getApplicationContext(), BMSClient.REGION_US_SOUTH); // You can change the region
			
			Analytics.init(getApplication(), your_app_name_here, your_api_key_here, hasUserContext, Analytics.DeviceEvent.LIFECYCLE);
		```
		{: codeblock}
		
    The **bluemixRegion** parameter specifies which Bluemix deployment you are using, for example, `BMSClient.REGION_US_SOUTH` and `BMSClient.REGION_UK`. 
    <!-- , or `BMSClient.REGION_SYDNEY`.-->
    
    **Note:** Set the value for `hasUserContext` to **true** or **false**. If false (default value), each device is counted as an active user. The [`Analytics.setUserIdentity("username");`](sdk.html#android-tracking-users) method will not work when `hasUserContext` is false. If true, each use of [`Analytics.setUserIdentity("username");`](sdk.html#android-tracking-users) counts as an active user. There is no default user identity when`hasUserContext` is true, and therefore must be set to populate the active user charts.

  #### iOS
  {: #ios-initialize}
  
  1. Import the `BMSCore` and `BMSAnalytics` frameworks:
	```
	import BMSCore
	import BMSAnalytics
	```
	{: codeblock}
    
  2. Initialize the Client SDK inside your application code to record usage analytics and application sessions, using your [API Key](sdk.html#analytics-clientkey) value.
 
	Swift 2:
	
	```Swift
	BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.REGION_US_SOUTH) // You can change the region
	Analytics.initializeWithAppName(your_app_name_here, apiKey: your_api_key_here, hasUserContext: false, deviceEvents: DeviceEvent.LIFECYCLE)
	```
	{: codeblock}
	
	Swift 3:
	
	```Swift
	BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.REGION_US_SOUTH) // You can change the region
	Analytics.initializeWithAppName(appName: your_app_name_here, apiKey: your_api_key_here, hasUserContext: false, deviceEvents: DeviceEvent.LIFECYCLE)
	```
	{: codeblock}
	
	The **bluemixRegion** parameter specifies which Bluemix deployment you are using, for example, `BMSClient.REGION_US_SOUTH` and `BMSClient.REGION_UK`.
	<!-- , or `BMSClient.REGION_SYDNEY`. -->
	
	**Note:** Set the value for `hasUserContext` to **true** or **false**. If false (default value), each device is counted as an active user. The [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) method will not work when `hasUserContext` is false. If true, each use of [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) counts as an active user. There is no default user identity when`hasUserContext` is true, and therefore must be set to populate the active user charts.

4. Send recorded usage analytics to the Mobile Analytics Service. A simple way to test your analytics is to run the following code when your application starts:

	#### Android
	{: #android-send}

	You can add the `Analytics.send()` method in the `onCreate` method of the main activity in your Android application, or in a location that works best for your project.

	```
	Analytics.send();
	```
	{: codeblock}

	#### iOS
	{: #ios-send}

	Use the `Analytics.send` method to send analytics data to the server. Place the `Analytics.send` method in the `application(_:didFinishLaunchingWithOptions:)` method of your application delegate, or in a location that works best for your project.

	```
	Analytics.send()
	```
	{: codeblock}

	Read the [Instrumenting your application](sdk.html) topic.
5. Compile and run the application on your emulator or device.

6. Go to the {{site.data.keyword.mobileanalytics_short}} **Dashboard** to see usage analytics, such as new devices and total devices using the application. You can also monitor your app by <!--[creating custom charts](app-monitoring.html#custom-charts),-->[setting alerts](app-monitoring.html#alerts) and [monitoring app crashes](app-monitoring.html#monitor-app-crash).


# rellinks

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## API Reference
{: #api}
* [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
