---

copyright:
 years: 2015, 2016

---

# Registro de dispositivos Android
{: #android_register}

Utilice la API de `IMFPush.register()` para registrar el dispositivo con un Servicio de notificaciones Push. Para el registro con dispositivos Android, primero debe añadir la información de Google Cloud Messaging (GCM) en el panel de control de configuración del servicio push de Bluemix. Para obtener más información, consulte [Configuración de credenciales para Google Cloud Messaging](t_push_provider_android.html).

Copie y pegue los siguientes fragmentos de código en la aplicación para móviles de Android.

```
	//Register Android devices
	push.register(new MFPPushResponseListener<String>() {
	    @Override
	    public void onSuccess(String deviceId) {
	           //maneje el éxito aquí
	    }
	    @Override
    public void onFailure(MFPPushException ex) {
	    //maneje la anomalía aquí
	    }
	});
```

```
	//Maneja la notificación cuando llega
	MFPPushNotificationListener notificationListener = new MFPPushNotificationListener() {
	    @Override
	    public void onReceive (final MFPSimplePushNotification message){
	      // Manejar la notificación push
	    }
	};
```
