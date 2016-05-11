---

copyright:
  years: 2015, 2016

---

# Configuring the {{site.data.keyword.amashort}} client SDK for Android
{: #custom-android}
Configure your Android application that is using custom authentication to use the {{site.data.keyword.amashort}} client SDK and connect your application to {{site.data.keyword.Bluemix}}.

## Before you begin
{: #before-you-begin}
You must have a resource that is protected by an instance of the {{site.data.keyword.amashort}} service that is configured to use a custom identity provider.  Your mobile app also must be instrumented with the {{site.data.keyword.amashort}} client SDK.  For more information, see the following information:
 * [Getting started with {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Setting up Android SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-android.html)
 * [Using a custom identity provider](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Creating a custom identity provider](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configuring {{site.data.keyword.amashort}} for custom authentication](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## Initializing the {{site.data.keyword.amashort}} client SDK
{: #custom-android-initialize}
1. In your Android project in Android Studio, open the `build.gradle` file of your app module.
<br/>**Tip:** Your Android project might have two `build.gradle` files: for the project and for the application module. Use the application module file.

1. In the `build.gradle` file file, find the `dependencies` section and check for the following compile dependency. Add this dependency if it is not already there.

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '1.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```

1. Synchronize your project with Gradle. Click **Tools > Android > Sync Project with Gradle Files**.

1. Open the `AndroidManifest.xml` file of your Android project.
Add the internet access permission under the `<manifest>` element:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```

1. Initialize the SDK.  
A common, though not mandatory, place to put the initialization code is in the `onCreate` method of the main activity in your Android application.
Replace *applicationRoute* and *applicationGUID* with the **Route** and **App GUID** values you get when you click **Mobile Options** in your app on the {{site.data.keyword.Bluemix_notm}} dashboard.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");					
	```

## AuthenticationListener interface
{: #custom-android-authlistener}

The {{site.data.keyword.amashort}} client SDK provides the `AuthenticationListener` interface so that you can implement a custom authentication flow. The `AuthenticationListener` interface exposes three methods that are called on different phases of the authentication process.

### onAuthenticationChallengeReceived method
{: #custom-onAuth}
Call this method when a custom authentication challenge is received from the {{site.data.keyword.amashort}} service.

```Java
void onAuthenticationChallengeReceived(AuthenticationContext authContext, JSONObject challenge, Context context);
```
#### Arguments
{: #custom-android-onAuth-arg}

* `AuthenticationContext`: Provided by {{site.data.keyword.amashort}} client SDK so that you can report back authentication challenge answers or failures during credentials collection.  For example, when a user cancels the authentication.
* `JSONObject`: Contains a custom authentication challenge, as returned by a custom identity provider.
* `Context`: A reference to the Android Context that was used when the request was sent. Usually this argument represents an Android Activity.

By calling the `onAuthenticationChallengeReceived` method, the {{site.data.keyword.amashort}} client SDK is delegating control to the developer.  The service waits for credentials. The developer must collect credentials and report them back to the {{site.data.keyword.amashort}} client SDK by using one of `AuthenticationContext` interface methods.

### onAuthenticationSuccess method
{: #custom-android-authlistener-onsuccess}
Call this method after a successful authentication. The arguments include the Android Context and an optional JSONObject that contains extended information about the authentication success.
```Java
void onAuthenticationSuccess(Context context, JSONObject info);
```

### onAuthenticationFailure method
{: #custom-android-authlistener-onfail}
Call this method after authentication fails. The arguments include Android Context and an optional JSONObject that contains extended information about authentication failure.
```Java
void onAuthenticationFailure(Context context, JSONObject info);
```

## AuthenticationContext interface
{: #custom-android-authcontext}

The `AuthenticationContext` is supplied as an argument to the `onAuthenticationChallengeReceived` method of a custom `AuthenticationListener`. You must collect credentials and use the `AuthenticationContext` methods to either return credentials to {{site.data.keyword.amashort}} client SDK or report a failure. Use one of the following methods.

```Java
void submitAuthenticationChallengeAnswer(JSONObject answer);
```
```Java
void submitAuthenticationFailure (JSONObject info);
```

## Sample implementation of a custom AuthenticationListener
{: #custom-android-samplecustom}

This AuthenticationListener sample is designed to work with a custom identity provider. You can download this sample from the [Github repository](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample).

```Java
package com.ibm.helloworld;
import android.content.Context;
import android.util.Log;
import com.ibm.mobilefirstplatform.clientsdk.android.security.api.AuthenticationContext;
import com.ibm.mobilefirstplatform.clientsdk.android.security.api.AuthenticationListener;
import org.json.JSONException;
import org.json.JSONObject;

public class CustomAuthenticationListener implements AuthenticationListener {
	@Override
	public void onAuthenticationChallengeReceived (AuthenticationContext authContext,
											JSONObject challenge, Context context) {

		log("onAuthenticationChallengeResceived :: " + challenge.toString());

		// In this sample the AuthenticationListener immediatelly returns a hardcoded
		// set of credentials. In a real life scenario this is where developer would
		// show a login screen, collect credentials and invoke
		// authContext.submitAuthenticationChallengeAnswer() API

		JSONObject challengeResponse = new JSONObject();
		try {
			challengeResponse.put("username", "john.lennon");
			challengeResponse.put("password", "12345");
			authContext.submitAuthenticationChallengeAnswer(challengeResponse);
		} catch (JSONException e){

			// In case there was a failure collecting credentials you need to report
			// it back to the AuthenticationContext. Otherwise Mobile Client
			// Access client SDK will remain in a waiting-for-credentials state
			// forever

			log("This should never happen...");
			authContext.submitAuthenticationFailure(null);
		}
	}

	@Override
	public void onAuthenticationSuccess (Context context, JSONObject info) {
		log("onAuthenticationSuccess :: " + info.toString());
	}

	@Override
	public void onAuthenticationFailure (Context context, JSONObject info) {
		log("onAuthenticationFailure :: " + info.toString());
	}

	private void log(String text){
		Log.d("CustomAuthListener", text);
	}
}
```

## Registering a custom AuthenticationListener
{: #custom-android-register}

After you create a custom AuthenticationListener, register it with `BMSClient` before you start using the listener. Add the following code to your application. This code must be called before you send any requests to your protected resources.

```Java
BMSClient.getInstance().registerAuthenticationListener(realmName,
									new CustomAuthenticationListener());
```

Use the *realmName* that you specified in the {{site.data.keyword.amashort}} dashboard.


## Testing the authentication
{: #custom-android-testing}
After the client SDK is initialized and a custom AuthenticationListener is registered, you can start making requests to your mobile backend.

### Before you begin
{: #custom-android-testing-before}
You must have an application that was created with the {{site.data.keyword.mobilefirstbp}} boilerplate and have a resource that is protected by {{site.data.keyword.amashort}} at the `/protected` endpoint.


1. Send a request to protected endpoint of your mobile backend in your browser by opening `{applicationRoute}/protected`, for example `http://my-mobile-backend.mybluemix.net/protected`.

1. The `/protected` endpoint of a mobile backend that is created with the {{site.data.keyword.mobilefirstbp}} boilerplate is protected with {{site.data.keyword.amashort}}. The endpoint can  be accessed by only mobile applications that are instrumented with the {{site.data.keyword.amashort}} client SDK. As a result, an `Unauthorized` message displays in your  browser.

1. Use your Android application to make request to the same endpoint. Add the following code after you initialize `BMSClient` and register your custom AuthenticationListener.

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

1. 	When your request succeeds, the following output is in the LogCat tool:

	![image](images/android-custom-login-success.png)

 You can also add logout functionality by adding the following code:

 ```Java
 AuthorizationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 If you call this code after a user is logged in, the user is logged out. When the user tries to log in again, they must answer the challenge received from the server again.

 The value for `listener` passed to the logout function can be `null`.
