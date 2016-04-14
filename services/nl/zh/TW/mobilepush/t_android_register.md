---

copyright:
 years: 2015, 2016

---

# 登錄 Android 裝置
{: #android_register}

使用 **IMFPush.register()** API，以向 Push Notification Service 登錄裝置。

複製下列程式碼 Snippet，並將其貼入 Android 行動式應用程式。

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
