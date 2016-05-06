---

copyright:
 years: 2015, 2016

---

# Android デバイスの登録
{: #android_register}

**IMFPush.register()** API を使用して、Push Notification Service にデバイスを登録します。

以下のコード・スニペットを Android モバイル・アプリケーションにコピーして貼り付けます。


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
