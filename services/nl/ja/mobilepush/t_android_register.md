---

copyright:
 years: 2015, 2016

---

# Android デバイスの登録
{: #android_register}

```IMFPush.register()``` API を使用して、Push Notification Service にデバイスを登録します。Android デバイスを登録する場合、まず、Google Cloud Messaging (GCM) 情報を Bluemix プッシュ・サービス構成ダッシュボードに追加します。詳しくは、[Google Cloud Messaging の資格情報の構成](t_push_provider_android.html)を参照してください。

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
