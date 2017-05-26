---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-21"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java pour les développeurs de terminaux
{: #java}

Vous pouvez créer et personnaliser des terminaux qui interagissent avec votre organisation sur {{site.data.keyword.iot_full}} en utilisant Java. Une bibliothèque client Java pour {{site.data.keyword.iot_short_notm}}, de la documentation, ainsi que des exemples vous sont fournis pour vous permettre de vous initier au développement de terminal.
{:shortdesc}

## Téléchargement du client et des ressources Java
{: #java_client_download}

Pour accéder aux bibliothèques et exemples client Java pour {{site.data.keyword.iot_short_notm}}, accédez au référentiel [iot-java ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-java){: new_window} dans GitHub et exécutez des instructions d'installation.

## Constructeur
{: #constructor}

Le constructeur génère l'instance client et accepte l'objet `Propriétés` contenant les définitions suivantes :

|Définition |Description |
|:----|:----|
|`org` |Valeur requise qui doit être définie avec votre ID d'organisation. Si vous utilisez un flux Quickstart, spécifiez `quickstart`.|
|`type`  |Valeur requise qui spécifie le type du terminal.|
|`id`  |Valeur requise qui spécifie l'ID unique du terminal.|
|`auth-method`  |Méthode d'authentification à utiliser. La seule méthode prise en charge est `token`.|
|`auth-token`   |Jeton d'authentification permettant d'établir une connexion sécurisée entre votre terminal et {{site.data.keyword.iot_short_notm}}.|
|`clean-session`|Valeur true ou false requise uniquement si vous souhaitez connecter l'application en mode d'abonnement durable. Par défaut, `clean-session` a pour valeur true.|
|`Port`|Numéro de port auquel se connecter. Indiquez 8883 ou 443. Si vous n'indiquez pas de numéro de port, le client se connecte à {{site.data.keyword.iot_short_notm}} sur le numéro de port 8883 par défaut.|
|`MaxInflightMessages`  |Définit le nombre maximal de messages en cours pour la connexion. La valeur par défaut est 100.|
|`Automatic-Reconnect`  |Valeur true ou false qui est requise lorsque vous souhaitez reconnecter automatiquement le terminal à {{site.data.keyword.iot_short_notm}} alors qu'il est en ode déconnecté. La valeur par défaut est false.|
|`Disconnected-Buffer-Size`|Nombre maximal de messages qui peut être stocké en mémoire alors que le client est déconnecté. La valeur par défaut est 5 000.|
|`WebSocket`|Valeur true ou false requise uniquement si vous souhaitez utiliser des connexions WebSocket avec {{site.data.keyword.iot_short_notm}}. La valeur par défaut est false.|

**Remarque :** Pour connecter le terminal en mode d'abonnement durable, affectez la valeur `false` à l'option `clean-session`. Pour plus d'informations sur l'option 'clean-session', voir la section 'Subscription Buffers and Clean Session' de la [documentation MQTT](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

L'objet `Propriétés` crée des définitions qui sont utilisées pour interagir avec le module {{site.data.keyword.iot_short_notm}}.

L'exemple de code suivant montre comment les terminaux peuvent publier des événements en mode Quickstart.

```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class QuickstartDeviceEventPublish {

    public static void main(String[] args) {

        //Provide the device specific data using Properties class
        Properties options = new Properties();
        options.setProperty("org", "quickstart");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generate a JSON object of the event to be published
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Quickstart flow allows only QoS = 0
        myClient.publishEvent("status", event, 0);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

L'exemple de code suivant montre comment les terminaux peuvent publier des événements dans un flux enregistré.


```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublish {

    public static void main(String[] args) {

        //Provide the device specific data, as well as Auth-key and token using Properties class
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generate a JSON object of the event to be published
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Registered flow allows 0, 1 and 2 QoS
        myClient.publishEvent("status", event);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

### Utilisation d'un fichier de configuration

Au lieu d'utiliser directement l'objet `Properties`, vous pouvez utiliser un fichier de configuration contenant les paires nom-valeur pour les propriétés. Si vous utilisez un fichier de configuration contenant un objet `Properties`, utilisez le format de code suivant :

```
package com.ibm.iotf.sample.client.device;

import java.io.File;
import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublishPropertiesFile {

    public static void main(String[] args) {
        //Provide the device specific data, as well as Auth-key and token using Properties class
        Properties options = DeviceClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generate a JSON object of the event to be published
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Registered flow allows 0, 1 and 2 QoS
        myClient.publishEvent("status", event, 1);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

Le fichier de configuration de l'application doit posséder le format suivant :

```
    [device]
    org=$orgId
    typ=$myDeviceType
    id=$myDeviceId
    auth-method=token
    auth-token=$token
```

## Connexion à {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}


Pour établir la connexion à {{site.data.keyword.iot_short_notm}}, utilisez la fonction `connect()`. La fonction `connect()` inclut un paramètre booléen facultatif appelé `autoRetry`, qui détermine si la bibliothèque tente de se reconnecter si un échec de connexion MqttException se produit. Par défaut, `autoRetry` a pour valeur true. Si une connexion MqttSecurityException échoue en raison de détails d'enregistrement de terminal incorrects, la bibliothèque ne tente pas de se reconnecter, même si `autoRetry` a pour valeur true.

Afin de définir l'intervalle 'keep alive' pour MQTT, vous pouvez éventuellement utiliser la méthode `setKeepAliveInterval(int)` avant d'appeler la fonction `connect()`. La valeur `setKeepAliveInterval(int)` est mesurée en secondes et définit l'intervalle de temps maximal entre les messages envoyés ou reçus. Lorsque cette valeur d'intervalle est utilisée, le client peut détecter à quel moment le serveur n'est plus disponible sans avoir à attendre la fin du délai d'attente TCP/IP. Le client s'assure qu'au moins un message transite par le réseau au cours de chaque période d'intervalle 'keep alive'. Si aucun message relatif aux données n'est reçu pendant le délai d'attente, le client envoie un petit message `ping` dont le serveur accuse réception. Par défaut, le paramètre `setKeepAliveInterval(int)` prend la valeur 60 secondes. Pour désactiver la fonction de traitement 'keep alive' sur le client, affectez la valeur 0 au paramètre `setKeepAliveInterval(int)`.


```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(true);
```

Pour contrôler le nombre de tentatives en cas d'échec d'une connexion, utilisez la fonction overloaded connect(int numberOfTimesToRetry).


```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(10);
```

Une fois qu'ils sont connectés à {{site.data.keyword.iot_short_notm}}, vos terminaux peuvent publier des événements et s'abonner afin de recevoir des commandes de terminal d'une application.


## Publication d'événements
{: #publishing_events}

Les événements constituent le mécanisme par lequel les terminaux publient des données sur {{site.data.keyword.iot_short_notm}}. Le terminal contrôle le contenu de l'événement et affecte un nom à chaque événement qu'il envoie.

Lorsqu'un événement est reçu par l'instance {{site.data.keyword.iot_short_notm}}, les données d'identification de l'événement reçu identifient le terminal qui a envoyé l'événement, ce qui signifie qu'un terminal ne peut pas simuler les droits d'accès d'un autre terminal.

Les événements peuvent être publiés avec n'importe lequel des trois [niveaux de qualité de service (QoS)](../../reference/mqtt/index.html#qos-levels) définis par le protocole MQTT.  Par défaut, les événements sont publiés avec le niveau QoS 0.

### Publication d'événements avec le niveau QoS par défaut

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

myClient.publishEvent("status", event);
```


### Augmentation du niveau QoS pour un événement

Vous pouvez augmenter les [niveaux QoS](../../reference/mqtt/index.html#qos-levels) des événements qui sont publiés. La publication des événements dont le niveau QoS est supérieur à zéro peut prendre plus de temps, en raison des informations de réception de confirmation supplémentaires qui sont incluses.

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

//Registered flow allows 0, 1 and 2 QoS
myClient.publishEvent("status", event, 2);
```

### Publication d'événements dans des formats personnalisés

Des événements peuvent être publiés dans différents formats, par exemple, JSON, chaîne, binaire, etc. Par défaut, la bibliothèque publie des événements au format JSON, mais vous pouvez spécifier les données dans d'autres formats, si vous le souhaitez. Par exemple, pour publier des données au format chaîne, utilisez le fragment de code suivant :

```
myClient.connect();

String data = "cpu:"+getProcessCpuLoad();
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

byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = myClient.publishEvent("blink", cpuLoad , "binary", 1);
```

### Publication d'événements à l'aide de HTTP
{: #publishing_events_http}


Outre l'utilisation de MQTT, vous pouvez également configurer vos terminaux pour qu'ils publient des événements sur {{site.data.keyword.iot_short_notm}} via HTTP. Les étapes suivantes permettent de publier des événements via HTTP :

1. Construire une instance `DeviceClient` à l'aide du fichier de propriétés.
2. Construire un événement à publier.
3. Spécifier le nom d'événement et publier l'événement à l'aide de la méthode `publishEventOverHTTP()`, comme illustré dans le code suivant :

``` 
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

boolean response  = myClient.api().publishDeviceEventOverHTTP("blink", event, ContentType.json);
```

Pour visualiser la totalité du code, voir l'exemple de terminal [HttpDeviceEventPublish ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")].{: new_window}

En fonction des paramètres définis dans le fichier de propriétés, la méthode `publishEventOverHTTP()` publie l'événement en mode Quickstart ou en mode de flux enregistré. Lorsque l'ID d'organisation défini dans le fichier de propriétés a pour valeur `quickstart`, la méthode `publishEventOverHTTP()` publie l'événement sur le service Quickstart de l'exemple de terminal au format HTTP normal. Lorsqu'une organisation enregistrée valide est spécifiée dans le fichier de propriétés, les événements sont publiés de manière sécurisée via HTTPS.

Le protocole HTTP fournit une distribution de type 'une fois tout au plus', semblable au niveau de qualité de service 'une fois tout au plus' (QoS 0) du protocole MQTT. Lorsque vous utilisez la distribution de type 'une fois tout au plus' pour publier des événements, l'application doit implémenter une logique de relance au cas où une erreur se produirait.

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## Traitement des commandes
{: #handling_commands}

Lorsque le client du terminal se connecte, il s'abonne automatiquement aux commandes de ce terminal. Pour traiter des commandes spécifiques, vous devez enregistrer une méthode de rappel de commande.
Les messages sont renvoyés en tant qu'instance de la classe `Command` qui possède les propriétés suivantes :

| Propriété     |Type de données     | Description|
|----------------|----------------|
|`payload` |java.lang.String| Données du contenu du message.|
|`format`  |java.lang.String| Le format peut être n'importe quelle chaîne, par exemple, JSON.|
|`command`   |java.lang.String|Identifie la commande.|
|`timestamp`   |org.joda.time.DateTime|Date et heure de l'événement.|


```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;


import com.ibm.iotf.client.device.Command;
import com.ibm.iotf.client.device.CommandCallback;
import com.ibm.iotf.client.device.DeviceClient;


//Implement the CommandCallback class to provide the way in which you want the command to be handled
class MyNewCommandCallback implements CommandCallback, Runnable {

    // A queue to hold & process the commands for smooth handling of MQTT messages
    private BlockingQueue<Command> queue = new LinkedBlockingQueue<Command>();

    /**
    * This method is invoked by the library whenever there is command matching the subscription criteria
    */
    @Override
    public void processCommand(Command cmd) {
        try {
            queue.put(cmd);
            } catch (InterruptedException e) {
        }
    }

    @Override
    public void run() {
        while(true) {
            Command cmd = null;
            try {
                //In this sample, we just display the command
                cmd = queue.take();
                System.out.println("COMMAND RECEIVED = '" + cmd.getCommand() + "'\twith Payload = '" + cmd.getPayload() + "'");
            } catch (InterruptedException e) {}
        }
    }
}

public class RegisteredDeviceCommandSubscribe {


    public static void main(String[] args) {

        //Provide the device specific data, as well as Auth-key and token using Properties class
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Pass the above implemented CommandCallback as an argument to this device client
        myClient.setCommandCallback(new MyNewCommandCallback());

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();
    }
}
```

## Exemples
{: #samples}

Pour obtenir une liste d'exemples de terminal et de gestion des terminaux développés à l'aide de la bibliothèque client Java {{site.data.keyword.iot_short_notm}}, voir le [référentiel GitHub iot-device-samples ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iot-device-samples/tree/master/java){: new_window}.
