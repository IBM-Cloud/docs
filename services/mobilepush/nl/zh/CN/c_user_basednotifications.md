---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 启用基于用户的通知
{: #user_based_notifications}
上次更新时间：2017 年 1 月 16 日
{: .last-updated}

基于用户标识的 {{site.data.keyword.mobilepushshort}} 针对具有定制消息的移动应用程序用户。使用基于用户的通知，您可以根据首选项选择通知特定个人。

## 使用用户标识注册设备
要按用户标识向目标推送通知，确保您在设置了用户标识字段的情况下注册设备。     

用户标识可以是应用程序提供给设备注册 API 的任何字符串。通常，移动应用程序首先会运行认证周期，在这期间会针对认证服务（如 [{{site.data.keyword.amafull}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html "外部链接图标"){: new_window}）认证移动应用程序用户。在成功认证之后，已认证的用户标识会传递至推送设备注册 API。 

## 同步用户登录和注销 

您可以选择仅在用户登录时发送通知。 

例如，假设设备由家庭或工作团队的成员共享，而您需要定址特定用户。在此用例中，将会有用户登录和注销序列。此认证机制允许应用程序跟踪应用程序当前用户的身份。这样确保针对特定用户的通知始终由该用户接收。成功登录之后，调用传递登录用户的用户标识的设备注册 API。同样，在注销之前，调用设备注销 API。使用登录和注销对这些 Push API 进行序列化可确保针对特定用户的通知仅会发送到该用户。
