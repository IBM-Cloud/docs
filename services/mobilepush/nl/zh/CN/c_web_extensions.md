---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 使 Chrome Apps and Extensions 能够接收推送通知
{: #web_notifications}
上次更新时间：2017 年 4 月 12 日
{: .last-updated}

您可以支持 Chrome Apps and Extensions 接收 {{site.data.keyword.mobilepushshort}}。请确保您已经完成[配置通知提供程序的凭证](t__main_push_config_provider.html)，然后再继续相关步骤。

## 安装客户机 SDK 以支持 Push Notifications
{: #web_install}

本主题描述如何安装和使用客户机 JavaScript 推送 SDK 来进一步开发 Chrome Apps and Extensions。

### Google Chrome Apps and Extensions 中的初始化
{: #initialize_google_extn_app}

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



### 初始化 推送 SDK 
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

### 注册 Chrome Apps and Extensions
{: #web_register}

使用 `register()` API 向 {{site.data.keyword.mobilepushshort}} 服务注册设备。要从 Google Chrome 注册，请在 Bluemix {{site.data.keyword.mobilepushshort}} 服务 Web 配置仪表板中添加 Firebase 云消息传递 (FCM) API 密钥和 Web 站点 URL。有关更多信息，请参阅[配置通知提供程序的凭证](t__main_push_config_provider.html)。 

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


## 向 Chrome Apps and Extensions 发送基本通知 
{: #web_extensions_notifications}

开发应用程序后，可以发送推送通知。 

1. 选择**发送通知**，并通过选择 **Web 通知**作为**发送至**选项来编辑消息。 
2. 键入需要在**消息**字段中传递的消息。
3. 您可以选择提供可选设置：
  - **通知标题**：这是作为消息警报标题显示的文本。
  - **通知图标 URL**：如果您的消息需要与应用程序通知图标一起传递，请在字段中提供图标的链接。
  - **折叠键**：折叠键附加在通知上。如果设备脱机时多个通知使用相同的折叠键按顺序抵达，那么将折叠通知。在设备联机时，将从 FCM/GCM 服务器接收通知，并只显示带有相同折叠键的最新通知。如果没有设置折叠键，将存储新和旧的消息，以在以后传递。
  - **生存时间**：此值以秒为单位进行设置。如果未指定此参数，FCM/GCM 服务器将把消息存储 4 周时间并将尝试传递。4 周后有效性到期。值可以为 0 至 2,419,200 秒之间的值。
  - **空闲时延迟**：将此值设置为 `true` 将指示 FCM/GCM 服务器在设备空闲时不要传递通知。将此值设置为 `false`，以确保在设备空闲时传递通知。
  - **其他有效内容**：为您的通知指定定制的有效内容值。

下面的图像显示仪表板中的 Chrome Apps and Extensions 通知选项。

  ![“通知”屏幕](images/push_chrome_extns.jpg)
  
### 后续步骤
{: #next_steps_tags}

成功设置基本通知后，可以选择配置基于标记的通知和高级选项。

将这些 {{site.data.keyword.mobilepushshort}} 服务功能添加到应用程序中。要使用基于标记的通知，请参阅[基于标记的通知](c_tag_basednotifications.html)。要使用高级通知选项，请参阅[高级通知](t_advance_badge_sound_payload.html)。



