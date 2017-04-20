---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Protection des ressources de back-end
{: #protecting-resources}

Vous pouvez accéder aux ressources protégées à l'aide des SDK client.
{:shortdesc}

L'appel d'une ressource protégée lance, en cas de besoin, le widget de connexion. Si un jeton d'accès valide a déjà été obtenu, le widget de connexion n'est pas lancé et l'accès direct à la ressource est autorisé.


## Utilisation du SDK Swift iOS
{: #requesting-swift}

1. Importez BMSCore.

  ```swift
  import BMSCore
  ```
  {:pre}

2. Invocation d'une demande de ressource protégée.

  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<URL_de_votre_ressource_protégée>")
  request.send(completionHandler: {(response:Response?, error:Error?) //code gérant la réponse
  })
  ```
  {:pre}


## Utilisation du SDK Android
{: #requesting-android}

1. Invocation d'une demande de ressource protégée.

  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<URL_de_votre_ressource protégée>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
		public void onSuccess (Response response) {
     //code gérant la réponse
  }
  @Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
      //code gérant la réponse
  });
  ```
  {:pre}
