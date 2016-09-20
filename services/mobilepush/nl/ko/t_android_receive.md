---

copyright:
 years: 2015, 2016

---

# Android 디바이스에서 푸시 알림 수신
{: #android_receive}

notificationListener 오브젝트를 푸시에 등록하려면 **MFPPush.listen()** 메소드를 호출하십시오. 푸시 알림을 처리하는 활동의 **onResume()** 메소드에서 일반적으로 이 메소드가 호출됩니다. 

1. notificationListener 오브젝트를 푸시에 등록하려면 **listen()** 메소드를 호출하십시오. 푸시 알림을 처리하는 활동의 **onResume()** 메소드에서 일반적으로 이 메소드가 호출됩니다. 

	```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
	       push.listen(notificationListener);
	   }
	}
```
2. 프로젝트를 빌드하고 디바이스 또는 에뮬레이터에서 이를 실행하십시오. register() 메소드의 응답 리스너에 대해 onSuccess() 메소드가 호출되면 디바이스가 푸시 알림 서비스에 정상적으로 푸시에 등록된 것입니다. 이 때 기본 푸시 알림 전송에 설명된 대로 메시지를 보낼 수 있습니다. 
3. 디바이스가 알림을 수신했는지 확인하십시오. 애플리케이션이 포그라운드에 있는 경우 **MFPPushNotificationListener**에 의해 알림이 처리됩니다. 애플리케이션이 백그라운드에 있는 경우 알림 막대에 메시지가 표시됩니다. 
