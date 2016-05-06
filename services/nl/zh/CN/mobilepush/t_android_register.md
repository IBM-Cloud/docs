---

copyright:
 years: 2015, 2016

---

# 注册 Android 设备
{: #android_register}

使用 **IMFPush.register()** API 可向 Push Notification Service 注册设备。

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
