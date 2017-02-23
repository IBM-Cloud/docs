---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Sviluppo dei dispositivi gestiti utilizzando Java
{: #java_deviceManagement}

##Introduzione
{: #introduction}

In {{site.data.keyword.iot_full}}, un dispositivo gestito è un dispositivo che può eseguire operazioni di gestione dispositivo, come gli aggiornamenti del firmware, dell'ubicazione e della diagnostica.
Utilizzando la libreria client Java™ {{site.data.keyword.iot_short}} e le informazioni fornite, puoi sviluppare il codice Java per modificare i tuoi dispositivi collegati in dispositivi gestiti. Vengono inoltre forniti degli esempi per aiutarti nello sviluppo del codice Java per collegare un dispositivo al servizio di gestione del dispositivo ed eseguire le operazioni di gestione del dispositivo.

Per ulteriori informazioni su come le tue applicazioni possono utilizzare la libreria client Java per interagire con i dispositivi, consulta [Java per gli sviluppatori dell'applicazione](../../applications/libraries/java.html).

## Gestione del dispositivo
{: #device_management}

La funzione [gestione del dispositivo](../reference/device_mgmt.html) migliora il servizio {{site.data.keyword.iot_short_notm}} con l'aggiunta di ulteriori funzionalità per la gestione dei dispositivi. La gestione dispositivo effettua una distinzione tra i dispositivi gestiti e non gestiti:

-   **Dispositivi gestiti** sono definiti come dispositivi che hanno un agent di gestione installato. L'agent di gestione invia e riceve i metadati del dispositivo e risponde ai comandi di gestione del dispositivo da {{site.data.keyword.iot_short_notm}}.
-   **Dispositivi non gestiti** sono tutti i dispositivi che non hanno un agent di gestione del dispositivo. Tutti i dispositivi iniziano il loro ciclo di vita come dispositivi non gestiti e possono diventare dispositivi gestiti inviando un messaggio da un agent di gestione del dispositivo a {{site.data.keyword.iot_short_notm}}.

## Connessione al servizio di gestione del dispositivo {{site.data.keyword.iot_short_notm}}
{: #connecting_dm_service}

## Creazione dei dati del dispositivo
{: #creating_device_data}

Il [modello dispositivo](../reference/device_model.html) descrive le caratteristiche di gestione e metadati di un dispositivo. Il database del dispositivo in {{site.data.keyword.iot_short_notm}} è l'origine principale delle informazioni sul dispositivo. Le applicazioni e i dispositivi gestiti sono in grado di inviare gli aggiornamenti al database come un'ubicazione o il progresso di un aggiornamento firmware. Una volta che sono stati ricevuti questi aggiornamenti da {{site.data.keyword.iot_short_notm}}, il database del dispositivo viene aggiornato, rendendo le informazioni disponibili per le applicazioni.

`DeviceData` è il modello del dispositivo nella libreria client ibmiotf e include i seguenti oggetti:

-   DeviceInfo (obbligatorio)
-   DeviceLocation (richiesto se il dispositivo supporta l'aggiornamento di ubicazione)
-   DiagnosticErrorCode (richiesto se il dispositivo desidera aggiornare ErrorCode)
-   DiagnosticLog (richiesto se il dispositivo desidera aggiornare le informazioni log)
-   DeviceFirmware (richiesto se il dispositivo supporta le azioni firmware)
-   DeviceMetadata (facoltativo)

Il seguente esempio di codice mostra come creare l'oggetto obbligatorio `DeviceInfo` insieme a un oggetto `DeviceMetadata` facoltativo con dati di esempio:

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
  * Crea un oggetto DeviceMetadata
 **/
JsonObject data = new JsonObject();
data.addProperty("customField", "customValue");
DeviceMetadata metadata = new DeviceMetadata(data);
```

Utilizza il seguente esempio di codice per creare un oggetto `DeviceData` che include gli oggetti `DeviceInfo` e `DeviceMetadata` che hai creato nel precedente esempio.

  ```
  DeviceData deviceData = new DeviceData.Builder().
               deviceInfo(deviceInfo).
               metadata(metadata).
               build();
  ```

## Costruisci ManagedDevice
{: #construct_managed_device}

`ManagedDevice` è una classe del dispositivo che collega il dispositivo come un dispositivo gestito a {{site.data.keyword.iot_short_notm}} e lo abilita ad eseguire una o più operazioni di gestione del dispositivo. Puoi anche utilizzare un'istanza `ManagedDevice` per eseguire le operazioni del dispositivo normali come la pubblicazione di eventi del dispositivo e l'elenco dei comandi da un'applicazione.

`ManagedDevice` espone i seguenti constructor, che supportano i diversi modelli utente:

**Constructor uno**

Il constructor uno crea un'istanza `ManagedDevice` in {{site.data.keyword.iot_short_notm}} accettando `DeviceData` e tutte le seguenti proprietà richieste:

|Proprietà |Descrizione |
|:---|:---|
|`Organization-ID` |Il tuo ID dell'organizzazione|
|`Device-Type` |Il tipo del tuo dispositivo. Generalmente, il deviceType è un raggruppamento di dispositivi che esegue un'attività specifica, ad esempio "weatherballoon".|
|`Device-ID` |L'ID del tuo dispositivo. Generalmente, per determinato tipo di dispositivo, il deviceId è un identificativo univoco di tale dispositivo, ad esempio un numero seriale o un indirizzo MAC.|
|`Authentication-Method` |Il metodo di autenticazione da utilizzare. L'unico valore al momento supportato è `token`.|
|`Authentication-Token` |Un token di autenticazione per la connessione sicura al tuo dispositivo su Watson IoT Platform.|


Il seguente codice illustra come puoi creare un'istanza `ManagedDevice`:

```
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Device-Type", "iotsample-arduino");
options.setProperty("Device-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

Se stai utilizzando un'istanza `DeviceClient`, avrai notato che i nomi delle proprietà sono leggermente differenti e rispecchiano i nomi nel dashboard {{site.data.keyword.iot_short_notm}}. Per migrare da `DeviceClient` a `ManagedDevice` puoi continuare ad utilizzare il precedente formato creando l'istanza `ManagedDevice` come descritto nel seguente esempio:

```
Properties options = new Properties();
options.setProperty("org", "uguhsp");
options.setProperty("type", "iotsample-arduino");
options.setProperty("id", "00aabbccde03");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");
ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

**Constructor due**

Crea un'istanza `ManagedDevice` accettando le istanze `DeviceData` e `MqttClient`. Questo constructor richiede che `DeviceData` sia creata con ulteriori attributi del dispositivo come il tipo e l'ID del dispositivo, come descritto nel seguente esempio:

```
// Codice che crea MqttClient (sia MqttClient sincrono che asincrono)
.....

// Codice che crea DeviceData
DeviceData deviceData = new DeviceData.Builder().
             typeId("Device-Type").
             deviceId("Device-ID").
             deviceInfo(deviceInfo).
             metadata(metadata).
             build();

....
ManagedDevice managedDevice = new ManagedDevice(mqttClient, deviceData);
```

**Nota:** questo constructor aiuta gli utenti del dispositivo personalizzato a creare un'istanza `ManagedDevice` con l'istanza `MqttClient` già creata e collegata per usufruire delle operazioni di gestione del dispositivo. Tuttavia, agli utenti è consigliato di utilizzare la libreria per tutte le funzionalità del dispositivo.

## Gestione

Il dispositivo `Manage` può richiamare il metodo di manage() in modo che partecipi alle attività di gestione del dispositivo. La richiesta di gestione avvia una richiesta di connessione internamente se il dispositivo non è già connesso a {{site.data.keyword.iot_short_notm}}.

```
managedDevice.manage();
```

Il dispositivo che utilizza il metodo overloaded manage (lifetime) per registrare il dispositivo per un determinato intervallo di tempo. L'intervallo di tempo specifica l'arco di tempo in cui il dispositivo deve inviare un'altra richiesta di **Gestione del dispositivo** per evitare di venire riconvertito in un dispositivo non gestito ed essere contrassegnato come inattivo.

```
managedDevice.manage(3600);
```

Per ulteriori informazioni sull'operazione `Manage`, consulta la [documentazione].

  [documentation]:../device_mgmt/operations/manage.html

## Annulla gestione

Un dispositivo può richiamare il metodo unmanage() quando non è più necessario che sia un dispositivo gestito. {{site.data.keyword.iot_short_notm}} non invierà più nuove richieste di gestione del dispositivo a questo dispositivo e tutte le richieste di gestione da questo dispositivo saranno rifiutate con l'eccezione della richiesta di **Gestione del dispositivo**.

```
managedDevice.unmanage();
```

Per ulteriori informazioni sull'operazione `Unmanage`, consulta la [documentazione].

  [documentation]:../device_mgmt/operations/manage.html

## Aggiornamento dell'ubicazione
{: #construct_location_update}
I dispositivi che possono determinare la loro ubicazione possono scegliere di inviare notifiche a {{site.data.keyword.iot_short_notm}} sulle modifiche dell'ubicazione. Per aggiornare l'ubicazione, il dispositivo deve prima creare un'istanza `DeviceData` con l'oggetto `DeviceLocation`.

```
// Crea l'oggetto di ubicazione con latitudine, longitudine e altitudine
DeviceLocation deviceLocation = new DeviceLocation.Builder(30.28565, -97.73921).
                            elevation(10).
                            build();
DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceLocation(deviceLocation).
             metadata(metadata).
             build();
```

Quando il dispositivo si collega a {{site.data.keyword.iot_short_notm}}, puoi aggiornare l'ubicazione utilizzando il seguente metodo:

```
int rc = deviceLocation.sendLocation();
if(rc == 200) {
        System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
            System.err.println("Failed to update the location");
}
```

I successivi aggiornamenti dell'ubicazione del dispositivo possono essere effettuati modificando le proprietà dell'oggetto `DeviceLocation`, come descritto nel seguente esempio:

```
int rc = deviceLocation.update(40.28, -98.33, 11);
if(rc == 200) {
    System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
    System.err.println("Failed to update the location");
}
```

Il metodo update() fornisce informazioni a {{site.data.keyword.iot_short_notm}} sulla nuova ubicazione.

Per ulteriori informazioni sull'aggiornamento delle ubicazioni, consulta la documentazione [](../device_mgmt/operations/update.html) collegata.



## Aggiunta e cancellazione dei codici di errore
{: #appending_error_codes}

I dispositivi possono scegliere di inviare notifiche a {{site.data.keyword.iot_short_notm}} sulle modifiche nei loro stati di errore. Per inviare i codici di errore, il dispositivo ha bisogno di creare un oggetto `DiagnosticErrorCode` come descritto nel seguente esempio:

```
DiagnosticErrorCode errorCode = new DiagnosticErrorCode(0);

DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceErrorCode(errorCode).
             metadata(metadata).
             build();
```

Non appena viene collegato il dispositivo a {{site.data.keyword.iot_short_notm}}, `ErrorCode` può essere inviato richiamando il metodo send() nel seguente modo:

```
errorCode.send();
```

Successivamente, ogni nuovo `ErrorCodes` può essere facilmente aggiunto a {{site.data.keyword.iot_short_notm}} richiamando il metodo append nel seguente modo:

```
int rc = errorCode.append(500);
if(rc == 200) {
    System.out.println("Current Errorcode (" + errorCode + ")");
} else {
    System.out.println("Errorcode addition failed!");
}
```

Inoltre, `ErrorCodes` può essere cancellato {{site.data.keyword.iot_short_notm}} richiamando il metodo clear() nel seguente modo:

```
int rc = errorCode.clear();
if(rc == 200) {
    System.out.println("ErrorCodes are cleared successfully!");
} else {
    System.out.println("Failed to clear the ErrorCodes!");
}
```

## Aggiunta e cancellazione dei messaggi di log

I dispositivi possono scegliere di inviare notifiche a {{site.data.keyword.iot_short_notm}} sulle modifiche aggiungendo una nuova voce di log. Una voce di log include le seguenti informazioni:
- Messaggio di log
- Data/ora
- Severità
- Dati di diagnostica binari basati su base64 (facoltativo)

Per inviare i messaggi di log, il dispositivo ha bisogno di creare un oggetto `DiagnosticLog` come descritto nel seguente esempio:

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

Non appena viene collegato il dispositivo a {{site.data.keyword.iot_short_notm}}, il messaggio di log può essere inviato richiamando il metodo send() come descritto nel seguente esempio:

```
log.send();
```

Successivamente, tutti i messaggi di log possono essere facilmente aggiunti a {{site.data.keyword.iot_short_notm}} richiamando il metodo append, come illustrato nel seguente esempio:

```
int rc = log.append("sample log", new Date(), DiagnosticLog.LogSeverity.informational);

if(rc == 200) {
    System.out.println("Current Log (" + log + ")");
} else {
    System.out.println("Log Addition failed");
}
```

Inoltre, i messaggi di log possono essere eliminati da {{site.data.keyword.iot_short_notm}} richiamando il metodo clear, come illustrato nel seguente esempio:

```
rc = log.clear();
if(rc == 200) {
    System.out.println("Logs are cleared successfully");
} else {
    System.out.println("Failed to clear the Logs")
}
```

Le operazioni di diagnostica del dispositivo sono pensate per fornire informazioni sugli errori del dispositivo e non forniscono informazioni di diagnostica relative alla connessione dei dispositivi a {{site.data.keyword.iot_short_notm}}.

Per ulteriori informazioni sull'operazione di diagnostica, fai riferimento alla documentazione [](../device_mgmt/operations/diagnostics.html).

## Azioni firmware
{: #firmware_actions}

Il processo di aggiornamento Firmware è diviso in due azioni distinte:

* Scaricamento del firmware
* Aggiornamento del firmware

Il dispositivo deve completare le seguenti attività per supportare le azioni firmware:

**1. Creare l'oggetto DeviceFirmware**

Per eseguire le azioni firmware il dispositivo ha bisogno di creare l' oggetto `DeviceFirmware` e aggiungerlo a `DeviceData` nel seguente modo:

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

L'oggetto `DeviceFirmware` rappresenta il firmware corrente del dispositivo e sarà utilizzato per notificare lo stato delle azioni di scaricamento e aggiornamento del firmware a {{site.data.keyword.iot_short_notm}}.

**2. Informare il server sul supporto dell'azione firmware**

Il dispositivo deve impostare l'indicatore dell'azione firmware su true per consentire al server di avviare la richiesta firmware. Ciò può essere eseguito richiamando il seguente metodo con un valore booleano:

```
managedDevice.supportsFirmwareActions(true);
managedDevice.manage();
```

Come la richiesta di gestione invia le informazioni a {{site.data.keyword.iot_short_notm}} sul supporto dell'azione firmware, il metodo manage() deve essere richiamato subito dopo la configurazione del supporto dell'azione firmware.

**3. Creare il gestore dell'azione firmware**

Per supportare l'azione firmware, il dispositivo deve creare un gestore e aggiungerlo a `ManagedDevice`. Il gestore deve estendere una classe `DeviceFirmwareHandler` e implementare i seguenti metodi:

```
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**3.1 Implementazione di esempio di downloadFirmware**

L'implementazione deve aggiungere la logica di scaricamento del firmware e notificare lo stato dello scaricamento utilizzando un oggetto `DeviceFirmware`. Se l'operazione di scaricamento del firmware ha esito positivo, lo stato viene quindi impostato su `DOWNLOADED` e `UpdateStatus` viene impostato su `SUCCESS`.

Se si verifica un errore durante lo scaricamento del firmware, lo stato viene impostato su `IDLE` e `updateStatus` deve essere impostato su uno dei seguenti valori di stato dell'errore:

* `OUT_OF_MEMORY
* CONNECTION_LOST
* INVALID_URI`

Il seguente esempio descrive un'implementazione di scaricamento del firmware per un dispositivo Raspberry Pi:

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
            // utilizza la data/ora come nome
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
            //Non è presente alcun dato da leggere, imposta l'errore
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.INVALID_URI);
        }
    } catch(MalformedURLException me) {
        // URL non valido, imposta lo stato per rispecchiarlo,
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

Un dispositivo può controllare l'integrità dell'immagine firmware scaricata utilizzando il verificatore e notificare lo stato a {{site.data.keyword.iot_short_notm}}. Il verificatore può essere impostato dal dispositivo durante l'avvio (durante la creazione dell'oggetto DeviceFirmware) oppure come parte della richiesta Scaricamento del firmware da parte dell'applicazione. Un codice di esempio per eseguire la stessa verifica è illustrato di seguito:

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

Per il codice completo, consulta l'esempio di gestione del dispositivo [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java).



**3.2 Implementazione di esempio di updateFirmware**

L'implementazione deve aggiungere la logica per installare il firmware scaricato e notificare lo stato dell'aggiornamento tramite l'oggetto `DeviceFirmware`. Se l'operazione di aggiornamento del firmware ha esito positivo, lo stato del firmware deve essere impostato su In sospeso e `updateStatus` deve essere impostato su `SUCCESS`.

Se si verifica un errore durante l'aggiornamento del firmware, `updateStatus` deve essere impostato su uno dei valori dello stato di errore illustrati di seguito:

`* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE`

Un'implementazione dell'aggiornamento del firmware per un dispositivo Raspberry Pi è illustrata di seguito:

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

Il codice completo può essere trovato nell'esempio di gestione del dispositivo [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java).


**4. Aggiungere il gestore a ManagedDevice**

Il gestore creato deve essere aggiunto all'istanza ManagedDevice in modo che la libreria client ibmiotf richiami il metodo corrispondente quando viene effettuata una richiesta dell'azione firmware da {{site.data.keyword.iot_short_notm}}.

```
DeviceFirmwareHandlerSample fwHandler = new DeviceFirmwareHandlerSample();
deviceData.addFirmwareHandler(fwHandler);
```

Fai riferimento a [questa pagina](../device_mgmt/operations/firmware_actions.html) per ulteriori informazioni sull'azione firmware.

## Azioni dispositivo

{{site.data.keyword.iot_short_notm}} supporta le seguenti azioni del dispositivo:

* Riavvio
* Ripristino impostazioni predefinite

Il dispositivo deve completare le seguenti attività per supportare le azioni dispositivo:

**1. Informare il server sul supporto delle azioni del dispositivo**

Per eseguire un riavvio o una reimpostazione delle impostazioni predefinite, il dispositivo deve prima inviare informazioni a {{site.data.keyword.iot_short_notm}} sul suo supporto. Ciò può essere eseguito richiamando il seguente metodo con un valore booleano:

```
managedDevice.supportsDeviceActions(true);
    managedDevice.manage();
```

Come la richiesta di gestione invia le informazioni a {{site.data.keyword.iot_short_notm}} sul supporto dell'azione del dispositivo, il metodo manage() deve essere richiamato subito dopo la configurazione del supporto dell'azione del dispositivo.

**2. Creare il gestore dell'azione del dispositivo**

Per supportare l'azione dispositivo, il dispositivo deve creare un gestore e aggiungerlo a ManagedDevice. Il gestore deve estendere una classe DeviceActionHandler e fornire l'implementazione dei seguenti metodi:

```
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**2.1 Implementazione di esempio di handleReboot**

L'implementazione deve aggiungere una logica per riavviare il dispositivo e notificare lo stato del riavvio tramite l'oggetto DeviceAction. Il dispositivo deve aggiornare lo stato con un messaggio facoltativo solo se è presente un malfunzionamento (perché l'operazione con esito positivo riavvia il dispositivo e il codice del dispositivo non avrà il controllo per aggiornare {{site.data.keyword.iot_short_notm}}). Un'implementazione di esempio del riavvio per un dispositivo Raspberry Pi è illustrata di seguito:

```
public void handleReboot(DeviceAction action) {
    ProcessBuilder processBuilder = null;
    Process p = null;
    processBuilder = new ProcessBuilder("sudo", "shutdown", "-r", "now");
    boolean status = false;
    try {
        p = processBuilder.start();
        // attendi due minuti prima di fornire
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

Il codice completo può essere trovato nell'esempio di gestione del dispositivo [DeviceActionHandlerSample].

  [DeviceActionHandlerSample]: https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java

**2.2 Implementazione di esempio di handleFactoryReset**

L'implementazione deve aggiungere una logica per reimpostare il dispositivo alle impostazioni di fabbrica e notificare lo stato tramite l'oggetto DeviceAction. Il dispositivo deve aggiornare lo stato con un messaggio facoltativo solo se è presente un malfunzionamento (perché come parte di questo processo, il dispositivo viene riavviato e il codice del dispositivo non avrà il controllo per aggiornare lo stato di {{site.data.keyword.iot_short_notm}}). Lo scheletro dell'implementazione della reimpostazione alle impostazioni di fabbrica è illustrato di seguito:

```
public void handleFactoryReset(DeviceAction action) {
    try {
        // codice per eseguire la reimpostazione dei valori predefiniti
    } catch (IOException e) {
        action.setMessage(e.getMessage());
    }
    if(status == false) {
        action.setStatus(DeviceAction.Status.FAILED);
    }
}
```

**3. Aggiungere il gestore a ManagedDevice**

Il gestore creato deve essere aggiunto all'istanza ManagedDevice in modo che la libreria client ibmiotf richiami il metodo corrispondente quando viene effettuata una richiesta dell'azione del dispositivo da {{site.data.keyword.iot_short_notm}}.

```
DeviceActionHandlerSample actionHandler = new DeviceActionHandlerSample();
deviceData.addDeviceActionHandler(actionHandler);
```

Fai riferimento a [questa pagina](../device_mgmt/operations/device_actions.html) per ulteriori informazioni sull'azione del dispositivo.



## Resta in ascolto per le modifiche dell'attributo del dispositivo
{: #listen_device_attribute}

Questa libreria client ibmiotf aggiorna i corrispettivi oggetti se è presente una richiesta di aggiornamento da {{site.data.keyword.iot_short_notm}}, queste richieste di aggiornamento sono avviate dall'applicazione direttamente o indirettamente (aggiornamento firmware) tramite l'API REST {{site.data.keyword.iot_short_notm}}. Oltre ad aggiornare questi attributi, la libreria fornisce un meccanismo tramite il quale il dispositivo può ricevere notifiche quando viene aggiornato un attributo dispositivo.

Gli attributi che possono essere aggiornati da questa operazione sono `location`, `metadata`, `device information` e `firmware`.

Per ricevere notifiche, il dispositivo deve aggiungere un listener di modifica della proprietà negli oggetti di interesse.

```
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

Inoltre, il dispositivo deve implementare il metodo `propertyChange()` su cui riceve la notifica. Il seguente esempio illustra come può essere implementato:

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

Per ulteriori informazioni sull'aggiornamento degli attributi del dispositivo, consulta [questa pagina](../device_mgmt/operations/update.html).

## Esempi
{: #examples}

-   [SampleRasPiDMAgent](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgent.java) - Un codice dell'agent di esempio che mostra come eseguire varie operazioni di gestione del dispositivo su Raspberry Pi.
-   [SampleRasPiManagedDevice](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiManagedDevice.java) - Un codice di esempio che mostra come è possibile eseguire sia le operazioni di gestione che del dispositivo.
-   [SampleRasPiDMAgentWithCustomMqttAsyncClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttAsyncClient.java) - Un codice dell'agent di esempio di MqttAsyncClient personalizzato.
-   [SampleRasPiDMAgentWithCustomMqttClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttClient.java) - Un codice dell'agent di esempio di MqttClient personalizzato.
-   [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java) - Un'implementazione di esempio di FirmwareHandler per Raspberry Pi.
-   [DeviceActionHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java) - Un'implementazione di esempio di DeviceActionHandler
-   [ManagedDeviceWithLifetimeSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/ManagedDeviceWithLifetimeSample.java) - Un esempio che mostra come inviare la richiesta di gestione regolare con il ciclo di vita specificato.
-   [DeviceAttributesUpdateListenerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceAttributesUpdateListenerSample.java) - n codice listener che mostra come essere in ascolto per varie modifiche dell'attributo del dispositivo.
-   [NonBlockingDiagnosticsErrorCodeUpdateSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/NonBlockingDiagnosticsErrorCodeUpdateSample.java) - Un esempio che mostra come aggiungere ErrorCode senza attendere la risposta dal server.

##Ricette
{: #Recipes}

Fai riferimento a [la ricetta](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-managed-device-to-ibm-iot-foundation/) che mostra come collegarti al dispositivo Raspberry Pi come un dispositivo gestito di {{site.data.keyword.iot_short_notm}} e ad eseguire varie operazioni di gestione del dispositivo passo dopo passo utilizzando la libreria client.
