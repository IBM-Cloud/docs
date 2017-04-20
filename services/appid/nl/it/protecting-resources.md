---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Protezione delle risorse di back-end
{: #protecting-resources}

Puoi accedere alle risorse protette utilizzando le SDK client.
{:shortdesc}

Il richiamo di una risorsa protetta avvia il widget di accesso, se necessario. Se è già stato ottenuto un token valido, il widget di accesso non viene avviato e si accede direttamente alla risorsa.


## Utilizzo dell'SDK Swift iOS
{: #requesting-swift}

1. Importa BMSCore.

  ```swift
  import BMSCore
  ```
  {:pre}

2. Richiama una richiesta della risorsa protetta.

  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //il codice gestisce la risposta qui
  })
  ```
  {:pre}


## Utilizzo dell'SDK Android
{: #requesting-android}

1. Richiama una richiesta della risorsa protetta.

  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
		public void onSuccess (Response response) {
     //il codice gestisce la risposta qui
  }
  @Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
      //il codice gestisce la risposta qui
  });
  ```
  {:pre}
