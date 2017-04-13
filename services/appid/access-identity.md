---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Access and identity tokens
{: #access-and-identity}

{{site.data.keyword.appid_short}} uses two types of tokens: access and identity. The tokens are formatted as <a href="https://jwt.io/introduction/" target="_blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
{:shortdesc}


## Access token
{: #access-tokens}

The access token enables communication with [back-end resources](/docs/services/appid/protecting-resources.html) that are protected by {{site.data.keyword.appid_short_notm}} authorization filters. The token conforms to JavaScript Object Signing and Encryption (JOSE) specifications and have the following format:

```
Header: {

    "typ": "JOSE", // header type, according to spec

    "alg": "RS256", // algorithm, according to spec

}
Payload: {

    "iss": "", // issuer, the AppID server that issued this token. StringOrURL

    "sub": "", // subject, who this token was issued to. Most probably userId

    "aud": "", // audience, who is this token intended for. OAuth2 client_id.

    "exp: "", // expiration timestamp, epoch time

    "iat": "", // issued at timestamp, epoch time

    "tenant": "xxx", the AppID tenantId the token was issued for

    "auth_by": "appid_anon / appid_facebook / appid_google",

    "scope": "", // the scope[s] this token was issued for

}
```
{:screen}

## Identity token
{: #identity-tokens}

The identity token contains information about the user, including name, email, gender, picture, and location.

```
Header: {

    "typ": "JOSE", // header type, according to spec

    "alg": "RS256", // algorithm, according to spec

}
Payload: {

    "iss": "", // issuer, the AppID server that issued this token. StringOrURL

    "sub": "", // subject, who this token was issued to. AppID userid.

    "aud": "", // audience, who is this token intended for. OAuth2 client_id.

    "exp: "", // expiration timestamp, epoch time

    "iat": "", // issued at timestamp, epoch time

    "tenant": "xxx", // the AppID tenantId the token was issued for

    "name": "John Smith", // user's full name as reported by IDP, mandatory,

    "email": "js@mail.com", // user's email as reported by IDP, only if available,

    "gender", "male", // user's gender as reported by IDP, only if available,

    "locale": "en", // user's locale as reported by IDP, only if available

    "picture": "https://url.to.photo", // URL to user's picture, only if available

    "auth_by": "appid_facebook/appid_google", // the name of IDP used for authentication, mandatory

    "identities": [

        "provider: "appid_facebook/appid_google", // mandatory

        "id": "unique user id as reported by IDP", // mandatory

        "profile": { ... } // JSON object returned by IDP,  mandatory

      },

      {...}, {...} // more linked identities

    ],

    "oauth_client":{

      "type": "serverapp/mobileapp from client registration", // mandatory

      "name": "client_name as reported during client registration", // mandatory

      "software_id": "software_id as reported during client registration", // mandatory

      "software_version": "software_version as reported during client registration", // mandatory

      "device_id": "device_id from client registration", //mobile only

      "device_model": "device_model from client registration", //mobile only

      "device_os": "device_os from client registration", //mobile only

    }

}
```
{:screen}
