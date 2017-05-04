---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Señales de identidad y de acceso
{: #access-and-identity}

{{site.data.keyword.appid_short}} utiliza dos tipos de señales: acceso e identidad. Las señales están formateadas como <a href="https://jwt.io/introduction/" target="_blank">Señales web JSON <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
{:shortdesc}


## Señal de acceso
{: #access-tokens}

La señal de acceso permite la comunicación con [recursos de fondo](/docs/services/appid/protecting-resources.html) que están protegidos por filtros de autorización de {{site.data.keyword.appid_short_notm}}. La señal se ajusta a las especificaciones de JOSE (JavaScript Object Signing and Encryption) y tiene el formato siguiente:

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

## Señal de identidad
{: #identity-tokens}

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
