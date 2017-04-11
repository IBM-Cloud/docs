---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

#Développement de passerelles sur {{site.data.keyword.iot_short_notm}} à l'aide de Java
{: #java_cli_gw}

Si vos terminaux ne peuvent pas se connecter directement à votre organisation sur {{site.data.keyword.iot_full}}, vous pouvez créer et personnaliser des passerelles à l'aide de Java. Une bibliothèque client Java pour {{site.data.keyword.iot_short_notm}}, de la documentation, ainsi que des exemples vous sont fournis pour vous permettre de vous initier au développement de passerelle.
{:shortdesc}

## Téléchargement du client et des ressources Java
{: #java_client_download}

Pour accéder aux bibliothèques et exemples client Java pour {{site.data.keyword.iot_short_notm}}, accédez au référentiel [iot-java](https://github.com/ibm-watson-iot/iot-java) dans GitHub et exécutez les instructions d'installation.

## Constructeur
{: #constructor}

Le constructeur génère l'instance client de passerelle et accepte l'objet `Propriétés` contenant les définitions suivantes :

|Définition |Description |
|:----|:----|
|`org`|Valeur requise qui doit être définie avec votre ID d'organisation. Si vous utilisez un flux Quickstart, spécifiez `quickstart`.|
|`domain`|URL de noeud final de message, qui est facultative. Si vous n'indiquez pas une valeur pour un domaine, l'URL prend la valeur par défaut `internetofthings.ibmcloud.com`, qui est le serveur de production {{site.data.keyword.iot_short_notm}}.|
|`type`|Valeur requise qui spécifie le type de la passerelle.|
|`id` |Valeur requise qui spécifie l'ID unique de la passerelle.|
|`auth-method`|Méthode d'authentification à utiliser. La seule méthode prise en charge est `token`.|
|`auth-token`|Jeton d'authentification de clé d'API permettant d'établir une connexion sécurisée entre votre passerelle et {{site.data.keyword.iot_short_notm}}.|
|`clean-session`|Valeur true ou false requise uniquement si vous souhaitez connecter la passerelle en mode d'abonnement durable. Par défaut, `clean-session` a pour valeur true.|
|`WebSocket`|Valeur true ou false requise uniquement si vous souhaitez connecter la passerelle à l'aide de WebSockets.|
|`Port`|Numéro de port auquel se connecter. Indiquez 8883 ou 443. Si vous n'indiquez pas de numéro de port, le client se connecte à {{site.data.keyword.iot_short_notm}} sur le numéro de port 8883 par défaut.|
|`MaxInflightMessages`|Définit le nombre maximal de messages en cours pour la connexion. La valeur par défaut est 100.|
|`Automatic-Reconnect`|Valeur true ou false lorsque vous souhaitez reconnecter automatiquement la passerelle à {{site.data.keyword.iot_short_notm}} alors qu'elle est en mode déconnecté. La valeur par défaut est false.|
|`Disconnected-Buffer-Size`|Nombre maximal de messages qui peut être stocké en mémoire alors que le client est déconnecté. La valeur par défaut est 5 000.|

**Remarque :** Pour connecter le passerelle en mode d'abonnement durable, affectez la valeur `false` à l'option `clean-session`. Pour plus d'informations sur l'option 'clean-session', voir la section 'Subscription Buffers and Clean Session' de la [documentation MQTT](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

L'objet `Propriétés` crée des définitions qui sont utilisées pour interagir avec le module {{site.data.keyword.iot_short_notm}}.

L'exemple de code suivant montre comment créer une instance client de passerelle :

```java
Properties options = new Properties();
options.setProperty("org", "<Your organization ID>");
options.setProperty("type", "<The gateway device type>");
options.setProperty("id", "The gateway device ID");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "API token");
GatewayClient gwClient = new GatewayClient(options);

```


### Utilisation d'un fichier de configuration

Au lieu d'utiliser l'objet `Propriétés` directement pour créer une instance de passerelle, vous pouvez utiliser un fichier de configuration contenant les paires nom-valeur pour les propriétés de la passerelle. Pour utiliser un fichier de configuration afin de créer l'objet `Propriétés` pour la passerelle, utilisez le format de code suivant :

```Java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
...
```

Le fichier de configuration de l'application doit posséder le format suivant :

```java
[Gateway]
org=$orgId
domain=$domain
typ=$myGatewayDeviceType
id=$myGatewayDeviceId
auth-method=token
auth-token=$token

```

## Connexion à {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

Pour établir la connexion à {{site.data.keyword.iot_short_notm}}, utilisez la fonction `connect()`. La fonction `connect()` inclut un paramètre booléen facultatif appelé `autoRetry`, qui détermine si la bibliothèque tente de se reconnecter en cas d'échec de la connexion MQTT (MqttException). Par défaut, `autoRetry` a pour valeur true. Si une connexion MqttSecurityException échoue en raison de détails d'enregistrement de terminal incorrects, la bibliothèque ne tente pas de se reconnecter, même si `autoRetry` a pour valeur true.

Afin de définir l'intervalle keep alive pour MQTT, vous pouvez éventuellement utiliser la méthode `setKeepAliveInterval(int)` avant d'appeler la fonction `connect()`. La valeur `setKeepAliveInterval(int)` est mesurée en secondes et définit l'intervalle de temps maximal entre les messages envoyés ou reçus. Lorsqu'une valeur `setKeepAliveInterval(int)` est spécifiée, le client peut détecter que le serveur n'est plus disponible sans avoir à attendre la fin du délai d'attente TCP/IP. Le client s'assure qu'au moins un message transite par le réseau au cours de chaque période d'intervalle keep alive. Si aucun message relatif aux données n'est reçu pendant le délai d'attente, le client envoie un petit message `ping` dont le serveur accuse réception. Par défaut, le paramètre `setKeepAliveInterval(int)` prend la valeur 60 secondes. Pour désactiver la fonction de traitement keep alive sur le client, affectez la valeur 0 au paramètre `setKeepAliveInterval(int)`.

```java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient.connect();
```

Pour contrôler le nombre de tentatives en cas d'échec d'une connexion, utilisez la fonction overloaded connect(int numberOfTimesToRetry).

```java
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient .connect(10);
```

Lorsque le client de passerelle se connecte à {{site.data.keyword.iot_short_notm}}, la passerelle peut publier des événements et s'abonner aux commandes pour elle-même et pour le compte des terminaux qui sont connectés à la passerelle.

## Enregistrement des terminaux qui se trouvent derrière la passerelle
{: #register_device_gateway}

Vous pouvez enregistrer des terminaux qui se trouvent derrière la passerelle connectée à votre instance {{site.data.keyword.iot_short_notm}} soit automatiquement soit en développant un code à l'aide de l'API.

### Enregistrement de terminal automatique
Vous pouvez enregistrer vos terminaux automatiquement sur {{site.data.keyword.iot_short_notm}} chaque fois que la passerelle publie des événements ou s'abonne à des commandes pour les terminaux qui lui sont connectés.

### Enregistrement de terminal d'API
Vous pouvez utiliser l'API {{site.data.keyword.iot_short_notm}} pour enregistrer les terminaux situés derrière une passerelle auprès de votre instance {{site.data.keyword.iot_short_notm}}.

Pour simplifier le développement à l'aide de l'API {{site.data.keyword.iot_short_notm}}, initiez une instance client API en appelant la méthode api(), illustrée dans l'exemple de code suivant :

```java
import com.ibm.iotf.client.api.APIClient;
....

GatewayClient gwClient = new GatewayClient(props);
gwClient.connect();

APIClient api = gwClient.api();
```
Lorsque vous recevez le descripteur du client API, vous pouvez commencer à enregistrer des terminaux auprès d'une passerelle, comme décrit dans l'exemple de code suivant :

```java
gwClient.connect();

  String deviceToBeAdded = "{\"deviceId\": \"" + DEVICE_ID +
					"\",\"authToken\": \"qwer123\"}";

    JsonParser parser = new JsonParser();
    JsonElement input = parser.parse(deviceToBeAdded);
    JsonObject response = this.gwClient.api().registerDeviceUnderGateway(DEVICE_TYPE, gwDeviceId, gwDeviceType, input);

```

Lorsqu'un terminal situé derrière une passerelle est enregistré, le terminal est associé à la passerelle par les valeurs des attributs `gwDeviceId` et `gwDeviceType`.

## Publication d'événements
{: #publish_events}

Les événements constituent le mécanisme par lequel les passerelles et les terminaux publient des données sur {{site.data.keyword.iot_short_notm}}. La passerelle ou le terminal contrôle le contenu de l'événement et affecte un nom à chaque événement qu'il envoie. Une passerelle peut publier des événements elle-même ou pour le compte de n'importe quel terminal connecté via la passerelle.

Lorsqu'un événement est reçu par l'instance {{site.data.keyword.iot_short_notm}}, les données d'identification de l'événement reçu identifient la passerelle qui a envoyé l'événement, ce qui signifie qu'une passerelle ne peut pas simuler les droits d'accès d'un autre terminal.

Les événements peuvent être publiés avec n'importe lequel des trois [niveaux de qualité de service (QoS)](../../reference/mqtt/index.html#qos-levels) définis par le protocole MQTT.  Par défaut, les événements sont publiés avec le niveau QoS 0.

### Code de publication d'événements de passerelle au niveau QoS par défaut

```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event);
```

### Code d'augmentation du niveau QoS par défaut pour un événement

Vous pouvez augmenter les [niveaux QoS](../../reference/mqtt/index.html#qos-levels) des événements de passerelle qui sont publiés. La publication des événements dont le niveau QoS est supérieur à zéro peut prendre plus de temps, en raison des informations de réception de confirmation supplémentaires qui sont incluses.


```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event, 2);
```

### Code de publication d'événements dans des formats personnalisés

Des événements peuvent être publiés dans différents formats, par exemple, JSON, chaîne, binaire, etc. Par défaut, la bibliothèque publie des événements au format JSON, mais vous pouvez spécifier les données dans d'autres formats, si vous le souhaitez. Par exemple, pour publier des données au format chaîne, utilisez le fragment de code suivant :

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishGatewayEvent("load", data, "text", 2);
```

**Remarque :** Dans l'exemple de code précédent, le contenu de l'événement doit être au format chaîne.

Des données XML peuvent être converties au format chaîne et publiées comme illustré dans l'exemple de code suivant :

```java
status = gwClient.publishGatewayEvent("load", xmlConvertedString, "xml", 2);
```

De même, pour publier des événements au format binaire, utilisez le tableau d'octets, comme illustré dans l'exemple suivant :

```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishGatewayEvent("blink", cpuLoad , "binary", 1);
```

### Code de publication d'événements à partir de terminaux
{: #publishing_events_devices}

Une passerelle peut publier des événements pour le compte de n'importe quel terminal connecté via la passerelle en transmettant les valeurs ID type et ID terminal de l'événement d'origine, comme décrit dans l'exemple suivant :

```java

gwClient.connect()

//Generate the event to be published
    JsonObject event = new JsonObject();
    event.addProperty("name", "foo");
    event.addProperty("cpu",  60);
    event.addProperty("mem",  40);

// publish the event on behalf of device
gwClient.publishDeviceEvent(deviceType, deviceId, eventName, event);
```

Utilisez la méthode `publishDeviceEvent()` surchargée pour publier l'événement de terminal à un niveau de qualité de service préféré. Pour plus d'informations sur la structure de sujet utilisée, voir [Connectivité MQTT pour les passerelles](../mqtt.html).

### Code de publication d'événements de terminal dans un format personnalisé

A l'instar des événements de passerelle, les événements de terminal peuvent également être publiés dans différents formats. Par défaut, la bibliothèque publie des événements de terminal au format JSON, mais vous pouvez spécifier les données dans d'autres formats, si vous le souhaitez. Par exemple, pour publier des données au format chaîne, utilisez l'exemple de code suivant :

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", data, "text", 2);
```

**Remarque :** Le contenu de l'événement doit être au format chaîne.

Toutes les données XML peuvent être converties au format chaîne et publiées comme illustré dans l'exemple suivant :

```java
status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", xmlConvertedString, "xml", 2);
```

De même, pour publier des événements de terminal au format binaire, utilisez le tableau d'octets, comme illustré dans l'exemple suivant :
```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishDeviceEvent(deviceType, deviceId, "blink", cpuLoad , "binary", 1);
```

## Traitement des commandes
{: #handling_commands}

La passerelle peut s'abonner aux commandes qui lui sont envoyées directement et qui sont envoyées à tout terminal connecté derrière une passerelle. Lorsque le client de passerelle se connecte, il s'abonne automatiquement aux commandes de cette passerelle. Mais, pour vous abonner aux commandes des terminaux qui sont connectés via la passerelle, utilisez la méthode `subscribeToDeviceCommands()` surchargée, comme illustré dans l'exemple suivant :

```java
gwClient.connect()

// subscribe to commands on behalf of device
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

Pour traiter des commandes spécifiques, vous devez enregistrer une méthode de rappel `Command`. Les messages sont renvoyés en tant qu'instance de la classe `Command` et contiennent les propriétés suivantes :


| Propriété     |Type de données     | Description|
|----------------|----------------|---------------
|`deviceType`|Chaîne| Type de terminal pour lequel la commande est reçue.|
|`deviceId`|Chaîne| ID terminal pour lequel la commande est reçue ; il peut s'agir de la passerelle ou d'un terminal connecté via la passerelle.|
|`data`|objet| Contenu de la commande.|
|`format`|Chaîne| Format du contenu de la commande ; il peut s'agir de n'importe quel chaîne, par exemple, JSON, d'un format binaire, texte ou autre.|
|`command`|Chaîne|Nom de la commande.|
|`timestamp`|org.joda.time.DateTime|Date et heure auxquelles la commande a été envoyée.|

L'exemple de code suivant montre comment vous pouvez implémenter la méthode de rappel `Command` :

```java
import com.ibm.iotf.client.gateway.Command;
import com.ibm.iotf.client.gateway.GatewayCallback;

public class GatewayCommandCallback implements GatewayCallback, Runnable {
	// A queue to hold and process the commands
	private BlockingQueue<Command> queue = new LinkedBlockingQueue<Command>();

	public void processCommand(Command cmd) {
  	    queue.put(cmd);
  	}

  	public void run() {
  	    while(true) {
  	        Command cmd = queue.take();
  	        System.out.println("Command " + cmd.getData());

  	        // code to process the command
  	    }
  	}

  	/**
	 * Si une passerelle s'abonne à un sujet d'un terminal ou envoie des données pour le compte d'un terminal
	 * auquel elle n'est pas autorisée à se connecter, le message ou l'abonnement est ignoré.
	 * Ce comportement est différent de celui des applications pour lesquelles la connexion prend fin.
	 * La passerelle est avertie du sujet de notification :
	 */
  	@Override
public void processNotification(Notification notification) {

}
  }

```
Lorsque le rappel `Command` est ajouté au client de passerelle, la méthode `processCommand()` est appelée chaque fois qu'une commande est publiée avec les critères souscrits.

L'exemple de code suivant montre comment ajouter le rappel `Command` dans l'instance client de passerelle.

```java
gwClient.connect()
GatewayCommandCallback callback = new GatewayCommandCallback();
gwClient.setGatewayCallback(callback);
//Subscribe to a device that is connected to the gateway
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

Des méthodes surchargées sont disponibles pour contrôler l'abonnement aux commandes.

### Affichage de la liste des terminaux qui sont connectés via une passerelle
{: #list_devices_gw}


Pour extraire tous les terminaux qui sont connectés via la passerelle spécifiée (typeId, deviceId) à {{site.data.keyword.iot_short_notm}}, appelez la méthode `getDevicesConnectedThroughGateway()`.

```java
gwClient.connect()
gwClient.api().getDevicesConnectedThroughGateway(gatewayType, gatewayId);
```

## Exemples
{: #samples}

Plusieurs exemples sont disponibles pour vous aider à connecter des passerelles et les terminaux situés derrière les passerelles à votre instance de {{site.data.keyword.iot_short_notm}}. Les exemples utilisent la bibliothèque client Java {{site.data.keyword.iot_short_notm}} et figurent dans le [référentiel GitHub d'exemples de passerelle ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples){: new_window}.

## Recettes
{: #recipes}

| Recette     | Description|
|----------------|----------------
|[Connecting your device as a gateway to {{site.data.keyword.iot_short_notm}} ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-gateway-to-watson-iot-platform/){: new_window}| Projet GitHub et instructions détaillées qui expliquent comment connecter une passerelle Raspberry Pi et les terminaux Arduino Uno situés derrière la passerelle à {{site.data.keyword.iot_short_notm}}.
|[Raspberry Pi as a managed gateway in {{site.data.keyword.iot_short_notm}} ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/){: new_window}|Extension de la recette de passerelle précédente qui explique comment connecter votre passerelle Raspberry Pi en tant que terminal géré dans {{site.data.keyword.iot_short_notm}} et comment effectuer des opérations de gestion de terminaux.
