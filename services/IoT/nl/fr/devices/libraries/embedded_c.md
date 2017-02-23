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


# Embedded C pour les développeurs de terminaux
{: #embedded_c}

Vous pouvez utiliser Embedded C pour générer et personnaliser des terminaux qui interagissent avec votre organisation sur {{site.data.keyword.iot_full}}. Utilisez les informations et les exemples fournis pour commencer à développer vos terminaux à l'aide de Embedded C.
{:shortdesc}

## Téléchargement du client et des ressources Embedded C
{: #embeddedc_client_download}

Pour accéder aux bibliothèques et exemples client Embedded C pour {{site.data.keyword.iot_short_notm}}, accédez au référentiel [iotf-embeddedc](https://github.com/ibm-messaging/iotf-embeddedc) dans GitHub et exécutez les instructions d'installation.


## Dépendances
{: #dependencies}

|Dépendance |Description|
|:---|:---|
|[Bibliothèque Eclipse Paho Embedded C](http://git.eclipse.org/c/paho/org.eclipse.paho.mqtt.embedded-c.git) |Fournit une bibliothèque client MQTT C. Pour plus d'informations, voir [MQTT Client Package -  C for embedded devices](http://www.eclipse.org/paho/clients/c/embedded/).|


## Installation
{: #installation}

Pour installer la bibliothèque client {{site.data.keyword.iot_short_notm}} pour Embedded C, exécutez les instructions suivantes :

1. Pour installer la dernière version de la bibliothèque, entrez le code suivant sur la ligne de commande :
```
  [root@localhost ~]# git clone https://github.com/ibm-messaging/iotf-embeddedc.git
```
2. Copiez le fichier .tar de la bibliothèque Paho dans le répertoire *lib*.
```
    cd iotf-embeddedc
    cp ~/org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz lib/
```
3. Extrayez le fichier bibliothèque.
```  cd lib
    tar xvzf org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz
```
Le client téléchargé possède la structure de fichier suivante :

```
 |-lib - contient tous les fichiers dépendants
 |-samples - contient les exemples helloWorld et sampleDevice
   |-sampleDevice.c - implémentation de l'exemple de terminal
   |-helloworld.c - application quickstart
   |-README.md
   |-Makefile
   |-build.sh
 |-iotfclient.c - principal fichier client
 |-iotfclient.h - fichier d'en-tête pour le client
```

## Initialisation de la bibliothèque client
{: #initialize_client_library}

Une fois la bibliothèque client téléchargée, elle doit être initialisée et connectée à {{site.data.keyword.iot_short_notm}}. Vous pouvez initialiser la bibliothèque client {{site.data.keyword.iot_short_notm}} pour Embedded C en transmettant des paramètres ou en utilisant un fichier de configuration.

### Transmission de paramètres

La fonction `initialize` utilise les paramètres suivants pour établir la connexion au service {{site.data.keyword.iot_short_notm}} :

|Définition |Description |
|:---|:---|
|`client`|Pointeur vers *iotfclient*.|
|`org`|ID de votre organisation.|
|`type` |Type de votre terminal.|
|`id` |ID de terminal.|
|`auth-method` |Méthode d'authentification à utiliser. La seule valeur actuellement prise en charge est `token`.|
|`auth-token`|Jeton d'authentification permettant d'établir une connexion sécurisée entre votre terminal et Watson IoT Platform.|


```
	#include "iotfclient.h"
	....
	....
	Iotfclient client;
	//quickstart
	rc = initialize(&client,"quickstart","iotsample","001122334455",NULL,NULL);
	//registered
	rc = initialize(&client,"org","type","id","auth-method","auth-token");
	....
```

### Utilisation d'un fichier de configuration

Vous pouvez également utiliser un fichier de configuration pour initialiser la bibliothèque client Embedded C. La fonction `initialize_configfile` prend le chemin de fichier de configuration en tant que paramètre.

```
	#include "iotfclient.h"
	....
	....
	char *filePath = "./device.cfg";
	Iotfclient client;
	rc = initialize_configfile(&client, filePath);
	....
```

Le fichier de configuration doit utiliser le format suivant :

```
	org=$orgId
	type=$myDeviceType
	id=$myDeviceId
	auth-method=token
	auth-token=$token
```

## Connexion au service
{: #connecting_service}

Après avoir initialisé la bibliothèque client {{site.data.keyword.iot_short_notm}} Embedded C, vous pouvez vous connecter à {{site.data.keyword.iot_short_notm}} en appelant la fonction `connectiotf`.

```
	#include "iotfclient.h"
	....
	....
	Iotfclient client;
	char *configFilePath = "./device.cfg";

	rc = initialize_configfile(&client, configFilePath);

	if(rc != SUCCESS){
		printf("initialize failed and returned rc = %d.\n Quitting..", rc);
		return 0;
	}

	rc = connectiotf(&client);

	if(rc != SUCCESS){
		printf("Connection failed and returned rc = %d.\n Quitting..", rc);
		return 0;
	}
	....
```

## Traitement des commandes
{: #handling_commands}

Lorsque le client du terminal se connecte, il s'abonne automatiquement aux commandes de ce terminal. Pour traiter des commandes spécifiques, vous devez enregistrer une méthode de rappel de commande en appelant la fonction `setCommandHandler`. La fonction de rappel possède les propriétés suivantes :

|Propriété |Description|
|:---|:---|
|`commandName`  |Nom de la commande qui a été appelée. |  
|`format`  |Format de l'événement. Le format peut être n'importe quelle chaîne, par exemple, JSON.|
|`payload`  |Données du contenu de la commande. La longueur maximale est de 131072 octets. |


```
	#include "iotfclient.h"

	void myCallback (char* commandName, char* format, void* payload)
	{
	printf("The command received :: %s\n", commandName);
	printf("format : %s\n", format);
	printf("Payload is : %s\n", (char *)payload);
	}
	...
	...
	char *filePath = "./device.cfg";
	rc = connectiotfConfig(filePath);
	setCommandHandler(myCallback);

	yield(1000);
	....

```
**Remarque :** La fonction `yield()` permet au terminal de recevoir des commandes de la part de Watson IoT Platform et maintient la connexion active. Si la fonction `yield()` n'est pas appelée dans le délai spécifié par l'intervalle de signal de présence, les commandes envoyées à la plateforme ne seront pas reçues par le terminal. La valeur affectée à la fonction `yield()` spécifie la durée (en millisecondes) pendant laquelle les données peuvent être lues à partir du socket avant que l'application ne reprenne la main.

## Publication d'événements
{: #publishing_events}

Les événements peuvent être publiés à l'aide des propriétés suivantes :

|Propriété |Description|
|:---|:---|
|eventType  |Type d'événement publié, par exemple, status ou gps. |  
|eventFormat  |Le format peut être n'importe quelle chaîne, par exemple, `json`. |
|data  |Données du contenu. La longueur maximale est de 131072 octets. |
|QoS  |Niveau de qualité de service de l'événement publié. Les valeurs prises en charge sont `0`, `1` et `2`.|


```
	#include "iotfclient.h"
	....
	rc = connectiotf (org, type, id , authmethod, authtoken);
	char *payload = {\"d\" : {\"temp\" : 34 }};

	rc= publishEvent("status","json", "{\"d\" : {\"temp\" : 34 }}", QOS0);
	....
```

## Déconnexion du client
{: #disconnect_client}

Pour déconnecter le client et libérer les connexions, exécutez le fragment de code suivant :

```
	#include "iotfclient.h"
	....
	rc = connectiotf (org, type, id , authmethod, authtoken);
	char *payload = {\"d\" : {\"temp\" : 34 }};

	rc= publishEvent("status","json", payload , QOS0);
	...
	rc = disconnect();
	....
```

## Exemples
{: #samples}

Un exemple de terminal et le code d'application sont fournis dans [GitHub](https://github.com/ibm-messaging/iotf-embeddedc/tree/master/samples).
