---

copyright:
  years: 2015, 2016
  
---

# Enabling Google authentication in Android apps
{: #google-auth-android}

## Before you begin
{: #before-you-begin}

* You must have a resource that is protected by {{site.data.keyword.amashort}} and an Android project that is instrumented with {{site.data.keyword.amashort}} Client SDK.  For more information, see [Getting started with {{site.data.keyword.amashort}}](https://www.{DomainName}/docs/services/mobileaccess/getting-started.html) and [Setting up the Android SDK](https://www.{DomainName}/docs/services/mobileaccess/getting-started-android.html).  
* Manually protect your backend application with {{site.data.keyword.amashort}} Server SDK. For more information, see [Protecting resources](https://www.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

## Configuring a Google project for the Android Platform
{: #google-auth-android-project}
To start using Google as an identity provider, create a project in the Google Developer Console. Part of creating a project is to obtain a Google client ID.  The client ID is a unique identifier for your application.

1. Create a project in [Google Developer Console](https://console.developers.google.com).
If you already have a project, you can skip the steps that describe project creation and start with adding credentials.

1. Create a project. Click **Create project**.

1. Select your project and click **Use Google APIs** (you can also click **Enable APIs and get credentials like keys**)

1. In the API list, choose Google+ API and click **Enable API**.

1. Click **Credentials** in the menu.

1. Click **New credentials** and select **OAuth 2.0 client ID**.

1. Set a product name on the **OAuth consent screen** tab.

1. Select an application type. Click **Android**. Provide a meaningful name for your Android client.

1. For Google to verify your application authenticity, you must specify a signing certificate fingerprint.

	 **More about Android security:** The Android OS requires all applications that are installed on an Android device to be signed with a Developer certificate. An Android application can be built in two modes: debug and release. It is usually advised to have different certificates for debug and release modes.  Certificates that are used for signing Android applications in debug mode are bundled with Android SDK.  The Android SDK is usually installed automatically by Android Studio. When you want to release your application to Google Play, you must sign the app with another certificate, which you usually generate yourself. For more information, see [signing your Android applications](http://developer.android.com/tools/publishing/app-signing.html).

1. A keystore that contains a certificate for development environments is stored in a `~/.android/debug.keystore` file. The default keystore password is `android`. This certificate is used to build applications in debug mode.

1. Retrieve your signing certificate fingerprint:

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore -list -v
	```
	You can use same syntax for retrieving the key hash of your release mode certificate as well. Replace the alias and keystore path in the command.

1. Find the line that starts with `SHA1` under **Certificate Fingerprints**. Copy the fingerprint that was obtained by running the **keytool** command to the Google Developer Console.

1. Specify the package name of your Android application. To find the package name of your Android application, open the `AndroidManifest.xml` file in Android Studio and look for: `<manifest package="{your-package-name}">`. When you are done, click **Create**.

1. Take a note of your new Android Client ID. You need to provide this value to {{site.data.keyword.Bluemix}}.


## Configuring {{site.data.keyword.amashort}} for Google authentication
{: #google-auth-android-config}

Now that you have an Android Client ID, you can enable Google authentication in the {{site.data.keyword.amashort}} Dashboard.

1. Open your app in the {{site.data.keyword.Bluemix_notm}} dashboard.

1. Click **Mobile Options** and take note of your **Route** (`applicationRoute`) and **App GUID** (`applicationGUID`). You need these values when you initialize the SDK.

1. Click the {{site.data.keyword.amashort}} tile. The {{site.data.keyword.amashort}} dashboard loads.

1. Click the **Google** tile.

1. In **Application ID for Android**, specify your Android Client ID for Android and click **Save**.

## Configuring {{site.data.keyword.amashort}} Client SDK for Android
{: #google-auth-android-sdk}

1. Return to Android Studio.

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

	You can remove the dependency on the `core` module of the `com.ibm.mobilefirstplatform.clientsdk.android` group if you have it. The `googleauthentication` module downloads it automatically for you. The `googleauthentication` module downloads and installs the Google SDK in your Android project.

1. Synchronize your project with Gradle by clicking **Tools > Android > Sync Project with Gradle Files**.

1. Open the `AndroidManifest.xml` file of your Android project.

1. Add internet access permission under the `<manifest>` element:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	```

1. To use the {{site.data.keyword.amashort}} Client SDK, you must initialize it by passing the context, applicationGUID, and applicationRoute parameters.

	A common, though not mandatory, place to put the initialization code is in the onCreate method of the main activity in your Android application

1. Initialize the Client SDK and register the Google authentication manager. Replace the `applicationRoute` and `applicationGUID` with the values from **Route** and **App GUID** from the **Mobile Options** section in the dashboard.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");

	GoogleAuthenticationManager.getInstance().register(this);
	```

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
After the Client SDK is initialized and the Google Authentication Manager is registered, you can start making requests to your mobile backend.

### Before you begin
{: #google-auth-android-testing-before}
You must have a mobile backend that was created with the MobileFirst Services Starter boilerplate and already have a resource protected by {{site.data.keyword.amashort}} at the `/protected` endpoint. For more information, see [Protecting resources](https://www.{DomainName}/docs/services/mobileaccess/protecting-resources.html)

1. Try to send a request to the protected endpoint of your mobile backend in your desktop browser by opening `{applicationRoute}/protected`, for example: `http://my-mobile-backend.mybluemix.net/protected`.
 The `/protected` endpoint of a mobile backend created with MobileFirst Services Boilerplate is protected with {{site.data.keyword.amashort}}. Therefore, it can only be accessed by mobile applications that are instrumented with the {{site.data.keyword.amashort}} Client SDK. As a result, you will see `Unauthorized` in your desktop browser.

1. Use your Android application to make request to the same endpoint. Add the following code after you initialize the `BMSClient` instance and register `GoogleAuthenticationManager`.

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

1. Run your application. A Google Login screen pops up:

	![image](images/android-google-login.png)

	Depending on your Android device and whether you're currently logged in to Google you might have a different UI.

1. By clicking **OK**, you are authorizing {{site.data.keyword.amashort}} to use your Google user identity for authentication purposes.

1. 	After your request succeeds, you can see the following output in the LogCat tool:

	![image](images/android-google-login-success.png)
