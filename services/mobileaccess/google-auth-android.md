---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-03"

---
{:screen: .screen}
{:shortdesc: .shortdesc}

# Enabling Google authentication for Android apps
{: #google-auth-android}

Use Google to authenticate users on your {{site.data.keyword.amafull}} Android application. Add {{site.data.keyword.amashort}} security functionality.

## Before you begin
{: #before-you-begin}
You must have:
* An instance of an {{site.data.keyword.amafull}} service and {{site.data.keyword.Bluemix_notm}} application. For more information about how to create a {{site.data.keyword.Bluemix_notm}} back-end application, see [Getting started](index.html).
* The URL of your back-end application (**App Route**). You will need this values for sending requests to the protected endpoints of your back-end application.
* Your **TenantID** value. Open your service in the  {{site.data.keyword.amashort}} dashboard. Click the **Mobile Options** button. The `tenantId` (also known as `appGUID`)  value is displayed in the **App GUID / TenantId** field. You will need this value for intializing the Authorization Manager.
* Your {{site.data.keyword.Bluemix_notm}} **Region**. You can find your current {{site.data.keyword.Bluemix_notm}} region in the header, next to the **Avatar** icon ![Avatar icon](images/face.jpg "Avatar icon"). The region value that appears should be one of the following: `US South`, `United Kingdom`, or `Sydney`, and correspond to the SDK values required in the WebView Javascript code: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY`, or `BMSClient.REGION_UK`. You will need this value for initializing the {{site.data.keyword.amashort}} client.
* An Android project that is configured to work with Gradle. The project does not need to be instrumented with {{site.data.keyword.amashort}} client SDK.  

Setting up Google authentication for your {{site.data.keyword.amashort}}  Android app will require further configuring of:
* The {{site.data.keyword.Bluemix_notm}} application
* Your Android Studio project

## Creating a project on the Google Developer Console
{: #create-google-project}

To start using Google as an identity provider, create a project in the [Google Developer Console](https://console.developers.google.com).
Part of creating a project is to obtain a Google Client ID.  The Google Client ID is a unique identifier for your application used by Google authentication, and is needed for setting up the{{site.data.keyword.amashort}} service.

From the console:

1. Create a project using the **Google+** API.
2. Add the  **OAuth** user access.
3. Before  you add the credentials, you must choose the platform (Android).
4. Add the credentials.

To complete the credentials creation, you need to add the **signing certificate fingerprint**.



### Setting up the signing certificate
For Google to verify your application authenticity, you must specify a signing certificate fingerprint.

The Android OS requires all applications that are installed on an Android device to be signed with a developer certificate. An Android application can be built in two modes: debug and release. It is usually advised to have different certificates for debug and release modes.  Certificates that are used for signing Android applications in debug mode are bundled with Android SDK.  The Android SDK is usually installed automatically by Android Studio. When you want to release your application to Google Play, you must sign the app with another certificate, which you usually generate yourself. For more information, see [signing your Android applications](http://developer.android.com/tools/publishing/app-signing.html).

A keystore that contains a certificate for development environments is stored in a `~/.android/debug.keystore` file. The default keystore password is `android`. This certificate is used to build applications in debug mode.

1. Retrieve your signing certificate fingerprint from your client development environment:

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore -list -v
	```

	You can use same syntax for retrieving the key hash of your release mode certificate as well. Replace the alias and keystore path in the command.

1. In the Google Console Credential dialog, find the line that starts with `SHA1` under **Certificate Fingerprints**. Copy the fingerprint value that was obtained by running the **keytool** command to the text box.

###Package name

1. On the Credentials dialog, enter the package name of your Android application.

  To find the package name of your Android application, open the `AndroidManifest.xml` file in Android Studio and look for:

  	`<manifest package="{your-package-name}">`

1. When you are done, click **Create**. This completes the credentials creation.

###Google Client ID

Once the credentials are successfully created, the credential page displays your Google Client ID. Take note of this value. You need to register this value in the {{site.data.keyword.Bluemix}} application.


## Configuring {{site.data.keyword.amashort}} for Google authentication
{: #google-auth-android-config}

Now that you have a Google Client ID for Android, you can enable Google authentication in the {{site.data.keyword.amashort}} Dashboard.

1. Open your service in the {{site.data.keyword.amashort}} dashboard.
1. From the **Manage** tab, pull the **Authorization** lever to the **On** position.
1. Expand the **Google** section.
1. In **Client ID for Android**, specify your Google Client ID for Android and click **Save**.

## Configuring {{site.data.keyword.amashort}} client SDK for Android
{: #google-auth-android-sdk}

From your Android Studio project.

1. Open the `build.gradle` file of your app module.

	Your Android project might have two `build.gradle` files: one for project and another one for application module. Use the application module.

  Find the dependencies section and add a new compile dependency for client SDK:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'googleauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```
	**Note:** You can remove the dependency on the `core` module of the `com.ibm.mobilefirstplatform.clientsdk.android` group if you have it. The `googleauthentication` module downloads it automatically for you. The `googleauthentication` module downloads and installs the Google+ SDK in your Android project.

1. Synchronize your project with Gradle by clicking **Tools > Android > Sync Project with Gradle Files**.

1. Open the `AndroidManifest.xml` file of your Android project.

1. Add internet access permission under the `<manifest>` element:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	```

1. To use the {{site.data.keyword.amashort}} client SDK, you must initialize it by passing the **context** and the **region** parameters.

	A common, though not mandatory, place to put the initialization code is in the `onCreate` method of the main activity in your Android application.

1. Initialize the client SDK and register the Google authentication manager.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

	BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));

	GoogleAuthenticationManager.getInstance().register(this);
	```

  * Replace  `BMSClient.REGION_UK` with your {{site.data.keyword.Bluemix_notm}} **Region**.
  * Replace `<MCAServiceTenantId>`  with the **TenantId** value.

	For more information on obtaining these values, see [Before you begin](##before-you-begin).

   **Note:** If your Android application is targeting Android version 6.0 (API level 23) or higher, you must ensure that the application has an `android.permission.GET_ACCOUNTS` call before calling `register`. For more information, see [https://developer.android.com/training/permissions/requesting.html](https://developer.android.com/training/permissions/requesting.html){: new_window}.

1. Add the following code to your Activity:

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		GoogleAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```

## Testing the authentication
{: #google-auth-android-test}
After the client SDK is initialized and the Google Authentication Manager is registered, you can start making requests to your back-end application.

Before you begin testing, you must have a mobile back-end application that was created with the **MobileFirst Services Starter** boilerplate, and already have a resource protected by the {{site.data.keyword.amashort}} `/protected` endpoint. For more information, see [Protecting resources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Try to send a request to the protected endpoint of your mobile back-end application in your desktop browser by opening `{applicationRoute}/protected`, for example: `http://my-mobile-backend.mybluemix.net/protected`.  For information on obtaining the `{applicationRoute}` value, see [Before you begin](#before-you-begin).

	The `/protected` endpoint of a mobile back-end application created with MobileFirst Services Boilerplate is protected with {{site.data.keyword.amashort}}. Therefore, it can only be accessed by mobile applications that are instrumented with the {{site.data.keyword.amashort}} client SDK. As a result, you will see `Unauthorized` in your desktop browser.

1. Use your Android application to make request to the same protected endpoint. Add the following code after you initialize the `BMSClient` instance and register `GoogleAuthenticationManager`.

	```Java
	Request request = new Request("{applicationRoute}/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp", MCAAuthorizationManager.getInstance().getUserIdentity().toString());
		}
		@Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
			if (null != t) {
				Log.d("Myapp", "onFailure :: " + t.getMessage());
			} else if (null != extendedInfo) {
				Log.d("Myapp", "onFailure :: " + extendedInfo.toString());
			} else {
				Log.d("Myapp", "onFailure :: " + response.getResponseText());
			}
		}
	});
	```

1. Run your application. A Google Login screen pops up. After login, the app requests permission to access resources:

	![image](images/android-google-login.png)

	Depending on your Android device, and whether you're currently logged in to Google, you might have a different UI.

  By clicking **OK**, you are authorizing {{site.data.keyword.amashort}} to use your Google user identity for authentication purposes.

1. 	After your request succeeds, you can see the following output in the LogCat tool:

	![image](images/android-google-login-success.png)

 You can also add logout functionality by adding the following code:

 ```Java
 GoogleAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 If you call this code after a user is logged in with Google, the user is logged out of Google. When the user tries to log in again, they must select a Google account for logging in again. When they try to log in with a previous logged in Google ID, the user is not prompted for their credentials again. To be prompted for login credentials again, the user must remove their Google account from the Android device.

 The value for `listener` passed to the logout function can be `null`.
