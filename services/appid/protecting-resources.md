---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Protecting back-end resources
{: #protecting-resources}

You can access protected resources by using the client SDKs.
{:shortdesc}

Calling a protected resource launches the login widget, if necessary. If a valid token was already obtained, the login widget is not launched, and the resource is accessed directly.


## Using the iOS Swift SDK
{: #requesting-swift}

1. Import BMSCore.

  ```swift
  import BMSCore
  ```
  {:pre}

2. Invoke a protected resource request.

  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //code handling the response here
  })
  ```
  {:pre}


## Using the Android SDK
{: #requesting-android}

1. Invoke a protected resource request.

  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
  public void onSuccess (Response response) {
     //code handling the response here
  }
  @Override
  public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
      //code handling the failure here
  });
  ```
  {:pre}
