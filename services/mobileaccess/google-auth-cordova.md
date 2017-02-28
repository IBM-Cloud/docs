---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Enabling Google authentication for Cordova apps
{: #google-auth-cordova}

To integrate your {{site.data.keyword.amafull}} Cordova applications for Google authentication,  you must make changes in the Cordova application native platform code (Java or Objective-C), as well as in the Cordova WebView (Javascript). Each platform must be configured separately. Use the native development environment to make changes in the native code, for example, in Android Studio or Xcode.

## Before you begin
{: #before-you-begin}

You must have:

* A Cordova project that is instrumented with {{site.data.keyword.amashort}} client SDK.  For more information, see  [Setting up the Cordova plug-in](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html).  
* An instance of a  {{site.data.keyword.Bluemix_notm}} application that is protected by {{site.data.keyword.amashort}} service. For more information about how to create a {{site.data.keyword.Bluemix_notm}} back-end service, see [Getting started](index.html).
* Your application route. This is the URL of your back-end application.
* Your **TenantID**. Open your service in the {{site.data.keyword.Bluemix_notm}} dashboard. Click **Mobile Options**. The `tenantId`   (also known as `appGUID`) value is displayed in the **App GUID / TenantId** field. You will need this value for intializing the Authorization Manager.
*  Find the region where your {{site.data.keyword.Bluemix_notm}} application is hosted. You can find your current Bluemix region in the header, next to the **Avatar** icon ![Avatar icon](images/face.jpg "Avatar icon"). The region value should be one of the following: **US South**, **Sydney**, or **UK**. The exact SDK constant values that correspond to these names are indicated in the code examples.
* (optional) Get familiar with the following sections:
   * [Enabling Google authentication for Android apps](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)
   * [Enabling Google authentication for iOS apps](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)


## Configuring the Android platform
{: #google-auth-cordova-android}

The steps required to configure Android platform of a Cordova application for Google authentication are very similar to the steps required for native applications. See [Enabling Google authentication in Android apps](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html) and set up the following:

   * [Creating a project on the Google Developer Console](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html#create-google-project). This shows you how to set up the authentication service on the Google Developers website.
   * [Configuring MCA for Google authentication](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html#google-auth-android-config). This shows you how to set up your {{site.data.keyword.amashort}} to use Google authorization.

### Configure the {{site.data.keyword.amashort}} client SDK for Android Cordova

1. In your Android project folder, open the `build.gradle` file for the application module (**not** the  project `build.gradle` file).
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
	{: codeblock}

1. Synchronize your project with Gradle by clicking **Tools > Android > Sync Project with Gradle Files**.

1. The `GoogleAuthenticationManager` API must still be registered in your native code. Add this code to the main activity `onCreate` method:

	```Java
	String tenantId = "<tenantId>";
	MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
	BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
	GoogleAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
	```
	{: codeblock}

1. Add the following code to your Activity:

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		GoogleAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}

## Configuring the iOS Platform
{: #google-auth-cordova-ios}

The steps required to configure iOS Platform of Cordova application for Google authentication integration are similar to the steps for native applications. The major difference is that currently Cordova CLI does not support the CocoaPods dependency manager. You must manually add the required files for integrating with Google authentication. For more information, see  [Enabling Google authentication for iOS apps (Swift SDK)](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html). Complete the following steps:

   * [Preparing your app for Google Sign-In](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-sign-in-ios): Prepares the Google Sign-In for authenticating  {{site.data.keyword.amashort}} iOS applications.

   * [Configuring MCA for Google authentication](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-auth-ios-config): Configures your {{site.data.keyword.amashort}} service to work with the Google Sign-In.

   * [Configuring the MCA client SDK for iOS](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-auth-ios-sdk): Configures your {{site.data.keyword.amashort}} client to work with the Google Sign-In.


### Enable Keychain Sharing for iOS
{: #enable_keychain}

Enable `Keychain Sharing`. Go to the `Capabilities` tab and switch the `Keychain Sharing` to `On` in your Xcode project.


### Initializing the Authorization Manager in your iOS code

Initialize the {{site.data.keyword.amashort}} Authorization Manager in Objective-C in the `AppDelgate.m` file.

```
#import "<your_module_name>-Swift.h"

- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

{
	[CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];

	[[GoogleAuthenticationManager sharedInstance] register];

	self.viewController = [[MainViewController alloc] init];

	[[GoogleAuthenticationManager sharedInstance] onFinishLaunchingWithApplication:application withOptions:launchOptions];

	return [super application:application didFinishLaunchingWithOptions:launchOptions];
}

- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(NSString *)sourceApplication annotation:(id)annotation

{
	return [[GoogleAuthenticationManager sharedInstance] onOpenURLWithApplication:application url:url
	sourceApplication:sourceApplication annotation:annotation];
}
```
{: codeblock}


####Note:
{: #note notoc}

* Replace `<your_module_name>` with the module name of your project. For example, if your module name is `Cordova`, then the import line should be `#import "Cordova-Swift.h"` Find the module name go to the
`Build Settings`  tab,  `Packaging` > `Product Module Name`.
* Replace your `<tenantId>` with your tenant id (see [Before you begin](#before-you-begin)).


## Initializing the {{site.data.keyword.amashort}} client SDK in your Cordova WebView
{: #google-auth-cordova-initialize}

For all platforms, use the following Javascript code in your Cordova application to initialize the {{site.data.keyword.amashort}} client SDK.

```JavaScript
BMSClient.initialize("<applicationBluemixRegion>");
```
{: codeblock}

Replace `<applicationBluemixRegion>` with your region (see [Before you begin](#before-you-begin)).

## Testing the authentication
{: #google-auth-cordova-test}

After the client SDK is initialized, you can start making requests to your mobile back-end application.

### Before you begin
{: #google-auth-cordova-testing-before}

You must have a back-end application protected by {{site.data.keyword.amashort}} at the `/protected` endpoint. If you need to set up a `/protected` endpoint, see [Protecting resources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Try to send a request to a protected endpoint of your mobile back-end application in your desktop browser by opening `{applicationRoute}/protected`, for example `http://my-mobile-backend.mybluemix.net/protected`.

1. The `/protected` endpoint of a mobile back-end application created with the MobileFirst Services Boilerplate is protected with {{site.data.keyword.amashort}}, therefore it can be accessed only by mobile applications that are instrumented with the  {{site.data.keyword.amashort}} client SDK. As a result, you will see `Unauthorized` in your desktop browser.

1. Use your Cordova application to make a request to the same endpoint, using the full URL (for example `http://my-mobile-backend.mybluemix.net/protected`). Add the following code after you initialize `BMSClient`.

	```JavaScript
	var success = function(data){
		console.log("success", data);
	}
	var failure = function(error){
		console.log("failure", error);
	}
	var request = new BMSRequest("<your-application-route>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

1. Run your application. The Google login screen displays.

	![Google login screen](images/android-google-login.png)

	![Google login screen](images/ios-google-login.png)

	This screen might look slightly different if you do not have the Facebook app installed on your device, or if you are not currently logged in to Facebook.

1. By clicking **OK** you are authorizing {{site.data.keyword.amashort}} to use your Google user identity for authentication purposes.

1. Your request should succeed. Depending on the platform that you use, you will see the following output in LogCat/Xcode console:

	![Code snippet on android](images/android-google-login-success.png)

	![Code snippet on iOS](images/ios-google-login-success.png)
