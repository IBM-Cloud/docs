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


# mBed C++ pour les développeurs de terminaux
{: #mbedcpp}

Utilisez la [bibliothèque client mBed C++ ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/){: new_window} pour connecter facilement des [terminaux mBed ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://www.mbed.com/en/){: new_window}, tels que [LPC1768](https://developer.mbed.org/platforms/mbed-LPC1768/) ou[FRDM-K64F ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.mbed.org/platforms/FRDM-K64F/){: new_window}, au service {{site.data.keyword.iot_full}}.
{:shortdesc}

Pour plus d'informations, voir [ibmiotf ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/){: new_window} sur [developer.mbed.org ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.mbed.org/){: new_window}.

Bien que la bibliothèque utilise C++, elle évite les allocations de mémoire dynamiques et l'utilisation de fonctions STL car les terminaux mBed incluent parfois des modèles de mémoire idiosyncratiques qui rendent le portage difficile. Dans tous les cas, la bibliothèque permet de rendre l'utilisation de la mémoire aussi prévisible que possible.

## Dépendances
{: #dependencies}

|Dépendance |Description|
|:---|:---|
|[Bibliothèque Eclipse Paho MQTT ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.mbed.org/teams/mqtt/code/MQTT/){: new_window}|Fournit une bibliothèque client MQTT pour les terminaux mBed. Pour plus d'informations, voir [Embedded MQTT C/C++ Client Libraries ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](http://www.eclipse.org/paho/clients/c/embedded/){: new_window}|
|[EthernetInterface Library ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.mbed.org/users/mbed_official/code/EthernetInterface/){: new_window}|Bibliothèque IP mBed via Ethernet.|

## Comment utiliser la bibliothèque
{: #library_use}

Utilisez le [compilateur mBed ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.mbed.org/compiler/){: new_window} pour créer vos applications lorsque vous utilisez la bibliothèque client mBed C++ IBMIoTF. Le compilateur mBed fournit un environnement de développement intégré C/C++ en ligne, qui est configuré pour vous permettre d'écrire, de compiler et de télécharger des programmes à exécuter sur le microcontrôleur mbed.

**Remarque :** Vous n'avez rien à installer ni à configurer pour commencer à utiliser mbed.

Pour plus d'informations sur la connexion d'un microcontrôleur ARM mBed NXP LPC 1768 à {{site.data.keyword.iot_short_notm}}, voir la recette[mBed C++ client library for IBM Watson IoT Platform ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/mbed-c-client-library-for-ibm-iot-foundation/){: new_window}.

## Constructeur
{: #constructor}

Le constructeur génère l'instance client et accepte les paramètres suivants :

|Paramètre |Description |
|:---|:---|
|`org` |ID de votre organisation. Cette valeur est obligatoire. Si vous utilisez un flux Quickstart, spécifiez `quickstart`.|
|`type`   |Type de votre terminal. Cette zone est obligatoire.|
|`id`   |ID de votre terminal. Cette zone est obligatoire.|
|`auth-method`   |Méthode d'authentification. Cette zone facultative n'est requise que pour un flux enregistré. La seule valeur actuellement prise en charge est `token`.|
|`auth-token`   |Jeton d'authentification permettant d'établir une connexion sécurisée entre votre terminal et Watson IoT Platform. Zone facultative qui n'est requise que pour un flux enregistré.|

Ces paramètres créent des définitions utilisées pour interagir avec le service {{site.data.keyword.iot_short_notm}}.

L'exemple de code suivant montre comment une instance DeviceClient peut interagir avec le service {{site.data.keyword.iot_short_notm}} Quickstart :

```
  #include "DeviceClient.h"
  ....
  ....

  // Set {{site.data.keyword.iot_short_notm}} connection parameters
  char organization[11] = "quickstart";     // For a registered connection, replace with your org
  char deviceType[8] = "LPC1768";           // For a registered connection, replace with your device type
  char deviceId[3] = "01";                  // For a registered connection, replace with your device id

  // Create DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId);

  // Get the DeviceID(MAC Address) if we are in quickstart mode and device ID is not specified
  if((strcmp(organization, QUICKSTART) == 0) && (strcmp("", deviceId) == 0))
  {
  	char tmpBuf[50];
  	client.getDeviceId(tmpBuf, sizeof(tmpBuf));
  }
  ....
```

Comme illustré dans l'exemple de code précédent, si l'ID de terminal n'est pas spécifié, l'instance DeviceClient utilise l'adresse MAC du terminal comme ID de terminal pour se connecter à {{site.data.keyword.iot_short_notm}}. Le code de terminal peut utiliser la méthode `getDeviceId()` pour extraire l'ID de terminal de l'instance DeviceClient.

Le bloc de code suivant montre comment créer une instance DeviceClient pour interagir avec l'organisation enregistrée {{site.data.keyword.iot_short_notm}}.

```
  #include "DeviceClient.h"
  ....
  ....

  // Set {{site.data.keyword.iot_short_notm}} connection parameters
  char organization[11] = "hrcl78";
  char deviceType[8] = "LPC1768";
  char deviceId[3] = "LPC176801";
  char method[6] = "token";
  char token[9] = "password";

  // Create DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId, method, token);
  ....
```

## Connexion à {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

Le terminal peut se connecter à {{site.data.keyword.iot_short_notm}} en appelant la fonction connect sur l'instance DeviceClient.

```
  #include "DeviceClient.h"
  ....
  ....

  // Create DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId, method, token);

  bool status = client.connect();

```
Une fois la connexion établie, le terminal peut publier des événements sur {{site.data.keyword.iot_short_notm}} et écouter des commandes.

En outre, le terminal peut interroger le statut de la connexion à l'aide de la méthode `isConnected()`, comme illustré ci-dessous :

```
  #include "DeviceClient.h"
  ....
  ....

  client.isConnected();

```


## Publication d'événements
{: #publishing_events}

Les événements constituent le mécanisme par lequel les terminaux publient des données sur {{site.data.keyword.iot_short_notm}}. Le terminal contrôle le contenu de l'événement et affecte un nom à chaque événement qu'il envoie.

Lorsqu'un événement est reçu par l'instance {{site.data.keyword.iot_short_notm}}, les données d'identification de l'événement reçu identifient le terminal qui a envoyé l'événement, ce qui signifie qu'un terminal ne peut pas simuler les droits d'accès d'un autre terminal.

Les événements peuvent être publiés avec n'importe lequel des trois [niveaux de qualité de service (QoS)](../../reference/mqtt/index.html#qos-levels) définis par le protocole MQTT. Par défaut, les événements sont publiés avec le niveau QoS 0.

### Publication d'événement à l'aide du niveau de qualité de service par défaut

L'exemple suivant montre comment publier les points de données suivants sur {{site.data.keyword.iot_short_notm}} au format JSON :

- LPC1768, par exemple, l'axe x,y et z,
- la position de la manette ou
- le relevé de température en cours

```
	boolean status = client.connect();

	// Create buffer to hold the event
	char buf[250];

	// Construct an event message with desired datapoints in JSON format
	sprintf(buf,
            "{\"d\":{\"myName\":\"IoT mbed\",\"accelX\":%0.4f,\"accelY\":%0.4f,\"accelZ\":%0.4f,
            \"temp\":%0.4f,\"joystick\":\"%s\",\"potentiometer1\":%0.4f,\"potentiometer2\":%0.4f}}",
            MMA.x(), MMA.y(), MMA.z(), sensor.temp(), joystickPos, ain1.read(), ain2.read());

        status = client.publishEvent("blink", buf);
	....
```
Pour afficher la totalité de l'exemple de code, voir l'exemple d'application [ IBMIoTClientLibrarySample ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp){: new_window}.

### Augmentation du niveau QoS pour un événement

Vous pouvez augmenter les [niveaux QoS](../../reference/mqtt/index.html#qos-levels) des événements qui sont publiés. La publication des événements dont le niveau QoS est supérieur à `0` peut prendre plus de temps, en raison des informations de réception de confirmation supplémentaires qui sont incluses.

**Remarque :** Le mode flux Quickstart ne prend en charge que le niveau QoS 0.

```
	#include "MQTTClient.h"

	boolean status = client.connect();

	// Create buffer to hold the event
	char buf[250];

	// Construct an event message with desired datapoints in JSON format
	sprintf(buf,
            "{\"d\":{\"myName\":\"IoT mbed\",\"accelX\":%0.4f,\"accelY\":%0.4f,\"accelZ\":%0.4f,
            \"temp\":%0.4f,\"joystick\":\"%s\",\"potentiometer1\":%0.4f,\"potentiometer2\":%0.4f}}",
            MMA.x(), MMA.y(), MMA.z(), sensor.temp(), joystickPos, ain1.read(), ain2.read());

        status = client.publishEvent("blink", buf, MQTT::QOS2);
	....
```

### Traitement de l'erreur de perte de connexion durant la publication d'événement


Lorsque la méthode `publishEvent()` renvoie la valeur false, vous pouvez vérifier le statut de la connexion et appeler `reConnect()` si la connexion est perdue.

```
	#include "MQTTClient.h"

	status = client.publishEvent("blink", buf, MQTT::QOS2);

	if(status == false) {
	    // Check if connection is lost and retry
	    while(!client.isConnected())
	    {
	        client.reConnect();
	        wait(5.0);
	    }
	}
	....
```
La bibliothèque ne stocke pas les événements publiés à l'état non connecté, par conséquent, le terminal doit rappeler la méthode `publishEvent()` pour pouvoir envoyer ces événements une fois la connexion réétablie.


## Traitement des commandes
{: #handling_commands}

Lorsque le client du terminal se connecte, il s'abonne automatiquement aux commandes de ce terminal. Pour traiter des commandes, vous devez enregistrer une méthode de rappel de commande.
Les messages sont renvoyés en tant qu'instance de la classe Command qui possède les propriétés suivantes :

|Propriété |Description|
|:---|:---|
|`command` | Nom de la commande qui a été appelée.|  
|`format`  |Format de l'événement. Le format peut être n'importe quelle chaîne, par exemple, JSON. |
|`payload`  |Données du contenu de la commande. La longueur maximale est de 131072 octets. |


Le code suivant définit un exemple de fonction de rappel de commande qui traite la commande de gestion de l'intervalle de clignotement d'un voyant provenant de l'application et définit la fonction ajoute handle de l'instance DeviceClient de sorte que la méthode de rappel soit exécutée chaque fois que l'instance reçoit la commande de gestion de l'intervalle.

```
    #include "DeviceClient.h"
    #include "Command.h"

    // Process the command and set the LED blink interval
    void processCommand(IoTF::Command &cmd)
    {
        if (strcmp(cmd.getCommand(), "blink") == 0)
    	{
    	    char *payload = cmd.getPayload();
    	    char* pos = strchr(payload, '}');
    	    if (pos != NULL) {
    	        *pos = '\0';
    	        char* ratepos = strstr(payload, "rate");
    	        if(ratepos == NULL)
    	            return;
    	        if ((pos = strchr(ratepos, ':')) != NULL)
    	        {
    	            int blink_rate = atoi(pos + 1);
    	            blink_interval = (blink_rate <= 0) ? 0 : (blink_rate > 50 ? 1 : 50/blink_rate);
    	        }
    	    }
    	} else {
            WARN("Unsupported command: %s\n", cmd.getCommand());
        }
    }

    client.setCommandCallback(processCommand);

    client.yield(1000);  // allow the MQTT client to receive messages
    ....
```
Pour afficher la totalité de l'exemple de code, voir l'exemple d'application [ IBMIoTClientLibrarySample ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp){: new_window}.

**Remarque :** La fonction `client.yield()` doit être appelée régulièrement pour permettre la réception des commandes.
La fonction `client.yield()` permet au terminal de recevoir des commandes de la part de Watson IoT Platform et maintient la connexion active. Si la fonction `client.yield()` n'est pas appelée dans le délai spécifié par l'intervalle de signal de présence, les commandes envoyées à la plateforme ne seront pas reçues par le terminal. La valeur affectée à la fonction `client.yield()` spécifie la durée (en millisecondes) pendant laquelle les données peuvent être lues à partir du socket avant que l'application ne reprenne la main.

## Déconnexion du client
{: #disconnect_client}

Pour déconnecter le client et libérer les connexions, exécutez le fragment de code suivant :

```
	...
	client.disconnect();
	....
```
## Exemples
{: #samples}

[IBMIoTClientLibrarySample ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/){: new_window} est un exemple de code qui montre comment utiliser la bibliothèque client {{site.data.keyword.iot_short_notm}} pour connecter les terminaux mbed LPC1768 ou FRDM-K64F à l'instance de service.
