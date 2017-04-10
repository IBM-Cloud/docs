---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Protección de recursos de fondo
{: #protecting-resources}

El SDK del servidor de {{site.data.keyword.appid_short}} proporciona estrategias para proteger dos tipos de recursos: API y aplicaciones web.
{:shortdesc}


## Cómo acceder a recursos protegidos desde SDK de cliente
{: #accessing}

Llamar a un recurso protegido inicia el widget de inicio de sesión, en caso necesario. Si ya se ha obtenido una señal válida, el widget de inicio de sesión no se inicia, y se accede al recurso directamente.


### Utilización del SDK de Swift
{: #requesting-swift notoc}

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


### Utilización del SDK de Android
{: #requesting-android notoc}

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



## Filtros de autorización
{: #auth-filter}

La estrategia de protección de API devuelve una respuesta HTTP 401 con una lista de ámbitos para obtener la autorización para un cliente no autenticado. La estrategia de protección de aplicaciones web devuelve una redirección HTTP 302. La redirección envía a un cliente no autenticado a la página de inicio de sesión que aloja el servicio {{site.data.keyword.appid_short_notm}}, o bien directamente a la página de inicio de sesión de un proveedor de identidad, en función de su configuración.



### Estrategia de API
{: #api notoc}

La estrategia de API espera que las solicitudes contengan una cabecera de autorización con una señal de acceso válida. La respuesta también puede incluir una señal de identidad, pero no es obligatorio; consulte [Señales de acceso e identidad](/docs/services/appid/about.html#acess-and-identity).

Si una señal no es válida o ha caducado, la estrategia de API devuelve un error HTTP 401 que contiene la siguiente información: Www-Authenticate=Bearer scope="{scope}" error="{error}". El componente `error` es opcional.

Si la solicitud devuelve una señal válida, el control se pasa al siguiente middleware y la propiedad `appIdAuthorizationContext` se inyecta en el objeto de solicitud. Esta propiedad contiene señales de acceso e identidad originales, así como información de carga útil descodificada como objetos JSON simples.


### Estrategia de app web
{: #web notoc}

Cuando la estrategia de app web detecta intentos no autenticados de acceso a un recurso protegido, automáticamente redirige el navegador de un usuario a la página de autenticación. Tras la correcta autenticación, el usuario vuelve al URL de devolución de llamada de la aplicación web. El servicio utiliza la clase de estrategia de app web para obtener señales de acceso e identidad. Después de obtener estas señales, la clase de estrategia de app web las almacena en una sesión HTTP bajo `WebAppStrategy.AUTH_CONTEXT`. Depende del usuario decidir si desea almacenar las señales de acceso e identidad en la base de datos de la aplicación.

## Cabecera de autorización
{: #auth-header}

La cabecera de autorización de la solicitud entrante consta de tres partes, que están separadas por espacios en blanco: Bearer, señal de acceso y señal de ID. La señal de acceso es un componente obligatorio mientras que la señal de ID es opcional. La estructura de cabecera esperada es: Authorization=Bearer {access_token} [{id_token}]
