---

copyright:
 years: 2015, 2016

---

# Android 디바이스 등록
{: #android_register}

**IMFPush.register()** API를 사용하여 푸시 알림 서비스에 디바이스를 등록합니다. 

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
