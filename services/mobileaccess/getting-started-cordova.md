---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-03"

---
{:shortdesc: .shortdesc}

# Setting up the Cordova plug-in
{: #getting-started-cordova}

Instrument your Cordova client application with {{site.data.keyword.amafull}} client SDK. Initialize the Authorization Manager in your Android (Java) or iOS (Objective C) code. Initialize the client, and make requests to protected and unprotected resources from the WebView.

{:shortdesc}

## Before you begin
{: #before-you-begin}
You must have:
* An instance of a  {{site.data.keyword.Bluemix_notm}} application. For more information about how to create a {{site.data.keyword.Bluemix_notm}} back-end application, see [Getting started](index.html).
* An instance of a {{site.data.keyword.amafull}} service.
* The URL of your back-end application (**App Route**). You will need this values for sending requests to the protected endpoints of your back-end application.
* Your **TenantID** value. Open your service in the  {{site.data.keyword.amashort}} dashboard. Click the **Mobile Options** button. The `tenantId` (also known as `appGUID`)  value is displayed in the **App GUID / TenantId** field. You will need this value for intializing the Authorization Manager.
* Your {{site.data.keyword.Bluemix_notm}} **Region**. You can find your current {{site.data.keyword.Bluemix_notm}} region in the header, next to the **Avatar** icon ![Avatar icon](images/face.jpg "Avatar icon"). The region value that appears should be one of the following: `US South`, `United Kingdom`, or `Sydney`, and correspond to the SDK values required in the WebView Javascript code: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY`, or `BMSClient.REGION_UK`. You will need this value for initializing the {{site.data.keyword.amashort}} client.
* A  Cordova application or an existing project. For more information about how to set up your Cordova application, see the [Cordova website](https://cordova.apache.org/).

## Installing the {{site.data.keyword.amashort}} Cordova plug-in
{: #getting-started-cordova-plugin}

The {{site.data.keyword.amashort}} client SDK for Cordova is a Cordova plug-in that wraps the native {{site.data.keyword.amashort}} client SDKs. It is distributed using the Cordova Command Line Interface (CLI) and `npmjs`, a plug-in repository for Cordova projects. The Cordova CLI automatically downloads plug-ins from repositories, and makes them available to your Cordova application.

1. Add Android and/or iOS platforms to your Cordova application. Run one or both of the following commands from the command line:

	###Android
	{: #install-cordova-android}

	```
	cordova platform add android
	```

	###iOS
	{: #install-cordova-ios}

	```Bash
	cordova platform add ios
	```

2. If you added the Android platform, you must add the minimum supported API level to the `config.xml` file of your Cordova application. Open the `config.xml` file, and add the following line to the `<platform name="android">` element:

	```XML
	<platform name="android">  
		<preference name="android-minSdkVersion" value="15"/>
		<preference name="android-targetSdkVersion" value="23"/>
		<!-- add minimum and target Android API level declaration -->
	</platform>
	```

	The *minSdkVersion* value must be `15` or higher. The *targetSdkVersion* value must be the latest Android SDK that is available from Google.

3. If you added the iOS operating system, update the `<platform name="ios">` element with a target declaration:

	```XML
 	  <platform name="ios">
		<preference name="deployment-target" value="8.0"/>
		<!-- add deployment target declaration -->
	 </platform>
	```

4. Install the {{site.data.keyword.amashort}} Cordova plug-in:

 	```Bash
	cordova plugin add bms-core
	```

5. Configure your platform for Android, iOS, or both.

	####Android
	{: #cordova-android}

	Before opening your project in Android Studio, build your Cordova application through your command-line interface (CLI) to avoid build errors.

	```Bash
	cordova build android
	```

	####iOS
	{: #cordova-ios}

	Configure your Xcode project as follows.

	1. Use the most recent version of Xcode to open your `xcode.proj` file in the `<app_name>/platforms/ios` directory.

		**Important:** If you receive a message to convert to the latest Swift syntax, click **Cancel**.

	4. Build and run your application with Xcode.

	**Note**: You may receive the following error when running `cordova build ios`. This issue is due to a bug in a dependency plugin which is being tracked in [Issue 12](https://github.com/blakgeek/cordova-plugin-cocoapods-support/issues/12). You can still run the iOS project in XCode through a simulator or device.

	```
	xcodebuild: error: Unable to find a destination matching the provided destination specifier:
			{ platform:iOS Simulator }

		Missing required device specifier option.
		The device type “iOS Simulator” requires that either “name” or “id” be specified.
		Please supply either “name” or “id”.
	```
6. Verify that the plug-in installed successfully by running the following command:

	```Bash
	cordova plugin list
	```
7. Enable Keychain Sharing for iOS.

  Enable **Keychain Sharing** by going to the  **Capabilities** tab and switch the **Keychain Sharing** to `On`.


## Initializing the {{site.data.keyword.amashort}} client in the Cordova WebView (Javascript)
{: #getting-started-cordova-initialize}

To use the {{site.data.keyword.amashort}} client SDK, you must initialize the SDK by passing the `applicationBluemixRegion`.

Add the following call to your `index.js` file to initialize the {{site.data.keyword.amashort}} client SDK.

```JavaScript
BMSClient.initialize(<applicationBluemixRegion>);
```

**NB:** Replace `<applicationBluemixRegion>` with the region where your {{site.data.keyword.Bluemix_notm}} service is hosted, see  [Before you begin](#before-you-begin).

##Initializing the {{site.data.keyword.amashort}} AuthorizationManager from your native code
{: #initializing-auth-manager}

In order to use `BMSAuthorizationManager` you will need to add the following code snippet. The following native code initializes the `BMSAuthorizationManager` with the {{site.data.keyword.amashort}} service `tenantId` (see [Before you begin](#before-you-begin)).

### Android (Java)

In the `OnCreate` method in the `MainActivity.java` file add the code before `loadUrl`.
```Java
MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),"<tenantId>");
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
```
### iOS (Objective C)
Add the Authorization Manager initialization in the `AppDelegate.m` according to your version of Xcode.

```Objective-C
  [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"]; 
```


## Making a request to the mobile back-end service
{: #getting-started-request}

After the {{site.data.keyword.amashort}} client SDK is initialized, you can start making requests to your mobile back-end service.

1. Try to send a request to a protected endpoint of your mobile back-end application. In your browser, open the following URL: `{applicationRoute}/protected` (for example: `http://my-mobile-backend.mybluemix.net/protected`).

	The `/protected` endpoint of a mobile back-end application that was created with MobileFirst Services Starter boilerplate is protected with {{site.data.keyword.amashort}}. An `Unauthorized` message is returned in your browser. This message is returned because this endpoint is accessed only by mobile applications that are instrumented with {{site.data.keyword.amashort}} client SDK.

2. Use your Cordova application to make a request to the same endpoint. Add the following code after you initialize `BMSClient`:

	```Javascript
	var success = function(data){
	 console.log("success", data);
	 }

	 var failure = function(error){
	 console.log("failure", error);
	 }

	 var request = new BMSRequest("<your route>/protected", BMSRequest.GET);

	 request.send(success, failure);
	```

3. When your request succeeds, you will see the following output in the LogCat or Xcode console (depending on the platform that you are using):

	![image](images/getting-started-android-success.png)

	## Next steps
	{: #next-steps}

	When you connected to the protected endpoint, no credentials were required. To require your users to log in to your application, you must configure Facebook, Google, or custom authentication.
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [Custom](custom-auth-cordova.html)
