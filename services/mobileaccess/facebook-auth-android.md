---

copyright:
  years: 2015, 2016

---

# Enabling Facebook authentication in Android apps
{: #facebook-auth-android}
To use Facebook as identity provider in your Android applications, add and configure the Android Platform for your Facebook application.

## Before you begin
{: #facebook-auth-android-before}
 * You must have a resource that is protected by {{site.data.keyword.amashort}} and an Android project that is instrumented with {{site.data.keyword.amashort}} client SDK.  For more information, see [Getting started with {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) and [Setting up the Android SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-android.html).  
 * Manually protect your backend application with {{site.data.keyword.amashort}} server SDK. For more information, see [Protecting resources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).
 * Create a Facebook Application ID. For more information, see [Obtaining a Facebook application ID from the Facebook Developer Portal](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).


## Configuring a Facebook application for the Android Platform
{: #facebook-auth-android-config}
To use Facebook as identity provider in your Android applications, you must add and configure the Android platform for your Facebook application.

1. Open your Facebook application in the Facebook Developer Portal.

1. Click **Settings &gt; Add Platform &gt; Android**.

1. Specify the package name of your Android application in the Google Play Package Name prompt. To find the package name of your Android application, open the `AndroidManifest.xml` files in Android Studio and look for `<manifest ..... package="{your-package-name}">`.

1. Specify the class name of your main activity in the **Class Name** prompt. To find the main activity class name of your Android application open the `AndroidManifest.xml` file and look for activity declaration with intent filter similar to the following code snippet:

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

1. For Facebook to ensure your application authenticity, you must specify a hash of your developer certificate SHA1.

	**More about Android security:** The Android OS requires that all applications installed on an Android device are signed with a developer certificate. The Android application can be built in two modes: debug and release. <br/>
  Use different certificates for debug and release modes.  Certificates that are used for signing Android applications in debug mode are bundled with Android SDK, which is usually installed automatically by Android Studio. When you want to release your app to the Google Play store, you must sign your app with another certificate that you usually generate yourself. <br/>You can enter two sets of key hashes with facebook: one key hash for applications that are built in debug mode with a debug certificate, and another key hash for applications that are built in release mode with a release certificate. For more information, see [signing your Android applications](http://developer.android.com/tools/publishing/app-signing.html).

1. The keystore that contains the certificate you are using for the development environment is stored in the `~/.android/debug.keystore` file. The default keystore password is: `android`. Use this certificate to build applications in debug mode.

1. Retrieve the key hash of your debug mode certificate:

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore | openssl sha1 -binary | openssl base64
	```

	**Tip**: You can use same syntax for retrieving the key hash of your release mode certificate. Replace the alias and keystore path in the command.

1. Copy and paste the key hash that you obtained with the **keytool** command to a Development/Release Key Hashes prompt in the Facebook Developer Portal.

	**Tip**: Consider enabling single sign on if you're planning to use this feature.

1. Click **Save Settings**.

## Configuring {{site.data.keyword.amashort}} for Facebook authentication
{: #facebook-auth-android-mca}
After you have Facebook Application ID and you configured you Facebook Application to serve Android clients, you can enable Facebook authentication in the {{site.data.keyword.amashort}} dashboard.

1. Open your app in the {{site.data.keyword.Bluemix_notm}} dashboard.

1. Click **Mobile Options** and take note of your **Route** (`applicationRoute`) and **App GUID** (`applicationGUID`). You need these values when you initialize the SDK.

1. Click the {{site.data.keyword.amashort}} tile. The {{site.data.keyword.amashort}} dashboard loads.

1. Click the **Facebook** tile.

1. Specify the Facebook Application ID and click **Save**.

## Configuring {{site.data.keyword.amashort}}  client SDK for Android
{: #facebook-auth-android-sdk}
To configure the client SDK for Android, use the Gradle dependency manager in Android Studio.

1.  Open the `build.gradle` file of your app module.
You Android project might have two `build.gradle` files:  for the project and application module. Use the application module file.

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

	You can remove the dependency on the `core` module of `com.ibm.mobilefirstplatform.clientsdk.android` group, if it is in your file. The `facebookauthentication` module downloads the `core` module automatically.

  After you save your updates, the `facebookauthentication` module downloads and installs Facebook SDK in your Android project.


1. Synchronize your project with Gradle. Click **Tools > Android > Sync project with Gradle Files**.

1. Open the `res/values/strings.xml` file and add a `facebook_app_id` string that contains your Facebook Application ID:

	```XML
	<resources>
		<string name="app_name">HelloWorld</string>
		<string name="action_settings">Settings</string>
		<string name="facebook_app_id">522733366802111</string>
	</resources>
```

1. In the `AndroidManifest.xml` file of your Android project:
   1. Add the internet access permission under the `<manifest>` element:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```
  2. Add required metadata for the Facebook SDK to the `<application>` element:

	```XML
	<application .......>

		<meta-data
			android:name="com.facebook.sdk.ApplicationId"
			android:value="@string/facebook_app_id"/>

		<activity ...../>
		<activity ...../>
	</application>
```

   1. Add a Facebook Activity element under your existing activities:

	```XML
	<application .....>
		<activity ...../>
		<activity ...../>

		<activity 	android:name="com.facebook.FacebookActivity"
					android:configChanges=
						"keyboard|keyboardHidden|screenLayout|screenSize|orientation"
					android:theme="@android:style/Theme.Translucent.NoTitleBar"
					android:label="@string/app_name" />

	</application>
```

1. Initialize the client SDK and register Facebook authentication manager. Initialize the {{site.data.keyword.amashort}} client SDK by passing the context, app GUID (`applicationGUID`), and route (`applicationRoute`) parameters.<br/>
 A common, though not mandatory, place to put the initialization code is in the `onCreate` method of the main activity in your Android application.<br/>
 Replace *applicationRoute* and *applicationGUID* with values for **Route** and **App GUID** from the **Mobile Options** menu on the main page of your app in the Bluemix dashboard.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");

	FacebookAuthenticationManager.getInstance().register(this);
```


1. Add the following code to your Activity:

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
```

## Testing the authentication
After the client SDK is initialized and Facebook Authentication Manager is registered,you can start making requests to your mobile backend.

### Before you begin
{: #facebook-auth-android-testing-before}
You must be using the {{site.data.keyword.mobilefirstbp}} boilerplate and already have a resource protected by {{site.data.keyword.amashort}} at the `/protected` endpoint. If you need to set up a `/protected` endpoint, see [Protecting resources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Try to send a request to protected endpoint of your newly created mobile backend in your browser. Open the following URL: `{applicationRoute}/protected`. For example: `http://my-mobile-backend.mybluemix.net/protected`
<br/>The `/protected` endpoint of a mobile backend that was created with MobileFirst Services Starter boilerplate is protected with {{site.data.keyword.amashort}}. An `Unauthorized` message is returned in your browser. This message is returned because this endpoint can only be accessed by mobile applications that are instrumented with {{site.data.keyword.amashort}} client SDK.

1. Use your Android application to make request to the same endpoint. Add the following code after you initialize `BMSClient` and register `FacebookAuthenticationManager`.

	```Java
	Request request = new Request("/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp", AuthorizationManager.getInstance().getUserIdentity().toString());
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

1. Run your application. A Facebook login screen displays.

	![image](images/android-facebook-login.png)

	This screen might look slightly different if you do not have the Facebook app installed on your device, or if you are not currently logged in to Facebook.

1. Click **OK** to authorize {{site.data.keyword.amashort}} to use your Facebook user identity for authentication purposes.

1. 	When your request succeeds, the following output is in the LogCat utility:

	![image](images/android-facebook-login-success.png)

 You can also add logout functionality by adding the following code:

 ```
FacebookAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 If you call this code after a user is logged in with Facebook, the user is logged out of Facebook. When the user tries to log in again, they are prompted for their Facebook credentials.

 The value for `listener` passed to the logout function can be `null`.
