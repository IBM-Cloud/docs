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


# C# pour les développeurs d'applications
{: #c_sharp}


Vous pouvez utiliser C# pour générer et personnaliser des applications qui interagissent avec votre organisation sur {{site.data.keyword.iot_full}}. Utilisez les informations et les exemples fournis pour commencer à développer vos applications en utilisant C#.
{:shortdesc}

## Téléchargement du client et des ressources C#
{: #csharp_client_download}

Pour accéder aux bibliothèques et exemples client C# pour {{site.data.keyword.iot_short_notm}}, accédez au référentiel [iot-csharp ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-csharp){: new_window} dans GitHub et exécutez les instructions d'installation.


## Constructeur
{: #constructor}

Le constructeur génère l'instance client et accepte des arguments contenant les définitions suivantes :

|Définition |Description |
|:---|:---|
|`orgId`   |ID de votre organisation.|
|`appId`   |ID unique d'une application au sein de votre organisation.|
|`auth-key`   |Clé d'API permettant d'établir une connexion sécurisée entre votre application et Watson IoT Platform.|
|`auth-token`   |Jeton de clé d'API permettant d'établir une connexion sécurisée entre votre application et Watson IoT Platform.|

Si `appId` est le seul argument fourni, le client se connecte au service {{site.data.keyword.iot_short_notm}} Quickstart en tant que terminal non enregistré. La liste d'arguments définit la manière dont le client se connecte au module {{site.data.keyword.iot_short_notm}}.

```
ApplicationClient applicationClient = new ApplicationClient(orgId, appId, apiKey, authToken);  
applicationClient.connect();
```


## Abonnement aux événements d'un terminal
{: #subscribe_device_events}

Les terminaux utilisent des événements pour publier des données sur l'instance {{site.data.keyword.iot_short_notm}}. Le terminal contrôle le contenu de l'événement et affecte un nom à chaque événement qu'il envoie.

Lorsqu'un événement est reçu par l'instance {{site.data.keyword.iot_short_notm}}, les données d'identification de l'événement reçu identifient le terminal qui a envoyé l'événement, ce qui signifie qu'un terminal ne peut pas simuler les droits d'accès d'un autre terminal.

Par défaut, les applications s'abonnent à tous les événements depuis tous les terminaux connectés. Utilisez les paramètres de type de terminal, d'ID de terminal, d'événement et de format de message pour contrôler la portée de l'abonnement. Les exemples de code suivants vous montrent comment définir la portée d'un abonnement à l'aide de ces paramètres :

### Abonnement à tous les événements depuis tous les terminaux

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents();
```

### Abonnement à tous les événements depuis tous les terminaux d'un type donné

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType);
```

### Abonnement à un événement spécifique depuis tous les terminaux

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(evt);
```

###  Abonnement à un événement spécifique depuis au moins deux terminaux différents :

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt);
```

### Abonnement à tous les événements publiés au format JSON

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt, "json", 0);
```

**Remarque** : Une instance client unique peut prendre en charge plusieurs abonnements.

### Traitement des événements provenant des terminaux

Pour traiter les événements reçus par vos abonnements, enregistrez une méthode de rappel d'événement, comme illustré dans l'exemple suivant :

```
public static void processEvent(String eventName, string eventFormat, string eventData) {
// Do something
}
applicationClient.connect();
applicationClient.eventCallback += processEvent;
applicationClient.subscribeToDeviceEvents();
```
Le tableau suivant décrit les paramètres de la méthode de rappel d'événement :

|Paramètre|Type de données|Description|
|:---|:---|
|`eventName`|Chaîne|Identifie l'événement. |
|`eventFormat`|Chaîne| Le format peut être n'importe quelle chaîne, par exemple, JSON.|
|`eventData`|Dictionnaire| Données du contenu du message. La longueur maximale est de 131072 octets.|


## Abonnement au statut des terminaux
{: #subscribe_device_status}

Par défaut, cet abonnement est défini pour recevoir les mises à jour de statut pour tous les terminaux connectés. Utilisez les paramètres de type et d'ID de terminal pour contrôler la portée de l'abonnement. Les exemples de code suivants vous montrent comment définir la portée d'un abonnement à l'aide de ces paramètres :

### Abonnement aux mises à jour de statut pour tous les terminaux

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus();
```

### Abonnement aux mises à jour de statut pour deux terminaux différents

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus(deviceType, deviceId);
```

**Remarque** : Une instance client unique peut prendre en charge plusieurs abonnements.

### Traitement des mises à jour du statut des terminaux

Pour traiter les mises à jour de statut reçues par vos abonnements, enregistrez une méthode de rappel d'événement, comme illustré dans l'exemple suivant :

```
public static void processDeviceStatus(String deviceType, string deviceId, string data)
        {
           //
        }
applicationClient.connect();
applicationClient.appStatusCallback += processAppStatus;
applicationClient.subscribeToApplicationStatus();
```

## Publication des événements à partir de terminaux
{: #publish_events_devices}

Les applications peuvent publier des événements comme s'ils provenaient d'un terminal.

```
applicationClient.connect();
applicationClient.publishEvent(deviceType, deviceId, evt, data, 0);

```

Le tableau suivant décrit les paramètres spécifiés dans la méthode `publishEvent()` :

|Paramètre|Type de données|Description|
|:---|:---|
|`deviceType`|Chaîne| Type de terminal. Généralement, deviceType regroupe des terminaux qui effectuent une tâche spécifique, par exemple, "weatherballoon".|
|`deviceId`|Chaîne| ID du terminal. Généralement, pour un type de terminal donné, deviceId est un identificateur unique, par exemple, un numéro de série ou une adresse MAC.|
|`evt`|Chaîne| Nom de l'événement.|
|`format`|Chaîne| Le format peut être n'importe quelle chaîne, par exemple, JSON.|
|`data`|Dictionnaire| Données du contenu du message. La longueur maximale est de 131072 octets.|
|`QoS`|Entier| Qualité de service. Les valeurs valides sont `0`, `1`, `2`. |


## Publication de commandes sur des terminaux
{: #publish_commands_devices}

Les applications peuvent publier des commandes sur des terminaux connectés.

```
applicationClient.connect();
applicationClient.publishCommand(deviceType, deviceId, "testcmd", "json", data, 0);
```
Le tableau suivant décrit les paramètres spécifiés dans la méthode `publishCommand()` :

|Paramètre|Type de données|Description|
|:---|:---|
|`deviceType`|Chaîne| Type de terminal. Généralement, deviceType regroupe des terminaux qui effectuent une tâche spécifique, par exemple, "weatherballoon".|
|`deviceId`|Chaîne| ID du terminal. Généralement, pour un type de terminal donné, deviceId est un identificateur unique, par exemple, un numéro de série ou une adresse MAC.|
|`command`|Chaîne| Nom de la commande.|
|`format`|Chaîne| Le format peut être n'importe quelle chaîne, par exemple, JSON.|
|`data`|Dictionnaire| Données du contenu du message. La longueur maximale est de 131072 octets.|
|`QoS`|Entier| Qualité de service. Les valeurs valides sont `0`, `1`, `2`. |
