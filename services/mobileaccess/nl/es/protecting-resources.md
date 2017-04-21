---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---

{:shortdesc: .shortdesc}
{:codeblock:.codeblock}

**Importante: El servicio {{site.data.keyword.amafull}} se sustituye por el servicio {{site.data.keyword.appid_full}}.**

# Protección de recursos de fondo con el servicio {{site.data.keyword.amashort}}
{: #protecting-resources}


Con el servicio de {{site.data.keyword.amafull}}, puede proteger las aplicaciones de fondo basadas en Java y Node.js que se estén ejecutando en {{site.data.keyword.Bluemix_notm}} con la supervisión y la seguridad OAuth habilitada para móviles.
{:shortdesc}

## Antes de empezar
{: #before-you-begin}
Antes de empezar, asegúrese de que existe el servicio Node.js en la aplicación de fondo de {{site.data.keyword.Bluemix_notm}}.


## Filtro de autorización
{: #auth-filter}
El SDK del servidor de {{site.data.keyword.amashort}} dispone de filtros de autorización que se pueden utilizar para proteger las aplicaciones de fondo.  El filtro de autorización intercepta las solicitudes entrantes y las valida si existe una cabecera de autorización. Si no existe cabecera de autorización o esta no es válida, el filtro devuelve una respuesta con el código HTTP 401. El SDK del cliente de {{site.data.keyword.amashort}} sabe cómo interceptar una respuesta HTTP 401 devuelta por el SDK del servidor de {{site.data.keyword.amashort}} y activa el flujo de autenticación.
## Cabecera de autorización
{: #auth-header}
La cabecera de autorización de la solicitud entrante consta de tres partes: bearer, la señal de acceso y la señal de ID separados por espacios. La `señal de acceso` es un componente obligatorio mientras que la `señal de ID` es opcional.

Cada filtro de autorización procesa la cabecera de autorización entrante correspondiente. El filtro valida las firmas de la señal de acceso y la señal de ID, la fecha de caducidad y la integridad estructural. Tras superar la validación, se añade un objeto de contexto de seguridad al objeto de solicitud. Puede obtener una referencia al contexto de seguridad con la API relevante.

El contexto de seguridad almacena el sujeto, el usuario, el dispositivo y la información de la aplicación con la siguiente estructura:
```JSON
{
    "imf.sub":"myclientid",
    "imf.user": {
        "id":"user-name",
        "authBy":"myrealm",
        "displayName":"display-name"
    },
    "imf.device": {
        "id":"device-id",
        "platform":"iOSnative",
        "model":"device-model",
        "osVersion":"device-os"
    },
    "imf.application": {
        "id":"ios.bundle.id",
        "version":"1.0"
    }
}
```
{: codeblock}

* `imf.sub`: especifica el sujeto de la señal de ID o el ID exclusivo del cliente si no hay ninguna señal de ID.
* `imf.user`: especifica la identidad del usuario que se ha extraído de la señal de ID. Si no hay ninguna señal de ID, este campo tendrá un objeto vacío.
* `imf.device`: especifica la identidad del dispositivo que se ha extraído de la señal de ID. Si no hay ninguna señal de ID, este campo tendrá un objeto vacío.
* `imf.application`: especifica la identidad de la aplicación que se ha extraído de la señal de ID. Si no hay ninguna señal de ID, este campo tendrá un objeto en blanco.

## Pasos siguientes
{: #next-steps}
* [Protección de recursos Node.js](protecting-resources-nodejs.html)
* [Protección de los recursos de Liberty for Java&trade;](protecting-resources-java.html)
* [Desarrollo local](protecting-resources-local.html)
