---

copyright:
  years: 2015, 2016
  
---

{:shortdesc: .shortdesc}

# {{site.data.keyword.amashort}} 入门
{: #getting-started}

{{site.data.keyword.amafull}} 服务为移动应用程序提供了安全性和监视功能。您可以配置客户机认证和身份提供者。此外，还可以向应用程序添加监视功能，以同时支持客户机日志记录和使用情况统计信息。

注：Mobile Client Access 服务先前称为 Advanced Mobile Access。
{: shortdesc}

1. 在 Bluemix 中设置移动后端，并在移动应用程序中配置 SDK。有关更多信息，请参阅[入门](getting-started.html)。
1. 保护服务器端资源。通过支持移动的 OAuth 安全性，保护正在 Node.js 或 Liberty for Java&trade; 运行时上运行的移动后端资源。有关更多信息，请参阅[保护资源](protecting-resources.html)。
1. 可选：为应用程序配置身份提供者。可以每个应用程序配置一个身份提供者。配置身份提供者使移动应用程序的用户能够使用其现有 Facebook 或 Google+ 帐户登录。或者，您可以定义用户如何通过创建定制认证来登录。
   * [Facebook](facebook-auth-overview.html)
   * [Google](google-auth-overview.html)
   * [定制](custom-auth.html)
1. 配置应用程序监视和日志记录。有关更多信息，请参阅[应用程序监视](app-monitoring.html)。


># 相关链接 {:class="linklist"}
>## 教程和样本 {:id="samples"}
>* [android-helloauthentication](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication)
>* [ios-helloauthentication](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication)
>
># 相关链接 {:class="linklist"}
>## API 参考 {:id="api"}
>* [核心 API 参考 (Android)](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
>* [核心 API 参考 (iOS)](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)
>
># 相关链接 {:class="linklist"}
>## SDK {:id="sdk"}
>* [核心 SDK (iOS) ](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)  
>* [bms-clientsdk-android-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)
>* [bms-clientsdk-cordova-plugin-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)
>
>{:elementKind="article" id="rellinks"}
