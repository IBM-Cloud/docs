---

copyright:
 years: 2015, 2016

---

# Receiving push notifications on Android devices
{: #android_receive}

To register the notificationListener object with Push, call the **MFPPush.listen()** method. This method is typically called from the **onResume()** method of the activity that is handling push notifications.

1. To register the notificationListener object with Push, call the **listen()** method. This method is typically called from the **onResume()** method of the activity that is handling push notifications.

	```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
	       push.listen(notificationListener);
	   }
	}
```
2. Build the project and run it on the device or emulator. When the onSuccess() method for the response listener in the register() method is invoked, it confirms that the device has successfully registered with Push Notification Service. At this time you can send a message as described in Sending basic push notifications.
3. Verify that your devices have received your notification. If the application is in the foreground, the notification is handled by the **MFPPushNotificationListener**. If the application is in the background, a message is displayed in the notification bar.