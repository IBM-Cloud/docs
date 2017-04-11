---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Gerätemodell
{: #device_model}

Im Gerätemodell werden die Metadaten und die Managementmerkmale eines Geräts beschrieben. Die Gerätedatenbank in {{site.data.keyword.iot_full}} ist die Masterquelle für Geräteinformationen. Anwendungen und verwaltete Geräte können Aktualisierungen einschließlich Positionsänderungen oder den Fortschritt eines Firmware-Updates an die Datenbank des Geräts senden. Sobald diese Aktualisierungen von {{site.data.keyword.iot_short_notm}} empfangen werden, wird die Datenbank aktualisiert und die Informationen werden Anwendungen zur Verfügung gestellt.

**Hinweis:** Mit Ausnahme der [Gerätemanagementerweiterung](#devicemanagementextension) steht das gesamte Gerätemodell sowohl verwalteten als auch nicht verwalteten Geräten zur Verfügung. Ein nicht verwaltetes Gerät kann jedoch sein zugehöriges Gerätemodell nicht direkt in der Datenbank aktualisieren.

## Geräteidentifikation
{: #device_id}

Jedes Gerät hat die Attribute `typeId` (Typ-ID) und `deviceId` (Geräte-ID). In der Regel stellt die `typeId` das Modell Ihres Geräts dar, während `deviceId` dessen Seriennummer darstellen kann. Die Kombination aus `typeId` und `deviceId` muss in Ihrer {{site.data.keyword.iot_short_notm}}-Organisation für jedes Gerät eindeutig sein.

Zusätzlich zu diesen Attributen erstellt {{site.data.keyword.iot_short_notm}} für jedes Gerät eine weitere ID. Diese ID wird `clientId` genannt. Die `clientId` basiert auf Ihrer `organizationId` (Organisations-ID) und auf den Werten für `typeId` (Typ-ID) und `deviceId` (Geräte-ID) des Geräts. Die `clientId` bietet die Möglichkeit, ein einzelnes Gerät eindeutig zu identifizieren. Die in diesen Kennungen verwendete Zeichen sind eingeschränkt, sodass die Kennungen mit Kommunikationsprotokollen und REST-APIs kompatibel sind.

Auch folgende optionale Geräte-IDs können verwendet werden:

- deviceInfo.manufacturer
- deviceInfo.serialNumber
- deviceInfo.model
- deviceInfo.deviceClass
- deviceInfo.description

Weitere Informationen zu den Kennungen sowie Beschreibungen vergleichbarer Kennungen in anderen Gerätemanagementstandards finden Sie in [Attribute](#attributes).


## IDs und Typen von Geräten
{: #id_and_device_types}

Jedem mit {{site.data.keyword.iot_short_notm}} verbundenen Gerät ist ein Gerätetyp zugeordnet. Gerätetypen sind Gruppen von Geräten, die gemeinsame Merkmale haben oder gleiches Verhalten zeigen.

Ein Gerätetyp hat eine Gruppe von Attributen. Wenn ein Gerät zu {{site.data.keyword.iot_short_notm}} hinzugefügt wird, werden die Attribute im zugehörigen Gerätetyp als Vorlage verwendet. Wenn das Gerät einen Wert hat, wird dieser Wert verwendet. Wenn das Gerät keinen Wert hat, wird der für den Gerätetyp angegebene Wert verwendet. Beispielsweise könnte der Gerätetyp einen Wert für das Attribut `deviceInfo.fwVersion` aufweisen, das die Firmware-Version zum Zeitpunkt der Herstellung widerspiegelt. Dieser Wert wird beim Hinzufügen der Geräte vom Gerätetyp in die Geräte kopiert. Wenn ein Gerät hinzugefügt wird und der Wert `deviceInfo.fwVersion` bereits vorhanden ist, wird er nicht überschrieben.

Beim Aktualisieren eines Attributs für einen Gerätetyp übernehmen nur neue zu registrierende Geräte die Änderungen, die an der Gerätetypschablone vorgenommen wurden.

## Attribute
{: #attributes}

In der folgenden Tabelle wird die Liste der Attribute angezeigt, die auf Geräte in {{site.data.keyword.iot_short_notm}} angewendet werden können. In Kursivdruck angezeigte Attribute können auch für Gerätetypen gelten.

Schlüssel:
  - API: Kann mithilfe von APIs aktualisiert werden
  - DMA: Kann vom Gerätemanagementagenten aktualisiert werden
  - R: Schreibgeschützt
  - W: Schreiben und Lesen
  - A: Anhängen

Attribut                        | Typ       | Beschreibung                                       | API | DMA   
------------- | ------------- | ------------- | ------------- | -------------  |
 clientId                         | Zeichenfolge     | Die mit MQTT-Verbindungen verwendete Client-ID          |  R  |   -  
 *typeId*                         | Zeichenfolge     | Gerätetyp                                       |  R  |   -  
 deviceId                         | Zeichenfolge     | Geräte-ID                                         |  R  |    -
 classId                          | Zeichenfolge     | Geräteklasse ("Gerät" oder "Gateway")           |  R  |   -  
 gatewayTypeId                    | Zeichenfolge     | Typ-ID des Gateways, das von diesem Gerät verwendet wird       |  R  |    -
 gatewayId                        | Zeichenfolge     | Geräte-ID des Gateways, das von diesem Gerät verwendet wird     |  R  |   -  
 status.alert                     | Boolescher Wert    | Gibt an, ob das Gerät einen Alert hat                   |  W  |  -   
 *deviceInfo.serialNumber*        | Zeichenfolge     | Die Seriennummer des Geräts                   |  W  |  W    
 *deviceInfo.manufacturer*        | Zeichenfolge     | Der Hersteller des Geräts                    |  W  |  W   
 *deviceInfo.model*               | Zeichenfolge     | Das Modell des Geräts                           |  W  |  W  
 *deviceInfo.deviceClass*         | Zeichenfolge     | Die Klasse des Geräts                           |  W  |  W  
 *deviceInfo.description*         | Zeichenfolge     | Der beschreibende Name des Geräts                |  W  |  W  
 *deviceInfo.fwVersion*           | Zeichenfolge     | Die Firmwareversion, die das Gerät aktuell aufweist    |  W  |  W  
 *deviceInfo.hwVersion*           | Zeichenfolge     | Die Hardwareversion des Geräts                |  W  |  W  
 *deviceInfo.descriptiveLocation* | Zeichenfolge     | Die beschreibende Position, wie beispielsweise ein Raum, eine Gebäudenummer oder eine geografische Region      |  W  |  W  
 *metadata*                       | komplex    | Unformatierte Metadaten                                |  W  |  W  
 added.auth.id                    | Zeichenfolge     | Die ID, mit der das Gerät hinzugefügt wurde                          |  R  |   -  
 added.dateTime                   | Zeichenfolge     | ISO8601 date-time: Datum und Zeit des Zeitpunkts, an dem das Gerät hinzugefügt wurde |  R  |    -
 refs.diag.errorCodes             | Zeichenfolge     | URI der Diagnoseerweiterung für Fehlercodes, falls vorhanden |  R  |   -  
 refs.diag.logs                   | Zeichenfolge     | URI der Diagnoseerweiterung für Protokolle, falls vorhanden        |  R  |   -  
 refs.location                    | Zeichenfolge     | URI der Positionserweiterung, falls vorhanden             |  R  |   -  
 refs.mgmt                        | Zeichenfolge     | URI der Gerätemanagementerweiterung, falls vorhanden                 |  R  |    -



## Erweiterte Attribute
{: #extended_attributes}

Zusätzlich zu den oben im Abschnitt 'Attribute' aufgeführten Kernattributen gibt es zusätzliche Attribute, die als Erweiterungen des Basisgerätemodells behandelt werden. Einfache Abfragen zu den Geräterückgabeinformationen vom Basisgerätemodell, aber keine Erweiterungen. Informationen von Erweiterungen müssen ausdrücklich angefordert werden.


Erweiterungsname    | Präfix der Attribute | Verwendungszweck      
------------- | ------------- | -------------                                         
 Diagnose       | diag                 | Fehlerprotokolle und Diagnoseinformationen                 
 Position          | location             | Position des Geräts, wird möglicherweise regelmäßig aktualisiert
Gerätemanagement | mgmt                 | Gerätemanagementaktionen, wie zum Beispiel 'Firmware-Update'       


### Diagnoseerweiterung


Die Diagnoseattribute sind optional und nur für Geräte verfügbar, die Fehlerprotokollinformationen haben. Diese Attribute sind für die Diagnose von Geräteproblemen konzipiert und nicht für die Behebung von Fehlern im Zusammenhang mit der Verbindung zu {{site.data.keyword.iot_short_notm}}. Der Umfang der in Diagnoseattributen gespeicherten Informationen kann sehr groß sein und muss daher in besonderer Weise abgefragt werden.

Diagnoseprotokollinformationen werden als eine Reihe von Einträgen gespeichert. Jeder Eintrag besteht aus einer Nachricht, einer Angabe zum Schweregrad, einer Zeitmarke und optional Daten in Bytefeldgruppen. Sie können Einträge mithilfe einer API anhängen. Das Anhängen von Einträgen kann jedoch dazu führen, dass ältere Einträge verloren gehen, damit die Diagnoseprotokolle eine praktikable Größe beibehalten.


Attribut            | Typ       | Beschreibung                                                 | API | DMA
------------- | ------------- | ------------- | ------------- | -------------
 diag.errorCodes[]    | Feldgruppe aus </br> ganzen Zahlen  | Feldgruppe aus Fehlercodes                                        |  A  |  A  
 diag.log[]           | Feldgruppe      | Feldgruppe aus Diagnosedaten                                    |  A  |  A  
 diag.log[].message   | Zeichenfolge     | Diagnosenachricht                                          |  -   |    -
 diag.log[].timestamp | Zeichenfolge     | ISO8601 date-time: Datum und Zeit des Protokolleintrags               |  -   |    -
 diag.log[].logData   | Zeichenfolge     | byte: Diagnosedaten, base-64-codiert                      |  -   |    -
 diag.log[].severity  | Zahl     | Schweregrad der Nachricht, 0: Informationsnachricht, 1: Warnung, 2: Fehler |  -   |    -


### Positionserweiterung

Die Positionsattribute sind optional und nur für Geräte verfügbar, die Positionsinformationen haben. Die Positionsinformationen werden separat gespeichert, um die Verwendung von Speicherverfahren zu ermöglichen, die für dynamische Informationen besser geeignet sind. Dies kann wichtig sein, wenn Informationen häufig aktualisiert werden, beispielsweise wie das bei einem mobilen Gerät der Fall ist.

Bei Lösungen, für die häufige Positionsaktualisierungen im Vordergrund stehen, wird erwartet, dass die Position als Teil der Ereignisnutzdaten des Geräts behandelt wird, wodurch höhere Aktualisierungsraten, ein einfacheres Speichern von archivierten Daten und eine einfachere Datenanalyse möglich sind.


Attribut                 | Typ   | Beschreibung                                             | API | DMA
------------- | ------------- | ------------- | ------------- | -------------
 location.longitude        | Zahl | Längengrad in Dezimalgrad unter Verwendung von WGS84                |  W  |  W  
 location.latitude         | Zahl | Breitengrad in Dezimalgrad unter Verwendung von WGS84                 |  W  |  W  
 location.elevation        | Zahl | Erhebung in Meter unter Verwendung von WGS84                         |  W  |  W  
 location.measuredDateTime | Zeichenfolge |ISO8601 date-time: Datum und Zeit der Positionsmessung |  W  |  W  
 location.updatedDateTime  | Zeichenfolge | ISO8601 date-time: Datum und Zeit                        |  R  |   
 location.accuracy         | Zahl | Genauigkeit der Position in Meter                      |  W  |  W  


### Gerätemanagementerweiterung
{: #devicemanagementextension}

Managementattribute stehen nur für verwaltete Geräte zur Verfügung. Wenn ein verwaltetes Gerät zu einem ruhenden Gerät wird, wird es zu einem nicht verwalteten Gerät und die Attribute des Typs `mgmt.` werden gelöscht. Die Attribute des Typs `mgmt.` werden von {{site.data.keyword.iot_short_notm}} als Ergebnis der Verarbeitung von Gerätemanagementanforderungen festgelegt. Diese Attribute können mithilfe der API nicht direkt geschrieben werden.

Geräte haben einen Lebenszyklus im Management, der durch ihren Status als verwaltete Geräte definiert ist. Der Gerätemanagementagent eines Geräts ist dafür zuständig, die Anforderung 'Gerät verwalten' mithilfe des Gerätemanagementprotokolls zu senden. Zur Handhabung von nicht mehr vorhandenen Geräten in einer Umgebung mit einer großen Anzahl von Geräten kann ein verwaltetes Gerät so eingerichtet werden, dass es regelmäßig die Anforderung 'Gerät verwalten' sendet. Ein verwaltetes Gerät wird zu einem ruhenden Gerät, wenn diese Anforderung innerhalb eines angegebenen Zeitraums nicht an {{site.data.keyword.iot_short_notm}} gesendet wird. Zum Vereinfachen dieser Funktionalität hat die Anforderung 'Gerät verwalten' einen optionalen Parameter für den Lebenszyklus. Wenn {{site.data.keyword.iot_short_notm}} die Anforderung 'Gerät verwalten' empfängt, für die der Parameter für den Lebenszyklus festgelegt ist, wird der Zeitpunkt berechnet, vor dem eine weitere Anforderung 'Gerät verwalten' erforderlich ist, und im Attribut `mgmt.dormantDateTime` gespeichert.


Attribut                     | Typ    | Beschreibung                             | API | DMA
------------- | ------------- | ------------- | ------------- | -------------
 mgmt.dormant                   | Boolescher Wert | Gibt an, ob das Gerät zu einem ruhenden Gerät wurde                  |  R  |  -
 mgmt.dormantDateTime           | Zeichenfolge  | ISO8601 date-time: Datum und Zeit des Zeitpunkts, an dem das Gerät zu einem ruhenden Gerät wird   |  R  |  -   
 mgmt.lastActivityDateTime      | Zeichenfolge  | ISO8601 date-time: Datum und Zeit der letzten Aktivität, wird regelmäßig aktualisiert    |  R  |    -
 mgmt.supports.deviceActions    | Boolescher Wert | Gibt an, ob von dem Gerät die Aktionen für Neustart und das Zurücksetzen auf Werkseinstellungen unterstützt werden  |  R  |   -  
 mgmt.supports.firmwareActions  | Boolescher Wert | Gibt an, ob von dem Gerät die Aktionen für Firmware-Download und Firmware-Update unterstützt werden    |  R  |     -
 mgmt.firmware.version          | Zeichenfolge  | Die Version der Firmware auf dem Geräts              |  R  |  W  
 mgmt.firmware.name             | Zeichenfolge  | Der Name der Firmware, die auf dem Gerät verwendet wird      |  R  |  W  
 mgmt.firmware.uri              | Zeichenfolge  | Die URI, von der das Firmware-Image heruntergeladen werden kann |  R  |  W  
 mgmt.firmware.verifier         | Zeichenfolge  | Die Verifizierungszeichenfolge (zum Beispiel eine Kontrollsumme) für das Firmware-Image, die zum Überprüfen der Integrität verwendet wird |  R  |  W  
 mgmt.firmware.state            | Zahl  | Gibt den Status des Firmware-Downloads an               |  R  |  W  
 mgmt.firmware.updateStatus     | Zahl  | Gibt den Status der Aktualisierung an                     |  R  |  W  
 mgmt.firmware.updatedDateTime  | Zeichenfolge  | ISO8601 date-time: Datum und Zeit der letzten Aktualisierung                 |  R  |    -
