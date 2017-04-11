---

copyright:
 years: 2015, 2016

---

# 在 Android 设备上接收推送通知
{: #android_receive}

要向 Push 注册 notificationListener 对象，请调用 **MFPPush.listen()** 方法。此方法通常是通过处理推送通知的活动的 **onResume()** 方法进行调用。

1. 要向 Push 注册 notificationListener 对象，请调用 **listen()** 方法。此方法通常是通过处理推送通知的活动的 **onResume()** 方法进行调用。

	```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
	       push.listen(notificationListener);
	   }
	}
```
2. 构建项目，然后在设备或仿真器上运行该项目。在 register() 方法中针对响应侦听器调用 onSuccess() 方法时，这证实设备已成功向 Push Notification Service 进行注册。此时，可以如“发送基本推送通知”中所述发送消息。
3. 验证设备是否收到通知。如果应用程序在前台运行，那么通知将由 **MFPPushNotificationListener** 进行处理。如果应用程序在后台运行，那么通知栏中会显示一条消息。
