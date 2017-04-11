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


# C# für Anwendungsentwickler
{: #c_sharp}


Verwenden Sie C#, um Anwendungen zu erstellen und anzupassen, die in {{site.data.keyword.iot_full}} mit Ihrer Organisation interagieren. Verwenden Sie die bereitgestellten Informationen und Beispiele, um mit der Entwicklung von Anwendungen mithilfe von C# zu beginnen.
{:shortdesc}

## C#-Client und Ressourcen herunterladen
{: #csharp_client_download}

Wechseln Sie für den Zugriff auf die C#-Clientbibliotheken und Beispiele für {{site.data.keyword.iot_short_notm}} in das Repository [iot-csharp ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-watson-iot/iot-csharp){: new_window} in GitHub und folgen Sie den Installationsanweisungen.


## Konstruktor
{: #constructor}

Der Konstruktor erstellt die Clientinstanz und akzeptiert Argumente, die folgende Definitionen enthalten:

|Definition |Beschreibung |
|:---|:---|
|`orgId`   |Die ID Ihrer Organisation.|
|`appId`   |Die eindeutige ID einer Anwendung in Ihrer Organisation.|
|`auth-key`   |API-Schlüssel, um Ihre Anwendung sicher mit Watson IoT Platform zu verbinden.|
|`auth-token`   |API-Schlüsseltoken, um Ihre Anwendung sicher mit Watson IoT Platform zu verbinden.|

Ist als einziges Argument `appId` angegeben, wird der Client als nicht registriertes Gerät mit dem Quickstart-Service von {{site.data.keyword.iot_short_notm}} verbunden. Die Argumentliste definiert die Art und Weise, wie der Client eine Verbindung zum {{site.data.keyword.iot_short_notm}}-Modul herstellt.

```
ApplicationClient applicationClient = new ApplicationClient(orgId, appId, apiKey, authToken);  
applicationClient.connect();
```


## Geräteereignisse subskribieren
{: #subscribe_device_events}

Geräte verwenden Ereignisse, um Daten in der {{site.data.keyword.iot_short_notm}}-Instanz zu publizieren. Das Gerät steuert den Inhalt des Ereignisses und ordnet jedem Ereignis, das von ihm gesendet wird, einen Namen zu.

Wenn ein Ereignis von der {{site.data.keyword.iot_short_notm}}-Instanz empfangen wird, geben die Berechtigungsnachweise des empfangenen Ereignisses das sendende Gerät an; dies bedeutet, dass ein Gerät nicht die Identität eines anderen Geräts annehmen kann.

Anwendungen subskribieren standardmäßig alle Ereignisse von allen verbundenen Geräten. Steuern Sie den Bereich der Subskription mithilfe der Parameter für den Geräte-Typ, die Geräte-ID, das Ereignis und das Nachrichtenformat. Folgende Codebeispiele zeigen, wie der Bereich einer Subskription mithilfe dieser Parameter definiert werden kann:

### Alle Ereignisse von allen Geräten subskribieren

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents();
```

### Alle Ereignisse von allen Geräten eines bestimmten Typs subskribieren

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType);
```

### Bestimmtes Ereignis von allen Geräten subskribieren

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(evt);
```

###  Bestimmtes Ereignis von mindestens zwei unterschiedlichen Geräten subskribieren

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt);
```

### Alle Ereignisse subskribieren, die im JSON-Format publiziert sind

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt, "json", 0);
```

**Hinweis**: Eine einzelne Clientinstanz kann mehrere Subskriptionen unterstützen.

### Ereignisse von Geräten verarbeiten

Zum Verarbeiten von Ereignissen, die über Ihre Subskriptionen empfangen werden, registrieren Sie wie im folgenden Beispiel gezeigt eine Callback-Methode für Ereignisse:

```
public static void processEvent(String eventName, string eventFormat, string eventData) {
// Führen Sie etwas aus
}
applicationClient.connect();
applicationClient.eventCallback += processEvent;
applicationClient.subscribeToDeviceEvents();
```
In der folgenden Tabelle werden die Parameter der Callback-Methode für Ereignisse beschrieben:

|Parameter|Datentyp|Beschreibung|
|:---|:---|
|`eventName`|Zeichenfolge|Gibt das Ereignis an. |
|`eventFormat`|Zeichenfolge| Das Format kann eine beliebige Zeichenfolge sein, zum Beispiel 'JSON'.|
|`eventData`|Wörterverzeichnis| Die Angaben für die Nachrichtennutzdaten. Die maximale Länge beträgt 131072 Byte.|


## Gerätestatus subskribieren
{: #subscribe_device_status}

Die Subskription ist standardmäßig so eingestellt, dass Statusaktualisierungen aller verbundenen Geräte empfangen werden. Steuern Sie den Bereich der Subskription mithilfe der Parameter für den Gerätetyp und die Geräte-ID. Folgende Codebeispiele zeigen, wie der Bereich einer Subskription mithilfe dieser Parameter definiert werden kann:

### Statusaktualisierungen aller Geräte subskribieren

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus();
```

### Statusaktualisierungen für zwei unterschiedliche Geräte subskribieren

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus(deviceType, deviceId);
```

**Hinweis**: Eine einzelne Clientinstanz kann mehrere Subskriptionen unterstützen.

### Statusaktualisierungen von Geräten verarbeiten

Zum Verarbeiten von Statusaktualisierungen, die über Ihre Subskriptionen empfangen werden, registrieren Sie wie im folgenden Beispiel gezeigt eine Callback-Methode für Ereignisse:

```
public static void processDeviceStatus(String deviceType, string deviceId, string data)
        {
           //
        }
applicationClient.connect();
applicationClient.appStatusCallback += processAppStatus;
applicationClient.subscribeToApplicationStatus();
```

## Ereignisse von Geräten publizieren
{: #publish_events_devices}

Anwendungen können Ereignisse so publizieren, als stammten sie von einem Gerät.

```
applicationClient.connect();
applicationClient.publishEvent(deviceType, deviceId, evt, data, 0);

```

In der folgenden Tabelle werden die Parameter beschrieben, die in der Methode `publishEvent()` angegeben sind:

|Parameter|Datentyp|Beschreibung|
|:---|:---|
|`deviceType`|Zeichenfolge| Der Gerätetyp. In der Regel ist 'deviceType' eine Zusammenfassung von Geräten, die eine bestimmte Aufgabe ausführen, beispielsweise 'Wetterballon'.|
|`deviceId`|Zeichenfolge| Die ID des Geräts. In der Regel ist 'deviceId' bei vorgegebenem Gerätetyp eine eindeutige Kennung des betreffenden Geräts, beispielsweise die Seriennummer oder MAC-Adresse.|
|`evt`|Zeichenfolge| Der Name des Ereignisses.|
|`format`|Zeichenfolge| Das Format kann eine beliebige Zeichenfolge sein, zum Beispiel 'JSON'.|
|`data`|Wörterverzeichnis| Die Angaben für die Nachrichtennutzdaten. Die maximale Länge beträgt 131072 Byte.|
|`QoS`|Ganze Zahl| Die Servicequalität. Gültige Werte sind `0`, `1`, `2`. |


## Befehle für Geräte publizieren
{: #publish_commands_devices}

Anwendungen können Befehle an verbundene Geräte publizieren.

```
applicationClient.connect();
applicationClient.publishCommand(deviceType, deviceId, "testcmd", "json", data, 0);
```
In der folgenden Tabelle werden die Parameter beschrieben, die in der Methode `publishCommand()` angegeben sind:

|Parameter|Datentyp|Beschreibung|
|:---|:---|
|`deviceType`|Zeichenfolge| Der Gerätetyp. In der Regel ist 'deviceType' eine Zusammenfassung von Geräten, die eine bestimmte Aufgabe ausführen, beispielsweise 'Wetterballon'.|
|`deviceId`|Zeichenfolge| Die ID des Geräts. In der Regel ist 'deviceId' bei vorgegebenem Gerätetyp eine eindeutige Kennung des betreffenden Geräts, beispielsweise die Seriennummer oder MAC-Adresse.|
|`command`|Zeichenfolge| Der Name des Befehls.|
|`format`|Zeichenfolge| Das Format kann eine beliebige Zeichenfolge sein, zum Beispiel 'JSON'.|
|`data`|Wörterverzeichnis| Die Angaben für die Nachrichtennutzdaten. Die maximale Länge beträgt 131072 Byte.|
|`QoS`|Ganze Zahl| Die Servicequalität. Gültige Werte sind `0`, `1`, `2`. |
