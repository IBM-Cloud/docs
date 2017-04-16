---

copyright:
 years: 2015, 2016

---

# Android-Geräte registrieren
{: #android_register}

Verwenden Sie die API `IMFPush.register()`, um das Gerät beim Service 'Push Notifications' zu registrieren. Für die Registrierung bei Android-Geräten müssen Sie zunächst die GCM-Angaben (Google Cloud Messaging) im Bluemix-Dashboard für die Konfiguration des Push-Service hinzufügen. Weitere Informationen finden Sie im Abschnitt zur [Konfiguration von Berechtigungsnachweisen für Google Cloud Messaging](t_push_provider_android.html).

Kopieren Sie die folgenden Code-Snippets und fügen Sie sie in Ihre mobile Android-Anwendung ein.

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
