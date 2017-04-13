---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-06"

---

{:codeblock:.codeblock}

**Important: The {{site.data.keyword.amafull}} service is replaced with the {{site.data.keyword.appid_full}} service.**

# Configuring custom authentication for your Mobile Client Access iOS (Swift SDK) app
{: #custom-ios}

Configure your iOS application that is using custom authentication to use the {{site.data.keyword.amafull}} client SDK and connect your application to {{site.data.keyword.Bluemix}}.  


## Before you begin
{: #before-you-begin}

Before you begin you must have:

* A resource that is protected by an instance of the {{site.data.keyword.amashort}} service that is configured to use a custom identity provider (see [Configuring custom authentication](custom-auth-config-mca.html)).  
* Your **TenantID** value. Open your service in the  {{site.data.keyword.amashort}} dashboard. Click the **Mobile Options** button. The `tenantId` (also known as `appGUID`)  value is displayed in the **App GUID / TenantId** field. You will need this value for intializing the Authorization Manager.
* Your **Realm** name. This is the value you you specificed in the **Realm Name** field of the **Custom** section in the **Management** tab of the {{site.data.keyword.amashort}} dashboard.
* The URL of your back-end application (**App Route**). You will need this values for sending requests to the protected endpoints of your back-end application.
* Your {{site.data.keyword.Bluemix_notm}} **Region**. You can find your current {{site.data.keyword.Bluemix_notm}} region in the header, next to the **Avatar** icon ![Avatar icon](images/face.jpg "Avatar icon"). The region value that appears should be one of the following: **US South**, **United Kingdom**, or **Sydney**, and correspond to the constants required in the code:  `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom`, or `BMSClient.Region.sydney`.

For more information, see the following information:
 * [Getting started with {{site.data.keyword.amashort}}](index.html)
 * [Setting up the iOS Swift SDK](getting-started-ios-swift-sdk.html)
 * [Using a custom identity provider](custom-auth.html)
 * [Creating a custom identity provider](custom-auth-identity-provider.html)
 * [Configuring {{site.data.keyword.amashort}} for custom authentication](custom-auth-config-mca.html)

### Enable Keychain Sharing for iOS
{: #enable_keychain}

Enable `Keychain Sharing`. Go to the `Capabilities` tab and switch the `Keychain Sharing` to `On` in your Xcode project.


### Initializing the client SDK
{: #custom-ios-sdk-initialize}

Initialize the SDK by passing the `applicationGUID` (**TenantId**) parameter. A common, though not mandatory, place to put the initialization code is in the `application:didFinishLaunchingWithOptions` method of your application delegate.

1. Import the required frameworks in the class where you want to use {{site.data.keyword.amashort}} client SDK.

	```Swift
	import UIKit
	import BMSCore
	import BMSSecurity
	```
	{: codeblock}

1. Initialize the {{site.data.keyword.amashort}} client SDK, change the authorization manager to the  `MCAAuthorizationManager`, and define and register an authentication delegate.

```Swift

	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>
	let customRealm = "<yourProtectedRealm>"

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions:
		[UIApplicationLaunchOptionsKey: Any]?) -> Bool {

		let mcaAuthManager = MCAAuthorizationManager.sharedInstance
	    		mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
	 //the regionName should be one of the following BMSClient.Region constants: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney   
		BMSClient.sharedInstance.authorizationManager = mcaAuthManager

	//Auth delegate for handling custom challenge
	     class MyAuthDelegate : AuthenticationDelegate {
		func onAuthenticationChallengeReceived(_ authContext: AuthenticationContext, challenge: AnyObject){
		    print("onAuthenticationChallengeReceived")
		    let answer = try? Utils.parseJsonStringtoDictionary( "{\"userName\":\"" + "test" + "\",\"password\":\"" + "test" + "\"}")
			authContext.submitAuthenticationChallengeAnswer(answer)
		}

		func onAuthenticationSuccess(_ info: AnyObject?) {
		    print("onAuthenticationSuccess info = \(info)")
		    print("onAuthenticationSuccess")
		}

		func onAuthenticationFailure(_ info: AnyObject?){
		     print("onAuthenticationFailure info = \(info)")
		     print("onAuthenticationFailure")
		}
	     }

	     let delegate = MyAuthDelegate()
	     mcaAuthManager.registerAuthenticationDelegate(delegate, realm: customRealm)

	     return true
	}


```
{: codeblock}

In the code:
* Replace `MCAServiceTenantId` with the **TenantId** value and `<applicationBluemixRegion>` with your {{site.data.keyword.amashort}} **Region** (see [Before you begin](##before-you-begin)).
* Use the `realmName` that you specified in the {{site.data.keyword.amashort}} dashboard (see [Configuring custom authentication](custom-auth-config-mca.html)).
* Replace `<applicationBluemixRegion>` with the region where your {{site.data.keyword.Bluemix_notm}} application is hosted. To view your {{site.data.keyword.Bluemix_notm}} region, click the Avatar icon ![Avatar icon](images/face.jpg "Avatar icon")  in the menu bar to open the **Account and Support** widget.  The region value that appears should be one of the following: **US South**, **United Kingdom**, or **Sydney**, and correspond to the constants required in the code:  `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom`, or `BMSClient.Region.sydney`.


## Testing the authentication
{: #custom-ios-testing}

After you initialize the client SDK and register a custom authentication delegate, you can start making requests to your mobile back-end application.

### Before you begin
{: #custom-ios-testing-before}

 You must have an application that was created with the {{site.data.keyword.mobilefirstbp}} boilerplate, and have a resource that is protected by {{site.data.keyword.amashort}} at the `/protected` endpoint.

1. Send a request to protected endpoint of your mobile back-end application in your browser by opening `{applicationRoute}/protected`. Replace the   `{applicationRoute}` with the value retrieved from the **Mobile options** (see [Configuring Mobile Client Access for custom authentication](#custom-auth-ios-configmca)). For example `http://my-mobile-backend.mybluemix.net/protected`.

 The `/protected` endpoint of a mobile back-end application that is created with the {{site.data.keyword.mobilefirstbp}} boilerplate is protected with {{site.data.keyword.amashort}}. The endpoint can  be accessed by only mobile applications that are instrumented with the {{site.data.keyword.amashort}} client SDK. As a result, an `Unauthorized` message displays in your browser.

1. Use your iOS application to make request to the same endpoint. Add the following code after you initialize `BMSClient` and register your custom authentication delegate:

    ```Swift

	let protectedResourceURL = "<your protected resource absolute path>"
	let request = Request(url: protectedResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
	   if error == nil {
	       print ("response:\(response?.responseText), no error")
	    } else {
	       print ("error: \(error)")
	    }
	}

	request.send(completionHandler: callBack)
     ```
     {: codeblock}

1. When your requests succeeds, you see the following output in the Xcode console:

	 ```
	 onAuthenticationSuccess info = Optional({
	     attributes =     {
	     };
	     deviceId = don;
	     displayName = "Don+Lon";
	     isUserAuthenticated = 1;
	     userId = don;
	 })
	 response:Optional("Hello Don Lon"), no error
	 ```
	 {: codeblock}

1. You can also add logout functionality by adding the following code:

	 ```
	 MCAAuthorizationManager.sharedInstance.logout(callBack)
	 ```
	 {: codeblock}

 If you call this code after a user is logged in, the user is logged out. When the user tries to log in again, they must answer the challenge received from the server again.

 Passing `callBack` to the logout function is optional. You can also pass `nil`.
