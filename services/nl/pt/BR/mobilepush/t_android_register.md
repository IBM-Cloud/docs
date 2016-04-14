---

copyright:
 years: 2015, 2016

---

# Registrando dispositivos Android
{: #android_register}

Use a API **IMFPush.register()** para registrar o dispositivo em
um Serviço de notificação push.

Copie e cole os seguintes fragmentos de códigos em seu
aplicativo móvel Android.

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
