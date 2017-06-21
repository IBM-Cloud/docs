---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-07"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# HTTP-REST-APIs für Gateway-Geräte
{: #api_link}


Weitere Informationen zum Zugriff auf die Dokumentation der {{site.data.keyword.iot_short_notm}}-HTTP-REST-API und zur Vorgehensweise beim Erstellen, Aktualisieren, Löschen und Auflisten von Geräten finden Sie in [{{site.data.keyword.iot_short_notm}}-HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html).

Die einzige unterstützte {{site.data.keyword.iot_short_notm}}-HTTP-REST-API ist Version 2. Stellen Sie sicher, dass Ihre {{site.data.keyword.iot_short_notm}}-Lösungen Version 2 verwenden.

## Clientverbindungen
{: #client_connections}

Informationen zur Clientsicherheit und zur Vorgehensweise beim Herstellen von Verbindungen zwischen Clients und Gateway-Geräten in {{site.data.keyword.iot_short_notm}} finden Sie in [Anwendungen, Geräte und Gateways mit {{site.data.keyword.iot_short_notm}} verbinden](../reference/security/connect_devices_apps_gw.html).


### Authentifizierung

Alle Anforderungen müssen einen Berechtigungsheader enthalten. Die Basisauthentifizierung ist die einzige Methode, die unterstützt ist. Wenn ein Gerät eine HTTP-Anforderung mithilfe der {{site.data.keyword.iot_short_notm}}-HTTP-REST-API übergibt, sind folgende Berechtigungsnachweise erforderlich:

|Berechtigungsnachweis|Erforderliche Eingabe|
|:---|:---|
|Benutzername| `g/{orgId}/{gwType}/{gwDevId}`
|Kennwort| Das Authentifizierungstoken, das beim Registrieren des Gateway-Geräts entweder automatisch generiert oder manuell angegeben wurde.

Dabei gilt:

<dl>
<dt>orgId</dt>  
<dd>Der Name der Organisation, der mit dem im Host-Header angegebenen Namen übereinstimmen muss.</dd>

<p></p>
<dt>gwType</dt>  
<dd>Der Typ von Gateway. </dd>
<p></p>
<dt>gwDevId</dt>  
<dd>Die Gerätekennung des Gateways. </dd>
</dl>


### Anforderungsheader des Typs 'Content-Type'

Zusammen mit der Anforderung muss ein Anforderungsheader des Typs `Content-Type` ('Inhaltstyp') angegeben werden. Die folgende Tabelle zeigt die Zuordnung der unterstützten Typen zu den internen {{site.data.keyword.iot_short_notm}}-Formaten:

|Header vom Typ 'Content-Type'|Format in {{site.data.keyword.iot_short_notm}}|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

## Cache für zuletzt gemeldete Ereignisse
{: #last-event-cache}

Durch Verwendung der {{site.data.keyword.iot_short_notm}}-API für zuletzt gemeldete Ereignisse können Sie das zuletzt von einem Gerät gesendete Ereignis abrufen. Diese API funktioniert unabhängig davon, ob das Gerät online oder offline ist, wodurch Sie den Gerätestatus unabhängig vom physischen Standort des Geräts oder dem Status seiner Verwendung abrufen können. Sie können den zuletzt aufgezeichneten Wert einer Ereignis-ID für ein bestimmtes Gerät oder den zuletzt aufgezeichneten Wert für alle Ereignis-IDs abrufen, die von einem bestimmten Gerät gemeldet wurden. Daten zum letzten Ereignis eines Geräts können für jedes Ereignis abgerufen werden, das nicht später als 365 Tage zurückliegt.

Zum Abfragen des letzten aktuellen Werts für eine bestimmte Ereignis-ID verwenden Sie die folgende API-Anforderung, die den zuletzt aufgezeichneten Wert für die Ereignis-ID 'power' (Spannung) zurückgibt:

```
GET /api/v0002/device/types/<Gerätetyp>/devices/<Geräte-ID>/events/power
```

Die Antwort wird im folgenden JSON-Format zurückgegeben:

```
{
    "deviceId": "<Geräte-ID>",
    "eventId": "power",
    "format": "json",
    "payload": "eyJzdGF0ZSI6Im9uIn0=",
    "timestamp": "2016-03-14T14:12:06.527+0000",
    "typeId": "<Gerätetyp>"
}
```

**Hinweis:** Auch wenn die API-Antwort das Format JSON hat, können Ereignisnutzdaten in einem beliebigen anderen Format geschrieben werden. Nutzdaten, die von der API für zuletzt gemeldete Ereignisse zurückgegeben werden, haben die Base64-Codierung.

Zum Abfragen des letzten aktuellen Werts für die einzelnen Ereignis-IDs, die von einem Gerät gemeldet wurden, verwenden Sie folgende API-Anforderung:

```
GET /api/v0002/device/types/<Gerätetyp>/devices/<Geräte-ID>/events
```

Die Antwort enthält alle Ereignis-IDs, die vom Gerät gesendet wurden. Im folgenden Beispiel werden Werte für die Ereignisse 'power' (Spannung) und 'temperature' (Temperatur) zurückgegeben.

```
[
    {
        "deviceId": "<Geräte-ID>",
        "eventId": "power",
        "format": "json",
        "payload": "eyJzdGF0ZSI6Im9uIn0=",
        "timestamp": "2016-03-14T14:12:06.527+0000",
        "typeId": "<Gerätetyp>"
    },
    {
        "deviceId": "<Geräte-ID>",
        "eventId": "temperature",
        "format": "json",
        "payload": "eyJpbnRlcm5hbCI6MjIsICJleHRlcm5hbCI6MTZ9",
        "timestamp": "2016-03-14T14:17:44.891+0000",
        "typeId": "<Gerätetyp>"
    }
]
```
