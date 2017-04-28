---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Activation de webhooks 
{: #tag_based_notifications}
Dernière mise à jour : 1er mars 2017
{: .last-updated}


Avec le service {{site.data.keyword.mobilepushshort}}, vous pouvez opter de recevoir des alertes sur des informations qui ont été modifiées. Les modifications des informations de l'entreprise créent des événements pour lesquels vous pouvez être notifié en les enregistrant en tant qu'événements webhook. Ces événements webhook déclenchent une alerte. 

Les webhooks sont des rappels définis par l'utilisateur qui sont déclenchés par un événement, tels que l'enregistrement d'un appareil ou l'abonnement à des balises. Sur
le service {{site.data.keyword.mobilepushshort}}, vous pouvez vous enregistrer pour les événements webhook suivants : 

- **onDeviceRegister** : un événement webhook est déclenché pour les appareils enregistrés pour opérations push.
- **onDeviceUpdate** : un événement webhook est déclenché quand des informations sur un appareil enregistré sont mises à jour.
- **onDeviceUnregister** : un événement webhook à est déclenché quand l'enregistrement d'un appareil est annulé. 
- **onSubscribe** : un événement webhook à est déclenché quand un utilisateur s'abonne à un intitulé.
- **onUnsubscribe** :un événement webhook à est déclenché quand un utilisateur se désabonne d'un intitulé.
- **onNotificationSend** : un événement webhook est déclenché pour une notification qui a été transmise.
- **onNotificationFailure** : un événement webhook est déclenché pour des échecs de notification.


**Remarque ** : les transmissions de notifications sont effectuées par lots. Une transmission de message peut avoir plusieurs événements webhook, lesquels peuvent inclure à la fois des réussites et des échecs. 
Les événements webhook porteraient le même messageID que le message transmis. 

Pour plus d'informations sur les webhooks, reportez-vous au document [API REST IBM de notifications Push ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://mobile.{DomainName}/imfpush/#/webhooks){: new_window}.

## Réception d'alertes sur les événements webhook
{: #webhook_alert_event}

Les abonnés peuvent choisir de recevoir des alertes sur les événements webhook sous forme de fichiers JSON. La structure d'événement et le contenu exemple sous les suivants :

- Enregistrement d'un appareil
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

- Désenregistrement d'un appareil
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

- Abonnement à une balise
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

- Désabonnement à une balise
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

- Envoi d'une notification
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

- Echec de notification
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

