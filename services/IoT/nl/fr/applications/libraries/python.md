---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-02-20"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Python pour les développeurs d'applications
{: #python}


Vous pouvez utiliser Python pour générer et développer des applications qui interagissent avec votre organisation sur {{site.data.keyword.iot_full}}. Le client Python pour {{site.data.keyword.iot_short_notm}} fournit une API qui facilite l'interaction simple avec les fonctions {{site.data.keyword.iot_short_notm}} en faisant abstraction des protocoles sous-jacents, tels que MQTT et HTTP.

{:shortdesc}

Utilisez les informations et les exemples fournis pour commencer à développer vos applications en utilisant Python.

## Téléchargement du client et des ressources Python
{: #python_client_download}

Pour accéder au client Python pour {{site.data.keyword.iot_short_notm}} et aux autres ressources disponibles, accédez au référentiel [iot-python ![](../../../../icons/launch-glyph.svg)](https://github.com/ibm-messaging/iot-python) dans GitHub et exécutez les instructions d'installation. 

## Constructeur
{: #constructor}

Le dictionnaire d'options crée des définitions utilisées pour interagir avec le module {{site.data.keyword.iot_short_notm}}. Le constructeur génère l'instance client et accepte un dictionnaire d'options qui contient les définitions suivantes :

|Définition|Description |
|:-----|:-----|
|`orgId`|ID de votre organisation.|
|`appId`|ID unique d'une application au sein de votre organisation.|
|`auth-method`|Méthode d'authentification. La seule méthode prise en charge est `apikey`.|
|`auth-key`|Clé d'API facultative qui est requise lorsque vous affectez la valeur `apikey` au paramètre auth-method.|
|`auth-token`|Jeton de clé d'API qui est également requis lorsque vous affectez la valeur `apikey` au paramètre auth-method.|
|`clean-session`|Valeur true ou false requise uniquement si vous souhaitez connecter l'application en mode d'abonnement durable. Par défaut, `clean-session` a pour valeur true.|


Si aucun dictionnaire d'options n'est fourni, le client se connecte au service QuickStart de {{site.data.keyword.iot_short_notm}} en tant que terminal non enregistré.

```python

import ibmiotf.application
try:
  options = {
    "org": organization,
    "id": appId,
    "auth-method": authMethod,
    "auth-key": authKey,
    "auth-token": authToken,
    "clean-session": true
  }
  client = ibmiotf.application.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

### Utilisation d'un fichier de configuration


Si vous n'utilisez pas de dictionnaire d'options, vous devez inclure un fichier de configuration contenant un dictionnaire d'options au format de code suivant :

```python

import ibmiotf.application
try:
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)
except ibmiotf.ConnectionException as e:
...
```
Le fichier de configuration de l'application doit posséder le format suivant :

```python

[application]
org=orgId
id=myApplication
auth-method=apikey
auth-key=key
auth-token=token
clean-session=true/false

```

## Appels d'API
{: #api_calls}

Chaque méthode du client API répond avec :

- Une réponse JSON ou booléenne valide, si elle aboutit.
- Une exception IoTFCReSTException, si elle échoue.

Pour plus d'informations sur la raison de l'échec d'un appel d'API, ou pour déterminer si l'action a partiellement abouti, une application peut effectuer l'analyse syntaxique des propriétés d'une réponse négative. La réponse négative IoTFCReSTException contient les propriétés suivantes :

|Propriété|Description|
|:---|:---|
|`httpcode`|Code de statut HTTP.|
|`message`|Message d'exception qui contient le motif de l'échec.|
|`response`|Elément JSON qui contient la réponse partielle. En l'absence de réponse, cette valeur est NULL.|

## Abonnement aux événements d'un terminal
{: #subscribe_device_events}

Les événements constituent le mécanisme par lequel les terminaux publient des données sur  l'instance {{site.data.keyword.iot_short_notm}}. Le terminal contrôle le contenu de l'événement et affecte un nom à chaque événement qu'il envoie.

Lorsqu'un événement est reçu par l'instance {{site.data.keyword.iot_short_notm}}, les données d'identification de l'événement reçu identifient le terminal qui a envoyé l'événement, ce qui signifie qu'un terminal ne peut pas simuler les droits d'accès d'un autre terminal.

Par défaut, les applications s'abonnent à tous les événements depuis tous les terminaux connectés. Utilisez les paramètres deviceType, deviceId, event et msgFormat pour contrôler la portée de l'abonnement. Un même client peut prendre en charge plusieurs abonnements. Les exemples de code suivants vous montrent comment utiliser ces paramètres afin de définir la portée d'un abonnement :


### Abonnement à tous les événements depuis tous les terminaux


```python

import ibmiotf.application
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents()
```

### Abonnement à tous les événements depuis tous les terminaux d'un type donné


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType)
```

### Abonnement à un événement spécifique depuis tous les terminaux


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(event=myEvent)
```

### Abonnement à un événement spécifique depuis au moins deux terminaux différents

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, event=myEvent)
client.subscribeToDeviceEvents(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId, event=myEvent)
```

### Abonnement à tous les événements publiés au format JSON

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, msgFormat="json")
```

## Traitement des événements provenant des terminaux
{: #handling_events_devices}

Pour traiter les événements reçus par vos abonnements, vous devez enregistrer une méthode de rappel d'événement. Les messages sont renvoyés sous la forme d'une instance de la classe Event :

|Propriété|Type de données|Description|
|:---|:---|
|`event.device`|Chaîne|Identifie le terminal de manière unique parmi tous les types de terminal dans l'organisation.|
|`event.deviceType`|Chaîne|Identifie le type de terminal. Généralement, deviceType regroupe des terminaux qui effectuent une tâche spécifique, par exemple, "weatherballoon".|
|`event.deviceId`|Chaîne|Représente l'ID du terminal. Généralement, pour un type de terminal donné, deviceId est un identificateur unique, par exemple, un numéro de série ou une adresse MAC.|
|`event.event`|Chaîne|Utilisé généralement pour regrouper des événements spécifiques, par exemple, "status", "warning" et "data".
|`event.format`|Chaîne|Le format peut être n'importe quelle chaîne, par exemple, JSON.
|`event.data`|Dictionnaire|Données du contenu du message. La longueur maximale est de 131072 octets.
|`event.timestamp`|Date et heure|Date et heure de l'événement.|

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  def myEventCallback(event):
      str = "%s event '%s' received from device [%s]: %s"
      print(str % (event.format, event.event, event.device, json.dumps(event.data)))

...
client.connect()
client.deviceEventCallback = myEventCallback
client.subscribeToDeviceEvents()
```


## Abonnement au statut des terminaux
{: #subscribe_device_status}


Par défaut, lorsque vous vous abonnez au statut de terminal, des mises à jour de statut sont reçues pour tous les terminaux connectés. Utilisez les paramètres de type et d'ID pour contrôler la portée de l'abonnement. Un client unique peut prendre en charge plusieurs abonnements.

### Abonnement aux mises à jour de statut pour tous les terminaux


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus()
```

### Abonnement aux mises à jour de statut pour tous les terminaux d'un type donné


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType)
```

### Abonnement aux mises à jour de statut pour deux terminaux différents


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType, deviceId=myDeviceId)
client.subscribeToDeviceStatus(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId)
```

## Traitement des mises à jour du statut des terminaux
{: #handling_device_updates}

Evénements de statut

Pour traiter les mises à jour de statut reçues par vos abonnements, vous devez enregistrer une méthode de rappel d'événement. Les messages sont renvoyés sous la forme d'une instance de la classe Status.

Il existe deux types d'événement de statut, `Connect` et `Disconnect`. Tous les événements de statut comprennent les propriétés suivantes :

|Propriété|Type de données|
|:---|:---|
|`status.clientAddr`|Chaîne|
|`status.protocol`|Chaîne|
|`status.clientId`|Chaîne|
|`status.user`|Chaîne|
|`status.time`|Date et heure|
|`status.action`|Chaîne|
|`status.connectTime`|Date et heure|
|`status.port`|Entier|


La propriété `status.action` détermine si un événement de statut est de type `Connect` ou `Disconnect`.

Les événements de statut `Disconnect` incluent les propriétés supplémentaires suivantes :

|Propriété|Type de données|
|:---|:---|
|`status.writeMsg`|Entier|
|`status.readMsg`|Entier|
|`status.reason`|Chaîne|
|`status.readBytes`|Entier|
|`status.writeBytes`|Entier|

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

def myStatusCallback(status):

  if status.action == "Disconnect":
    str = "%s - device %s - %s (%s)"
    print(str % (status.time.isoformat(), status.device, status.action, status.reason))
    else:
      print("%s - %s - %s" % (status.time.isoformat(), status.device, status.action))
  ...
client.connect()
client.deviceStatusCallback = myStatusCallback
client.subscribeToDeviceStstus()
```


## Publication des événements à partir de terminaux
{: #publishing_device_events}

Les applications peuvent publier des événements comme s'ils provenaient d'un terminal.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent(myDeviceType, myDeviceId, "status", "json", myData)
```


## Publication de commandes sur des terminaux
{: #publishing_commands_devices}


Les applications peuvent publier des commandes sur des terminaux connectés.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
commandData={'rebootDelay' : 50}
client.publishCommand(myDeviceType, myDeviceId, "reboot", "json", commandData)
```


## Informations concernant l'organisation
{: #org_details}

Les applications peuvent utiliser la méthode `getOrganizationDetails()` pour extraire les détails sur la configuration de l'organisation.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    orgDetail = client.api.getOrganizationDetails()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

Pour plus d'informations sur le modèle de demande et de réponse et les codes de statut HTTP, voir la section Organization Configuration dans la documentation de l'[API {{site.data.keyword.iot_short_notm}}![](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html).


## Opérations globales sur les terminaux
{: #bulk_device_ops}

Vos applications peuvent utiliser des opérations globales pour obtenir, ajouter ou retirer plusieurs terminaux simultanément.

Pour plus d'informations sur la liste de paramètres de requête, le modèle de réponse et de demande et les codes de statut HTTP, voir la section Bulk Operations dans la documentation de l'[API {{site.data.keyword.iot_short_notm}}![](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Bulk_Operations/).


### Extraction d'informations sur les terminaux

Les informations sur les terminaux peuvent être extraits à l'aide de la méthode `getAllDevices()`. Cette méthode permet d'extraire des informations sur tous les terminaux enregistrés dans l'organisation. Chaque demande peut contenir 512 Ko au maximum.

La réponse contient des paramètres qui sont requis par l'application. Utilisez les résultats de dictionnaire de la réponse pour obtenir le tableau de terminaux renvoyé. D'autres paramètres contenus dans la réponse sont nécessaires pour effectuer d'autres appels, par exemple, l'élément `_bookmark` peut être utilisé pour parcourir les pages de résultats. Soumettez la première demande sans spécifier de signet, puis récupérez le signet qui est renvoyé dans la réponse et indiquez-le dans la demande relative à la page suivante. Répétez cette opération jusqu'à la fin de l'ensemble de résultats, signalé par l'absence de signet. Chaque demande doit utiliser les mêmes valeurs pour les autres paramètres, sinon, les résultats seront non définis.


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceList = client.api.getAllDevices()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```
### Ajout de plusieurs terminaux


Utilisez la méthode `addMultipleDevices()` pour ajouter un ou plusieurs terminaux à votre organisation {{site.data.keyword.iot_short_notm}}. Une demande ne peut pas être supérieure à 512 ko. La réponse contient les jetons d'authentification qui ont été générés pour chaque terminal. Prenez soin d'effectuer une copie des jetons d'authentification car si vous les perdez, vous ne pouvez pas les récupérer.


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  listOfDevicesToAdd = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
  deviceList = client.api.addMultipleDevices(listOfDevicesToAdd)
except IoTFCReSTException as e:
  print("ERROR [" + e.httpcode + "] " + e.message)
```

### Suppression de plusieurs terminaux


Utilisez la méthode `deleteMultipleDevices()` pour supprimer plusieurs terminaux sur une organisation {{site.data.keyword.iot_short_notm}}. Une demande ne peut pas être supérieure à 512 ko.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  listOfDevicesToDelete = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
      deviceList = client.api.deleteMultipleDevices(listOfDevicesToDelete)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```


## Opérations relatives aux types de terminaux
{: #device_type_ops}

Les types de terminal que vous créez dans votre organisation peuvent être utilisés pour créer des modèles destinés à l'ajout de terminaux. En utilisant les fonctions API de {{site.data.keyword.iot_short_notm}}, vos applications peuvent répertorier, créer, supprimer, afficher ou mettre à jour des types de terminal dans votre organisation.

Pour plus d'informations sur les paramètres de requête, le modèle de demande et de réponse et les codes de statut HTTP, voir la section Device types dans la documentation de l'[API {{site.data.keyword.iot_short_notm}}![](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html).  


### Extraction de tous les types de terminal

Utilisez la méthode `getAllDeviceTypes()` pour extraire tous les types de terminal que compte votre organisation {{site.data.keyword.iot_short_notm}}.
Utilisez les résultats de dictionnaire de la réponse pour obtenir le tableau de terminaux renvoyé. D'autres paramètres contenus dans la réponse sont nécessaires pour effectuer d'autres appels, par exemple, l'élément `_bookmark` peut être utilisé pour parcourir les pages de résultats. Soumettez la première demande sans spécifier de signet, puis récupérez le signet qui est renvoyé dans la réponse et indiquez-le dans la demande relative à la page suivante. Répétez cette opération jusqu'à la fin de l'ensemble de résultats, signalé par l'absence de signet. Chaque demande doit utiliser les mêmes valeurs pour les autres paramètres, sinon, les résultats seront non définis.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

 listOfDevicesToAdd = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
   options = {'_limit' : 2}
   deviceTypeList = client.api.getAllDeviceTypes(options)
except IoTFCReSTException as e:
   print("ERROR [" + e.httpcode + "] " + e.message)

```

### Ajout d'un type de terminal

Utilisez la méthode `addDeviceType()` pour enregistrer un type de terminal sur votre instance {{site.data.keyword.iot_short_notm}}. Dans chaque demande, vous devez d'abord définir les informations sur le terminal et les éléments de métadonnées de terminal à appliquer à tous les terminaux de ce type. L'élément d'informations sur le terminal se compose de plusieurs variables, tels que le numéro de série, le fabricant, le modèle, la classe, la description, le microprogramme, les versions de matériel et l'emplacement descriptif. L'élément de métadonnées se compose de variables et de valeurs personnalisées, qui peuvent être définies par l'utilisateur.


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  info = {
      "serialNumber": "100087",
      "manufacturer": "ACME Co.",
      "model": "7865",
      "deviceClass": "A",
      "description": "My shiny device",
      "fwVersion": "1.0.0",
      "hwVersion": "1.0",
      "descriptiveLocation": "Office 5, D Block"
  }
  meta = {
      "customField1": "customValue1",
      "customField2": "customValue2"
  }

try:
      deviceType = client.api.addDeviceType(deviceType = "myDeviceType", description = "My first device type", deviceInfo = info, metadata = meta)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```

### Suppression d'un type de terminal


Utilisez la méthode `deleteDeviceType()` pour supprimer un type de terminal de votre organisation {{site.data.keyword.iot_short_notm}}.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
      success = client.api.deleteDeviceType("myDeviceType")
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```

### Extraction d'informations pour certains types de terminal


Utilisez la méthode `getDeviceType()` afin d'extraire des informations pour un certain type de terminal. L'élément `typeId` du type de terminal que vous souhaitez extraire doit être spécifié en tant que paramètre.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceTypeInfo = client.api.getDeviceType("myDeviceType")
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

### Mise à jour d'un type de terminal


Utilisez la méthode `updateDeviceType()` pour modifier les propriétés d'un type de terminal. Lorsque vous utilisez la méthode `updateDeviceType()`, spécifiez d'abord l'élément `typeId` du type de terminal à mettre à jour, puis indiquez les éléments suivants :

- `description`
- `deviceInfo`
- `metadata`

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  info = {
      "serialNumber": "100087",
      "manufacturer": "ACME Co.",
      "model": "7865",
      "deviceClass": "A",
      "description": "My shiny device",
      "fwVersion": "1.0.0",
      "hwVersion": "1.0",
      "descriptiveLocation": "Office 5, D Block"
  }
  meta = {
      "customField1": "customValue1",
      "customField2": "customValue2",
      "customField3": "customValue3"
  }

try:
      updatedDeviceTypeInfo = client.api.updateDeviceType("myDeviceType", "New description", deviceInfo, metadata)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```


## Opérations relatives aux terminaux
{: #device_ops}

Les opérations relatives aux terminaux disponibles dans l'API incluent le recensement, l'ajout, le retrait, l'affichage, la mise à jour, la visualisation de l'emplacement et la visualisation des informations de gestion des terminaux dans une organisation {{site.data.keyword.iot_short_notm}}.

Pour plus d'informations sur les paramètres de requête, le modèle de demande et de réponse et les codes de statut HTTP, voir la section Device section dans la documentation de l'[API {{site.data.keyword.iot_short_notm}} ![](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html).


### Extraction de terminaux d'un type donné

Utilisez la méthode `retrieveDevices()` pour extraire tous les terminaux d'un type donné d'une organisation dans une instance {{site.data.keyword.iot_short_notm}}, illustrée dans l'exemple suivant :


```python

   print("\nRetrieving All existing devices")
   print("Retrieved Devices = ", apiCli.retrieveDevices(deviceTypeId))
```

Utilisez les résultats de dictionnaire de la réponse pour obtenir le tableau de terminaux renvoyé. D'autres paramètres contenus dans la réponse sont nécessaires pour effectuer d'autres appels, par exemple, l'élément *_bookmark* peut être utilisé pour parcourir les pages de résultats. Soumettez la première demande sans spécifier de signet, puis récupérez le signet qui est renvoyé dans la réponse et indiquez-le dans la demande relative à la page suivante. Répétez cette opération jusqu'à la fin de l'ensemble de résultats, signalé par l'absence de signet. Chaque demande doit utiliser les mêmes valeurs pour les autres paramètres, sinon, les résultats seront non définis.

Pour transmettre l'élément *_bookmark* ou n'importe quelle autre condition, vous devez utiliser la méthode surchargée. Cette dernière prend les paramètres sous la forme d'un dictionnaire, comme illustré dans l'exemple suivant :

```python
response = apiClient.retrieveDevices("iotsample-arduino", parameters);
```

L'exemple de code précédent trie la réponse en fonction de l'ID de terminal, puis utilise le signet pour parcourir les pages de résultats.

### Ajout d'un terminal


Pour ajouter un terminal à une organisation {{site.data.keyword.iot_short_notm}}, utilisez la méthode `registerDevice()`. La méthode `registerDevice()` ajoute un terminal à votre organisation {{site.data.keyword.iot_short_notm}}. Lorsque vous ajoutez un terminal, vous pouvez définir les paramètres suivants :

|Paramètre|Exigence|Description
|:---|:---|
|`deviceTypeId`|Facultatif|Affecte un type de terminal au terminal. En cas de conflit entre les variables définies par le type de terminal et celles définies par la variable `deviceInfo`, les variables spécifiques du terminal sont prioritaires.|
|`deviceId`|Obligatoire||
|`authToken`|Facultatif|Si ce paramètre n'est pas défini, un jeton d'authentification est généré et inclus dans la réponse.|
|`deviceInfo`|Facultatif|Contient plusieurs variables, notamment le numéro de série, le fabricant, le modèle, la classe de terminaux, la description, l'emplacement descriptif, le microprogramme et les versions de matériel.|
|`metadata`|Facultatif|Paires de chaînes personnalisées zone:valeur, comme indiqué dans [Exemple de code pour l'ajout d'un type de terminal](#sample_device_type).|
|`location`|Facultatif|Contient les variables longitude, latitude, elevation, accuracy et measuredDateTime.|

Pour plus d'informations sur ces paramètres et le format et les codes de réponse, voir la [documentation de l'API![](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Devices/post_device_types_typeId_devices).

Lorsque vous utilisez la méthode `registerDevice()`, définissez le paramètre deviceID obligatoire, ainsi que les paramètres facultatifs requis pour votre terminal, puis appelez la méthode à l'aide des paramètres que vous avez sélectionnés.

### Exemple de code pour l'ajout d'un type de terminal
{: #sample_device_type}

Insérez le code suivant après le code du constructeur dans un fichier script Python(.py). L'exemple illustre une méthode permettant d'ajouter un type de  terminal en définissant les paramètres deviceId, authToken, metadata, deviceInfo et location.

```python

deviceId = "200020002000"
authToken = "password"
metadata = {"customField1": "customValue1", "customField2": "customValue2"}
deviceInfo = {"serialNumber": "001", "manufacturer": "Blueberry", "model": "abc1", "deviceClass": "A", "descriptiveLocation" : "Bangalore", "fwVersion" : "1.0.1", "hwVersion" : "12.01"}
location = {"longitude" : "12.78", "latitude" : "45.90", "elevation" : "2000", "accuracy" : "0", "measuredDateTime" : "2015-10-28T08:45:11.662Z"}

apiCli.registerDevice(deviceTypeId, deviceId, metadata, deviceInfo, location)
```
### Suppression d'un terminal

Utilisez la méthode `deleteDevice()` pour retirer un terminal d'une organisation sur l'organisation {{site.data.keyword.iot_short_notm}}. Lorsque vous supprimez un terminal en utilisant la méthode `deleteDevice()`, vous devez spécifier les paramètres deviceTypeId et deviceId.

L'exemple de code suivant présente le format requis pour cette méthode :

```python
apiCli.deleteDevice(deviceTypeId, deviceId)
```

### Extraction d'un terminal

Utilisez la méthode `getDevice()` pour extraire un terminal d'une organisation sur {{site.data.keyword.iot_short_notm}}. Lorsque vous extrayez les détails d'un termina en utilisant la méthode `getDevice()`, vous devez spécifier les paramètres deviceTypeId et deviceId.

L'exemple de code suivant présente le format requis pour cette méthode.

```python
apiCli.getDevice(deviceTypeId, deviceId)
```

### Extraction de tous les terminaux

Utilisez la méthode `getAllDevices()` pour extraire tous les terminaux d'une organisation sur {{site.data.keyword.iot_short_notm}}.

```python
apiCli.getAllDevices({'typeId' : deviceTypeId})
```

### Mise à jour d'un terminal

Pour modifier une ou plusieurs propriétés d'un terminal, utilisez la méthode `updateDevice()`.

Vous pouvez mettre à jour n'importe quelle propriété dans les paramètres deviceInfo ou metadata. Pour mettre à jour une propriété de terminal, définissez le paramètre deviceInfo avant d'appeler la méthode `updateDevice()`. Le paramètre status doit contenir `alert`: True. La propriété d'alerte détermine si un terminal affiche des codes d'erreur dans l'interface utilisateur de {{site.data.keyword.iot_short_notm}} et doit prendre par défaut la valeur `enabled`: True, comme indiqué dans l'exemple de code suivant :

```python
status = { "alert": { "enabled": True }  }
apiCli.updateDevice(deviceTypeId, deviceId, metadata2, deviceInfo, status)
```

### Exemple de code pour la mise à jour des propriétés du paramètre deviceInfo

L'exemple de code suivant identifie un terminal donné, puis met à jour plusieurs propriétés du paramètres deviceInfo.

```python
status = { "alert": { "enabled": True } }
deviceInfo = {descriptiveLocation: "London", hwVersion: "2.0.1", fwVersion: "2.5.1"}
apiCli.updateDevice("MyDeviceType", "200020002000", deviceInfo, status)
```

### Extraction d'informations d'emplacement


Utilisez la méthode `getDeviceLocation()` pour extraire les informations d'emplacement d'un terminal. Les paramètres requis pour l'extraction des données d'emplacement sont deviceTypeId et deviceId.

```python
apiClient.getDeviceLocation("iotsample-arduino", "arduino01")
```  

La réponse à cette méthode inclut les propriétés longitude, latitude, elevation, accuracy, measuredTimeStamp et updatedTimeStamp.

### Mise à jour des informations d'emplacement


Utilisez la méthode `updateDeviceLocation()` afin de modifier les informations d'emplacement pour un terminal. Comme pour la mise à jour des propriétés de terminal, le paramètre deviceLocation doit être défini avec les modifications que vous souhaitez appliquer. L'exemple de code suivant montre comment modifier les données d'emplacement pour un terminal donné :

```python
deviceLocation = { "longitude": 0, "latitude": 0, "elevation": 0, "accuracy": 0, "measuredDateTime": "2015-10-28T08:45:11.673Z"}
apiCli.updateDeviceLocation(deviceTypeId, deviceId, deviceLocation)
```

Si une date n'est pas fournie, la date du jour et l'heure en cours sont utilisées.


### Obtention d'informations de gestion


Utilisez la méthode `getDeviceManagementInformation()` pour obtenir les informations de gestion des terminaux pour un terminal. La réponse contient la date et l'heure de la dernière activité, le statut de veille du terminal (True/False), la prise en charge des actions sur les terminaux et le microprogramme et les données de microprogramme. Pour obtenir une liste complète du contenu de réponse, voir la documentation d'API appropriée.

L'exemple de code suivant renvoie les informations de gestion des terminaux pour un terminal dont le paramètre deviceId a pour valeur "00aabbccde03" et le paramètre deviceTypeId a pour valeur "iotsample-arduino" :

```
apiCli.getDeviceManagementInformation("iotsample-arduino", "00aabbccde03")
```

## Opérations de diagnostic d'un terminal
{: #device_diag_ops}

Utilisez les opérations de diagnostic d'un terminal pour implémenter les tâches de gestion de journal et d'identification et de résolution des problèmes décrites ci-dessous :
- Effacement des journaux
- Extraction de l'ensemble ou de certains des journaux d'un terminal
- Ajout d'informations de journal
- Suppression de journaux
- Effacement de codes d'erreur
- Extraction de codes d'erreur de terminaux
- Ajout de codes d'erreur

Pour plus d'informations sur les modèles de requête et de réponse, les codes de réponse et les paramètres de requête, voir la [documentation de l'API![](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html) {{site.data.keyword.iot_short_notm}}. 

### Extraction de journaux de diagnostic


Utilisez la méthode `getAllDiagnosticLogs()` pour extraire tous les journaux de diagnostic pour un terminal donné. La méthode `getAllDiagnosticLogs()` requiert les paramètres deviceTypeId et deviceId.

```python
apiCli.getAllDiagnosticLogs(deviceTypeId, deviceId)
```

Le modèle de réponse pour cette réponse contient les propriétés d'ID de journal, de message, de gravité, de données et d'horodatage.

### Effacement des journaux de diagnostic d'un terminal


Utilisez la méthode `clearAllDiagnosticLogs()` pour supprimer tous les journaux de diagnostic pour un terminal donné* Les paramètres obligatoires sont deviceTypeId et deviceId. Soyez prudent lorsque vous supprimez des fichiers journaux, car ils ne peuvent pas être récupérés une fois qu'ils ont été supprimés.

```python
apiCli.clearAllDiagnosticLogs(deviceTypeId, deviceId)
```

### Ajout d'un journal de diagnostic


Utilisez la méthode `addDiagnosticLog()` pour ajouter une entrée dans le journal de diagnostic du terminal. Le journal peut être élagué lorsque la nouvelle entrée est ajoutée. Si une date n'est pas fournie, la date du jour et l'heure en cours sont ajoutées à l'entrée. Pour utiliser cette méthode, vous devez définir un paramètre 'logs' avec les variables suivantes :


|Variable|Exigence|Description|
|:---|:---|:---|
|`message`|Obligatoire|Contient le message de diagnostic que vous souhaitez ajouter|
|`severity`|Facultatif|Correspond à la gravité du journal de diagnostic et peut prendre la valeur 0, 1 ou 2, correspondant aux catégories d'informations, d'avertissement et d'erreur|
|`data`|Facultatif|Contient des données de diagnostic|
|`timestamp`|Facultatif|Contient la date et l'heure de l'entrée de journal au format ISO8601. Si cette variable n'est pas définie, la date du jour et l'heure en cours sont utilisées|


Les autres paramètres requis dans la méthode sont les valeurs deviceTypeId et deviceId pour le terminal.

L'exemple de code suivant contient un exemple de la méthode `addDiagnosticLog()` :

```python
logs = { "message": "MessageContent", "severity": 0, "data": "LogData"}
apiCli.addDiagnosticLog(deviceTypeId, deviceId, logs)
```

### Extraction d'un journal de diagnostic donné


Utilisez la méthode `getDiagnosticLog()` pour extraire un journal de diagnostic pour un terminal spécifié en fonction de l'ID de journal. Les paramètres requis pour cette méthode sont deviceTypeId, deviceId et logId.

```python
apiCli.getDiagnosticLog(deviceTypeId, deviceId, logId)
```

### Suppression d'un journal de diagnostic


Utilisez la méthode `deleteDiagnosticLog()` pour supprimer un journal de diagnostic donné. Pour spécifier un journal de diagnostic, les paramètres deviceTypeId, deviceId et logID doivent être fournis.

```python
apiCli.deleteDiagnosticLog(deviceTypeId, deviceId, logId)
```

### Extraction de codes d'erreur de terminaux


Utilisez la méthode `getAllDiagnosticErrorCodes()` pour extraire tous les codes d'erreur de diagnostic qui sont associés à un terminal donné.

```python
apiCli.getAllDiagnosticErrorCodes(deviceTypeId, deviceId)
```

### Effacement des codes d'erreur de diagnostic


Utilisez la méthode `clearAllErrorCodes()` pour effacer la liste de codes d'erreur qui sont associés au terminal. La liste est remplacée par le code d'erreur unique 0.

```python
apiCli.clearAllErrorCodes(deviceTypeId, deviceId)
```

### Ajout d'un code d'erreur de diagnostic


Utilisez la méthode `addErrorCode()` pour ajouter un code d'erreur à la liste de codes d'erreur qui sont associés au terminal. La liste peut être élaguée lorsque la nouvelle entrée est ajoutée. Les paramètres requis dans la méthode sont deviceTypeId, deviceId et errorCode. Le paramètre errorCode contient les variables suivantes :

- errorCode : Cette variable est obligatoire et doit correspondre à un entier. Cette variable définit le numéro du code d'erreur qui est créé.
- timestamp : Cette variable est facultative et contient la date et l'heure de l'entrée de journal au format ISO8601. Si cette variable n'est pas incluse, elle est ajoutée automatiquement avec la date et l'heure en cours.

```python
errorCode = { "errorCode": 1234, "timestamp": "2015-10-29T05:43:57.112Z" }
apiCli.addErrorCode(deviceTypeId, deviceId, errorCode)
```

## Identification d'un problème de connexion
{: #connection_problem_determination}

Utilisez la méthode `getDeviceConnectionLogs()` pour obtenir la liste des événements de journal de connexion pour un terminal. Les événements de journal de connexion peuvent être utilisés pour diagnostiquer des problèmes de connectivité entre le terminal et le service {{site.data.keyword.iot_short_notm}}. Les entrées enregistrent des événements de connexion ayant abouti, de tentatives de connexion ayant échoué, de déconnexion volontaire et de déconnexion à l'initiative du serveur.

```
apiCli.getDeviceConnectionLogs(deviceTypeId, deviceId)
```

La réponse inclut une liste d'entrées de journal contenant des messages de journal et des horodatages.
