---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 关于 {{site.data.keyword.mobilepushshort}}
{: #overview-push}
上次更新时间：2017 年 1 月 18 日
{: .last-updated}

IBM {{site.data.keyword.mobilepushshort}} 是一项服务，您可以使用该服务将通知发送到设备和平台。通知可以针对所有应用程序用户，也可以针对一组使用标记的特定用户和设备。您可以管理设备、标记和预订。  

您可以使用以下任何选项，来创建绑定或未绑定服务：

- 通过从目录使用 MobileFirst Services Starter 样板创建 Bluemix 应用程序。这会创建绑定到 Bluemix 后端应用程序的 Push Notifications 服务。
- 通过从 Mobile 目录直接创建未绑定的 Push Notifications 服务。您可以稍后绑定到应用程序或者选择在未绑定的情况下使用它。 
- 通过使用 [Mobile 仪表板 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/docs/mobile/services.html){: new_window}。

请注意，{{site.data.keyword.mobilepushshort}} 监视选项卡并不显示分析数据。

{{site.data.keyword.mobilepushshort}} 服务现在支持 OpenWhisk。有关更多信息，请参阅 [OpenWhisk](/docs/openwhisk/index.html)。


## {{site.data.keyword.mobilepushshort}} 服务流程
{: #overview_push_process}

移动、Web 浏览器客户机和 Google Chrome Apps and Extensions 可以针对 {{site.data.keyword.mobilepushshort}} 服务进行预订和注册。客户端应用程序会在启动时自行注册并预订 {{site.data.keyword.mobilepushshort}} 服务。通知会分派到 Apple 推送通知服务 (APNs) 或 Firebase 云消息传递 (FCM)/Google 云消息传递 (GCM) 服务器，然后发送到注册的移动或浏览器客户端。

![推送概述](images/overview.jpg)


###移动和浏览器应用程序 
{: mobile-applications}

启动时，客户机应用程序会自行注册并预订 {{site.data.keyword.mobilepushshort}} 服务来接收通知。

###后端应用程序
{: backend-applications}

后端应用程序可以位于内部部署中，也可以位于公共云中。后端应用程序使用 {{site.data.keyword.mobilepushshort}} 服务将上下文相关通知发送给移动和浏览器应用程序用户。后端应用程序无需维护和管理用于发送推送通知的移动设备、浏览器代理程序和用户信息。相反，后端应用程序可以使用将用于对其进行管理和维护的 {{site.data.keyword.mobilepushshort}} 服务。

###应用程序后端所有者
{: app-backend-owner}

应用程序后端所有者会创建捆绑 {{site.data.keyword.mobilepushshort}} 服务实例的移动后端应用程序。应用程序后端所有者还会使用该服务搭配以 {{site.data.keyword.mobilepushshort}} 为目标的移动和浏览器应用程序，配置和设置 {{site.data.keyword.mobilepushshort}} 服务，以符合后端应用程序。

###{{site.data.keyword.mobilepushshort}} 服务
{: push-notification-service}

{{site.data.keyword.mobilepushshort}} 服务可管理与注册通知的移动设备和 Web 浏览器相关的所有信息。对于如何将通知发送给异构移动和 Web 浏览器平台，您的应用程序无需了解详细的技术信息，该服务会在其内部对所有这一切进行处理。

###网关
{: gateways}

平台特定的 Push Notifications 云服务（例如，IBM {{site.data.keyword.mobilepushshort}} 服务使用的 FCM/GCM 或 Apple 推送通知服务 (APNs)）将通知分派给移动和浏览器应用程序。

###推送安全
{: push-security}

{{site.data.keyword.mobilepushshort}} API 由两种类型的私钥进行保护：

- **appSecret**：“appSecret”会保护通常由后端应用程序调用的 API，如用于发送 {{site.data.keyword.mobilepushshort}} 的 API 和用于配置设置的 API。
- **clientSecret**：“clientSecret”会保护通常由移动客户端应用程序调用的 API。只有一个 API 与设备注册相关，且其相关联用户标识需要此“clientSecret”。从移动客户端调用的其他 API 没有一个需要 clientSecret。 

在将应用程序与 {{site.data.keyword.mobilepushshort}} 服务绑定在一起时，“appSecret”和“clientSecret”会分配给每一个服务实例。
请参阅 [REST API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://mobile.{DomainName}/imfpush/) 文档，以获取如何传递私钥以及相关联的 API 的更多信息。

**注**：仅在使用用户标识字段注册或更新设备时需要较早版本的应用程序来传递 clientSecret。移动和浏览器客户端调用的所有其他 API 不
需要 clientSecret。这些旧应用程序可以选择针对设备注册或更新调用继续使用 clientSecret。但是，强烈建议对所有客户端 API 调用强制执行 clientSecret 检查。要在现有应用程序中强制执行此检查，已发布了一个新的“verifyClientSecret”API。对于所有新的应用程序，将对所有客户端 API 调用强制执行 clientSecret 检查，而此行为无法使用“verfiyClientSecret”API 进行更改。

缺省情况下，客户端密钥验证仅在新应用程序中强制执行。允许现有的和新的应用程序使用 verifyClientSecret REST API 启用或停用客户端密钥验证。建议您强制执行客户端密钥验证，以避免向可能了解 applicationId 和 deviceId 的用户公开设备。

请确保秘密保存“clientSecret”，绝不要将其硬编码到移动应用程序中。可以使用多种应用程序初始化模式，在应用程序运行时，动态地拉入“clientSecret”。时序图概述了此可能模式。
![启用推送](images/init_client_secret.jpg) 

## {{site.data.keyword.mobilepushshort}} 类型
{: #overview-push-types}

###广播
{: broadcast}

当客户机应用程序在向 {{site.data.keyword.mobilepushshort}} 服务进行注册时即可开始接收广播。广播通知是向跨移动设备、浏览器安装，或实现为 Chrome 应用程序或扩展实例，以及针对 {{site.data.keyword.mobilepushshort}} 服务配置的所有应用程序实例发送的消息。缺省情况下，已启用 {{site.data.keyword.mobilepushshort}} 的任何应用程序都已启用广播通知。启用了 {{site.data.keyword.mobilepushshort}} 服务的应用程序都具有预定义的 Push.ALL 标记预订，服务器使用该标记来向所有设备广播通知消息。要使用 REST Push API 发送广播通知，请确保发布到消息资源时，“目标”是一个空的 JSON 文件。

###基于标记的通知
{: tag-based-notifications}

标记通知是针对预订了特定标记的所有设备的消息。基于标记的通知允许根据主题区域或主题对通知进行细分。通知接收方可以选择仅接收关于所关注主题的通知。因此，基于标记的通知提供了一种对接收方进行细分的方法。此功能可以定义标记，然后按标记发送和接收消息。消息的目标对象只包括已预订某标记的客户机应用程序实例（在移动、浏览器上或作为应用程序或扩展）。必须首先为应用程序创建标记，设置标记预订，然后再启动基于标记的通知。要使用 REST API 发送基于标记的通知，请确保发布到消息资源时提供了“tagNames”。

###单点广播通知
{: unicast-notifications}

单点广播通知是针对特定设备或用户的通知消息。单点广播通知不需要任何额外的设置，当应用程序启用了 {{site.data.keyword.mobilepushshort}} 时，缺省情况下就会启用单点广播通知。

但是，面向用户的单点广播通知要求在向 {{site.data.keyword.mobilepushshort}} 注册客户机移动设备或 Web 浏览器或 Chrome Apps and Extensions 时将用户标识与设备关联。   

通常，客户机应用程序首先会运行认证周期，在这期间会针对认证服务（如 [Mobile Client Access](docs/services/mobileaccess/index.html)）认证移动应用程序用户。在成功认证之后，已认证的用户标识会传递至推送设备注册 API。要通过 REST API 发送单点广播通知，请确保发布到消息资源时提供了 deviceId 或 userId。

###基于平台的通知
{: platform-based-notifications}

可将通知定向发送到特定的设备平台。例如，可以只将通知发送给所有 Android 用户或 Google Chrome 用户。要使用 REST API 发送基于平台的通知，请确保发布到消息资源时提供了目标平台。将平台指定为数组。支持的平台如下所示：
* A (Apple) 
* G (Google)
* WEB_CHROME（Google Chrome 浏览器 Web 推送）
* WEB_FIREFOX（Mozilla Firefox 浏览器 Web 推送）
* WEB_SAFARI（Safari 浏览器 Web 推送）
* APPEXT_CHROME (Google Chrome Apps & Extensions)

## {{site.data.keyword.mobilepushshort}} 消息大小
{: #push-message-size}

{{site.data.keyword.mobilepushshort}} 消息有效内容大小取决于网关（FCM/GCM、APNs）和客户机平台规定的约束。 

### iOS 和 Safari
{: ios-message-size}

对于 iOS 8 和更高版本，所允许的最大大小为 2 KB。Apple 推送通知服务不会发送超过此限制的通知。

###Android、Firefox 浏览器、Chrome 浏览器以及 Chrome Apps & Extensions 
{: android-message-size}

允许的消息有效内容最大大小限制为 4 KB。  
