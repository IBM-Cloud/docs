---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Back-End-Ressourcen schützen
{: #protecting-resources}

Mithilfe der Client-SDKs können Sie auf geschützte Ressourcen zugreifen.
{:shortdesc}

Beim Aufrufen einer geschützten Ressource wird ggf. das Anmelde-Widget gestartet. Wenn bereits ein gültiges Token angefordert wurde, wird das Anmelde-Widget nicht gestartet. Auf die Ressource kann dann direkt zugegriffen werden.


## iOS-Swift-SDK verwenden
{: #requesting-swift}

1. Importieren Sie BMSCore.

  ```swift
  import BMSCore
  ```
  {:pre}

2. Rufen Sie eine Anforderung für die geschützte Ressource auf.

  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //Code-Handling der Antwort hier
  })
  ```
  {:pre}


## Das Android-SDK verwenden
{: #requesting-android}

1. Rufen Sie eine Anforderung für die geschützte Ressource auf.

  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
	public void onSuccess (Response response) {
     //Code-Handling der Antwort hier
  }
  @Override
	public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
      //Code-Handling des Fehlers hier
  });
  ```
  {:pre}
