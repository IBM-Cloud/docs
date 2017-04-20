---

copyright:
  years: 2017 lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Protegendo recursos de backend
{: #protecting-resources}

É possível acessar recursos protegidos usando os SDKs do cliente.
{:shortdesc}

Chamar um recurso protegido ativa o widget de login, se necessário. Se um token válido já foi obtido, o widget de login não será ativado e o recurso será
acessado diretamente.


## Usando o SDK do Swift do iOS
{: #requesting-swift}

1. Importe o BMSCore.

  ```swift
  import BMSCore
  ```
  {:pre}

2. Chame uma solicitação de recurso protegido.

  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //code handling the response here
  })
  ```
  {:pre}


## Usando o SDK do Android
{: #requesting-android}

1. Chame uma solicitação de recurso protegido.

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
