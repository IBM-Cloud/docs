---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Gerätemanagementprotokoll
{: #index}

## Einführung
{: #introduction}

{{site.data.keyword.iot_full}} erkennt zwei Geräteklassen: **Verwaltete Geräte** und **nicht verwaltete Geräte**.

**Verwaltete Geräte** sind als Geräte definiert, die über einen Gerätemanagementagenten verfügen. Ein Gerätemanagementagent ist eine Logikeinheit, die es dem Gerät ermöglicht, über das Gerätemanagementprotokoll mit dem {{site.data.keyword.iot_short_notm}}-Gerätemanagementservice zu interagieren. Verwaltete Geräte können Gerätemanagementoperationen einschließlich von Positionsaktualisierungen, Firmware-Downloads und Aktualisierungen, Neustarts und das Zurücksetzen auf Werkseinstellungen ausführen.

Das Gerätemanagementprotokoll definiert eine Gruppe von unterstützten Operationen. Ein Gerätemanagementagent kann eine Untergruppe der Operationen unterstützen, die Operationen der **verwalteten Geräte** und der **nicht verwalteten Geräte** müssen unterstützt werden. Ein Gerät, das Operationen für Firmwareaktionen unterstützt, muss auch Beobachtungen unterstützen.

Ein Gerätemanagementprotokoll wird auf der Grundlage eines MQTT-Nachrichtenprotokolls erstellt. Weitere Informationen zu der Vorgehensweise, wie das Gerätemanagementprotokoll mit MQTT interagiert, finden Sie in [MQTT-Konnektivität für Geräte](../mqtt.html).


### Lebenszyklus im Gerätemanagement

1. Ein Gerät und sein zugeordneter Gerätetyp werden in {{site.data.keyword.iot_short_notm}} mithilfe des Dashboards oder der REST-API erstellt.
2. Ein Gerät stellt eine Verbindung zu {{site.data.keyword.iot_short_notm}} her und verwendet die Operation für **verwaltete Geräte**, um ein verwaltetes Gerät zu werden.
3. Sie können die Metadaten eines Geräts anzeigen und bearbeiten, indem Sie die Geräteoperationen verwenden. Diese Operationen - beispielsweise die Operationen für das Firmware-Update und den Geräteneustart - sind in der Dokumentation zum Gerätemodell umrissen. Weitere Informationen zum Gerätemodell finden Sie in [Gerätemodell](https://console.ng.bluemix.net/docs/services/IoT/reference/device_model.html).
4. Ein Gerät kann Aktualisierungen zu seiner Position, zu Diagnoseinformationen und Fehlercodes mithilfe des Gerätemanagementprotokolls kommunizieren.
5. Zum Handhaben nicht mehr vorhandener Geräte in Beständen mit einer großen Zahl von Geräten enthält die Anforderung für die Operation **Verwaltete Geräte** einen optionalen Parameter für den Lebenszyklus. Der Parameter für den Lebenszyklus ist die Anzahl der Sekunden, in denen das Geräte eine weitere Anforderung des Typs **Verwaltete Geräte** vornehmen muss, um zu verhindern, dass es als 'ruhend' klassifiziert und damit zu einem 'nicht verwalteten Gerät' wird.
6. Wenn ein Gerät stillgelegt wird, können Sie es mithilfe des Dashboards oder der REST-API aus {{site.data.keyword.iot_short_notm}} entfernen.

Siehe die Anleitung [Raspberry Pi als verwaltetes Gerät mit IBM Watson IoT Platform verbinden](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-managed-device-to-ibm-iot-foundation/).

### Zusammenfassung der Rückkehrcodes


Die folgende Tabelle zeigt die Rückkehrcodes an, die in verschiedenen Stadien des Lebenszyklus des Geräts generiert werden.

|Rückkehrcode |Nachricht |
|:---|:---|
|200   |Operation erfolgreich|
|202   |Akzeptiert (für initiierende Befehle)|
|204   |Geändert (für Attributaktualisierungen)|
|400   |Falsche Anforderung (Beispiel: Ein Gerät befindet sich für diesen Befehl nicht im entsprechenden Status)|
|404   |Attribut wurde nicht gefunden (wird auch verwendet, wenn die Operation in einem ungültigen Topic publiziert wurde)|
|409   |Ressource wegen Konflikt nicht aktualisiert (Beispiel: Wenn eine Ressource durch zwei simultane Anforderungen aktualisiert wird, kann eine Aktualisierung später erneut versucht werden)|
|500   |Nicht erwarteter Gerätefehler|
|501   |Operation nicht implementiert|


## Anforderungen des Typs 'Gerät verwalten'
{: #manage_device_request}

Ein Gerät verwendet die Anforderung 'Gerät verwalten', um ein verwaltetes Gerät zu werden. Die Anforderung 'Gerät verwalten' muss die erste Gerätemanagementanforderung sein, die nach dem Herstellen einer Verbindung zu {{site.data.keyword.iot_short_notm}} von dem Gerät gesendet wird. Ein Gerätemanagementagent sendet diesen Anforderungstyp in der Regel bei jedem Start oder Neustart.

**Wichtig:** Unterstützung für diese Operation ist für alle verwalteten Geräte obligatorisch.


### Topic für eine Anforderung des Typs 'Gerät verwalten'

Ein Gerät publiziert eine Anforderung des Typs 'Gerät verwalten' im folgenden Topic:

```
iotdevice-1/mgmt/manage
```

Der Server antwortet auf eine Anforderung des Typs 'Gerät verwalten' im folgenden Topic:

```
iotdm-1/response
```




### Nachrichtenformat für eine Anforderung des Typs 'Gerät verwalten'


In einer Anforderung des Typs 'Gerät verwalten' sind das Feld `d` und alle seine untergeordneten Felder optional. Die Werte der Felder `metadata` und `deviceInfo` ersetzen die entsprechenden Attribute für das sendende Gerät, falls sie gesendet werden.

Das optionale Feld `lifetime` gibt den Zeitraum in Sekunden an, in dem das Gerät eine weitere Anforderung des Typs 'Gerät verwalten' senden muss, um nicht als 'ruhend' klassifiziert und ein nicht verwaltetes Gerät zu werden. Wenn das Feld `lifetime` ausgelassen oder auf `0` gesetzt wird, wird das verwaltete Gerät nicht 'ruhend'. Der für das Feld `lifetime` unterstützte Mindestwert lautet `3600` Sekunden, das heißt, eine Stunde.

Die optionalen Felder `supports.deviceActions` und `supports.firmwareActions` geben die Möglichkeiten des Gerätemanagementagenten an. Wenn `supports.deviceActions` festgelegt wird, unterstützt der Agent sowohl die Aktion für den Neustart als auch die Aktion für das Zurücksetzen auf die Werkseinstellungen. Für ein Gerät, das nicht zwischen einem Neustart und dem Zurücksetzen auf Werkseinstellungen unterscheidet, ist es akzeptabel, dass für beide Aktionen dasselbe Verhalten verwendet wird. Wenn `supports.firmwareActions` festgelegt ist, unterstützt der Agent sowohl die Aktionen für den Firmware-Download als auch für das Firmware-Update.

Das folgende Beispiel zeigt das Anforderungsformat:

```
Ausgehende Nachricht vom Gerät:

Topic: iotdevice-1/mgmt/manage
{
    "d": {
        "metadata":{},
        "lifetime": number,
        "supports": {
            "deviceActions": boolean,
            "firmwareActions": boolean
        },
        "deviceInfo": {
            "serialNumber": "string",
            "manufacturer": "string",
            "model": "string",
            "deviceClass": "string",
            "description" :"string",
            "fwVersion": "string",
            "hwVersion": "string",
            "descriptiveLocation": "string"
        }
    },
    "reqId": "string"
}
```

Das folgende Beispiel zeigt das Antwortformat:

```
Eingehende Nachricht vom Server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```


### Antwortcodes für eine Anforderung des Typs 'Gerät verwalten'

|Antwortcode |Nachricht |
|:---|:---|
|200   |Die Operation war erfolgreich.|
|400   |Die Eingabenachricht stimmt nicht mit dem erwarteten Format überein oder einer der Werte liegt außerhalb des gültigen Bereichs.|
|404   |Der Topicname ist falsch oder das Gerät ist nicht in der Datenbank vorhanden.|
|409   |Bei der Gerätedatenbankaktualisierung trat ein Konflikt auf. Vereinfachen Sie, falls erforderlich, die Operation, um den Konflikt zu lösen.|


## Anforderungen des Typs 'Gerät nicht verwalten'
{: #manage-unmanage}


Ein Gerät verwendet eine Anforderung des Typs 'Gerät nicht verwalten', wenn eine Verwaltung nicht mehr erforderlich ist. Wenn ein Gerät nicht mehr verwaltet wird, sendet {{site.data.keyword.iot_short_notm}} keine neuen Gerätemanagementanforderungen an das Gerät. Nicht verwaltete Geräte publizieren weiterhin Fehlercodes, Protokollnachrichten und Positionsnachrichten.
**Wichtig:** Unterstützung für diese Operation ist für alle verwalteten Geräte obligatorisch.

### Topic für die Anforderung 'Gerät nicht verwalten'


Ein Gerät publiziert eine Anforderung des Typs 'Gerät nicht verwalten' im folgenden Topic:

```
iotdevice-1/mgmt/unmanage
```

Der Server antwortet auf eine Anforderung des Typs 'Gerät nicht verwalten' im folgenden Topic:

```
iotdm-1/response
```

### Nachrichtenformat für eine Anforderung des Typs 'Gerät nicht verwalten'

Anforderungsformat:

```
Ausgehende Nachricht vom Gerät:

Topic: iotdevice-1/mgmt/unmanage
{
    "reqId": "string"
}
```

Antwortformat:

```
Eingehende Nachricht vom Server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Antwortcodes für eine Anforderung des Typs 'Nicht verwaltetes Gerät'

|Antwortcode |Nachricht |
|:---|:---|
|200   |Die Operation war erfolgreich.|
|400   |Die Eingabenachricht stimmt nicht mit dem erwarteten Format überein oder einer der Werte liegt außerhalb des gültigen Bereichs.|
|404   |Der Topicname ist falsch oder das Gerät ist nicht in der Datenbank vorhanden.|
|409   |Bei der Gerätedatenbankaktualisierung trat ein Konflikt auf. Vereinfachen Sie, falls erforderlich, die Operation, um den Konflikt zu lösen.|


## Anforderung 'Position aktualisieren'
{: #update-location}

Ein Gerät verwendet eine Anforderung des Typs 'Position aktualisieren', um die Positionsdaten für ein Gerät zu verwalten. Die Metadaten zur Position eines Geräts können in {{site.data.keyword.iot_short_notm}} anhand folgender Möglichkeiten aktualisiert werden:

#### Automatische Aktualisierungen der Geräteposition
- Das Gerät benachrichtigt {{site.data.keyword.iot_short_notm}} über die Aktualisierung der Position. Das Gerät ruft seine Position von einem GPS-Empfänger ab und sendet eine Gerätemanagementnachricht an die {{site.data.keyword.iot_short_notm}}-Instanz, um seine Position zu aktualisieren. Anhand einer Zeitmarke wird der Zeitpunkt erfasst, an dem die Position vom GPS-Empfänger abgerufen wurde. Die Zeitmarke ist gültig, auch wenn beim Senden der Nachricht zur Aktualisierung der Position eine Verzögerung auftritt. Wenn die Zeitmarke in der Gerätemanagementnachricht ausgelassen wird, werden das Datum und die Uhrzeit des Nachrichtenempfangs verwendet, um die Metadaten zur Position zu aktualisieren.

#### Manuelle Aktualisierungen der Geräteposition mithilfe der REST-API
- Sie können die Metadaten zur Position für ein statisches Gerät manuell festlegen, indem Sie beim Registrieren des Geräts die {{site.data.keyword.iot_short_notm}}-REST-API verwenden. Sie können die Position auch später ändern. Die Einstellung der Zeitmarke ist optional; wird sie jedoch ausgelassen, werden das aktuelle Datum und die Uhrzeit in den Metadaten zur Position des Geräts festgelegt.

### Positionsaktualisierungen, die von Geräten ausgelöst werden

Für Geräte, die ihre Position bestimmen können, kann ausgewählt werden, dass der {{site.data.keyword.iot_short_notm}}-Gerätemanagementserver über Positionsänderungen benachrichtigt wird.

### Topic für eine Anforderung des Typs 'Position aktualisieren', die durch ein Gerät ausgelöst wird:


Ein Gerät publiziert eine Anforderung des Typs 'Position aktualisieren' im folgenden Topic:

```
iotdevice-1/device/update/location
```

Der Server antwortet auf eine Anforderung des Typs 'Position aktualisieren' im folgenden Topic:

```
iotdm-1/response
```

### Positionsaktualisierung, die von Benutzern oder Apps ausgelöst wird


Wenn ein Benutzer oder eine Aktualisierung die Position eines aktiven verwalteten Geräts aktualisiert, ruft das Gerät eine Aktualisierungsnachricht ab.




### Topic für eine Anforderung des Typs 'Position aktualisieren', die von Benutzern oder Apps ausgelöst wird


Der Server publiziert eine Anforderung des Typs 'Position aktualisieren' im folgenden Topic:

```
iotdm-1/device/update
```

### Nachrichtenformat für eine Anforderung des Typs 'Position aktualisieren'


Das Feld `measuredDateTime` ist das Datum der Positionsmessung. Das Feld `updatedDateTime` gibt das Datum der Aktualisierung für die Geräteinformationen an. Aus Effizienzgründen werden die Aktualisierungen der Positionsinformationen von {{site.data.keyword.iot_short_notm}} manchmal im Stapelbetrieb ausgeführt, wodurch die Aktualisierungen leicht verzögert sind. Der Breitengrad und der Längengrad muss anhand des World Geodetic System 1984 (WGS84) in Dezimalgraden angegeben werden.

Bei jeder Aktualisierung der Position werden die für den Breiten- und den Längengrad, die Höhe und die Unsicherheit angegebenen Werte als einzige mehrwertige Aktualisierung betrachtet. Der Breiten- und der Längengrad sind obligatorisch und sie müssen bei jeder Aktualisierung angegeben werden.  Die Höhe und die Unsicherheit sind optional und sie können ausgelassen werden.

Wenn bei einer Aktualisierung ein optionaler Wert angegeben und bei einer späteren Aktualisierung ausgelassen wird, wird der frühere Wert durch die spätere Aktualisierung gelöscht. Jede Aktualisierung wird als vollständige mehrwertige Aktualisierung betrachtet.

### Positionsaktualisierungen, die durch das Gerät ausgelöst werden


Anforderungsformat:

```
Ausgehende Nachricht vom Gerät:

Topic: iotdevice-1/device/update/location
{
    "d": {
        "longitude": number,
        "latitude": number,

        "elevation": number,
        "measuredDateTime": "string in ISO8601 format",
        "updatedDateTime": "string in ISO8601 format",
        "accuracy": number
    },
    "reqId": "string"
}
```

Antwortformat:

```
Eingehende Nachricht vom Server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Antwortcodes für eine Anforderung des Typs 'Position aktualisieren'

|Antwortcode |Nachricht |
|:---|:---|
|200   |Die Operation war erfolgreich.|
|400   |Die Eingabenachricht stimmt nicht mit dem erwarteten Format überein oder einer der Werte liegt außerhalb des gültigen Bereichs.|
|404   |Der Topicname ist falsch oder das Gerät ist nicht in der Datenbank vorhanden.|
|409   |Bei der Gerätedatenbankaktualisierung trat ein Konflikt auf. Vereinfachen Sie, falls erforderlich, die Operation, um den Konflikt zu lösen.|


### Positionsaktualisierungen, die von Benutzern oder Apps ausgelöst werden


Das folgende Beispiel umreißt das Nutzdatenformat:

```
Eingehende Nachricht vom Server:

Topic: iotdm-1/device/update
{
    "d": {
        "fields": [
            {
                "field": "location",
                "value": {
                    "latitude": number,
                    "longitude": number,
                    "elevation": number,
                    "accuracy": number,
                    "measuredDateTime": "string in ISO8601 format"
                }
            }
        ]
    }
}
```

**Hinweis:** Der Parameter `reqID` wird nicht verwendet, da das Gerät nicht antworten muss.

## Anforderungen des Typs 'Geräteattribute aktualisieren'
{: #update-attributes}

Mithilfe der REST-API kann {{site.data.keyword.iot_short_notm}} eine Anforderung an ein Gerät senden, um den Wert mindestens eines der folgenden Geräteattribute zu aktualisieren:


|Attribut | Weitere Informationen|
|:---|:---|
|location  | Siehe [Position aktualisieren](index.html#update-location)|
|metadata  | Optional|
|deviceInfo | Optional|
|mgmt.firmware | Siehe [Firmware-Update-Prozess](requests.html#firmware-actions-update)|

### Topic für eine Anforderung des Typs 'Geräteattribute aktualisieren'


Der Server publiziert eine Anforderung des Typs 'Geräteattribute aktualisieren' im folgenden Topic:

```
iotdm-1/device/update
```


### Nachrichtenformat für eine Anforderung des Typs 'Geräteattribute aktualisieren'


Das folgende Beispiel umreißt das Nutzdatenformat für die Anforderung:

```
Eingehende Nachricht vom Server:

Topic: iotdm-1/device/update
{
    "d": {
        "fields": [
            {
                "field": "location",
                "value": ""
            }
        ]
    }
}
```


## Anforderungen des Typs 'Fehlercode hinzufügen'
{: #diag-add-error-code}

Geräte können festlegen, den Gerätemanagementserver von {{site.data.keyword.iot_short_notm}} mithilfe des Anforderungstyps 'Fehlercode hinzufügen' über Änderungen ihres Fehlerstatus zu benachrichtigen.

### Topic für eine Anforderung des Typs 'Fehlercode hinzufügen'


Ein Gerät publiziert eine Anforderung des Typs 'Fehlercode hinzufügen' im folgenden Topic:

```
iotdevice-1/add/diag/errorCodes
```

### Nachrichtenformat für eine Anforderung des Typs 'Fehlercode hinzufügen'


Der `errorCode` zugeordnete Wert ist der aktuelle Fehlercode des Geräts und muss der {{site.data.keyword.iot_short_notm}}-Instanz hinzugefügt werden.

Anforderungsformat:

```
Ausgehende Nachricht vom Gerät:

Topic: iotdevice-1/add/diag/errorCodes
{
    "d": {
        "errorCode": number
    },
    "reqId": "string"
}
```

Antwortformat:

```
Eingehende Nachricht vom Server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Antwortcodes für eine Anforderung des Typs 'Fehlercode hinzufügen'

|Antwortcode |Nachricht |
|:---|:---|
|200   |Die Operation war erfolgreich.|
|400   |Die Eingabenachricht stimmt nicht mit dem erwarteten Format überein oder einer der Werte liegt außerhalb des gültigen Bereichs.|
|404   |Der Topicname ist falsch oder das Gerät ist nicht in der Datenbank vorhanden.|
|409   |Bei der Gerätedatenbankaktualisierung trat ein Konflikt auf. Vereinfachen Sie, falls erforderlich, die Operation, um den Konflikt zu lösen.|


## Anforderungen des Typs 'Fehlercodes löschen'
{: #diag-clear-error-codes}

Geräte können anfordern, dass {{site.data.keyword.iot_short_notm}} alle Fehlercodes für das Gerät mithilfe des Anforderungstyps 'Fehlercodes löschen' löscht.

### Topic für eine Anforderung des Typs 'Fehlercodes löschen'


Ein Gerät publiziert diese Anforderung im folgenden Topic:

```
iotdevice-1/clear/diag/errorCodes
```

### Nachrichtenformat für eine Anforderung des Typs 'Fehlercodes löschen'


Anforderungsformat:

```
Ausgehende Nachricht vom Gerät:

Topic: iotdevice-1/clear/diag/errorCodes
{
    "reqId": "string"
}
```

Antwortformat:

```
Eingehende Nachricht vom Server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Antwortcodes für eine Anforderung des Typs 'Fehlercodes löschen'

|Antwortcode |Nachricht |
|:---|:---|
|200   |Die Operation war erfolgreich.|
|400   |Die Eingabenachricht stimmt nicht mit dem erwarteten Format überein oder einer der Werte liegt außerhalb des gültigen Bereichs.|
|404   |Der Topicname ist falsch oder das Gerät ist nicht in der Datenbank vorhanden.|
|409   |Bei der Gerätedatenbankaktualisierung trat ein Konflikt auf. Vereinfachen Sie, falls erforderlich, die Operation, um den Konflikt zu lösen.|


## Anforderungen des Typs 'Protokoll hinzufügen'
{: #diag-add-log}

Für Geräte kann festgelegt werden, ob die {{site.data.keyword.iot_short_notm}}-Gerätemanagementunterstützung über Änderungen benachrichtigt werden soll, indem ein neuer Protokolleintrag hinzugefügt wird. Protokolleinträge enthalten eine Protokollnachricht, eine Zeitmarke, den Schweregrad und optional die mit Base64 codierten binären Diagnosedaten.

### Topic für eine Anforderung des Typs 'Protokoll hinzufügen'
Ein Gerät publiziert diese Anforderung im folgenden Topic:

```
iotdevice-1/add/diag/log
```


### Nachrichtenformat für eine Anforderung des Typs 'Protokoll hinzufügen'

In der folgenden Tabelle wird das Format der Attribute der ausgehenden Nachricht beschrieben:

|Attribut |Beschreibung |
|:---|:---|
|`message`|Gibt eine Diagnosenachricht an, die der {{site.data.keyword.iot_short_notm}}-Instanz hinzugefügt werden muss|
|`timestamp`|Gibt das Datum und die Uhrzeit des Protokolleintrags im Format ISO8601 an |
|`data`|Gibt optionale, mit Base64 codierte Diagnosedaten an|
|`severity`|Gibt den Schweregrad der Nachricht an (0: Informationsnachricht, 1: Warnung, 2: Fehler)|


Anforderungsformat:

```
Ausgehende Nachricht vom Gerät:

Topic: iotdevice-1/add/diag/log
{
    "d": {
        "message": string,
        "timestamp": string,
        "data": string,
        "severity": number
    },
    "reqId": "string"
}
```

Antwortformat:

```
Eingehende Nachricht vom Server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```


### Antwortcodes für eine Anforderung des Typs 'Protokoll hinzufügen'

|Antwortcode |Nachricht |
|:---|:---|
|200   |Die Operation war erfolgreich.|
|400   |Die Eingabenachricht stimmt nicht mit dem erwarteten Format überein oder einer der Werte liegt außerhalb des gültigen Bereichs.|
|404   |Der Topicname ist falsch oder das Gerät ist nicht in der Datenbank vorhanden.|
|409   |Bei der Gerätedatenbankaktualisierung trat ein Konflikt auf. Vereinfachen Sie, falls erforderlich, die Operation, um den Konflikt zu lösen.|

## Anforderungen des Typs 'Protokolle löschen'
{: #diag-clear-logs}

Geräte können anfordern, dass {{site.data.keyword.iot_short_notm}} mithilfe des Anforderungstyps 'Protokolle löschen' alle Protokolleinträge für das Gerät löscht.

### Topic für eine Anforderung des Typs 'Protokolle löschen'


Ein Gerät publiziert die Anforderung 'Protokolle löschen' im folgenden Topic:

```
iotdevice-1/clear/diag/log
```

### Nachrichtenformat für eine Anforderung des Typs 'Protokolle löschen'


Anforderungsformat:

```
Ausgehende Nachricht vom Gerät:

Topic: iotdevice-1/clear/diag/log
{
    "reqId": "string"
}
```

Antwortformat:

```
Ausgehende Nachricht vom Gerät:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Antwortcodes für eine Anforderung des Typs 'Protokolle löschen'

|Antwortcode |Nachricht |
|:---|:---|
|200   |Die Operation war erfolgreich.|
|400   |Die Eingabenachricht stimmt nicht mit dem erwarteten Format überein oder einer der Werte liegt außerhalb des gültigen Bereichs.|
|404   |Der Topicname ist falsch oder das Gerät ist nicht in der Datenbank vorhanden.|
|409   |Bei der Gerätedatenbankaktualisierung trat ein Konflikt auf. Vereinfachen Sie, falls erforderlich, die Operation, um den Konflikt zu lösen.|

## Anforderungen des Typs 'Attributänderungen beobachten'
{: #observations-observe}

{{site.data.keyword.iot_short_notm}} kann eine Anforderung des Typs 'Attributänderungen beobachten' an ein Gerät senden, um mithilfe des Anforderungstyps 'Attributänderungen beobachten' die Änderungen mindestens eines Geräteattributs zu beobachten. Wenn das Gerät die Anforderung empfängt, muss es bei jeder Änderung der Werte für die beobachteten Attribute eine Benachrichtigungsanforderung an {{site.data.keyword.iot_short_notm}} senden.

**Wichtig:** Geräte müssen Operationen zum Beobachten, Benachrichtigen und Abbrechen implementieren, um Anforderungen des Typs [Firmwareaktionen - Update](requests.html#firmware-actions-update) zu unterstützen.

### Topic für eine Anforderung des Typs 'Attributänderungen beobachten'


Der Server publiziert eine Anforderung des Typs 'Attributänderungen beobachten' im folgenden Topic:

```
iotdm-1/observe
```

### Nachrichtenformat für eine Anforderung des Typs 'Attributänderungen beobachten'


Der Array `fields` ist ein Array des Geräteattributs vom Gerätemodell. Bei Angabe eines komplexen Feldes wie beispielsweise `mgmt.firmware` wird erwartet, dass seine zugrunde liegenden Felder zum selben Zeitpunkt aktualisiert werden, sodass nur eine einzige Benachrichtigungsnachricht generiert wird.

Der Parameter `message`, der in der Antwort verwendet wird, kann angegeben werden, wenn der Wert des Parameters `rc` nicht `200` lautet. Wenn ein bestimmter Parameterwert nicht abgerufen werden kann, muss für den Parameter `rc` der Wert `404` eingestellt werden, wenn das Gerät nicht gefunden wurde, oder der Wert `500`, falls eine andere Ursache vorliegt. Wenn Werte für Parameter nicht gefunden werden können, sollte die Feldgruppe `fields` Elemente enthalten, bei denen für `field` die Namen der einzelnen Parameter festgelegt sind, die nicht gelesen werden konnten. Der Parameter `value` sollte weggelassen werden. Damit der Parameter für den Antwortcode auf `200` eingestellt werden kann, muss sowohl das Feld `field` als auch `value` angegeben werden, wobei `value` der aktuelle Wert eines Attributs ist, das durch den Wert des Parameters `field` angegeben wird.

Anforderungsformat:

```
Eingehende Nachricht vom Server:

Topic: iotdm-1/observe
{
    "d": {
        "fields": [
            "string"
        ]
    },
    "reqId": "string"
}
```

Antwortformat:

```
Ausgehende Nachricht vom Gerät:

Topic: iotdevice-1/response
{
    "rc": number,
    "message": "string",
    "d": {
        "fields": [
            {
                "field": "field_name",
                "value": "field_value"
            }
        ]
    },
    "reqId": "string"
}
```


## Anforderungen des Typs 'Attributbeobachtung abbrechen'
{: #observations-cancel}

{{site.data.keyword.iot_short_notm}} kann mithilfe des Anforderungstyps 'Attributbeobachtung abbrechen' eine Anforderung an ein Gerät senden, dass die aktuelle Beobachtung mindestens eines der Geräteattribute abgebrochen werden soll. Der `fields`-Teil der Anforderung ist eine Feldgruppe der Geräteattributnamen aus dem Gerätemodell, beispielsweise die Parameter `location`, `mgmt.firmware` oder `mgmt.firmware.state`.

Der Parameter `message` muss angegeben werden, wenn der Wert des Parameters `rc` nicht `200` lautet.

**Wichtig:** Geräte müssen Operationen zum Beobachten, Benachrichtigen und Abbrechen implementieren, um Anforderungen des Typs [Firmwareaktionen - Update](requests.html#firmware-actions-update) zu unterstützen.

### Topic für eine Anforderung des Typs 'Attributbeobachtung abbrechen'


Der Server publiziert eine Anforderung des Typs 'Attributbeobachtung abbrechen' im folgenden Topic:

```
iotdm-1/cancel
```


### Nachrichtenformat für eine Anforderung des Typs 'Attributbeobachtung abbrechen'


Anforderungsformat:

```
Eingehende Nachricht vom Server:

Topic: iotdm-1/cancel
{
    "d": {
        "fields": [
            "string"
        ]
    },
    "reqId": "string"
}
```

Antwortformat:

```
Ausgehende Nachricht vom Gerät:

Topic: iotdevice-1/response
{
    "rc": number,
    "message": "string",
    "reqId": "string"
}
```



## Anforderungen des Typs 'Über Attributänderungen benachrichtigen'
{: #observations-notify}

{{site.data.keyword.iot_short_notm}} kann für ein bestimmtes Attribut oder eine Gruppe von Werten eine Beobachtungsanforderung vornehmen, indem der Anforderungstyp 'Über Attributänderungen benachrichtigen' verwendet wird. Wenn der Wert des Attribut bzw. der Attribute geändert wird, muss das Gerät eine Benachrichtigung senden, die den zuletzt aktuellen Wert enthält.

Der Wert des Parameters `field_name` ist der Name des geänderten Attributs und der Feldwert (`field_value`) ist der aktuelle Wert des Attributs. Das Attribut kann ein komplexes Feld sein. Wenn als Ergebnis einer einzigen Operation mehrere Werte in einem komplexen Feld aktualisiert werden, wird nur eine einzige Benachrichtigungsnachricht gesendet.

Wenn die Benachrichtigungsanforderung erfolgreich verarbeitet wird, wird für den Parameter `rc` der Wert `200` eingestellt. Wenn die Anforderung nicht richtig ist, wird für den Parameter `rc` der Wert `400` eingestellt. Wenn der in der Benachrichtigungsanforderung angegebene Parameter nicht beobachtet wird, wird für den Parameter `rc` der Wert `404` eingestellt.

**Wichtig:** Geräte müssen Operationen zum Beobachten, Benachrichtigen und Abbrechen implementieren, um Anforderungen des Typs [Firmwareaktionen - Update](requests.html#firmware-actions-update) zu unterstützen.


### Topic für eine Anforderung des Typs 'Über Attributänderungen benachrichtigen'


Ein Gerät publiziert eine Anforderung des Typs 'Über Attributänderungen benachrichtigen' im folgenden Topic:

```
iotdevice-1/notify
```


### Nachrichtenformat für eine Anforderung des Typs 'Über Attributänderungen benachrichtigen'


Anforderungsformat:

```
Ausgehende Nachricht vom Gerät:

Topic: iotdevice-1/notify
{
    "d": {
        "field": "field_name",
        "value": "field_value"
    }
    "reqId": "string"
}
```

Antwortformat:

```
Eingehende Nachricht vom Server:

Topic: iotdm-1/response
{
    "rc": number,
    "reqId": "string"
}
```

### Antwortcodes für eine Anforderung des Typs 'Über Attributänderungen benachrichtigen'

|Antwortcode |Nachricht |
|:---|:---|
|200   |Die Operation war erfolgreich.|
|400   |Die Eingabenachricht stimmt nicht mit dem erwarteten Format überein oder einer der Werte liegt außerhalb des gültigen Bereichs.|
|404   |Der Topicname ist falsch, das Gerät ist nicht in der Datenbank vorhanden oder es gibt für das Feld keine berichtete Beobachtung.|
|409   |Bei der Gerätedatenbankaktualisierung trat ein Konflikt auf. Vereinfachen Sie, falls erforderlich, die Operation, um den Konflikt zu lösen.|
|500   |Es ist ein interner Fehler aufgetreten.|
