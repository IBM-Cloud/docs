---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

The {{site.data.keyword.amafull}} service is replaced with the {{site.data.keyword.appid_full}} service.

# Enabling Facebook authentication for Cordova apps
{: #facebook-auth-cordova}

To configure {{site.data.keyword.amafull}}  Cordova applications for Facebook authentication integration, configure each platform separately. The Cordova application must already be instrumented with the {{site.data.keyword.amashort}} SDK.

Both your native platform and the Cordova WebView Javascript code require changes in order to enable Facebook authentication.

Use the native development environment to make changes in the native code, for example, in Android Studio or Xcode.
{:shortdesc}

## Before you begin
{: #facebook-auth-before}

You must have:
* A Cordova project (Android or iOS) that is instrumented with the {{site.data.keyword.amashort}} client SDK, see [Setting up the Cordova plug-in](getting-started-cordova.html#getting-started-cordova-plugin).
* An instance of a  {{site.data.keyword.Bluemix_notm}} application that is protected by {{site.data.keyword.amashort}} service. For more information about how to create a {{site.data.keyword.Bluemix_notm}} back-end service, see [Getting started](index.html).
* Your application route. This is the URL of your back-end application.
* Your `tenantId` value. Open your {{site.data.keyword.amashort}} service dashboard. Click **Mobile Options**. The `tenantId` (also known as `appGUID`)  value is displayed in the **App GUID / TenantId** field. You will need these values for intializing the SDK and for sending requests to the back-end service.
*  Find the region where your {{site.data.keyword.Bluemix_notm}} service is hosted. You can find your current {{site.data.keyword.Bluemix_notm}} region in the header, next to the **Avatar** icon ![Avatar icon](images/face.jpg "Avatar icon")  in the menu bar. The region value should be one of the following: **US South**, **Sydney**, or **UK**. The exact SDK constant values that correspond to these names are indicated in the code examples.
* A Facebook application and App ID. For more information, see [Obtaining a Facebook App ID from the Facebook Developer Portal](facebook-auth-overview.html#facebook-appID).



## Configuring the Android Platform
{: #facebook-auth-cordova-android}

The steps that are required to configure the Android platform of a Cordova application for Facebook authentication integration are very similar to the steps that are required for native Android applications. For more information, see [Enabling Facebook authentication in Android apps](facebook-auth-android.html). Complete the following steps:

* [Configuring your Facebook application for the Android Platform](facebook-auth-android.html#facebook-auth-android-config). This sets up the Facebook authentication on the Facebook Developers site for Android apps.
* [Configuring MCA for Facebook authentication](facebook-auth-android.html#facebook-auth-android-mca). This configures your {{site.data.keyword.amashort}} service on the {{site.data.keyword.Bluemix}} server for Android Facebook authentication.


### Configuring {{site.data.keyword.amashort}} Facebook client SDK for the Android platform
{: #configure_android}

The {{site.data.keyword.amashort}} Facebook client SDK must be added by Gradle within your native Android app project.

1. In your Android project folder, open the `build.gradle` file for the application module (**not** the project `build.gradle` file). Find the dependencies section, and add a new compile dependency for client SDK:

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

2. Click **Tools > Android > Sync Project with Gradle Files** to synchronize your project with Gradle.

3. Open the `android/res/values/strings.xml` file and add a `<facebook_app_id>` string that contains your Facebook App ID.

	```XML
	<resources>
		<string name="app_name">HelloCordova</string>
		<string name="launcher_name">@string/app_name</string>
		<string name="activity_name">@string/launcher_name</string>
		<string name="facebook_app_id">"<facebook_app_id>"</string>
	</resources>
	```
	{: codeblock}

4. In the `AndroidManifest.xml` file of your Android project (`android/manifests/AndroidManifest.xml`):

	* Add required metadata for the Facebook SDK to the <application> element:

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

        <activity   android:name="com.facebook.FacebookActivity"
	              android:configChanges="keyboard|keyboardHidden|screenLayout|screenSize|orientation"
	              android:theme="@android:style/Theme.Translucent.NoTitleBar"
	              android:label="@string/app_name"
        />
    </application>
    ```
    {: codeblock}

5. Add the following to your Activity Java code.

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
	   super.onActivityResult(requestCode, resultCode, data);
	    FacebookAuthenticationManager.getInstance()
	      .onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}

### Initialize the Authorization Manager in your native Android code
{: #initialize_android}

The  `FacebookAuthenticationManager`  API must still be registered in your native code. Add this code to the main activity `onCreate` method using the `<tenantId>` (see [Before you begin](#before-you-begin)).

```
String tenantId = "<tenantId>";
MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
FacebookAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
```
{: codeblock}


## Configuring the iOS platform
{: #facebook-auth-cordova-ios}

The steps required to configure iOS Platform of Cordova application for Facebook authentication integration are similar to the steps required for native iOS Swift applications (header files are needed for using Objective-C code with the Swift SDK). The major difference is that currently Cordova CLI does not support the CocoaPods dependency manager. You must manually add files that are required for integrating the {{site.data.keyword.amashort}} client with Facebook authentication. For more information, see [Enabling Facebook authentication for iOS apps (Swift SDK)](facebook-auth-ios-swift-sdk.html). Complete the following steps:

* [Configuring your Facebook application for the iOS Platform](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-config). This sets up the Facebook authentication service on the Facebook Developers site.
* [Configuring MCA for Facebook authentication](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-configmca). This configures your {{site.data.keyword.amashort}} service on the {{site.data.keyword.Bluemix}} server.
* [Configuring MCA Facebook client SDK for iOS](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-sdk). This installs the {{site.data.keyword.amashort}} iOS Swift SDK for Facebook authorization using CocoaPods.


### Enable Keychain Sharing for iOS
{: #enable_keychain}

Enable `Keychain Sharing`. Go to the `Capabilities` tab and switch the `Keychain Sharing` to `On` in your Xcode project.

### Initialize the {{site.data.keyword.amashort}} Authorization Manager in Objective-C
{: #initialize_objc}

The Authorization Manager must be initialized in the native Objective-C code in the  `app-delegate.m ` file, according to your version of Xcode.

```
	#import "<your_module_name>-Swift.h"

	- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

	{

	    [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];

	    [[FacebookAuthenticationManager sharedInstance] register];

	    self.viewController = [[MainViewController alloc] init];

	    [[FacebookAuthenticationManager sharedInstance] onFinishLaunchingWithApplication:application withOptions:launchOptions];


	    return [super application:application didFinishLaunchingWithOptions:launchOptions];
	}


	- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(NSString *)sourceApplication
			annotation:(id)annotation
	{

	   return [[FacebookAuthenticationManager sharedInstance] onOpenURLWithApplication:application
	   		url:url sourceApplication:sourceApplication annotation:annotation];
	}

```
{: codeblock}

**Note:** The imported header file name is composed of your module name concatenated to the string `-Swift.h`, for example, if your module name is `Cordova` then the import line would be `#import "Cordova-Swift.h"` To find the module name go to
`Build Settings` > `Packaging` > `Product Module Name`.

Replace `<tenantId>` your tenant id (see [Before you begin](#facebook-auth-before)).


##Initializing the  {{site.data.keyword.amashort}} client SDK in the Cordova WebView
{: #initialize_webview}

For all platforms, use the following JavaScript code in your Cordova Javascript WebView to initialize the  {{site.data.keyword.amashort}} client SDK.

```javascript
BMSClient.initialize(<applicationBluemixRegion>);
```
{: codeblock}

Replace `<applicationBluemixRegion>` with your region (see [Before you begin](#facebook-auth-before)).

## Testing the authentication
{: #facebook-auth-cordova-test}

After the client SDK is initialized and Facebook authentication manager is registered, you can start making requests to your mobile back-end service.

### Before you begin
{: #testing_auth_before}

You must be using the {{site.data.keyword.mobilefirstbp}} boilerplate and already have a resource protected by {{site.data.keyword.amashort}} at the `/protected` endpoint. For more information, see [Protecting resources](protecting-resources.html).

1. Try to send a request to protected endpoint of your mobile back-end application from your browser. Open the following URL: `{applicationRoute}/protected`. For example: `http://my-mobile-backend.mybluemix.net/protected`.

	The `/protected` endpoint value should be any protected endpoint of a mobile back-end service that was created with MobileFirst Services Starter boilerplate and is protected with {{site.data.keyword.amashort}}. An `Unauthorized` message is returned in your browser. This message is returned because this endpoint can only be accessed by mobile applications that are instrumented with {{site.data.keyword.amashort}} client SDK.

1. Use your Cordova application to make request to the same endpoint. Add the following code after you initialize `BMSClient`:

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error){
    	console.log("failure", error);
    }
	var request = new BMSRequest("<applicationRoute}/protected>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

1. Run your application. A Facebook login screen pops up:

	![image](images/android-facebook-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![image](images/ios-facebook-login.png)

	This screen might look slightly different if you do not have the Facebook app installed on your device, or if you are not currently logged in to Facebook.

1. Click **OK** to authorize {{site.data.keyword.amashort}}  to use your Facebook user identity for authentication purposes.

1. 	When your request succeeds, the following output is in the LogCat utility or Xcode console:

	![Facebook authentication success message for Android](images/android-facebook-login-success.png)

	![Facebook authentication success message for iOS ](images/ios-facebook-login-success.png)
