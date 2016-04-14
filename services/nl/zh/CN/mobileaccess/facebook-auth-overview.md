---

copyright:
  years: 2015, 2016

---

# 使用 Facebook 凭证认证用户
{: #facebook-auth-overview}
您可以将 {{site.data.keyword.amashort}} 服务配置为通过将 Facebook 用作身份提供者来保护资源。移动应用程序用户可以使用自己的 Facebook 凭证进行认证。

**重要信息**：您无需单独安装 Facebook SDK。配置 {{site.data.keyword.amashort}} 客户端 SDK 时，依赖关系管理器会自动安装 Facebook SDK。

## {{site.data.keyword.amashort}} 请求流程
{: #mca-facebook-sequence}

请参阅以下简化图，以了解 {{site.data.keyword.amashort}} 如何与 Facebook 集成进行认证。

![图像](images/mca-sequence-facebook.jpg)

1. 使用 {{site.data.keyword.amashort}} SDK 对受 {{site.data.keyword.amashort}} 服务器 SDK 保护的后端资源发起请求。
* {{site.data.keyword.amashort}} 服务器 SDK 检测到未授权的请求，然后返回 HTTP 401 代码和授权作用域。
* {{site.data.keyword.amashort}} 客户端 SDK 自动检测到上述 HTTP 401 代码，然后启动认证过程。
* {{site.data.keyword.amashort}} 客户端 SDK 访问 {{site.data.keyword.amashort}} 服务，并要求发出 Authorization 头。
* {{site.data.keyword.amashort}} 服务通过提供认证质询，要求客户端先向 Facebook 进行认证。
* {{site.data.keyword.amashort}} 客户端 SDK 使用 Facebook SDK 来启动认证过程。成功认证后，Facebook SDK 将返回 Facebook 访问令牌。
* Facebook 访问令牌被视为认证质询回复。该令牌会发送到 {{site.data.keyword.amashort}} 服务。
* 该服务将向 Facebook 服务器验证认证质询回复。
* 如果验证成功，{{site.data.keyword.amashort}} 服务会生成 Authorization 头，并将其返回给 {{site.data.keyword.amashort}} 客户端 SDK。Authorization 头包含两个令牌：一个是访问令牌，用于包含访问许可权信息；一个是标识令牌，用于包含有关当前用户、设备和应用程序的信息。
* 从此刻开始，通过 {{site.data.keyword.amashort}} 客户端 SDK 发起的所有请求都具有新获取的 Authorization 头。
* {{site.data.keyword.amashort}} 客户端 SDK 自动重新发送触发了授权流程的原始请求。
* {{site.data.keyword.amashort}} 服务器 SDK 从请求中抽取 Authorization 头，通过 {{site.data.keyword.amashort}} 服务对其进行验证，然后授予对后端资源的访问权。

## 从 Facebook 开发者门户网站获取 Facebook 应用程序标识
{: #facebook-appID}

要开始将 Facebook 用作身份提供者，必须在 Facebook 开发者门户网站中创建应用程序。在此过程中，您将获取 Facebook 应用程序标识，这是供 Facebook 用于确定哪个应用程序正在尝试进行连接的唯一标识。

1. 打开 [Facebook 开发者门户网站](https://developers.facebook.com)。

1. 单击顶部菜单中的**我的应用程序**，然后选择**新建应用程序**。
如果显示有选项供您选择 iOS 或 Android 应用程序，请选取其中一个应用程序，然后在下一个屏幕上单击**跳过并创建应用程序标识**。

1. 设置所选的应用程序显示名称，并选取类别。单击**创建应用程序标识**以继续。

1. 复制显示的**应用程序标识**。此值是您的 Facebook 应用程序标识。配置对移动应用程序的 Facebook 认证时需要此值。

## 后续步骤
{: #next-steps}

* [在 Android 应用程序中启用 Facebook 认证](facebook-auth-android.html)
* [在 iOS 应用程序 (Swift SDK) 中启用 Facebook 认证](facebook-auth-ios-swift-sdk.html)
* [在 iOS 应用程序 (Objective-C SDK) 中启用 Facebook 认证](facebook-auth-ios.html)
* [在 Cordova 应用程序中启用 Facebook 认证](facebook-auth-cordova.html)
