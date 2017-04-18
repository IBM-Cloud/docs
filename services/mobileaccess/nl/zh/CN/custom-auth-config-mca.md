---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-07"

---

**重要信息：{{site.data.keyword.amafull}} 服务已替换为 {{site.data.keyword.appid_full}} 服务。**

# 配置 Mobile Client Access 进行定制认证
{: #custom-dash}


要将定制认证用于移动应用程序，必须在 {{site.data.keyword.amashort}} 服务仪表板中注册定制身份提供者的定制认证域和基本 URL。

## 开始之前
{: #custom-dash-begin}
您必须具有：
* {{site.data.keyword.amafull}} 服务的实例。
* 定制身份提供者应用程序。

## 在仪表板中配置定制认证
{: #custom-dash-config}

使用 {{site.data.keyword.amafull}}“仪表板”可配置定制认证。

1. 在 {{site.data.keyword.amafull}}“仪表板”中打开服务。
1. 在**管理**选项卡中，将**授权**切换为“开启”。
1. 展开**定制**部分。
1. 输入**域名**和**定制身份提供者 URL**。仅 Web 应用程序需要 **Web 应用程序重定向 URI** 值。

## 后续步骤
{: #next-steps}
* [针对 Android 配置定制认证](custom-auth-android.html)
* [针对 iOS 配置定制认证](custom-auth-ios-swift-sdk.html)
* [针对 Cordova 配置定制认证](custom-auth-cordova.html)
