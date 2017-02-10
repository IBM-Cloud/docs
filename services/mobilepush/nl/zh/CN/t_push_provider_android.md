---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 为 FCM 配置凭证
{: #create-push-enable-gcm}
上次更新时间：2017 年 1 月 16 日
{: .last-updated}

Firebase 云消息传递 (FCM) 是用于向 Android 设备和 Google Chrome 传递推送通知的网关。FCM 是 Google 云消息传递 (GCM) 的新版本。要在仪表板上设置 {{site.data.keyword.mobilepushshort}} 服务，您需要获取 FCM 凭证。请确保您为新应用程序使用 FCM 配置。现有应用程序将继续以 GCM 配置运作。

##获取发送方标识和 API 密钥
{: #android-senderid-apikey}

API 密钥以安全方式存储，并由 {{site.data.keyword.mobilepushshort}} 服务用于连接到 FCM 服务器，而发送方标识（项目编号）由客户机端的适用于 Google Chrome 和 Mozilla Firefox 的 Android SDK 和 JS SDK 使用。 

要设置 FCM，产生 API 密钥和发送方标识，请完成以下步骤：

1. 访问 [Firebase 控制台 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.firebase.google.com/?pli=1 "外部链接图标"){: new_window}。
2. 选择**创建新项目**。 
3. 在“创建项目”窗口中，提供项目名称，选择国家/地区并单击**创建项目**。
3. 在导航窗格中，单击“设置”图标并选择**项目设置**。
4. 选择“云消息传递”选项卡，以生成服务器 API 密钥和发送方标识。

##针对 Android 和 Chrome Apps and Extensions 设置 {{site.data.keyword.mobilepushshort}} 服务
{: #setup-push-android}

**注：**您将需要 FCM/GCM API 密钥和发送方标识（项目编号）。

1. 打开 Bluemix 仪表板，然后单击您创建的 {{site.data.keyword.mobilepushfull}} 服务实例，以打开仪表板。这将显示推送仪表板。要针对 Android 设置未绑定的 {{site.data.keyword.mobilepushshort}} 服务，请选择“未绑定 {{site.data.keyword.mobilepushshort}} 服务”图标，以打开 {{site.data.keyword.mobilepushshort}} 服务仪表板。 

![推送仪表板](images/push_unbound.jpg)

2. 单击**设置 Push** 按钮，以为 Android 应用程序和 Google Chrome Apps and Extensions 配置 FCM/GCM 凭证。
3. 在**配置**页面上，对于 Android，转至**移动**选项卡，然后配置发送方标识（GCM 项目编号）和 API 密钥。对于 Google Chrome Apps and Extensions，转至 **Web** 选项卡，然后适当地配置发送方标识（FCM/GCM 项目编号）和 API 密钥。
4. 单击**保存**。
5. 后续步骤：[针对 Android 启用通知](c_enable_push.html)或[针对 Google Chrome Apps & Extensions 启用通知](c_enable_push.html)。


