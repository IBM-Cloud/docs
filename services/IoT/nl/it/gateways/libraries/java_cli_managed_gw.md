---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-12-06"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Sviluppo dei gateway gestiti utilizzando Java
{: #java_cli_managed_gw}

I gateway hanno un ruolo importante nella gestione dei dispositivi a loro collegati. Molti dispositivi sono molto basici e non dispongono di funzionalità di gestione, per cui questi dispositivi di base devono essere gestiti da un gateway. In {{site.data.keyword.iot_full}}, un gateway gestito è un gateway che può gestire i dispositivi collegati ad esso e fornisce funzionalità di gestione, come gli aggiornamenti del firmware, dell'ubicazione e della diagnostica.
{:shortdesc}

Utilizzando la libreria client Java™ {{site.data.keyword.iot_short}} e le informazioni fornite, puoi sviluppare il codice Java per modificare il tuo gateway in un gateway gestito. Vengono inoltre forniti degli esempi per aiutarti nello sviluppo del codice Java per collegare un gateway al servizio di gestione del dispositivo ed eseguire le operazioni di gestione del dispositivo.

## Servizio di gestione dispositivo
{: #dm_service}

Il servizio Gestione del dispositivo (DM) {{site.data.keyword.iot_short}} fornisce le funzionalità di gestione del dispositivo ai gateway per gestire i dispositivi ad esso collegati.

Un gateway gestito esegue un agent di gestione del dispositivo, che viene eseguito come un proxy per tutti i dispositivi collegati a {{site.data.keyword.iot_short}} tramite il gateway.

### Agent di gestione del dispositivo

I dispositivi collegati a {{site.data.keyword.iot_short}} indirettamente tramite un gateway possono utilizzare vari protocolli di connessione, se supportati dal dispositivo gateway.

L'istanza `ManagedGateway` è un agent di gestione del dispositivo che fornisce un elenco di metodi per l'esecuzione di una o più azioni di gestione, ad esempio, partecipando all'attività di gestione del dispositivo, aggiornando i codici di  errore, i log e il firmware o le azioni del dispositivo.

L'agent di gestione del dispositivo sul gateway converte ed elabora i protocolli di connessione dei dispositivi collegati, per assicurare che il dispositivo possa essere gestito da {{site.data.keyword.iot_short}}. Tramite l'agent di gestione del dispositivo, il gateway diventa qualcosa di più rispetto a un tunnel trasparente tra il dispositivo collegato e {{site.data.keyword.iot_short}}. Ad esempio, se un dispositivo collegato a un gateway non riesce a scaricare il firmware, l'agent di gestione del dispositivo sul gateway può eseguire le seguenti azioni:
- Intercettare una richiesta di un dispositivo per scaricare il firmware
- Scaricare il firmware per il dispositivo
- Memorizzare il firmware del dispositivo sul gateway

In un momento successivo, quando viene richiesto al dispositivo di eseguire l'aggiornamento, l'agent di gestione del dispositivo sul gateway può passare il firmware al dispositivo e aggiornarlo.

## Creazione del modello del dispositivo
{: #create_device_model}

In {{site.data.keyword.iot_short}}, il modello dispositivo descrive le caratteristiche di gestione e metadati di un gateway. Il database del dispositivo è l'origine principale delle informazioni sul gateway o sul dispositivo. Le applicazioni e i dispositivi gestiti possono inviare aggiornamenti sull'ubicazione, sull'avanzamento dell'aggiornamento del firmware e altri tipi di aggiornamenti. Quando gli aggiornamenti sono ricevuti da {{site.data.keyword.iot_short}}, il database del dispositivo viene aggiornato in modo che le informazioni siano disponibili per il collegamento delle applicazioni.

Nella libreria client Java {{site.data.keyword.iot_short}}, il modello del dispositivo è rappresentato dalla classe Java `DeviceData`.

Per creare la classe `DeviceData`, crea i seguenti oggetti:

- `DeviceInfo` (Facoltativo)
- `DeviceLocation` (Facoltativo, obbligatorio solo se il dispositivo deve essere notificato sull'ubicazione impostata dall'applicazione tramite l'API {{site.data.keyword.iot_short}})
- `DeviceFirmware` (Facoltativo)
- `DeviceMetadata` (Facoltativo)

Per ulteriori informazioni, consulta il [modello del dispositivo](../../reference/device_model.html).

### DeviceInfo

Il seguente frammento di codice che contiene i dati di esempio mostra come creare gli oggetti `DeviceInfo` e `DeviceMetadata`:

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
  * Crea un oggetto DeviceMetadata
 **/
JsonObject data = new JsonObject();
data.addProperty("customField", "customValue");
DeviceMetadata metadata = new DeviceMetadata(data);

```

Il seguente frammento di codice illustra come creare la classe `DeviceData` utilizzando gli oggetti `DeviceInfo` e `DeviceMetadata` creati nel precedente esempio:

```java
DeviceData deviceData = new DeviceData.Builder().
                         deviceInfo(deviceInfo).
                         metadata(metadata).
                         build();
```

Ogni gateway e dispositivo collegato devono avere la propria definizione di classe `DeviceData` che li rappresenta in {{site.data.keyword.iot_short}}. Per i gateway, la classe `DeviceData` viene trasmessa alla libreria come parte della creazione dell'istanza `ManagedGateway`. Per i gateway allegati, la classe `DeviceData` viene trasmessa alla libreria come parte dell'oggetto `sendDeviceManageRequest()`.

## Constructor ManagedGateway
{: #construct_managed_gateway}

`ManagedGateway` è una classe Java che collega un gateway a {{site.data.keyword.iot_short}} come un gateway gestito che può eseguire almeno un'operazione di gestione del dispositivo per se stesso o per i dispositivi collegati. Può anche essere utilizzata un'istanza `ManagedGateway` per le normali operazioni gateway, come la pubblicazione degli eventi del gateway, il collegamento di eventi del dispositivo e l'elenco dei comandi dalle applicazioni. L'istanza `ManagedGateway` è un agent di gestione del dispositivo.

Nella classe `ManagedGateway`, due diversi constructor, Constructor uno e Constructor due, supportano diversi modelli utente.

### Constructor uno

Il constructor uno crea un'istanza `ManagedGateway` accettando una classe `DeviceData` che contiene tutte le seguenti proprietà:

| Proprietà     |Descrizione     |
|----------------|----------------|
|`Organization-ID` |Il tuo ID dell'organizzazione.|
|`Gateway-Type` |Il tipo del tuo dispositivo gateway.|
|`Gateway-ID` |L'ID del dispositivo gateway.|
|`Authentication-Method`|Il metodo di autenticazione. L'unico metodo supportato è "token".|
|`Authentication-Token`|Il token della chiave API.|
|`auth-key`   |Una chiave API facoltativa, che devi specificare quando imposti il valore di auth-method su `apikey`.|
|`auth-token`   |Un token chiave API, che è inoltre obbligatorio quando imposti il valore di auth-method su `apikey`. |
|`clean-session`|Un valore true o false obbligatorio solo se desideri collegarti al gateway con il metodo di sottoscrizione durevole. Per impostazione predefinita, `clean-session` è impostato su `true`.|
|`Porta`|Il numero di porta a cui collegarsi. Specifica 8883 o 443. Se non specifichi un numero di porta, il client si collega a {{site.data.keyword.iot_short_notm}} nel numero di porta 8883 per impostazione predefinita.|
|`WebSocket`|Un valore true o false obbligatorio solo se desideri collegarti al gateway utilizzando i socket web.|
|`MaxInflightMessages`  |Imposta il numero massimo di messaggi in elaborazione per la connessione. Il valore predefinito è 100.|
|`Automatic-Reconnect`  |Un valore true o false obbligatorio quando desideri ricollegare automaticamente il dispositivo a {{site.data.keyword.iot_short_notm}} mentre è in uno stato disconnesso. Il valore predefinito è false.|
|`Disconnected-Buffer-Size`|Il numero massimo di messaggi che possono essere archiviati nella memoria mentre il client è disconnesso. Il valore predefinito è 5000.|

**Nota:** per collegare il gateway con il metodo di sottoscrizione durevole, imposta `clean-session` su `false`. Per ulteriori informazioni sulla proprietà `clean-session`, consulta la sezione 'Sottoscrizione buffer e ripulitura sessione' della [Documentazione MQTT](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

Il seguente codice illustra come creare un'istanza `ManagedGateway`:

```java
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Gateway-Type", "iotsample-arduino");
options.setProperty("Gateway-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedGateway ManagedGateway = new ManagedGateway(options, deviceData);
```

### Constructor due

Il constructor due crea un'istanza `ManagedGateway` accettando un oggetto `DeviceData` e l'istanza client MQTT. Il constructor due richiede inoltre che l'oggetto `DeviceData` nell'istanza includa l'ID e il tipo di dispositivo, come illustrato nel seguente esempio di codice:

```java
// Codice che crea un'istanza client MQTT sincrona o asincrona di mqttClient.
.....

// Codice che crea l'oggetto DeviceData
DeviceData deviceData = new DeviceData.Builder().
                         typeId("Gateway-Type").
                         deviceId("Gateway-ID").
                         deviceInfo(deviceInfo).
                         metadata(metadata).
                         build();

....
ManagedGateway ManagedGateway = new ManagedGateway(mqttClient, deviceData);

```

**Nota:**  se stai sviluppando dei dispositivi personalizzati, utilizza il constructor due, perché questo constructor crea un'istanza gateway gestita utilizzando l'istanza client MQTT collegata esistente in modo che puoi sfruttare le operazioni di gestione del dispositivo. Utilizza la libreria client Java per tutte le altre funzioni del dispositivo.

## Richieste di gestione dispositivo da un gateway
{: #dm_requests}

### Invio di una richiesta di gestione da un gateway

Per indicare a un gateway di partecipare alle azioni di gestione del dispositivo, richiama il metodo `sendGatewayManageRequest()`, come illustrato nel seguente esempio di codice:

```java
managedGateway.sendGatewayManageRequest(0, true, true);
```
La richiesta di gestione avvia una richiesta di connessione internamente se il dispositivo non è già collegato a {{site.data.keyword.iot_short}}.

Il metodo `sendGatewayManageRequest()` accetta i seguenti parametri:

| Parametro     |Descrizione     |
|----------------|----------------|
|`lifetime`|La durata in secondi in cui il gateway deve inviare un'altra richiesta di gestione del dispositivo per evitare di essere classificato come inattivo e diventare un dispositivo non gestito. Se il campo `lifetime` viene omesso o impostato su 0, il gateway gestito non diventa inattivo. L'impostazione supportata minima per il campo `lifetime` è 3600 secondi (1 ora).|
|`supportFirmwareActions`|Un valore true o false che determina se il gateway supporta le azioni firmware. Il gateway deve inoltre aggiungere un gestore firmware per gestire le richieste del firmware.|
|`supportDeviceActions`|Un valore true o false che determina se il gateway supporta le azioni del dispositivo. Il gateway deve inoltre aggiungere un gestore azioni del dispositivo per gestire le richieste di ripristino delle impostazioni predefinite e di riavvio.|


L'istanza `ManagedGateway` è un agent di gestione del dispositivo che fornisce un elenco di metodi per l'esecuzione di una o più azioni di gestione, ad esempio, partecipando all'attività di gestione del dispositivo, aggiornando i codici di  errore, i log e il firmware o le azioni del dispositivo.

### Invio di una richiesta di gestione dai dispositivi collegati

Per consentire ai dispositivi collegati dietro a un gateway di partecipare alle azioni di gestione del dispositivo sul gateway, richiama il metodo `sendDeviceManageRequest()`.

Il metodo `sendDeviceManageRequest()` accetta i dettagli dei dispositivi collegati e i parametri `lifetime`, `supportFirmwareActions` e `supportDeviceActions`. Un gateway può inoltre utilizzare il metodo overloaded `sendDeviceManageRequest()` per definire l'oggetto `DeviceData` per il dispositivo collegato.

#### Esempio di invio di una richiesta di gestione dai dispositivi collegati

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, lifetime, true, true);
```

### Invio di una richiesta di annullamento della gestione da un gateway

Quando un gateway non deve più essere gestito, per arrestare le attività di gestione del dispositivo sul gateway, richiama il metodo `sendGatewayUnmanageRequet()`.  Quando viene richiamato `sendGatewayUnmanageRequet()`, {{site.data.keyword.iot_short}} non invierà più nuove richieste di gestione del dispositivo e tutte le richiesta dal gateway vengono rifiutate, con eccezione delle richieste **Gestione**. Le richieste dai dispositivi dietro a un gateway vengono rifiutate.

#### Esempio di invio di una richiesta di annullamento della gestione da un gateway

```java
managedGateway.sendGatewayUnmanageRequet();
```

### Invio di una richiesta di annullamento della gestione dai dispositivi collegati

Quando un dispositivo dietro a un gateway non deve più essere gestito, per modificare lo stato di un dispositivo da gestito a non gestito, il gateway può richiamare il metodo `sendDeviceUnmanageRequet()`. Quando viene richiamato `sendDeviceUnmanageRequet()`, {{site.data.keyword.iot_short}} non invia più nuove richieste di gestione del dispositivo per il dispositivo e tutte le richieste dal gateway per il dispositivo collegato vengono rifiutate, con l'eccezione delle richieste **Gestione**.

#### Esempio di invio di una richiesta di annullamento della gestione dai dispositivi collegati

```java
managedGateway.sendDeviceUnmanageRequet();
```

## Aggiornamenti ubicazione
{: #location_updates}

### Invio degli aggiornamenti dell'ubicazione del gateway

I gateway che possono determinare la loro ubicazione possono scegliere di inviare notifiche a {{site.data.keyword.iot_short}} sulle modifiche dell'ubicazione. Il gateway può richiamare uno dei metodi overloaded `updateLocation()` per aggiornare l'ubicazione del dispositivo.

```java
    // aggiornare l'ubicazione con latitudine, longitudine e altitudine.
int rc = managedGateway.updateGatewayLocation(30.28565, -97.73921, 10);
if(rc == 200) {
    System.out.println("Location updated successfully!");
} else {
System.err.println("Failed to update the location!");
    }
```

### Invio degli aggiornamenti sull'ubicazione dei dispositivi collegati

Il gateway può richiamare il metodo del dispositivo `updateDeviceLocation()` corrispondente per aggiornare l'ubicazione dei dispositivi collegati. Il metodo overloaded può essere utilizzato per specificare il metodo `measuredDateTime`.  

```java
// aggiornare l'ubicazione del dispositivo collegato con latitudine, longitudine e altitudine
int rc = managedGateway.updateDeviceLocation(typeId, deviceId, 30.28565, -97.73921, 10);
```
Per ulteriori informazioni sugli aggiornamenti dell'ubicazione, consulta [Richieste di gestione del dispositivo](../../devices/device_mgmt/index.html#/update-location#update-location).

## Gestione dei codici di errore
{: #errors}

### Creazione ed eliminazione dei codici di errore gateway

Un gateway può scegliere di inviare notifiche a {{site.data.keyword.iot_short}} sulle modifiche al proprio stato di errore. Il gateway può richiamare il metodo `addErrorCode()` per aggiungere il codice di errore corrente a {{site.data.keyword.iot_short}}.

```java
int rc = managedGateway.addGatewayErrorCode(300);
```

I codici di errore per un gateway possono essere cancellati da {{site.data.keyword.iot_short}} richiamando il metodo `clearErrorCodes()` nel seguente modo:

```java
int rc = managedGateway.clearGatewayErrorCodes();
```

### Creazione ed eliminazione dei codici di errore per i dispositivi collegati

Un gateway può anche richiamare il metodo del dispositivo corrispondente per aggiungere o cancellare i codici di errore per i dispositivi collegati:

```java
int rc = managedGateway.addDeviceErrorCode(typeId, deviceId, 300);
rc = managedGateway.clearDeviceErrorCodes(typeId, deviceId);
```

### Creazione ed eliminazione dei codici dei messaggi di log

Un gateway può scegliere di inviare notifiche a {{site.data.keyword.iot_short}} sulle modifiche aggiungendo una nuova voce di log. Una voce di log include i seguenti elementi:

- Stringa messaggio
- Data/ora
- Severità
- Facoltativamente, i dati di diagnostica codificati base64

I gateway possono richiamare il metodo `addGatewayLog()` per inviare i messaggi di log, come illustrato nel seguente esempio:

```java
// Un esempio di evento di log
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addGatewayLog(message, timestamp, severity);
```

I messaggi di log possono essere cancellati da {{site.data.keyword.iot_short}} richiamando il metodo `clearLogs()`:

```java
rc = managedGateway.clearGatewayLogs();
```

### Creazione ed eliminazione dei log per i dispositivi collegati

Allo stesso modo, il gateway può richiamare il metodo del dispositivo corrispondente per creare e cancellare i log per i dispositivi collegati, come illustrato nel seguente esempio di codice:

```java

// Un esempio di evento di log:
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addDeviceLog(typeId, deviceId, message, timestamp, severity);
```

Per cancellare i log dei dispositivi collegati, richiama il metodo `clearDeviceLogs()` specificando i dettagli del dispositivo collegato, come illustrato nel seguente esempio di codice:

```java
int rc = managedGateway.clearDeviceLogs(typeId, deviceId);
```

Le operazioni di diagnostica del dispositivo sono pensate per fornire informazioni sul gateway o sugli errori del dispositivo. Non forniscono informazioni di diagnostica su una connessione del dispositivo a {{site.data.keyword.iot_short}}.

Per ulteriori informazioni sull'operazione di diagnostica, consulta [Richieste di gestione del dispositivo](../../devices/device_mgmt/index.html#/update-location#update-location).

## Azioni e aggiornamenti firmware
{: #firmware}

Il processo di aggiornamento del firmware è separato in due azioni distinte:

- Scaricamento del firmware
- Aggiornamento del firmware

Il gateway deve eseguire le seguenti azioni per supportare le azioni firmware per se stesso e per i propri dispositivi collegati:

1. Facoltativo: creare un oggetto `DeviceFirmware`.
2. Informare il server sul supporto dell'azione firmware.
3. Creare il gestore dell'azione firmware.
4. Aggiungere il gestore a `ManagedGateway`.

### Passo 1: creazione di un oggetto `DeviceFirmware`

Per eseguire azioni firmware, un gateway può facoltativamente creare un oggetto `DeviceFirmware` per se stesso e per i propri dispositivi collegati e quindi aggiungerlo all'oggetto `DeviceData`, come descritto nel seguente esempio:

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

Per i dispositivi collegati, l'oggetto `DeviceData` creato può essere trasmesso alla libreria durante l'invio della richiesta di gestione, come illustrato nel seguente esempio di codice:

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, lifetime, supportFirmwareActions, supportDeviceActions);
```

L'oggetto `DeviceFirmware` rappresenta il firmware corrente del gateway o del dispositivo collegato e viene utilizzato per notificare lo stato delle azioni di scaricamento e aggiornamento firmware a {{site.data.keyword.iot_short}}. Se l'oggetto `DeviceFirmware` non è stato creato dal gateway, la libreria crea un oggetto vuoto e notifica lo stato a {{site.data.keyword.iot_short}}.

### Passo 2: Informare il server sul supporto dell'azione firmware

Il gateway e i suoi dispositivi collegati devono impostare l'indicatore dell'azione firmware su true per consentire al server di avviare la richiesta firmware. Questa modifica può essere archiviata trasmettendo un valore true per il parametro `supportFirmwareActions` nella richiesta di gestione.

Il gateway può richiamare il seguente metodo per informare il server riguardo il suo supporto firmware:
```java
managedGateway.sendGatewayManageRequest(3600, true, false);
```

Allo stesso modo, il gateway può richiamare il metodo del dispositivo corrispondente per informare il supporto firmware dei dispositivi collegati:

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, 3600, true, false);
```

Quando il supporto viene informato dal server di gestione del dispositivo, inoltra le azioni firmware al gateway per il gateway stesso o per i suoi dispositivi.

### Passo 3: creazione del gestore dell'azione firmware

Per supportare l'azione firmware, il gateway deve creare un gestore e aggiungerlo a `managedGateway`. Il gestore deve estendere una classe `DeviceFirmwareHandler` e implementare i seguenti metodi:

```java
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**Nota**: deve venire aggiunto solo un gestore alla libreria sia per il gateway che per i dispositivi collegati in cui sono reindirizzate le richieste di aggiornamento e scaricamento firmware. L'implementazione deve creare un thread o un pool di thread per gestire più richieste firmware contemporaneamente.

Puoi trovare un'implementazione di esempio del gestore del pool di thread nel [Gateway samples GutHub repository](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java).

### Un'implementazione di esempio di `downloadFirmware`

L'implementazione deve aggiungere la logica di scaricamento del firmware e notificare lo stato dello scaricamento utilizzando l'oggetto `DeviceFirmware`. Se l'operazione di scaricamento del firmware ha esito positivo, lo stato del firmware deve essere impostato su 'SCARICATO' e la proprietà `UpdateStatus` deve essere impostata su 'RIUSCITO'.

Se si verifica un errore durante uno scaricamento del firmware, lo stato deve essere impostato su 'IN SOSPESO' e la proprietà `updateStatus` deve essere impostata su uno dei seguenti valori di stato di errore:

- OUT_OF_MEMORY
- CONNECTION_LOST
- INVALID_URI

Viene mostrata un'implementazione di scaricamento firmware di esempio nel seguente esempio di codice:

**Importante:** l'esempio di codice che viene fornito non include la sezione pool di thread. Per l'implementazione completa del gestore firmware, è disponibile un esempio nel [IBM Java gateway samples GitHub repository ](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java).

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

Un gateway gestito può controllare l'integrità dell'immagine firmware scaricata utilizzando il verificatore e notificare lo stato a {{site.data.keyword.iot_short}}. Il verificatore può essere impostato dal gateway durante le seguenti fasi:

- Durante l'avvio quando viene creato l'oggetto 'DeviceFirmware'
- Quando un'applicazione invia una richiesta 'downloadFirmware'

#### Esempio

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

Il codice completo può essere trovato nell'esempio di gestione del gateway [GatewayFirmwareHandlerSample](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java).

### Un'implementazione di esempio di `updateFirmware`

L'implementazione deve creare un gestore separato e aggiungere la logica per installare il firmware scaricato e notificare lo stato dell'aggiornamento utilizzando l'oggetto `DeviceFirmware`. Se l'operazione di aggiornamento del firmware ha esito positivo, lo stato del firmware deve essere impostato su 'IN SOSPESO' e il valore `updateStatus` deve essere impostato su 'RIUSCITO'.

Se si verifica un errore durante l'aggiornamento del firmware, il valore `updateStatus` deve essere impostato su uno dei valori dello stato di errore illustrati di seguito:

* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE

Il seguente codice di esempio descrive come puoi implementare un aggiornamento firmware per un dispositivo Raspberry Pi:

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

Il codice completo può essere trovato nell'esempio `GatewayFirmwareHandlerSample` nel [Gateway samples GitHub repository](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java).

### Passo 4: aggiunta del gestore a `ManagedGateway`

Quando viene creato un gestore, deve essere aggiunto all'istanza `ManagedGateway` in modo che la libreria client Java invochi il metodo corrispondente se è presente una richiesta di azione firmware da {{site.data.keyword.iot_short}}.

```java
GatewayFirmwareHandlerSample fwHandler = new GatewayFirmwareHandlerSample();
mgdGateway.addFirmwareHandler(fwHandler);
```

Per ulteriori informazioni sulle azioni firmware, consulta [Richieste di gestione del dispositivo](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/requests.html#/firmware-actions#firmware-actions).

## Azioni dispositivo
{: #dev_actions}

{{site.data.keyword.iot_short}} supporta le seguenti azioni del dispositivo:

- Riavvio
- Reimpostazione fabric

Il gateway deve eseguire le seguenti azioni per supportare le azioni del dispositivo per se stesso e anche per i suoi dispositivi.

1. Informare il server sul supporto delle azioni del dispositivo.
2. Creare il gestore dell'azione del dispositivo.
3. Aggiungere il gestore a `ManagedGateway`.

### Passo 1: informare il server sul supporto delle azioni del dispositivo

Per eseguire un riavvio o un'azione di ripristino delle impostazioni predefinite per un gateway e i suoi dispositivi collegati, il gateway deve prima informare {{site.data.keyword.iot_short}} sul supporto. Questa azione può essere eseguita trasmettendo un valore true per il parametro `supportDeviceActions` durante l'invio della richiesta di **Gestione**.

Un gateway può richiamare il seguente metodo per informare il server riguardo il suo supporto per l'azione del dispositivo:

```java
// L'ultimo parametro rappresenta il supporto per l'azione del dispositivo
managedGateway.sendGatewayManageRequest(3600, true, true);
```

Un gateway può richiamare il metodo del dispositivo corrispondente per informare il supporto dell'azione del dispositivo dei dispositivi collegati:

```java
// L'ultimo parametro rappresenta il supporto per l'azione del dispositivo
managedGateway.sendDeviceManageRequest(typeId, deviceId, 0, true, true);
```

Quando il supporto viene informato dal server di gestione del dispositivo, inoltra le richieste di azione al dispositivo.

### Passo 2: creazione del gestore dell'azione del dispositivo

Per supportare l'azione del dispositivo, il gateway deve creare un gestore e aggiungerlo all'istanza `managedGateway`. Il gestore deve estendere una classe `DeviceActionHandler` e fornire l'implementazione dei seguenti metodi:

```java
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**Nota:** deve venire aggiunto solo un gestore alla libreria sia per il gateway che per i dispositivi collegati in cui sono reindirizzate le richieste dell'azione del dispositivo. L'implementazione deve creare un thread o un pool di thread per gestire più richieste di azione del dispositivo contemporaneamente. Un'implementazione del gestore di esempio che utilizza un pool di thread viene illustrata nel [iot-gateway-samples GitHub repository](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java).

### Un'implementazione di esempio di `handleReboot`

L'implementazione deve creare un gestore separato e aggiungere la logica per riavviare il gateway e il dispositivo collegato e notificare lo stato del riavvio utilizzando l'oggetto `DeviceAction`. Dopo la ricezione della richiesta, il gateway deve prima informare il server sul supporto o il malfunzionamento prima di procedere con il riavvio attuale. Se l'esempio non può riavviare il dispositivo o si è verificato un qualsiasi altro errore durante il riavvio, il gateway può aggiornare lo stato in un messaggio facoltativo. Viene fornita un'implementazione di esempio del riavvio per un dispositivo Raspberry Pi nel seguente esempio di codice:

```java
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

L'implementazione del gestore di esempio completa che utilizza un pool di thread viene illustrata nel [iot-gateway-samples GitHub repository](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java).


### Un'implementazione di esempio di `handleFactoryReset`

L'implementazione deve creare un gestore separato e aggiungere la logica per ripristinare il gateway e il dispositivo collegato alle impostazioni predefinite e notificare lo stato del ripristino utilizzando l'oggetto DeviceAction. Quando la richiesta viene ricevuta, il gateway deve informare il server sul supporto o il malfunzionamento prima di procedere con il ripristino attuale. Le linee di base dell'implementazione del ripristino alle impostazioni predefinite vengono illustrate nel seguente esempio di codice:

```java
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

### Passo 3: aggiunta del gestore a `ManagedGateway`

Quando viene creato un gestore, deve essere aggiunto all'istanza `ManagedGateway` in modo che la libreria client Java invochi il metodo corrispondente se è presente una richiesta di azione del dispositivo da {{site.data.keyword.iot_short}}.

```java
GatewayActionHandlerSample actionHandler = new GatewayActionHandlerSample();
mgdGateway.addDeviceActionHandler(actionHandler);
```

Per ulteriori informazioni sulle azioni del dispositivo, consulta [Richieste di gestione del dispositivo](../../devices/device_mgmt/requests.html#/device-actions-reboot#device-actions-reboot).

## Restare in ascolto per le modifiche dell'attributo del dispositivo
{: #listen_device_attributes}

La libreria client Java aggiorna i corrispettivi oggetti se è presente una richiesta di aggiornamento da {{site.data.keyword.iot_short}}. Queste richieste di aggiornamento sono avviate dall'applicazione direttamente o indirettamente tramite un aggiornamento firmware utilizzando l'API REST {{site.data.keyword.iot_short}}. Oltre ad aggiornare questi attributi, la libreria fornisce un meccanismo tramite il quale il gateway può ricevere notifiche quando viene aggiornato un attributo dispositivo.

Gli attributi che possono essere aggiornati da questo tipo di operazione sono l'ubicazione, i metadati, le informazioni sul dispositivo e il firmware del gateway o del dispositivo collegato.

Per ricevere notifiche sulle modifiche dell'attributo, il gateway deve aggiungere un listener di modifica della proprietà agli oggetti per cui è interessato, come illustrato nel seguente esempio di codice:

```java
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

Il gateway deve anche implementare il metodo `propertyChange()` su cui riceve la notifica, come illustrato nella seguente implementazione di esempio:

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

Per ulteriori informazioni sull'aggiornamento degli attributi del dispositivo, consulta [Richieste di gestione del dispositivo](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/index.html#/update-device-attributes#update-device-attributes).

## Esempi
{: #samples}

Sono disponibili molti esempi per aiutarti nel collegamento di gateway e dispositivi dietro un gateway alla tua istanza {{site.data.keyword.iot_short_notm}}. Gli esempi utilizzano la libreria client Java {{site.data.keyword.iot_short_notm}} ubicata nel [Gateway Samples GitHub repository](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples).

## Istruzioni specifiche
{: #recipes}

Per una ricetta che ti mostra come collegare un dispositivo Rasberry Pi come un gateway gestito a {{site.data.keyword.iot_short_notm}} e come gestire i dispositivi collegati, consulta [Raspberry Pi as a managed gateway in {{site.data.keyword.iot_short_notm}} ](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/).

La ricetta illustra come puoi utilizzare il protocollo di gestione del dispositivo di {{site.data.keyword.iot_short_notm}} per gestire un dispositivo Arduino Uno da un dispositivo Raspberry Pi che agisce come un gateway ed effettua operazioni di gestione del dispositivo, come ad esempio il riavvio del dispositivo o l'aggiunta di un programma bozza.
