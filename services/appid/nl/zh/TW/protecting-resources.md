---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# 保護後端資源
{: #protecting-resources}

您可以使用用戶端 SDK 來存取受保護的資源。
{:shortdesc}

呼叫受保護資源會啟動登入小組件（必要的話）。如果已取得有效記號，則不會啟動登入小組件，並且會直接存取資源。


## 使用 iOS Swift SDK
{: #requesting-swift}

1. 匯入 BMSCore。

  ```swift
  import BMSCore
  ```
  {:pre}

2. 呼叫受保護的資源要求。

  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //code handling the response here
  })
  ```
  {:pre}


## 使用 Android SDK
{: #requesting-android}

1. 呼叫受保護的資源要求。

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
