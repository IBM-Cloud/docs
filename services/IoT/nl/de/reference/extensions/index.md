---

copyright:
  years: 2015, 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Externe Services integrieren 
{: #ref-index}
Letzte Aktualisierung: 13. September 2016
{: .last-updated}

Die Integration von externen Services ermöglicht Ihnen den Zugriff auf Daten und Operationen von Drittanbietern oder externen Services innerhalb Ihrer {{site.date.keyword.iot_full}}-Organisation. 

## Jasper 
{: #jasper}

Jasper ist eine Verwaltungs- und Managementplattform für SIM-Geräte. Jasper ist in das Dashboard von {{site.data.keyword.iot_short_notm}} integriert, sodass es nun möglich ist, Jasper-Geräte über Ihr Organisationsdashboard von {{site.data.keyword.iot_short_notm}} zu verwalten. 

### Unterstützte Operationen für Jasper 

Die von Ihrer Plattform bereitgestellte Integration von Jasper bietet Unterstützung für folgende Jasper-Operationen: 

- Gesamte Jasper-Daten anzeigen 
  - Folgendes wird angezeigt: Status, Tarifplan, Datennutzung für den Monat bisher, SMS-Nutzung für den Monat bisher, Telefonnutzung für den Monat bisher, Überschreitungsgrenzwerte, Hinzufügungsdatum und Änderungsdatum. 
- SIM-Aktivierungsstatus ändern. 
  - Folgendes kann ausgewählt werden: Bestand, Aktivierungsbereit, Aktiviert, Inaktiviert und Ruhezustand. 
- SIM-Nutzung anzeigen 
  - Folgendes wird angezeigt: Zyklusstartdatum, abrechnungsfähige und gesamte Datennutzung, abrechnungsfähige und gesamte SMS-Nutzung, abrechnungsfähige und gesamte Telefonnutzung. 
  - Das Zyklusstartdatum kann im Format JJJJ-MM-TT festgelegt werden. 
- Send SMS to SIM 
- Tarifplan ändern 

Sie können auf diese Operationen im Geräte-Drilldown eines verbundenen Jasper-Geräts zugreifen, nachdem die nachfolgend beschriebenen Konfigurationsschritte abgeschlossen sind. 


### Konfiguration für Jasper 

Damit eine Verbindung zwischen Ihrem Jasper-Service mit Ihrer {{site.data.keyword.iot_short_notm}}-Organisation hergestellt werden kann, müssen zuvor zwei Konfigurationsphasen ausgeführt werden. Zunächst muss {{site.data.keyword.iot_short_notm}} mit Ihrem Jasper-Service verbunden werden, anschließend müssen Ihre {{site.data.keyword.iot_short_notm}}-Geräte konfiguriert werden. 


1. Jasper-Erweiterung aktivieren. Führen Sie folgende Schritte aus, um die Integration von Jasper in Ihre {{site.data.keyword.iot_short_notm}}-Organisation zu ermöglichen. 
  1. Wählen Sie im {{site.data.keyword.iot_short_notm}}-Dashboard die Option **Erweiterungen**. 
  2. Klicken Sie auf der Seite **Erweiterungen** auf **Erweiterung hinzufügen**. 
  3. Klicken Sie neben AT&T auf die Option **Hinzufügen**. 
  4. Geben Sie Ihren Benutzernamen, das Kennwort, den Zugriffsschlüssel und die Domänen-ID für AT&T ein. 
  5. Klicken Sie auf **Fertig**. 

2. Geräte konfigurieren
Sie können die Geräte, die sowohl mit Ihrer {{site.data.keyword.iot_short_notm}}-Organisation als auch mit Ihrem Jasper-Konto verbunden sind, so konfigurieren, dass Daten von Jasper im Dashboard von {{site.data.keyword.iot_short_notm}} angezeigt werden.
**Wichtig:** Die Jasper-Konfiguration kann nicht im Rahmen des Prozesses zum Hinzufügen von Geräten angewendet werden, nur zuvor bereits verbundene Geräte können mit Jasper konfiguriert werden.
Führen Sie folgende Schritte aus, um Ihre mit Jasper verbundenen Geräte zu konfigurieren: 
 1. Suchen Sie auf der Registerkarte 'Geräte' in Ihrem {{site.data.keyword.iot_short_notm}}-Dashboard nach dem zu konfigurierenden und mit Jasper verbundenen Gerät. 
 2. Wählen Sie das Gerät aus, um die Ansicht Drilldown-Ansicht für Geräte zu öffnen. 
 3. Blättern Sie abwärts zur Option *Erweiterungskonfiguration*. 
 4. Geben Sie die Erweiterungskonfiguration ein, indem Sie das folgende JSON-Format verwenden, und klicken Sie anschließend auf **Änderungen bestätigen**, um Ihre Konfiguration zu speichern.   

```json  
    {
        "jasper": {
            "iccid": "string"
        }
    }

```

Wenn die Organisation erfolgreich konfiguriert ist, wird der Abschnitt *Erweiterungen* unterhalb des Abschnitts zur Erweiterungskonfiguration in der Drilldown-Ansicht für Geräte angezeigt. 

## AT&T
{: #att}

### Unterstützte Operationen für AT&T 

Die AT&T-Erweiterung ermöglicht folgende AT&T-Operationen: 

- Gesamte AT&T- Daten anzeigen 
  - Folgendes wird angezeigt: Status, Tarifplan, Datennutzung für den Monat bisher, SMS-Nutzung für den Monat bisher, Telefonnutzung für den Monat bisher, Überschreitungsgrenzwerte, Hinzufügungsdatum und Änderungsdatum. 
- SIM-Aktivierungsstatus ändern. 
  - Folgendes kann ausgewählt werden: Bestand, Aktivierungsbereit, Aktiviert, Inaktiviert und Ruhezustand. 
- SIM-Nutzung anzeigen 
  - Folgendes wird angezeigt: Zyklusstartdatum, abrechnungsfähige und gesamte Datennutzung, abrechnungsfähige und gesamte SMS-Nutzung, abrechnungsfähige und gesamte Telefonnutzung. 
  - Das Zyklusstartdatum kann im Format JJJJ-MM-TT festgelegt werden. 
- Send SMS to SIM 
- Tarifplan ändern 

### Konfiguration für AT&T 

Um Ihre {{site.data.keyword.iot_short_notm}}-Organisation mit AT&T zu verbinden, müssen Sie eine Organisationskonfiguration und eine Gerätekonfiguration ausführen. 

Führen Sie folgende Schritte aus, um Ihre {{site.data.keyword.iot_short_notm}}-Plattform zu konfigurieren. 

1. AT&T-Erweiterung aktivieren. Führen Sie folgende Schritte aus, um die Integration von AT&T und der {{site.data.keyword.iot_short_notm}}-Organisation zu aktivieren: 
  1. Wählen Sie im {{site.data.keyword.iot_short_notm}}-Dashboard die Option **Erweiterungen**. 
  2. Klicken Sie auf der Seite **Erweiterungen** auf **Erweiterung hinzufügen**. 
  3. Klicken Sie neben AT&T auf die Option **Hinzufügen**. 
  4. Geben Sie Ihren Benutzernamen, das Kennwort, den Zugriffsschlüssel und die Domänen-ID für AT&T ein. 
  5. Klicken Sie auf **Fertig**. 

Zum Verbinden Ihrer {{site.data.keyword.iot_short_notm}}-Organisation mit Ihrem AT&T-Konto müssen zunächst zwei Konfigurationsphasen ausgeführt werden. Führen Sie die Konfiguration der Organisation aus und konfigurieren Sie anschließend Ihre Geräte. 


2. Geräte konfigurieren
Sie können die Geräte, die sowohl mit Ihrer {{site.data.keyword.iot_short_notm}}-Organisation als auch mit Ihrem AT&T-Konto verbunden sind, so konfigurieren, dass Daten von AT&T im {{site.data.keyword.iot_short_notm}}-Dashboard angezeigt werden.
**Wichtig:** Die AT&T-Konfiguration kann nicht im Rahmen des Prozesses zum Hinzufügen von Geräten angewendet werden, nur zuvor bereits verbundene Geräte können mit AT&T konfiguriert werden.
Führen Sie folgende Schritte aus, um Ihre mit AT&T verbundenen Geräte zu konfigurieren: 
 1. Suchen Sie auf der Registerkarte 'Geräte' in Ihrem {{site.data.keyword.iot_short_notm}}-Dashboard nach dem zu konfigurierenden und mit AT&T verbundenen Gerät. 
 2. Wählen Sie das Gerät aus, um die Ansicht Drilldown-Ansicht für Geräte zu öffnen. 
 3. Blättern Sie abwärts zur Option *Erweiterungskonfiguration*. 
 4. Geben Sie die Erweiterungskonfiguration ein, indem Sie das folgende JSON-Format verwenden, und klicken Sie anschließend auf **Änderungen bestätigen**, um Ihre Konfiguration zu speichern.   

```json  
    {
        "atnt": {
            "iccid": "string"
        }
    }

```

Wenn die Organisation erfolgreich konfiguriert ist, wird der Abschnitt *Erweiterungen* unterhalb des Abschnitts zur Erweiterungskonfiguration in der Drilldown-Ansicht für Geräte angezeigt. 

<!--
## ARM mbed connector
{: #arm}

The ARM mbed connector is an extension that allows you to connect your ARM mbed device to your {{site.data.keyword.iot_short_notm}}. The ARM mbed extension is allows the ARM mbed portal and the {{site.data.keyword.iot_short_notm}} to send and receive data from the ARM mbed portal.

### Setup Configuration


1. Enable the ARM mbed connector extension. To enable the ARM mbed connector extension complete the following steps:
  1. From the {{site.data.keyword.iot_short_notm}} dashboard, select **Settings** and navigate to **Extensions**.
  2. In the **Extensions** menu, click **Add Extension**.
  3. Click **Add** next to ARM mbed connector extension.
  4. Enter your ARM mbed access key and domain ID. You can find these by using the ARM mbed portal at https://connector.mbed.com.
  5. Check the credentials are correct by clicking the **Check Connection** button.
  6. Click **Done**.

### Payload Format

There are two types of incoming messages from the ARM mbed platform, notifications and asynchronous responses. The {{site.data.keyword.iot_short_notm}} can send commands to devices that are connected to the ARM mbed platform.

#### Notifications

Notifications are generated by changes in device or sensor data. After the {{site.data.keyword.iot_short_notm}} processes the message, it is to the device event topic in the same way as a device connected directly to the {{site.data.keyword.iot_short_notm}}. The event type used for notifications originating on devices connected to the ARM mbed platform is `notify`.

The following code sample shows the payload format for a notification sent by the ARM mbed platform API:

```
{
  "ep":<endpoint/deviceID>,
  "path":<resource path>,
  "ct":<content type>,
  "payload":<Base64 encoded payload>,
  "max-age":<how long the payload is valid, in seconds>
}
```

#### Asynchronous responses

When the {{site.data.keyword.iot_short_notm}} sends a command to a device connected to the ARM mbed platform, the device sends a confirmation message back to the {{site.data.keyword.iot_short_notm}}. This confirmation message is called an _asynchronous response_ and uses the event type `asyncResponse`.

The following code sample shows the payload format for an asynchronous response sent by the ARM mbed cloud service:

```
{
  "id":<transaction id>,
  "status":<200 is command was sucessfully executed. Check other HTTP response codes>,
  "ct":<content type>,
  "max-age":<how long the payload is valid, in seconds>,
  "payload":<base64 encoded payload>,
  "ep":<endpoint/deviceID affected by the command>,
  "path":<resource path affected by the command>
}
```

#### Sending commands to the ARM mbed platform

The {{site.data.keyword.iot_short_notm}} can send commands to devices connected to the ARM mbed platform. Commands sent to the ARM mbed platform it must use the following JSON format.

```
{
  "method":<PUT or POST>,
  "deviceId":<endpoint/deviceId>,
  "resourceId":<resource path>,
  "payload": <Base64 encoded payload>
}
```

The payload should be published to the following topic:

```
iot-2/type/<device_type>/id/<deviceId>/cmd/<command_type>/fmt/<command_format>
```
-->

## Orange 
{: #orange}

Die Orange-Erweiterung ermöglicht Ihnen die Daten der SIM-Karte von Geräten anzuzeigen, die mit {{site.data.keyword.iot_short_notm}} verbunden sind und in die eine Orange-SIM-Arte installiert ist. 

https://developer.ibm.com/iotplatform/2016/03/30/watson-iot-platform-integration-with-orange-beta/

### Unterstützte Operationen für Orange 

Wenn Sie ein Gerät haben, das mit Ihrem {{site.data.keyword.iot_short_notm}}-Service verbunden ist und eine Orange-SIM-Karte hat, können Sie die Orange-Erweiterung verwenden, um die folgenden Daten der SIM-Karte anzuzeigen: 

- SIM-Seriennummer 
- Aktivierungsstatus 
- Letzter Änderungsstatus 
- Letzter Aktualisierungsstatus 
- Standortstatus 

### Konfiguration für Orange 



Gehen Sie wie folgt vor, die Orange-Erweiterung zu aktivieren: 

1. Wählen Sie im {{site.data.keyword.iot_short_notm}}-Dashboard die Option **Erweiterungen**. 
2. Klicken Sie auf der Seite **Erweiterungen** auf **Erweiterung hinzufügen**. 
3. Klicken Sie neben der Orange-Erweiterung auf **Hinzufügen**. 
4. Geben Sie Ihren Benutzernamen und das Kennwort für Orange ein. 
6. Klicken Sie auf **Fertig**. 

Nach dem Aktivieren der Orange-Erweiterung muss jedes Gerät mit einer Orange-SIM-Karte für die Anzeige von Daten der Orange-SIM-Karte konfiguriert werden. 

1. Suchen Sie auf der Registerkarte 'Geräte' in Ihrem {{site.data.keyword.iot_short_notm}}-Dashboard nach dem zu konfigurierenden Orange-SIM-Gerät. 
2. Wählen Sie das Gerät aus und blättern Sie abwärts zu *Erweiterungskonfiguration*. 
3. Geben Sie die Erweiterungskonfiguration ein, indem Sie das folgende JSON-Format verwenden, und klicken Sie anschließend auf **Änderungen bestätigen**, um Ihre Konfiguration zu speichern. 

```  
    {
        "orange": {
            "serialnumber": "<Seriennummer der Orange-SIM>"
        }
    }

```
Wenn die Organisation erfolgreich konfiguriert ist, wird der Abschnitt *Erweiterungen* unterhalb des Abschnitts zur Erweiterungskonfiguration in der Drilldown-Ansicht für Geräte angezeigt.
## Gerätemanagementerweiterungen 
{: #device_mgmt}

Gerätemanagement ist eine zentrale Funktion von {{site.data.keyword.iot_short_notm}}; es kann jedoch erweitert werden, um zusätzliche Funktionen zu entwickeln. 

Die Gerätemanagementerweiterung ermöglicht es Ihnen, angepasste Funktionen für das Gerätemanagement zu installieren. Weitere Informationen zu angepassten Gerätemanagementfunktionen finden Sie in [angepasste Erweiterungen für das Gerätemanagement](../../devices/device_mgmt/custom_actions.html){: new_window}. 

## Blockchain 
{: #blockchain}

{{site.data.keyword.iot_short_notm}} mit Blockchain ermöglicht es IoT-Geräten, Daten für Blockchain-Transaktionen zur Verfügung zu stellen, wodurch die Daten im nicht veränderbaren Blockchain-Konto gespeichert und in Geschäftsregeln für intelligente Verträge verwendet werden. {{site.data.keyword.iot_short_notm}} ordnet Gerätedaten dem Datenformat zu, das für intelligente Blockchain-Verträge erforderlich ist, und übergibt sie zur Speichern im Blockchain-Konto an ein Blockchain-Fabric. 

### Unterstützte Operationen für Blockchain 
- Auslösen von Aktualisierungen für intelligente Verträge durch Geräteereignisse. 
- Ausführen von Geschäftslogik für intelligente Verträge, um den Kontostatus durch Ereignisdaten von Geräten zu aktualisieren. 
- Überwachen von Blockchain, von Transaktionen und des Kontostatus mit der Benutzerschnittstelle für die Überwachung. 

### Konfiguration für Blockchain 

{{site.data.keyword.iot_short_notm}}-Blockchain-Integration ist ein Serviceangebot, das in {{site.data.keyword.iot_short_notm}} nicht standardmäßig aktiviert ist. Führen Sie folgende Schritte aus, um die Funktion in Ihrer Umgebung zu aktivieren: 
 1. Wählen Sie im {{site.data.keyword.iot_short_notm}}-Dashboard die Option **Einstellungen** aus und navigieren Sie zu **Erweiterungen**. 
 2. Klicken Sie neben der Blockchain-Erweiterung auf den Link **Weitere Informationen**, um auf die Seite mit den Serviceangeboten von IoT-Blockchain zu wechseln. 
 3. Füllen Sie das Serviceanforderungsformular aus und übergeben Sie es.
Die Genehmigung des Service dauert in der Regel ca. einen Tag. Nach der Genehmigung Ihrer Anforderung erhalten Sie eine E-Mail mit Anweisungen, wie die Blockchain-Integration in Ihrer {{site.data.keyword.iot_short_notm}}-Organisation aktiviert wird. 
 5. Kehren Sie zu dem für Ihre Organisation gültigen {{site.data.keyword.iot_short_notm}}-Dashboard zurück, um das Setup zu beenden. Weitere Informationen finden Sie in [{{site.data.keyword.iot_short_notm}}-Blockchain-Integration](../../bl_blockchain_integration.html). 
