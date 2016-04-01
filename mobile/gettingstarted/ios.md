<!-- Attribute definitions -->
{:codeblock: .codeblock}
{:screen: .screen}

# Getting started with the HelloWorld sample
{: #gettingstarted-ios}
*Last Updated: 28 January 2016*
If you want to get started with a new iOS app, you can use the HelloWorld app. This app demonstrates how to connect to your {{site.data.keyword.Bluemix}} backend from a mobile app without authentication. The app already has the SDK installed. When you're ready, you can get the specific libraries that you want to use in your app.

1. Create your mobile backend in {{site.data.keyword.Bluemix_notm}}.
<ol>
	<li>In the Boilerplates section of the  {{site.data.keyword.Bluemix_notm}} catalog, click **MobileFirst Services Starter**.</li>
    <li>Enter a name and host for your app and click **Create**.</li>
    <li>Click **Finish**. </li>
</ol>
2. Get the project from GitHub.
From your computer, open the terminal and enter the following command:
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld
```

3. Initialize the project.
To initialize the SDK, copy the following code to the `didFinishLaunchingWithOptions` method in the Application Delegate.
   * Objective-C:
```
// initialize SDK with IBM Bluemix application ID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<insert route>" backendGUID:@"<insertGUID>"];
return YES;
```{: codeblock}
   * Swift:
```
// initialize SDK with IBM Bluemix application ID and route
IMFClient.sharedInstance().initializeWithBackendRoute("<insert route>", backendGUID: "<insertGUID>")
return true
```{: codeblock}

4. Run the sample in your development environment.
In Xcode, click **Product &gt; Run**. An iOS simulator starts.
In the simulator, click **Ping {{site.data.keyword.Bluemix_notm}}**. The sample app obtains the authorization header from the Mobile Client Access service. If the ping is successful, the text in the simulator is updated.
<br/>When you successfully connect to {{site.data.keyword.Bluemix_notm}} from the mobile app in Xcode, a message that says "Yay! You are connected" displays:<br/>
![Hello World application successfully connected to {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figure 1. Hello World application successfully connected to {{site.data.keyword.Bluemix_notm}}")
<br/>
If you connect successfully, the debug login Xcode contains the following message:
```You have connected to {{site.data.keyword.Bluemix_notm}} successfully```
5. Resolve any problems.
When the connection fails, a message "Bummer Something went wrong" displays. More information about the error is included.<br/>
![Hello World application not connected to {{site.data.keyword.Bluemix_notm}}](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")
<br/>Verify that you correctly pasted the route and GUID values:
   * Objective-C:
  ```
  [imfClient initializeWithBackendRoute:@"https://hellotest.mybluemix.net"
  backendGUID:@"9d48d73a-0878-4254-test-bdcbe6c79c31"];
  ``` {: codeblock}
   * Swift:
  ```
  IMFClient.sharedInstance().initializeWithBackendRoute("https://hellotest.mybluemix.net", backendGUID: "9d48d73a-0878-4254-test-bdcbe6c79c31")
  ```{: codeblock}


You can also check the debug log for more information.

## Next steps:
{: #next}
For information about how to get the SDK and integrate it into your mobile app, see the information about setting up the {{site.data.keyword.Bluemix}} services.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# rellinks

## samples
   * [HelloWorld sample](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld)

## sdk
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-ios-core)

## api
   *
[Core API](https://classicdocs.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)
