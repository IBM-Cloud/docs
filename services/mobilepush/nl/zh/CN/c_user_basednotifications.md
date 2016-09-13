---

标题：启用基于用户的推送通知

关键字：基于用户的推送通知, userId
copyright:
 years: 2015, 2016

---

# 启用基于用户的通知
{: #user_based_notifications}
上次更新时间：2016 年 8 月 16 日
{: .last-updated}

基于用户标识的 {{site.data.keyword.mobilepushshort}} 针对具有定制消息的移动应用程序用户。基于用户的通知可以帮助参与的特定个人利用其自己的首选项和选择。  

## 使用用户标识注册设备
要按用户标识向目标推送通知，请确保您是使用用户标识注册设备的，并且还需要传递在供应 {{site.data.keyword.mobilepushshort}} 服务时分配的“clientSecret”。没有有效的“clientSecret”，设备注册将会失败。  

用户标识可以是应用程序提供给设备注册 API 的任何字符串。通常，移动应用程序首先会运行认证周期，在这期间会针对认证服务（如 [{{site.data.keyword.amafull}}](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html)）认证移动应用程序用户。在成功认证之后，已认证的用户标识会随“clientSecret”一起，传递至推送设备注册 API。“clientSecret”的存在仅会强制执行用户标识与移动设备注册的已授权关联。


秘密保存“clientSecret”，绝不要将其硬编码到移动应用程序中。可以使用多种应用程序初始化模式，在应用程序运行时，动态地拉入“clientSecret”。时序图概述了此模式。

![Enable_Push](images/init_client_secret.jpg) 

您还可以注册要与“匿名”用户相关联的设备。这需要您使用不需要用户标识和“clientSecret”自变量的设备注册 API 的变体。   

## 同步用户登录/注销并启用推送通知 

您可以选择仅在用户登录时发送通知。 

例如，如果设备由家庭或工作团队共享，而您需要定址家庭或团队中的特定用户。在此用例中，将会有用户登录和注销序列，保护应用程序跟踪应用程序当前用户的身份。要确保针对特定用户的通知始终只由该用户接收，请在成功登录之后，调用传递登录用户的用户标识的设备注册 API。同样，在注销之前，调用设备注销 API。使用登录和注销对这些 Push API 进行序列化可确保针对特定用户的推送通知仅会发送到该用户。
