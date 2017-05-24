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


# Python pour les développeurs de terminaux
{: #python}

Vous pouvez utiliser Python pour générer et développer un code de terminal afin d'interagir avec votre organisation sur {{site.data.keyword.iot_full}}. Le client Python pour {{site.data.keyword.iot_short_notm}} fournit une API qui facilite l'interaction simple avec les fonctions {{site.data.keyword.iot_short_notm}} en faisant abstraction des protocoles sous-jacents, tels que MQTT et HTTP.
{:shortdesc}

Utilisez les informations et les exemples fournis pour commencer à développer vos terminaux à l'aide de Python.

## Téléchargement du client et des ressources Python
{: #python_client_download}

Pour accéder au client Python pour {{site.data.keyword.iot_short_notm}} et aux autres ressources disponibles, accédez au référentiel [iot-python ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-python){: new_window} dans GitHub et exécutez les instructions d'installation.

## Constructeur
{: #constructor}

Le dictionnaire d'options crée des définitions utilisées pour interagir avec le module {{site.data.keyword.iot_short_notm}}. Le constructeur génère l'instance client et accepte un dictionnaire d'options qui contient les définitions suivantes :

|Définition|Description |
|:---|:---|
|`orgId`|ID de votre organisation.|
|`type`|Type du terminal. Le type de terminal est un regroupement pour les terminaux qui exécutent une tâche spécifique, par exemple, "weatherballoon".|
|`id`|ID unique pour identifier un terminal. Généralement, pour un type de terminal donné, l'ID de terminal est un identificateur unique de ce terminal, par exemple, un numéro de série ou une adresse MAC.|
|`auth-method`|Méthode d'authentification. La seule méthode prise en charge est `apikey`.|
|`auth-token`|Jeton de clé d'API qui est également requis lorsque vous affectez la valeur `apikey` au paramètre auth-method.|
|`clean-session`|Valeur true ou false requise uniquement si vous souhaitez connecter l'application en mode d'abonnement durable. Par défaut, `clean-session` a pour valeur true.|

Si aucun dictionnaire d'options n'est fourni, le client se connecte au service QuickStart de {{site.data.keyword.iot_short_notm}} en tant que terminal non enregistré.

```python

import ibmiotf.device
try:
  options = {
    "org": orgId,
    "type": deviceType,
    "id": deviceId,
    "auth-method": authMethod,
    "auth-token": authToken,
    "clean-session": true
  }
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

### Utilisation d'un fichier de configuration

Au lieu de définir un dictionnaire d'options directement, vous pouvez également définir un dictionnaire d'options séparément dans un fichier de configuration, comme illustré dans l'exemple de code suivant :

```python

import ibmiotf.device
try:
  options = ibmiotf.device.ParseConfigFile(configFilePath)
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

Le fichier de configuration contenant le dictionnaire d'options doit être au format suivant :

```python

[device]
org=orgID
type=deviceType
id=deviceId
auth-method=token
auth-token=token
clean-session=true/false
```

## Publication d'événements
{: #publishing_events}

Les événements constituent le mécanisme par lequel les terminaux publient des données sur {{site.data.keyword.iot_short_notm}}. Le terminal contrôle le contenu de l'événement et affecte un nom à chaque événement qu'il envoie.

Lorsqu'un événement est reçu par l'instance {{site.data.keyword.iot_short_notm}}, les données d'identification de l'événement reçu identifient le terminal qui a envoyé l'événement, ce qui signifie qu'un terminal ne peut pas simuler les droits d'accès d'un autre terminal.

Les événements peuvent être publiés avec n'importe lequel des trois niveaux de qualité de service (QoS) définis par le protocole MQTT.  Par défaut, les événements sont publiés avec le niveau QoS `0`.

### Publication d'un événement à l'aide de la qualité de service par défaut

```
client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData)
```

### Augmentation du niveau QoS pour un événement

Vous pouvez augmenter le [niveau de qualité de service (QoS)](../../reference/mqtt/index.html#qos-levels) des événements qui sont publiés. La publication des événements dont le niveau QoS est supérieur à `0` peut prendre plus de temps, en raison des informations de réception de confirmation supplémentaires qui sont incluses.

**Remarque :** Le mode flux Quickstart ne prend en charge que le niveau QoS `0`.

```
client.connect()
myQosLevel=2
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData, myQosLevel)
```
## Traitement des commandes
{: #handling_commands}

Lorsque le client du terminal se connecte, il s'abonne automatiquement aux commandes spécifiées pour ce terminal. Pour traiter des commandes spécifiques, vous devez enregistrer une méthode de rappel de commande. Les messages sont renvoyés en tant qu'instance de la classe Command qui possède les propriétés suivantes :

|Propriété|Type de données|Description|
|:---|:---|
|`command`|Chaîne|Identifie la commande.|
|`format`|Chaîne|Le format peut être n'importe quelle chaîne, par exemple, JSON.|
|`data`|Dictionnaire|Données du contenu. La longueur maximale est de 131072 octets.|
|`timestamp`|Date et heure|Date et heure de l'événement.|


```python

def myCommandCallback(cmd):
  print("Command received: %s" % cmd.data)
  if cmd.command == "setInterval":
    if 'interval' not in cmd.data:
      print("Error - command is missing required information: 'interval'")
    else:
      interval = cmd.data['interval']
  elif cmd.command == "print":
    if 'message' not in cmd.data:
      print("Error - command is missing required information: 'message'")
    else:
      print(cmd.data['message'])

...
client.connect()
client.commandCallback = myCommandCallback
```

## Prise en charge d'un format de message personnalisé
{: #custom_message_format}

Par défaut, le format de message est `json`, ce qui signifie que la bibliothèque prend en charge le codage et le décodage des objets dictionnaire Python au format JSON. Lorsque le format de message est `json-iotf`, le message est codé conformément à la spécification de contenu JSON {{site.data.keyword.iot_short_notm}}. Pour ajouter la prise en charge de vos propres formats de message personnalisés, voir l'[exemple de format de message personnalisé ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-python/tree/master/samples/customMessageFormat){: new_window} dans GitHub.

Lorsque vous créez un module de codage personnalisé, vous devez l'enregistrer dans le client de terminal, comme illustré dans l'exemple suivant :

```python

import myCustomCodec

client.setMessageEncoderModule("custom", myCustomCodec)
client.publishEvent("status", "custom", myData)
```
Si un événement est envoyé dans un format inconnu ou si un terminal ne reconnaît pas le format, la bibliothèque de terminal renvoie une condition `MissingMessageDecoderException`.
