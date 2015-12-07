# Getting started with the HelloWorld sample
{: #gettingstarted-cordova}

If you want to get started with a new Cordova application, you can use the HelloWorld app. This app demonstrates how to connect to your Bluemix backend from a mobile app without authentication. The app already has the SDK installed. When you're ready, you can get the specific libraries that you want to use in your app.

1. Create your mobile backend in Bluemix.
<ol><li>In the Boilerplates section Bluemix catalog, click MobileFirst Services Starter.</li>
    <li>Enter a name and host for your app and click **Create**.</li>
    <li>Click **Finish**. </li>
    </ol>
2. Get the project from GitHub. You can optionally use the git clone command to get the project. From your computer, open the terminal and then enter the following command:
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-Cordova-helloworld.git
```
Before you start, download the Gradle.zip file and install Gradle by extracting the downloaded compressed file into the directory of your choice. Android Studio might ask for a GRADLE HOME when you import the sample for the first time. Set that path to the bin directory that is located in the extracted Gradle.zip file. The build.gradle file automatically builds your project by pulling in the required dependencies.

3. Initialize the project.
To initialize the SDK, replace &lt;APPLICATION_ROUTE&gt; and &lt;APPLICATION_ID&gt; with your Application route and GUID in the try block within the BMSClient.getInstance().initialize() function:
```
// initialize SDK with IBM Bluemix application ID and route
BMSClient.getInstance().initialize(this, "<APPLICATION_ROUTE>", "<APPLICATION_ID>");
```
4. Run the sample in your development environment.
From the Android Studio toolbar, click the play button and select a simulator.
In the simulator, click **Ping Bluemix**. The sample app sends a Get request to a protected resource on the Node.js run time on Bluemix. If the request is successful, the connection is verified and the text in the simulator is updated.
Note: The Node.js runtime code is provided in the MobileFirst Services Starter boilerplate. If the backend application was not created with the MobileFirst Services Starter boilerplate, the application will not connect successfully.


![Hello World application successfully connected to Bluemix](images/yayconnected.jpg "Figure 1. Hello World application successfully connected to Bluemix")

When you successfully connect to Bluemix from the mobile app in Android Studio, a message that says "Yay! You are connected" displays.
5. Resolve any problems.

![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")

When the connection fails, a message: "Bummer Something went wrong" displays. More information about the error is included.
Check the following items:
 * Verify that you correctly pasted the route and GUID values.
 * You can also check the debug log for more information.

## Next steps:
{: #next}
For information about how to get the SDK and integrate it into your mobile app, see Setting up the Android client SDK.
