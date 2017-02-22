---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 为移动设备启用通知
{: #c_enable_push-notifications}
上次更新时间：2017 年 1 月 18 日
{: .last-updated}

请确保您已经完成[配置通知提供程序的凭证](t__main_push_config_provider.html)。

本部分描述了如何使您的客户机应用程序（移动、Web 浏览器应用程序以及 Chrome Apps and Extensions）能够接收推送通知，如何创建基本通知、获取和初始化SDK 或插件，以及如何注册您的设备或浏览器来接收推送通知。您还可以通过 [REST API](t_restapi.html) 使移动和 Web 浏览器应用程序能够接收推送通知。

**注**：对于设备、浏览器、Chrome Apps and Extensions 注册，{{site.data.keyword.mobilepushshort}} 服务会保持对通知提供者颁发的令牌的唯一引用。对于 Apple，通知提供者为 APNs；而对于 Google，则为 FCM。{{site.data.keyword.mobilepushshort}} 服务通知提供者可能会基于一些原因让令牌失效。 

例如，在设备上卸载应用程序期间。在这种情况下，如果有传递通知的尝试，通知提供者就会给出有关设备已失效的响应，{{site.data.keyword.mobilepushshort}} 服务会根据该响应来除去设备或 Web 浏览器注册。这样会抑制后续的尝试，阻止将通知发送给这些已失效的设备。
