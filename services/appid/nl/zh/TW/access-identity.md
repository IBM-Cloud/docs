---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# 存取及身分記號
{: #access-and-identity}

{{site.data.keyword.appid_short}} 使用兩種類型的記號：存取及身分。記號會格式化為 <a href="https://jwt.io/introduction/" target="_blank">JSON Web 記號 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
{:shortdesc}


## 存取記號
{: #access-tokens}

存取記號會啟用與 {{site.data.keyword.appid_short_notm}} 授權過濾器所保護的[後端資源](/docs/services/appid/protecting-resources.html)進行通訊。記號符合「JavaScript 物件簽署及加密 (JOSE)」規格，並且具有下列格式：

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

## 身分記號
{: #identity-tokens}

身分記號包含使用者的相關資訊，包括姓名、電子郵件、性別、圖片及位置。

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
