---

copyright:
 years: 2015, 2016

---

# Enregistrement d'appareils Android
{: #android_register}

Utilisez l'API `IMFPush.register()` pour enregistrer l'appareil auprès d'un service de notifications push. Pour enregistrer des appareils Android, vous devez entrer au préalable des informations GCM (Google Cloud Messaging) dans le tableau de bord de configuration du service Push Bluemix. Pour plus d'informations, voir [Configuration de données d'identification pour Google Cloud Messaging](t_push_provider_android.html).

Copiez et collez les fragments de code suivants dans votre application mobile Android :

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
