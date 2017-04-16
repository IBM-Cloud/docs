---

copyright:
  years: 2015, 2017
lastupdated: "2016-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Développement de terminaux gérés à l'aide de Java
{: #java_deviceManagement}

## Introduction
{: #introduction}

Dans {{site.data.keyword.iot_full}}, un terminal géré est un terminal qui peut effectuer des opérations de gestion des terminaux, telles que les mises à jour de microprogramme, d'emplacement et de diagnostic.
Vous pouvez utiliser la bibliothèque client Java {{site.data.keyword.iot_short}} et les informations fournies pour développer du code Java et faire de vos terminaux connectés des terminaux gérés. Des exemples sont également fournis pour vous aider à développer du code Java dans le but de connecter un terminal au service de gestion des terminaux et d'exécuter des opérations de gestion des terminaux.

Pour plus d'informations sur la façon dont vos applications peuvent utiliser la bibliothèque client Java pour interagir avec des terminaux, voir [Java pour les développeurs d'applications](../../applications/libraries/java.html).

## Gestion des terminaux
{: #device_management}

La fonction de [gestion des terminaux](../reference/device_mgmt.html) améliore le service {{site.data.keyword.iot_short_notm}} grâce à d'autres fonctionnalités relatives à la gestion des terminaux. Elle établit une distinction entre les terminaux gérés et les terminaux non gérés :

-   Les **terminaux gérés** sont définis comme des terminaux sur lesquels un agent de gestion est installé. L'agent de gestion envoie et reçoit des métadonnées de terminal et répond à des commandes de gestion des terminaux à partir de {{site.data.keyword.iot_short_notm}}.
-   Les **terminaux non gérés** sont des terminaux sur lesquels aucun agent de gestion des terminaux n'est installé. Tous les terminaux commencent leur cycle de vie en tant que terminaux non gérés et peuvent passer au statut de terminaux gérés en envoyant un message depuis un agent de gestion des terminaux à {{site.data.keyword.iot_short_notm}}.

## Connexion au service de gestion des terminaux de {{site.data.keyword.iot_short_notm}}
{: #connecting_dm_service}

## Création de données de terminal
{: #creating_device_data}

Le [modèle de terminal](../reference/device_model.html) décrit les métadonnées et les caractéristiques de gestion d'un terminal. La base de données de terminaux d'{{site.data.keyword.iot_short_notm}} représente la principale source d'informations sur les terminaux. Les applications et les terminaux gérés peuvent envoyer des mises à jour à la base de données, telles qu'un emplacement ou la progression d'une mise à jour de microprogramme. Dès que ces mises à jour sont reçues par {{site.data.keyword.iot_short_notm}}, la base de données de terminaux est mise à jour et les informations sont disponibles pour les applications.

`DeviceData` est le modèle de terminal de la bibliothèque client ibmiotf et inclut les objets suivants :

-   DeviceInfo (obligatoire)
-   DeviceLocation (obligatoire si le terminal prend en charge la mise à jour de l'emplacement)
-   DiagnosticErrorCode (obligatoire si le terminal doit mettre à jour le code d'erreur)
-   DiagnosticLog (obligatoire si le terminal doit mettre à jour les informations de journal)
-   DeviceFirmware (obligatoire si le terminal prend en charge les actions sur le microprogramme)
-   DeviceMetadata (facultatif)

L'exemple de code suivant montre comment créer l'objet obligatoire `DeviceInfo` en même temps qu'un objet `DeviceMetadata` facultatif avec des exemples de données :

```
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

Utilisez l'exemple de code suivant pour créer un objet `DeviceData` incluant les objets `DeviceInfo` et `DeviceMetadata` que vous avez créés dans l'exemple précédent.

  ```
  DeviceData deviceData = new DeviceData.Builder().
               deviceInfo(deviceInfo).
               metadata(metadata).
               build();
  ```

## Construction de ManagedDevice
{: #construct_managed_device}

`ManagedDevice` est une classe de terminaux qui connecte le terminal en tant que terminal géré à {{site.data.keyword.iot_short_notm}} et permet au terminal d'effectuer une ou plusieurs opérations de gestion des terminaux. Vous pouvez également utiliser une instance `ManagedDevice` pour effectuer des opérations de terminal normales, telles que la publication d'événements de terminal et l'écoute de commandes à partir d'une application.

`ManagedDevice` expose les constructeurs suivants pour prendre en charge différents modèles d'utilisateur :

**Constructeur 1**

Le constructeur 1 construit une instance `ManagedDevice` dans {{site.data.keyword.iot_short_notm}} en acceptant `DeviceData` et toutes les propriétés requises suivantes :

|Propriété |Description |
|:---|:---|
|`Organization-ID` |ID de votre organisation|
|`Device-Type` |Type de votre terminal. Généralement, deviceType regroupe des terminaux qui effectuent une tâche spécifique, par exemple, "weatherballoon".|
|`Device-ID` |ID de votre terminal. Généralement, pour un type de terminal donné, deviceId est un identificateur unique, par exemple, un numéro de série ou une adresse MAC.|
|`Authentication-Method` |Méthode d'authentification à utiliser. La seule valeur actuellement prise en charge est `token`.|
|`Authentication-Token` |Jeton d'authentification permettant d'établir une connexion sécurisée entre votre terminal et Watson IoT Platform.|


Le code suivant montre comment créer une instance `ManagedDevice` :

```
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Device-Type", "iotsample-arduino");
options.setProperty("Device-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

Si vous utilisez déjà une instance `DeviceClient`, vous constaterez que les noms des propriétés sont légèrement différents et vous refléterez les noms dans le tableau de bord {{site.data.keyword.iot_short_notm}}. Pour effectuer une migration depuis `DeviceClient` vers `ManagedDevice`, continuez d'utiliser le format antérieur en construisant l'instance `ManagedDevice` comme décrit dans l'exemple suivant :

```
Properties options = new Properties();
options.setProperty("org", "uguhsp");
options.setProperty("type", "iotsample-arduino");
options.setProperty("id", "00aabbccde03");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");
ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

**Constructeur 2**

Construisez une instance `ManagedDevice` en acceptant les instances `DeviceData` et `MqttClient`. Ce constructeur requiert que `DeviceData` soit créé avec des attributs de terminal supplémentaires, tels que Type de terminal et ID de terminal, comme décrit dans l'exemple suivant :

```
// Code that constructs the MqttClient (either Synchronous or Asynchronous MqttClient)
.....

// Code that constructs the DeviceData
DeviceData deviceData = new DeviceData.Builder().
             typeId("Device-Type").
             deviceId("Device-ID").
             deviceInfo(deviceInfo).
             metadata(metadata).
             build();

....
ManagedDevice managedDevice = new ManagedDevice(mqttClient, deviceData);
```

**Remarque :** Ce constructeur permet aux utilisateurs de terminal personnalisé de créer une instance `ManagedDevice` avec l'instance `MqttClient` déjà créée et connectée pour bénéficier des opérations de gestion des terminaux. Il est recommandé d'utiliser la bibliothèque pour toutes les fonctionnalités du terminal.

## Gestion

Le terminal `géré` peu appeler une méthode manage() pour participer aux activités de gestion des terminaux. La demande de gestion lance une demande de connexion en interne si le terminal n'est pas connecté à {{site.data.keyword.iot_short_notm}}.

```
managedDevice.manage();
```

Le terminal peut utiliser une méthode manage (durée de vie) surchargée pour enregistrer le terminal pendant une période donnée. La période spécifie la durée pendant laquelle le terminal doit envoyer une autre demande **Gérer le terminal** afin de ne pas être rétrogradé au statut de terminal non géré et marqué comme étant en mode veille.

```
managedDevice.manage(3600);
```

Pour plus d'informations sur l'opération `Manage`, voir la [documentation].

  [documentation]:../device_mgmt/operations/manage.html

## Méthode Unmanage

Un terminal peut appeler la méthode unmanage() lorsqu'il n'a plus besoin d'être géré. {{site.data.keyword.iot_short_notm}} n'envoie plus de nouvelles demandes de gestion des terminaux à ce terminal et toutes les demandes de gestion des terminaux à partir de ce terminal, autres qu'une demande **Gérer le terminal**, sont rejetées.

```
managedDevice.unmanage();
```

Pour plus d'informations sur l'opération `Unmanage`, voir la [documentation].

  [documentation]:../device_mgmt/operations/manage.html

## Mise à jour d'emplacement
{: #construct_location_update}
Les terminaux qui peuvent déterminer leur emplacement peuvent choisir d'avertir {{site.data.keyword.iot_short_notm}} que des modifications d'emplacement ont été apportées. Pour mettre à jour l'emplacement, le terminal doit créer une instance `DeviceData` d'abord avec l'objet `DeviceLocation`.

```
// Construct the location object with latitude, longitude and elevation
DeviceLocation deviceLocation = new DeviceLocation.Builder(30.28565, -97.73921).
                            elevation(10).
                            build();
DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceLocation(deviceLocation).
             metadata(metadata).
             build();
```

Lorsque le terminal est connecté à {{site.data.keyword.iot_short_notm}}, vous pouvez mettre à jour l'emplacement à l'aide de la méthode suivante :

```
int rc = deviceLocation.sendLocation();
if(rc == 200) {
        System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
            System.err.println("Failed to update the location");
}
```

Les mises à jour suivantes de l'emplacement de terminal peuvent être mises à jour en modifiant les propriétés de l'objet `DeviceLocation`, comme décrit dans l'exemple suivant :

```
int rc = deviceLocation.update(40.28, -98.33, 11);
if(rc == 200) {
    System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
    System.err.println("Failed to update the location");
}
```

La méthode update() informe {{site.data.keyword.iot_short_notm}} du nouvel emplacement.

Pour plus d'informations sur la mise à jour d'emplacements, voir la [documentation](../device_mgmt/operations/update.html) liée.



## Ajout et effacement de codes d'erreur
{: #appending_error_codes}

Les terminaux peuvent choisir d'informer {{site.data.keyword.iot_short_notm}} que leur statut d'erreur a changé. Pour envoyer des codes d'erreur, le terminal doit construire un objet `DiagnosticErrorCode`, comme décrit dans l'exemple suivant :

```
DiagnosticErrorCode errorCode = new DiagnosticErrorCode(0);

DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceErrorCode(errorCode).
             metadata(metadata).
             build();
```

Dès que le terminal est connecté à {{site.data.keyword.iot_short_notm}}, l'objet `ErrorCode` peut être envoyé en appelant la méthode send(), comme décrit ci-dessous :

```
errorCode.send();
```

Ensuite, tous les nouveaux objets `ErrorCodes` peuvent facilement être ajoutés à {{site.data.keyword.iot_short_notm}} en appelant la méthode append, comme décrit ci-dessous :

```
int rc = errorCode.append(500);
if(rc == 200) {
    System.out.println("Current Errorcode (" + errorCode + ")");
} else {
    System.out.println("Errorcode addition failed!");
}
```

De plus, les objets `ErrorCodes` peuvent être effacés de {{site.data.keyword.iot_short_notm}} en appelant la méthode clear(), comme décrit ci-dessous :

```
int rc = errorCode.clear();
if(rc == 200) {
    System.out.println("ErrorCodes are cleared successfully!");
} else {
    System.out.println("Failed to clear the ErrorCodes!");
}
```

## Ajout et effacement de messages de journal

Les terminaux peuvent choisir d'informer {{site.data.keyword.iot_short_notm}} que des modifications ont été apportées en ajoutant une nouvelle entrée de journal. Une entrée de journal inclut les informations suivantes :
- Message de journal
- Horodatage
- Gravité
- Données de diagnostic binaires codées en base 64 (facultatif)

Pour envoyer des messages de journal, le terminal doit construire un objet `DiagnosticLog`, comme décrit dans l'exemple suivant :

```
DiagnosticLog log = new DiagnosticLog(
            "Simple Log Message",
            new Date(),
            DiagnosticLog.LogSeverity.informational);

DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceLog(log).
             metadata(metadata).
             build();
```

Dès que le terminal est connecté à {{site.data.keyword.iot_short_notm}}, le message de journal peut être envoyé en appelant la méthode send(), comme décrit dans l'exemple suivant :

```
log.send();
```

Ensuite, les nouveaux messages de journal peuvent facilement être ajoutés à {{site.data.keyword.iot_short_notm}} en appelant la méthode append, comme décrit dans l'exemple suivant :

```
int rc = log.append("sample log", new Date(), DiagnosticLog.LogSeverity.informational);

if(rc == 200) {
    System.out.println("Current Log (" + log + ")");
} else {
    System.out.println("Log Addition failed");
}
```

Ensuite, les messages de journal peuvent être effacés de {{site.data.keyword.iot_short_notm}} en appelant la méthode clear, comme décrit dans l'exemple suivant :

```
rc = log.clear();
if(rc == 200) {
    System.out.println("Logs are cleared successfully");
} else {
    System.out.println("Failed to clear the Logs")
}
```

Les opérations de diagnostic des terminaux fournissent des informations sur les erreurs des terminaux mais ne transmettent pas d'informations de diagnostic sur la connexion des terminaux à {{site.data.keyword.iot_short_notm}}.

Pour plus d'informations sur l'opération de diagnostic, voir la [documentation](../device_mgmt/operations/diagnostics.html).

## Actions sur le microprogramme
{: #firmware_actions}

Le processus de mise à jour du microprogramme est scindé en deux actions distinctes :

* Téléchargement du microprogramme
* Mise à jour du microprogramme

Le terminal doit exécuter les activités suivantes pour prendre en charge les actions sur le microprogramme :

**1. Construire un objet DeviceFirmware**

Pour effectuer des actions sur le microprogramme, le terminal doit construire l'objet `DeviceFirmware` et l'ajouter à `DeviceData`, comme décrit ci-dessous :

```
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

ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
managedDevice.connect();
```

L'objet `DeviceFirmware` représente le microprogramme en cours du terminal et sera utilisé pour signaler le statut des actions de téléchargement de microprogramme et de mise à jour de microprogramme sur {{site.data.keyword.iot_short_notm}}.

**2. Informer le serveur de la prise en charge de l'action sur le microprogramme**

Le terminal doit associer l'action sur le microprogramme à la valeur true pour permettre au serveur de lancer la demande de microprogramme. Cette opération peut être effectuée en appelant la méthode suivante avec une valeur booléenne :

```
managedDevice.supportsFirmwareActions(true);
managedDevice.manage();
```

Comme la demande de gestion informe {{site.data.keyword.iot_short_notm}} de la prise en charge de l'action sur le microprogramme, la méthode manage() doit être appelée juste après la définition de la prise en charge de l'action sur le microprogramme.

**3. Créer le gestionnaire d'action sur le microprogramme**

Pour que l'action sur le microprogramme soit prise en charge, le terminal doit créer un gestionnaire et l'ajouter à `ManagedDevice`. Le gestionnaire doit étendre une classe `DeviceFirmwareHandler` et implémenter les méthodes suivantes :

```
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**3.1 Exemple d'implémentation de downloadFirmware**

L'implémentation doit ajouter une logique pour télécharger le microprogramme et signaler le statut du téléchargement à l'aide d'un objet `DeviceFirmware`. Si l'opération de téléchargement de microprogramme aboutit, le statut prend la valeur `DOWNLOADED`, puis `UpdateStatus` prend la valeur `SUCCESS`.

Si une erreur se produit lors du téléchargement de microprogramme, l'état prend la valeur `IDLE`, puis `updateStatus` prend l'une des valeurs de statut d'erreur suivantes :

* `OUT_OF_MEMORY
* CONNECTION_LOST
* INVALID_URI`

L'exemple suivant illustre une implémentation de téléchargement de microprogramme pour un terminal Raspberry Pi :

```
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
            // use the timestamp as the name
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

Un terminal peut vérifier l'intégrité de l'image de microprogramme téléchargée à l'aide du vérificateur et signaler le statut à {{site.data.keyword.iot_short_notm}}. Le vérificateur peut être défini par le terminal au démarrage (lors de la création de l'objet DeviceFirmware) ou dans le cadre de la demande de téléchargement du microprogramme de l'application. Un exemple de code de vérification est présenté ci-dessous :

```
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
    System.out.println("Download firmware checksum verification failed.. "
            + "Expected "+verifier + " found "+md5);
    return false;
}
```

Pour la totalité du code, voir l'exemple de gestion des terminaux [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java).



**3.2 Exemple d'implémentation de updateFirmware**

L'implémentation doit ajouter une logique pour installer le microprogramme téléchargé et signaler le statut de la mise à jour via l'objet `DeviceFirmware`. Si l'opération de mise à jour de microprogramme aboutit, l'état du microprogramme doit prendre la valeur IDLE et `updateStatus` doit prendre la valeur `SUCCESS`.

Si une erreur se produit lors de la mise à jour de microprogramme, `updateStatus` doit prendre l'une des valeurs de statut d'erreur suivantes :

`* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE`

Un exemple d'implémentation de la mise à jour du microprogramme du terminal Raspberry Pi est présenté ci-dessous :

```
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

La totalité du code est consultable dans l'exemple de gestion des terminaux [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java).


**4. Ajouter le gestionnaire à ManagedDevice**

Le gestionnaire créé doit être ajouté à l'instance ManagedDevice de sorte que la bibliothèque client ibmiotf appelle la méthode correspondante lorsqu'une demande d'action sur le microprogramme est émise par {{site.data.keyword.iot_short_notm}}.

```
DeviceFirmwareHandlerSample fwHandler = new DeviceFirmwareHandlerSample();
deviceData.addFirmwareHandler(fwHandler);
```

Pour plus d'information sur l'action sur le microprogramme, voir [cette page](../device_mgmt/operations/firmware_actions.html).

## Actions sur les terminaux

{{site.data.keyword.iot_short_notm}} prend en charge les actions sur les terminaux décrites ci-dessous :

* Réamorcer
* Réinitialiser avec les paramètres d'usine

Le terminal doit effectuer les opérations suivantes pour prendre en charge les actions sur les terminaux :

**1. Informer le serveur de la prise en charge des actions sur les terminaux**

Pour effectuer les opérations Réamorcer et Réinitialiser avec les paramètres d'usine, le terminal doit d'abord avertir {{site.data.keyword.iot_short_notm}} qu'il prend en charge ces opérations. Pour cela, il appelle la méthode suivante avec une valeur booléenne :

```
managedDevice.supportsDeviceActions(true);
    managedDevice.manage();
```

Comme la demande de gestion informe {{site.data.keyword.iot_short_notm}} de la prise en charge de l'action sur le terminal, la méthode manage() doit être appelée juste après la définition de la prise en charge de l'action sur le terminal.

**2. Créer le gestionnaire d'action sur le terminal**

Pour que l'action sur le terminal soit prise en charge, le terminal doit créer un gestionnaire et l'ajouter à ManagedDevice. Le gestionnaire doit étendre une classe DeviceActionHandler et implémenter les méthodes suivantes :

```
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**2.1 Exemple d'implémentation de handleReboot**

L'implémentation doit ajouter une logique permettant de réinitialiser le terminal et signaler le statut du réamorçage via l'objet DeviceAction. Le terminal doit mettre à jour le statut avec un message facultatif uniquement en cas d'échec (car l'opération qui aboutit redémarre le terminal et le code de terminal n'a aucun contrôle pour mettre à jour {{site.data.keyword.iot_short_notm}}). Un exemple d'implémentation du réamorçage pour le terminal Raspberry Pi est présenté ci-dessous :

```
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

La totalité du code est consultable dans l'exemple de gestion des terminaux [DeviceActionHandlerSample].

  [DeviceActionHandlerSample]: https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java

**2.2 Exemple d'implémentation de handleFactoryReset**

L'implémentation doit ajouter une logique permettant de réinitialiser le terminal avec les paramètres d'usine et signaler le statut via l'objet DeviceAction. Le terminal doit mettre à jour le statut avec un message facultatif uniquement en cas d'échec (car dans le cadre de ce processus, le terminal redémarre et n'a aucun contrôle pour mettre à jour le statut {{site.data.keyword.iot_short_notm}}). Le squelette de l'implémentation de réinitialisation avec les paramètres d'usine est présenté ci-dessous :

```
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

**3. Ajouter le gestionnaire à ManagedDevice**

Le gestionnaire créé doit être ajouté à l'instance ManagedDevice de sorte que la bibliothèque client ibmiotf appelle la méthode correspondante lorsqu'une demande d'action sur le terminal est émise par {{site.data.keyword.iot_short_notm}}.

```
DeviceActionHandlerSample actionHandler = new DeviceActionHandlerSample();
deviceData.addDeviceActionHandler(actionHandler);
```

Pour plus d'informations sur l'action sur le terminal, voir [cette page](../device_mgmt/operations/device_actions.html).



## Ecoute des modifications d'attribut de terminal
{: #listen_device_attribute}

Cette bibliothèque client ibmiotf met à jour les objets correspondants chaque fois qu'une demande de mise à jour émane de {{site.data.keyword.iot_short_notm}}. Ces demandes de mise à jour sont initiées par l'application de manière directe ou indirecte (mise à jour de microprogramme) via l'API REST {{site.data.keyword.iot_short_notm}}. En dehors de la mise à jour de ces attributs, la bibliothèque fournit un mécanisme au cours duquel le terminal peut être averti chaque fois qu'un attribut de terminal est mis à jour.

Les attributs qui peuvent être mis à jour par cette opération sont `location`, `metadata`, `device information` et `firmware`.

Pour recevoir une notification, le terminal doit ajouter un code d'écoute des modifications de propriétés sur les objets qui l'intéressent.

```
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

En outre, le terminal doit implémenter la méthode `propertyChange()` à l'endroit où il reçoit la notification. L'exemple suivant illustre cette implémentation :

```
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

Pour plus d'informations sur la mise à jour des attributs de terminal, voir [cette page](../device_mgmt/operations/update.html).

## Exemples
{: #examples}

-   [SampleRasPiDMAgent](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgent.java) - Exemple de code d'agent indiquant comment effectuer différentes opérations de gestion des terminaux sur Raspberry Pi.
-   [SampleRasPiManagedDevice](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiManagedDevice.java) - Exemple de code indiquant comment effectuer des opérations sur les terminaux et des opérations de gestion.
-   [SampleRasPiDMAgentWithCustomMqttAsyncClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttAsyncClient.java) - Exemple de code d'agent avec code MqttAsyncClient personnalisé.
-   [SampleRasPiDMAgentWithCustomMqttClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttClient.java) - Exemple de code d'agent avec code MqttClient personnalisé.
-   [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java) - Exemple d'implémentation de FirmwareHandler pour le terminal Raspberry Pi.
-   [DeviceActionHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java) - Exemple d'implémentation de DeviceActionHandler
-   [ManagedDeviceWithLifetimeSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/ManagedDeviceWithLifetimeSample.java) - Exemple indiquant comment envoyer une demande de gestion standard avec une durée de vie définie.
-   [DeviceAttributesUpdateListenerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceAttributesUpdateListenerSample.java) - Exemple de code d'écoute indiquant comment détecter différentes modifications apportées à des attributs de terminal.
-   [NonBlockingDiagnosticsErrorCodeUpdateSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/NonBlockingDiagnosticsErrorCodeUpdateSample.java) - Exemple indiquant comment ajouter un code d'erreur sans attendre la réponse du serveur.

## Recettes
{: #Recipes}

Voir [la recette](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-managed-device-to-ibm-iot-foundation/) qui montre comment connecter le terminal Raspberry Pi en tant que terminal géré à {{site.data.keyword.iot_short_notm}} pour effectuer différentes opérations de gestion des terminaux étape par étape à l'aide de cette bibliothèque client.
