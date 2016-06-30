---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Getting started with the Hello Bluemix for iOS sample
{: #gettingstarted-android}
*Last Updated: 1 June 2016*
{: .last-updated}  

If you want to get started with a new iOS app, you can use the HelloWorld app. This app demonstrates how to connect to your {{site.data.keyword.Bluemix}} backend from a mobile app without authentication. The app already has the SDK installed. When you're ready, you can get the specific libraries that you want to use in your app.

1. Create your mobile backend in {{site.data.keyword.Bluemix_notm}}.
    1. In the Boilerplates section of the {{site.data.keyword.Bluemix_notm}} catalog, click MobileFirst Services Starter.
    2. Enter a name and host for your app and click **Create**.
    3. Click **Finish**.
2. Get the project from GitHub. You can optionally use the git clone command to get the project. From your computer, open the terminal and then enter the following command:
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld.git
    ```

3. Initialize the project. To initialize the SDK, copy the following code to the `didFinishLaunchingWithOptions` method in the Application Delegate.

	###Ojbective-C
	{: initializeobjc}

	**Important**: While the Objective-C SDK remains fully supported, and is still considered the primary SDK for {{site.data.keyword.Bluemix}} Mobile Services, it is planned to be discontinued later this year in favor of the new Swift SDK.

	The Objective-C SDK reports monitoring data to the Monitoring Console of the {{site.data.keyword.amashort}} service. If you rely on the monitoring functions of the {{site.data.keyword.amashort}} service, continue to use the Objective-C SDK.

	```
	// initialize SDK with IBM Bluemix application ID and route
	IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<insert route>" backendGUID:@"<insertGUID>"];
return YES;
	```

	###Swift
	{: initializeswift}
	```
	// initialize SDK with IBM Bluemix application ID and route
	IMFClient.sharedInstance().initializeWithBackendRoute("<insert route>", backendGUID: "<insertGUID>")
	return true
	```

4. Run the sample in your development environment. In Xcode, click **Product &gt; Run**. An iOS simulator starts.
5. In the simulator, click **Ping {{site.data.keyword.Bluemix_notm}}**. The sample app obtains the authorization header from the Mobile Client Access service. If the ping is successful, the text in the simulator is updated.

  When you successfully connect to {{site.data.keyword.Bluemix_notm}} from the mobile app in Xcode, the following message displays:

  `Yay! You are connected`
  {: screen}

  ![Hello World application successfully connected to {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figure 1. Hello World application successfully connected to Bluemix")

  If the connection fails, you see:
  `Bummer. Something went wrong`
  {: screen}

  ![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")

	You can troubleshoot the failed connection as follows:
	* Verify that you correctly pasted the route and GUID values.
		####Objective-C
		{: #objcvals}
		```
		[imfClient initializeWithBackendRoute:@"https://hellotest.mybluemix.net"
		backendGUID:@"9d48d73a-0878-4254-test-bdcbe6c79c31"];
		```

		####Swift
		{: #swiftvals}
		```
		IMFClient.sharedInstance().initializeWithBackendRoute("https://hellotest.mybluemix.net", backendGUID: "9d48d73a-0878-4254-test-bdcbe6c79c31")
		```

	* Review the debug log for more information.


## Next steps:
{: #next}
For information about how to get the SDK and integrate it into your mobile app, see the information about setting up the Bluemix services.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# rellinks

## samples
   * [Hello Bluemix sample (iOS)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix)

## sdk
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [Core API](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
