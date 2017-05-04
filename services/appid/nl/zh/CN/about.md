---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# 工作原理
{: #about}

您可以了解 {{site.data.keyword.appid_short_notm}} 所使用的组件、体系结构和请求流程。
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
{: #architecture}

利用 {{site.data.keyword.appid_short_notm}}，您可以通过要求用户登录来提高应用程序安全性级别。您还可以使用服务器 SDK 来保护后端资源。

下图显示了 {{site.data.keyword.appid_short_notm}} 服务的工作原理概述。

![{{site.data.keyword.appid_short_notm}} 体系结构图](/images/appid_architecture2.png)

图 1. {{site.data.keyword.appid_short_notm}} 体系结构图

<dl>
  <dt> 客户端 SDK</dt>
    <dd> 客户端 SDK 用于与云资源进行通信的请求类。客户端 SDK 在检测到授权质询时将自动启动认证流程。</dd>
  <dt> Bluemix</dt>
    <dd>  服务器 SDK 从请求中抽取访问令牌，并使用 {{site.data.keyword.appid_short_notm}} 进行验证。成功认证后，{{site.data.keyword.appid_short_notm}} 会将授权和身份令牌返回到应用程序。</dd>
  <dt> 身份提供者</dt>
    <dd> 您可以配置 Facebook 和/或 Google 来认证应用程序。</dd>
</dl>


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
* 如果认证以相同的授权代码结束，那么该代码会发送到令牌端点。端点会返回两个令牌：访问令牌和身份令牌。从此刻开始，通过客户端 SDK 发起的请求全部具有新获取的授权头。
* 客户端 SDK 自动重新发送触发了授权流程的原始请求。
* 服务器 SDK 从请求中抽取授权头，通过服务对该头进行验证，然后授予对后端资源的访问权。
