---

copyright :
  années : 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java pour les développeurs d'applications
{: #java}

Dernière mise à jour : 7 septembre 2016
{: .last-updated}

Vous pouvez utiliser Java pour générer et personnaliser des applications qui interagissent avec votre organisation sur {{site.data.keyword.iot_full}}. Utilisez les informations et les exemples fournis pour commencer à développer vos applications en utilisant Java. {:shortdesc}

## Téléchargement du client et des ressources Java
{: #java_client_download}

Pour accéder aux bibliothèques et exemples client Java pour {{site.data.keyword.iot_short_notm}}, accédez au référentiel [iot-java](https://github.com/ibm-watson-iot/iot-java) dans GitHub et exécutez les instructions d'installation. 


## Constructeur
{: #constructor}

Le constructeur génère l'instance client et accepte un objet `Propriétés` contenant les définitions suivantes : 

| Définition     |Description     |
|----------------|----------------|
|`org` |ID de votre organisation. Cette valeur est obligatoire. Si vous utilisez un flux Quickstart, spécifiez `quickstart`.|
|`id` |ID unique de l'application au sein de votre organisation.|
|`auth-method`  |Méthode d'authentification, pour laquelle la seule valeur actuellement prise en charge est `apikey`.|
|`auth-key`   |Clé d'API facultative, requise lorsque le paramètre auth-method a pour valeur `apikey`.  |
|`auth-token`   |Jeton de clé d'API, requis lorsque le paramètre auth-method a pour valeur `apikey`. |
|`clean-session`|Valeur true ou false requise uniquement si vous souhaitez connecter l'application en mode d'abonnement durable. Par défaut, `clean-session` prend la valeur `true`.|
|`shared-subscription`|Valeur booléenne. Affectez la valeur `true` si vous souhaitez générer des applications évolutives qui équilibrent la charge des messages sur plusieurs instances de l'application. Pour plus d'informations, voir [Applications évolutives](mqtt.html#/scalable-applications#scalable-applications).

L'objet `Propriétés` crée des définitions qui sont utilisées pour interagir avec le module {{site.data.keyword.iot_short_notm}}. Si vous ne spécifiez pas les propriétés de cet objet, ou si vous indiquez `quickstart`, le client se connecte au service  Quickstart de {{site.data.keyword.iot_short_notm}} en tant que terminal non enregistré. 

L'exemple de code suivant vous montre comment construire l'instance ApplicationClient en mode `quickstart` :

```
    import com.ibm.iotf.client.app.ApplicationClient;
    import java.util.Properties;

    Properties options = new Properties();
    options.put("org", "quickstart");

    ApplicationClient myClient = new ApplicationClient(options);
```

L'exemple de code suivant vous montre comment construire l'instance ApplicationClient en mode flux enregistré : 

```
    Properties options = new Properties();
    options.put("org", "uguhsp");
    options.put("id", "app" + (Math.random() * 10000));
    options.put("Authentication-Method","apikey");
    options.put("API-Key", "<API-Key>");
    options.put("Authentication-Token", "<Authentication-Token>");

    ApplicationClient myClient = new ApplicationClient(options);
```

### Utilisation d'un fichier de configuration

Au lieu d'inclure directement un objet `Propriétés`, vous pouvez utiliser un fichier de configuration qui contient les paires nom-valeur pour l'objet `Propriétés` dans le format suivant : 

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    ...
```
Le fichier de configuration de l'application doit posséder le format suivant :

```
    [application]
    org=$orgId
    id=$myApplication
    auth-method=apikey
    auth-key=$key
    auth-token=$token
    enable-shared-subscription=true|false
```

## Connexion à {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

Pour établir la connexion à {{site.data.keyword.iot_short_notm}}, utilisez la fonction `connect()`. La fonction `connect()` inclut un paramètre booléen facultatif appelé `autoRetry` qui détermine si la bibliothèque tente de se reconnecter si un échec de connexion MqttException se produit. Par défaut, `autoRetry` a pour valeur true. Si une connexion MqttSecurityException échoue en raison de détails d'enregistrement de terminal incorrects, la bibliothèque ne tente pas de se reconnecter, même si `autoRetry` a pour valeur `true`.

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);

    myClient.connect();
```

Une fois la connexion au service {{site.data.keyword.iot_short_notm}} établie, vos clients d'application peuvent s'abonner à des événements de terminal, s'abonner à des statuts de terminal et publier des événements et des commandes de terminal. 

## Abonnement aux événements d'un terminal
{: #subscribing_device_events}

Les événements constituent le mécanisme par lequel les terminaux publient des données sur {{site.data.keyword.iot_short_notm}}. Le terminal contrôle le contenu de l'événement et affecte un nom à chaque événement qu'il envoie. 

Lorsqu'un événement est reçu par l'instance {{site.data.keyword.iot_short_notm}}, les données d'identification de l'événement reçu identifient le terminal qui a envoyé l'événement, ce qui signifie qu'un terminal ne peut pas simuler les droits d'accès d'un autre terminal. 


Par défaut, les applications s'abonnent à tous les événements depuis tous les terminaux connectés. Utilisez les paramètres de type de terminal, d'ID de terminal, d'événement et de format de message pour contrôler la portée de l'abonnement. Les exemples de code suivants vous montrent comment utiliser ces paramètres afin de définir la portée d'un abonnement :

### Abonnement à tous les événements depuis tous les terminaux


```
    myClient.connect();
    myClient.subscribeToDeviceEvents();
```
### Abonnement à tous les événements depuis tous les terminaux d'un type donné


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino");
```

### Abonnement à tous les événements depuis un terminal donné


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee");
```
### Abonnement à un événement spécifique depuis au moins deux terminaux différents

```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee", "myEvent");
    myClient.subscribeToDeviceEvents("iotsample-arduino", "10aabbccddee", "myEvent");
```
### Abonnement aux événements publiés au format JSON


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee", "myEvent", "json", 0);
```

**Remarque** : Un client unique peut prendre en charge plusieurs abonnements. 

## Traitement des événements provenant des terminaux
{: #handling_device_events}

Pour traiter les événements reçus par vos abonnements, enregistrez une méthode de rappel d'événement. Les messages sont renvoyés en tant qu'instance de la classe Event qui possède les propriétés suivantes : 

|Paramètre|Type de données|Description|
|:---|:---|
|`event.device`|Chaîne|Identifie le terminal de manière unique parmi tous les types de terminal dans l'organisation. |
|`event.deviceType`|Chaîne|Identifie le type de terminal. Généralement, deviceType regroupe des terminaux qui effectuent une tâche spécifique, par exemple, "weatherballoon".|
|`event.deviceId`|Chaîne|Représente l'ID du terminal. Généralement, pour un type de terminal donné, deviceId est un identificateur unique, par exemple, un numéro de série ou une adresse MAC. |
|`event.event`|Chaîne|Utilisé généralement pour regrouper des événements spécifiques, par exemple, "status", "warning" et "data".|
|`event.format`|Chaîne|Le format peut être n'importe quelle chaîne, par exemple, JSON.  |
|`event.data`|Dictionnaire|Données du contenu du message. La longueur maximale est de 131072 octets.|
|`event.timestamp`|Date et heure|Date et heure de l'événement. |


Le code suivant illustre un exemple d'implémentation du rappel d'événement :

```
  import com.ibm.iotf.client.app.Event;
  import com.ibm.iotf.client.app.EventCallback;
  import com.ibm.iotf.client.app.Command;

  import java.util.concurrent.BlockingQueue;
  import java.util.concurrent.LinkedBlockingQueue;

  /**
    * A sample Event callback class that processes the device events in a separate thread.
    *
    */
   class MyEventCallback implements EventCallback, Runnable {

	// A queue to hold and process the Events for smooth handling of MQTT messages
	private BlockingQueue<Event> evtQueue = new LinkedBlockingQueue<Event>();

	public void processEvent(Event e) {
		try {
			evtQueue.put(e);
		} catch (InterruptedException e1) {
			e1.printStackTrace();
		}
	}

	@Override
	public void processCommand(Command cmd) {
		System.out.println("Command received:: " + cmd);
	}

	@Override
	public void run() {
		while(true) {
			Event e = null;
			try {
				e = evtQueue.take();
				// In this example, the only output is the event
				System.out.println("Event:: " + e.getDeviceId() + ":" + e.getEvent() + ":" + e.getPayload());
			} catch (InterruptedException e1) {
				// Ignore the Interuppted exception, retry
				continue;
			}
		}
	}
    }
```

Lorsque le rappel d'événement est ajouté à ApplicationClient, la méthode `processEvent()` est appelée chaque fois qu'un événement correspondant à l'abonnement est publié. Le fragment suivant montre comment ajouter le rappel d'événement dans une instance ApplicationClient :



```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToDeviceEvents();
```

Comme pour l'abonnement à des événements de terminaux, l'application peut s'abonner à des commandes envoyées aux terminaux. L'exemple de code suivant montre comment vous abonner à toutes les commandes pour tous les terminaux de l'organisation :

```

    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToDeviceCommands();
```

Des méthodes surchargées sont disponibles pour contrôler l'abonnement aux commandes. La méthode `processCommand()` est appelée lorsqu'une commande correspondant à l'abonnement à la commande est envoyée au terminal. 


## Abonnement au statut des terminaux
{: #subscribing_device_status}

De la même manière qu'elles s'abonnent aux événements des terminaux, les applications peuvent s'abonner aux statuts des terminaux, par exemple, connecter et déconnecter un terminal avec {{site.data.keyword.iot_short_notm}}. Par défaut, cet abonnement porte sur toutes les mises à jour de statut pour tous les terminaux connectés. Utilisez les paramètres de type et d'ID de terminal pour contrôler la portée de l'abonnement. Les exemples de code suivants vous montrent comment utiliser ces paramètres afin de définir la portée d'un abonnement :

### Abonnement aux mises à jour du statut de tous les terminaux

```
    myClient.connect();
    myClient.subscribeToDeviceStatus();
```

### Abonnement aux mises à jour du statut de tous les terminaux d'un type donné


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-arduino");
```

### Abonnement aux mises à jour du statut de deux terminaux différents


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-arduino", "00aabbccddee");
    myClient.subscribeToDeviceStatus("iotsample-arduino", "10aabbccddee");
```

**Remarque** : Un client unique peut prendre en charge plusieurs abonnements. 

## Traitement des mises à jour du statut des terminaux
{: #handling_device_status_updates}

Pour traiter les mises à jour de statut reçues par vos abonnements, vous devez enregistrer une méthode de rappel d'événement d'événement de statut. Pour les événements de statut `Connect` et `Disconnect`, les messages sont renvoyés en tant qu'instance de la classe Status qui possède les propriétés suivantes : 


| Paramètre     |Type de données     |
|----------------|----------------|
|`status.clientAddr` |Chaîne|
|`status.protocol`  |Chaîne|
|`status.clientId`   |Chaîne|
|`status.user`   |Chaîne|
|`status.time`   |java.util.Date|
|`status.action` |Chaîne|
|`status.connectTime`   |java.util.Date|
|`status.port`|Entier|

Les propriétés suivantes ne sont définies que lorsque l'événement de statut est `Disconnect` :

| Propriété     |Type de données     |
|----------------|----------------|
|`status.writeMsg` |Entier|
|`status.readMsg`  |Entier|
|`status.reason`   |Chaîne|
|`status.readBytes`   |Entier|
|`status.writeBytes`   |Entier|


L'exemple de code suivant fournit un exemple d'implémentation du rappel de statut :

```

  private static class MyStatusCallback implements StatusCallback {

      public void processApplicationStatus(ApplicationStatus status) {
          System.out.println("Application Status = " + status.getPayload());
      }

      public void processDeviceStatus(DeviceStatus status) {
          if(status.getAction() == "Disconnect") {
              System.out.println("device: "+status.getDeviceId()
                                  + "  time: "+ status.getTime()
                                  + "  action: " + status.getAction()
                                  + "  reason: " + status.getReason());
          } else {
              System.out.println("device: "+status.getDeviceId()
                                  + "  time: "+ status.getTime()
                                  + "  action: " + status.getAction());
          }
      }
  }
```

Lorsque le rappel de statut est ajouté à ApplicationClient, la méthode `processDeviceStatus()` est appelée chaque fois qu'un terminal correspondant aux critères est connecté ou déconnecté avec {{site.data.keyword.iot_short_notm}}. L'exemple de code suivant vous montre comment ajouter l'instance de rappel de statut à ApplicationClient : 
```

    myClient.connect()
    myClient.setStatusCallback(new MyStatusCallback());
    myClient.subscribeToDeviceStatus();
```
Les applications peuvent s'abonner à n'importe quel statut d'application, par exemple, les statuts de connexion et de déconnexion avec Watson IoT Platform. L'exemple de fragment de code  suivant montre comment vous abonner au statut d'application dans l'organisation :

```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToApplicationStatus();
```
La méthode surchargée permet de contrôler l'abonnement aux statuts d'une application donnée. La méthode processApplicationStatus() est appelée chaque fois qu'une application correspondant aux critères est connectée ou déconnectée de {{site.data.keyword.iot_short_notm}}.


## Publication des événements à partir de terminaux
{: #publishing_events_devices}

L'exemple de code suivant montre comment les applications peuvent publier des événements comme s'ils provenaient d'un terminal. 

```

    myClient.connect()

    //Generate the event to be published
    JsonObject event = new JsonObject();
    event.addProperty("name", "foo");
    event.addProperty("cpu",  60);
    event.addProperty("mem",  40);

    // publish the event on behalf of device
    myClient.publishEvent(deviceType, deviceId, "blink", event);
```

### Publication d'événements à l'aide de HTTP
{: #publishing_events_http}

Outre MQTT, vous pouvez configurer vos applications pour qu'elles publient des événements de terminal sur {{site.data.keyword.iot_short_notm}} à l'aide de HTTP en exécutant les étapes suivantes : 

* Construire l'instance ApplicationClient à l'aide du fichier de propriétés
* Construire l'événement qui doit être publié
* Spécifier le nom d'événement, le type de terminal et l'ID de terminal
* Publier l'événement à l'aide de la méthode `publishEventOverHTTP`(), comme illustré dans le code suivant :

```

    	ApplicationClient myClient = new ApplicationClient(props);

    	JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

    	code = myClient.publishEventOverHTTP(deviceType, deviceId, "blink", event);
```

Pour la totalité de l'exemple de code, voir l'exemple d'application suivant :

[HttpApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpApplicationDeviceEventPublish.java)

En fonction des paramètres définis dans le fichier de propriétés, la méthode `publishEventOverHTTP()` publie l'événement en mode Quickstart ou en mode de flux enregistré. Lorsque l'ID d'organisation défini dans le fichier de propriétés est `quickstart`, la méthode `publishEventOverHTTP()` publie l'événement sur le service Quickstart de {{site.data.keyword.iot_short_notm}} au format HTTP normal. Lorsqu'une organisation enregistrée valide est spécifiée dans le fichier de propriétés, l'événement est toujours publié à l'aide de HTTPS de sorte que toutes les communications soient sécurisées. 

Le protocole HTTP fournit une distribution de type 'une fois tout au plus', semblable au niveau de qualité de service 'une fois tout au plus' (QoS 0) du protocole MQTT. Lorsque vous utilisez la distribution de type 'une fois tout au plus' pour publier des événements, l'application doit implémenter une logique de relance au cas où une erreur se produirait. 


## Publication de commandes sur des terminaux
{: #publishing_commands_devices}

Les applications peuvent publier des commandes sur des terminaux connectés, comme illustré dans l'exemple suivant :

```

    myClient.connect()

    //Generate the event to be published
    JsonObject data = new JsonObject();
    data.addProperty("name", "stop-rotation");
    data.addProperty("delay",  0);

    //Registered flow allows 0, 1 and 2 QoS
    myAppClient.publishCommand(deviceType, deviceId, "stop", data);
```


## Exemples
{: #examples}


-  [MQTTApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/MQTTApplicationDeviceEventPublish.java) - Exemple d'application qui vous montre comment publier des événements de terminal. 
-   [RegisteredApplicationCommandPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationCommandPublish.java) - Exemple d'application qui vous montre comment publier une commande sur un terminal. 
-  [RegisteredApplicationSubscribeSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationSubscribeSample.java) - Exemple d'application qui vous montre comment vous abonner à différents événements, tels que des événements sur des terminaux, des commandes de terminal, des statuts de terminal et desstatutsd'application. 
-   [SharedSubscriptionSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/SharedSubscriptionSample.java) - Exemple d'application qui vous montre comment générer une application évolutive qui équilibre la charge des messages sur plusieurs instances de l'application. 
-  [Backup and restore sample](https://github.com/ibm-messaging/iot-backup-restore-sample) - Exemple qui vous montre comment sauvegarder et restaurer la configuration de terminal dans une base de données Cloudant NoSQL. 
