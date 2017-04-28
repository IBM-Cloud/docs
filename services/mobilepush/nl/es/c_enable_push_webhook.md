---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Habilitación de webhooks 
{: #tag_based_notifications}
Última actualización: 1 de marzo de 2017
{: .last-updated}


Con el servicio de {{site.data.keyword.mobilepushshort}}, puede elegir recibir alertas sobre información que se ha modificado. Los cambios en la información de la empresa crean sucesos, de los que se le puede notificar registrándolos como sucesos de webhook. Estos sucesos de webhook desencadenan una alerta. 

Los webhooks son devoluciones de llamada definidas por el usuario que desencadena un suceso, como por ejemplo el registro de un dispositivo o la suscripción a etiquetas. En el servicio de {{site.data.keyword.mobilepushshort}}, puede registrarse para los siguientes sucesos de webhook: 

- **onDeviceRegister**: Un suceso de webhook se desencadena para dispositivos registrados para push.
- **onDeviceUpdate**: Un suceso de webhook se desencadena cuando se actualiza la información en un dispositivo registrado.
- **onDeviceUnregister**: Un suceso de webhook se desencadena al eliminar el registro de un dispositivo. 
- **onSubscribe**: Un suceso de webhook se desencadena cuando un usuario se suscribe a una etiqueta.
- **onUnsubscribe**: Un suceso de webhook se desencadena cuando un usuario elimina la suscripción a una etiqueta.
- **onNotificationSend**: Un suceso de webhook se desencadena para una notificación que se ha asignado.
- **onNotificationFailure**: Un suceso de webhook se desencadena para errores de notificación.


**Nota**: Las asignaciones de notificación se realizan por lotes. Una asignación de mensaje puede tener varios sucesos de webhook, que pueden incluir tanto fallos como éxitos. 
Los sucesos de webhook podrían tener el mismo messageID que el del mensaje asignado. 

Para obtener más información sobre webhooks, consulte [API REST de notificaciones Push de IBM ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://mobile.{DomainName}/imfpush/#/webhooks){: new_window}.

## Recepción de alertas sobre sucesos de webhook
{: #webhook_alert_event}

Los suscriptores pueden recibir alertas sobre sucesos de webhook como archivos JSON. La estructura de los sucesos y la carga útil de ejemplo son los siguientes: 

- Registro de un dispositivo
	```
		{ type: 'onDeviceRegister',
		entity:
		{ id: 1,
		deviceId: 'device1',
		applicationId: 'app1',
		userId: 'user1',
		token: 'token1',
		platform: 'G' },
		applicationId: 'app1',
		eventTimeStamp: 1487523766958 }
	```
		{: codeblock}

- Eliminación de un registro del dispositivo
	```
		{ type: 'onDeviceUnregister',
		entity:
		{ id: 1,
		deviceId: 'device1',
		applicationId: 'app1',
		userId: 'user1',
		token: 'token1',
		platform: 'G' },
		applicationId: 'app1',
		eventTimeStamp: 1487523841874 }
	```
		{: codeblock}

- Suscripción a una etiqueta
	```
		{ type: 'onSubscribe',
		entity:
		{ device:
		{ id: 18,
		deviceId: 'device1',
		applicationId: 'app1',
		userId: 'user1',
		token: 'token1',
		platform: 'G' },
		tagName: 'tag1',
		deviceId: 'device1',
		subscriptionId: 'b0246677bfa655385fbc2b5532f6443f' },
		applicationId: 'app1',
		eventTimeStamp: 1487755527470 }
	```
		{: codeblock}

- Cancelación de la suscripción a una etiqueta
	```
		{ type: 'onUnsubscribe',
		entity:
		{ device:
		{ id: 18,
		deviceId: 'device1',
		applicationId: 'app1',
		userId: 'user1',
		token: 'token1',
		platform: 'G' },
		tagName: 'tag1',
		deviceId: 'device1',
		subscriptionId: 'b0246677bfa655385fbc2b5532f6443f' },
		applicationId: 'app1',
		eventTimeStamp: 1487755581059 }
	```
		{: codeblock}

- Envío de una notificación
	```
		{ type: 'onNotificationSent',
		entity:
		{ applicationId: 'app1',
		deviceIds:
		[ 'device1',
		'device2'],
		platform: 'A',
		msgStatus: 'dispatched',
		messageId: '55cb688' },
		applicationId: 'app1',
		eventTimeStamp: 1487524517353 }
	```
		{: codeblock}

- Error de notificación
	```
		{ type: 'onNotificationFailure',
		entity:
		{ applicationId: 'app1',
		deviceIds: [ 'device1' ],
		platform: 'G',
		msgStatus: 'failure',
		failureReason: 'InvalidRegistration',
		messageId: '55cb688' },
		applicationId: 'app1',
		eventTimeStamp: 1487524519453 }
	```
		{: codeblock}

