---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# 保护后端资源
{: #protecting-resources}

您可以使用客户端 SDK 来访问受保护资源。
{:shortdesc}

调用受保护资源会根据需要启动登录窗口小部件。如果已经获取有效的令牌，那么不会启动登录窗口小部件，而是会直接访问该资源。


## 使用 iOS Swift SDK
{: #requesting-swift}

1. 导入 BMSCore。

  ```swift
  import BMSCore
  ```
  {:pre}

2. 调用受保护资源请求。

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

1. 调用受保护资源请求。

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
