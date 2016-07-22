---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Getting started with the Hello Bluemix for iOS sample
{: #gettingstarted-android}
Last Updated: 1 June 2016
{: .last-updated}  

If you want to get started with a new iOS app, you can use the Hello Bluemix app. This app demonstrates how to connect to your {{site.data.keyword.Bluemix}} backend from a mobile app without authentication. When you're ready, you can get the specific libraries that you want to use in your app.

1. Create your mobile backend in {{site.data.keyword.Bluemix_notm}}.
    1. In the Boilerplates section of the {{site.data.keyword.Bluemix_notm}} catalog, click MobileFirst Services Starter.
    2. Enter a name and host for your app and click **Create**.
    3. Click **Finish**.
2. Run the Hello Bluemix sample application:
	1. Get the project from GitHub. You can optionally use the git clone command to get the project. From your computer, open the terminal and then enter the following command:
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix.git
    ```
	2. Run the `pod install` command from within the `bms-samples-swift-hellobluemix` directory, where the project was cloned. If you do not have Cocoapods installed, get it from [https://cocoapods.org](https://cocoapods.org).
	3. Open the Xcode workspace with the `open HelloBluemix.xcworkspace` command.
	4. In your `AppDelegate.swift` file, update the appRoute and appGuid values to those obtained from the Bluemix backend that you created earlier.

3. Run the sample in your development environment. In Xcode, click **Product &gt; Run**. An iOS simulator starts.

	**Important:** Your appRoute must use an `https` protocol and not `http`, or you might get a connection failure, due to the app transport security settings. You can read more about those settings in the [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/) blog post.
	
4. In the simulator, click **Ping {{site.data.keyword.Bluemix_notm}}**. The sample app obtains the authorization header from the Mobile Client Access service. If the ping is successful, the text in the simulator is updated.

  When you successfully connect to {{site.data.keyword.Bluemix_notm}} from the mobile app in Xcode, you see:
  `Yay! You are connected`
  {: screen}

  <!--
  ![Hello World application successfully connected to {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figure 1. Hello World application successfully connected to Bluemix")
-->

  If the connection fails, you see:
  `Bummer. Something went wrong`
  {: screen}

 <!--
  ![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")
  -->

	You can troubleshoot the failed connection as follows:
	* Verify that you correctly pasted the route and GUID values.
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
