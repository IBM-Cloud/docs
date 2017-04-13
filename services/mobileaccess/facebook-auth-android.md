---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**Important: The {{site.data.keyword.amafull}} service is replaced with the {{site.data.keyword.appid_full}} service.**

# Enabling Facebook authentication for Android apps
{: #facebook-auth-android}

To use Facebook as identity provider in your {{site.data.keyword.amafull}} Android client applications, add and configure the Android client to access your Facebook application on the Facebook for Developers site.
{:shortdesc}

## Before you begin
{: #before-you-begin}

You must have:

* An instance of an {{site.data.keyword.amafull}} service and {{site.data.keyword.Bluemix_notm}} application. For more information about how to create a {{site.data.keyword.Bluemix_notm}} back-end application, see [Getting started](index.html).
* The URL of your back-end application (**App Route**). You will need this value for sending requests to the protected endpoints of your back-end application.
* Your **TenantID** value. Open your service in the  {{site.data.keyword.amashort}} dashboard. Click the **Mobile Options** button. The `tenantId` (also known as `appGUID`)  value is displayed in the **App GUID / TenantId** field. You will need this value for intializing the Authorization Manager.
* Your {{site.data.keyword.Bluemix_notm}} **Region**. You can find your current {{site.data.keyword.Bluemix_notm}} region in the header, next to the **Avatar** icon ![Avatar icon](images/face.jpg "Avatar icon"). The region value that appears should be one of the following: `US South`, `United Kingdom`, or `Sydney`, and correspond to the SDK value required in the WebView Javascript code: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY`, or `BMSClient.REGION_UK`. You will need this value for initializing the {{site.data.keyword.amashort}} client.
* An Android project that is configured to work with Gradle. The project does not need to be instrumented with {{site.data.keyword.amashort}} client SDK.  
* A Facebook app with an Android platform on the [Facebook for Developers site ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developers.facebook.com/){: new_window} .

**Important:** You do not need to separately install the Facebook SDK (`com.facebook.FacebookSdk`). The Facebook SDK is installed automatically by Gradle when you add the {{site.data.keyword.amashort}} Facebook client SDK. You can skip this step when you add the Android platform in the Facebook for Developers site.

## Configuring the application on the Facebook  for Developers site
{: #facebook-auth-android-config}

From the Facebook for Developers website:

1. Log in to your account on the [Facebook for Developers website ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developers.facebook.com){: new_window}.

1. From the **Products List**, choose **Facebook Login**.

1. Add or configure the Android platform.

1. Specify the package name of your Android application in the Google Play Package Name prompt. To find the package name of your Android application look for `<manifest ..... package="{your-package-name}">` in  the `AndroidManifest.xml` file in Android Studio project.

1. Specify the class name of your main activity in the **Class Name** prompt. The class name is the value of the `android:name` property in the activity enclosure. If there is more than one activity in the  `AndroidManifest.xml` file, look for the activity  that contains the `<intent-filter>`:

	```XML
	<activity
		android:name=".MainActivity"
		android:label="@string/app_name">
		<intent-filter>
			<action android:name="android.intent.action.MAIN"/>
			<category android:name="android.intent.category.LAUNCHER"/>
		</intent-filter>
	</activity>
	```
	{: codeblock}

1. For Facebook to ensure your application authenticity, you must specify a hash of your developer certificate SHA1.

	**More about Android security:** The Android OS requires that all applications installed on an Android device are signed with a developer certificate. The Android application can be built in two modes: debug and release.

	Use different certificates for debug and release modes.  Certificates that are used for signing Android applications in debug mode are bundled with Android SDK, which is usually installed automatically by Android Studio. When you want to release your app to the Google Play store, you must sign your app with another certificate that you usually generate yourself.

	You can enter two sets of key hashes with Facebook: one key hash for applications that are built in debug mode with a debug certificate, and another key hash for applications that are built in release mode with a release certificate. For more information, see [signing your Android applications ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://developer.android.com/tools/publishing/app-signing.html){: new_window}.

1. The keystore that contains the certificate you are using for the development environment is stored in the `~/.android/debug.keystore` file. The default keystore password is: `android`. Use this certificate to build applications in debug mode.

1. Retrieve the key hash of your debug mode certificate:

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore | openssl sha1 -binary | openssl base64
	```
	{: codeblock}

	**Tip**: You can use the same syntax for retrieving the key hash of your release mode certificate. Replace the alias and keystore path in the command.

1. Copy and paste the key hash that you obtained with the **keytool** command to a Development/Release Key Hashes prompt in the Facebook for Developers site.

	**Tip**: Consider enabling single sign on if you're planning to use this feature.

1. Click **Save Settings**.

## Configuring the {{site.data.keyword.amashort}} service for Facebook authentication
{: #facebook-auth-android-mca}

After you have the Facebook Application ID and you have configured your Facebook Application to serve Android clients, you can enable Facebook authentication with the {{site.data.keyword.amashort}} dashboard.

1. Open your  {{site.data.keyword.amashort}} service in the dashboard.
1. From the **Manage** tab, toggle **Authorization** on.
1. Expand the **Facebook** section.
1. Add the **Facebook Application ID**.
1. Click **Save**.

## Configuring {{site.data.keyword.amashort}} client Android SDK for Facebook authentication
{: #facebook-auth-android-sdk}

To configure the client SDK for Android, use the Gradle dependency manager in Android Studio.

1.  Open the `build.gradle` file of your app module.
Your Android project might have two `build.gradle` files:  for the project and application module. Use the application module file.

1. Find the dependencies section of the `build.gradle` file and add a new compile dependency for client SDK:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
			name:'facebookauthentication',
			version: '2.+',
			ext: 'aar',
			transitive: true
			// other dependencies  
	}
	```
	{: codeblock}

	**Note:** You can remove the dependency on the `core` module of `com.ibm.mobilefirstplatform.clientsdk.android` group, if it is in your file. The `facebookauthentication` module downloads the `core` module, as well as Facebook's own SDK automatically.

	After you save your updates, the `facebookauthentication` module downloads and installs all necessary SDKs in your Android project.

1. Synchronize your project with Gradle by clicking **Tools > Android > Sync project with Gradle Files**.

1. Open the `res/values/strings.xml` file and add a `facebook_app_id` string that contains your Facebook Application ID:

	```XML
	<resources>
		<string name="app_name">HelloWorld</string>
		<string name="action_settings">Settings</string>
		<string name="facebook_app_id">522733366802111</string>
	</resources>
	```
	{: codeblock}

1. In the `AndroidManifest.xml` file of your Android project:
	* Add the internet access permission under the `<manifest>` element:

		```XML
		<uses-permission android:name="android.permission.INTERNET" />
		```
		{: codeblock}

	* Add required metadata for the Facebook SDK to the `<application>` element:

		```XML
		<application .......>

			<meta-data
				android:name="com.facebook.sdk.ApplicationId"
				android:value="@string/facebook_app_id"/>

			<activity ...../>
			<activity ...../>
		</application>
		```
		{: codeblock}

	* Add a Facebook Activity element under your existing activities:

		```XML
		<application .....>
			<activity ...../>
			<activity ...../>

			<activity android:name="com.facebook.FacebookActivity"
				android:configChanges="keyboard|keyboardHidden|screenLayout|screenSize|orientation"
				android:theme="@android:style/Theme.Translucent.NoTitleBar"
				android:label="@string/app_name" />
		</application>
		```
		{: codeblock}

1. Initialize the client SDK and register the authentication manager. Initialize the {{site.data.keyword.amashort}} client SDK by passing the **context** and **region**.

	A common, though not mandatory, place to put the initialization code is in the `onCreate` method of the main activity in your Android application.<br/>

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

	BMSClient.getInstance().setAuthorizationManager(
		MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));

	FacebookAuthenticationManager.getInstance().register(this);
	```
	{: codeblock}

   * Replace `BMSClient.REGION_UK` with the appropriate region.
   * Replace `<MCAServiceTenantId>` with the `tenantId` value

	For more information on obtaining these values see  [Before you begin](#before-you-begin)).

	**Note:** If your Android application is targeting Android version 6.0 (API level 23) or higher, you must ensure that the application has an `android.permission.GET_ACCOUNTS` call before calling `register`. For more information, see the [this topic ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.android.com/training/permissions/requesting.html){: new_window} on the Android Developers site.

1. Add the following code to your Activity:

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}


## Testing the authentication
{: #testing_auth}

After the client SDK is initialized and Facebook Authentication Manager is registered, you can start making requests to your mobile backend.

### Before you begin testing
{: #facebook-auth-android-testing-before}

You must be using the {{site.data.keyword.mobilefirstbp}} boilerplate and already have a resource that is protected by {{site.data.keyword.amashort}} at the `/protected` endpoint. If you need to set up a `/protected` endpoint, see [Protecting resources](protecting-resources.html).

1. Try to send a request to a protected endpoint of your newly created mobile back-end application in your browser. Open the following URL:

	`{applicationRoute}/protected`. For example: `http://my-mobile-backend.mybluemix.net/protected`.  

	The `/protected` endpoint of a mobile back-end application that was created with MobileFirst Services Starter boilerplate is protected with {{site.data.keyword.amashort}}. An `Unauthorized` message is returned in your browser. This message is returned because this endpoint can only be accessed by mobile applications that are instrumented with {{site.data.keyword.amashort}} client SDK.

1. Use your Android application to make request to the same endpoint. Add the following code after you initialize `BMSClient` and register `FacebookAuthenticationManager`.

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
	{: codeblock}

1. Run your application. A Facebook login screen displays.

	![image](images/android-facebook-login.png)

	This screen might look slightly different if you do not have the Facebook app installed on your device, or if you are not currently logged in to Facebook.

1. Click **OK** to authorize {{site.data.keyword.amashort}} to use your Facebook user identity for authentication purposes.

1. When your request succeeds, the following output is in the LogCat utility:

	![image](images/android-facebook-login-success.png)

	You can also add logout functionality by adding the following code:

	```
	FacebookAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
	```
	{: codeblock}

	If you call this code after a user is logged in with Facebook, the user is logged out of Facebook. When the user tries to log in again, they are prompted for their Facebook credentials.

	The value for `listener` passed to the logout function can be `null`.
