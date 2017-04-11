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


# Gerätemanagementanforderungen
{: #requests}


{{site.data.keyword.iot_full}} bietet Aktionen, die für ein oder mehrere Geräte initiiert werden können. Diese Aktionen können mithilfe des Dashboards oder mithilfe der REST-API initiiert werden. Zu den verfügbaren Aktionstypen gehören **Geräteaktionen** und **Firmwareaktionen**.

## Gerätemanagementanforderungen mithilfe des Dashboards initiieren
{: #initiating-dm-dashboard}

Anforderungen können über das Dashboard durch Verwenden der Registerkarte **Aktionen** auf der Seite 'Geräte' initiiert werden. Klicken Sie auf **Aktion initiieren**, um eine Aktion auszuwählen, um Geräte auszuwählen und um lle zusätzlichen Parameter anzugeben, die von der ausgewählten Aktion unterstützt werden.

## Gerätemanagementanforderungen mithilfe der REST-API initiieren
{: #initiating-dm-api}

Anforderungen können mithilfe des folgenden REST-API-Beispiels initiiert werden:  

`POST https://<Organisation>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

ere Informationen zum Hauptteil einer Gerätemanagementanforderung finden Sie in der [API-Dokumentation ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.

## Geräteaktionen
{: #device-actions}

Ein Gerät kann beim Publizieren einer Managementanforderung angeben, dass es Geräteaktionen unterstützt. Eine Geräteaktionsanforderung gibt für {{site.data.keyword.iot_short_notm}} an, dass das Gerät auf die Aktionen 'Geräteneustart' und 'Zurücksetzen des Geräts' antworten kann.


## Geräteaktionen - Neu starten
{: #device-actions-reboot}

Sie können die Aktion für den Geräteneustart mithilfe des {{site.data.keyword.iot_short_notm}}-Dashboards oder mithilfe der REST-API initiieren.

Zum Initiieren eines Geräteneustarts mithilfe der REST-API setzen Sie eine POST-Anforderung an die folgende Adresse ab:

`https://<Organisation>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Geben Sie folgende Informationen an:

- Die Aktion `device/reboot`.
- Eine Liste der Geräte, für die ein Neustart ausgeführt werden soll, mit maximal 5000 Geräten.

Beispielanforderung für einen Geräteneustart:

```
{
    "action": "device/reboot",
    "devices": [
        {
            "typeId": "someType",
            "deviceId": "someId"
        }
    ]
}
```

Nach dem Initiieren einer Anforderung wird an alle Geräte, die im Hauptteil der Anforderung für einen Neustart angegeben sind, eine MQTT-Nachricht publiziert. Von jedem Gerät muss eine Antwort zurückgesendet werden, um anzugeben, ob die Aktion für den Neustart initiiert werden kann. Wenn diese Operation sofort initiiert werden kann, legen Sie den Parameter `rc` auf `202` fest. Wenn der Versuch des Neustarts fehlschlägt, legen Sie für den Parameter `rc` den Wert `500` fest und stellen Sie den Parameter `message` entsprechend ein. Wenn ein Neustart (reboot) nicht unterstützt wird, legen Sie für den Parameter `rc` den Wert `501` fest und stellen Sie den Parameter `message` optional entsprechend ein.

Die Aktion für den Neustart ist abgeschlossen, wenn das Gerät nach dem erfolgten Neustart die Anforderung 'Gerät verwalten' sendet.

### Topic für die Anforderung für einen Geräteneustart

Der Server publiziert eine Anforderung für einen Geräteneustart im folgenden Abschnitt an ein Gerät:

```
iotdm-1/mgmt/initiate/device/reboot
```

### Nachrichtenformat für die Anforderung für einen Geräteneustart


Anforderungsformat:

```
Incoming message from the server:

Topic: iotdm-1/mgmt/initiate/device/reboot
{
    "reqId": "string"
}
```

Antwortformat:

```
Outgoing message from the device:

Topic: iotdevice-1/response
{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```

## Geräteaktionen - Zurücksetzen auf Werkseinstellungen
{: #device-actions-factory-reset}

Sie können die Aktion für das Zurücksetzen auf Werkseinstellungen mithilfe des {{site.data.keyword.iot_short_notm}}-Dashboards oder mithilfe der REST-API initiieren

Zum Initiieren des Zurücksetzens von Geräten auf Werkseinstellungen mithilfe der REST-API setzen Sie eine POST-Anforderung an folgende Adresse ab:

`https://<Organisation>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Folgende Informationen werden angegeben:

- Die Aktion `device/factoryReset`.
- Eine Liste der Geräte, die zurückgesetzt werden sollen, mit maximal 5000 Geräten.

Das folgende Beispiel zeigt eine Beispielanforderung für das Zurücksetzen von Geräten:

```
{
    "action": "device/factoryReset",
    "devices": [
        {
            "typeId": "someType",
            "deviceId": "someId"
        }
    ]
}
```

Nach dem Initiieren einer Anforderung für das Zurücksetzen von Geräten wird an alle Geräte, die im Hauptteil der Anforderung angegeben sind, eine MQTT-Nachricht publiziert. Von jedem Gerät muss eine Antwort zurückgegeben werden, um anzugeben, ob die Aktion zum Zurücksetzen auf Werkseinstellungen initiiert werden kann. Der Antwortcode wird auf `202` festgelegt, wenn diese Aktion sofort ausgeführt werden kann. Wenn der Versuch des Zurücksetzens auf Werkseinstellungen fehlschlägt, legen Sie für den Parameter `rc` den Wert `500` fest und stellen Sie den Parameter `message` entsprechend ein. Wenn die Aktion zum Zurücksetzen auf Werkseinstellungen nicht unterstützt ist, legen Sie für den Parameter `rc` den Wert `501` fest und stellen Sie den Parameter `message` optional entsprechend ein.

Die Aktion zum Zurücksetzen auf Werkseinstellungen ist abgeschlossen, wenn das Gerät nach dem Zurücksetzen auf Werkseinstellungen die Anforderung 'Gerät verwalten' sendet.

### Topic für die Anforderung zum Zurücksetzen auf Werkseinstellungen

Der Server publiziert folgende Anforderung an ein Gerät:

```
iotdm-1/mgmt/initiate/device/factory_reset
```


### öNachrichtenformat für die Anforderung zum Zurücksetzen auf Werkseinstellungen


Anforderungsformat:

```
Das folgende Topic zeigt die eingehene Nachricht vom Server:

Topic: iotdm-1/mgmt/initiate/device/factory_reset
{
    "reqId": "string"
}
```

Antwortformat:

```
Das folgende Topic zeigt eine ausgehende Nachricht vom Gerät:

Topic: iotdevice-1/response
{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```


## Firmwareaktionen
{: #firmware-actions}

Die Firmwareversion, die ein Gerät aktuell aufweist, ist im Attribut `deviceInfo.fwVersion` gespeichert. Die `mgmt.firmware`-Attribute werden zum Ausführen eines Firmware-Updates und zum Beobachten seines Status verwendet.

**Wichtig:** Das verwaltete Gerät muss die Beobachtung der `mgmt.firmware`-Attribute unterstützen, damit Firmwareaktionen unterstützt sind.

Der Prozess für das Firmware-Update ist in unterschiedliche Aktionen aufgeteilt:
- Herunterladen der Firmware
- Aktualisieren der Firmware

Der Status der einzelnen Firmwareaktionen wird in einem separaten Attribut auf dem Gerät gespeichert. Das Attribut `mgmt.firmware.state` beschreibt den Status des Herunterladens der Firmware. In der folgenden Tabelle werden die möglichen Werte beschrieben, die für das Attribut `mgmt.firmware.state` eingestellt werden können:

 |Wert |Status  | Bedeutung |
 |:---|:---|:---|
 |0  | Inaktiv        | Das Gerät lädt keine Firmware herunter. |  
 |1  | Download läuft | Das Gerät lädt Firmware herunter. |
 |2  | Heruntergeladen  | Das Firmware-Update wurde von dem Gerät erfolgreich heruntergeladen und kann jetzt installiert werden. |


Das Attribut `mgmt.firmware.updateStatus` beschreibt den Status des Firmware-Updates. Folgende Werte sind für das Attribut `mgmt.firmware.updateStatus` möglich:

|Wert |Status | Bedeutung |  
|:---|:---|:---|
|0 | Erfolg | Die Firmware wurde erfolgreich aktualisiert. |
|1 | In Bearbeitung | Das Firmware-Update wurde initiiert, ist aber noch nicht abgeschlossen.|
|2 | Speicherkapazität erschöpft | Während der Operation wurde eine abnormale Speicherbedingung festgestellt.|
|3 | Verbindung unterbrochen     | Die Verbindung wurde während des Herunterladens der Firmware unterbrochen. |
|4 | Überprüfung fehlgeschlagen | Die Überprüfung der Firmware ist fehlgeschlagen. |
|5 | Nicht unterstütztes Image   | Das heruntergeladene Firmware-Image wird von dem Gerät nicht unterstützt. |
|6 | Ungültiger URI         | Das Gerät konnte die Firmware von dem angegebenen URI nicht herunterladen. |

## Firmwareaktionen - Herunterladen
{: #firmware-actions-download}

Sie können die Aktion zum Herunterladen von Firmware mithilfe des {{site.data.keyword.iot_short_notm}}-Dashboards oder mithilfe der REST-API initiieren.

Zum Initiieren des Herunterladens von Firmware mithilfe der REST-API setzen Sie eine POST-Anforderung an die folgende Adresse ab:

`https://<Organisation>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Folgende Informationen werden angegeben:

- Die Aktion `firmware/download`
- Eine Liste der Geräte, die das Image erhalten sollen, mit maximal 5000 Geräten
- Die URI für das Firmware-Image (optional)
- Verifizierungszeichenfolge zum Überprüfen des Image (optional)
- Firmware-Name (optional)
- Firmwareversion (optional)

Das folgende Beispiel zeigt die Anforderung zum Herunterladen von Firmware, die die Basis für alle folgenden Beispielnachrichten ist:

```
{
   "action" : "firmware/download",
   "parameters" : [{
         "name" : "uri",
         "value" : "some uri for firmware location"
      }, {
         "name" : "name",
         "value" : "some firmware name"
      }, {
         "name" : "verifier",
         "value" : "some validation code"
      }, {
         "name" : "version",
         "value" : "some firmware version"
      }
   ],
   "devices" : [{
         "typeId" : "someType",
         "deviceId" : "someId"
      }
   ]
}
```

Wenn keine optionalen Parameter angegeben sind, wird der erste Schritt im folgenden Prozess übersprungen.

Der Gerätemanagementserver in {{site.data.keyword.iot_short_notm}} verwendet das Gerätemanagementprotokoll, um eine Anforderung an die Geräte zu senden, mit der der Download von Firmware initiiert wird. Der Prozess zum Herunterladen besteht aus den folgenden Schritten:

1. An das Topic `iotdm-1/device/update` wird eine Anforderung zum Aktualisieren von Firmwaredetails gesendet.
Die Aktualisierungsanforderung veranlasst das Gerät zu prüfen, ob sich die angeforderte Firmware von der aktuell installierten Firmware unterscheidet. Falls ein Unterschied besteht, müssen Sie den Parameter `rc` auf den Wert `204` festlegen, wodurch der Status in 'Geändert' (`Changed`) umgesetzt wird.  
Das folgende Beispiel zeigt, welche Nachricht für die zuvor gesendete Beispielanforderung zum Herunterladen von Firmware zu erwarten ist und welche Antwort gesendet wird, wenn ein Unterschied festgestellt wird:
```
   Incoming request from the {{site.data.keyword.iot_short_notm}}:

   Topic: iotdm-1/device/update
   Message:
   {
      "reqId" : "f38faafc-53de-47a8-a940-e697552c3194",
      "d" : {
         "fields" : [{
               "field" : "mgmt.firmware",
               "value" : {
                  "version" : "some firmware version",
                  "name" : "some firmware name",
                  "uri" : "some uri for firmware location",
                  "verifier" : "some validation code",
                  "state" : 0,
                  "updateStatus" : 0,
                  "updatedDateTime" : ""
               }
            }
         ]
      }
   }

   Outgoing response from device:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 204,
      "reqId" : "f38faafc-53de-47a8-a940-e697552c3194"
   }
   ```
   Diese Antwort löst die nächste Anforderung aus.
2. Die Beobachtungsanforderung `iotdm-1/observe` für den Downloadstatus der Firmware wird gesendet.
Die Beobachtungsanforderung prüft, ob das Gerät zum Starten des Firmware-Downloads bereit ist. Wenn der Download sofort gestartet werden kann, legen Sie für den Parameter `rc` den Wert `200` (`Ok`), für das Attribut `mgmt.firmware.state` die Einstellung `0` (`Idle`) und für das Attribut `mgmt.firmware.updateStatus` die Einstellung `0` (`Idle`) fest. Der folgende Code zeigt eine Beispielkommunikation zwischen {{site.data.keyword.iot_short_notm}} und einem Gerät:
   ```
   Incoming request from the {{site.data.keyword.iot_short_notm}}:

   Topic: iotdm-1/observe
   Message:
   {
      "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
      "d" : {
         "fields" : [ {
            "field" : "mgmt.firmware"
            }
         ]
      }
   }

   Outgoing response from device:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 200,
      "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8"
   }
   ```
Dieser Austausch löst den letzten Schritt aus.  

3. Die Anforderung zum Herunterladen wird im Topic `iotdm-1/mgmt/initiate/firmware/download` gesendet:

   Die Anforderung zum Herunterladen weist ein Gerät an, den Download der Firmware zu starten. Wenn die Aktion sofort initiiert werden kann, legen Sie für den Parameter `rc` den Wert `202` fest. Der folgende Code zeigt ein Beispiel für die Initiierung einer Downloadanforderung:

   ```
   Incoming request from the {{site.data.keyword.iot_short_notm}}:

   Topic: iotdm-1/mgmt/initiate/firmware/download
   Message:
   {
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }

   Outgoing response from device:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 202,
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }
   ```

Nachdem ein Firmware-Download auf diese Weise initiiert wurde, muss das Gerät den Status des Downloads an {{site.data.keyword.iot_short_notm}} berichten. Das Gerät berichtet den Status, indem es eine Nachricht im Topic `iotdevice-1/notify` publiziert, wobei für das Attribut `mgmt.firmware.state` entweder `1` (`Downloading` - Download läuft) oder `2` (`Downloaded` - Heruntergeladen) festgelegt wird.
An den folgenden Beispielen sehen Sie die Initiierung des Downloads von Firmware:

```
Outgoing message from device:

Topic: iotdevice-1/notify
Message:
{
   "reqId" : "123456789",
   "d" : {
      "fields" : [ {
         "field" : "mgmt.firmware",
         "value" : {
                 "state" : 1
             }
      } ]
   }
}


Wait some time...


Outgoing message from device:

Topic: iotdevice-1/notify
Message:
{
   "reqId" : "1234567890",
   "d" : {
      "fields" : [ {
         "field" : "mgmt.firmware",
         "value" : {
                 "state" : 2
             }
      } ]
   }
}
```



Nachdem die Benachrichtigung publiziert wurde, wobei für das Attribut `mgmt.firmware.state` die Einstellung `2` festgelegt war, wird im Topic `iotdm-1/cancel` eine Anforderung ausgelöst. Mit dieser Anforderung wird die Beobachtung des Attributs `mgmt.firmware` abgebrochen.
Nachdem eine Antwort gesendet wurde, bei der der Parameter `rc` auf `200` eingestellt war, ist der Download der Firmware abgeschlossen. Der folgende Code zeigt ein Beispiel:

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/cancel
Message:
{
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f",
   "d" : {
      "fields" : [{
            "field" : "mgmt.firmware"
         }
      ]
   }
}


Outgoing message from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

Folgende Informationen sind bei der Fehlerbehandlung nützlich:

- Wenn für das Attribut `mgmt.firmware.state` nicht die Einstellung `0` ('Idle' - 'Inaktiv') festgelegt ist, senden Sie einen Fehler, der den Antwortcode `400` und einen optionalen Nachrichtentext aufweist.
- Wenn das Attribut `mgmt.firmware.uri` nicht festgelegt ist oder kein gültiger URI ist, legen Sie für den Parameter `rc` die Einstellung `400` fest.
- Wenn der Versuch, die Firmware herunterzuladen, fehlschlägt, legen Sie für den Parameter `rc` den Wert `500` fest und stellen Sie den Parameter `message` entsprechend ein.
- Wenn der Download von Firmware nicht unterstützt wird, legen Sie für den Parameter `rc` den Wert `500` fest und stellen Sie den Parameter `message` entsprechend ein.
- Wenn vom Gerät eine Anforderung zum Ausführen empfangen wird, ändern Sie für das Attribut `mgmt.firmware.state` die Einstellung von `0` (Idle - Inaktiv) in `1` (Downloading - Download läuft).
- Wenn der Download erfolgreich abgeschlossen ist, legen Sie für das Attribut `mgmt.firmware.state` die Einstellung `2` (Downloaded - Heruntergeladen).
- Wenn während des Herunterladens ein Fehler auftritt, legen Sie für das Attribut `mgmt.firmware.state` die Einstellung `0` (Idle - Inaktiv) und für das Attribut `mgmt.firmware.updateStatus` einen der folgenden Werte für den Fehlerstatus fest:
  - 2 (Speicherkapazität erschöpft)
  - 3 (Verbindung unterbrochen)
  - 6 (Ungültiger URI)
- Wenn eine Firmware-Verifizierung festgelegt wurde, versucht das Gerät, das Firmware-Image zu verifizieren. Wenn die Verifizierung des Image fehlschlägt, legen Sie für das Attribut `mgmt.firmware.state` die Einstellung `0` (Inaktiv) und für das Attribut `mgmt.firmware.updateStatus` den Fehlerstatuswert `4` (Überprüfung fehlgeschlagen) fest.

## Firmwareaktionen - Update
{: #firmware-actions-update}

Die Installation der heruntergeladenen Firmware wird mithilfe der REST-API durch Absetzen einer POST-Anforderung an die folgende Adresse initiiert:

`https://<Organisation>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Folgende Informationen werden angegeben:

- Die Aktion `firmware/update`
- Eine Liste der Geräte, die das Image erhalten sollen und die alle denselben Gerätetyp aufweisen müssen.
- Die URI für das Firmware-Image (optional)
- Verifizierungszeichenfolge zum Überprüfen des Image (optional)
- Firmware-Name (optional)
- Firmwareversion (optional)

Der folgende Code ist eine Beispielanforderung:

```
   {
      "action" : "firmware/update",
      "devices" : [{
            "typeId" : "someType",
            "deviceId" : "someId"
         }
      ]
   }

```

Ist ein optionaler Parameter angegeben, ist die erste Nachricht, die vom Gerät empfangen wird, eine Anforderung des Typs 'Geräteattribute aktualisieren'. Diese Anforderung entspricht der ersten Nachricht bei einer Anforderung zum Herunterladen von Firmware.

Zum Überwachen des Status des Firmware-Updates löst {{site.data.keyword.iot_short_notm}} zunächst eine Beobachtungsanforderung im Topic `iotdm-1/observe` aus. Wenn das Gerät für den Start des Aktualisierungsprozesses bereit ist, sendet es eine Antwort, bei der für den Parameter `rc` der Wert `200`, für das Attribut `mgmt.firmware.state` die Einstellung `0` und für das Attribut `mgmt.firmware.updateStatus` die Einstellung `0` festgelegt ist.

Der folgende Code zeigt ein Beispiel:

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/observe
Message:
{
   "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
   "d" : {
      "fields" : [
         {
            "field": "mgmt.firmware"
         }
      ]
   }
}

Outgoing response from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
   "d" : {
      "fields" : [{
            "field" : "mgmt.firmware",
            "value" : {
               "state" : 0,
               "updateStatus" : 0
            }
         }
      ]
   }
}
```



Nach dem erfolgreichen Herunterladen des Firmware-Updates verwendet der Gerätemanagementserver in {{site.data.keyword.iot_short_notm}} das Gerätemanagementprotokoll, um anzufordern, dass die angegebenen Geräte die Firmwareinstallation mithilfe des Topics `iotdm-1/mgmt/initiate/firmware/update` auslösen.
Wenn diese Operation sofort initiiert werden kann, legen Sie den Parameter `rc` auf `202` fest.
Wenn die Firmware zuvor nicht erfolgreich heruntergeladen wurde, legen Sie für den Parameter `rc` den Wert `400` fest.

Der folgende Code zeigt ein Beispiel:

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/mgmt/initiate/firmware/update
Message:
{
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}

Outgoing response from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 202,
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}
```

Zum Abschließen der Anforderung zum Aktualisieren von Firmware berichtet das Gerät seinen Aktualisierungsstatus mithilfe einer Statusnachricht, die im zugehörigen Topic `iotdevice-1/notify` publiziert wird, an {{site.data.keyword.iot_short_notm}}.
Wenn ein Firmware-Update abgeschlossen wird, wird das Attribut `mgmt.firmware.updateStatus` auf die Einstellung `0` (Erfolg) gesetzt und für das Attribut `mgmt.firmware.state` wird die Einstellung `0` (Inaktiv) festgelegt. Das heruntergeladene Firmware-Image kann anschließend im Gerät gelöscht werden und für das Attribut `deviceInfo.fwVersion` wird der Wert des Attributs `mgmt.firmware.version` festgelegt.

Der folgende Code zeigt ein Beispiel einer Hinweisnachricht:

```
Outgoing message from device:

Topic: iotdevice-1/notify
Message:
{
   "d" : {
      "fields": [
         {
            "field" : "mgmt.firmware",
            "value" : {
               "state" : 0,
               "updateStatus" : 0
            }
         }
      ]
   }
}
```

Wenn {{site.data.keyword.iot_short_notm}} eine Benachrichtigung über ein abgeschlossenes Firmware-Update empfängt, wird im Topic `iotdm-1/cancel` eine letzte Anforderung zum Abbrechen der Beobachtung des Attributs `mgmt.firmware` ausgelöst.


Bei Senden einer Antwort, bei der für den Parameter `rc` der Wert `200` festgelegt wurde, wird die Anforderung zum Aktualisieren der Firmware abgeschlossen, wie im folgenden Beispiel gezeigt:

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/cancel
Message:
{
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f",
   "d" : {
      "fields" : [
         {
            "field" : "mgmt.firmware"
         }
      ]
   }
}


Outgoing message from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

Die folgende Liste bietet einige nützliche Informationen zur Fehler- und Prozessbehandlung:

- Wenn der Versuch, die Firmware zu aktualisieren, fehlschlägt, legen Sie für den Parameter `rc` den Wert `500` fest und stellen Sie optional den Parameter `message` ein, der relevante Informationen enthalten kann.
- Wenn das Firmware-Update nicht unterstützt ist, legen Sie für den Parameter `rc` den Wert `501` fest und stellen Sie optional den Parameter `message` ein, der relevante Informationen enthalten kann.
- Wenn für das Attribut `mgmt.firmware.state` nicht die Einstellung `2` (Heruntergeladen) festgelegt ist, senden Sie einen Fehler, bei dem der Parameter `rc` auf den Wert `400` festgelegt ist, sowie einen optionalen Nachrichtentext.
- Legen Sie andernfalls für das Attribut `mgmt.firmware.updateStatus` die Einstellung `1` (In Bearbeitung) fest und die Firmwareinstallation wird in der Regel gestartet.
- Wenn die Installation der Firmware fehlschlägt, legen Sie für das Attribut `mgmt.firmware.updateStatus` einen der folgenden Werte fest:
  - `2` (Speicherkapazität erschöpft)
  - `5` (Nicht unterstütztes Image)


**Wichtig:** Alle Parameter, die als Bestandteil des Attributs `mgmt.firmware` aufgelistet sind, müssen gleichzeitig festgelegt werden, damit nur eine einzige Hinweisnachricht gesendet wird, falls eine aktuelle Beobachtung für `mgmt.firmware` besteht.

## Anleitungen zu Geräteaktionen und Firmwareaktionen

Die folgenden Anleitungen beschreiben den vollständigen erforderlichen Ablauf zum Ausführen von Geräte- und Firmwareaktionen.

- [Gerätemanagement in WIoT Platform – Rollback & Zurücksetzen auf Werkseinstellungen ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/){: new_window}

- [Vom Gerät eingeleitetes Firmware-Update ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-device-initiated-firmware-upgrade/){: new_window}

- [Von der Plattform eingeleitetes Firmware-Update ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/){: new_window}

- [Von der Plattform eingeleitetes Firmware-Update zur Ausführung im Hintergrund ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/){: new_window}

- [Firmware-Rollback & Zurücksetzen auf Werkseinstellungen ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/){: new_window}
