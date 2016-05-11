---

copyright:
  years: 2015, 2016
  
---

# 配置 {{site.data.keyword.amashort}} 进行定制认证
{: #custom-dash}
要将定制认证用于移动应用程序，必须在 {{site.data.keyword.amashort}} 服务仪表板中注册定制身份提供者的定制认证域和基本 URL。

## 开始之前
{: #custom-dash-begin}
* 请阅读[入门](getting-started.html)。
* 使用 {{site.data.keyword.amashort}} 服务器 SDK 保护后端应用程序。有关更多信息，请参阅[保护资源](protecting-resources.html)。
* 让定制身份提供者应用程序开始运行。

## 在 {{site.data.keyword.Bluemix}}“仪表板”中配置定制认证
{: #custom-dash-config}
使用 {{site.data.keyword.amashort}}“仪表板”可配置定制认证。

1. 在 {{site.data.keyword.Bluemix}}“仪表板”中打开应用程序。

1. 单击**移动选项**，然后记录**路径** (`applicationRoute`) 和**应用程序 GUID** (`applicationGUID`)。初始化 SDK 时需要这些值。

1. 单击 {{site.data.keyword.amashort}} 磁贴。这将装入 {{site.data.keyword.amashort}}“仪表板”。

1. 单击**定制**磁贴。

1. 输入定制身份提供者的**域名** 和**基本 URL**，然后保存更改。

## 后续步骤
{: #next-steps}
* [针对 Android 配置定制认证](custom-auth-android.html)
* [针对 iOS 配置定制认证](custom-auth-ios.html)
* [针对 Cordova 配置定制认证](custom-auth-cordova.html)
