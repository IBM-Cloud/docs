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

# Verwaltete Geräte unter Verwendung von Java entwickeln
{: #java_deviceManagement}

## Einführung
{: #introduction}

Ein verwaltetes Gerät ist in {{site.data.keyword.iot_full}} ein Gerät, das Gerätemanagementoperationen wie Firmware-, Positions- und Diagnoseaktualisierungen durchführen kann.
Unter Verwendung der {{site.data.keyword.iot_short}}-Java™-Clientbibliothek und der bereitgestellten Informationen können Sie Java-Code entwickeln, der Ihre verbundenen Geräte zu verwalteten Geräten macht. Darüber hinaus werden hilfreiche Beispiele zum Entwickeln von Java-Code bereitgestellt, um ein Gerät mit dem Gerätemanagementservice zu verbinden und Gerätemanagementoperationen auszuführen.

Weitere Informationen dazu, wie Ihre Anwendungen die Java-Clientbibliothek für die Interaktion mit Geräten verwenden können, finden Sie in [Java für Anwendungsentwickler](../../applications/libraries/java.html).

## Gerätemanagement
{: #device_management}

Die Funktion [Gerätemanagement](../reference/device_mgmt.html) erweitert den {{site.data.keyword.iot_short_notm}}-Service um weitere Funktionen zur Verwaltung von Geräten. Beim Gerätemanagement besteht ein Unterschied zwischen verwalteten und nicht verwalteten Geräten:

-   **Verwaltete Geräte** sind als Geräte definiert, die über einen installierten Managementagenten verfügen. Der Managementagent sendet und empfängt gerätebezogene Metadaten und antwortet auf Gerätemanagementbefehle, die von {{site.data.keyword.iot_short_notm}} stammen.
-   **Nicht verwaltete Geräte** sind sämtliche Geräte, die über keinen Gerätemanagementagenten verfügen. Der Lebenszyklus jedes Geräts beginnt als nicht verwaltetes Gerät. Wenn vom Gerätemanagementagenten eine entsprechende Nachricht an {{site.data.keyword.iot_short_notm}} gesendet wird, kann das Gerät zu einem verwalteten Gerät werden.

## Herstellen der Verbindung zum {{site.data.keyword.iot_short_notm}}-Gerätemanagementservice
{: #connecting_dm_service}

## Gerätedaten erstellen
{: #creating_device_data}

Im [Gerätemodell](../reference/device_model.html) werden die Metadaten und die Managementmerkmale eines Geräts beschrieben. Die Gerätedatenbank in {{site.data.keyword.iot_short_notm}} ist die Masterquelle für Geräteinformationen. Anwendungen und verwaltete Geräte können Aktualisierungen an die Datenbank senden, wie beispielsweise eine Position oder den Verarbeitungsfortschritt eines Firmware-Updates. Sobald diese Aktualisierungen von {{site.data.keyword.iot_short_notm}} empfangen werden, wird die Gerätedatenbank aktualisiert, wodurch die Informationen für Anwendungen verfügbar werden.

`DeviceData` ist das Gerätemodell in der Clientbibliothek 'ibmiotf', das folgende Objekte enthält:

-   DeviceInfo (erforderlich)
-   DeviceLocation (erforderlich, wenn das Gerät die Positionsaktualisierung unterstützt)
-   DiagnosticErrorCode (erforderlich, wenn der Fehlercode (ErrorCode) des Geräts aktualisiert werden soll)
-   DiagnosticLog (erforderlich, wenn die Protokollinformationen des Geräts aktualisiert werden sollen)
-   DeviceFirmware (erforderlich, wenn das Gerät Firmwareaktionen unterstützt)
-   DeviceMetadata (optional)

Das folgende Codebeispiel zeigt die Erstellung des obligatorischen `DeviceInfo`-Objekts zusammen mit dem optionalen `DeviceMetadata`-Objekt und Beispieldaten:

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
  * Erstellen Sie ein DeviceMetadata-Objekt
 **/
JsonObject data = new JsonObject();
data.addProperty("customField", "customValue");
DeviceMetadata metadata = new DeviceMetadata(data);
```

Erstellen Sie mithilfe des folgenden Codebeispiels ein `DeviceData`-Objekt, in dem die `DeviceInfo`- und `DeviceMetadata`-Objekte enthalten sind, die Sie im vorangegangenen Beispiel erstellt haben.

  ```
  DeviceData deviceData = new DeviceData.Builder().
               deviceInfo(deviceInfo).
               metadata(metadata).
               build();
  ```

## 'ManagedDevice' erstellen
{: #construct_managed_device}

`ManagedDevice` ist eine Geräteklasse, die das Gerät als verwaltetes Gerät mit {{site.data.keyword.iot_short_notm}} verbindet und dem Gerät ermöglicht, mindestens eine Gerätemanagementoperation auszuführen. Sie können zum Ausführen von üblichen Geräteoperationen wie beispielsweise dem Publizieren von Geräteereignissen und der Empfangsbereitschaft für Befehle, die von einer Anwendung stammen, auch eine `ManagedDevice`-Instanz verwenden.

`ManagedDevice` stellt folgende Konstruktoren bereit, durch die unterschiedliche Benutzermuster unterstützt werden:

**Konstruktur 1**

Konstruktor 1 erstellt eine `ManagedDevice`-Instanz in {{site.data.keyword.iot_short_notm}}, indem `DeviceData` und alle folgenden erforderlichen Eigenschaften akzeptiert werden:

|Eigenschaft |Beschreibung |
|:---|:---|
|`Organization-ID` |Die ID Ihrer Organisation.|
|`Device-Type` |Der Typ Ihres Geräts. In der Regel ist 'deviceType' eine Zusammenfassung von Geräten, die eine bestimmte Aufgabe ausführen, beispielsweise 'Wetterballon'.|
|`Device-ID` |Die ID Ihres Geräts. In der Regel ist 'deviceId' bei vorgegebenem Gerätetyp eine eindeutige Kennung des betreffenden Geräts, beispielsweise die Seriennummer oder MAC-Adresse.|
|`Authentication-Method` |Die zu verwendende Authentifizierungsmethode. Der einzige Wert, der aktuell unterstützt ist, lautet `token`.|
|`Authentication-Token` |Ein Authentifizierungstoken zum Herstellen einer sicheren Verbindung zwischen Ihrem Gerät und Watson IoT Platform.|


Der folgende Code umreisst, wie Sie eine `ManagedDevice`-Instanz erstellen können:

```
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Device-Type", "iotsample-arduino");
options.setProperty("Device-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

Wenn Sie bereits eine `DeviceClient`-Instanz verwenden, werden Sie feststellen, dass die Namen der Eigenschaften leicht abweichend sind und die im {{site.data.keyword.iot_short_notm}}-Dashboard verwendeten Namen widerspiegeln. Zum Migrieren von `DeviceClient` auf `ManagedDevice` können Sie weiterhin das frühere Format verwenden, indem Sie die `ManagedDevice`-Instanz wie im folgenden Beispiel umrissen erstellen:

```
Properties options = new Properties();
options.setProperty("org", "uguhsp");
options.setProperty("type", "iotsample-arduino");
options.setProperty("id", "00aabbccde03");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");
ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

**Konstruktor 2**

Erstellen Sie eine `ManagedDevice`-Instanz, indem Sie sowohl die `DeviceData`-Instanz als auch die `MqttClient`-Instanzen akzeptieren. Für diesen Konstruktor sind Gerätedaten (`DeviceData`) erforderlich, die mit zusätzlichen Geräteattributen wie beispielsweise Gerätetyp und Geräte-ID erstellt werden, wie im folgenden Beispiel umrissen:

```
// Code, mit dem 'MqttClient' (ein synchrones oder ein asynchrones MqttClient-Element) erstellt wird
.....

// Code, mit dem 'DeviceData' erstellt wird
DeviceData deviceData = new DeviceData.Builder().
             typeId("Device-Type").
             deviceId("Device-ID").
             deviceInfo(deviceInfo).
             metadata(metadata).
             build();

....
ManagedDevice managedDevice = new ManagedDevice(mqttClient, deviceData);
```

**Hinweis:** Dieser Konstruktor hilft Benutzern angepasster Geräte, eine `ManagedDevice`-Instanz mithilfe der bereits erstellten und verbundenen `MqttClient`-Instanz zu erstellen, um Gerätemanagementoperationen nutzen zu können. Benutzern wird jedoch empfohlen, für die gesamte Gerätefunktionalität die Bibliothek zu verwenden.

## Verwalten

Das Gerät `Manage` kann die Methode 'manage()' aufrufen, um an den Gerätemanagementaktivitäten teilzunehmen. Die Managementanforderung initiiert intern eine Verbindungsanforderung, wenn für das Gerät noch keine Verbindung zu {{site.data.keyword.iot_short_notm}} hergestellt wurde.

```
managedDevice.manage();
```

Das Gerät kann die überladene Methode für die Verwaltung (Lebensdauer) verwenden, um das Gerät für einen bestimmten Zeitrahmen zu registrieren. Durch den Zeitrahmen wird die Länge der Zeit angegeben, innerhalb der das Gerät eine weitere Anforderung des Typs **Gerät verwalten** senden muss, damit es nicht auf den Status eines 'Nicht verwalteten Geräts' zurückgesetzt und als 'Ruhend' markiert wird.

```
managedDevice.manage(3600);
```

Weitere Informationen zur Operation `Manage` finden Sie in der [Dokumentation].

  [documentation]:../device_mgmt/operations/manage.html

## Nicht verwalten

Ein Gerät kann die Methode 'unmanage()' aufrufen, wenn es nicht mehr verwaltet werden muss. {{site.data.keyword.iot_short_notm}} sendet an dieses Gerät keine neuen Managementanforderungen mehr und bis auf die Anforderung **Gerät verwalten** werden alle Gerätemanagementanforderungen dieses Geräts abgelehnt.

```
managedDevice.unmanage();
```

Weitere Informationen zur Operation `Unmanage` finden Sie in der [Dokumentation].

  [documentation]:../device_mgmt/operations/manage.html

## Positionsaktualisierung
{: #construct_location_update}
Für Geräte, die ihre Position bestimmen können, kann ausgewählt werden, dass {{site.data.keyword.iot_short_notm}} über Positionsaktualisierungen benachrichtigt wird. Zum Aktualisieren der Position muss das Gerät eine `DeviceData`-Instanz erstellen, wobei das `DeviceLocation`-Objekt an erster Stelle steht.

```
// Erstellen Sie das Positionsobjekt mit Breitengrad, Längengrad und Höhe
DeviceLocation deviceLocation = new DeviceLocation.Builder(30.28565, -97.73921).
                            elevation(10).
                            build();
DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceLocation(deviceLocation).
             metadata(metadata).
             build();
```

Wenn für das Gerät eine Verbindung zu {{site.data.keyword.iot_short_notm}} hergestellt wird, können Sie die Position anhand der folgenden Methode aktualisieren:

```
int rc = deviceLocation.sendLocation();
if(rc == 200) {
        System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
            System.err.println("Failed to update the location");
}
```

Nachfolgende Aktualisierungen für die Geräteposition können durch Ändern der Eigenschaften des `DeviceLocation`-Objekts wie im folgenden Beispiel gezeigt aktualisiert werden:

```
int rc = deviceLocation.update(40.28, -98.33, 11);
if(rc == 200) {
    System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
    System.err.println("Failed to update the location");
}
```

Durch die Methode 'update()' wird {{site.data.keyword.iot_short_notm}} die neue Position mitgeteilt.

Weitere Informationen zum Aktualisieren von Positionen finden Sie in der über einen Link aufzurufenden [Dokumentation](../device_mgmt/operations/update.html).



## Fehlercodes anhängen und löschen
{: #appending_error_codes}

Für Geräte kann ausgewählt werden, dass {{site.data.keyword.iot_short_notm}} zu Änderungen in ihren Fehlercodes benachrichtigt wird. Zum Senden der Fehlercodes muss das Gerät wie im folgenden Beispiel dargestellt ein `DiagnosticErrorCode`-Objekt erstellen:

```
DiagnosticErrorCode errorCode = new DiagnosticErrorCode(0);

DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceErrorCode(errorCode).
             metadata(metadata).
             build();
```

Sobald für das Gerät eine Verbindung zu {{site.data.keyword.iot_short_notm}} hergestellt wurde, kann der Fehlercode (`ErrorCode`) durch Aufrufen der Methode 'send()' wie folgt gesendet werden:

```
errorCode.send();
```

Später können neue Fehlercodes (`ErrorCodes`) ohne großen Aufwand zu {{site.data.keyword.iot_short_notm}} hinzugefügt werden, indem wie folgt die Methode 'append' aufgerufen wird:

```
int rc = errorCode.append(500);
if(rc == 200) {
    System.out.println("Current Errorcode (" + errorCode + ")");
} else {
    System.out.println("Errorcode addition failed!");
}
```

Die Fehlercodes (`ErrorCodes`) können auch aus {{site.data.keyword.iot_short_notm}} gelöscht werden, indem die Methode 'clear()' wie folgt aufgerufen wird:

```
int rc = errorCode.clear();
if(rc == 200) {
    System.out.println("ErrorCodes are cleared successfully!");
} else {
    System.out.println("Failed to clear the ErrorCodes!");
}
```

## Protokollnachrichten anhängen und löschen

Für Geräte kann ausgewählt werden, dass {{site.data.keyword.iot_short_notm}} durch Hinzufügen eines neuen Protokolleintrags über Änderungen benachrichtigt wird. Ein Protokolleintrag enthält folgende Informationen:
- Protkollnachricht
- Zeitmarke
- Schweregrad
- binäre Diagnosedaten mit Base64-Codierung (optional)

Zum Senden von Protokollnachrichten muss das Gerät wie im folgenden Beispiel gezeigt ein `DiagnosticLog`-Objekt erstellen:

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

Sobald für das Gerät eine Verbindung zu {{site.data.keyword.iot_short_notm}} hergestellt wurde, kann die Protokollnachricht durch Aufrufen der Methode 'send()' wie im folgenden Beispiel gesendet werden:

```
log.send();
```

Später können neue Protokollnachrichten ohne großen Aufwand zu {{site.data.keyword.iot_short_notm}} hinzugefügt werden, indem die Methode 'append' wie im folgenden Beispiel gezeigt aufgerufen wird:

```
int rc = log.append("sample log", new Date(), DiagnosticLog.LogSeverity.informational);

if(rc == 200) {
    System.out.println("Current Log (" + log + ")");
} else {
    System.out.println("Log Addition failed");
}
```

Die Protokollnachrichten können auch aus {{site.data.keyword.iot_short_notm}} gelöscht werden, indem die Methode 'clear' wie im folgenden Beispiel gezeigt aufgerufen wird:

```
rc = log.clear();
if(rc == 200) {
    System.out.println("Logs are cleared successfully");
} else {
    System.out.println("Failed to clear the Logs")
}
```

Die Operationen zur Gerätediagnose sollen Informationen zu Gerätefehlern bereitstellen; sie geben keine Diagnoseinformationen an, die sich auf die Verbindung der Geräte zu {{site.data.keyword.iot_short_notm}} beziehen.

Weitere Informationen zu Diagnoseinformationen finden Sie in der [Dokumentation](../device_mgmt/operations/diagnostics.html).

## Firmwareaktionen
{: #firmware_actions}

Der Prozess für das Firmware-Update ist in zwei unterschiedliche Aktionen aufgeteilt:

* Herunterladen der Firmware
* Aktualisieren der Firmware

Das Gerät muss zum Unterstützen von Firmwareaktionen folgende Aktivitäten ausführen:

**1. Erstellen eines DeviceFirmware-Objekts**

Zum Ausführen von Firmwareaktionen muss das Gerät das `DeviceFirmware`-Objekt erstellen und es wie folgt zu `DeviceData` hinzufügen:

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

Das `DeviceFirmware`-Objekt stellt die aktuelle Firmware des Geräts dar und wird zum Berichten des Status für die Aktionen 'Firmware-Download' und 'Firmware-Update' an {{site.data.keyword.iot_short_notm}} verwendet.

**2. Informieren des Servers über die Firmwareaktionsunterstützung**

Für das Gerät muss für das Aktionsflag für Firmware 'true' eingestellt werden, damit der Server die Firmwareanforderung initiiert. Dies wird erreicht, wenn folgende Methode mit einem booleschen Wert aufgerufen wird:

```
managedDevice.supportsFirmwareActions(true);
managedDevice.manage();
```

Wenn die Managementanforderung {{site.data.keyword.iot_short_notm}} über die Unterstützung der Firmwareaktion benachrichtigt, muss die Methode 'manage()' sofort nach der Festlegung der Unterstützung für die Firmwareaktion aufgerufen werden.

**3. Erstellen des Firmwareaktionshandlers**

Zum Unterstützen der Firmwareaktion muss das Gerät einen Handler erstellen und ihn zu `ManagedDevice` hinzufügen. Der Handler muss eine `DeviceFirmwareHandler`-Klasse erweitern und folgende Methoden implementieren:

```
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**3.1 Beispielimplementierung von downloadFirmware**

Durch die Implementierung muss Logik hinzugefügt werden, um die Firmware herunterzuladen und den Status des Downloads mithilfe eines `DeviceFirmware`-Objekts zu berichten. Wenn die Operation für den Download der Firmware erfolgreich ist, wird der Status auf `DOWNLOADED` festgelegt und für `UpdateStatus` wird anschließend `SUCCESS` eingestellt.

Wenn während des Firmware-Downloads ein Fehler auftritt, wird für den Status die Einstellung `IDLE` festgelegt und für `updateStatus` wird anschließend einer der folgenden Werte für den Fehlerstatus eingestellt:

* `OUT_OF_MEMORY
* CONNECTION_LOST
* INVALID_URI`

Das folgende Beispiel zeigt die Implementierung eines Firmware-Downloads für ein Raspberry Pi-Gerät:

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
            // Verwenden Sie die Zeitmarke als Namen
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
            //Da keine Daten zum Lesen vorliegen, legen Sie einen Fehler fest
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.INVALID_URI);
        }
    } catch(MalformedURLException me) {
        // Ungültige URL, legen Sie als Status etwas fest, dass dies widerspiegelt
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

Ein Gerät kann die Integrität des heruntergeladenen Firmware-Image mithilfe der Verifizierung prüfen und den Status zurück an {{site.data.keyword.iot_short_notm}} berichten. Die Verifizierung kann während des Starts (während der Erstellung des DeviceFirmware-Objekts) vom Gerät oder im Rahmen der Anforderung 'Firmware herunterladen' von der Anwendung festgelegt werden. Nachfolgend finden Sie einen Beispielcode, mit dem dies überprüft werden kann:

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

Sie finden den vollständigen Code im Gerätemanagementbeispiel [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java).



**3.2 Beispielimplementierung von updateFirmware**

Durch die Implementierung muss Logik hinzugefügt werden, um die heruntergeladene Firmware zu installieren und den Status der Aktualisierung mithilfe des `DeviceFirmware`-Objekts zu berichten. Wenn die Operation für das Firmware-Update erfolgreich ist, sollte als Status der Firmware die Einstellung IDLE (inaktiv) und als `updateStatus` sollte `SUCCESS` (Erfolg) festgelegt sein.

Wenn während des Firmware-Updates ein Fehler auftritt, sollte für `updateStatus` einer der Werte des Fehlerstatus eingestellt werden:

`* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE`

Nachfolgend wird eine Beispielimplementierung des Firmware-Updates für ein Raspberry Pi-Gerät gezeigt:

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

Sie finden den vollständigen Code im Gerätemanagementbeispiel [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java).


**4. Hinzufügen des Handlers zu ManagedDevice**

Der erstellte Handler muss der ManagedDevice-Instanz hinzugefügt werden, sodass die Clientbibliothek 'ibmiotf' die entsprechende Methode aufruft, wenn eine Firmwareaktionsanforderung von {{site.data.keyword.iot_short_notm}} vorliegt.

```
DeviceFirmwareHandlerSample fwHandler = new DeviceFirmwareHandlerSample();
deviceData.addFirmwareHandler(fwHandler);
```

Weitere Informtionen zur Firmwareaktion finden Sie auf [dieser Seite](../device_mgmt/operations/firmware_actions.html).

## Geräteaktionen

{{site.data.keyword.iot_short_notm}} unterstützt folgende Geräteaktionen:

* Neu starten
* Zurücksetzen auf Werkseinstellungen

Das Geräte muss zur Unterstützung von Geräteaktionen folgende Aktivitäten ausführen:

**1. Informieren des Servers über die Geräteaktionsunterstützung**

Zum Ausführen von 'Neu starten' und 'Zurücksetzen auf Werkseinstellungen' muss das Gerät {{site.data.keyword.iot_short_notm}} zunächst über die zugehörige Unterstützung informieren. Dies wird erreicht, wenn folgende Methode mit einem booleschen Wert aufgerufen wird:

```
managedDevice.supportsDeviceActions(true);
    managedDevice.manage();
```

Wenn die Managementanforderung {{site.data.keyword.iot_short_notm}} über die Unterstützung der Geräteaktion benachrichtigt, muss die Methode 'manage()' sofort nach der Festlegung der Unterstützung für die Geräteaktion aufgerufen werden.

**2. Erstellen des Geräteaktionshandlers**

Zum Unterstützen der Geräteaktion muss das Gerät einen Handler erstellen und ihn zu 'ManagedDevice' hinzufügen. Der Handler muss eine DeviceActionHandler-Klasse erweitern und die Implementierung folgender Methoden vornehmen:

```
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**2.1 Beispielimplementierung von handleReboot**

Durch die Implementierung muss Logik hinzugefügt werden, um das Gerät neu zu starten und den Status von 'Neu starten' über das DeviceAction-Objekt berichten. Das Gerät muss den Status (zusammen mit der Ausgabe einer optionalen Nachricht) nur aktualisieren, falls ein Fehler auftritt (da das Gerät durch eine erfolgreiche Operation neu gestartet wird und der Gerätecode keine Steuerungsmöglichkeit für die Aktualisierung von {{site.data.keyword.iot_short_notm}} hat. Nachfolgend wird eine Beispielimplementierung von 'Neu starten' für ein Raspberry Pi-Gerät gezeigt:

```
public void handleReboot(DeviceAction action) {
    ProcessBuilder processBuilder = null;
    Process p = null;
    processBuilder = new ProcessBuilder("sudo", "shutdown", "-r", "now");
    boolean status = false;
    try {
        p = processBuilder.start();
        // Warten Sie ca. 2 Minuten, bevor Sie es aufgeben
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

Sie finden den vollständigen Code im Gerätemanagementbeispiel [DeviceActionHandlerSample].

  [DeviceActionHandlerSample]: https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java

**2.2 Beispielimplementierung von handleFactoryReset**

Durch die Implementierung muss Logik hinzugefügt werden, um das Gerät auf die Werkseinstellungen zurückzusetzen und den Status über das DeviceAction-Objekt zu berichten. Das Gerät muss den Status (zusammen mit der Ausgabe einer optionalen Nachricht nur aktualisieren, falls ein Fehler vorliegt (da das Gerät im Rahmen dieses Prozesses neu gestartet wird und das Gerät keine Steuerungsmöglichkeit hat, den Status von {{site.data.keyword.iot_short_notm}} zu aktualisieren). Das Gerüst für die Implementierung von 'Zurücksetzen auf Werkseinstellungen' wird nachfolgend gezeigt:

```
public void handleFactoryReset(DeviceAction action) {
    try {
        // Code für die Ausführung von 'Zurücksetzen auf Werkseinstellungen'
    } catch (IOException e) {
        action.setMessage(e.getMessage());
    }
    if(status == false) {
        action.setStatus(DeviceAction.Status.FAILED);
    }
}
```

**3. Hinzufügen des Handlers zu ManagedDevice**

Der erstellte Handler muss der ManagedDevice-Instanz hinzugefügt werden, sodass die Clientbibliothek 'ibmiotf' die entsprechende Methode aufruft, wenn eine Geräteaktionsanforderung von {{site.data.keyword.iot_short_notm}} vorliegt.

```
DeviceActionHandlerSample actionHandler = new DeviceActionHandlerSample();
deviceData.addDeviceActionHandler(actionHandler);
```

Weitere Informationen zur Geräteaktion finden Sie auf [dieser Seite](../device_mgmt/operations/device_actions.html).



## Empfangsbereit für Geräteattributänderungen sein
{: #listen_device_attribute}

Mit der Clientbibliothek 'ibmiotf' werden die entsprechenden Objekte jedes Mal aktualisiert, wenn eine Aktualisierungsanforderung von {{site.data.keyword.iot_short_notm}} vorliegt; diese Aktualisierungsanforderungen werden von der Anwendung entweder direkt oder indirekt (Firmware-Update) über die {{site.data.keyword.iot_short_notm}}-REST-API initiiert. Neben der Aktualisierung dieser Attribute bietet die Bibliothek einen Mechanismus, mit dem das Gerät benachrichtigt werden kann, sobald ein Geräteattribut aktualisiert wird.

Mit dieser Operation können die Attribute `location`, `metadata`, `device information` und `firmware` aktualisiert werden.

Damit eine Benachrichtigung erfolgt, muss das Gerät für die Objekte, die von Interesse sind, einen Listener für Eigenschaftsänderungen hinzufügen.

```
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

Das Gerät muss an der Position, an der die Benachrichtigung empfangen wird, außerdem die Methode `propertyChange()` hinzufügen. Das folgende Beispiel zeigt, wie dies implementiert werden kann:

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

Weitere Informationen zur Aktualisierung der Geräteattribute finden Sie auf [dieser Seite](../device_mgmt/operations/update.html).

## Beispiele
{: #examples}

-   [SampleRasPiDMAgent](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgent.java) - Beispielagentencode, der zeigt, wie verschiedene Gerätemanagementoperationen in Raspberry Pi ausgeführt werden können.
-   [SampleRasPiManagedDevice](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiManagedDevice.java) - Beispielagentencode, der zeigt, wie sowohl Geräteoperationen als auch Managementoperationen ausgeführt werden können.
-   [SampleRasPiDMAgentWithCustomMqttAsyncClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttAsyncClient.java) - Beispielagentencode mit einem angepassten MqttAsyncClient-Element.
-   [SampleRasPiDMAgentWithCustomMqttClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttClient.java) - Beispielagentencode mit einem angepassten MqttClient-Element.
-   [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java) - Beispielimplementierung von 'FirmwareHandler' für Raspberry Pi.
-   [DeviceActionHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java) - Beispielimplementierung von 'DeviceActionHandler'.
-   [ManagedDeviceWithLifetimeSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/ManagedDeviceWithLifetimeSample.java) - Beispiel, das zeigt, wie reguläre Managementanforderungen mit angegebener Lebenszeit gesendet werden.
-   [DeviceAttributesUpdateListenerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceAttributesUpdateListenerSample.java) - Beispielcode für den Listener, der zeigt, wie die Empfangsbereitschaft für verschiedene Geräteattributänderungen aussieht.
-   [NonBlockingDiagnosticsErrorCodeUpdateSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/NonBlockingDiagnosticsErrorCodeUpdateSample.java) - Beispielcode, der zeigt, wie Fehlercode (ErrorCode) hinzugefügt wird, ohne auf eine Antwort vom Server zu warten.

## Anleitungen
{: #Recipes}

Lesen Sie [die Anleitung](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-managed-device-to-ibm-iot-foundation/), in der gezeigt wird, wie das Raspberry Pi-Gerät als verwaltetes Gerät mit {{site.data.keyword.iot_short_notm}} verbunden wird, um Schritt für Schritt verschiedene Gerätemanagementoperationen mithilfe dieser Clientbibliothek auszuführen.
