---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-20"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Développement de passerelles gérées à l'aide de Java
{: #java_cli_managed_gw}

Les passerelles jouent un rôle important dans la gestion des terminaux qui leur sont connectés. De nombreux terminaux sont très basiques et ne sont dotés d'aucune fonction de gestion des terminaux, par conséquent, ces terminaux basiques doivent être gérés depuis une passerelle. Dans {{site.data.keyword.iot_full}}, une passerelle gérée est une passerelle qui peut gérer les terminaux qui lui sont connectés et fournir des fonctions de gestion des terminaux, telles que les mises à jour de microprogramme, d'emplacement et de diagnostic.
{:shortdesc}

Vous pouvez utiliser la bibliothèque client Java {{site.data.keyword.iot_short}} et les informations fournies pour développer du code Java et faire de votre passerelle une passerelle connectée. Des exemples sont également fournis pour vous aider à développer du code Java dans le but de connecter une passerelle au service de gestion des terminaux et d'exécuter des opérations de gestion des terminaux.

## Service de gestion de terminaux
{: #dm_service}

Le service de gestion des terminaux {{site.data.keyword.iot_short}} fournit des fonctions de gestion des terminaux permettant aux passerelles de gérer les terminaux qui lui sont connectés.

Une passerelle gérée exécute un agent de gestion des terminaux, lequel s'exécute en tant que proxy pour tous les terminaux qui se connectent à {{site.data.keyword.iot_short}} via la passerelle.

### Agent de gestion des terminaux

Les terminaux qui se connectent à {{site.data.keyword.iot_short}} indirectement via une passerelle peuvent utiliser différents protocoles de connexion, s'ils sont pris en charge par le terminal de passerelle.

L'instance `ManagedGateway` est un agent de gestion des terminaux qui fournit une liste de méthodes permettant d'effectuer une ou plusieurs actions de gestion des terminaux, telles que la participation à l'activité de gestion des terminaux et la mise à jour de codes d'erreur, de journaux, d'emplacement et de microprogramme ou de terminal.

L'agent de gestion des terminaux sur la passerelle convertit et traite le protocole de connexion des terminaux qui se connectent, garantissant ainsi que le terminal peut être géré par {{site.data.keyword.iot_short}}. Grâce à l'agent de gestion des terminaux, la passerelle devient plus qu'un tunnel transparent entre le terminal connecté et {{site.data.keyword.iot_short}}. Par exemple, si un terminal connecté à une passerelle ne parvient pas à télécharger un microprogramme, l'agent de gestion des terminaux sur la passerelle peut effectuer les actions suivantes :
- Intercepter une demande de téléchargement de microprogramme émise par un terminal
- Télécharger le microprogramme pour le terminal
- Stocker le microprogramme de terminal sur la passerelle

Plus tard, lorsque le terminal reçoit l'instruction d'effectuer la mise à niveau, l'agent de gestion des terminaux sur la passerelle peut envoyer le microprogramme au terminal et le mettre à jour.

## Création du modèle de terminal
{: #create_device_model}

Dans {{site.data.keyword.iot_short}}, le modèle de terminal décrit les métadonnées et les caractéristiques de gestion de terminaux et de passerelles. La base de données de terminaux représente la principale source d'informations sur les terminaux ou les passerelles. Les applications et les terminaux gérés peuvent envoyer des mises à jour d'emplacement, des mises à jour de processus de mise à niveau de microprogramme et d'autres types de mise à jour. Lorsque des mises à jour sont reçues par {{site.data.keyword.iot_short}}, la base de données de terminaux est mise à jour et les informations sont disponibles pour les applications qui se connectent.

Dans la bibliothèque client Java {{site.data.keyword.iot_short}}, le modèle de terminal est représenté par la classe Java `DeviceData`.

Pour créer la classe `DeviceData`, créez les objets suivants :

- `DeviceInfo` (facultatif)
- `DeviceLocation` (facultatif, requis uniquement si le terminal souhaite être averti de l'emplacement qui est défini par l'application via l'API {{site.data.keyword.iot_short}})
- `DeviceFirmware` (facultatif)
- `DeviceMetadata` (facultatif)

Pour plus d'informations, voir [Modèle de terminal](../../reference/device_model.html).

### DeviceInfo

Le fragment de code suivant contient des exemples de données illustrant la création des objets `DeviceInfo` et `DeviceMetadata` :

```java
DeviceInfo deviceInfo = new DeviceInfo.Builder().
                           serialNumber("10087").
                           manufacturer("IBM").
                           model("7865").
                           deviceClass("A").
                           description("My RasPi Device").
                           fwVersion("1.0.0").
                           hwVersion("1.0").
                           descriptiveLocation("EGL C").
                           build();

/**
  * Create a DeviceMetadata object
 **/
JsonObject data = new JsonObject();
data.addProperty("customField", "customValue");
DeviceMetadata metadata = new DeviceMetadata(data);

```

Le fragment de code suivant illustre la création de la classe `DeviceData` à l'aide des objets `DeviceInfo` et `DeviceMetadata` qui ont été créés dans l'exemple précédent :

```java
DeviceData deviceData = new DeviceData.Builder().
                         deviceInfo(deviceInfo).
                         metadata(metadata).
                         build();
```

Chaque passerelle et chaque terminal connecté doivent posséder leur propre définition de classe `DeviceData` destinée à les représenter dans {{site.data.keyword.iot_short}}. Pour les passerelles, la classe `DeviceData` est transmise à la bibliothèque dans le cadre de la construction de l'instance `ManagedGateway`. Pour les terminaux connectés, la classe `DeviceData` est transmise à la bibliothèque en même temps que l'objet `sendDeviceManageRequest()`.

## Constructeurs ManagedGateway
{: #construct_managed_gateway}

`ManagedGateway` est une classe Java qui permet de connecter une passerelle à {{site.data.keyword.iot_short}} en tant que passerelle gérée pouvant effectuer au moins une opération de gestion des terminaux soit pour elle même soit pour les terminaux connectés. Une instance `ManagedGateway` peut également être utilisée pour effectuer des opérations de passerelle normales, telles que la publication d'événements de terminal, la connexion d'événements de terminal et l'écoute de commandes provenant d'applications. L'instance `ManagedGateway` est un agent de gestion des terminaux.

Dans la classe `ManagedGateway`, deux constructeurs, Constructeur 1 et Constructeur 2, prennent en charge des modèles d'utilisateur distincts.

### Constructeur 1

Le constructeur 1 construit une instance `ManagedGateway` en acceptant une classe `DeviceData` qui contient toutes les propriétés suivantes :

| Propriété     |Description     |
|----------------|----------------|
|`Organization-ID` |ID de votre organisation.|
|`Gateway-Type` |Type de votre terminal de passerelle.|
|`Gateway-ID` |ID du terminal de passerelle.|
|`Authentication-Method`|Méthode d'authentification. La seule méthode prise en charge est "token".|
|`Authentication-Token`|Jeton de clé d'API.|
|`auth-key`   |Clé d'API facultative qui est requise lorsque vous affectez la valeur `apikey` au paramètre auth-method.|
|`auth-token`   |Jeton de clé d'API qui est également requis lorsque vous affectez la valeur `apikey` au paramètre auth-method. |
|`clean-session`|Valeur true ou false requise uniquement si vous souhaitez connecter la passerelle en mode d'abonnement durable. Par défaut, `clean-session` prend la valeur `true`.|
|`Port`|Numéro de port auquel se connecter. Indiquez 8883 ou 443. Si vous n'indiquez pas de numéro de port, le client se connecte à {{site.data.keyword.iot_short_notm}} sur le numéro de port 8883 par défaut.|
|`WebSocket`|Valeur true ou false requise uniquement si vous souhaitez connecter la passerelle à l'aide de WebSockets.|
|`MaxInflightMessages`  |Définit le nombre maximal de messages en cours pour la connexion. La valeur par défaut est 100.|
|`Automatic-Reconnect`  |Valeur true ou false qui est requise lorsque vous souhaitez reconnecter automatiquement le terminal à {{site.data.keyword.iot_short_notm}} alors qu'il est en ode déconnecté. La valeur par défaut est false.|
|`Disconnected-Buffer-Size`|Nombre maximal de messages qui peut être stocké en mémoire alors que le client est déconnecté. La valeur par défaut est 5 000.|

**Remarque :** Pour connecter le passerelle en mode d'abonnement durable, affectez la valeur `false` à l'option `clean-session`. Pour plus d'informations sur la propriété `clean-session`, voir la section 'Subscription Buffers and Clean Session' de la [documentation MQTT](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

Le code suivant montre comment créer une instance `ManagedGateway` :

```java
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Gateway-Type", "iotsample-arduino");
options.setProperty("Gateway-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedGateway ManagedGateway = new ManagedGateway(options, deviceData);
```

### Constructeur 2

Le constructeur 2 construit une instance `ManagedGateway` en acceptant un objet `DeviceData` et l'instance client MQTT. Le constructeur 2 requiert également que l'objet `DeviceData` figurant dans l'instance comporte le type de terminal et l'ID terminal, comme illustré dans l'exemple de code suivant :

```java
// Code that constructs either a synchronous or asynchronous MQTT client instance of mqttClient.
.....

// Code that constructs the DeviceData object
DeviceData deviceData = new DeviceData.Builder().
                         typeId("Gateway-Type").
                         deviceId("Gateway-ID").
                         deviceInfo(deviceInfo).
                         metadata(metadata).
                         build();

....
ManagedGateway ManagedGateway = new ManagedGateway(mqttClient, deviceData);

```

**Remarque :** Dans le cadre du développement pour des terminaux personnalisés, utilisez le constructeur 2, car ce dernier crée une instance de passerelle gérée en utilisant l'instance client MQTT connectée existante et vous permet ainsi de bénéficier des opérations de gestion des terminaux. Utilisez la bibliothèque client Java pour toutes les fonctions de terminal.

## Demandes de gestion de terminal à partir d'une passerelle
{: #dm_requests}

### Envoi d'une demande de gestion à partir d'une passerelle

Pour indiquer à une passerelle qu'elle doit participer à des activités de gestion des terminaux, appelez la méthode `sendGatewayManageRequest()`, illustrée dans l'exemple de code suivant :

```java
managedGateway.sendGatewayManageRequest(0, true, true);
```
La demande de gestion lance une demande de connexion en interne si le terminal n'est pas encore connecté à {{site.data.keyword.iot_short}}.

La méthode `sendGatewayManageRequest()` accepte les paramètres suivants :

| Paramètre     |Description     |
|----------------|----------------|
|`lifetime`|Nombre de secondes durant lesquelles la passerelle doit envoyer une autre demande de gestion de type de terminal afin d'éviter d'être classée comme en veille et de devenir un terminal non géré. Si la zone `lifetime` est omise ou si elle a pour valeur 0, la passerelle gérée n'est pas classée comme en veille. La valeur minimale prise en charge pour la zone `lifetime` est 3600 secondes (1 heure).|
|`supportFirmwareActions`|Valeur true ou false qui détermine si la passerelle prend en charge des actions de microprogramme. La passerelle doit également ajouter un gestionnaire de microprogramme pour gérer les demandes de microprogramme.|
|`supportDeviceActions`|Valeur true ou false qui détermine si la passerelle prend en charge des actions sur les terminaux. La passerelle doit également ajouter un gestionnaire d'actions sur les terminaux pour gérer les demandes de réamorçage et de réinitialisation avec les paramètres d'usine.|


L'instance `ManagedGateway` est un agent de gestion des terminaux qui fournit une liste de méthodes permettant d'effectuer une ou plusieurs actions de gestion des terminaux, telles que la participation à l'activité de gestion des terminaux et la mise à jour de codes d'erreur, de journaux, d'emplacement et de microprogramme ou de terminal.

### Envoi d'une demande de gestion à partir de terminaux connectés

Pour permettre aux terminaux connectés derrière une passerelle de participer aux activités de gestion des terminaux sur la passerelle, appelez la méthode `sendDeviceManageRequest()`.

La méthode `sendDeviceManageRequest()` accepte les détails des terminaux connectés, ainsi que les paramètres `lifetime`, `supportFirmwareActions` et `supportDeviceActions`. Une passerelle peut également utiliser la méthode `sendDeviceManageRequest()` surchargée afin de définir l'objet `DeviceData` pour le terminal connecté.

#### Exemple d'envoi d'une demande de gestion à partir de terminaux connectés

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, lifetime, true, true);
```

### Envoi d'une demande d'annulation de gestion à partir d'une passerelle

Lorsqu'une passerelle n'a pas plus besoin d'être gérée, vous pouvez appeler la méthode `sendGatewayUnmanageRequet()` pour arrêter les activités de gestion des terminaux sur la passerelle.  Lorsque la méthode `sendGatewayUnmanageRequet()` est appelée, {{site.data.keyword.iot_short}} n'envoie plus aucune nouvelle demande de gestion des terminaux pour la passerelle et toutes les demandes de gestion des terminaux depuis la passerelle sont rejetées, à l'exception des demandes **Manage**. Les demandes émises par les terminaux situés derrière la passerelle ne sont pas rejetées.

#### Exemple d'envoi d'une demande d'annulation de gestion à partir d'une passerelle

```java
managedGateway.sendGatewayUnmanageRequet();
```

### Envoi d'une demande d'annulation de gestion à partir de terminaux connectés

Lorsqu'un terminal situé derrière une passerelle n'a plus besoin d'être géré, pour faire passer un terminal connecté de l'état Géré à l'état Non géré, la passerelle peut appeler la méthode `sendDeviceUnmanageRequet()`. Lorsque la méthode `sendDeviceUnmanageRequet()` est appelée, {{site.data.keyword.iot_short}} n'envoie plus aucune nouvelle demande de gestion des terminaux pour le terminal et toutes les demandes de gestion des terminaux depuis la passerelle relatives au terminal connecté sont rejetées, à l'exception des demandes **Manage**.

#### Exemple d'envoi d'une demande d'annulation de gestion à partir de terminaux connectés

```java
managedGateway.sendDeviceUnmanageRequet();
```

## Mise à jour d'emplacement
{: #location_updates}

### Envoi de mises à jour d'emplacement de passerelle

Les passerelles qui peuvent déterminer leur emplacement peuvent choisir d'avertir {{site.data.keyword.iot_short}} que des modifications d'emplacement ont été apportées. La passerelle peut appeler l'une des méthodes `updateLocation()` surchargées pour mettre à jour l'emplacement du terminal.

```java
    // update the location with latitude, longitude, and elevation.
int rc = managedGateway.updateGatewayLocation(30.28565, -97.73921, 10);
if(rc == 200) {
    System.out.println("Location updated successfully!");
} else {
System.err.println("Failed to update the location!");
    }
```

### Envoi de mises à jour d'emplacement de terminal connecté

La passerelle peut appeler la méthode de terminal `updateDeviceLocation()` correspondante pour mettre à jour l'emplacement des terminaux connectés. La méthode surchargée peut être utilisée pour spécifier la méthode `measuredDateTime`.

```java
// update the location of the attached device with latitude, longitude, and elevation
int rc = managedGateway.updateDeviceLocation(typeId, deviceId, 30.28565, -97.73921, 10);
```
Pour plus d'informations sur les mises à jour d'emplacement, voir [Demandes de gestion des terminaux](../../devices/device_mgmt/index.html#/update-location#update-location).

## Traitement de code d'erreur
{: #errors}

### Création et suppression de codes d'erreur de passerelle

Une passerelle peut choisir d'avertir {{site.data.keyword.iot_short}} que son état d'erreur a été modifié. La passerelle peut appeler la méthode`addErrorCode()` pour ajouter le code d'erreur en cours à {{site.data.keyword.iot_short}}.

```java
int rc = managedGateway.addGatewayErrorCode(300);
```

Les codes d'erreur affichés pour une passerelle peuvent être effacés de {{site.data.keyword.iot_short}} en appelant la méthode `clearErrorCodes()`, comme illustré ci-dessous :

```java
int rc = managedGateway.clearGatewayErrorCodes();
```

### Création et suppression de codes d'erreur de terminaux connectés

Une passerelle peut également appeler la méthode de terminal correspondante afin d'ajouter ou d'effacer des codes d'erreur pour les terminaux connectés :

```java
int rc = managedGateway.addDeviceErrorCode(typeId, deviceId, 300);
rc = managedGateway.clearDeviceErrorCodes(typeId, deviceId);
```

### Création et suppression de messages de journal de passerelle

Une passerelle peut choisir d'avertir {{site.data.keyword.iot_short}} que des modifications ont été apportées en ajoutant une nouvelle entrée de journal. Une entrée de journal inclut les éléments suivants :

- Chaîne de message
- Horodatage
- Gravité
- Eventuellement, données de diagnostic binaires codées en base64

Les passerelles peuvent appeler la méthode `addGatewayLog()` pour envoyer des messages de journal, comme illustré dans l'exemple suivant :

```java
// An example Log event
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addGatewayLog(message, timestamp, severity);
```

Les messages de journal peuvent être effacés de {{site.data.keyword.iot_short}} en appelant la méthode `clearLogs()` :

```java
rc = managedGateway.clearGatewayLogs();
```

### Création et suppression de journaux pour des terminaux connectés

De même, la passerelle peut appeler la méthode de terminal correspondante pour créer ou effacer les journaux des terminaux connectés, comme illustré dans l'exemple de code suivant :

```java

// An example log event:
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addDeviceLog(typeId, deviceId, message, timestamp, severity);
```

Pour effacer les journaux de terminaux connectés, appelez la méthode `clearDeviceLogs()` en spécifiant les détails du terminal connecté, comme illustré dans l'exemple de code suivant :

```java
int rc = managedGateway.clearDeviceLogs(typeId, deviceId);
```

Les opérations de diagnostic des terminaux ont pour but de fournir des informations sur les erreurs de terminal ou de passerelle. Elles ne fournissent pas d'informations de diagnostic sur la connexion d'un terminal à {{site.data.keyword.iot_short}}.

Pour plus d'informations sur l'opération de diagnostic, voir [Demandes de gestion des terminaux](../../devices/device_mgmt/index.html#/update-location#update-location).

## Mises à jour et actions sur un microprogramme
{: #firmware}

Le processus de mise à jour du microprogramme est scindé en deux actions distinctes :

- Téléchargement du microprogramme
- Mise à jour du microprogramme

La passerelle doit exécuter les activités suivantes afin de prendre en charge les actions sur le microprogramme à la fois pour elle-même et pour les terminaux qui lui sont connectés :

1. Facultatif : Construire un objet `DeviceFirmware`.
2. Informer le serveur de la prise en charge de l'action sur le microprogramme.
3. Créer le gestionnaire d'actions sur le microprogramme.
4. Ajouter le gestionnaire à `ManagedGateway`.

### Etape 1 : Construire un objet `DeviceFirmware`

Pour effectuer des actions sur le microprogramme, une passerelle peut éventuellement construire un objet `DeviceFirmware` à la fois pour elle-même et pour les terminaux qui lui sont connectés, puis l'ajouter à l'objet `DeviceData`, comme illustré dans l'exemple suivant :

```java
DeviceFirmware firmware = new DeviceFirmware.Builder().
			version("Firmware.version").
			name("Firmware.name").
			url("Firmware.url").
			verifier("Firmware.verifier").
			state(FirmwareState.IDLE).
			build();

DeviceData deviceData = new DeviceData.Builder().
			deviceInfo(deviceInfo).
			deviceFirmware(firmware).
			metadata(metadata).
			build();

ManagedGateway ManagedGateway = new ManagedGateway(options, deviceData);
managedGateway.connect();
```

Pour les terminaux connectés, l'objet `DeviceData` construit peut être transmis à la bibliothèque lors de l'envoi de la demande de gestion, comme illustré dans l'exemple de code suivant :

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, lifetime, supportFirmwareActions, supportDeviceActions);
```

L'objet `DeviceFirmware` représente le microprogramme en cours du passerelle ou du terminal connecté et sera utilisé pour signaler l'état des actions de téléchargement de microprogramme et de mise à jour de microprogramme sur {{site.data.keyword.iot_short}}. Si l'objet `DeviceFirmware` n'est pas construit par la passerelle, la bibliothèque crée un objet vide et signale l'état à {{site.data.keyword.iot_short}}.

### Etape 2 : Informer le serveur de la prise en charge de l'action sur le microprogramme

La passerelle ou les terminaux qui lui sont connectés doivent affecter la valeur true à l'indicateur d'action sur le microprogramme pour permettre au serveur de lancer la demande de microprogramme. Cette modification peut être obtenue en affectant la valeur true au paramètre `supportFirmwareActions` dans la demande de gestion.

La passerelle peut appeler la méthode suivante pour informer le serveur de sa prise en charge de microprogramme :
```java
managedGateway.sendGatewayManageRequest(3600, true, false);
```

De même, la passerelle peut appeler la méthode de terminal correspondante pour informer la prise en charge de microprogramme des terminaux connectés :

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, 3600, true, false);
```

Lorsque la prise en charge est signalée au serveur de gestion des terminaux, celui-ci transmet les actions sur le microprogramme à la passerelle, soit pour elle-même soit pour les terminaux situés derrière elle.

### Etape 3 : Créer le gestionnaire d'actions sur le microprogramme

Pour que l'action sur le microprogramme soit prise en charge, la passerelle doit créer un gestionnaire et l'ajouter à `managedGateway`. Le gestionnaire doit étendre une classe `DeviceFirmwareHandler` et implémenter les méthodes suivantes :

```java
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**Remarque** : Un seul gestionnaire peut être ajouté à la bibliothèque, à la fois pour la passerelle et pour les terminaux connectés vers lesquels les demandes de mise à jour ou de téléchargement de microprogramme sont redirigées. L'implémentation doit créer une unité d'exécution ou un pool d'unités d'exécution pour gérer plusieurs demandes de microprogramme à la fois.

Un exemple d'implémentation d'un gestionnaire de pool d'unités d'exécution figure dans le [référentiel GitHub d'exemples de passerelle ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java){: new_window}.

### Exemple d'implémentation de `downloadFirmware`

L'implémentation doit ajouter une logique pour télécharger le microprogramme et signaler l'état du téléchargement à l'aide de l'objet `DeviceFirmware`. Si l'opération de téléchargement de microprogramme aboutit, l'état du microprogramme doit prendre la valeur 'DOWNLOADED' et la propriété `UpdateStatus` doit prendre la valeur 'SUCCESS'.

Si une erreur se produit lors du téléchargement d'un microprogramme, l'état prend la valeur 'IDLE' et la propriété `updateStatus` doit prendre l'une des valeurs d'état d'erreur suivantes :

- OUT_OF_MEMORY
- CONNECTION_LOST
- INVALID_URI

Un exemple d'implémentation de téléchargement de microprogramme est illustré dans l'exemple de code suivant :

**Important :** L'exemple de code fourni n'inclut pas la section de pool d'unités d'exécution. Pour obtenir l'implémentation complète du gestionnaire de microprogramme, voir l'exemple disponible dans le [référentiel GitHub d'exemples de passerelle Java IBM ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java){: new_window}.

```java
public void downloadFirmware(DeviceFirmware deviceFirmware) {
	boolean success = false;
    URL firmwareURL = null;
    URLConnection urlConnection = null;

	try {
		firmwareURL = new URL(deviceFirmware.getUrl());
        urlConnection = firmwareURL.openConnection();
        if(deviceFirmware.getName() != null) {
			downloadedFirmwareName = deviceFirmware.getName();
        } else {
			// use the time stamp as the name
			downloadedFirmwareName = "firmware_" +new Date().getTime()+".deb";
		}

		File file = new File(downloadedFirmwareName);
		BufferedInputStream bis = new BufferedInputStream(urlConnection.getInputStream());
		BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(file.getName()));

		int data = bis.read();
        if(data != -1) {
			bos.write(data);
            byte[] block = new byte[1024];
            while (true) {
				int len = bis.read(block, 0, block.length);
                if(len != -1) {
					bos.write(block, 0, len);
                } else {
					break;
                }
			}
            bos.close();
            bis.close();
            success = true;
        } else {
			//There is no data to read, so set an error
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.INVALID_URI);
        }
	} catch(MalformedURLException me) {
		// Invalid URL, so set the status to reflect the same,
        deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.INVALID_URI);
    } catch (IOException e) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.CONNECTION_LOST);
    } catch (OutOfMemoryError oom) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.OUT_OF_MEMORY);
    }

    if(success == true) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.SUCCESS);
        deviceFirmware.setState(FirmwareState.DOWNLOADED);
    } else {
		deviceFirmware.setState(FirmwareState.IDLE);
    }
}
```

Une passerelle gérée peut vérifier l'intégrité de l'image de microprogramme téléchargée à l'aide du vérificateur et signaler l'état à {{site.data.keyword.iot_short}}. Le vérificateur peut être défini par la passerelle au cours des étapes suivantes :

- Pendant le démarrage lors de la création de l'objet 'DeviceFirmware'
- Lors de la soumission d'une demande 'downloadFirmware' par une application

#### Exemple

```java
private boolean verifyFirmware(File file, String verifier) throws IOException {
	FileInputStream fis = null;
    String md5 = null;
    try {
		fis = new FileInputStream(file);
        md5 = org.apache.commons.codec.digest.DigestUtils.md5Hex(fis);
        System.out.println("Downloaded Firmware MD5 sum:: "+ md5);
    } catch (FileNotFoundException e) {
		e.printStackTrace();
    } catch (IOException e) {
		e.printStackTrace();
    } finally {
		fis.close();
    }
    if(verifier.equals(md5)) {
		System.out.println("Firmware verification successful");
		return true;
	}
	System.out.println("Download firmware checksum verification failed."
			+ "Expected "+verifier + " found "+md5);
    return false;
}
```

La totalité du code est consultable dans l'exemple de gestion des passerelles[GatewayFirmwareHandlerSample](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java).

### Exemple d'implémentation de `updateFirmware`

L'implémentation doit créer une unité d'exécution distincte et ajouter une logique pour installer le microprogramme téléchargé et signaler l'état de la mise à jour via l'objet `DeviceFirmware`. Si l'opération de mise à jour de microprogramme aboutit, l'état du microprogramme doit prendre la valeur 'IDLE' et la propriété `updateStatus` doit prendre la valeur 'SUCCESS'.

Si une erreur se produit lors de la mise à jour de microprogramme, `updateStatus` doit prendre l'une des valeurs d'état d'erreur suivantes :

* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE

L'exemple de code suivant montre comment vous pouvez implémenter une mise à jour de microprogramme pour un terminal Raspberry Pi :

```java
public void updateFirmware(DeviceFirmware deviceFirmware) {
	try {
		ProcessBuilder pkgInstaller = null;
        Process p = null;
        pkgInstaller = new ProcessBuilder("sudo", "dpkg", "-i", downloadedFirmwareName);
        boolean success = false;
        try {
			p = pkgInstaller.start();
            boolean status = waitForCompletion(p, 5);
            if(status == false) {
				p.destroy();
                deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
                return;
            }
            System.out.println("Firmware Update command "+status);
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.SUCCESS);
            deviceFirmware.setState(FirmwareState.IDLE);
        } catch (IOException e) {
			e.printStackTrace();
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
        } catch (InterruptedException e) {
			e.printStackTrace();
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
        }
	} catch (OutOfMemoryError oom) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.OUT_OF_MEMORY);
    }
}
```

La totalité du code est illustrée dans l'exemple `GatewayFirmwareHandlerSample` qui figure dans le [référentiel GitHub d'exemples de passerelle ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java){: new_window}.

### Etape 4 : Ajouter le gestionnaire à `ManagedGateway`

Lorsqu'un gestionnaire est créé, il doit être ajouté à l'instance `ManagedGateway` de sorte que la bibliothèque client Java appelle la méthode correspondante lorsqu'une demande d'action sur le microprogramme est émise par {{site.data.keyword.iot_short}}.

```java
GatewayFirmwareHandlerSample fwHandler = new GatewayFirmwareHandlerSample();
mgdGateway.addFirmwareHandler(fwHandler);
```

Pour plus d'informations sur les actions sur le microprogramme, voir [Demandes de gestion des terminaux ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/requests.html#/firmware-actions#firmware-actions){: new_window}.

## Actions sur les terminaux
{: #dev_actions}

{{site.data.keyword.iot_short}} prend en charge les actions sur les terminaux décrites ci-dessous :

- Réamorçage
- Réinitialisation avec les paramètres d'usine

La passerelle doit exécuter les activités suivantes afin de prendre en charge les actions sur les terminaux à la fois pour elle-même et pour les terminaux situés derrière elle :

1. Informer le serveur de la prise en charge des actions sur les terminaux.
2. Créer le gestionnaire d'actions sur les terminaux.
3. Ajouter le gestionnaire à `ManagedGateway`.

### Etape 1 : Informer le serveur de la prise en charge des actions sur les terminaux

Pour effectuer une action de réamorçage ou de réinitialisation avec les paramètres d'usine pour une passerelle et les terminaux qui lui sont connectés, la passerelle doit d'abord avertir {{site.data.keyword.iot_short}} de la prise en charge de ces actions. Pour cela, une valeur true peut être affectée au paramètre `supportDeviceActions` lors de l'envoi de la demande **Manage**.

Une passerelle peut appeler la méthode suivante afin de signaler au serveur la prise en charge des actions sur les terminaux :

```java
// Last parameter represents the device action support
managedGateway.sendGatewayManageRequest(3600, true, true);
```

Une passerelle peut appeler la méthode de terminal correspondante pour signaler la prise en charge des actions sur les terminaux pour les terminaux connectés,

```java
// Last parameter represents the device action support
managedGateway.sendDeviceManageRequest(typeId, deviceId, 0, true, true);
```

Lorsque la prise en charge est signalée au serveur de gestion des terminaux, celui-ci transmet les demandes d'action sur les terminaux au terminal.

### Etape 2 : Créer le gestionnaire d'actions sur les terminaux

Pour que l'action sur les terminaux soit prise en charge, la passerelle doit créer un gestionnaire et l'ajouter à l'instance `managedGateway`. Le gestionnaire doit étendre une classe `DeviceActionHandler` et implémenter les méthodes suivantes :

```java
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**Remarque** : Un seul gestionnaire peut être ajouté à la bibliothèque, à la fois pour la passerelle et pour les terminaux connectés vers lesquels les demandes d'action sur les terminaux sont redirigées. L'implémentation doit créer une unité d'exécution ou un pool d'unités d'exécution pour gérer plusieurs demandes d'action sur les terminaux à la fois. Un exemple d'implémentation de gestionnaire qui utilise un pool d'unités d'exécution est illustré dans le [référentiel GitHub iot-gateway-samples ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java){: new_window}.

### Exemple d'implémentation de `handleReboot`

L'implémentation doit créer une unité d'exécution distincte et ajouter une logique pour réamorcer la passerelle et le terminal connecté et signaler l'état du réamorçage via l'objet `DeviceAction`. Après avoir reçu la demande, la passerelle doit d'abord informer le serveur de la prise en charge ou de l'échec avant d'effectuer réellement l'amorçage. Si l'exemple ne peut pas réamorcer le terminal ou si n'importe quelle autre erreur se produit lors du réamorçage, la passerelle peut mettre à jour l'état dans le message facultatif. Un exemple d'implémentation de réamorçage d'un terminal Raspberry Pi est illustré dans l'exemple de code suivant :

```java
public void handleReboot(DeviceAction action) {
	ProcessBuilder processBuilder = null;
    Process p = null;
    processBuilder = new ProcessBuilder("sudo", "shutdown", "-r", "now");
    boolean status = false;
    try {
		p = processBuilder.start();
        // wait for say 2 minutes before giving it up
        status = waitForCompletion(p, 2);
    } catch (IOException e) {
		action.setMessage(e.getMessage());
    } catch (InterruptedException e) {
		action.setMessage(e.getMessage());
    }
    if(status == false) {
		action.setStatus(DeviceAction.Status.FAILED);
    }
}
```

La totalité de l'exemple d'implémentation de gestionnaire qui utilise un pool d'unités d'exécution est illustrée dans le [référentiel GitHub iot-gateway-samples ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java){: new_window}.


### Exemple d'implémentation de `handleFactoryReset`

L'implémentation doit créer une unité d'exécution distincte et ajouter une logique pour réinitialiser la passerelle et le terminal connecté et signaler l'état de la réinitialisation via l'objet DeviceAction. Après avoir reçu la demande, la passerelle doit d'abord informer le serveur de la prise en charge ou de l'échec avant d'effectuer réellement la réinitialisation. Un exemple d'implémentation de la réinitialisation avec les paramètres d'usine est illustré dans l'exemple de code suivant :

```java
public void handleFactoryReset(DeviceAction action) {
	try {
		// code to perform Factory reset
    } catch (IOException e) {
		action.setMessage(e.getMessage());
    }
    if(status == false) {
		action.setStatus(DeviceAction.Status.FAILED);
    }
}
```

### Etape 3 : Ajouter le gestionnaire à `ManagedGateway`

Lorsqu'un gestionnaire est créé, il doit être ajouté à l'instance `ManagedGateway` de sorte que la bibliothèque client Java appelle la méthode correspondante lorsqu'une demande d'action sur les terminaux est émise par {{site.data.keyword.iot_short}}.

```java
GatewayActionHandlerSample actionHandler = new GatewayActionHandlerSample();
mgdGateway.addDeviceActionHandler(actionHandler);
```

Pour plus d'informations sur les actions sur les terminaux, voir [Demande de gestion des terminaux ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](../../devices/device_mgmt/requests.html#/device-actions-reboot#device-actions-reboot){: new_window}.

## Packages d'extension de gestion des terminaux
{: #dme}

Un package d'extension de gestion des terminaux (DME, Device Management Extension) est un document JSON qui définit un ensemble d'actions personnalisées de gestion de terminaux. Les actions
peuvent être initiées sur un ou plusieurs terminaux qui les acceptent. Les actions sont initiées soit à l'aide du tableau de bord {{site.data.keyword.iot_short}}, soit par l'intermédiaire
des API REST de gestion des terminaux. 

Pour plus d'informations sur les formats de package DME, référez-vous à [Extension de la gestion des terminaux](../../devices/device_mgmt/custom_actions.html).

### Prise en charge des actions de gestion des terminaux personnalisées

Les actions de gestion des terminaux qui sont définies dans un package
d'extension peuvent être lancées sur une passerelle ou par des terminaux connectés qui les acceptent. 

Un terminal spécifie les types d'actions qu'il accepte lorsqu'il publie une demande de gestion sur {{site.data.keyword.iot_short}}. 
Pour que le terminal puisse recevoir des actions personnalisées définies dans un package d'extension particulier,
il doit spécifier l'identificateur du bundle (regroupement) de cette extension dans l'objet supports en même temps qu'il publie une
demande de gestion.


La passerelle peut appeler l'API `manage()` avec la liste
des ID de bundle pour informer {{site.data.keyword.iot_short}} qu'elle-même ou
les terminaux connectés supportent les actions DME pour cette liste d'ID de bundle.


Le fragment de code suivant est utilisé pour publier une demande de gestion afin de faire savoir à
{{site.data.keyword.iot_short}} que cette passerelle supporte une action DME :


```java
List<String> bundleIds = new ArrayList<String>();
bundleIds.add("example-dme-actions-v1");

mgdGateway.sendGatewayManageRequest(0, false, false, bundleIds);
```

Le dernier paramètre spécifie l'action personnalisée que le terminal supporte.

De même, une passerelle peut appeler la méthode de terminal correspondante pour faire connaître le support d'actions DME par les terminaux connectés : 

```java
List<String> bundleIds = new ArrayList<String>();
bundleIds.add("example-dme-actions-v1");

mgdGateway.sendDeviceManageRequest(typeId, deviceId, 0, false, false, bundleIds);
```

### Traitement des actions de gestion des terminaux personnalisées

Lorsqu'une action personnalisée est initiée sur une passerelle ou un terminal connecté à {{site.data.keyword.iot_short}},
un message MQTT est publié à destination de la passerelle.
Ce message contient les paramètres qui ont été spécifiés dans le cadre de la demande. La passerelle doit ajouter un CustomActionHandler pour permettre la réception et le traitement du message. Le message est retourné en
tant qu'instance de la classe `CustomAction`, dont les propriétés sont les suivantes :


| Propriété     | Type de données     | Description |
|----------------|----------------|----------------|
|`bundleId` |Chaîne | Un identificateur unique pour le package DME.|
|`actionId` |Chaîne|L'action personnalisée qui est lancée.|
|`typeId` |Chaîne|Le type de terminal sur lequel l'action personnalisée est lancée.|
|`deviceId` |Chaîne|Le terminal sur lequel l'action personnalisée est lancée.|
|`payload` |Chaîne|Le message proprement dit, contenant la liste des paramètres au format JSON.|
|`reqId` |Chaîne|L'ID de demande utilisé pour répondre à la demande d'action personnalisée.|

Le code suivant est un exemple d'implémentation d'un `CustomActionHandler` :

```java
import java.util.HashMap;
import java.util.Map;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;

import com.google.gson.JsonArray;
import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.ibm.iotf.client.CustomAction;
import com.ibm.iotf.client.CustomAction.Status;
import com.ibm.iotf.devicemgmt.CustomActionHandler;

public class MyCustomActionHandler extends CustomActionHandler implements Runnable {

	// A queue to hold & process the commands for smooth handling of MQTT messages
	private BlockingQueue<CustomAction> queue = new LinkedBlockingQueue<CustomAction>();
	// A map to hold the publish interval time for each device
	private Map<String, Long> intervalMap = new HashMap<String, Long>();

	@Override
	public void run() {
		while(true) {
			CustomAction action = null;
			try {
				action = queue.take();
				System.out.println(" "+action.getActionId()+ " "+action.getPayload());
				JsonArray fields = action.getPayload().get("d").getAsJsonObject().get("fields").getAsJsonArray();
				for(JsonElement field : fields) {
					JsonObject fieldObj = field.getAsJsonObject();
					if("PublishInterval".equals(fieldObj.get("field").getAsString())) {
						long val = fieldObj.get("value").getAsLong();
						String key = action.getTypeId() + ":" + action.getDeviceId();
						long publishInterval = val * 1000;
						intervalMap.put(key, publishInterval);
						System.out.println("Updated the publish interval to "+val);
					}
				}
				action.setStatus(Status.OK);

			} catch (InterruptedException e) {}
		}
	}

	public long getPublishInterval(String deviceType, String deviceId) {
		String key = deviceType + ":" + deviceId;
		Long val = intervalMap.get(key);
		if(val == null) {
			return 1000; // default is 1 second
		} else {
			return val.longValue();
		}
	}

	@Override
	public void handleCustomAction(CustomAction action) {
		try {
			queue.put(action);
			} catch (InterruptedException e) {
		}

	}
}
```

Lorsque le `CustomActionHandler` est ajouté à l'instance de `ManagedGateway`,
la méthode `handleCustomAction()` est appelée chaque fois qu'une action personnalisée est initiée par l'application.

L'exemple de code suivant montre comment ajouter le `CustomActionHandler` à l'instance de `ManagedGateway`.

```java
MyCustomActionHandler handler = new MyCustomActionHandler();
mgdGateway.addCustomActionHandler(handler);
```

Lorsque la passerelle reçoit le message d'action personnalisée, elle exécute l'action ou répond avec un code d'erreur indiquant la raison pour laquelle elle ne peut pas exécuter l'action.
La passerelle doit utiliser la méthode *setStatus()* pour fixer l'état de l'action : 

```java
action.setStatus(Status.OK);
```

Pour plus d'informations sur DME, consultez [Extension des demandes de gestion de terminal ![Icône de lien externe](../../../../icons/launch-glyph.svg "Icône de lien externe")](../../devices/device_mgmt/custom_actions.html){: new_window}.

## Ecoute des modifications d'attribut de terminal
{: #listen_device_attributes}

La bibliothèque client Java met à jour les objets correspondants chaque fois qu'une demande de mise à jour émane de {{site.data.keyword.iot_short}}. Ces demandes de mise à jour sont initiées par l'application de manière directe ou indirecte via une mise à jour de microprogramme à l'aide de l'API REST {{site.data.keyword.iot_short}}. En dehors de la mise à jour de ces attributs, la bibliothèque fournit un mécanisme au cours duquel la passerelle peut être avertie chaque fois qu'un attribut de terminal est mis à jour.

Les attributs qui peuvent être mis à jour par ce type d'opération sont l'emplacement, les métadonnées, les informations sur les terminaux et le microprogramme de la passerelle et des terminaux connectés.

Pour être avertie des modifications d'attribut, la passerelle doit ajouter un programme d'écoute de modification de propriété aux objets qui l'intéressent, comme illustré dans l'exemple de code suivant :

```java
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

La passerelle doit également implémenter la méthode `propertyChange()` à l'endroit où elle reçoit la notification, comme illustré dans l'exemple d'implémentation suivant :

```java
public void propertyChange(PropertyChangeEvent evt) {
	if(evt.getNewValue() == null) {
		return;
	}
	Object value = (Object) evt.getNewValue();
		switch(evt.getPropertyName()) {
		case "metadata":
            DeviceMetadata metadata = (DeviceMetadata) value;
            System.out.println("Received an updated metadata -- "+ metadata);
            break;

			case "location":
            DeviceLocation location = (DeviceLocation) value;
            System.out.println("Received an updated location -- "+ location);
            break;

			case "deviceInfo":
            DeviceInfo info = (DeviceInfo) value;
            System.out.println("Received an updated device info -- "+ info);
            break;

			case "mgmt.firmware":
            DeviceFirmware firmware = (DeviceFirmware) value;
            System.out.println("Received an updated device firmware -- "+ firmware);
            break;
    }
}
```

Pour plus d'informations sur la mise à jour des attributs de terminal, voir [Demande de gestion des terminaux ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/index.html#/update-device-attributes#update-device-attributes){: new_window}.

## Exemples
{: #samples}

Plusieurs exemples sont disponibles pour vous aider à connecter des passerelles et les terminaux situés derrière les passerelles à votre instance de {{site.data.keyword.iot_short_notm}}. Les exemples utilisent la bibliothèque client Java {{site.data.keyword.iot_short_notm}} et figurent dans le [référentiel GitHub d'exemples de passerelle ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples){: new_window}.

## Recettes
{: #recipes}

Pour obtenir une recette expliquant comment connecter un terminal Raspberry Pi en tant que passerelle gérée à {{site.data.keyword.iot_short_notm}} et comment gérer les terminaux connectés, voir [Raspberry Pi as a managed gateway in {{site.data.keyword.iot_short_notm}} ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/){: new_window}.

Cette recette explique comment utiliser le protocole de gestion des terminaux de {{site.data.keyword.iot_short_notm}} pour gérer un terminal Arduino Uno à partir d'un terminal Raspberry Pi qui agit en tant que passerelle et comment effectuer des opérations de gestion des terminaux, telles que le réamorçage du terminal ou l'ajout d'un programme d'esquisse.
