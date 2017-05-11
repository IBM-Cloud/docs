---

copyright:
  years: 2017
lastupdated: "2017-05-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Adding {{site.data.keyword.appid_short_notm}} to an existing app

You can use App ID with your existing application to authenticate and store profile information about your users.


## Prerequisites

* An existing iOS Swift, Android, Node.js, or Swift application.
* An existing instance of {{site.data.keyword.appid_short_notm}}.


## Adding {{site.data.keyword.appid_short_notm}} to an existing Android app

1. Add the JitPack repository to your root build.gradle file.

  ```gradle
  allprojects {
      		repositories {
         	 ...
         	 maven { url 'https://jitpack.io' }
      		}
  }
  ```
  {: pre}

2. Open the build.gradle file for your application, find the dependencies section of the file, and add a compile dependency for the {{site.data.keyword.appid_short_notm}} client SDK.

  ```gradle
  dependencies {
      compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
  }
  ```
  {: pre}

3. Find the defaultConfig section and add the following line of code.

  ```gradle
  defaultConfig {
                         ...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: pre}

4. Synchronize your project with Gradle.
5. Initialize the client SDK by passing the context, tenant ID, and region parameters to the initialize method. A common, though not mandatory, place to put the initialization code is in the onCreate method of the main activity in your Android application.

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: pre}

  <table>
  <caption> Command components explained </caption>
    <tr>
      <th> Components </th>
      <th> Description </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> You can find this value by clicking **View credentials** in the **service credentials** tab of your service dashboard. </td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> You can find your region in the UI. Options are `AppID.REGION_US_SOUTH`, `AppID.REGION_UK`, or `AppID.REGION_Sydney`. </td>
    </tr>
  </table>

6. After the {{site.data.keyword.appid_short_notm}} client SDK is initialized, you can authenticate your users by running the login widget.

  ```Java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launch(this, new AuthorizationListener() {
          @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
            //Exception occurred
          }

          @Override
          public void onAuthorizationCanceled () {
            //Authentication canceled by the user
          }

          @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
            //User authenticated
          }
        });
  ```
  {: pre}

## Adding {{site.data.keyword.appid_short_notm}} to an existing iOS Swift App

1. Open the podfile in the project's directory.
2. Under your project's target, add a dependency for the 'BluemixAppID' pod. Be sure the `use_frameworks!` command is also under your target.
3. To download the `BluemixAppID` dependency, run the following command.

  ```
  pod install --repo-update
  ```
  {: pre}

4. Open your Xcode project and enable keychain sharing. Under **Project Settings**, click **Capabilities** > **Keychain Sharing**.
5. Under **Project Settings** > **Info** > **URL Types**, add a **URL Type**. Fill both the **Identifier** text box and the **URL Scheme** text box with the following value.

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: pre}

6. Add the following import to your AppDelegate.swift file.

  ```swift
  import BluemixAppID
  ```
  {: pre}

7. Initialize the client SDK by passing tenant ID and region parameters to the initialize method. A common, though not mandatory, place to put the initialization code is in the application:didFinishLaunchingWithOptions: method of the AppDelegate in your application.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: pre}

  <table>
  <caption> Command components explained </caption>
    <tr>
      <th> Components </th>
      <th> Description </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> You can find this value by clicking **View credentials** in the **service credentials** tab of your service dashboard. </td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> You can find your region in the UI. Options are `AppID.REGION_US_SOUTH`, `AppID.REGION_UK`, or `AppID.REGION_Sydney`. </td>
    </tr>
  </table>

8. Add the following code to your AppDelegate file.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
         	return AppID.sharedInstance.application(application, open: url, options: options)
     	}
  ```
  {: pre}

9. After the {{site.data.keyword.appid_short_notm}} client SDK is initialized, you can authenticate your users by running the login widget.

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
  {: pre}

## Adding {{site.data.keyword.appid_short_notm}} to an existing Node.js web app

1. Add the `bluemix-appid` module to your Node.js application.

  ```javaScript
  npm install --save bluemix-appid
  ```
  {: pre}

2. Install the following modules if they are not installed already.

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: pre}

3. Add the following code to your app.js file.

  ```javaScript
  const express = require("express");
  const session = require("express-session");
  const passport = require("passport");
  const WebAppStrategy = require("bluemix-appid").WebAppStrategy;
  const app = express();
  const CALLBACK_URL = "/ibm/bluemix/appid/callback";

  // Setup express application to use express-session middleware
  // Must be configured with proper session storage for production
  // environments. See https://github.com/expressjs/session for
  // additional documentation
  app.use(session({
    secret: "123456",
    resave: true,
    saveUninitialized: true
  }));

  // Configure express application to use passportjs
  app.use(passport.initialize());
  app.use(passport.session());

  passport.use(new WebAppStrategy());

  // Configure passportjs with user serialization/deserialization. This is required
  // for authenticated session persistence across HTTP requests. See passportjs docs
  // for additional information http://passportjs.org/docs
  passport.serializeUser(function(user, cb) {
    cb(null, user);
  });

  passport.deserializeUser(function(obj, cb) {
    cb(null, obj);
  });

  // Callback to finish the authorization process. Will retrieve access and identity tokens/
  // from AppID service and redirect to either (in the following order)
  // 1. the original URL of the request that triggered authentication, as persisted in HTTP session under WebAppStrategy.ORIGINAL_URL key.
  // 2. successRedirect as specified in passport.authenticate(name, {successRedirect: "...."}) invocation
  // 3. application root ("/")
  app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));

  // Protected area. If current user is not authenticated - redirect to the login widget will be returned.
  // In case user is authenticated - a page with current user information will be returned.
  app.get("/protected", passport.authenticate(WebAppStrategy.STRATEGY_NAME), function(req, res){
  	//return the protected page with user info
  		res.json(req.user);
  });
  ```
  {: pre}

4. Redeploy your application.


## Adding {{site.data.keyword.appid_short_notm}} to an existing Swift web application

1. Open the `Package.swift` file in the directory of your Swift app and add the `appid-serversdk-swift` dependency.
  For example:

    ```swift
    import PackageDescription

    let package = Package(
       	dependencies: [
           	.Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
       		]
    )
    ```
    {: pre}

2. Add the following code to your Swift application.

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID

  // The following URLs will be used for AppID OAuth flows
  var CALLBACK_URL = "/ibm/bluemix/appid/callback"
  var LANDING_PAGE_URL = "/index.html"

  // Setup Kitura to use session middleware
  // Must be configured with proper session storage for production
  // environments. See https://github.com/IBM-Swift/Kitura-Session for
  // additional documentation
  let router = Router()
  let session = Session(secret: "Some secret")
  router.all(middleware: session)
  let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()
  let kituraCredentials = Credentials()
  kituraCredentials.register(plugin: webappKituraCredentialsPlugin)

  // Callback to finish the authorization process. Will retrieve access and identity tokens from AppID
  router.get(CALLBACK_URL,
    handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
      successRedirect: LANDING_PAGE_URL,
      failureRedirect: LANDING_PAGE_URL
      ))

  // Protected area
  router.get("/protected", handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name), { (request, response, next) in
    let appIdAuthContext:JSON? = request.session?[WebAppKituraCredentialsPlugin.AuthContext]
    let identityTokenPayload:JSON? = appIdAuthContext?["identityTokenPayload"]
    guard appIdAuthContext?.dictionary != nil, identityTokenPayload?.dictionary != nil else {
      response.status(.unauthorized)
      return next()
    }
    response.send(json: identityTokenPayload!)
    next()
    })
  ```
  {: pre}

4. Redeploy your application.



## Adding {{site.data.keyword.appid_short_notm}} to an existing application that does not run on {{site.data.keyword.Bluemix_notm}}


If you have a Node.js or Swift application that does not run on Bluemix, you can configure the WebAppStrategy or the WebAppKituraCredentialsPlugin to work remotely.


In your Node.js app, replace `passport.use(new WebAppStrategy());` with the following code.

  ```javaScript
  passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
  ```
{: pre}

In your Swift app, replace `let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()` with the following code.

  ```swift
  let options = [
        "clientId": "{client-id}",
        "secret": "{secret}",
        "tenantId": "{tenant-id}",
        "oauthServerUrl": "{oauth-server-url}",
        "redirectUri": "{app-url}" + CALLBACK_URL
    ]
    let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin(options: options)
  ```
  {: pre}

<table>
<caption> Command components for Swift and Node.js apps explained </caption>
  <tr>
    <th> Components </th>
    <th> Description </th>
  </tr>
  <tr>
    <td> <i> tenantID </i> </br> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
    <td> You can find these values by clicking **View credentials** in the **service credentials** tab of your service dashboard. </td>
  </tr>
  <tr>
    <td> <i> app-url </i> </td>
    <td> Your application URL. </td>
  </tr>
</table>
