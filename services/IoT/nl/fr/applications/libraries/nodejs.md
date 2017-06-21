---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# Node.js pour les développeurs d'applications
{: #nodejs}

Dernière mise à jour : 29 juillet 2016
{: .last-updated}

Vous pouvez adapter les bibliothèques et exemples client dans Node.js afin de générer et personnaliser des applications qui interagissent avec votre organisation sur {{site.data.keyword.iot_full}}.
{:shortdesc}

Utilisez les informations et les exemples fournis pour commencer à développer vos applications en utilisant Node.js.

## Téléchargement du client et des ressources Node.js
{: #nodejs_client_download}

Pour accéder aux bibliothèques client Node.js pour {{site.data.keyword.iot_short_notm}} et aux autres ressources disponibles, accédez au référentiel [iot-nodejs ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-nodejs){: new_window} dans GitHub et exécutez les instructions d'installation.


Pour plus d'informations, voir les ressources suivantes :
- [Exemples d'application ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples){: new_window} dans GitHub.
- [ibmiotf ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://www.npmjs.com/package/ibmiotf){: new_window} dans NPM.
- Section [Référence](#reference_nodejs) du présent document.


## Constructeur
{: #constructor}

Le constructeur génère l'instance client d'application et accepte un fichier de configuration JSON contenant les propriétés suivantes :

| Propriété     |Description     |
|----------------|----------------|
|`org` |ID de votre organisation. Cette valeur est obligatoire.|
|`id`  |ID unique de votre application au sein de votre organisation.|
|`auth-key`   |Clé d'API permettant d'établir une connexion sécurisée entre votre application et Watson IoT Platform.|
|`auth-token`   |Jeton de clé d'API permettant d'établir une connexion sécurisée entre votre terminal et Watson IoT Platform.|
|`type`  |Type d'abonnement. Spécifiez `shared` pour activer l'abonnement partagé.|


L'utilisation de Quickstart ne requiert que les deux premières propriétés.

```
  var Client = require("ibmiotf");
	var appClientConfig = {
		"org" : orgId,
		"id" : appId,
		"auth-key" : apiKey,
		"auth-token" : apiToken
	}

	var appClient = new Client.IotfApplication(appClientConfig);
```


### Utilisation d'un fichier de configuration


Au lieu de transmettre les propriétés JSON directement, vous pouvez également utiliser un fichier de configuration présenté dans l'exemple de code suivant :

```

  var Client = require("ibmiotf");
	var appClientConfig = require("./application.json");
	var appClient = new Client.IotfApplication(appClientConfig);
```

Assurez-vous que le fichier de configuration JSON est au format suivant :

```
    {
	  "org": 'xxxxx',
	  "id": 'myapp',
	  "auth-key": 'a-xxxxxxx-zenkqyfiea',
	  "auth-token": 'xxxxxxxxxx'
    }
```


## Connexion à {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

Pour vous connecter à {{site.data.keyword.iot_short_notm}}, soumettez une demande *connect*, comme suit :

```
  var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

	//Add your code here
	});
```

Après avoir établi une connexion au service {{site.data.keyword.iot_short_notm}}, le client d'application envoie un événement `connect`, par conséquent, n'importe quelle logique peut être implémentée au sein de cette fonction de rappel.



Le client d'application tente automatiquement de se reconnecter lorsque sa connexion est interrompue. Lorsque la reconnexion aboutit, le client envoie un événement `reconnect`.



## Journalisation
{: #logging}

Par défaut, seuls les événements de journal de type `warn` sont enregistrés. Si vous souhaitez augmenter ou réduire le niveau de journalisation, utilisez la fonction `log.setLevel`. Les niveaux de journalisation suivants sont pris en charge :
- trace
- debug
- info
- warn
- error

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//setting the log level to 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Add your code here
	});
```

## Abonnements partagés
{: #shared_subscriptions}

Utilisez la fonction d'abonnement partagé pour générer des applications évolutives qui équilibrent la charge des messages sur plusieurs instances de l'application. Pour activer l'équilibrage de charge, affectez à la zone `type` la valeur `shared`, comme illustré dans l'exemple suivant :

```

	var appClientConfig = {
	  org: 'xxxxx',
	  id: 'myapp',
	  "auth-key": 'a-xxxxxx-xxxxxxxxx',
	  "auth-token": 'xxxxx!xxxxxxxx',
	  "type" : "shared" // make this connection as shared subscription
	};
	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//setting the log level to 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Add your code here
	});
```

## Traitement des erreurs
{: #handling_errors}

Lorsque le client d'application rencontre une erreur, un événement `error` est généré.

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//setting the log level to 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Add your code here
	});
	appClient.on("error", function (err) {
		console.log("Error : "+err);
	});
```

## Abonnement aux événements d'un terminal
{: #subscribing_device_events}

Les événements constituent le mécanisme par lequel les terminaux publient des données sur  l'instance {{site.data.keyword.iot_short_notm}}. Le terminal contrôle le contenu de l'événement et affecte un nom à chaque événement qu'il envoie.

Lorsqu'un événement est reçu par l'instance {{site.data.keyword.iot_short_notm}}, les données d'identification de l'événement reçu identifient le terminal qui a envoyé l'événement, ce qui signifie qu'un terminal ne peut pas simuler les droits d'accès d'un autre terminal.


Par défaut, les applications s'abonnent à tous les événements depuis tous les terminaux connectés. Utilisez les paramètres de type de terminal, d'ID de terminal, d'événement et de format de message pour contrôler la portée de l'abonnement. Les exemples de code suivants vous montrent comment utiliser ces paramètres afin de définir la portée d'un abonnement :

### Abonnement à tous les événements depuis tous les terminaux


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents();
	});
```

### Abonnement à tous les événements depuis tous les terminaux d'un type donné

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("mydeviceType");
	});
```

### Abonnement à un événement spécifique depuis tous les terminaux


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("+","+","myevent");
	});
```

### Abonnement à un événement spécifique depuis au moins deux terminaux différents

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","myevent");
		appClient.subscribeToDeviceEvents("myOtherDeviceType","device02","myevent");
	});
```

### Abonnement à tous les événements publiés au format JSON


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","+","json");

	});
```

**Remarque** : Un client unique peut prendre en charge plusieurs abonnements.

### Traitement des événements provenant des terminaux


Pour traiter les événements reçus par vos abonnements, implémentez une méthode de rappel d'événement de terminal. Le client d'application {{site.data.keyword.iot_short_notm}} envoie l'événement `deviceEvent`. Cette fonction possède les propriétés suivantes :

- deviceType
- deviceId
- eventType
- format
- payload
- topic

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","+","json");

	});
	appClient.on("deviceEvent", function (deviceType, deviceId, eventType, format, payload) {

		console.log("Device Event from :: "+deviceType+" : "+deviceId+" of event "+eventType+" with payload : "+payload);

	});
```


## Abonnement au statut des terminaux
{: #subscribing_device_status}

Par défaut, lorsque vous vous abonnez au statut de terminal, des mises à jour de statut sont reçues pour tous les terminaux connectés. Utilisez les paramètres de type et d'ID pour contrôler la portée de l'abonnement. Un client unique peut prendre en charge plusieurs abonnements.

### Abonnement aux mises à jour de statut pour tous les terminaux

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus();

	});
```

### Abonnement aux mises à jour de statut pour tous les terminaux d'un type donné


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType");

	});
```

### Abonnement aux mises à jour de statut pour deux terminaux différents

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType","device01");
		appClient.subscribeToDeviceStatus("myOtherDeviceType","device02");

	});
```

### Traitement des mises à jour du statut des terminaux

Pour traiter les mises à jour de statut reçues par vos abonnements, implémentez une méthode de rappel d'événement de terminal. Le client d'application {{site.data.keyword.iot_short_notm}} envoie l'événement `deviceStatus`. Cette fonction possède les propriétés suivantes :

-   deviceType
-   deviceId
-   payload
-   topic

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType","device01");
		appClient.subscribeToDeviceStatus("myOtherDeviceType","device02");

	});
	appClient.on("deviceStatus", function (deviceType, deviceId, payload, topic) {

		console.log("Device status from :: "+deviceType+" : "+deviceId+" with payload : "+payload);

	});
```


## Publication des événements à partir de terminaux
{: #publishing_device_events}


Les applications peuvent publier des événements comme s'ils provenaient d'un terminal. La fonction nécessite les propriétés suivantes :

-   deviceType
-   deviceId
-   eventType
-   format
-   data


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50};
		myData = JSON.stringify(myData);
		appClient.publishDeviceEvent("myDeviceType","device01", "myEvent", "json", myData);

	});
```


## Publication de commandes sur des terminaux
{: #publishing_commands_devices}

Les applications peuvent publier des commandes sur des terminaux connectés. La fonction nécessite les propriétés suivantes :

-   deviceType
-   deviceId
-   eventType
-   format
-   data

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'DelaySeconds' : 10};
		myData = JSON.stringify(myData);
		appClient.publishDeviceCommand("myDeviceType","device01", "reboot", "json", myData);

	});
```


## Déconnexion du client
{: #disconnect_client}

L'exemple suivant déconnecte le client et libère également les connexions :

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'DelaySeconds' : 10}
		appClient.publishDeviceCommand("myDeviceType","device01", "reboot", "json", myData);

		appClient.disconnect();
	});
```


## Référence
{: #reference_nodejs}

Le tableau suivant décrit les paramètres utilisés dans les fonctions abordées dans la présente documentation Node.js :

|Paramètre|Type de données|Description|
|:---|:---|
|`deviceType`|Chaîne|Type de terminal. Généralement, deviceType regroupe des terminaux qui effectuent une tâche spécifique, par exemple, "weatherballoon".|
|`deviceId`|Chaîne|ID du terminal. Généralement, pour un type de terminal donné, deviceId est un identificateur unique, par exemple, un numéro de série ou une adresse MAC.|
|`eventType`|Chaîne|Groupe d'événements spécifiques, par exemple, "status", "warning" et "data".|
|`format`|Chaîne|Le format peut être n'importe quelle chaîne, par exemple, JSON.  |
|`data`|Dictionnaire|Données du contenu du message. La longueur maximale est de 131072 octets.|
|`payload`|Chaîne|Données du contenu du message. La longueur maximale est de 131072 octets.|
|`topic`|Chaîne|Lors de la publication en tant que terminal, la chaîne topic n'inclut pas le type de terminal ni l'ID de terminal ; ces informations sont extraites de l'ID de client.  Par exemple, `iot-2/evt/event_id/fmt/format_string`.  Lors de la publication en tant qu'application ou passerelle pour le compte d'un terminal, l'élément topic doit inclure le type de terminal et l'ID de terminal.  Par exemple `iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string`.|
