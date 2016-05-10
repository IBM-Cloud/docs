---

copyright:
 years: 2015, 2016

---

# Registrando dispositivos Android
{: #android_register}

Use a API ```IMFPush.register()``` para registrar o dispositivo com um Serviço de notificação push. Para o registro de dispositivos Android, primeiro
inclua as informações do Google Cloud Messaging (GCM) no painel de configuração de serviço de push do Bluemix. Para obter mais informações,
consulte [Configurando credenciais para o Google Cloud Messaging](t_push_provider_android.html).

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
