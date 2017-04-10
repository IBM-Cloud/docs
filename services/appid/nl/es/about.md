---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Acerca de {{site.data.keyword.appid_short_notm}}
{: #about}

Con {{site.data.keyword.appid_full}}, los desarrolladores pueden proteger y añadir autenticación a sus apps de {{site.data.keyword.Bluemix}}, con algunas líneas de código. Los desarrolladores también pueden gestionar datos específicos del usuario para crear experiencias personalizadas de la app.
{:shortdesc}


Puede utilizar el servicio de las siguientes maneras:

* Para añadir la autenticación a sus aplicaciones móviles y web
* Para otorgar acceso a los recursos de fondo protegidos y a las apps web
* Para proteger las aplicaciones Node.js y Swift alojadas en {{site.data.keyword.Bluemix_notm}}
* Para almacenar los datos de usuario, como por ejemplo las preferencias de la app o la información desde sus perfiles sociales públicos
* Para utilizar datos almacenados para crear experiencias de la app personalizadas
* Para proteger los recursos de los usuarios autenticados y anónimos

**Nota**: Los protocolos implementados son totalmente compatibles con OpenID Connect (OIDC).


## Componentes
{: #components}

* Panel de control: Descargar ejemplos de incorporación, consultar registros de actividad, configurar varios tipos de autenticación y de proveedores de identidad
* SDK de cliente: Crear apps móviles y web que utilizan el servicio para implementar la autenticación de usuario
    * Requisitos previos para Android: API 25 o superior, Java 8.x, Android SDK tools 25.2.5 o superior, Android SDK Platform Tools 25.0.3 o superior, Android Build Tools versión 25.0.2
    * Requisitos previos para iOS: iOS9 o superior, MacOS 10.11.5, Xcode 8.2
* SDK del servidor: proteja los recursos que se alojan en {{site.data.keyword.Bluemix_notm}}
    * Los tiempos de ejecución soportados son Node.js y Swift

## Visión general de la arquitectura

![Diagrama de la arquitectura de {{site.data.keyword.appid_short_notm}}](/images/appid_architecture.png)

Figura 1. Diagrama de arquitectura de {{site.data.keyword.appid_short_notm}}

Puede proteger los recursos de nube con el SDK del servidor de {{site.data.keyword.appid_short_notm}}. Utilice la clase request que proporciona el SDK del cliente de {{site.data.keyword.appid_short_notm}} para comunicarse con los recursos de nube protegidos.

* El SDK del servidor detecta una solicitud no autorizada y devuelve un error de autorización HTTP 401.
* El SDK del cliente detecta un error de autorización HTTP 401 e inicia automáticamente el proceso de autenticación en función de la configuración de los proveedores de identidad.
* Se ha intentado la autenticación de acuerdo con los proveedores de identidad configurados en este momento.
* Tras la correcta autenticación, el servicio devolverá las señales de identidad y de autorización.
* El SDK del cliente añade automáticamente la señal de autorización a la solicitud original y vuelve a enviar la solicitud al recurso de nube.
* El SDK del servidor extrae la señal de acceso de la solicitud y la valida con {{site.data.keyword.appid_short_notm}}.
Se otorga acceso y la respuesta se devuelve a la aplicación.


## Flujo de solicitudes
{: #request}

En el diagrama siguiente se describe el flujo de una solicitud, desde el SDK del cliente a los proveedores de identidad y de la aplicación de programa de fondo. 

Flujo de solicitudes de ![{{site.data.keyword.appid_short_notm}}](/images/appidflow.png) 


* Utilice el SDK del cliente de {{site.data.keyword.appid_short_notm}} para realizar una solicitud a los recursos de fondo protegidos por el SDK del servidor de {{site.data.keyword.appid_short_notm}}.
* El SDK del servidor de {{site.data.keyword.appid_short_notm}} detecta una solicitud no autorizada y devuelve HTTP 401 y el ámbito de autorización.
* El SDK del cliente detecta automáticamente el código HTTP 401 e inicia el proceso de autenticación.
* Cuando el SDK del cliente establece contacto con el servicio, el SDK del servidor devuelve el widget de inicio de sesión si hay más de un proveedor de identidad configurado. {{site.data.keyword.appid_short_notm}} llama al proveedor de identidad y presenta el formulario de inicio de sesión para dicho proveedor o devuelve un código de concesión que les permite autenticarse si no hay ningún proveedor de identidad configurado. 
* {{site.data.keyword.appid_short_notm}} solicita al cliente que se autentique especificando un cambio de autenticación. 
* Si Facebook o Google están configurados y el usuario inicia una sesión, la autenticación se gestiona mediante el flujo de OAuth del proveedor de identidad correspondiente. 
* Si la autenticación finaliza con el mismo código de concesión, el código se envía al punto final de señal. El punto final devuelve dos señales: una señal de acceso y una de identidad. A partir de este momento, todas las solicitudes realizadas con el SDK del cliente tendrán una cabecera de autorización nueva.
* El SDK del cliente vuelve a enviar automáticamente la solicitud original que activó el flujo de autorización.
* El SDK del servidor extrae la cabecera de autorización de la solicitud, valida la cabecera con el servicio y otorga acceso a un recurso de fondo.

## Señales de identidad y de acceso
{: #access-and-identity}

{{site.data.keyword.appid_short}} utiliza dos tipos de señales: acceso e identidad. Las señales están formateadas como <a href="https://jwt.io/introduction/" target="_blank">Señales web JSON <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.


### Señal de acceso
{: #access-tokens notoc}

La señal de acceso permite la comunicación con recursos protegidos por filtros de autorización de {{site.data.keyword.appid_short_notm}}, consulte [Protección de recursos de fondo](/docs/services/appid/protecting-resources.html).
La señal se ajusta a las especificaciones de JOSE (JavaScript Object Signing and Encryption) y tiene el formato siguiente:

```
Header: {

    "typ": "JOSE", // tipo de cabecera, de acuerdo con la especificación

    "alg": "RS256", // algoritmo, de acuerdo con la especificación

}
Payload: {

    "iss": "", // emisor, el servidor de AppID que ha emitido esta señal. StringOrURL

    "sub": "", // sujeto, a quién se ha emitido la señal. Probablemente userId

    "aud": "", // audiencia, para quién está destinada esta señal. OAuth2 client_id.

    "exp: "", // indicación de fecha y hora de la caducidad, tiempo de época

    "iat": "", // emitido en indicación de fecha y hora, tiempo de época

    "tenant": "xxx", el AppID tenantId para el que se ha emitido la señal

    "auth_by": "appid_anon / appid_facebook / appid_google",

    "scope": "", // el[los] ámbito[s] para el[los] que se ha emitido esta señal

}
```
{:screen}

### Señal de identidad
{: #identity-tokens notoc}

La señal de identidad contiene información sobre el usuario, tal como el nombre, el correo electrónico, el género, la imagen y la ubicación.

```
Header: {

    "typ": "JOSE", // tipo de cabecera, de acuerdo con la especificación

    "alg": "RS256", // algoritmo, de acuerdo con la especificación

}
Payload: {

    "iss": "", // emisor, el servidor de AppID que ha emitido esta señal. StringOrURL

    "sub": "", // sujeto, a quién se ha emitido la señal. ID de usuario de AppID.

    "aud": "", // audiencia, para quién está destinada esta señal. OAuth2 client_id.

    "exp: "", // indicación de fecha y hora de la caducidad, tiempo de época

    "iat": "", // emitido en indicación de fecha y hora, tiempo de época

    "tenant": "xxx", // el AppID tenantId para el que se ha emitido la señal

    "name": "John Smith", // nombre completo del usuario tal como lo ha notificado IDP, obligatorio,

    "email": "js@mail.com", // correo electrónico del usuario tal como lo ha notificado IDP, sólo si está disponible,

    "gender", "male", // género del usuario tal como lo ha notificado IDP, sólo si está disponible,

    "locale": "en", // entorno local del usuario tal como lo ha notificado IDP, sólo si está disponible

    "picture": "https://url.to.photo", // URL para imagen del usuario, sólo si está disponible

    "auth_by": "appid_facebook/appid_google", // el nombre del IDP utilizado para la autenticación, obligatorio

    "identities": [

        "provider: "appid_facebook/appid_google", // obligatorio

        "id": "unique user id as reported by IDP", // obligatorio

        "profile": { ... } // objeto JSON devuelto por IDP, obligatorio

      },

      {...}, {...} // más identidades enlazadas

    ],

    "oauth_client":{

      "type": "serverapp/mobileapp from client registration", // obligatorio

      "name": "client_name as reported during client registration", // obligatorio

      "software_id": "software_id as reported during client registration", // obligatorio

      "software_version": "software_version as reported during client registration", // obligatorio

      "device_id": "device_id from client registration", //sólo móvil

      "device_model": "device_model from client registration", //sólo móvil

      "device_os": "device_os from client registration", //sólo móvil

    }

}
```
{:screen}


## Visión general de los proveedores de identidad
{: #identity-providers-overview}

Puede utilizar los siguientes proveedores de identidad en sus aplicaciones web y móviles:

* **Facebook**: Los usuarios inician sesión en la app móvil o web con las credenciales de Facebook.
* **Google**: Los usuarios inician sesión en la app móvil o web con las credenciales de Google+.
<!--* **Custom** - Bring your own identity provider. The identity providers should be compliant with OIDC. -->

## Utilización de la configuración predeterminada
{: #default-configuration}

{{site.data.keyword.appid_short_notm}} proporciona una configuración predeterminada cuando se configuran inicialmente los proveedores de identidad. Puede utilizar la configuración predeterminada sólo en modalidad de desarrollo. Para cada proveedor de identidad, estas credenciales se limitan a 100 usos por instancia de {{site.data.keyword.appid_short_notm}}, por día. Antes de publicar la aplicación, actualice la configuración predeterminada a sus propias credenciales. Para actualizar la configuración, consulte [Configuración de los proveedores de identidad](/docs/services/appid/identity-providers.html).
