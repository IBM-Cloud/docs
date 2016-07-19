---

copyright:
 years: 2015, 2016

---

# Registering Android devices
{: #android_register}

Use the ```IMFPush.register()``` API to register the device with a Push Notification Service. For registering for Android devices, you first add the Google Cloud Messaging (GCM) information in the Bluemix push service configuration dashboard. For more information, see [Configuring credentials for Google Cloud Messaging](t_push_provider_android.html).

Copy and paste the following code snippets into your Android mobile application.

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
