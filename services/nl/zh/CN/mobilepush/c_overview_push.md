---

copyright:
 years: 2015, 2016

---

# 关于推送通知
{: #overview-push}

推送通知是一种服务，可用于将通知发送到 iOS 和 Android 设备。通知可以针对所有应用程序用户，也可以针对一组使用标记的特定用户和设备。您可以管理设备、标记和预订。还可以使用 SDK（软件开发包）和具象状态传输 (REST) 应用程序编程接口 (API) 来进一步开发您的客户机应用程序。有关 Push 专用服务的信息，请参阅[专用服务](../../dedicated/index.html)。 


## Push Notification Service 过程
{: #overview_push_process}

移动客户端可以预订和注册 Push Notification Service。启动时，移动应用程序会自行注册并预订 Push Notification Service。通知会分派到 Apple 推送通知服务 (APNs) 或 Google 云消息传递 (GCM) 服务器，然后发送到注册的移动客户端。

![推送概述](images/overview.jpg)


###移动应用程序

启动时，移动应用程序会自行注册并预订 Push Notification Service 来接收通知。

###后端应用程序

后端应用程序可以位于内部部署中，也可以位于公共云中。后端应用程序使用 Push Notification Service 将上下文相关通知发送给移动用户。后端应用程序无需维护和管理用于发送推送通知的移动设备和用户信息。后端应用程序可以使用 Push Notification Service 来执行这些操作。

###应用程序后端所有者

创建移动后端应用程序的角色，该移动后端应用程序捆绑了 Push Notification Service 实例。此人员会配置并设置 Push Notification Service，以适合使用 Push Notification Service 的后端应用程序和作为推送通知目标的移动应用程序。

###Push Notification Service

Push Notification Service 管理与注册通知的设备相关的所有信息。对于如何将通知发送给这些异构移动平台，您的应用程序无需了解详细的技术信息，该服务会在其内部对所有这一切进行处理。

###网关

移动设备平台特定的云服务（例如，Google 云消息传递 (GCM) 或 Apple 推送通知服务 (APNs)）使用 Push Notification Service 将通知分派给移动应用程序。

## 推送通知类型
{: #overview-push-types}

###广播

移动应用程序在向 Push Notifications Service 进行注册后即可开始接收广播。广播通知是针对安装了应用程序并进行了 Push Notification Service 配置的所有设备的通知消息。缺省情况下，已启用推送通知的任何应用程序都已启用广播通知。任何启用了 Push Notification Service 的应用程序都具有预定义的 Push.ALL 标记预订，服务器使用该标记来向所有设备广播通知消息。要使用 REST Push API 发送广播通知，请确保发布到消息资源时，“目标”是一个空的 JSON 文件。

###基于标记的通知

标记通知是针对已预订特定标记的所有设备的通知消息。基于标记的通知允许根据主题区域或主题对通知进行细分。通知接收方可以选择仅接收关于所关注主题的通知。因此，基于标记的通知提供了一种对接收方进行细分的方法。此功能可以定义标记，然后按标记发送和接收消息。消息的目标对象只包括已预订某标记的设备。必须首先为应用程序创建标记，设置标记预订，然后再启动基于标记的通知。要使用 REST API 发送基于标记的通知，请确保发布到消息资源时提供了“tagNames”。

###单点广播通知

单点广播通知是针对特定设备的通知消息。单点广播通知不需要任何额外的设置，当应用程序启用了推送通知时，缺省情况下就会启用单点广播通知。要使用 REST API 发送单点广播通知，请确保发布到消息资源时提供了 deviceId。

###基于平台的通知

可将通知定向发送到特定的设备平台。例如，可以只将通知发送给所有 Android 用户。要使用 REST API 发送基于平台的通知，请确保发布到消息资源时提供了目标平台。将平台指定为数组。支持的平台如下所示：
* A (Apple) 
* G (Google)
