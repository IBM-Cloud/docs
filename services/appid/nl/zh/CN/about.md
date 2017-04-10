---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# 关于 {{site.data.keyword.appid_short_notm}}
{: #about}

通过 {{site.data.keyword.appid_full}}，开发者只需几行代码即可保护 {{site.data.keyword.Bluemix}} 应用程序并向其添加认证。开发者还可以管理特定于用户的数据以构建个性化应用程序体验。
{:shortdesc}


可以通过以下方式来使用该服务：

* 向移动和 Web 应用程序添加认证
* 授予对受保护后端资源和 Web 应用程序的访问权
* 保护在 {{site.data.keyword.Bluemix_notm}} 上托管的 Node.js 和 Swift 应用程序
* 存储用户数据，例如应用程序首选项或用户公共社交个人档案中的信息
* 使用存储的数据来构建个性化应用程序体验
* 保护供已认证用户和匿名用户使用的资源

**注**：实施的协议完全符合 OpenID Connect (OIDC)。


## 组件
{: #components}

* 仪表板 - 下载上线样本，查看活动日志，配置各种认证类型和身份提供者
* 客户端 SDK - 构建使用服务来实施用户认证的移动和 Web 应用程序
    * Android 的必备软件：API 25 或更高版本，Java 8.x，Android SDK Tools 25.2.5 或更高版本，Android SDK Platform Tools 25.0.3 或更高版本，Android Build Tools V25.0.2
    * iOS 的必备软件：iOS9 或更高版本，MacOS 10.11.5，Xcode 8.2
* 服务器 SDK - 保护在 {{site.data.keyword.Bluemix_notm}} 上托管的资源
    * 支持的运行时为 Node.js 和 Swift

## 体系结构概述

![{{site.data.keyword.appid_short_notm}} 体系结构图](/images/appid_architecture.png)

图 1. {{site.data.keyword.appid_short_notm}} 体系结构图

您可以通过 {{site.data.keyword.appid_short_notm}} 服务器 SDK 来保护云资源。使用 {{site.data.keyword.appid_short_notm}} 客户端 SDK 提供的请求类可与受保护的云资源进行通信。

* 服务器 SDK 检测到未授权的请求，然后返回 HTTP 401 授权质询。
* 客户端 SDK 检测到 HTTP 401 授权质询，然后基于身份提供者的配置自动启动认证过程。
* 将根据当前配置的身份提供者尝试认证。
* 成功认证后，服务会返回授权和身份令牌。
* 客户端 SDK 将该授权令牌自动添加到原始请求，并将该请求重新发送到云资源。
* 服务器 SDK 从请求中抽取访问令牌，并使用 {{site.data.keyword.appid_short_notm}} 进行验证。授予访问权后，响应会返回给应用程序。


## 请求流程
{: #request}

下图描述了请求是如何从客户端 SDK 流向后端应用程序和身份提供者的。

![{{site.data.keyword.appid_short_notm}} 请求流程](/images/appidflow.png)


* 使用 {{site.data.keyword.appid_short_notm}} 客户端 SDK 对受 {{site.data.keyword.appid_short_notm}} 服务器 SDK 保护的后端资源发起请求。
* {{site.data.keyword.appid_short_notm}} 服务器 SDK 检测到未授权的请求，然后返回 HTTP 401 和授权作用域。
* 客户端 SDK 自动检测到 HTTP 401，然后启动认证过程。
* 当客户端 SDK 联系服务时，如果配置了多个身份提供者，那么服务器 SDK 返回登录窗口小部件。{{site.data.keyword.appid_short_notm}} 会调用身份提供者并为该提供者呈现登录表单，如果没有配置身份提供者，那么将返回授权代码，以允许他们进行认证。
* {{site.data.keyword.appid_short_notm}} 通过提供认证质询，要求客户端进行认证。
* 如果已配置 Facebook 或 Google，那么在用户登录时，各自的身份提供者 OAuth 流程会处理认证。
* 如果认证以相同的授权代码结束，那么该代码会发送到令牌端点。端点会返回两个令牌：访问令牌和身份令牌。从此刻开始，通过客户端 SDK 发起的请求全部具有新获取的 Authorization 头。
* 客户端 SDK 自动重新发送触发了授权流程的原始请求。
* 服务器 SDK 从请求中抽取 Authorization 头，通过服务对该头进行验证，然后授予对后端资源的访问权。

## 访问令牌和身份令牌
{: #access-and-identity}

{{site.data.keyword.appid_short}} 使用两种类型的令牌：访问令牌和身份令牌。令牌的格式为 <a href="https://jwt.io/introduction/" target="_blank">JSON Web 令牌 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。


### 访问令牌
{: #access-tokens notoc}

有了访问令牌，就可以与 {{site.data.keyword.appid_short_notm}} 授权过滤器保护的资源进行通信，请参阅[保护后端资源](/docs/services/appid/protecting-resources.html)。令牌符合 JavaScript 对象签名和加密 (JOSE) 规范，并且具有以下格式：

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

### 身份令牌
{: #identity-tokens notoc}

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


## 身份提供者概述
{: #identity-providers-overview}

可以在移动和 web 应用程序中使用以下身份提供者：

* **Facebook** - 用户使用自己的 Facebook 凭证登录到移动或 Web 应用程序。
* **Google** - 用户使用自己的 Google+ 凭证登录到移动或 Web 应用程序。
<!--* **Custom** - Bring your own identity provider. The identity providers should be compliant with OIDC. -->

## 使用缺省配置
{: #default-configuration}

初始设置身份提供者时，{{site.data.keyword.appid_short_notm}} 提供了缺省配置。缺省配置只能用于开发方式。对于每个身份提供者，这些凭证限制为每个 {{site.data.keyword.appid_short_notm}} 实例每天 100 次使用。在发布应用程序之前，请将缺省配置更新为您自己的凭证。要更新配置，请参阅[配置身份提供者](/docs/services/appid/identity-providers.html)。
