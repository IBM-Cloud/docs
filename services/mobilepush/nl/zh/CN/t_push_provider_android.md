
---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# 为 Google 云消息传递 (GCM) 配置凭证
{: #create-push-enable-gcm}
上次更新时间：2016 年 8 月 16 日
{: .last-updated}

获取 Google 云消息传递 (GCM) 凭证，然后在“推送”仪表板上设置 {{site.data.keyword.mobilepushshort}} 服务。

##获取发送方标识和 API 密钥

API 密钥以安全方式存储，并由 {{site.data.keyword.mobilepushshort}} 服务用于连接到 GCM 服务器，而发送方标识（项目编号）由客户机端的 Android SDK 使用。有关发送方标识的更多信息，请参阅 [Google Cloud Messaging](https://developers.google.com/cloud-messaging/gcm#arch)。

1. 从 [Google Dev Console](https://console.developers.google.com/start){: new_window} 获取一个 Google Development 帐户。有关 Google 云消息传递 (GCM) 的更多信息，请参阅 [Creating a Google API Project](https://developers.google.com/console/help/new/){: new_window}。

2. 在 Google Developers Console 中，创建一个新项目。例如，“hello world”。

![创建项目](images/gcm_createproject.jpg)

3. 在 **Project** 名称中，输入项目的名称，然后单击 **Create** 按钮。
4. 单击 **Home**，以查看项目编号。记录您的项目编号。

![GCM 项目编号](images/gcm_projectnumber.jpg)

	**注**：在您创建项目时，会创建项目编号（发送方标识）。在“推送”仪表板屏幕上设置 Push Notifications 服务时会用到此编号。

5. 单击 **APIs & Auth**，然后单击 **Mobile APIs** 部分中的 **Cloud Messaging for Android**。

![API](images/gcm_mobileapi.jpg)

6. 单击 **APIs**，然后单击 **Enable API** 按钮，以为您的项目创建 API 密钥。

![启用 API ](images/gcm_enable_api.jpg)

7. 转至 **APIs & Auths -> Credentials** 屏幕。单击 **Add Credentials**，然后单击 **API Key**。

![API 凭证](images/api_credentials.jpg)

8. 单击 **Server Key** 选项，以生成一个 GCM API 密钥，您在 Bluemix 的“推送”仪表板上会用到该密钥。
9. 在 **Name** 字段中，输入服务器 API 密钥的名称。

![GCM 服务器密钥](images/gcm_serverkey.jpg)

10. 单击 **Create** 按钮。这将显示 API 密钥。

![GCM API 密钥](images/gcm_apikey.jpg)

11. 复制您的 GCM API 密钥，然后单击 **OK** 按钮。在 Bluemix 的“推送通知”仪表板配置屏幕上配置凭证时，您将需要项目编号（发送方标识）和 API 密钥。 


##针对 Android 设置 {{site.data.keyword.mobilepushshort}} 服务

###开始之前
{: before-you-begin}

获取 GCM API 密钥和发送方标识（项目编号）。 

1. 在 Bluemix 仪表板中打开后端应用程序，然后单击 IBM {{site.data.keyword.mobilepushshort}} 服务，以打开仪表板。
 
![推送仪表板](images/bluemixdashboard_push.jpg)

这将显示“推送”仪表板。
	
![推送设置](images/setup_push_main.jpg)
要针对 Android 设置未绑定的 {{site.data.keyword.mobilepushshort}} 服务，请选择“未绑定 {{site.data.keyword.mobilepushshort}} 服务”图标，以打开 {{site.data.keyword.mobilepushshort}} 服务仪表板。
 
	![推送仪表板](images/push_unbound.jpg)

2. 单击**设置 Push** 按钮，以配置 GCM 凭证。
1. 在**配置**选项卡上，转至 **Google 云消息传递**部分，然后配置发送方标识（GCM 项目编号）和 API 密钥。

4. 单击**保存**按钮。 
5. 后续步骤：[为 Android 启用通知](c_enable_push.html)。


##针对 Android 创建未绑定 {{site.data.keyword.mobilepushshort}} 服务

###开始之前
{: before-you-begin}

创建 {{site.data.keyword.mobilepushshort}} 服务实例。您可以在未绑定任何后端应用程序的情况下使用 {{site.data.keyword.mobilepushshort}} 服务实例。

1. 将 {{site.data.keyword.mobilepushshort}} 服务实例绑定到 Bluemix 应用程序。在绑定时，您将能够看到与该服务相关的所有详细信息以 JSON 格式存储在 VCAP_SERVICES 环境变量中。 

![绑定 Push Notification 服务](images/unbound_1.jpg)
 
2. 单击**绑定**并选择要绑定的 {{site.data.keyword.mobilepushshort}} 服务实例。当应用程序绑定到 {{site.data.keyword.mobilepushshort}} 服务时，有关该服务的信息将以 JSON 格式存储在应用程序的 VCAP_SERVICES 环境变量中。例如： 

```
{
   "imfpush_Dev": [
   {
     "name": "neekrish_20JulUnbound",
         "label": "imfpush_Dev",
         "plan": "Basic",
         "credentials": null
      }
   ]
}
```
