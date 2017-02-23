---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-08-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# C# pour les développeurs de terminaux
{: #c_sharp}

Vous pouvez utiliser C# pour générer et personnaliser des terminaux qui interagissent avec votre organisation sur {{site.data.keyword.iot_full}}. Utilisez les informations et les exemples fournis pour commencer à développer vos terminaux à l'aide de C#.
{:shortdesc}

## Téléchargement du client et des ressources C#
{: #csharp_client_download}

Pour accéder au client et aux ressources C# pour {{site.data.keyword.iot_short_notm}}, accédez au référentiel [iot-csharp](https://github.com/ibm-watson-iot/iot-csharp) dans GitHub et exécutez les instructions d'installation.


## Constructeur
{: #constructor}

Le constructeur génère l'instance client et accepte des arguments contenant les définitions suivantes :

|Définition |Description |
|:---|:---|
|`orgId`|ID de votre organisation.|
|`deviceType`|Type de votre terminal.|
|`deviceId` |ID de votre terminal.|
|`auth-method`   |Méthode d'authentification à utiliser. La seule valeur actuellement prise en charge est `token`.|
|`auth-token`   |Jeton d'authentification permettant d'établir une connexion sécurisée entre votre terminal et Watson IoT Platform.|


Si `deviceId` et `deviceType` sont les seuls arguments fournis, le client se connecte au service Quickstart de {{site.data.keyword.iot_short_notm}} en tant que terminal non enregistré. La liste d'arguments définit la manière dont le client se connecte au module {{site.data.keyword.iot_short_notm}}.


```
namespace com.ibm.iotf.client

public DeviceClient(string orgId, string deviceType, string deviceID, string auth-method, string auth-token)
        : base(orgId, "d" + CLIENT_ID_DELIMITER + orgId + CLIENT_ID_DELIMITER + deviceType + CLIENT_ID_DELIMITER + deviceID, "use-token-auth", auth-token)
    {

    }
```

## Publication d'événements
{: #publishing-events}

Les terminaux utilisent des événements pour publier des données sur l'instance {{site.data.keyword.iot_short_notm}}. Le terminal contrôle le contenu de l'événement et affecte un nom à chaque événement qu'il envoie.

Lorsqu'un événement est reçu par l'instance {{site.data.keyword.iot_short_notm}}, les données d'identification de l'événement entrant identifient le terminal qui a envoyé l'événement, ce qui signifie qu'un terminal ne peut pas simuler les droits d'accès d'un autre terminal.

Les événements peuvent être publiés avec n'importe lequel des trois [niveaux de qualité de service (QoS)](../mqtt.html#managed-devices) définis par le protocole MQTT. Par défaut, les événements sont publiés avec le niveau QoS 0.


## Publication d'un événement à l'aide du niveau de qualité de service par défaut
{: #publish_event_default_qos}

```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}");
```


## Publication d'un événement à l'aide d'un niveau de qualité de service défini par l'utilisateur
{: #publish_event_user_qos}

La publication des événements dont le niveau QoS est supérieur à `0` peut prendre plus de temps, en raison des informations de réception de confirmation supplémentaires qui sont incluses.


```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}", 2);
```

## Traitement des commandes
{: #handling_commands}

Lorsque le client du terminal se connecte, il s'abonne automatiquement aux commandes de ce terminal. Pour traiter des commandes spécifiques, vous devez enregistrer une méthode de rappel de commande, comme illustré dans l'exemple suivant :

```
public static void processCommand(string cmdName, string cmdFormat, string cmdData) {
...
 }
```

```
deviceClient.connect();
deviceClient.commandCallback += processCommand;
```
Le tableau suivant décrit les paramètres de la méthode commandCallback :

|Paramètre|Type de données|Description|
|:---|:---|
|`cmdName`|Chaîne|Identifie la commande. |
|`cmdFormat`|Chaîne|Le format peut être n'importe quelle chaîne, par exemple, JSON.|
|`cmdData`|Dictionnaire|Données du contenu. La longueur maximale est de 131072 octets.|
