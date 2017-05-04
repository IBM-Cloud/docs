---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Zugriffs- und Identitätstoken
{: #access-and-identity}

{{site.data.keyword.appid_short}} verwendet zwei Typen von Token: Zugriffs- und Identitätstoken. Die Token sind als <a href="https://jwt.io/introduction/" target="_blank">JSON-Web-Token <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> formatiert.{:shortdesc}


## Zugriffstoken
{: #access-tokens}

Das Zugriffstoken ermöglicht die Kommunikation mit [Back-End-Ressourcen](/docs/services/appid/protecting-resources.html), die durch die {{site.data.keyword.appid_short_notm}}-Berechtigungsfilter geschützt sind. Das Token entspricht den JavaScript Object Signing and Encryption (JOSE)-Spezifikationen und hat das folgende Format:

```
Header: {

    "typ": "JOSE", // Headertyp, je nach Spezifikation

    "alg": "RS256", // Algorithmus, je nach Spezifikation

}
Payload: {

    "iss": "", // Aussteller, der AppID-Server, der dieses Token ausgegeben hat. StringOrURL

    "sub": "", // Betreff, zu dem dieses Token ausgegeben wurde. Wahrscheinlich userId

    "aud": "", // Zielgruppe, für die dieses Token bestimmt ist. OAuth2 client_id.

    "exp: "", // Ablauf Zeitmarke, Epochenzeit

    "iat": "", // bei Zeitmarke ausgegeben, Epochenzeit

    "tenant": "xxx", tenantId der AppID, für die das Token ausgegeben wurde

    "auth_by": "appid_anon / appid_facebook / appid_google",

    "scope": "", // Umfang, für den das Token ausgegeben wurde

}
```
{:screen}

## Identitätstoken
{: #identity-tokens}

Das Identitätstoken enthält Informationen über den Benutzer, einschließlich Name, E-Mail-Adresse, Geschlecht, Foto und Ort.

```
Header: {

    "typ": "JOSE", // Headertyp, je nach Spezifikation

    "alg": "RS256", // Algorithmus, je nach Spezifikation

}
Payload: {

    "iss": "", // Aussteller, der AppID-Server, der dieses Token ausgegeben hat. StringOrURL

    "sub": "", // Betreff, zu dem dieses Token ausgegeben wurde. userid der AppID.

    "aud": "", // Zielgruppe, für die dieses Token bestimmt ist. OAuth2 client_id.

    "exp: "", // Ablauf Zeitmarke, Epochenzeit

    "iat": "", // bei Zeitmarke ausgegeben, Epochenzeit

    "tenant": "xxx", // tenantId der AppID, für die das Token ausgegeben wurde

    "name": "John Smith", // vollständiger Benutzername wie von IDP bereitgestellt, obligatorisch,

    "email": "js@mail.com", // E-Mail-Adresse des Benutzers, wie von IDP bereitgestellt, wenn verfügbar,

    "gender", "male", // Geschlecht des Benutzers, wie von IDP bereitgestellt, wenn verfügbar,

    "locale": "en", // Ländereinstellung des Benutzers, wie von IDP bereitgestellt, wenn verfügbar

    "picture": "https://url.to.photo", // URL zum Benutzerfoto, wenn verfügbar

    "auth_by": "appid_facebook/appid_google", // Name des IDP, der für die Authentifizierung verwendet wird, obligatorisch

    "identities": [

        "provider: "appid_facebook/appid_google", // obligatorisch

        "id": "unique user id as reported by IDP", // obligatorisch

        "profile": { ... } // JSON-Objekt, das von IDP zurückgegeben wird, obligatorisch

      },

      {...}, {...} // weitere verknüpfte Identitäten

    ],

    "oauth_client":{

      "type": "serverapp/mobileapp from client registration", // obligatorisch

      "name": "client_name as reported during client registration", // obligatorisch

      "software_id": "software_id as reported during client registration", // obligatorisch

      "software_version": "software_version as reported during client registration", // obligatorisch

      "device_id": "device_id from client registration", //nur mobil

      "device_model": "device_model from client registration", //nur mobil

      "device_os": "device_os from client registration", //nur mobil

    }

}
```
{:screen}
