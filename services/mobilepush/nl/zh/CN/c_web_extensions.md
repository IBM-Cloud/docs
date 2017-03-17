---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 让 Chrome Apps and Extensions 能够接收 {{site.data.keyword.mobilepushshort}} 
{: #web_notifications}
上次更新时间：2017 年 1 月 18 日
{: .last-updated}

您可以支持 Chrome Apps and Extensions 接收 {{site.data.keyword.mobilepushshort}}。请确保您已经完成[配置通知提供程序的凭证](t__main_push_config_provider.html)，然后再继续相关步骤。

## 安装客户机 SDK 以支持 {{site.data.keyword.mobilepushshort}}
{: #web_install}

本主题描述如何安装和使用客户机 JavaScript 推送 SDK 来进一步开发 Chrome Apps and Extensions。

### Google Chrome Apps and Extensions 中的初始化

要在 Chrome Apps and Extensions 中安装 JavaScript SDK，请完成以下步骤：

从 [Bluemix Web 推送 SDK ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master){: new_window} 下载 `BMSPushSDK.js` 和 `manifest_Chrome_Ext.json`（对于 Chrome Extensions）或 `manifest_Chrome_App.json`（对于 Chrome Apps）。



- 对于 Chrome Apps，请配置清单文件：
 1. 在 `manifest_Chrome_App.json` 文件中，提供名称、描述和图标。
 2. 在 `app.background.scripts` 中添加 `BMSPushSDK.js`。
 3. 将 `manifest_Chrome_App.json` 更改为 `manifest.json`。

- 对于 Chrome Extensions，请配置清单文件：
 1. 在 `manifest_Chrome_Ext.json` 文件中，提供名称、描述和图标。
 2. 在 `background.scripts` 中添加 `BMSPushSDK.js`。
 3. 将 `manifest_Chrome_Ext.json` 更改为 `manifest.json`。

在 `background.js` 文件中，添加以下内容以接收推送通知。 
```
chrome.gcm.onMessage.addListener(BMSPushBackground.onMessageReceived)
chrome.notifications.onClicked.addListener(BMSPushBackground.notification_onClicked);
chrome.notifications.onButtonClicked.addListener(BMSPushBackground.notifiation_buttonClicked); 
```
	{: codeblock}



## 初始化 推送 SDK 
{: #web_initialize}

通过 Bluemix {{site.data.keyword.mobilepushshort}} 服务 `app GUID` 和 `app Region` 初始化推送 SDK。  

要获取您的应用程序 GUID，在初始化的推送服务的导航窗格中选择**配置**选项，并单击**移动选项**。修改代码片段以使用 Bluemix 推送通知服务 appGUID 参数。 

`App Region` 指定托管 {{site.data.keyword.mobilepushshort}} 服务的位置。可以使用以下三个值中的一个值：

 - 对于美国达拉斯：`.ng.bluemix.net`
 - 对于英国：`.eu-gb.bluemix.net`
 - 对于悉尼：`.au-syd.bluemix.net`

```
    var bmsPush = new BMSPush();
    function callback(response) {
        alert(response.response)
    }
    var initParams = {
      "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
   "clientSecret":"clientSecret of your push service"
    }
  bmsPush.initialize(params, callback)
```
	{: codeblock}

## 注册 Chrome Apps and Extensions
{: #web_register}

使用 `register()` API 向 {{site.data.keyword.mobilepushshort}} 服务注册设备。对于从 Google Chrome 注册，请在 Bluemix {{site.data.keyword.mobilepushshort}} 服务 Web 配置仪表板中添加 Firebase 云消息传递 (FCM) 和 Google 云消息传递 (GCM) API 密钥和 Web 站点 URL。有关更多信息，请参阅 Chrome 设置下的[为 Google 云消息传递配置凭证](t_push_provider_android.html)。

对于从 Mozilla Firefox 注册，在 Firefox 设置下的 Bluemix {{site.data.keyword.mobilepushshort}} 服务 Web 配置仪表板中添加 Web 站点 URL。

使用以下代码片段在 Bluemix {{site.data.keyword.mobilepushshort}} 服务中注册。
```
    var bmsPush = new BMSPush();
    function callback(response) {
        alert(response.response)
    }
    var initParams = {
      "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
  "clientSecret":"clientSecret of your push service"
  }
  bmsPush.initialize(params, callback)
    bmsPush.register(function(response) {
      alert(response.response)
  })
```
    {: codeblock}




