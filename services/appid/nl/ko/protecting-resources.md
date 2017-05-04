---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# 백엔드 리소스 보호
{: #protecting-resources}

클라이언트 SDK를 사용하여 보호된 리소스에 액세스할 수 있습니다.
{:shortdesc}

필요한 경우에 보호된 리소스 호출로 로그인 위젯을 실행합니다. 올바른 토큰이 이미 확보된 경우 로그인 위젯이 실행되지 않으며 리소스에 직접 액세스합니다.


## iOS Swift SDK 사용
{: #requesting-swift}

1. BMSCore를 가져오십시오.

  ```swift
  import BMSCore
  ```
  {:pre}

2. 보호된 리소스 요청을 호출하십시오.

  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //code handling the response here
  })
  ```
  {:pre}


## Android SDK 사용
{: #requesting-android}

1. 보호된 리소스 요청을 호출하십시오.

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
