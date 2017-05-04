---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Protección de recursos de fondo
{: #protecting-resources}

Puede acceder a recursos protegidos utilizando los SDK del cliente.
{:shortdesc}

Llamar a un recurso protegido inicia el widget de inicio de sesión, en caso necesario. Si ya se ha obtenido una señal válida, el widget de inicio de sesión no se inicia, y se accede al recurso directamente.


## Utilización del SDK de Swift de iOS
{: #requesting-swift}

1. Importe BMSCore.

  ```swift
  import BMSCore
  ```
  {:pre}

2. Invoque una solicitud de recurso protegido.

  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //el código maneja la respuesta aquí
  })
  ```
  {:pre}


## Utilización del SDK de Android
{: #requesting-android}

1. Invoque una solicitud de recurso protegido.

  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
		public void onSuccess (Response response) {
     //el código maneja la respuesta aquí
  }
  @Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
      //el código maneja el error aquí
  });
  ```
  {:pre}
