---

copyright:
  years: 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Getting started with {{site.data.keyword.mobileanalytics_short}} (Experimental)  

{: #gettingstartedtemplate}
*Last updated: 28 April 2016*

Use the {{site.data.keyword.mobileanalytics_full}} service to measure the state, behavior, and context of your mobile apps, mobile users, and mobile devices.
{: shortdesc}

To get up and running quickly with the {{site.data.keyword.mobileanalytics_short}} service, follow these steps:

1. After you [create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance) of the {{site.data.keyword.mobileanalytics_short}} service, you can access the {{site.data.keyword.mobileanalytics_short}} Console by clicking your tile in the Services section of the {{site.data.keyword.Bluemix}} Dashboard.

  **Important:** When you initially open your newly created Mobile Analytics service, a window displays to confirm that you allow {{site.data.keyword.Bluemix_notm}} to provide necessary information to the service about yourself so the service can validate your identity. Click **Confirm** to continue to the {{site.data.keyword.mobileanalytics_short}} console. If you cancel, the {{site.data.keyword.mobileanalytics_short}} console will not open.
2. Install the {{site.data.keyword.mobileanalytics_short}} [Client SDKs](install-client-sdk.html).
3. Import the Client SDKs and initialize them with the following code snippet to record usage analytics.
  #### Android
  {: #android-initialize}
  1. Import the Client SDK:
		
		```
		import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
		import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
		```

  2. Get your [Client Key](sdk.html#analytics-clientkey) value.
  3. Initialize the Client SDK inside your application code to record usage analytics and application sessions.
		
		```Java
		try {
		        BMSClient.getInstance().initialize(this.getApplicationContext(), "", "", BMSClient.REGION_US_SOUTH);
		    } catch (MalformedURLException e) {
		        Log.e("your_app_name","URL should not be malformed:  " + e.getLocalizedMessage());
		    }
		   Analytics.init(getApplication(), "your_app_name", "your_client_key", Analytics.DeviceEvent.LIFECYCLE);
		```
    The **bluemixRegion** parameter specifies which Bluemix deployment you are using, for example, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK`, or `BMSClient.REGION_SYDNEY`.

  #### iOS
  {: #ios-initialize}
  1. Import the `BMSCore` and `BMSAnalytics` frameworks:

    ```
    import BMSCore
    import BMSAnalytics
    ```

  2. Get your [Client Key](sdk.html#analytics-clientkey) value.

  3. Initialize the Client SDK inside your application code to record usage analytics and application sessions.
	
	```Swift
	BMSClient.sharedInstance.initializeWithBluemixAppRoute("nil",bluemixAppGUID: "nil", bluemixRegion: BMSClient.REGION_US_SOUTH) //You can change the region
	Analytics.initializeWithAppName("your_app_name", apiKey: "your_client_key", deviceEvents: DeviceEvent.LIFECYCLE)
	```

    The **bluemixRegion** parameter specifies which Bluemix deployment you are using, for example,   `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK`, or `BMSClient.REGION_SYDNEY`.

4. Send recorded usage analytics to the Mobile Analytics Service. A simple way to test your analytics is to run the following code when your application starts:

	#### Android
	{: #android-send}
	
	You can add the `Analytics.send()` method in the `onCreate` method of the main activity in your Android application, or in a location that works best for your project.
	
	```
	Analytics.send(new ResponseListener() {
	    @Override
	    public void onSuccess(Response response) {
	        Log.d("your_app_name", "Successfully sent analytics: " + response.toString());
	    }
		
	    @Override
	    public void onFailure(Response response, Throwable throwable, JSONObject jsonObject) {
	        Log.e("your_app_name", "Failed to send analytics: ");
	        if (response != null) {
	            Log.e("your_app_name", response.toString());
	        }
	        if (throwable != null) {
	            Log.e("your_app_name","Stack trace: ", throwable);
	        }
	    }
	});
	```
	
	#### iOS
	{: #ios-send}
	
	
	Use the `Analytics.send` method to send analytics data to the server. Place the `Analytics.send` method in the `application(_:didFinishLaunchingWithOptions:)` method of your application delegate, or in a location that works best for your project. 
		
	```
	Analytics.send { (response: Response?, error: NSError?) in
	  if response?.statusCode == 201 {
	      print("Successfully sent analytics: \(response?.responseText)")
	  }
	  else {
	      print("Failed to send analytics: \(response?.responseText). Error: \(error?.localizedDescription)")
	  }
	}
	```
See the [Instrumenting your application](sdk.html) topic.
5. Compile and run the application on your emulator or device.

6. Go to the {{site.data.keyword.mobileanalytics_short}} **Dashboard** to see usage analytics, such as new devices and total devices using the application. You can also monitor your app by [creating custom charts](app-monitoring.html#custom-charts), [setting alerts](app-monitoring.html#alerts), and [monitoring app crashes](app-monitoring.html#monitor-app-crash). 


# rellinks

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
