---

copyright:
 years: 2015, 2016

---

# Réception de notifications push sur des appareils Android
{: #android_receive}

Pour enregistrer l'objet notificationListener auprès de Push, appelez la méthode **MFPPush.listen()**. En général, elle est appelée depuis la
méthode **onResume()** de l'activité qui traite les notifications push.

1. Pour enregistrer l'objet notificationListener auprès de Push, appelez la méthode **listen()**. En général, elle est appelée depuis la
méthode **onResume()** de l'activité qui traite les notifications push.

	```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
	       push.listen(notificationListener);
	   }
	}
```
2. Générez le projet et exécutez-le sur l'appareil ou l'émulateur. Lorsque la méthode onSuccess() pour le programme d'écoute des réponses dans la méthode register() est appelée, cela signifie que l'appareil a été enregistré auprès de Push. A ce stade, vous pouvez envoyer un message comme décrit dans la rubrique Envoi de notifications push de base.
3. Vérifiez que vos appareils ont reçu votre notification. Si l'application se trouve au premier-plan, la notification est traitée par **MFPPushNotificationListener**. Si elle se trouve en arrière-plan, un message est affiché dans la barre de notification.
