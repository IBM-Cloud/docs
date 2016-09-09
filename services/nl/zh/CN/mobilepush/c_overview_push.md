---

copyright:
 years: 2015, 2016

---

# 关于 {{site.data.keyword.mobilepushshort}}
{: #overview-push}
上次更新时间：2016 年 8 月 16 日
{: .last-updated}

IBM {{site.data.keyword.mobilepushshort}} 是一种服务，可用于将通知发送到 iOS 和 Android 设备。通知可以针对所有应用程序用户，也可以针对一组使用标记的特定用户和设备。您可以管理设备、标记和预订。还可以使用 SDK（软件开发包）和具象状态传输 (REST) 应用程序编程接口 (API) 来进一步开发您的客户机应用程序。 

此外，{{site.data.keyword.mobilepushshort}} 还作为一种 Bluemix Dedicated 服务提供。有关 {{site.data.keyword.mobilepushshort}} 专用服务的信息，请参阅[专用服务](../../dedicated/index.html)。请注意，{{site.data.keyword.mobilepushshort}} 监视选项卡并不显示分析数据。

{{site.data.keyword.mobilepushshort}} 服务现在支持 OpenWhisk。有关更多信息，请参阅 [OpenWhisk](../../openwhisk/index.html)。


## {{site.data.keyword.mobilepushshort}} 服务流程
{: #overview_push_process}

移动客户端可以预订和注册 {{site.data.keyword.mobilepushshort}} 服务。移动应用程序会在启动时自行注册并预订 {{site.data.keyword.mobilepushshort}} 服务。通知会分派到 Apple 推送通知服务 (APNs) 或 Google 云消息传递 (GCM) 服务器，然后发送到注册的移动客户端。

![推送概述](images/overview.jpg)


###移动应用程序
{: mobile-applications}

移动应用程序会在启动时自行注册并预订 {{site.data.keyword.mobilepushshort}} 服务来接收通知。

###后端应用程序
{: backend-applications}

后端应用程序可以位于内部部署中，也可以位于公共云中。后端应用程序使用 {{site.data.keyword.mobilepushshort}} 服务将上下文相关通知发送给移动用户。后端应用程序无需维护和管理用于发送推送通知的移动设备和用户信息。相反，后端应用程序可以使用 {{site.data.keyword.mobilepushshort}} 服务。

###应用程序后端所有者
{: app-backend-owner}

应用程序后端所有者会创建捆绑 {{site.data.keyword.mobilepushshort}} 服务实例的移动后端应用程序。应用程序后端所有者还会使用该服务搭配以 {{site.data.keyword.mobilepushshort}} 为目标的移动应用程序，配置和设置 {{site.data.keyword.mobilepushshort}} 服务，以符合后端应用程序。

###{{site.data.keyword.mobilepushshort}} 服务
{: push-notification-service}

{{site.data.keyword.mobilepushshort}} 服务可管理与注册通知的设备相关的所有信息。对于如何将通知发送给异构移动平台，您的应用程序无需了解详细的技术信息，该服务会在其内部对所有这一切进行处理。

###网关
{: gateways}

移动设备平台特定的云服务（例如，Google 云消息传递 (GCM) 或 Apple 推送通知服务 (APNs)）使用 {{site.data.keyword.mobilepushshort}} 服务将通知分派给移动应用程序。

###推送安全
{: push-security}

{{site.data.keyword.mobilepushshort}} API 由两种类型的私钥进行保护 - i) appSecret ii) clientSecret。“appSecret”会保护通常由后端应用程序调用的 API，如发送 {{site.data.keyword.mobilepushshort}} 的 API、配置设置的 API。“clientSecret”会保护通常由移动客户端应用程序调用的 API。现在，仅有一个与使用相关联 UserId 注册设备相关的 API 需要此“clientSecret”。从移动客户端调用的所有其他 API 不需要 clientSecret。在将应用程序与 {{site.data.keyword.mobilepushshort}} 服务绑定在一起时，“appSecret”和“clientSecret”会分配给每一个服务实例。请参阅 ReST API 文档，以获取如何传递私钥以及涉及哪些 API 的相关信息。

## {{site.data.keyword.mobilepushshort}} 类型
{: #overview-push-types}

###广播
{: broadcast}

移动应用程序在向 {{site.data.keyword.mobilepushshort}} 服务进行注册后即可开始接收广播。广播通知是向针对 {{site.data.keyword.mobilepushshort}} 服务安装和配置了应用程序的所有设备发送的消息。缺省情况下，已启用 {{site.data.keyword.mobilepushshort}} 的任何应用程序都已启用广播通知。启用了 {{site.data.keyword.mobilepushshort}} 服务的应用程序都具有预定义的 Push.ALL 标记预订，服务器使用该标记来向所有设备广播通知消息。要使用 REST Push API 发送广播通知，请确保发布到消息资源时，“目标”是一个空的 JSON 文件。

###基于标记的通知
{: tag-based-notifications}

标记通知是针对预订了特定标记的所有设备的消息。基于标记的通知允许根据主题区域或主题对通知进行细分。通知接收方可以选择仅接收关于所关注主题的通知。因此，基于标记的通知提供了一种对接收方进行细分的方法。此功能可以定义标记，然后按标记发送和接收消息。消息的目标对象只包括已预订某标记的设备。必须首先为应用程序创建标记，设置标记预订，然后再启动基于标记的通知。要使用 REST API 发送基于标记的通知，请确保发布到消息资源时提供了“tagNames”。

###单点广播通知
{: unicast-notifications}

单点广播通知是针对特定设备或用户的通知消息。单点广播通知不需要任何额外的设置，当应用程序启用了 {{site.data.keyword.mobilepushshort}} 时，缺省情况下就会启用单点广播通知。

但是，针对用户的单点广播通知需要：

- 在注册推送通知的移动设备时，将用户标识与设备相关联。  

- 在将后端应用程序绑定到 {{site.data.keyword.mobilepushshort}} 服务时通过传递分配的“clientSecret”，来授权这样的用户标识注册。 

通常，移动应用程序首先会运行认证周期，在这期间会针对认证服务（如 [Mobile Client Access](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html)）认证移动应用程序用户。在成功认证之后，已认证的用户标识会随 clientSecret 一起，传递至推送设备注册 API。clientSecret 的存在仅会强制执行用户标识与移动设备注册的已授权关联。
要通过 REST API 发送单点广播通知，请确保发布到消息资源时提供了 deviceId 或 userId。

###基于平台的通知
{: platform-based-notifications}

可将通知定向发送到特定的设备平台。例如，可以只将通知发送给所有 Android 用户。要使用 REST API 发送基于平台的通知，请确保发布到消息资源时提供了目标平台。将平台指定为数组。支持的平台如下所示：
* A (Apple) 
* G (Google)

## {{site.data.keyword.mobilepushshort}} 消息大小
{: #push-message-size}

{{site.data.keyword.mobilepushshort}} 消息的有效内容大小取决于介体。 

###iOS
{: ios-message-size}

对于 iOS 8 和更高版本，所允许的最大大小为 2 KB。Apple 推送通知服务不会发送超过此限制的通知。

###Android
{: android-message-size}

Android 平台上没有限制。
