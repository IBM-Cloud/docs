---

copyright:
 years: 2015, 2016

---

# 在 Android 裝置上接收推送通知
{: #android_receive}

若要向 Push 登錄 notificationListener 物件，請呼叫 **MFPPush.listen()** 方法。此方法一般是透過處理推送通知之活動的 **onResume()** 方法所呼叫。

1. 若要向 Push 登錄 notificationListener 物件，請呼叫 **listen()** 方法。此方法一般是透過處理推送通知之活動的 **onResume()** 方法所呼叫。

	```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
	       push.listen(notificationListener);
	   }
	}
```
2. 建置專案，並在裝置或模擬器上執行該專案。在 register() 方法中呼叫回應接聽器的 onSuccess() 方法時，它會確認已順利向 Push Notification Service 登錄裝置。此時，您可以如「傳送基本推送通知」所述傳送訊息。
3. 驗證您的裝置已接收到通知。如果應用程式是在前景中，則 **MFPPushNotificationListener** 會處理通知。如果應用程式是在背景中，則會在通知列中顯示一則訊息。
