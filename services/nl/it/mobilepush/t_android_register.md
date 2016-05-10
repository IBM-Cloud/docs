---

copyright:
 years: 2015, 2016

---

# Registrazione di dispositivi Android
{: #android_register}

Utilizza la API ```IMFPush.register()``` per registrare il dispositivo con un Push Notification Service. Per registrare le periferiche Android, devi prima aggiungere le informazioni di GCM (Google Cloud Messaging) nel dashboard di configurazione del servizio push Bluemix. Per ulteriori informazioni, consulta [Configurazione delle credenziali per GCM (Google Cloud Messaging)](t_push_provider_android.html).

Copia e incolla i seguenti frammenti di codice nella tua applicazione mobile Android.

```
	//Registra dispositivi Android
	push.register(new MFPPushResponseListener<String>() {
	    @Override
	    public void onSuccess(String deviceId) {
	           //gestisce esiti positivi qui
	    }
	    @Override
	    public void onFailure(MFPPushException ex) {
	    //gestisce esiti negativi qui
	    }
	});
```

```
	//Gestisci la notifica quando arriva
	MFPPushNotificationListener notificationListener = new MFPPushNotificationListener() {
	    @Override
	    public void onReceive (final MFPSimplePushNotification message){
	      // Gestisci Push Notification
	    }
	};
```
