---

copyright:
 años: 2015, 2016

---

# Registro de dispositivos Android
{: #android_register}

Utilice la API de **IMFPush.register()** para registrar el dispositivo con un Servicio de notificaciones Push.

Copie y pegue los siguientes fragmentos de código en la aplicación para móviles de
                    Android.

```
	//Register Android devices
	push.register(new MFPPushResponseListener<String>() {
	    @Override
	    public void onSuccess(String deviceId) {
	           //handle success here
	    }
	    @Override
	    public void onFailure(MFPPushException ex) {
	    //maneje la anomalía aquí
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
