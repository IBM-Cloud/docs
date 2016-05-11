---

copyright:
  years: 2015, 2016

---

# Enabling Facebook authentication in Cordova apps
{: #facebook-auth-cordova}
To configure Cordova applications for Facebook authentication integration, you must make changes in native code of the Cordova application, in Java, Objective-C, or Swift. Configure each platform separately. Use the native development environment to make changes in the native code, for example, in Android Studio or Xcode.

## Before you begin
{: #facebook-auth-before}
* You must have a resource that is protected by {{site.data.keyword.amashort}} and a Cordova project that is instrumented with the {{site.data.keyword.amashort}} client SDK.  For more information, see [Getting started with {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) and [Setting up the Cordova plug-in](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html).
* Manually protect your backend application with {{site.data.keyword.amashort}} server SDK. For more information, see [Protecting resources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).
* Create a Facebook Application ID. For more information, see [Obtaining a Facebook application ID from the Facebook Developer Portal](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).
* (optional) Get familiar with the following sections:
   * [Enabling Facebook authentication in Android apps](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html)
   * [Enabling Facebook authentication in iOS apps](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)


## Configuring the Android Platform
{: #facebook-auth-cordova-android}

The steps that are required to configure the Android Platform of a Cordova application for Facebook authentication integration are very similar to the steps that are required for native Android applications. For more information, see [Enabling Facebook authentication in Android apps](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html). Complete the following steps:

* Configuring Facebook Application for Android Platform
* Configuring {{site.data.keyword.amashort}} for Facebook authentication
* Configuring {{site.data.keyword.amashort}} client SDK for Android

The only difference when you are configuring Cordova applications is that you must initialize the {{site.data.keyword.amashort}} client SDK in your JavaScript code instead of in the Java code. The `FacebookAuthenticationManager` API must still be registered in your native code.

## Configuring the iOS platform
{: #facebook-auth-cordova-ios}

The steps required to configure iOS Platform of Cordova application for Facebook authentication integration are similar to the steps required for native iOS applications. The major difference is that currently Cordova CLI does not support the CocoaPods dependency manager. You must manually add files that are required for integrating with Facebook authentication. For more information, see  [Enabling Facebook authentication in iOS apps](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html). Complete the following steps:

* Configuring Facebook Application for iOS Platform
* Configuring {{site.data.keyword.amashort}} for Facebook authentication

### Manually installing the {{site.data.keyword.amashort}} SDK for Facebook authentication and Facebook SDK
{: #facebook-auth-cordova-ios-sdk}
1. Download the archive that contains the [{{site.data.keyword.Bluemix_notm}} Mobile Services SDK for iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).

1. Go to the `Sources/Authenticators/IMFFacebookAuthentication` directory and copy (drag and drop) all of the files to your iOS project in Xcode. Copy the following files:
	* IMFDefaultFacebookAuthenticationDelegate.h
  * IMFDefaultFacebookAuthenticationDelegate.m
	* IMFFacebookAuthenticationDelegate.h
	* IMFFacebookAuthenticationHandler.h
	* IMFFacebookAuthenticationHandler.m

	When prompted by Xcode, select **Copy files...**.

1. Download and install [Facebook SDK v3.19](https://developers.facebook.com/resources/facebook-ios-sdk-3.19.pkg).

1. The Facebook SDK will be installed into `~/Documents/FacebookSDK` directory. Navigate to that directory and copy (drag and drop) the `FacebookSDK.framework` file to your iOS project in Xcode.

1. 	Click your project root in the left pane of Xcode and select **Build Phases**.

1. Add the `FacebookSDK.framework` file to the list of linked libraries in **Link binary with libraries**.

 See [Configuring iOS Platform for Facebook authentication](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html). Register the `IMFFacebookAuthenticationHandler` API in native code as described in the **Initializing the {{site.data.keyword.amashort}} client SDK** section. Do not initialize `IMFClient` in your native code.

Add the following line to the `application:openURL:sourceApplication:annotation` method of your application delegate. This code ensures that all Cordova plugins are notified of respective events.

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```

## Initializing the {{site.data.keyword.amashort}} client SDK
{: #facebook-auth-cordova-init}

Use the following JavaScript code in your Cordova application to initialize the {{site.data.keyword.amashort}} client SDK.

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```

Replace *applicationRoute* and *applicationGUID* with values obtained for **Route** and **App GUID** from **Mobile Options**.

## Testing the authentication
{: #facebook-auth-cordova-test}
After the client SDK is initialized and Facebook authentication manager is registered, you can start making requests to your mobile backend.

### Before you begin
You must be using the {{site.data.keyword.mobilefirstbp}} boilerplate and already have a resource protected by {{site.data.keyword.amashort}} at the `/protected` endpoint. For more information, see [Protecting resources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Try to send a request to protected endpoint of your newly created mobile backend in your browser. Open the following URL: `{applicationRoute}/protected`. For example: `http://my-mobile-backend.mybluemix.net/protected`
<br/>The `/protected` endpoint of a mobile backend that was created with MobileFirst Services Starter boilerplate is protected with {{site.data.keyword.amashort}}. An `Unauthorized` message is returned in your browser. This message is returned because this endpoint can only be accessed by mobile applications that are instrumented with {{site.data.keyword.amashort}} client SDK.

1. Use your Cordova application to make request to the same endpoint. Add the below code after you initialize `BMSClient`:

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error){
    	console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
	request.send(success, failure);
	```

1. Run your application. A Facebook Login screen pops up:

	![image](images/android-facebook-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![image](images/ios-facebook-login.png)

	> This screen might look slightly different if you do not have the Facebook app installed on your device, or if you are not currently logged in to Facebook.

1. Click **OK** to authorize {{site.data.keyword.amashort}}  to use your Facebook user identity for authentication purposes.

1. 	When your request succeeds, the following output is in the LogCat utility or Xcode console:

	![Facebook authentication success message for Android](images/android-facebook-login-success.png)

	![Facebook authentication success message for iOS ](images/ios-facebook-login-success.png)
