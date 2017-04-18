---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 使用 Facebook 凭证认证用户
{: #facebook-auth-overview}

您可以将 {{site.data.keyword.amafull}} 服务配置为通过将 Facebook 用作身份提供者来保护资源。您的移动或 Web 应用程序用户可以使用自己的 Facebook 凭证进行认证。


{:shortdesc}

**重要信息**：您无需单独安装 Facebook 提供的客户端 SDK。配置
{{site.data.keyword.amashort}} Facebook 客户端 SDK 时，依赖关系管理器会自动安装
Facebook SDK。

## {{site.data.keyword.amashort}} 请求流程
{: #mca-facebook-sequence}

### 移动客户端请求流程

请参阅下图，以了解 {{site.data.keyword.amashort}} 如何从移动客户端应用程序与
Facebook 集成进
行认证。

![移动客户端请求流程图](images/mca-sequence-facebook.jpg)

* 使用 {{site.data.keyword.amashort}} 客户端 SDK 对受 {{site.data.keyword.amashort}} 服务器 SDK 保护的后端资源发起请求。
* {{site.data.keyword.amashort}} 服务器 SDK 检测到未授权的请求，然后返回 HTTP 401 代码和授权作用域。
* {{site.data.keyword.amashort}} 客户端 SDK 自动检测到上述 HTTP 401 代码，然后启动认证过程。
* {{site.data.keyword.amashort}} 客户端 SDK 访问 {{site.data.keyword.amashort}} 服务，并请求 Authorization 头。
* {{site.data.keyword.amashort}} 服务通过提供认证质询，要求客户端先向 Facebook 进行认证。
* {{site.data.keyword.amashort}} 客户端 SDK 使用 Facebook SDK 来启动认证过程。成功认证后，Facebook SDK 将返回 Facebook 访问令牌。
* Facebook 访问令牌被视为认证质询回复。该令牌会发送到 {{site.data.keyword.amashort}} 服务。
* 该服务将向 Facebook 服务器验证认证质询回复。
* 如果验证成功，{{site.data.keyword.amashort}} 服务会生成 Authorization 头，并将其返回给 {{site.data.keyword.amashort}} 客户端 SDK。Authorization 头包含两个令牌：一个是访问令牌，用于包含访问许可权信息；一个是标识令牌，用于包含有关当前用户、设备和应用程序的信息。
* 从此刻开始，通过 {{site.data.keyword.amashort}} 客户端 SDK 发起的所有请求都具有新获取的 Authorization 头。
* {{site.data.keyword.amashort}} 客户端 SDK 自动重新发送触发了授权流程的原始请求。
* {{site.data.keyword.amashort}} 服务器 SDK 从请求中抽取 Authorization 头，通过 {{site.data.keyword.amashort}} 服务对其进行验证，然后授予对后端资源的访问权。

### {{site.data.keyword.amashort}} Web 应用程序请求流程
{: #mca-facebook-web-sequence}

{{site.data.keyword.amashort}} Web 应用程序请求流程类似于移动客户端的流程。但是，{{site.data.keyword.amashort}} 保护 Web 应用程序而非 {{site.data.keyword.Bluemix_notm}} 后端资源。

  * Web 应用程序会发送初始请求（例如，通过登录表单）。
  * 最终重定向会指向 Web 应用程序本身的受保护区域，而非后端受保护资源。


## 在 Facebook for Developers Web 站点上创建应用程序。
{: #facebook-appID}

要开始将 Facebook 用作身份提供者，必须在 Facebook for Developers Web 站点上创建应用程序。在此过程中，将创建 Facebook 应用程序标识。这是供 Facebook 用于确定哪个应用程序正在尝试进行连接的唯一标识。

为移动应用程序或 Web 应用程序配置 Facebook 认证时需要此值。

1. 访问 [Facebook for Developers ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developers.facebook.com "外部链接图标"){: new_window} 站点。

1. 打开**我的应用程序**下拉列表，并选择**添加新应用程序**。

1. 输入**显示名称**和**联系人电子邮件**值，然后从下拉列表中选择**类别**。

1. 单击**新建应用程序标识**。

1. 可能会显示安全性检查。执行请求的操作。

1. 这将显示**产品设置**页面。复制显示的**应用程序标识**。

## 后续步骤
{: #next-steps}

* [启用 Android 应用程序的 Facebook 认证](facebook-auth-android.html)
* [启用 iOS 应用程序 (Swift SDK) 的 Facebook 认证](facebook-auth-ios-swift-sdk.html)
* [启用 Cordova 应用程序的 Facebook 认证](facebook-auth-cordova.html)
