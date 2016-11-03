---

copyright:
  years: 2016
lastupdated: "2016-11-01"

---
{:screen:  .screen}
{:shortdesc: .shortdesc}

# Enabling Google authentication for iOS apps (Swift SDK)
{: #google-auth-ios}

Use Google Sign-In to authenticate users on your {{site.data.keyword.amafull}} iOS Swift app. The newly released {{site.data.keyword.amashort}} Swift SDK  adds to and improves the functionality provided by the existing Mobile Client Access Objective-C SDK.

**Note:** While the Objective-C SDK remains fully supported, and is still considered the primary SDK for  {{site.data.keyword.Bluemix_notm}} Mobile Services, there are plans to discontinue the Objective-C SDK later this year in favor of this new Swift SDK.



## Before you begin
{: #before-you-begin}
You must have:

* An instance of an {{site.data.keyword.amafull}} service and {{site.data.keyword.Bluemix_notm}} application. For more information about how to create a {{site.data.keyword.Bluemix_notm}} back-end application, see [Getting started](index.html).
* The URL of your back-end application (**App Route**). You will need this values for sending requests to the protected endpoints of your back-end application.
* Your **TenantID** value. Open your service in the  {{site.data.keyword.amashort}} dashboard. Click the **Mobile Options** button. The `tenantId` (also known as `appGUID`)  value is displayed in the **App GUID / TenantId** field. You will need this value for intializing the Authorization Manager.
* Your {{site.data.keyword.Bluemix_notm}} **Region**. You can find your current {{site.data.keyword.Bluemix_notm}} region in the header, next to the **Avatar** icon ![Avatar icon](images/face.jpg "Avatar icon"). The region value that appears should be one of the following: **US South**, **United Kingdom**, or **Sydney**, and correspond to the values required in the code:  `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom`, or `BMSClient.Region.sydney`.
* An iOS project in Xcode. It does not need to be instrumented with the {{site.data.keyword.amashort}} client SDK.  



## Preparing your app for Google Sign-In
{: #google-sign-in-ios}

Prepare your app for Google sign-in by following the instructions provided by Google at [Google Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start-integrating).

This process:
* prepares a new project on the Google Developers site,
* creates the `GoogleService-Info.plist` file and the `REVERSE_CLIENT_ID` value to add to your Xcode project, and
* creates the **Google Client ID** to add to your {{site.data.keyword.Bluemix_notm}} back-end application.

The following steps give you a brief outline of the tasks necessary for preparing your app.

**Note:** It is not necessary to add the Google Sign-In CocoaPod. The necessary SDK is added by the `BMSGoogleAuthentication` CocoaPod.

1. Note the **Bundle Identifier** in your Xcode project from the **Identity** section of the **General** tab of the main target. You need it to create your  Google Sign-In project.

1. Create a project on Google Developer for Google Sign-In for iOS at https://developers.google.com/mobile/add?platform=ios.

2. Add the Google Sign-In API to your project.

3. Retrieve the `GoogleService-Info.plist`.

  **Important:** When you get the `GoogleService-Info.plist` file, open it and note the `CLIENT_ID` value. You need this value later to configure {{site.data.keyword.amashort}} back-end application.

1. Add the `GoogleService-Info.plist` file to your Xcode project. For more information, see [Add the configuration file to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config).

1. Update the URL Schemes in your Xcode project with your `REVERSE_CLIENT_ID` and bundle identifier. For more information, see [Add URL schemes to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add_a_url_scheme_to_your_project).

1. Update your app's `project-Bridging-Header.h` file with the following code:

 ```
 #import <Google/SignIn.h>
 ```
 {: codeblock}

 For more information about updating the bridging header file,  [Enable sign-in](https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in).

## Configuring {{site.data.keyword.amashort}} for Google authentication
{: #google-auth-ios-config}

Now that you have an iOS client ID, you can enable Google authentication in the {{site.data.keyword.amashort}} service.

1. Open your service in the {{site.data.keyword.amashort}} dashboard.
1. From the **Manage** tab, toggle **Authorization** on.
1. Expand the **Google** section.
1. In **Application ID for iOS**, specify the `CLIENT_ID` value you obtained from the `GoogleService-Info.plist` file.
1. Click **Save**.

## Configuring the {{site.data.keyword.amashort}} client SDK for iOS
{: #google-auth-ios-sdk}

### Installing CocoaPods
{: #install-cocoapods}

1. Open Terminal and run the **pod --version** command. If you already have CocoaPods installed, the version number displays. You can skip to the next section to install the SDK.

1. If you do not have CocoaPods installed, run:
```
sudo gem install cocoapods
```
{: codeblock}

For more information, see the [CocoaPods website](https://cocoapods.org/).

### Installing the {{site.data.keyword.amashort}} client Swift SDK with CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. If you have no `Podfile` in your iOS project, run `pod init` to create the file.

1. Edit the `Podfile` and add the following lines to the relevant target:

 ```
 use_frameworks!
 pod 'BMSGoogleAuthentication'
 ```
 {: codeblock}

 **Note:** If you have already installed the {{site.data.keyword.amashort}} core SDK, you can remove this line: `pod 'BMSSecurity'`. The `BMSGoogleAuthentication` pod installs all necessary frameworks.

 **Tip:** You can add `use_frameworks!` to your Xcode target instead of having it in the Podfile.

1. Save the `Podfile` and run `pod install` from the command line. CocoaPods  installs the dependencies. You will see the progress and which components were added.

 **Important**: You now must open your project by using the `xcworkspace` file that is generated by CocoaPods. Usually the name is `{your-project-name}.xcworkspace`.  

1. Run `open {your-project-name}.xcworkspace` from the command line to open your iOS project workspace.

1. Copy the `GoogleAuthenticationManager.swift` file from the `BMSGoogleAuthentication` pod source files to your project directory.

### Enable Keychain Sharing for iOS
{: #enable_keychain}

Enable `Keychain Sharing`. Go to the `Capabilities` tab and switch the `Keychain Sharing` to `On` in your Xcode project.


## Initializing the {{site.data.keyword.amashort}} client Swift SDK
{: #google-auth-ios-initialize}

To use the {{site.data.keyword.amashort}} client SDK,  initialize it by passing the `tenantID` parameter.

A common, though not mandatory, place to put the initialization code is in the `application:didFinishLaunchingWithOptions` method of your application delegate.

1. Import the required frameworks in the class where you want to use the {{site.data.keyword.amashort}} client SDK. Add the following headers:

	 ```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {

	    let mcaAuthManager = MCAAuthorizationManager.sharedInstance
	    		mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
	 ///the regionName should be one of the following: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney   
	    BMSClient.sharedInstance.authorizationManager = mcaAuthManager
		GoogleAuthenticationManager.sharedInstance.register()
		return true
	}

	// [START openurl]
	    func application(_ application: UIApplication,
			     open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
		return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url,
			sourceApplication: sourceApplication, annotation: annotation)
	    }

	    @available(iOS 9.0, *)
	    func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any]) -> Bool {
		return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, options: options)
	    }

	 ```

 In the code:
 	* Replace  `<serviceTenantID>` with the value you retrieved from the **Mobile options**.
	* Replace `<applicationBluemixRegion>` with your {{site.data.keyword.Bluemix_notm}} **Region**. 
	
	For more information on obtaining these values see  [Before you begin](#before-you-begin).


## Testing the authentication
{: #google-auth-ios-testing}

After the client SDK is initialized and Google Authentication Manager is registered, you can start making requests to your mobile back-end application.

### Before you begin
{: #google-auth-ios-testing-before}

You must be using the {{site.data.keyword.mobilefirstbp}}  boilerplate and already have a resource protected by {{site.data.keyword.amashort}} at the `/protected` endpoint. If you need to set up a `/protected` endpoint, see [Protecting resources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Try to send a request to protected endpoint of your mobile back-end application in your desktop browser by opening `{applicationRoute}/protected`.  For example `http://my-mobile-backend.mybluemix.net/protected`.

1. The `/protected` endpoint of a mobile back-end application created with MobileFirst Services Boilerplate is protected with {{site.data.keyword.amashort}}, therefore it can only be accessed by mobile applications instrumented with {{site.data.keyword.amashort}} client SDK. As a result you will see `Unauthorized` in your desktop browser.

1. Use your iOS application to make request to the same endpoint.

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
1. Run your application. You will see a Google Login screen pop-up

 ![image](images/ios-google-login.png)

1. When you log in and click **OK**, you're authorizing {{site.data.keyword.amashort}} to use your Google user identity for authentication purposes.

1. Your request should succeed. The following output appears in the log.

 ```
response:Optional("Hello, this is a protected resource of the mobile backend application!"), no error

 ```
{: screen}

1. You can also add logout functionality by adding the following code:

 ```
 GoogleAuthenticationManager.sharedInstance.logout(callBack)
 ```

  If you call this code after a user is logged in with Google and the user tries to log in again, they are prompted to authorize {{site.data.keyword.amashort}} to use Google for authentication purposes. At that point, the user can click the user name <!--in the upper-right corner of the screen--> to select and log in with another user.

   Passing `callBack` to the logout function is optional. You can also pass `nil`.
