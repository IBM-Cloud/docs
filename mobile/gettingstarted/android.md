---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Getting started with the Hello Bluemix for Android sample
{: #gettingstarted-android}
*Last Updated: 27 May 2016*
{: .last-updated}  

If you want to get started with a new Android application, you can use the HelloWorld app. This app demonstrates how to connect to your {{site.data.keyword.Bluemix}} backend from a mobile app without authentication. The app already has the SDK installed. When you're ready, you can get the specific libraries that you want to use in your app.

1. Create your mobile backend in {{site.data.keyword.Bluemix_notm}}.
    1. In the Boilerplates section of the {{site.data.keyword.Bluemix_notm}} catalog, click MobileFirst Services Starter.
    2. Enter a name and host for your app and click **Create**.
    3. Click **Finish**.
2. Get the project from GitHub. You can optionally use the git clone command to get the project. From your computer, open the terminal and then enter the following command:
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld.git
    ```

3. Initialize the project by replacing &lt;APPLICATION_ROUTE&gt; and &lt;APPLICATION_ID&gt; with your Application route and GUID in the `try` block within the `BMSClient.getInstance().initialize()` function:
```
// initialize SDK with IBM Bluemix application ID and route
BMSClient.getInstance().initialize(this, "<APPLICATION_ROUTE>", "<APPLICATION_ID>");
```
4. Run the sample in your development environment.
From the Android Studio toolbar, click the **Play** button and select a simulator.
5. In the simulator, click **Ping {{site.data.keyword.Bluemix_notm}}**. The sample app sends a Get request to the `Node.js` runtime on {{site.data.keyword.Bluemix_notm}}. If the request is successful, the connection is verified and the text in the simulator is updated.

  **Note:** The `Node.js` runtime code is provided in the MobileFirst Services Starter boilerplate. If the backend application was not created with the MobileFirst Services Starter boilerplate, the application will not connect successfully.

  When you successfully connect to {{site.data.keyword.Bluemix_notm}} from the mobile app in Android Studio, the following message displays:

  `Yay! You are connected`
  {: screen}

  ![Hello World application successfully connected to {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figure 1. Hello World application successfully connected to Bluemix")

  If the connection fails, you see:
  `Bummer. Something went wrong`
  {: screen}

  ![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")

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
   * [Hello Bluemix sample (Android)](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld)

## sdk
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [Core API](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
