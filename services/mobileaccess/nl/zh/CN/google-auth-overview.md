---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

{{site.data.keyword.amafull}} 服务已替换为 {{site.data.keyword.appid_full}} 服务。


# 使用 Google 凭证认证用户
{: #google-auth}

您可以将 {{site.data.keyword.amafull}} 服务配置为将 Google 用作身份提供者来保护资源。然后，您的移动或 Web 应用程序用户可以使用自己的 Google 凭证进行认证。
{:shortdesc}

**重要信息**：您无需单独安装 Google 提供的客户端 SDK。配置
{{site.data.keyword.amashort}} 客户端 SDK 时，依赖关系管理器会自动安装 Google SDK。

## {{site.data.keyword.amashort}} 请求流程
{: #google-auth-overview}

### 客户端请求流程

请参阅下图，以了解 {{site.data.keyword.amashort}} 如何与 Google 集成进行
认证。

![客户端请求流程图](images/mca-sequence-google.jpg)

* 使用 {{site.data.keyword.amashort}} SDK 对受 {{site.data.keyword.amashort}} 服务器 SDK 保护的后端资源发起请求。
* {{site.data.keyword.amashort}} 服务器 SDK 检测到未授权的请求，然后返回 HTTP 401 代码和授权作用域。
* {{site.data.keyword.amashort}} 客户端 SDK 自动检测到上述 HTTP 401 代码，然后启动认证过程。
* {{site.data.keyword.amashort}} 客户端 SDK 访问 {{site.data.keyword.amashort}} 服务，并请求 Authorization 头。
* {{site.data.keyword.amashort}} 服务通过提供认证质询，要求客户端先向 Google 进行认证。
* {{site.data.keyword.amashort}} 客户端 SDK 使用 Google SDK 来启动认证过程。成功认证后，Google SDK 将返回 Google 访问令牌。
* Google 访问令牌被视为认证质询回复。该令牌会发送到 {{site.data.keyword.amashort}} 服务。
* 该服务将向 Google 服务器验证认证质询回复。
* 如果验证成功，{{site.data.keyword.amashort}} 服务会生成 Authorization 头，并将其返回给 {{site.data.keyword.amashort}} 客户端 SDK。Authorization 头包含两个令牌：一个是访问令牌，用于包含访问许可权信息；一个是标识令牌，用于包含有关当前用户、设备和应用程序的信息。
* 从此刻开始，通过 {{site.data.keyword.amashort}} 客户端 SDK 发起的所有请求都具有新获取的 Authorization 头。
* {{site.data.keyword.amashort}} 客户端 SDK 自动重新发送触发了授权流程的原始请求。
* {{site.data.keyword.amashort}} 服务器 SDK 从请求中抽取 Authorization 头，通过 {{site.data.keyword.amashort}} 服务对其进行验证，然后授予对后端资源的访问权。


### {{site.data.keyword.amashort}} Web 应用程序请求流程
{: #mca-google-web-sequence}
{{site.data.keyword.amashort}} Web 应用程序请求流程类似于移动客户端的流程。但是，{{site.data.keyword.amashort}} 保护 Web 应用程序而非 {{site.data.keyword.Bluemix_notm}} 后端资源。

  * Web 应用程序会发送初始请求（例如，通过登录表单）。
  * 最终重定向会指向 Web 应用程序本身的受保护区域，而非后端受保护资源。



## 后续步骤
{: #google-auth-nextsteps}

* [启用 Android 应用程序的 Google 认证](google-auth-android.html)
* [启用 iOS 应用程序 (Swift SDK) 的 Google 认证](google-auth-ios-swift-sdk.html)
* [启用 Cordova 应用程序的 Google 认证](google-auth-cordova.html)
