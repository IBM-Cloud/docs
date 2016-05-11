---

copyright:
 years: 2015, 2016

---

# Ricezione di notifiche di push su dispositivi Android
{: #android_receive}

Per registrare l'oggetto  notificationListener con Push, richiama il metodo **MFPPush.listen()**. Questo metodo viene di norma
                            richiamato dal metodo ** onResume() **dell'attività che
                            sta gestendo le notifiche di push.

1. Per registrare l'oggetto  notificationListener con Push, richiama il metodo **listen()**. Questo metodo viene di norma
                            richiamato dal metodo ** onResume() **dell'attività che
                            sta gestendo le notifiche di push.

	```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
	       push.listen(notificationListener);
	   }
	}
```
2. Crea il progetto ed eseguilo sul dispositivo o sull'emulatore. Quando viene richiamato il metodo onSuccess() per il listener di risposte nel metodo register(), ricevi una conferma che il dispositivo ha eseguito correttamente la registrazione presso il Push Notification Service. In questo momento puoi inviare un messaggio come descritto in Invio di notifiche di push di base.
3. Verifica che i tuoi dispositivi abbiano ricevuto la tua notifica. Se l'applicazione è in
            primo piano, la notifica viene gestita da **MFPPushNotificationListener**. Se l'applicazione è in background, viene visualizzato un messaggio nella barra di notifica.
