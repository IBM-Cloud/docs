---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---

The {{site.data.keyword.amafull}} service is replaced with the {{site.data.keyword.appid_full}} service.

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Configuring custom authentication for your {{site.data.keyword.amashort}} Android app
{: #custom-android}


Configure your Android application with custom authentication to use the {{site.data.keyword.amashort}} client SDK, and connect your application to {{site.data.keyword.Bluemix}}.

## Before you begin
{: #before-you-begin}
Before you begin you must have:

* A resource that is protected by an instance of the {{site.data.keyword.amashort}} service that is configured to use a custom identity provider (see [Configuring custom authentication](custom-auth-config-mca.html)).  
* Your **TenantID** value. Open your service in the  {{site.data.keyword.amashort}} dashboard. Click the **Mobile Options** button. The `tenantId` (also known as `appGUID`)  value is displayed in the **App GUID / TenantId** field. You will need this value for intializing the Authorization Manager.
* Your **Realm** name. This is the value you you specificed in the **Realm Name** field of the **Custom** section in the **Management** tab of the {{site.data.keyword.amashort}} dashboard.
* The URL of your back-end application (**App Route**). You will need this values for sending requests to the protected endpoints of your back-end application.
* Your {{site.data.keyword.Bluemix_notm}} **Region**. You can find your current {{site.data.keyword.Bluemix_notm}} region in the header, next to the **Avatar** icon ![Avatar icon](images/face.jpg "Avatar icon"). The region value that appears should be one of the following: `US South`, `United Kingdom`, or `Sydney`, and correspond to the SDK values required in the WebView Javascript code: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY`, or `BMSClient.REGION_UK`. You will need this value for initializing the {{site.data.keyword.amashort}} client.

For more information, see the following information:
 * [Getting started with {{site.data.keyword.amashort}}](getting-started.html)
 * [Setting up Android SDK](getting-started-android.html)
 * [Using a custom identity provider](custom-auth.html)
 * [Creating a custom identity provider](custom-auth-identity-provider.html)
 * [Configuring {{site.data.keyword.amashort}} for custom authentication](custom-auth-config-mca.html)



## Initializing the {{site.data.keyword.amashort}} client SDK
{: #custom-android-initialize}
If you have an Android app instrumented with the {{site.data.keyword.amashort}} Android SDK you can skip this section.
1. In your Android project in Android Studio, open the `build.gradle` file of your app module (not the project `build.gradle`).

1. In the `build.gradle`  file, find the `dependencies` section and check for that the following dependency exists:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```
	{: codeblock}

1. Synchronize your project with Gradle. Click **Tools > Android > Sync Project with Gradle Files**.

1. Open the `AndroidManifest.xml` file of your Android project.
Add the internet access permission under the `<manifest>` element:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```
	{: codeblock}

1. Initialize the SDK.  
	A common, though not mandatory, place to put the initialization code is in the `onCreate` method of the main activity in your Android application.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);
	```
	{: codeblock}

Replace the `BMSClient.REGION_UK` with the {{site.data.keyword.amashort}} region. For more information on obtaining these values see  [Before you begin](#before-you-begin).


## AuthenticationListener interface
{: #custom-android-authlistener}

The {{site.data.keyword.amashort}} client SDK provides the `AuthenticationListener` interface so that you can implement a custom authentication flow. The `AuthenticationListener` interface exposes three methods that are called in different phases during the authentication process.

### onAuthenticationChallengeReceived method
{: #custom-onAuth}
Call this method when a custom authentication challenge is received from the {{site.data.keyword.amashort}} service.

```Java
void onAuthenticationChallengeReceived(AuthenticationContext authContext, JSONObject challenge, Context context);
```
{: codeblock}


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
{: codeblock}

### onAuthenticationFailure method
{: #custom-android-authlistener-onfail}
Call this method after authentication fails. The arguments include Android Context and an optional `JSONObject` that contains extended information about authentication failure.
```Java
void onAuthenticationFailure(Context context, JSONObject info);
```
{: codeblock}

## AuthenticationContext interface
{: #custom-android-authcontext}

The `AuthenticationContext` is supplied as an argument to the `onAuthenticationChallengeReceived` method of a custom `AuthenticationListener`. You must collect credentials and use the `AuthenticationContext` methods to either return credentials to {{site.data.keyword.amashort}} client SDK or report a failure. Use one of the following methods.

```Java
void submitAuthenticationChallengeAnswer(JSONObject answer);
```
{: codeblock}

```Java
void submitAuthenticationFailure (JSONObject info);
```
{: codeblock}

## Sample implementation of a custom AuthenticationListener
{: #custom-android-samplecustom}

This AuthenticationListener sample is designed to work with a custom identity provider. You can download this sample from the [Github repository ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}.

```Java
package com.ibm.helloworld;
import android.content.Context;
import android.util.Log;
import com.ibm.mobilefirstplatform.clientsdk.android.security.mca.api.AuthenticationContext;
import com.ibm.mobilefirstplatform.clientsdk.android.security.mca.api.AuthenticationListener;
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
{: codeblock}

## Registering a custom AuthenticationListener
{: #custom-android-register}

After you create a custom AuthenticationListener, register it with `BMSClient` before you start using the listener. Add the following code to your application. This code must be called before you send any requests to your protected resources.

```Java
MCAAuthorizationManager mcaAuthorizationManager =
      MCAAuthorizationManager.createInstance(this.getApplicationContext(),"<MCAServiceTenantId>");
mcaAuthorizationManager.registerAuthenticationListener(realmName, new CustomAuthenticationListener());
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);

```
{: codeblock}


In the code:
* Replace `MCAServiceTenantId` with the **TenantId** value (see [Before you begin](##before-you-begin)).
* Use the `realmName` that you specified in the {{site.data.keyword.amashort}} dashboard (see [Configuring custom authentication](custom-auth-config-mca.html)).


## Testing the authentication
{: #custom-android-testing}
After the client SDK is initialized and a custom AuthenticationListener is registered, you can start making requests to your mobile back-end application.

### Before you test
{: #custom-android-testing-before}
You must have an application that has a resource that is protected by {{site.data.keyword.amashort}} at the `/protected` endpoint.


1. Send a request to the protected endpoint (`{applicationRoute}/protected`) of your mobile back-end application from your browser, for example `http://my-mobile-backend.mybluemix.net/protected`. For information on obtaining the `{applicationRoute}` value, see   [Before you begin](#before-you-begin).

1. The `/protected` endpoint of a mobile back-end application that is created with the {{site.data.keyword.mobilefirstbp}} boilerplate is protected with {{site.data.keyword.amashort}}. The endpoint can  be accessed by only mobile applications that are instrumented with the {{site.data.keyword.amashort}} client SDK. As a result, an `Unauthorized` message displays in your  browser.

1. Use your Android application to make request to the same protected endpoint that includes the `{applicationRoute}`. Add the following code after you initialize `BMSClient` and register your custom AuthenticationListener.

	```Java
	Request request = new Request("{applicationRoute}/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp",  MCAAuthorizationManager.getInstance().getUserIdentity().toString());
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

1. 	When your request succeeds, the following output is in the LogCat tool:

	![image](images/android-custom-login-success.png)

 You can also add logout functionality by adding the following code:

 ```Java
 MCAAuthorizationManager.getInstance().logout(getApplicationContext(), listener);
 ```
 {: codeblock}


 If you call this code after a user is logged in, the user is logged out. When the user tries to log in again, they must answer the challenge that is received from the server again.

 The value for `listener` passed to the logout function can be `null`.
