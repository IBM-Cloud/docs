---

copyright:
 años: 2015, 2016

---

# Recepción de notificaciones push en dispositivos Android
{: #android_receive}

Para registrar el objeto notificationListener con Push, invoque el método **MFPPush.listen()**. Este método normalmente se llama desde
                                el método **onResume()** de la actividad que maneja
                            las notificaciones push.

1. Para registrar el objeto notificationListener con Push, invoque el método **listen()**. Este método normalmente se llama desde
                                el método **onResume()** de la actividad que maneja
                            las notificaciones push.

	```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
	       push.listen(notificationListener);
	   }
	}
```
2. Cree el proyecto y ejecútelo en el dispositivo o en el emulador. Cuando se invoque el método onSuccess() para la escucha de respuestas en el método register(), confirmará que el dispositivo se ha registrado correctamente con el Servicio de notificaciones Push. En este momento puede enviar un mensaje tal como se describe en Envío de notificaciones push básicas.
3. Verifique que los dispositivos hayan recibido la notificación. Si la aplicación se encuentra en segundo
          plano, la notificación se manejará mediante el
            **MFPPushNotificationListener**. Si la aplicación se encuentra en segundo plano, se mostrará un
          mensaje en la barra de notificaciones.
