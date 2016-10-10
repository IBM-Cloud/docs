---

copyright:
  years: 2016
lastupdated: "2016-10-09"
---

# Configuring custom authentication for your {{site.data.keyword.amashort}} iOS (Swift SDK) app
{: #custom-ios}

Configure your iOS application that is using custom authentication to use the {{site.data.keyword.amafull}} client SDK and connect your application to {{site.data.keyword.Bluemix}}.  The newly released {{site.data.keyword.amashort}} Swift SDK  adds to and improves on the functionality provided by the existing Mobile Client Access Objective-C SDK.

**Note:** While the Objective-C SDK remains fully supported, and is still considered the primary SDK for  {{site.data.keyword.Bluemix_notm}} Mobile Services, there are plans to discontinue the Objective-C SDK later this year in favor of this new Swift SDK.

## Before you begin
{: #before-you-begin}

You must have a resource that is protected by an instance of the {{site.data.keyword.amashort}} service that is configured to use a custom identity provider.  Your mobile app also must be instrumented with the {{site.data.keyword.amashort}} client SDK.  For more information, see the following information:
 * [Getting started with {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/index.html)
 * [Setting up the iOS Swift SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)
 * [Using a custom identity provider](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Creating a custom identity provider](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configuring {{site.data.keyword.amashort}} for custom authentication](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## Configuring {{site.data.keyword.amashort}} for custom authentication
 {: #custom-auth-ios-configmca}

 1. Open your service dashboard.
 
 1. Click **Mobile options** and take note of the **Route** (*applicationRoute*) and **App GUID / TenantId** (*serviceTenantID*). You need these values when you initialize the SDK, and send requests to the back-end application.

 1. Click the {{site.data.keyword.amashort}} tile. The {{site.data.keyword.amashort}} dashboard loads.

 1. Click the **Custom** tile.

 1. In **Realm name**, specify your custom authentication realm.

 1. In **URL**, specify your applicationRoute.

 1. Click **Save**.




### Initializing the client SDK
{: #custom-ios-sdk-initialize}

Initialize the SDK by passing the `applicationGUID` (tenantId) parameter. A common, though not mandatory, place to put the initialization code is in the `application:didFinishLaunchingWithOptions` method of your application delegate

1. Import the required frameworks in the class where you want to use {{site.data.keyword.amashort}} client SDK.

	```Swift
	import UIKit
	import BMSCore
	import BMSSecurity
	```

1. Initialize the {{site.data.keyword.amashort}} client SDK, change the authorization manager to the  `MCAAuthorizationManager`, and define and register an authentication delegate.

```Swift

	let tenantId = "<serviceTenantID>"
	let regionName = "<applicationBluemixRegion>"
	let customRealm = “<yourProtectedRealm>”

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: 
		[UIApplicationLaunchOptionsKey: Any]?) -> Bool {

		let mcaAuthManager = MCAAuthorizationManager.sharedInstance
	    		mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
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

In the code:

* Replace `"<applicationBluemixRegion>"` with the region where your {{site.data.keyword.Bluemix_notm}} application is hosted. To view your {{site.data.keyword.Bluemix_notm}} region, click the Avatar icon ![Avatar icon](images/face.jpg "Avatar icon")  in the menu bar to open the **Account and Support** widget.  The region value should be one of the following: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY`, or `BMSClient.REGION_UK`.
* Replace `"<yourProtectedRealm>"` with the **Realm name** value you defined in the **Custom** tile of {{site.data.keyword.amashort}} dashboard. 
* Replace `"<serviceTenantID>"` with the **tenantId** value retrieved from **Mobile options**. See [Configuring Mobile Client Access for custom authentication](#custom-auth-ios-configmca).

### Initializing the client SDK
{: #custom-ios-sdk-initialize}
   
  
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

1. You can also add logout functionality by adding the following code:

	 ```
	 MCAAuthorizationManager.sharedInstance.logout(callBack)
	 ```  

 If you call this code after a user is logged in, the user is logged out. When the user tries to log in again, they must answer the challenge received from the server again.

 Passing `callBack` to the logout function is optional. You can also pass `nil`.
