---

copyright:
 years: 2015, 2016

---

# Recebendo notificações push em dispositivos Android
{: #android_receive}

Para registrar o objeto notificationListener com Push, chame o método
**MFPPush.listen()**. Esse método é chamado geralmente a partir do
método** onResume() **da atividade que está
manipulando as notificações push.

1. Para registrar o objeto notificationListener com Push, chame o método
**listen()**. Esse método é chamado geralmente a partir do
método** onResume() **da atividade que está
manipulando as notificações push.

	```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
	       push.listen(notificationListener);
	   }
	}
```
2. Compile o projeto e execute-o no dispositivo ou simulador. Quando o método
onSuccess() para o listener de resposta no método register() é chamado, ele confirma se o
dispositivo foi registrado com sucesso no Serviço de notificação push. Nesse momento, é
possível enviar uma mensagem conforme descrito em Enviando notificações push básicas.
3. Verifique se seus dispositivos receberam sua notificação. Se o
aplicativo estiver em execução no primeiro plano, a notificação será
manipulada por **MFPPushNotificationListener**. Se o aplicativo estiver em segundo plano, uma mensagem será exibida na barra de notificações.
