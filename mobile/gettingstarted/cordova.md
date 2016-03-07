<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Getting started with the HelloWorld sample
{: #gettingstarted-cordova}
*Last Updated: 2 March 2016*

If you want to get started with a new Cordova application, you can use the HelloWorld app. This app demonstrates how to connect to your mobile backend on {{site.data.keyword.Bluemix}} from a mobile app without authentication. The app already has the SDK installed. When you're ready, you can get the specific libraries that you want to use in your app.

1. Create your mobile backend in {{site.data.keyword.Bluemix_notm}}.

	1. In the Boilerplates section of the {{site.data.keyword.Bluemix_notm}} catalog, click MobileFirst Services Starter.
	1. Enter a name and host for your app and click **Create**.
	1. Click **Finish**.

2. Get the project from GitHub. You can  use the git clone command to get the project. From your computer, open the terminal and then enter the following command:

	```Bash
	git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld
	```

3. Run the following commands from your project directory to add the Android and iOS platform environments:

	Android:

	```Bash
	cordova platform add android
	```

	iOS:

	```Bash
	cordova platform add ios
	```

4. Add the Cordova plug-in with the following command:

	```Bash
	cordova plugin add ibm-mfp-core
	```

5. Configure your Cordova app for Android, iOS or both.

	* **Android**

		Before opening your project in Android Studio, build and run your Cordova application through your command-line interface (CLI) to avoid build errors.

		```Bash
		cordova build android
		```

		```Bash
		cordova run android
		```

	* **iOS**

		Configure your Xcode project as follows, to avoid build errors.

		- Use the most recent version of Xcode to open your `xcode.proj` file in the *&lt;app_name&gt;*/platforms/ios directory.

			**Important:** If you receive a message to "Convert to Latest Swift Syntax", click **Cancel**.

		- Go to **Build Settings > Swift Compiler - Code Generation > Objective-C Bridging Header** and add the following path:

			```
			<your_project_name>/Plugins/ibm-mfp-core/Bridging-Header.h
			```

		- Go to **Build settings > Linking > Runpath Search Paths** and add the following Frameworks parameter:

			```
			@executable_path/Frameworks
			```

		- Build and run your application with Xcode.		
6. Configure the HelloWorld sample.

	- Change to the directory where you cloned the project.
	- Open the *&lt;your_app_dir&gt;*/www/js/index.js file and replace the *&lt;APPLICATION_ROUTE&gt;* and *&lt;APPLICATION_ID&gt;* with your Bluemix application ID and route values.

		**Note:** Make sure that your route is securely using the https protocol.

		```Javascript
		// Bluemix credentials
		route: "<APPLICATION_ROUTE>",
		GUID: "<APPLICATION_GUID>",
		```

7. Run the sample on your mobile emulator or device.

	Build the Cordova app using the following commands:

	```Bash
	cordova build android
	```

	```Bash
	cordova build ios
	```

	Run the sample app using the following commands:

	```Bash
	cordova run android
	```

	```Bash
	cordova run ios
	```

A single view application with a **PING BLUEMIX** button displays. When you tap the button, the application tests the connection from the client to the backend {{site.data.keyword.Bluemix_notm}} application. The connection is tested by using the application route that you specified in the `index.js` file.


![Hello World application successfully connected to Bluemix](images/yayconnected.jpg "Figure 1. Hello World application successfully connected to Bluemix")


When you successfully connect to {{site.data.keyword.Bluemix_notm}} from the mobile app, a message that says "Yay! You are connected" displays.


<!--![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")-->

If the connection fails, an error message displays. More information about the error is included in the message. You can check the following items to troubleshoot your error:

- Verify that you correctly pasted the route and GUID values.
- View the Xcode or Android debug log.
- Check the status of your app in {{site.data.keyword.Bluemix_notm}}.

## Next steps:
{: #next}
For information about how to get the SDK and integrate it into your mobile app, see:
* [Mobile Client Access: Setting up the Cordova plug-in](../services/mobileaccess/getting-started-cordova.html)
* [Push Notifications: Setting up the Cordova plug-in](../mobilepush/enablepush_cordova.html#setup_sdk_cordova)

# rellinks

## samples
   * [HelloWorld (Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld)

## sdk
   * [bms-clientsdk-cordova-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

<!--## api
   * [Core API](https://www.{DomainName}/docs/api/content/api/mobilefirst/cordova/core-api-doc/overview-summary.html)
-->
