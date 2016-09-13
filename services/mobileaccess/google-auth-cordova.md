---

copyright:
  years: 2015, 2016

---
{:screen: .screen}
{:shortdesc: .shortdesc}

# Enabling Google authentrn for Cordova apps
{: #google-auth-cordova}


Last updated: 31 August 2016
{: .last-updated}

To configure your {{site.data.keyword.amafull}} Cordova applications for Google authentication integration,  you must make changes in the native code of the Cordova application (Java, Objective-C, or Swift). Each platform must be configured separately. Use the native development environment to make changes in the native code, for example, in Android Studio or Xcode.

## Before you begin
{: #before-you-begin}
You must have:
* A Cordova project that is instrumented with {{site.data.keyword.amashort}} client SDK.  For more information, see  [Setting up the Cordova plug-in](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html).  
* An instance of a  {{site.data.keyword.Bluemix_notm}} application that is protected by {{site.data.keyword.amashort}} service. For more information about how to create a {{site.data.keyword.Bluemix_notm}} back-end application, see [Getting started](index.html).
* (optional) Get familiar with the following sections:
   * [Enabling Google authentication for Android apps](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)
   * [Enabling Google authentication for iOS apps](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html)


## Configuring the Android Platform
{: #google-auth-cordova-android}

The steps required to configure Android Platform of a Cordova application for Google authentication integration are very similar to the steps required for native applications. See [Enabling Google authentication in Android apps](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html) and set up the following:

* Configuring Google Project for Android Platform
* Configuring {{site.data.keyword.amashort}} for Google authentication

### Configure the {{site.data.keyword.amashort}} client SDK for Android Cordova


2. In your Android project folder, open the `build.gradle` file for the application module (**not** the  project `build.gradle` file).
Find the dependencies section and add a new compile dependency for client SDK:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'googleauthentication',
        version: '1.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```

2. Synchronize your project with Gradle by clicking **Tools > Android > Sync Project with Gradle Files**.

3. For Cordova applications initialize the  {{site.data.keyword.amashort}}  client SDK in your JavaScript code instead of in the Java code. The `GoogleAuthenticationManager` API must still be registered in your native code. Add this code to the main activity `onCreate` method: 

	```Java
	GoogleAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
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

## Configuring the iOS Platform
{: #google-auth-cordova-ios}

The steps required to configure iOS Platform of Cordova application for Google authentication integration are similar to the steps for native applications. The major difference is that currently Cordova CLI does not support the CocoaPods dependency manager.  You must manually add the required files for integrating with Google authentication. For more information, see  [Enabling Google authentication in iOS apps](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html). Complete the following steps:

* Configuring Google Project for iOS Platform
* Configuring {{site.data.keyword.amashort}} for Google authentication

### Manually installing the {{site.data.keyword.amashort}} SDK for Google authentication and Google SDK
{: #google-auth-cordova-ios-sdk}
1. Download the archive containing [{{site.data.keyword.Bluemix}} Mobile Services SDK for iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).

1. Go to the `Sources/Authenticators/IMFGoogleAuthentication` directory and copy (drag and drop) all of the files to your iOS project in Xcode. The files you need to copy are:

	* IMFDefaultGoogleAuthenticationDelegate.h
	* IMFDefaultGoogleAuthenticationDelegate.m
	* IMFGoogleAuthenticationDelegate.h
	* IMFGoogleAuthenticationHandler.h
	* IMFGoogleAuthenticationHandler.m

	Select the **Copy files....** checkbox.

1. Download and install [Google+ iOS SDK](http://goo.gl/9cTqyZ).

1. Follow Step 2 of [Start integrating Google+ into your iOS app](https://developers.google.com/+/mobile/ios/getting-started) tutorial to integrate Google+ iOS SDK into your Xcode project.

Continue to the **Configuring iOS project for Google Authentication** section of [Configuring iOS Platform for Google authentication](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html). Register the `IMFGoogleAuthenticationHandler` in native code as described in the `Initializing the {{site.data.keyword.amashort}} client SDK` section. Do not initialize `IMFClient` in your native code (the client is initialized in JavaScript in the following section).

Add this line to the `application:openURL:sourceApplication:annotation` method of your application delegate. This ensures that all Cordova plug-ins are notified of respective events.

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```
{: codeblock}

## Initializing the {{site.data.keyword.amashort}} client SDK
{: #google-auth-cordova-initialize}

Use the following JavaScript code in your Cordova application to initialize the {{site.data.keyword.amashort}} client SDK.

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```
{: codeblock}

Replace the `applicationRoute` and `applicationGUID` values with the application **Route** and **AppGuid** values. You can find these values by clicking the **Mobile Options** button from within the application page on the dashboard.
	



##Initializing the {{site.data.keyword.amashort}} AuthorizationManager
Use the following JavaScript code in your Cordova application to initialize the {{site.data.keyword.amashort}} AuthorizationManager.

```JavaScript
MFPAuthorizationManager.initialize("tenantId");
```
{: codeblock}

Replace the `tenantId` value with the {{site.data.keyword.amashort}} service `tenantId`. This value you can find by clicking the **Show Credentials** button on the {{site.data.keyword.amashort}} service tile.





## Testing the authentication
{: #google-auth-cordova-test}
After the client SDK is initialized, you can start making requests to your mobile back-end application.

### Before you begin
{: #google-auth-cordova-testing-before}
You must have a back-end application protected by {{site.data.keyword.amashort}} at the `/protected` endpoint. If you need to set up a `/protected` endpoint, see [Protecting resources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Try to send a request to a protected endpoint of your mobile back-end application in your desktop browser by opening `{applicationRoute}/protected`, for example `http://my-mobile-backend.mybluemix.net/protected`.

1. The `/protected` endpoint of a mobile back-end application created with the MobileFirst Services Boilerplate is protected with {{site.data.keyword.amashort}}, therefore it can be accessed only by mobile applications that are instrumented with the  {{site.data.keyword.amashort}} client SDK. As a result, you will see `Unauthorized` in your desktop browser.

1. Use your Cordova application to make a request to the same endpoint. Add the following code after you initialize `BMSClient`.

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
	request.send(success, failure);
	```
{: codeblock}

1. Run your application. The Google login screen displays.

	![Google login screen](images/android-google-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![Google login screen](images/ios-google-login.png)
	
	This screen might look slightly different if you do not have the Facebook app installed on your device, or if you are not currently logged in to Facebook.
1. By clicking **OK** you are authorizing {{site.data.keyword.amashort}} to use your Google user identity for authentication purposes.

1. Your request should succeed. Depending on the platform that you use, you will see the following output in LogCat/Xcode console:

	![Code snippet on android](images/android-google-login-success.png)

	![Code snippet on iOS](images/ios-google-login-success.png)
