---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Gerätemodell 
{: #device_model}
Letzte Aktualisierung: 13. September 2016 {: .last-updated}

Im Gerätemodell werden die Metadaten und die Managementmerkmale eines Geräts beschrieben. Die Gerätedatenbank in {{site.data.keyword.iot_full}} ist die Masterquelle für Geräteinformationen.
Anwendungen und verwaltete Geräte können Aktualisierungen einschließlich Positionsänderungen oder den Fortschritt eines Firmware-Updates an die Datenbank senden. Sobald diese Aktualisierungen von {{site.data.keyword.iot_short_notm}} empfangen werden, wird die Gerätedatenbank aktualisiert und die Informationen stehen Anwendungen zur Verfügung. 

**Hinweis:** Mit Ausnahme der Managementerweiterung steht das gesamte Gerätemodell sowohl verwalteten als auch nicht verwalteten Geräten zur Verfügung. Ein nicht verwaltetes Gerät kann jedoch sein zugehöriges Gerätemodell nicht direkt in der Datenbank aktualisieren. 

## Geräteidentifikation 
{: #device_id}

Jedes Gerät hat die Attribute `typeId` (Typ-ID) und `deviceId` (Geräte-ID). In der Regel stellt die `typeId` das Modell Ihres Geräts dar, während `deviceId` dessen Seriennummer darstellen kann. Die Kombination aus `typeId` und `deviceId` muss für Ihre {{site.data.keyword.iot_short_notm}}-Organisation für jedes Gerät eindeutig sein. 

Zusätzlich erstellt {{site.data.keyword.iot_short_notm}} für jedes Gerät eine weitere ID, die `clientId` (Client-ID) genannt wird. Die `clientId` basiert auf Ihrer `organizationId` (Organisations-ID) sowie auf den Werten für `typeId` und `deviceId` des Geräts und bietet die Möglichkeit, ein einzelnes Gerät eindeutig zu identifizieren. 

Die in diesen Kennungen verwendete Zeichen sind eingeschränkt, sodass die Kennungen mit Kommunikationsprotokollen und REST-APIs kompatibel sind. Auch folgende optionale Gerätekennungen werden zusammen mit dem Gerätemanagementprotokoll verwendet:


- deviceInfo.manufacturer
- deviceInfo.serialNumber
- deviceInfo.model
- deviceInfo.deviceClass
- deviceInfo.description

Weitere Informationen zu den Kennungen sowie Beschreibungen vergleichbarer Kennungen in anderen Gerätemanagementstandards finden Sie in [Attribute](#attributes). 


## IDs und Typen von Geräten 
{: #id_and_device_types}

Jedem mit {{site.data.keyword.iot_short_notm}} verbundenen Gerät ist ein Gerätetyp zugeordnet. Gerätetypen sind Gruppen von Geräten, die gemeinsame Merkmale oder gleiches Verhalten haben. 

Ein Gerätetyp hat eine Gruppe von Attributen. Wenn ein Gerät zu {{site.data.keyword.iot_short_notm}} hinzugefügt wird, werden die Attribute im zugehörigen Gerätetyp als Vorlage verwendet, die von gerätespezifischen Attributen überschrieben werden. Beispielsweise könnte der Gerätetyp einen Wert für das Attribut `deviceInfo.fwVersion` aufweisen, das die Firmware-Version zum Zeitpunkt der Herstellung widerspiegelt; dieser Wert würde beim Hinzufügen eines Geräts aus den Informationen zum Gerätetyp in das betreffende Gerät kopiert. Wenn ein Gerät hinzugefügt wird und der Wert `deviceInfo.fwVersion` bereits vorhanden ist, wird er durch den Gerätetyp nicht überschrieben. 

Beim Aktualisieren eines Gerätetyps übernehmen nur neue zu registrierende Geräte Änderungen an der Gerätetypschablone. Vorhandene Geräte eines Gerätetyps sind nicht betroffen und bleiben ohne Änderung.


## Attribute 
{: #attributes}

In der folgenden Tabelle wird die Liste der Attribute angezeigt, die auf Geräte in {{site.data.keyword.iot_short_notm}} angewendet werden können. Darüber hinaus können in Kursivdruck angezeigte Attribute auch auf Gerätetypen angewendet werden. 

- API/DMA: Kann von der API bzw. dem Gerätemanagementagenten aktualisiert werden 

  - R: Schreibgeschützt 
  - W: Schreiben und Lesen 
  - A: Anhängen 

Attribut                         | Typ        | Beschreibung                                        | API  | DMA    
------------- | ------------- | ------------- | ------------- | -------------  
 clientId                         | Zeichenfolge      | Die mit MQTT-Verbindungen verwendete Client-ID           |  R  |     
 *typeId*                         | Zeichenfolge      | Gerätetyp                                        |  R  |     
 deviceId                         | Zeichenfolge      | Geräte-ID                                          |  R  |     
 classId                          | Zeichenfolge      | Geräteklasse ("Gerät" oder "Gateway")            |  R  |     
 gatewayTypeId                    | Zeichenfolge      | Typ-ID des Gateways, das von diesem Gerät verwendet wird        |  R  |     
 gatewayId                        | Zeichenfolge      | Geräte-ID des Gateways, das dieses Gerät verwendet      |  R  |     
 status.alert                     | Boolescher Wert     | Ob das Gerät einen Alert hat                    |  W  |     
 *deviceInfo.serialNumber*        | Zeichenfolge      | Die Seriennummer des Geräts                    |  W  |  W    
 *deviceInfo.manufacturer*        | Zeichenfolge      | Der Hersteller des Geräts                     |  W  |  W   
 *deviceInfo.model*               | Zeichenfolge      | Das Modell des Geräts                            |  W  |  W  
 *deviceInfo.deviceClass*         | Zeichenfolge      | Die Klasse des Geräts                            |  W  |  W  
 *deviceInfo.description*         | Zeichenfolge      | Der beschreibende Name des Geräts                 |  W  |  W  
 *deviceInfo.fwVersion*           | Zeichenfolge      | Die Firmware-Version, die das Gerät aktuell aufweist     |  W  |  W  
 *deviceInfo.hwVersion*           | Zeichenfolge      | Die Hardwareversion des Geräts                 |  W  |  W  
 *deviceInfo.descriptiveLocation* | Zeichenfolge      | Die beschreibende Position, wie beispielsweise ein Raum, eine Gebäudenummer oder eine geografische Region       |  W  |  W  
 *metadata*                       | komplex     | Unformatierte Metadaten                                 |  W  |  W  
 added.auth.id                    | Zeichenfolge      | ID, mit der das Gerät hinzugefügt wurde                           |  R  |     
 added.dateTime                   | Zeichenfolge      | ISO8601 date-time: Datum und Zeit des Zeitpunkts, an dem das Gerät hinzugefügt wurde  |  R  |     
 refs.diag.errorCodes             | Zeichenfolge      | URI der Diagnoseerweiterung für Fehlercode, sofern vorhanden  |  R  |     
 refs.diag.logs                   | Zeichenfolge      | URI der Diagnoseerweiterung für Protokolle, sofern vorhanden         |  R  |     
 refs.location                    | Zeichenfolge      | URI der Positionserweiterung, sofern vorhanden              |  R  |     
 refs.mgmt                        | Zeichenfolge      | URI der Managementerweiterung, sofern vorhanden                  |  R  |     



## Erweiterte Attribute 
{: #extended_attributes}

Zusätzlich zu den oben im Abschnitt 'Attribute' aufgeführten Kernattributen gibt es zusätzliche Attribute, die als Erweiterungen des Basisgerätemodells behandelt werden.
Einfache Abfragen zu den Geräterückgabeinformationen vom Basisgerätemodell, aber keine Erweiterungen.
Informationen von Erweiterungen müssen ausdrücklich angefordert werden.



Erweiterungsname     | Präfix der Attribute  | Verwendungszweck       
------------- | ------------- | -------------                                         
Diagnose        | diag                 | Fehlerprotokolle und Diagnoseinformationen                  
Position           | location              | Position des Geräts, wird möglicherweise regelmäßig aktualisiert
Gerätemanagement  | mgmt                  | Gerätemanagementaktionen, zum Beispiel 'Firmware-Update'        


### Diagnoseerweiterung 


Die Diagnoseattribute sind optional und nur für Geräte mit Fehlerprotokollinformationen verfügbar. Diese Attribute sind für die Diagnose von Geräteproblemen konzipiert und nicht für die Behebung von Fehlern im Zusammenhang mit der Verbindung zu {{site.data.keyword.iot_short_notm}}. Die Informationen in diesen Attributen müssen separat abgerufen werden, weil die in diesen Attributen gespeicherten Informationen unter Umständen sehr umfangreich sein können. 

Diagnoseprotokollinformationen bestehen aus einer Reihe von Einträgen, an die mithilfe einer API Einträge angehängt sein können; dabei können jedoch ältere Einträge verloren gehen, weil die Diagnoseprotokolle eine noch praktikable Größe aufweisen sollen. Jeder Eintrag besteht aus einer Nachricht, einer Angabe zum Schweregrad, einer Zeitmarke und optional Bytefeldgruppendaten. 


Attribut             | Typ        | Beschreibung                                                  | API | DMA
------------- | ------------- | ------------- | ------------- | -------------
 diag.errorCodes[]    | Feldgruppe aus </br> ganzen Zahlen   | Feldgruppe aus Fehlercodes                                         |  A  |  A  
 diag.log[]           | Feldgruppe       | Feldgruppe aus Diagnosedaten                                     |  A  |  A  
 diag.log[].message   | Zeichenfolge      | Diagnosenachricht                                           |     |     
 diag.log[].timestamp | Zeichenfolge      | ISO8601 date-time: Datum und Zeit des Protokolleintrags                |     |     
 diag.log[].logData   | Zeichenfolge      | byte: Diagnosedaten, base-64-codiert                       |     |     
 diag.log[].severity  | Zahl      | Schweregrad der Nachricht, 0: Informationsnachricht, 1: Warnung, 2: Fehler  |     |     


### Positionserweiterung 

Diese Attribute sind optional und nur für Geräte mit Positionsinformationen verfügbar. Die Positionsinformationen werden separat gespeichert, damit Speicherverfahren verwendet werden können, die für dynamische Informationen besser geeignet sind, die häufig aktualisiert werden, zum Beispiel auf einem Mobilgerät. 

Bei Lösungen, für die häufige Positionsaktualisierungen im Vordergrund stehen, wird erwartet, dass die Position als Teil der Ereignisnutzdaten des Geräts behandelt werden, was höhere Aktualisierungsraten sowie ein einfaches Speichern von archivierten Daten und Analysedaten ermöglicht. 


Attribut                  | Typ    | Beschreibung                                              | API  | DMA
------------- | ------------- | ------------- | ------------- | -------------
 location.longitude        | Zahl  | Längengrad in Dezimalgrad unter Verwendung von WGS84                 |  W  |  W  
 location.latitude         | Zahl  | Breitengrad in Dezimalgrad unter Verwendung von WGS84                  |  W  |  W  
 location.elevation        | Zahl  | Erhebung in Meter unter Verwendung von WGS84                          |  W  |  W  
 location.measuredDateTime | Zeichenfolge  |ISO8601 date-time: Datum und Zeit der Positionsmessung  |  W  |  W  
 location.updatedDateTime  | Zeichenfolge  | ISO8601 date-time: Datum und Zeit                         |  R  |     
 location.accuracy         | Zahl  | Accuracy of the position in metres                       |  W  |  W  


### Gerätemanagementerweiterung 

Attribute des Typs `mgmt.` stehen nur für verwaltete Geräte zur Verfügung. Wenn ein verwaltetes Gerät zu einem ruhenden Gerät wird, wird es zu einem nicht verwalteten Gerät und die Attribute des Typs `mgmt.` werden gelöscht. Die Attribute des Typs `mgmt.` werden von {{site.data.keyword.iot_short_notm}} als Ergebnis der Verarbeitung von Gerätemanagementanforderungen festgelegt. Diese Attribute können mithilfe der API nicht direkt geschrieben werden. 

Geräte haben einen Lebenszyklus im Management, der durch ihren Status als verwaltete Geräte definiert ist. Der Gerätemanagementagent eines Geräts ist dafür zuständig, die Anforderung 'Gerät verwalten' mithilfe des Gerätemanagementprotokolls zu senden. Zur Handhabung von nicht mehr vorhandenen Geräten in einer Umgebung mit einer großen Anzahl von Geräten kann ein verwaltetes Gerät so eingerichtet werden, dass es regelmäßig die Anforderung 'Gerät verwalten' sendet, damit {{site.data.keyword.iot_short_notm}} erkennen kann, ob ein Gerät in den ruhenden Zustand versetzt wurde. Zur Vereinfachung dieser Funktion verfügt die Anforderung 'Gerät verwalten' über einen optionalen Parameter für den Lebenszyklus. Wenn {{site.data.keyword.iot_short_notm}} eine Anforderung 'Gerät verwalten' mit dem Lebenszyklusparameter empfängt, wird der Zeitpunkt berechnet, vor dem eine weitere Anforderung 'Gerät verwalten' erforderlich ist, und im Attribut `mgmt.dormantDateTime` gespeichert. 


Attribut                       | Typ     | Beschreibung                                             | API  | DMA
------------- | ------------- | ------------- | ------------- | -------------
 mgmt.dormant                   | Boolescher Wert  | Gibt an, ob das Gerät zu einem ruhenden Gerät wurde                   |  R  |     
 mgmt.dormantDateTime           | Zeichenfolge   | ISO8601 date-time: Datum und Zeit des Zeitpunkts, an dem das Gerät zu einem ruhenden Gerät wird    |  R  |     
 mgmt.lastActivityDateTime      | Zeichenfolge   | ISO8601 date-time: Datum und Zeit der letzten Aktivität, wird regelmäßig aktualisiert     |  R  |     
 mgmt.supports.deviceActions    | Boolescher Wert  | Gibt an, ob von dem Gerät die Aktionen für Neustart und Factory-Reset unterstützt werden   |  R  |     
 mgmt.supports.firmwareActions  | Boolescher Wert  | Gibt an, ob von dem Gerät die Aktionen für Firmware-Download und Firmware-Update unterstützt werden     |  R  |     
 mgmt.firmware.version          | Zeichenfolge   | Die Version der Firmware des Geräts               |  R  |  W  
 mgmt.firmware.name             | Zeichenfolge   | Der Name der Firmware, die auf dem Gerät verwendet werden soll       |  R  |  W  
 mgmt.firmware.uri              | Zeichenfolge   | Die URI, von der das Firmware-Image heruntergeladen werden kann  |  R  |  W  
 mgmt.firmware.verifier         | Zeichenfolge   | Der Verifizierungszeichenfolge (zum Beispiel eine Kontrollsumme) für das Firmware-Image zum Überprüfen der Integrität  |  R  |  W  
 mgmt.firmware.state            | Zahl   | Gibt den Status des Firmware-Downloads an                |  R  |  W  
 mgmt.firmware.updateStatus     | Zahl   | Gibt den Status der Aktualisierung an                      |  R  |  W  
 mgmt.firmware.updatedDateTime  | Zeichenfolge   | ISO8601 date-time: Datum und Zeit der letzten Aktualisierung                  |  R  |     
