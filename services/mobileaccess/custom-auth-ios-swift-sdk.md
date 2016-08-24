---

copyright:
  years: 2016

---

# Configuring custom authentication for your {{site.data.keyword.amashort}} iOS (Swift SDK) app

{: #custom-ios}

Last updated: 23 August 2016
{: .last-updated}


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

 1. Open your app in the {{site.data.keyword.Bluemix_notm}} dashboard.

 1. Click **Mobile Options** and take note of **Route** (*applicationRoute*) and **AppGuid** (*applicationGUID*). You need these values when you initialize the SDK.

 1. Click the {{site.data.keyword.amashort}} tile. The {{site.data.keyword.amashort}} dashboard loads.

 1. Click the **Custom** tile.

 1. In **Realm name**, specify your custom authentication realm.

 1. In **URL**, specify your applicationRoute.

 1. Click **Save**.




### Initializing the client SDK
{: #custom-ios-sdk-initialize}

Initialize the SDK by passing the `applicationRoute`and `applicationGUID` parameters. A common, though not mandatory, place to put the initialization code is in the `application:didFinishLaunchingWithOptions` method of your application delegate

1. Get your application parameter values. Open your app in the {{site.data.keyword.Bluemix_notm}} dashboard. Click **Mobile Options**. The `applicationRoute` and `applicationGUID` values are displayed in the **Route** and **AppGuid** fields.

1. Import the required frameworks in the class where you want to use {{site.data.keyword.amashort}} client SDK.

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
```

1. Initialize the {{site.data.keyword.amashort}} client SDK, change the authorization manager to the  `MCAAuthorizationManager`, and define and register an authentication delegate.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"
 let customRealm = "<yourProtectedRealm>"
 let tenantId = "<MCAServiceTenantId>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<applicationBluemixRegion>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

  //Auth delegate for handling custom challenge
 class MyAuthDelegate : AuthenticationDelegate {
      func onAuthenticationChallengeReceived(authContext: AuthenticationContext, challenge: AnyObject){
          print("onAuthenticationChallengeReceived")
              let answer = <An answer to the challenge sent by the backend (Should be of type [String:AnyObject])>
              authContext.submitAuthenticationChallengeAnswer(answer)
      }

      func onAuthenticationSuccess(info: AnyObject?) {
           print("onAuthenticationSuccess info = \(info)")
           print("onAuthenticationSuccess")
      }

      func onAuthenticationFailure(info: AnyObject?){
        print("onAuthenticationFailure info = \(info)")
        print("onAuthenticationFailure")
      }
  }

  let delegate = MyAuthDelegate()
  let mcaAuthManager = MCAAuthorizationManager.sharedInstance
  mcaAuthManager.initialize(tenantId: tenantId)
 do {
      try mcaAuthManager.registerAuthenticationDelegate(delegate, realm: customRealm)
  } catch {
      print("error with register: \(error)")
  }
 return true
 }   
 ```

In the code:
 * Replace the `<applicationRoute>` and `<applicationGUID>` with values for **Route** and **AppGuid** that you obtained from **Mobile   Options** in the {{site.data.keyword.Bluemix_notm}} dashboard. 

* Replace `<applicationBluemixRegion>` with the region where your {{site.data.keyword.Bluemix_notm}} application is hosted. To view your {{site.data.keyword.Bluemix_notm}} region, click the Avatar icon ![Avatar icon](images/face.jpg "Avatar icon")  in the menu bar to open the Account and Support widget.

* Replace `<yourProtectedRealm>` with the **Realm name** value you defined in the **Custom** tile of {{site.data.keyword.amashort}} dashboard.
  
* Replace `<MCAServiceTenantId>` with the `tenantId` value. You can find this value by clicking the **Show Credentials** button on the {{site.data.keyword.amashort}} service tile.
   
  
## Testing the authentication
{: #custom-ios-testing}

After you initialize the client SDK and register a custom authentication delegate, you can start making requests to your mobile back-end application.

### Before you begin
{: #custom-ios-testing-before}

 You must have an application that was created with the {{site.data.keyword.mobilefirstbp}} boilerplate, and have a resource that is protected by {{site.data.keyword.amashort}} at the `/protected` endpoint.

1. Send a request to protected endpoint of your mobile back-end application in your browser by opening `{applicationRoute}/protected`, for example `http://my-mobile-backend.mybluemix.net/protected`.
  The `/protected` endpoint of a mobile back-end application that is created with the {{site.data.keyword.mobilefirstbp}} boilerplate is protected with {{site.data.keyword.amashort}}. The endpoint can  be accessed by only mobile applications that are instrumented with the {{site.data.keyword.amashort}} client SDK. As a result, an `Unauthorized` message displays in your browser.

1. Use your iOS application to make request to the same endpoint. Add the following code after you initialize `BMSClient` and register your custom authentication delegate:

 ```Swift
 let customResourceURL = "<your protected resource's path>"
 let request = Request(url: customResourceURL, method: HttpMethod.GET)
 let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in
  if error == nil {
      print ("response:\(response?.responseText), no error")
  } else {
      print ("error: \(error)")
  }
 }

 request.sendWithCompletionHandler(callBack)
 ```

1. 	When your requests succeeds, you see the following output in the Xcode console:

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
