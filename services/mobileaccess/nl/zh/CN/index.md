---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.amashort}} 入门
{: #gettingstarted}

使用 {{site.data.keyword.amafull}} 服务，将安全性添加到移动应用程序。您可以配置客户端权限，以访问在 {{site.data.keyword.Bluemix}} 上运行的受保护后端资源。使用身份提供者（Google 和 Facebook）或定制身份来认证用户，并授予对受保护后端资源和 Web 应用程序的访问权。
{:shortdesc}

**注：**{{site.data.keyword.amashort}} 服务先前称为 Advanced Mobile Access。


要启动和运行 {{site.data.keyword.amashort}} 服务：

1. 使用以下某个选项来创建绑定和未绑定服务：
 * 使用目录中的 **MobileFirst Services Starter** 样板来创建 {{site.data.keyword.Bluemix_notm}} 应用程序。这将创建绑定到 {{site.data.keyword.Bluemix_notm}} 后端应用程序的 {{site.data.keyword.amashort}} 服务。
 * 使用 {{site.data.keyword.amashort}} 控制台创建 {{site.data.keyword.amashort}} 服务。可以在 {{site.data.keyword.amashort}} 控制台中将该服务与现有后端应用程序绑定，并对其进行配置。

   使用 MobileFirst Services Starter 时，您会获得在 IBM {{site.data.keyword.Bluemix_notm}} 上运行的 Node.js 运行时的实例，以实现定制后端逻辑。此外，还会将一组提供了安全性、数据、推送和监视功能的核心移动服务绑定到该 Node.js 应用程序。创建 {{site.data.keyword.Bluemix_notm}} Node.js 应用程序后，可设置开发环境，并开始使用 {{site.data.keyword.Bluemix_notm}} Mobile Services SDK。您可以使用 SDK 通过简单的 API 调用来访问绑定到云应用程序的服务。

	有关如何创建和使用项目、应用程序和服务的更多信息，请参阅 [IBM Bluemix Mobile 仪表板](https://console.{DomainName}/docs/mobile/index.html)。

2. 保护服务器端资源。

   通过支持移动的 OAuth 安全性，保护正在 Node.js 或 Liberty for Java&trade; 运行时上运行的移动后端资源。有关更多信息，请参阅[保护资源](protecting-resources.html)。要了解有关缺省移动后端应用程序的更多信息，请参阅 [bms-hellotodo-strongloop ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop "外部链接图标"){: new_window} 样本应用程序。

3. 设置核心 {{site.data.keyword.amashort}} 开发环境。

  ####客户端开发
  {: #client-development}

	您可以将 {{site.data.keyword.amashort}} SDK 添加到现有 Android、iOS 或 Cordova 应用
程序，具体方法如下：
   * Android：（[设置 Android SDK](getting-started-android.html)）[样本 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication "外部链接图标"){: new_window}
    * iOS (Swift SDK)：（[设置 iOS Swift SDK](getting-started-ios-swift-sdk.html)）[样本 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "外部链接图标"){: new_window}    
   * Cordova：（[设置 Cordova 插件](getting-started-cordova.html)）[样本 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication "外部链接图标"){: new_window}


 ####Web 开发
 {: #web-development}

   {{site.data.keyword.amashort}} 服务可以保护 Web 应用程序而无需任何特殊的 SDK。除了 {{site.data.keyword.amashort}} 服务提供的保护之外，您还可以利用不同的身份提供者。{{site.data.keyword.amashort}} 集成可支持使用任何实现技术的任何 Web 应用程序来利用 OAuth2 协议。有关设置 {{site.data.keyword.amashort}} Web 应用程序以使用不同身份提供者访问 {{site.data.keyword.amashort}} 服务的更多信息，请参阅：

   * [启用 Web 应用程序的 Facebook 认证](facebook-auth-web.html)
   * [启用 Web 应用程序的 Google 认证](google-auth-web.html)
   * [启用 Web 应用程序的定制认证](custom-auth-web.html)

**可选：**为应用程序配置身份提供者。可以为每个应用程序配置一个身份提供者。配置身份提供者使移动应用程序的用户能够使用其现有 Facebook 或 Google+ 帐户登录。或者，您可以定义用户如何通过创建定制认证来登录。
   * [使用 Facebook 凭证认证用户](facebook-auth-overview.html)
   * [使用 Google 凭证认证用户](google-auth-overview.html)
   * [使用定制身份提供者认证用户](custom-auth.html)

## 教程和样本
{: #samples}

* [android-helloauthentication 样本 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication "外部链接图标"){: new_window}
* [ios-helloauthentication 样本 (Swift SDK) ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "外部链接图标"){: new_window}

## SDK
{: #sdk}

* [核心 SDK (Android) ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core "外部链接图标"){: new_window}

* [ios-helloauthentication 样本 (Swift SDK) ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "外部链接图标"){: new_window}

* [定制认证 - 简单样本 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "外部链接图标"){: new_window}

* [定制认证 - 高级样本 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management "外部链接图标"){: new_window}


