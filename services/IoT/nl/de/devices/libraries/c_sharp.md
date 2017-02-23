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


# C# für Geräteentwickler
{: #c_sharp}

Verwenden Sie C#, um Geräte zu erstellen und anzupassen, die in {{site.data.keyword.iot_full}} mit Ihrer Organisation interagieren. Verwenden Sie die bereitgestellten Informationen und Beispiele, um mit der Entwicklung Ihrer Geräte mithilfe von C# zu beginnen.
{:shortdesc}

## C#-Client und Ressourcen herunterladen
{: #csharp_client_download}

Wechseln Sie für den Zugriff auf den C#-Client und die Ressourcen Beispiele für {{site.data.keyword.iot_short_notm}} in GitHub in das Repository [iot-csharp](https://github.com/ibm-watson-iot/iot-csharp) und folgen Sie den Installationsanweisungen.


## Konstruktor
{: #constructor}

Der Konstruktor erstellt die Clientinstanz und akzeptiert Argumente, die folgende Definitionen enthalten:

|Definition |Beschreibung |
|:---|:---|
|`orgId`|Die ID Ihrer Organisation.|
|`deviceType`|Der Typ Ihres Geräts.|
|`deviceId` |Die ID Ihres Geräts.|
|`auth-method`   |Die zu verwendende Authentifizierungsmethode. Der einzige Wert, der aktuell unterstützt ist, lautet `token`.|
|`auth-token`   |Ein Authentifizierungstoken zum Herstellen einer sicheren Verbindung zwischen Ihrem Gerät und Watson IoT Platform.|


Wenn `deviceId` und `deviceType` die einzigen Argumente sind, die angegeben werden, stellt der Client eine Verbindung zum Quickstart-Service von {{site.data.keyword.iot_short_notm}} als nicht registriertes Gerät her. Die Argumentliste definiert die Art und Weise, wie der Client eine Verbindung zum {{site.data.keyword.iot_short_notm}}-Modul herstellt.


```
namespace com.ibm.iotf.client

public DeviceClient(string orgId, string deviceType, string deviceID, string auth-method, string auth-token)
        : base(orgId, "d" + CLIENT_ID_DELIMITER + orgId + CLIENT_ID_DELIMITER + deviceType + CLIENT_ID_DELIMITER + deviceID, "use-token-auth", auth-token)
    {

    }
```

## Ereignisse publizieren
{: #publishing-events}

Geräte verwenden Ereignisse, um Daten in der {{site.data.keyword.iot_short_notm}}-Instanz zu publizieren. Das Gerät steuert den Inhalt des Ereignisses und ordnet jedem Ereignis, das von ihm gesendet wird, einen Namen zu.

Wenn ein Ereignis von der {{site.data.keyword.iot_short_notm}}-Instanz empfangen wird, geben die Berechtigungsnachweise des eingehenden Ereignisses das sendende Gerät an; dies bedeutet, dass ein Gerät nicht die Identität eines anderen Geräts annehmen kann.

Ereignisse können mit einer beliebigen der drei durch das MQTT-Protokoll definierten [Servicequalitätsstufen (Qos)](../mqtt.html#managed-devices) publiziert werden. Standardmäßig werden Ereignisse mit der Servicequalitätsstufe (QoS) '0' publiziert.


## Ereignis mithilfe der standardmäßigen Servicequalitätsstufe publizieren
{: #publish_event_default_qos}

```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}");
```


## Ereignis mithilfe einer benutzerdefinierten Servicequalitätsstufe publizieren
{: #publish_event_user_qos}

Ereignisse, die mit einer MQTT-Servicequalitätsstufe publiziert werden, die höher als `0` ist, enthalten zusätzliche Empfangsbestätigungsinformationen und benötigen für die Publizierung möglicherweise länger als Ereignisse, die eine Servicequalitätsstufe von `0` aufweisen.


```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}", 2);
```

## Befehle verarbeiten
{: #handling_commands}

Wenn ein Geräteclient eine Verbindung herstellt, subskribiert er automatisch alle für dieses Geräte geltenden Befehle. Zum Verarbeiten bestimmter Befehle müssen Sie wie im folgenden Beispiel gezeigt eine Callback-Methode für Befehle registrieren:

```
public static void processCommand(string cmdName, string cmdFormat, string cmdData) {
...
 }
```

```
deviceClient.connect();
deviceClient.commandCallback += processCommand;
```
In der folgenden Tabelle werden die Parameter der Callback-Methode für Befehle beschrieben:

|Parameter|Datentyp|Beschreibung|
|:---|:---|
|`cmdName`|Zeichenfolge|Gibt den Befehl an. |
|`cmdFormat`|Zeichenfolge|Das Format kann eine beliebige Zeichenfolge sein, zum Beispiel 'JSON'.|
|`cmdData`|Wörterverzeichnis|Die Daten für die Nutzdaten. Die maximale Länge beträgt 131072 Byte.|
