---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:pre: .pre}


# Setting up the iOS Swift SDK
{: #getting-started-ios}

Build your Swift applications with the {{site.data.keyword.appid_short}} client SDK, initialize the SDK, authenticate users, and make requests to protected and unprotected resources.
{:shortdesc}


## Before you begin
{: #before-you-begin}

You need the following information:
  * An instance of {{site.data.keyword.appid_short_notm}}.
  * Your Tenant ID.
    * In the **Service Credentials** tab of your service dashboard, click **View Credentials**. Your Tenant ID is displayed in the **TenantID** field. This value is used for initializing your app.
  * Your {{site.data.keyword.Bluemix_notm}} Region.
  You can find your region by looking in the UI. The value is used for initializing your app.
    <table> <caption> Table 1. {{site.data.keyword.Bluemix_notm}} regions and corresponding SDK values </caption>
    <tr>
      <th> Bluemix Region </th>
      <th> SDK value </th>
    </tr>
    <tr>
      <td> US South </td>
      <td> BMSClient.Region.usSouth </td>
    </tr>
    <tr>
      <td> Sydney </td>
      <td> BMSClient.Region.sydney </td>
    </tr>
    <tr>
      <td> United Kingdom </td>
      <td> BMSClient.Region.unitedKingdom </td>
    </tr>
  </table>

  * An Xcode project (version 8.1 or higher).
  * CocoaPods (version 1.1.0 or higher).


## Installing the {{site.data.keyword.appid_short_notm}} client SDK
{: #install-appid-sdk}

The {{site.data.keyword.appid_short_notm}} client SDK is distributed with CocoaPods, a dependency manager for Swift and Objective-C Cocoa projects. CocoaPods downloads artifacts, and makes them available to your project.

1. Create an Xcode project, or open an existing project.
2. Open, or create, the Podfile in the project's directory.
3. Under your project's target add a dependency for the 'BluemixAppID' pod. Make sure the `use_frameworks!` command is also under your target.

  For example:

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {:pre}

4. To download the `BluemixAppID` dependency, run the following command:

  ```swift
  pod install --repo-update
  ```
  {:pre}

6. Open your Xcode project and enable keychain sharing. Under **Project Settings**, click **Capabilities** > **Keychain Sharing**.
7. Under **Project Settings** > **Info** > **URL Types**, add a URL Type. Fill both the **Identifier** text box and the **URL Scheme** text box with this value: $(PRODUCT_BUNDLE_IDENTIFIER)


## Initializing the {{site.data.keyword.appid_short_notm}} client SDK
{: #initialize-client-sdk}

1. Add the following import to your `AppDelegate.swift` file:

  ```swift
  import BluemixAppID
  ```
  {:pre}

2. Initialize the client SDK by passing tenant ID and region parameters to the initialize method. A common, though not mandatory, place to put the initialization code is in the application:didFinishLaunchingWithOptions: method of the AppDelegate in your Swift application.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.<region>)
  ```
  {:pre}

  * Replace ״tenantId״ with the tenant ID for your App ID service.
  * Replace ״region״ with your {{site.data.keyword.appid_short_notm}} region.

3. Add the following code to your AppDelegate file.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {:pre}

## Authenticate users by using the login widget
{: #authenticate-login}

After the {{site.data.keyword.appid_short_notm}} client SDK is initialized, you can authenticate your users by running the login widget. The login widget default configuration uses Facebook, Google, or both as authentication options. If you configure only one of them the login widget does not launch and the user is redirected to the configured IDP authentication screen.



1. Add the following import to the file in which you want to use the SDK.

  ```swift
  import BluemixAppID
  ```
  {:pre}

2. Run the following command to launch the widget.

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //User authenticated
      }

      public func onAuthorizationCanceled() {
          //Authentication canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Exception occurred
      }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {:pre}

## Accessing user attributes
{: #accessing}

When obtaining an access token, it is possible to gain access to the user protected attributes endpoint. This is done by using the following API methods:

  ```
  func setAttribute(key: String, value: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func setAttribute(key: String, value: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  ```
  {:pre}

When an access token is not explicitly passed, {{site.data.keyword.appid_short_notm}} uses the last received token.

For example, you can invoke this code to set a new attribute, or override an existing one:

  ```
  AppID.sharedInstance.userAttributeManager?.setAttribute("key", "value", completionHandler: { (error, result) in
      if error = nil {
          //Attributes recieved as a Dictionary
      } else {
          // An error has occurred
      }
  })
  ```
  {:pre}


### Anonymous login
{: #anonymous notoc}

With {{site.data.keyword.appid_short_notm}} you can log in anonymously, see [anonymous identity](/docs/services/appid/user-profile.html#anonymous).

  ```
  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //User authenticated
      }

      public func onAuthorizationCanceled() {
          //Authentication canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Error occurred
      }
   }

  AppID.sharedInstance.loginAnonymously( authorizationDelegate: delegate())`
  ```
  {:pre}

### Progressive authentication
{: #progressive notoc}

When you hold an anonymous access token, the user can become an identified user by passing it to the loginWidget.launch method:

  ```
  func launch(accessTokenString: String? , delegate: AuthorizationDelegate)
  ```
  {:pre}

After an anonymous login, progressive authentication occurs even if the login widget is called without passing an access token because the service used the last received token. If you want to clear your stored tokens, run the following command:

  ```
  var appIDAuthorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)
  appIDAuthorizationManager.clearAuthorizationData()
  ```
  {:pre}



## Next steps
{: #next-steps}

{{site.data.keyword.appid_short_notm}} provides a default configuration when you initially set up your identity providers. You can use the default configuration in development mode only. Before you publish your application, update the default [Facebook](/docs/services/appid/identity-providers.html#facebook) and [Google](/docs/services/appid/identity-providers.html#google) configuration to your own credentials.
