---

copyright:
  years: 2015, 2016
  
---

# Setting up the Cordova plug-in
{: #getting-started-cordova}

Instrument your Cordova application with {{site.data.keyword.amashort}} client SDK, initialize the SDK and make requests to protected and unprotected resources.

## Before you begin
{: #before-you-begin}

- You must have an instance of a mobile backend that is protected by {{site.data.keyword.amashort}} service. For more information about how to create a mobile backend, see [Getting started](getting-started.html).

- Create a Cordova application or use an existing project. For more information about how to set up your Cordova application, see the [Cordova website](https://cordova.apache.org/).

## Installing the {{site.data.keyword.amashort}} Cordova Plug-in
{: #getting-started-cordova-plugin}

The {{site.data.keyword.amashort}} client SDK for Cordova is a Cordova plug-in that is wrapping the native {{site.data.keyword.amashort}} client SDKs. It is distributed using the Cordova Command Line Interface (CLI) and `npmjs`, a plug-in repository for Cordova projects. The Cordova CLI automatically downloads plug-ins from repositories and makes them available to your Cordova application.

1. Add Android and iOS platforms to your Cordova application. Run one or both of the following commands from the command line:

	```Bash
	cordova platform add android
	```

	```Bash
	cordova platform add ios
	```

1. If you added the Android platform, you must add the minimum supported API level to the `config.xml` file of your Cordova application. Open the `config.xml` file and add the following line to the `<platform name="android">` element:

	```XML
	<platform name="android">  
		<preference name="android-minSdkVersion" value="15"/>
		<preference name="android-targetSdkVersion" value="23"/>
		<!-- add minimum and target Android API level declaration -->
	</platform>
	```

	The *minSdkVersion* value must be higher than `15`. The *targetSdkVersion* value must be the latest Android SDK that is available from Google.

1. If you added the iOS operating system, update the `<platform name="ios">` element with a target declaration:

	```XML
	<platform name="ios">
		<preference name="deployment-target" value="8.0"/>
		<!-- add deployment target declaration -->
	</platform>
	```

1. Install the {{site.data.keyword.amashort}} Cordova plug-in:

 	```Bash
	cordova plugin add ibm-mfp-core
	```

1. Configure your platform for Android, iOS or both.

	* **Android**

		Before opening your project in Android Studio, build your Cordova application through your command-line interface (CLI) to avoid build errors.

		```
		cordova build android
		```

	* **iOS**

		Configure your Xcode project as follows, to avoid build errors.

		1. Use the most recent version of Xcode to open your xcode.proj file in the &lt;*app_name*&gt;/platforms/ios directory.

		**Important:** If you receive a message to "Convert to Latest Swift Syntax", click Cancel.

		2. Go to **Build Settings > Swift Compiler - Code Generation > Objective-C Bridging Header** and add the following path:

			```
			<your_project_name>/Plugins/ibm-mfp-core/Bridging-Header.h
			```

		3. Go to **Build settings > Linking > Runpath Search Paths** and add the following Frameworks parameter:

			```
			@executable_path/Frameworks
			```

		4. Build and run your application with Xcode.

1. Verify that the plugin installed successfully by running the following command:

	```Bash
	cordova plugin list
	```

## Initializing the {{site.data.keyword.amashort}} client plug-in
{: #getting-started-cordova-initialize}

To use the {{site.data.keyword.amashort}} client SDK, you must initialize the SDK by passing the *applicationGUID* and *applicationRoute* parameters.

1. Find your route and app GUID values on the main page of the {{site.data.keyword.Bluemix_notm}} dashboard. Click your app name and then **Mobile Options** to display the **Application route** and **Application GUID** values to initialize the SDK.

3. Add the following call to your `index.js` file to initialize the {{site.data.keyword.amashort}} client SDK. Replace the *applicationRoute* and *applicationGUID* with the values from **Mobile Options** in the {{site.data.keyword.Bluemix_notm}} dashboard.

	```JavaScript
	BMSClient.initialize("applicationRoute", "applicationGUID");
	```

## Making a request to the mobile backend
{: #getting-started-request}

After the {{site.data.keyword.amashort}} client SDK is initialized, you can start making requests to your mobile backend.

1. Try to send a request to a protected endpoint of your new mobile backend. In your browser, open the following URL: `{applicationRoute}/protected`. For example:

	```
	http://my-mobile-backend.mybluemix.net/protected
	```

	The `/protected` endpoint of a mobile backend that was created with MobileFirst Services Starter boilerplate is protected with {{site.data.keyword.amashort}}. An `Unauthorized` message is returned in your browser. This message is returned because this endpoint is accessed only by mobile applications that are instrumented with {{site.data.keyword.amashort}} client SDK.

1. Use your Cordova application to make a request to the same endpoint. Add the following code after you initialize `BMSClient`:

	```Javascript
	var success = function(data){
	console.log("success", data);
	}

	var failure = function(error){
	console.log("failure", error);
	}

	var request = new MFPRequest("/protected", MFPRequest.GET);

	request.send(success, failure);
	```

1. When your request succeeds, you will see the following output in the LogCat or Xcode console (depending on the platform that you are using):

	![image](images/getting-started-android-success.png)

	## Next steps
	{: #next-steps}

	When you connected to the protected endpoint, no credentials were required. To require your users to log in to your application, you must configure Facebook, Google, or custom authentication.
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [Custom](custom-auth-cordova.html)
