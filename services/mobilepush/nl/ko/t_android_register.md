---

copyright:
 years: 2015, 2016

---

# Android 디바이스 등록
{: #android_register}

```IMFPush.register()``` API를 사용하여 디바이스를 푸시 알림 서비스에 등록할 수 있습니다. Android 디바이스의 등록인 경우, 우선 Bluemix 푸시 서비스 구성 대시보드에서 GCM(Google Cloud Messaging) 정보를 추가하십시오. 자세한 정보는 [GCM(Google Cloud Messaging)의 신임 정보 구성](t_push_provider_android.html)을 참조하십시오. 

다음 코드 스니펫을 복사하여 Android 모바일 애플리케이션에 붙여넣으십시오. 

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
