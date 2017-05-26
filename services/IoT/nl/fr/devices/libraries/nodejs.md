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


# Node.js pour les développeurs de terminaux
{: #nodejs}

Vous pouvez adapter les bibliothèques et exemples client dans Node.js afin de générer et développer un code de terminal qui interagit avec votre organisation sur {{site.data.keyword.iot_full}}.
{:shortdesc}

Utilisez les informations et les exemples fournis pour commencer à développer vos terminaux à l'aide de Node.js.

## Téléchargement du client et des ressources Node.js
{: #node.js_client_downloads}

Pour accéder aux bibliothèques client Node.js pour {{site.data.keyword.iot_short_notm}} et aux autres ressources disponibles, accédez au référentiel [iot-nodejs ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-nodejs){: new_window} dans GitHub et exécutez les instructions d'installation.


Pour plus d'informations, voir les ressources suivantes :

- [Exemples de terminaux ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples){: new_window} dans Github
- Le référentiel [ibmiotf ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://www.npmjs.com/package/ibmiotf){: new_window} sur NPM

## Constructeur
{: #constructor}

Le constructeur crée l'instance du client de terminal. Il accepte un JSON de configuration qui contient les définitions suivantes :

|Définition |Description |
|:---|:---|
|`org` |ID de votre organisation.|
|`type`  |Type de votre terminal. Généralement, deviceType regroupe des terminaux qui effectuent une tâche spécifique, par exemple, "weatherballoon".|
|`id`  |ID de votre terminal. Généralement, pour un type de terminal donné, deviceId est un identificateur unique, par exemple, un numéro de série ou une adresse MAC.|
|`auth-method`   |Méthode d'authentification à utiliser. La seule valeur actuellement prise en charge est `token`.|
|`auth-token`   |Jeton d'authentification permettant d'établir une connexion sécurisée entre votre terminal et Watson IoT Platform. Cette zone est obligatoire si `auth-method` a pour valeur `token`.|

**Remarque :** Si vous souhaitez utiliser le service Quickstart, vous ne devez soumettre que les trois premières propriétés.

```
    var iotf = require("ibmiotf");
    var config = {
		"org" : "organization",
		"id" : "deviceId",
		"type" : "deviceType",
		"auth-method" : "token",
		"auth-token" : "authToken"
    };


    var deviceClient = new iotf.IotfDevice(config);
```

### Utilisation d'un fichier de configuration

Au lieu de transmettre directement la configuration, vous pouvez utiliser un fichier de configuration JSON pour fournir les propriétés de configuration requises, comme illustré dans l'exemple suivant :


```  
    var iotf = require("ibmiotf");
    var config = require("./device.json");
    var deviceClient = new iotf.IotfDevice(config);  
```
Le fichier de configuration `device.json` doit être au format suivant :

```
	{
	  "org": "xxxxx",
	  "type": "raspi",
	  "id": "pi1",
	  "auth-method" : "token",
	  "auth-token" : "xxxxxxxxxxxxxxxx"
	}

```  

## Connexion à {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

Vous pouvez vous connecter à {{site.data.keyword.iot_short_notm}} en appelant la fonction `connect`.

```
	var iotf = require("ibmiotf");
	var config = require("./device.json");

	var deviceClient = new iotf.IotfDevice(config);

	//setting the log level to debug. By default its 'warn'
	deviceClient.log.setLevel('debug');

	deviceClient.connect();

	deviceClient.on('connect', function(){
		var i=0;
		console.log("connected");
		setInterval(function function_name () {
			i++;
			deviceClient.publish('myevt', 'json', '{"value":'+i+'}', 2);
		},2000);
	});

```

Une fois la connexion au service {{site.data.keyword.iot_short_notm}} établie, le client du terminal envoie un événement `connect`. Ce processus signifie que l'intégralité de la logique de terminal peut être implémentée au sein de cette fonction de rappel.

Le client de terminal tente automatiquement de se reconnecter lorsque la connexion s'interrompt. Lorsque la reconnexion aboutit, le client envoie un événement `reconnect`.

## Journalisation
{: #logging}

Par défaut, seuls les événements de journal de type *warn* sont enregistrés. Si vous souhaitez augmenter ou réduire le niveau de journalisation, utilisez la fonction log.setLevel. Les niveaux de journalisation suivants sont pris en charge :
- trace
- debug
- info
- warn
- error

```
	var iotf = require("ibmiotf");
	var config = require("./device.json");

	var deviceClient = new iotf.IotfDevice(config);

	//setting the log level to debug. By default its 'warn'
	deviceClient.log.setLevel('debug');

```


## Publication d'événements
{: #publishing_events}

Les événements constituent le mécanisme par lequel les terminaux publient des données sur {{site.data.keyword.iot_short_notm}}. Le terminal contrôle le contenu de l'événement et affecte un nom à chaque événement qu'il envoie.

Lorsqu'un événement est reçu par l'instance {{site.data.keyword.iot_short_notm}}, les données d'identification de l'événement reçu identifient le terminal qui a envoyé l'événement, ce qui signifie qu'un terminal ne peut pas simuler les droits d'accès d'un autre terminal.

Vous pouvez augmenter le niveau de qualité de service (QoS) des événements qui sont publiés. La publication des événements dont le niveau QoS est supérieur à `0` peut prendre plus de temps, en raison des informations de réception de confirmation supplémentaires qui sont incluses.

**Remarque :** Le mode flux Quickstart ne prend en charge que le niveau QoS `0`.


Les événements peuvent être publiés à l'aide des propriétés suivantes :

|Propriété |Description|
|:---|:---|
|`eventType`  | Type d'événement à publier, par exemple, status ou GPS. |  
|`eventFormat`  |Format de l'événement, par exemple, JSON. |
|`data`  | Contenu de l'événement, qui doit correspondre à une chaîne de mémoire tampon. |
|`QoS`  | Qualité de service MQTT de l'événement publié. Les valeurs prises en charge sont 0, 1 et 2.|


```
    var deviceClient = new Client.IotfDevice(config);

    deviceClient.connect();

    deviceClient.on("connect", function () {
       //publish an event at the default quality of service
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

       //publish an event at the user-defined quality of service
       var myQosLevel=2
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}', myQosLevel);
  });

```

## Traitement des commandes
{: #handling_commands}

Lorsque le client du terminal se connecte, il s'abonne automatiquement aux commandes de ce terminal. Pour traiter des commandes spécifiques, vous devez enregistrer une fonction de rappel de commande. Le client de terminal appelle la fonction de rappel de commande lorsqu'il reçoit une commande. La fonction de rappel possède les propriétés suivantes :

|Propriété |Description|
|:---|:---|
|`commandName`  | Chaîne qui indique le nom de la commande appelée. |  
|`format`  | Chaîne qui indique le format de l'événement, par exemple, JSON. |
|`payload`  | Chaîne qui indique les données du contenu de la commande.  |
|`topic`  | Lors de la publication en tant que terminal, la chaîne topic n'inclut pas le type de terminal ni l'ID de terminal ; ces informations sont extraites de l'ID de client.  Par exemple, `iot-2/evt/event_id/fmt/format_string`.  Lors de la publication en tant qu'application ou passerelle pour le compte d'un terminal, l'élément topic doit inclure le type de terminal et l'ID de terminal.  Par exemple `iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string`.|


```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	deviceClient.on("connect", function () {
		//publish an event at the default quality of service
		deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

	});

	deviceClient.on("command", function (commandName,format,payload,topic) {
		if(commandName === "blink") {
			console.log(blink);
			//function to be performed for this command
			blink(payload);
		} else {
			console.log("Command not supported.. " + commandName);
		}
	});

```

## Traitement des erreurs
{: #handling_errors}

Lorsque le client de terminal rencontre une erreur, il envoie un événement *error*.

```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	deviceClient.on("connect", function () {
		//publish an event at the default quality of service
		deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

	});

	deviceClient.on("error", function (err) {
		console.log("Error : "+err);
	});
	....

```

## Déconnexion du client
{: #disconnecting_client}

L'exemple suivant vous montre comment déconnecter le client et libérer la connexion :

```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	client.on("connect", function () {
		//publish an event at the default quality of service
		client.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

		//publishing event at the user-defined quality of service
		var myQosLevel=2
		client.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}', myQosLevel);

		//disconnect the client
		client.disconnect();
	});

	....
```
