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

# Configuring custom authentication for your Mobile Client Access Cordova app
{: #custom-cordova}

Instrument your Cordova application to use custom authentication and {{site.data.keyword.amafull}} client SDK to access your protected application.

## Before you begin
{: #before-you-begin}
* A resource that is protected by an instance of the {{site.data.keyword.amashort}} service that is configured to use a custom identity provider (see [Configuring custom authentication](custom-auth-config-mca.html)).  
* Your **TenantID** value. Open your service in the  {{site.data.keyword.amashort}} dashboard. Click the **Mobile Options** button. The `tenantId` (also known as `appGUID`)  value is displayed in the **App GUID / TenantId** field. You will need this value for intializing the Authorization Manager.
* Your **Realm** name. This is the value you you specificed in the **Realm Name** field of the **Custom** section in the **Management** tab of the {{site.data.keyword.amashort}} dashboard.
* Your {{site.data.keyword.Bluemix_notm}} **Region**. You can find your current {{site.data.keyword.Bluemix_notm}} region in the header, next to the **Avatar** icon ![Avatar icon](images/face.jpg "Avatar icon"). The region value that appears should be one of the following: `US South`, `United Kingdom`, or `Sydney`. Exact syntax of the corresponding SDK constants are given in the code examples.

For more information, see the following information:

 * [Configuring {{site.data.keyword.amashort}} for custom authentication](custom-auth-config-mca.html). This shows you how to set up the {{site.data.keyword.amashort}} service for custom authentication. Here you define the **Realm** value.
 * [Setting up Cordova SDK](getting-started-cordova.html). Information on setting  up the Cordova client app.
 * [Using a custom identity provider](custom-auth.html). How to authenticate users with a custom identity provider.
 * [Creating a custom identity provider](custom-auth-identity-provider.html). Some examples of how a custom identity provider works.

## Configure your Cordova WebView code
### Initializing the {{site.data.keyword.amashort}} client SDK in the Cordova WebView
{: #custom-cordova-sdk}
Initialize the SDK by passing the `<applicationBluemixRegion>` parameter in the `index.js` file.

```JavaScript
BMSClient.initialize("<applicationBluemixRegion>");
```
{: codeblock}

Replace `<applicationBluemixRegion>` with your region (see [Before you begin](#before-you-begin)).


### Authentication listener interface
{: #custom-cordva-auth}

The {{site.data.keyword.amashort}} client SDK provides an authentication listener interface to implement a custom authentication flow. You must add the following methods that are called in different phases of an authentication process.

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...},
	onAuthenticationSuccess: function(info){...},
	onAuthenticationFailure: function(info){...}
}
```
{: codeblock}

Each method handles a different phase of an authentication process.

### onAuthenticationChallengeReceived method
{: #onAuthenticationChallengeReceived}
This method is called when a custom authentication challenge is received from {{site.data.keyword.amashort}} service.
```JavaScript
onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...}
```
{: codeblock}

* `authenticationContext`: Provided by {{site.data.keyword.amashort}} client SDK so that developer can report back authentication challenge answers or failure during credentials collection, such as the user cancelling the authentication request.
* `challenge`: A JSON object that contains a custom authentication challenge, as returned by a custom identity provider.

Calling the `onAuthenticationChallengeReceived` method the {{site.data.keyword.amashort}} client SDK delegates control to developer. The {{site.data.keyword.amashort}} waits for credentials. The developer must collect credentials and report them back to the {{site.data.keyword.amashort}} client SDK by using one of the following  `authContext` interface methods.

```JavaScript
onAuthenticationSuccess: function(info){...}
```
{: codeblock}

This method is called after a successful authentication. The arguments include an optional JSON object that contains extended information about the authentication success.

```JavaScript
onAuthenticationFailure: function(info){...}
```
{: codeblock}

This method is called after an authentication failure. The arguments include an optional JSON object that contains extended information about the authentication failure.

### authenticationContext
{: #custom-cordova-authcontext}

The `authenticationContext` value is supplied as an argument to the `onAuthenticationChallengeReceived` method of a custom authentication listener. The developer must collect credentials and use the `authenticationContext` methods to either return credentials to the {{site.data.keyword.amashort}} client SDK or report a failure. Use one of the following methods:

```JavaScript
authenticationContext.submitAuthenticationChallengeAnswer(challengeAnswer);
```
{: codeblock}

```JavaScript
authenticationContext.submitAuthenticationFailure(info);
```
{: codeblock}

The following code demonstrates how a customer authentication listener can collect credentials, deal with challenges, and provide authentication responses.

## Sample implementation of a custom authentication listener workflow
{: #custom-cordova-authlisten-sample}

This authentication listener sample is designed to work with a custom identity provider. You can download the custom identity provider from [this Github repository ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}.

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {
		console.log("onAuthenticationChallengeReceived :: ", challenge);

		// In this sample the authentication listener immediatelly returns a hardcoded
		// set of credentials. In a real life scenario this is where developer would
		// show a login screen, collect credentials and invoke
		// authenticationContext.submitAuthenticationChallengeAnswer() API

		var challengeResponse = {
			username: "john.lennon",
			password: "12345"
		}

		authenticationContext.submitAuthenticationChallengeAnswer(challengeResponse);

		// In case there was a failure collecting credentials you need to report
		// it back to the authenticationContext. Otherwise Mobile Client
		// Access client SDK will remain in a waiting-for-credentials state
		// forever

	},

	onAuthenticationSuccess: function(info){
		console.log("onAuthenticationSuccess :: ", info);
	},

	onAuthenticationFailure: function(info){
		console.log("onAuthenticationFailure :: ", info);
	}
}
```
{: codeblock}

## Registering a custom authentication listener in the Cordova WebView
{: #custom-cordova-authreg}

After you create a custom authentication listener, you must register it with `BMSClient` before you can start using it. Add the following code to your application.  Call this code before you send any requests to your protected resources.

```Java
BMSClient.registerAuthenticationListener(<realmName>, customAuthenticationListener);
```
{: codeblock}
 Use `realmName` that you specified in the {{site.data.keyword.amashort}} dashboard.

## Set Authorization Manager in the native code

The  {{site.data.keyword.amashort}}  Authorization Manager must be registered in your native platform code.

**Android** (add to `onCreate` in the main activity)

```
String tenantId = "<tenantId>";
MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
```
{: codeblock}

**iOS Objective-C** (add to `AppDelegate.m`)

Register your Authorization Manager according to your version of Xcode.

```
#import "<your_module_name>-Swift.h"

- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

{  

    //[CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];
 }
```
{: codeblock}

Note: For the correct Swift header file name, replace `your_module_name` with the module name of your project, for example, if your module name is `Cordova` then it should be `#import "Cordova-Swift.h"`. To find the module name go to **Build Settings > Packagin` > Product Module Name**.

**Note:** Replace your `tenantId` with your tenant id found in **Mobile Options** button on the {{site.data.keyword.amashort}} service dashboard.


## Enable Keychain Sharing for iOS

Enable `Keychain Sharing` by going to `Capabilities` tab and switch the `Keychain Sharing` to `On` in your Xcode project.


## Testing the authentication
{: #custom-cordova-test}
After the client SDK is initialized and a custom `AuthenticationListener` is registered, you can start making requests to your mobile back-end application.

### Before you begin
{: #custom-cordova-testing-before}
You must have an application that was created with the {{site.data.keyword.mobilefirstbp}} boilerplate and have a resource that is protected by {{site.data.keyword.amashort}} at the `/protected` endpoint.


1. Send a request to protected endpoint of your mobile back-end application in your browser by opening `{applicationRoute}/protected`, for example `http://my-mobile-backend.mybluemix.net/protected`.
 The `/protected` endpoint of a mobile back-end application that is created with the {{site.data.keyword.mobilefirstbp}} boilerplate is protected with {{site.data.keyword.amashort}}. The endpoint can  be accessed only by mobile applications that are instrumented with the {{site.data.keyword.amashort}} client SDK. As a result, an `Unauthorized` message displays in your browser.

1. Use your Cordova application to make request to the same endpoint. Add the following code after you initialize `BMSClient` and register your custom AuthenticationListener.

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new BMSRequest("<your-application-route>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

	Replace `<your-application-route>` with your back-end application URL (see [Before you begin](#before-you-begin)).

1. 	When your request succeeds, the following output is in the `LogCat` or Xcode console:

	![image](images/android-custom-login-success.png)

	![image](images/ios-custom-login-success.png)
