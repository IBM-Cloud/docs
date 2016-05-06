---

copyright:
  years: 2015, 2016

---

# 入门
{: #getting-started}
要开始使用 {{site.data.keyword.amashort}}，您可以将 {{site.data.keyword.amashort}} 服务添加到现有 {{site.data.keyword.Bluemix}} 应用程序，也可以使用样板创建新的应用程序。  

## 创建 {{site.data.keyword.amashort}} 服务的实例
{: #service-instance}

您可以从 {{site.data.keyword.Bluemix}}“目录”创建新的 {{site.data.keyword.amashort}} 服务实例。如果不使用样板来创建新的移动后端，那么必须在现有后端上配置服务器 SDK。


  * **新建应用程序**：以下部分中的指示信息描述如何创建新的应用程序，用于创建移动后端并通过 {{site.data.keyword.amashort}} 服务器 SDK 对其进行保护。单击 **MobileFirst Services Starter** 样板以通过 {{site.data.keyword.amashort}} 服务创建新的应用程序。
  * **现有应用程序**：单击 {{site.data.keyword.amashort}} 图标，并创建绑定到现有应用程序的新服务实例。要在现有应用程序上配置服务器 SDK，请参阅[保护云资源](protecting-resources.html)。


## 使用 MobileFirst Services Starter 样板创建移动后端
{: #create-backend}
使用 MobileFirst Services Starter 时，您会获得在 IBM {{site.data.keyword.Bluemix_notm}} 上运行的 Node.js 运行时的实例，以实现定制后端逻辑。此外，还会将一组提供了安全性、数据、推送和监视功能的核心移动服务绑定到该 Node.js 应用程序。创建 {{site.data.keyword.Bluemix_notm}} Node.js 应用程序后，可设置开发环境，并开始使用 {{site.data.keyword.Bluemix_notm}} Mobile Services SDK。您可以使用 SDK 通过简单的 API 调用来访问绑定到云应用程序的服务。

1. 在 {{site.data.keyword.Bluemix_notm}}“目录”中，转至**样板**部分，然后单击 **MobileFirst Services Starter**。
1. 添加有关移动后端的信息，包括空间、名称、主机和服务套餐。
1. 单击**创建**。



## 后续步骤
{: #next-steps}
使用样板创建的 Node.js 应用程序的多个端点将通过 {{site.data.keyword.amashort}} 进行保护。要了解有关缺省移动后端应用程序的更多信息，请参阅 [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop)。

可以将移动应用程序设置为使用 {{site.data.keyword.amashort}} SDK。设置 SDK 后，可以开始在应用程序中设置认证和监视。遵循您的移动开发平台的指示信息：

* [Android](getting-started-android.html)
* [iOS (Swift SDK)](getting-started-ios.html)
* [iOS (Objective-C SDK)](getting-started-ios.html)
* [Cordova](getting-started-cordova.html)
