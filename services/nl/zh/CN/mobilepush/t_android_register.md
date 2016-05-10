---

copyright:
 years: 2015, 2016

---

# 注册 Android 设备
{: #android_register}

使用 ```IMFPush.register()``` API 可向 Push Notification Service 注册设备。对于注册 Android 设备，您首先要在 Bluemix 推送服务配置仪表板中添加 Google 云消息传递 (GCM) 信息。有关更多信息，请参阅[为 Google 云消息传递配置凭证](t_push_provider_android.html)。

将以下代码片段复制并粘贴到 Android 移动应用程序中。

```
	//Register Android devices
	push.register(new MFPPushResponseListener<String>() {
	    @Override
	    public void onSuccess(String deviceId) {
	           //handle success here
	    }
	    @Override
	    public void onFailure(MFPPushException ex) {
	    //handle failure here
	    }
	});
```

```
	//Handles the notification when it arrives
	MFPPushNotificationListener notificationListener = new MFPPushNotificationListener() {
	    @Override
	    public void onReceive (final MFPSimplePushNotification message){
	      // Handle Push Notification
	    }
	};
```
