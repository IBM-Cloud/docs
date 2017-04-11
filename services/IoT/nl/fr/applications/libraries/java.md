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

# Java pour les développeurs d'applications
{: #java}


Vous pouvez créer et personnaliser des applications qui interagissent avec votre organisation sur {{site.data.keyword.iot_full}} en utilisant Java. Une bibliothèque client Java pour {{site.data.keyword.iot_short_notm}}, de la documentation, ainsi que des exemples vous sont fournis pour vous permettre de vous initier au développement d'application.

{:shortdesc}

## Téléchargement du client et des ressources Java
{: #java_client_download}

Dernière mise à jour : 25 octobre 2016
{: .last-updated}

Pour accéder aux bibliothèques et exemples client Java pour {{site.data.keyword.iot_short_notm}}, accédez au référentiel [iot-java ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-java){: new_window} dans GitHub et exécutez des instructions d'installation. 


## Constructeur
{: #constructor}

Le constructeur génère l'instance client et accepte l'objet `Propriétés` contenant les définitions suivantes :

| Définition     |Description     |
|----------------|----------------|
|`org` |Valeur requise qui doit être définie avec votre ID d'organisation. Si vous utilisez un flux Quickstart, spécifiez `quickstart`.|
|`id` |ID unique de l'application au sein de votre organisation.|
|`auth-method`  |Méthode d'authentification. La seule méthode prise en charge est `apikey`.|
|`auth-key`   |Clé d'API facultative qui est requise lorsque vous affectez la valeur `apikey` au paramètre auth-method.|
|`auth-token`   |Jeton de clé d'API qui est également requis lorsque vous affectez la valeur `apikey` au paramètre auth-method. |
|`clean-session`|Valeur true ou false requise uniquement si vous souhaitez connecter l'application en mode d'abonnement durable. Par défaut, `clean-session` prend la valeur `true`.|
|`Port`|Numéro de port auquel se connecter. Indiquez 8883 ou 443. Si vous n'indiquez pas de numéro de port, le client se connecte à {{site.data.keyword.iot_short_notm}} sur le numéro de port 8883 par défaut.|
|`MaxInflightMessages`  |Définit le nombre maximal de messages en cours pour la connexion. La valeur par défaut est 100.|
|`Automatic-Reconnect`  |Valeur true ou false qui est requise lorsque vous souhaitez reconnecter automatiquement le terminal à {{site.data.keyword.iot_short_notm}} alors qu'il est en ode déconnecté. La valeur par défaut est false.|
|`Disconnected-Buffer-Size`|Nombre maximal de messages qui peut être stocké en mémoire alors que le client est déconnecté. La valeur par défaut est 5 000.|
|`shared-subscription`|Valeur booléenne à laquelle vous devez affecter la valeur true si vous souhaitez construire des applications évolutives qui équilibrent la charge des messages sur plusieurs instances de l'application. Pour plus d'informations, voir [Applications évolutives](../mqtt.html#scalable_apps).

L'objet `Propriétés` crée des définitions qui sont utilisées pour interagir avec le module {{site.data.keyword.iot_short_notm}}. Si vous ne spécifiez pas les propriétés de cet objet, ou si vous indiquez `quickstart`, le client se connecte au service  Quickstart de {{site.data.keyword.iot_short_notm}} en tant que terminal non enregistré.

L'exemple de code suivant vous montre comment construire l'instance de client d'application (`ApplicationClient`) en mode `quickstart` :

```
    import com.ibm.iotf.client.app.ApplicationClient;
    import java.util.Properties;

    Properties options = new Properties();
    options.put("org", "quickstart");

    ApplicationClient myClient = new ApplicationClient(options);
```

L'exemple de code suivant vous montre comment construire l'instance de client d'application (`ApplicationClient`) en mode flux enregistré :

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

Au lieu d'inclure directement l'objet `Propriétés`, vous pouvez utiliser un fichier de configuration qui contient les paires nom-valeur pour l'objet `Propriétés`, comme décrit dans l'exemple de code suivant :

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    ...
```
Le fichier de configuration d'application spécifié doit être au format suivant :

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

Pour établir la connexion à {{site.data.keyword.iot_short_notm}}, utilisez la fonction `connect()`. La fonction `connect()` inclut un paramètre booléen facultatif appelé `autoRetry`, qui détermine si la bibliothèque tente de se reconnecter si un échec de connexion MqttException se produit. Par défaut, `autoRetry` a pour valeur true. Si une connexion MqttSecurityException échoue en raison de détails d'enregistrement de terminal incorrects, la bibliothèque ne tente pas de se reconnecter, même si `autoRetry` a pour valeur true.

Afin de définir l'intervalle 'keep alive' pour MQTT, vous pouvez éventuellement utiliser la méthode `setKeepAliveInterval(int)` avant d'appeler la fonction `connect()`. La valeur `setKeepAliveInterval(int)` est mesurée en secondes et définit l'intervalle de temps maximal entre les messages envoyés ou reçus. Lorsque cette valeur d'intervalle est utilisée, le client peut détecter à quel moment le serveur n'est plus disponible sans avoir à attendre la fin du délai d'attente TCP/IP. Le client s'assure qu'au moins un message transite par le réseau au cours de chaque période d'intervalle 'keep alive'. Si aucun message relatif aux données n'est reçu pendant le délai d'attente, le client envoie un petit message `ping` dont le serveur accuse réception. Par défaut, le paramètre `setKeepAliveInterval(int)` prend la valeur 60 secondes. Pour désactiver la fonction de traitement 'keep alive' sur le client, affectez la valeur 0 au paramètre `setKeepAliveInterval(int)`.

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    myClient.setKeepAliveInterval(120);
    myClient.connect();
```

Pour contrôler le nombre de tentatives en cas d'échec d'une connexion, spécifiez un nombre entier dans la fonction myClient.connect(), comme indiqué dans le fragment de code suivant :

```
    DeviceClient myClient = new DeviceClient(options);
    myClient.setKeepAliveInterval(120);
    myClient.connect(10);
```

Une fois connectés au service {{site.data.keyword.iot_short_notm}}, vos clients d'application peuvent s'abonner à des événements et à des statuts de terminal et publier des événements et des commandes de terminal.

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
|`event.device`|Chaîne|Identifie le terminal de manière unique parmi tous les types de terminal dans l'organisation.|
|`event.deviceType`|Chaîne|Identifie le type de terminal. Généralement, deviceType regroupe des terminaux qui effectuent une tâche spécifique, par exemple, "weatherballoon".|
|`event.deviceId`|Chaîne|Représente l'ID du terminal. Généralement, pour un type de terminal donné, deviceId est un identificateur unique, par exemple, un numéro de série ou une adresse MAC.|
|`event.event`|Chaîne|Utilisé généralement pour regrouper des événements spécifiques, par exemple, "status", "warning" et "data".|
|`event.format`|Chaîne|Le format peut être n'importe quelle chaîne, par exemple, JSON.  |
|`event.data`|Dictionnaire|Données du contenu du message. La longueur maximale est de 131072 octets.|
|`event.timestamp`|Date et heure|Date et heure de l'événement.|


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

Lorsque le rappel de statut est ajouté au client d'application, la méthode `processDeviceStatus()` est appelée chaque fois qu'un terminal correspondant aux critères est connecté ou déconnecté avec {{site.data.keyword.iot_short_notm}}. L'exemple de code suivant vous montre comment ajouter l'instance de rappel de statut au client d'application :

```

    myClient.connect()
    myClient.setStatusCallback(new MyStatusCallback());
    myClient.subscribeToDeviceStatus();
```
Les applications peuvent s'abonner à n'importe quel autre statut d'application, par exemple, les statuts de connexion et de déconnexion avec {{site.data.keyword.iot_short_notm}}. L'exemple de fragment de code suivant montre comment vous abonner au statut d'application d'une organisation {{site.data.keyword.iot_short_notm}} :

```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToApplicationStatus();
```
La méthode surchargée permet de contrôler l'abonnement aux statuts d'une application donnée. La méthode `processApplicationStatus()` est appelée chaque fois qu'une application correspondant aux critères est connectée ou déconnectée de {{site.data.keyword.iot_short_notm}}.


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


Des événements peuvent être publiés dans différents formats, par exemple, JSON, chaîne, binaire, etc. Par défaut, la bibliothèque publie des événements au format JSON, mais vous pouvez spécifier les données dans d'autres formats, si vous le souhaitez. Par exemple, pour publier des données au format chaîne, utilisez le fragment de code suivant :

```
    myClient.connect();
    String data = "cpu:"+60;
    status = myClient.publishEvent("load", data, "text", 2);
```
**Remarque :** Dans l'exemple de code précédent, le contenu de l'événement doit être au format chaîne.

Toutes les données XML peuvent être converties au format chaîne et publiées comme suit :

```
    status = myClient.publishEvent("load", xmlConvertedString, "xml", 2);
```

De même, pour publier des événements au format binaire, utilisez le tableau d'octets, comme illustré dans l'exemple suivant :

```
    myClient.connect();
    byte[] cpuLoad = new byte[] {60, 35, 30, 25};
    status = myClient.publishEvent("blink", cpuLoad , "binary", 1);
```

### Publication d'événements à l'aide de HTTP
{: #publishing_events_http}

Outre l'utilisation de MQTT, vous pouvez également configurer vos applications pour qu'elles publient des événements de terminal sur {{site.data.keyword.iot_short_notm}} via HTTP. Les étapes suivantes permettent de publier des événements de terminal via HTTP :

1. Construire l'instance ApplicationClient à l'aide du fichier de propriétés.
2. Construire l'événement qui doit être publié.
3. Spécifier le nom d'événement, le type de terminal et l'ID de terminal.
4. Publier l'événement à l'aide de la méthode `publishEventOverHTTP`(), comme illustré dans l'exemple de code suivant :

```
    	ApplicationClient myClient = new ApplicationClient(props);

    	JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

    	boolean status = myClient.publishApplicationEventforDeviceOverHTTP(deviceId, deviceType, "blink", event, ContentType.json);
```

Pour afficher la totalité de l'exemple de code, voir l'exemple d'application [HttpApplicationDeviceEventPublish ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpApplicationDeviceEventPublish.java){: new_window}. 

En fonction des paramètres définis dans le fichier de propriétés, la méthode `publishEventOverHTTP()` publie l'événement en mode Quickstart ou en mode de flux enregistré. Lorsque `quickstart` est spécifié comme ID d'organisation dans le fichier de propriétés, la méthode `publishEventOverHTTP()` publie l'événement sur le service Quickstart de {{site.data.keyword.iot_short_notm}} au format HTTP normal. Lorsqu'une organisation enregistrée valide est spécifiée dans le fichier de propriétés, l'événement est toujours publié à l'aide de HTTPS de sorte que toutes les communications soient sécurisées.

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

### Publication de commandes à l'aide de HTTP
{: #publishing_commands_http}

Outre l'utilisation de MQTT, vous pouvez également configurer vos applications pour qu'elles publient des commandes sur le terminal connecté via HTTP. Les étapes suivantes permettent de publier des événements de terminal via HTTP :

1. Construire l'instance ApplicationClient à l'aide du fichier de propriétés
2. Construire la commande qui doit être publiée
3. Spécifier le nom de commande, le type de terminal et l'ID de terminal
4. Publier la commande à l'aide de la méthode `publishCommandOverHTTP`(), comme illustré dans le code suivant :

```

    	ApplicationClient myClient = new ApplicationClient(props);

    	// Generate a JSON object of the event to be published
	JsonObject event = new JsonObject();
	event.addProperty("reboot", 5);

	boolean response = myClient.publishCommandOverHTTP("execute", event);
```

Pour afficher la totalité de l'exemple de code, voir l'exemple d'application [HttpCommandPublish ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpCommandPublish.java){: new_window}. 

Le protocole HTTP fournit une distribution de type 'une fois tout au plus', semblable au niveau de qualité de service 'une fois tout au plus' (QoS 0) du protocole MQTT. Lorsque vous utilisez la distribution de type 'une fois tout au plus' pour publier des commandes, l'application doit implémenter une logique de relance au cas où une erreur se produirait. Pour plus d'informations, voir [API REST HTTP pour les applications](../api.html).


## Exemples
{: #samples}

-  [MQTTApplicationDeviceEventPublish ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/MQTTApplicationDeviceEventPublish.java){: new_window} - Exemple d'application qui vous montre comment publier des événements de terminal. 
-   [RegisteredApplicationCommandPublish ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationCommandPublish.java){: new_window} - Exemple d'application qui vous montre comment publier une commande sur un terminal. 
-  [RegisteredApplicationSubscribeSample ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationSubscribeSample.java){: new_window} - Exemple d'application qui vous montre comment vous abonner à différents événements, tels que des événements sur des terminaux, des commandes de terminal, des statuts de terminal et desstatutsd'application. 
-   [SharedSubscriptionSample ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/SharedSubscriptionSample.java){: new_window} - Exemple d'application qui vous montre comment générer une application évolutive qui équilibre la charge des messages sur plusieurs instances de l'application. 
-  [Backup-restore-sample ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iot-backup-restore-sample){: new_window} - Exemple qui vous montre comment sauvegarder et restaurer la configuration de terminal dans {{site.data.keyword.cloudant}}.  
