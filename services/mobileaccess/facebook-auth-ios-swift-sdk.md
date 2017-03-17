---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

The {{site.data.keyword.amafull}} service is replaced with the {{site.data.keyword.appid_full}} service.

# Enabling Facebook authentication for iOS apps (Swift SDK)
{: #facebook-auth-ios}

To use Facebook as an identity provider in your {{site.data.keyword.amafull}} iOS applications, add and configure the iOS Platform for your Facebook application.
{: shortdesc}

## Before you begin
{: #before-you-begin}

You must have

* An instance of an {{site.data.keyword.amafull}} service and {{site.data.keyword.Bluemix_notm}} application. For more information about how to create a {{site.data.keyword.Bluemix_notm}} back-end application, see [Getting started](index.html).
* The URL of your back-end application (**App Route**). You will need this values for sending requests to the protected endpoints of your back-end application.
* Your **TenantID** value. Open your service in the  {{site.data.keyword.amashort}} dashboard. Click the **Mobile Options** button. The `tenantId` (also known as `appGUID`)  value is displayed in the **App GUID / TenantId** field. You will need this value for intializing the Authorization Manager.
* Your {{site.data.keyword.Bluemix_notm}} **Region**. You can find your current {{site.data.keyword.Bluemix_notm}} region in the header, next to the **Avatar** icon ![Avatar icon](images/face.jpg "Avatar icon"). The region value that appears should be one of the following: `US South`, `United Kingdom`, or `Sydney`, and correspond to the SDK values required for the Swift SDK: `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom`, or `BMSClient.Region.sydney`. You will need this value for initializing the {{site.data.keyword.amashort}} client.
* An iOS project that is seft up to work with CocoaPods.  For more information, see **Install CocoaPods** in  [Setting up the iOS Swift SDK](getting-started-ios-swift-sdk.html).  
   **Note:** You do not need to install the core {{site.data.keyword.amashort}}  client SDK before proceeding.
* A Facebook application on the [Facebook for Developers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developers.facebook.com){: new_window} website.

**Important:** You do not need to separately install the Facebook SDK (`com.facebook.FacebookSdk`). The Facebook SDK  installs automatically with the {{site.data.keyword.amashort}} `BMSFacebookAuthentication` pod. You can skip the **Add the Facebook SDK to your Xcode Project** step when you add or configure your app on the Facebook for Developers website.

## Configuring your Facebook Application for the iOS Platform
{: #facebook-auth-ios-config}

On the Facebook for Developers site:

1. Log in to your account on  [Facebook for Developers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developers.facebook.com){: new_window}.

1. Ensure that the iOS platform has been added to your app. When you add or configure the iOS platform  you need to supply the **bundleId** of your iOS application. To find the **bundleId** of your iOS application, look for the **Bundle Identifier** in either the `info.plist` file or Xcode project **General** tab.

  **Tip**: Consider enabling URL Scheme Suffix or Single Sign On if you are planning to use these features.

1. Click **Save Settings**.

## Configuring {{site.data.keyword.amashort}} for Facebook authentication
{: #facebook-auth-ios-configmca}

After you configure the Facebook App ID and your Facebook Application to serve iOS clients, you can enable Facebook authentication in your {{site.data.keyword.amashort}} service.

1. Open your service in the  {{site.data.keyword.amashort}} dashboard.
1. From the **Manage** tab, toggle **Authorization** on.
1. Expand the **Facebook** section.
1. Add the **Facebook Application ID** and click **Save**.

## Configuring the {{site.data.keyword.amashort}} client SDK for iOS
{: #facebook-auth-ios-sdk}

### Installing CocoaPods
{: #install-cocoapods}

1. Open Terminal and run the **pod --version** command. If CocoaPods is installed, the version number displays. You can skip to the next section to install the SDK.

1. If you do not have CocoaPods installed, run:

   ```
   sudo gem install cocoapods
   ```
   {: codeblock}

For more information, see the [CocoaPods website ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cocoapods.org/){: new_window}.

### Installing the {{site.data.keyword.amashort}} client Swift SDK with CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. If you have no `Podfile` in your iOS project, run `pod init` to create the file.

1. Edit the `Podfile` and add the following lines:

   ```
   use_frameworks!
   pod 'BMSFacebookAuthentication'
   ```
   {: codeblock}

   **Note:** If you have this line in your Pod file: `pod 'BMSSecurity'`, you must remove it. The `BMSFacebookAuthentication` pod installs all necessary frameworks.

   **Tip:** You can add `use_frameworks!` to your Xcode target instead of having it in the Podfile.

1. Save the `Podfile` and run the `pod install` command from the command line. CocoaPods installs the dependencies. The progress and which components were added are displayed.

   **Important**: You now must open your project by using the `xcworkspace` file that is generated by CocoaPods. Usually the name is `{your-project-name}.xcworkspace`.  

1. Run `open {your-project-name}.xcworkspace` from command line to open your iOS project workspace.

### Enable Keychain Sharing for iOS
{: #enable_keychain}

Enable `Keychain Sharing`. Go to the `Capabilities` tab and switch the `Keychain Sharing` to `On` in your Xcode project.

### Configuring your iOS project for Facebook Authentication
{: #facebook-auth-ios-configproject}

1. Find the `info.plist` file, usually located under `Supporting files` folder in your Xcode project.

1. Configure Facebook integration by adding the following properties to your `info.plist` file:

   ![image](images/ios-facebook-infoplist-settings.png)

   Update the URL scheme and FacebookAppID properties with your Facebook Application ID.

   You can also update the `info.plist` file by right-clicking the file, selecting **Open as > Source Code** and adding the following XML:

   ```XML
   <key>CFBundleURLTypes</key>
   <array>
      <dict>
         <key>CFBundleURLSchemes</key>
         <array>
            <string>fb{your-facebook-application-id}</string>
         </array>
      </dict>
   </array>
   <key>FacebookAppID</key>
   <string>{your-facebook-application-id}</string>
   <key>FacebookDisplayName</key>
   <string>{your-faceebook-application-name}</string>
   <key>LSApplicationQueriesSchemes</key>
   <array>
      <string>fbauth</string>
      <string>fbauth2</string>
   </array>
   <key>NSAppTransportSecurity</key>
   <dict>
      <key>NSExceptionDomains</key>
      <dict>
         <key>facebook.com</key>
         <dict>
            <key>NSIncludesSubdomains</key>
            <true/>                
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
         </dict>
         <key>fbcdn.net</key>
         <dict>
            <key>NSIncludesSubdomains</key>
            <true/>
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
         </dict>
         <key>akamaihd.net</key>
         <dict>
            <key>NSIncludesSubdomains</key>
            <true/>
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
         </dict>
      </dict>
   </dict>
   ```
   {: codeblock}

   Update the `CFBundleURLSchemes` and `FacebookappID` properties with your Facebook Application ID. Update the `FacebookDisplayName` with the name of your Facebook application.

   **Important**: Make sure you are not overriding any existing properties in  the `info.plist` file. If you have overlapping properties, you must merge manually. For more information, see [Configure Xcode Project ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developers.facebook.com/docs/ios/getting-started/){: new_window} and [Preparing Your Apps for iOS9 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developers.facebook.com/docs/ios/ios9){: new_window}.

## Initializing the {{site.data.keyword.amashort}} client Swift SDK
{: #facebook-auth-ios-initalize-swift}

Initialize the client SDK by passing the `tenantId`.

A common, though not mandatory, place to put the initialization code is in the `application:didFinishLaunchingWithOptions` method of your application delegate.

1. Import required framework in the class that you want to use {{site.data.keyword.amashort}} client SDK by adding the following headers:

   ```swift
   import UIKit
   import BMSCore
   import BMSSecurity
   ```
   {: codeblock}

1. Initialize the client SDK.

   ```Swift
   let tenantId = "<serviceTenantID>"
   let regionName = <applicationBluemixRegion>

   func application(_ application: UIApplication,
      didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
      let mcaAuthManager = MCAAuthorizationManager.sharedInstance
      mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
      //the regionName should be one of the following: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney
      BMSClient.sharedInstance.authorizationManager = mcaAuthManager
      FacebookAuthenticationManager.sharedInstance.register()
   }
   ```
   {: codeblock}

   In the code:

   * Replace `<applicationBluemixRegion>` with the region where your {{site.data.keyword.Bluemix_notm}} application is hosted.
   * Replace `tenantId` with the **TenantId/App GUID** value.

   For more information about these values, see [Before you begin](#before-you-begin).

1. Notify the Facebook SDK about the app activation and register the Facebook Authentication Handler by adding the following code to the `application:didFinishLaunchingWithOptions` method in your app delegate. Add this code after you initialize the BMSClient instance and register Facebook as the authentication manager.

   ```Swift
   return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
   ```
   {: codeblock}

1. Copy the `FacebookAuthenticationManager.swift` file from the `BMSFacebookAuthentication` pod source files to your project directory.

1. Add the following code to your app delegate.

   ```Swift
   func application(_ app: UIApplication,
      open url: URL,
      options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool{
         return FacebookAuthenticationManager.sharedInstance.onOpenURL(app, open: url, options: options)
      }
   ```
   {: codeblock}

## Testing the authentication
{: #facebook-auth-ios-testing}

After the client SDK is initialized and Facebook Authentication Manager is registered, you can start making requests to your mobile back-end application.

### Before you begin
{: #facebook-auth-ios-testing-before}

You must be using the {{site.data.keyword.mobilefirstbp}} boilerplate and already have a resource protected by {{site.data.keyword.amashort}} at the `/protected` endpoint. If you need to set up a `/protected` endpoint, see [Protecting resources](protecting-resources.html).

1. Try to send a request to protected endpoint of your newly created mobile back-end application in your browser. Open the following URL: `{applicationRoute}/protected`, replacing the `{applicationRoute}` with the value you retrieved from the **Mobile options** (see [Configuring Mobile Client Access for Facebook authentication](#facebook-auth-ios-configmca)).
For example: `http://my-mobile-backend.mybluemix.net/protected`
<br/>The `/protected` endpoint of a mobile back-end application that was created with MobileFirst Services Starter boilerplate is protected with {{site.data.keyword.amashort}}. An `Unauthorized` message is returned in your browser. This message is returned because this endpoint can be accessed only by mobile applications that are instrumented with {{site.data.keyword.amashort}} client SDK.

1. Use your iOS application to make a request to the same endpoint.

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

1. Run your application. A Facebook login screen pops up.

   ![image](images/ios-facebook-login.png)

   This screen might look slightly different if you are not currently logged in to Facebook.

1. Click **OK** to authorize {{site.data.keyword.amashort}}  to use your Facebook user identity for authentication purposes.

1. 	When your request succeeds, the following output is displayed in the Xcode console:

   ```
   response:Optional("Hello, this is a protected resouce of the mobile backend application!"), no error
   ```
   {: screen}

1. You can also add logout functionality by adding the following code:

   ```
   FacebookAuthenticationManager.sharedInstance.logout(callBack)
   ```
   {: codeblock}

   If you call this code after a user is logged in with Facebook, and the user tries to log in again, they are prompted to authorize {{site.data.keyword.amashort}} to use Facebook for authentication purposes.

   To switch users, you must call this code and the user must log out from Facebook in their browser.

   Passing `callBack` to the logout function is optional. You can also pass `nil`.
