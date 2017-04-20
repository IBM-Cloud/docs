---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# 访问令牌和身份令牌
{: #access-and-identity}

{{site.data.keyword.appid_short}} 使用两种类型的令牌：访问令牌和身份令牌。令牌的格式为 <a href="https://jwt.io/introduction/" target="_blank">JSON Web 令牌 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。{:shortdesc}


## 访问令牌
{: #access-tokens}

有了访问令牌，就可以与受 {{site.data.keyword.appid_short_notm}} 授权过滤器保护的[后端资源](/docs/services/appid/protecting-resources.html)进行通信。令牌符合 JavaScript 对象签名和加密 (JOSE) 规范，并且具有以下格式：

```
Header: {

    "typ": "JOSE", // 根据规范确定的头类型

    "alg": "RS256", // 根据规范确定的算法

}
Payload: {

    "iss": "", // 发放者，发放此令牌的 AppID 服务器。StringOrURL

    "sub": "", // 主体，向其发放此令牌的对象。最有可能是 userId

    "aud": "", // 受众，此令牌适用的对象。OAuth2 client_id。

    "exp: "", // 到期时间戳记（戳记时间）

    "iat": "", // 发放时间戳记（戳记时间）

    "tenant": "xxx", // 为其发放令牌的 AppID tenantId

    "auth_by": "appid_anon / appid_facebook / appid_google",

    "scope": "", // 此令牌发放用于的作用域

}
```
{:screen}

## 身份令牌
{: #identity-tokens}

身份令牌包含有关用户的信息，包括姓名、电子邮件、性别、照片和位置。

```
Header: {

    "typ": "JOSE", // 根据规范确定的头类型

    "alg": "RS256", // 根据规范确定的算法

}
Payload: {

    "iss": "", // 发放者，发放此令牌的 AppID 服务器。StringOrURL

    "sub": "", // 主体，向其发放此令牌的对象。AppID userid。

    "aud": "", // 受众，此令牌适用的对象。OAuth2 client_id。

    "exp: "", // 到期时间戳记（戳记时间）

    "iat": "", // 发放时间戳记（戳记时间）

    "tenant": "xxx", // 为其发放令牌的 AppID tenantId

    "name": "John Smith", // IDP 所报告的用户全名，必需

    "email": "js@mail.com", // IDP 所报告的电子邮件，仅可用时

    "gender", "male", // IDP 所报告的用户性别，仅可用时

    "locale": "en", // IDP 所报告的用户语言环境，仅可用时

    "picture": "https://url.to.photo", // 用户照片的 URL，仅可用时

    "auth_by": "appid_facebook/appid_google", // 用于认证的 IDP 的名称，必需

    "identities": [

        "provider: "appid_facebook/appid_google", // 必需

        "id": "unique user id as reported by IDP", // 必需

        "profile": { ... } // IDP 返回的 JSON 对象，必需

      },

      {...}, {...} // 更多链接的身份

    ],

    "oauth_client":{

      "type": "serverapp/mobileapp from client registration", // 必需

      "name": "client_name as reported during client registration", // 必需

      "software_id": "software_id as reported during client registration", // 必需

      "software_version": "software_version as reported during client registration", // 必需

      "device_id": "device_id from client registration", //仅移动

      "device_model": "device_model from client registration", //仅移动

      "device_os": "device_os from client registration", //仅移动

    }

}
```
{:screen}
