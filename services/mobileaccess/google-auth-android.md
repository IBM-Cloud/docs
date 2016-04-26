---

copyright:
  years: 2015, 2016

---

# Enabling Google authentication in Android apps
{: #google-auth-android}

## Before you begin
{: #before-you-begin}

* You must have a resource that is protected by {{site.data.keyword.amashort}} and an Android project that is instrumented with {{site.data.keyword.amashort}} client SDK.  For more information, see [Getting started with {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) and [Setting up the Android SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-android.html).  
* Manually protect your backend application with {{site.data.keyword.amashort}} server SDK. For more information, see [Protecting resources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

## Configuring a Google project for the Android Platform
{: #google-auth-android-project}
To start using Google as an identity provider, create a project in the Google Developer Console. Part of creating a project is to obtain a Google client ID.  The Google client ID is a unique identifier for your application used by Google authentication.

1. Create a project in [Google Developer Console](https://console.developers.google.com).
If you already have a project, you can skip the steps that describe project creation and start with adding credentials.
   1.    Open the new project menu.

         ![image](images/FindProject.jpg)

   2.    Click **Create a project**.

         ![image](images/CreateAProject.jpg)


   1. From the **Social APIs** list, choose **Google+ API**.

     ![image](images/chooseGooglePlus.jpg)

   1. Click **Enable** from the next screen.

1. Select the **Consent Screen** tab and provide  the Product name shown to users. Other values are optional. Click **Save**.

    ![image](images/consentScreen.png)

1. From the **Credentials** list, choose OAuth client ID.

     ![image](images/chooseCredentials.png)



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

A dialog appears that displays your Google client id. Take note of this value. You need to register this value on {{site.data.keyword.Bluemix}}.


## Configuring {{site.data.keyword.amashort}} for Google authentication
{: #google-auth-android-config}

Now that you have a Google client ID for Android, you can enable Google authentication in the {{site.data.keyword.amashort}} Dashboard.

1. Open your app in the {{site.data.keyword.Bluemix_notm}} dashboard.

1. Click **Mobile Options** and take note of your **Route** (`applicationRoute`) and **App GUID** (`applicationGUID`). You need these values when you initialize the SDK.

1. Click the {{site.data.keyword.amashort}} tile. The {{site.data.keyword.amashort}} dashboard loads.

1. Click the **Google** tile.

1. In **Application ID for Android**, specify your Google client ID for Android and click **Save**.

## Configuring {{site.data.keyword.amashort}} client SDK for Android
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

1. To use the {{site.data.keyword.amashort}} client SDK, you must initialize it by passing the context, applicationGUID, and applicationRoute parameters.

	A common, though not mandatory, place to put the initialization code is in the onCreate method of the main activity in your Android application

1. Initialize the client SDK and register the Google authentication manager. Replace *applicationRoute* and *applicationGUID* with the values from **Route** and **App GUID** from the **Mobile Options** section in the dashboard.

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
After the client SDK is initialized and the Google Authentication Manager is registered, you can start making requests to your mobile backend.

### Before you begin
{: #google-auth-android-testing-before}
You must have a mobile backend that was created with the MobileFirst Services Starter boilerplate and already have a resource protected by {{site.data.keyword.amashort}} at the `/protected` endpoint. For more information, see [Protecting resources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)

1. Try to send a request to the protected endpoint of your mobile backend in your desktop browser by opening `{applicationRoute}/protected`, for example: `http://my-mobile-backend.mybluemix.net/protected`.
 The `/protected` endpoint of a mobile backend created with MobileFirst Services Boilerplate is protected with {{site.data.keyword.amashort}}. Therefore, it can only be accessed by mobile applications that are instrumented with the {{site.data.keyword.amashort}} client SDK. As a result, you will see `Unauthorized` in your desktop browser.

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

1. Run your application. A Google Login screen pops up. After login, the app requests permission to access resources:

	![image](images/android-google-login.png)

	Depending on your Android device and whether you're currently logged in to Google you might have a different UI.

  By clicking **OK**, you are authorizing {{site.data.keyword.amashort}} to use your Google user identity for authentication purposes.

1. 	After your request succeeds, you can see the following output in the LogCat tool:

	![image](images/android-google-login-success.png)

 You can also add logout functionality by adding the following code:

 ```Java
 GoogleAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 If you call this code after a user is logged in with Google, the user is logged out of Google. When the user tries to log in again, they must select a Google account under which they will be logged in again. When they try to log in with a previous logged in Google ID, the user is not prompted for their credentials again. To be prompted for login credentials again, the user must remove their Google account from the Android device.

 The value for `listener` passed to the logout function can be `null`.
