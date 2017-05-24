---

copyright:
years: 2016, 2017
lastupdated: "2017-04-11"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Anwendungsschnittstelle - Szenario 2 (Beta)
{: #scenario}

Durch die Verwendung einer Anwendungsschnittstelle entfällt für eine Anwendung die Notwendigkeit zu verstehen, wie ein Gerät oder ein Ding konfiguriert ist. Sie können beispielsweise die Temperatur eines Raumes mithilfe eines einzelnen Geräts messen oder die Raumtemperatur berechnen, indem Sie den durchschnittlichen Messwert einer Reihe von Geräten nehmen. Die Anwendung benötigt Informationen zum Status eines Raumes oder von Räumen, wobei eine Komponente eine Temperatureigenschaft ist. Dabei ist es egal, wie der von der Anwendung empfangene Temperaturwert berechnet wird.

In diesem Szenario geben Temperatur- und Feuchtigkeitssensoren Umgebungsdaten aus, die in zwei Besprechungsräumen erfasst werden. Die Daten des Temperatur- und des Feuchtigkeitssensors werden separat zwei Anwendungsschnittstellen für Geräte-Typen zugeordnet: einer für den Gerätetyp Thermometer und einer anderen für den Gerätetyp Hygrometer. Es wird dann ein 'Ding'-Typ mit der Bezeichnung *Raumtyp* gemeinsam mit zwei 'Ding'-Instanzen für den Raumtyp erstellt: *Besprechungsraum 1* und *Besprechungsraum 2*.

In diesem Szenario wird eine Zusammensetzung eingerichtet, die die Anwendungsschnittstellen für Thermometer und Hygrometer enthält. Die richtigen Umgebungssensoren werden dann den einzelnen Rauminstanzen zugeordnet: Beispielsweise werden *Temperatursensor 1* und *Feuchtigkeitssensor 1* dem *Besprechungsraum 1* zugeordnet.

## Voraussetzungen
{: #pre_req}

Dieses Szenario baut auf dem vorherigen Szenario [Anwendungsschnittstelle - Szenario 1](im_index_scenario) auf.

Bevor Sie fortfahren, stellen Sie Folgendes sicher:
- Verwenden Sie die gleiche {{site.data.keyword.iot_short_notm}}-Organisationsinstanz und einen API-Schlüssel oder Token für diese Organisation. Weitere Informationen zu API-Schlüsseln und Token finden Sie in [HTTP-REST-API für Anwendungen](../applications/api.html#authentication).
- Sie haben zwei Anwendungsschnittstellen erstellt, eine für einen Temperatursensor und eine für einen Feuchtigkeitssensor. Informationen zum Konfigurieren einer Anwendungsschnittstelle für einen Temperatursensor finden Sie im Abschnitt mit dem [Szenario für Anwendungsschnittstellen für Gerätetypen](../information_management/im_index_scenario).

## Informationen zu diesem Vorgang
{: #about}

In {{site.data.keyword.iot_short_notm}} kann ein 'Ding' aus einer Reihe von Geräten und Dingen bestehen. Ein 'Ding'-Typ definiert, wie sich Instanzen eines Dings zusammensetzen. Eine Anwendungsschnittstelle kann einem
'Ding'-Typ zugeordnet werden. Diese Zuordnung definiert die Struktur des Status, der für eine Instanz des 'Ding'-Typs generiert wird. Mit Zuordnungen wird festgelegt, wie Eigenschaften von den aggregierten Geräten und Dingen zu Eigenschaften für einen 'Ding'-Status zugeordnet werden.

In diesem Szenario geben zwei Temperatursensoren und zwei Feuchtigkeitssensoren Ereignisse an {{site.data.keyword.iot_short_notm}} aus. Ein Temperatursensor und ein Feuchtigkeitssensor befinden sich im Besprechungsraum 1 eines Bürogebäudes. Der andere Temperatursensor und der andere Feuchtigkeitssensor sind im Besprechungsraum 2.

![Zuordnung zwischen Ding 'Temperatur' und 'Feuchtigkeit' und einer Anwendung auf {{site.data.keyword.iot_short_notm}}.](images/Information "Zuordnung zwischen mehreren Umgebungssensoren in einem Raum und einer Anwendung auf {{site.data.keyword.iot_short_notm}}")

Mit einem 'Ding'-Typ mit der Bezeichnung *Raumtyp* wird angegeben, wie sich Instanzen von Räumen zusammensetzen. Eine Anwendungsschnittstelle ist dem *Raumtyp* zugeordnet und legt fest, dass eingehende Ereignisse einem einzelnen Messwert zugeordnet werden, der sowohl die Temperatur als auch die Feuchtigkeit anzeigt. Dieser einzelne Messwert ist der 'Ding'-Status. Mit Zuordnungen wird festgelegt, wie Eigenschaften von den Temperatur- und Feuchtigkeitssensoren diesem 'Ding'-Status zugeordnet werden. Wenn diese Sensoren einen neuen Messwert ausgeben, wird der Wert der Eigenschaft geändert, die dem 'Ding'-Status zugeordnet ist.

Die folgenden vier Geräte sind eingeschlossen:

Gerät/Typ | Ereignis | Ereignisnutzdaten/Eigenschaft
------------- |  ------------- | -------------
*Temperatursensor 1*/Thermometer (Besprechungsraum 1) | `iot-2/evt/`*`tevt`*`/fmt/json` | `{ “t” : 34.5 }`/ **temperature1**
*Temperatursensor 2*/Thermometer (Besprechungsraum 2) | `iot-2/evt/`*`tempevt`*`/fmt/json` | `{ “temp” : 34.5 }`/ **temperature2**  
*Feuchtigkeitssensor 1*/Hygrometer (Besprechungsraum 1) | `iot-2/evt/`*`hevt`*`/fmt/json` | `{  “h” : "75%" }`/ **humidity1**
*Feuchtigkeitssensor 2*/Hygrometer (Besprechungsraum 2) |`iot-2/evt/`*`humevt`*`/fmt/json` | `{  “hum” : "75%"}`/ **humidity2**

Die Anwendungsschnittstelle des 'Ding'-Typs stellt den 'Ding'-Status in der folgenden Struktur dar:
```
{
  “temperature” : <aktueller Temperaturwert in Celsius>
  "humidity" : <aktueller Feuchtigkeitswert>
  }
```

<!--
The code that is used in this example is available in the updated {{site.data.keyword.iot_short_notm}} [[Python library ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-python){: new_window} in GitHub, in the **thingDataTransform** sample.
-->  

Verwenden Sie das folgende Beispielszenario zum Einrichten Ihrer eigenen Schnittstellenumgebung.  

## Fügen Sie bei Bedarf einen Gerätetyp und ein Gerät hinzu  
{: #add_device}  
In diesem Szenario werden zwei Gerätetypen und vier Geräteinstanzen verwendet. Die Geräteinstanzen *Temperatursensor 1* und *Temperatursensor 2* sind dem Gerättyp *Thermometer* zugeordnet. Die Geräteinstanzen *Feuchtigkeitssensor 1* und *Feuchtigkeitssensor 2* sind dem Gerättyp *Hygrometer* zugeordnet.

Informationen zur Verwendung von REST-APIs zum Hinzufügen eines Gerätetyps finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofThings.ibmcloud.com/swagger/v0002.html#!/Device_Types).  

## Schritt 1: Zusammensetzungsschemadatei erstellen  
{: #crt_composition_file}  
Erstellen Sie eine Zusammensetzungsschemadatei, die die Anwendungsschnittstellen-IDs des Geräts für jeden Gerätetyp für Feuchtigkeit und Temperatur referenziert.  

Das folgende Beispiel zeigt das Erstellen einer Zusammensetzungsschemadatei mit dem Namen *Raumtypschema*.  
```
{
   "$schema": "http://json-schema.org/draft-04/schema#",
   "type" : "object",
   "title" : "Raumtypschema",
   "description" : "JSON-Schema, das die Struktur des 'Ding'-Typs 'Raum' angibt.",
   "properties" : {
       "temperatureSensor": {
           "description": "Das Temperatursensorgerät",
           "$applicationInterfaceRef": "58c135e352faff0001198a89"
       },
       "humiditySensor": {
           "description": "Das Feuchtigkeitssensorgerät",
           "$applicationInterfaceRef": "58c135ea52faff0001678f06"
       }
   },
   "required" : [
       "temperatureSensor",
       "humiditySensor"
   ]
}
```
**Tipp:** Verwenden Sie den Parameter "required", um eine oder mehrere Eigenschaften als erforderlich zu markieren. Erforderliche Eigenschaften müssen in einer Gerätenachricht enthalten sein, damit Watson IoT Platform den Gerätestatus mit den Gerätedaten aktualisieren kann. Eine Nachricht, die die erforderliche Eigenschaft nicht enthält, wird nicht verarbeitet.   
**Hinweis:** Die Schema-ID, die beim Erstellen einer Schemadatei für den 'Ding'-Typ generiert wird, muss beim Erstellen des 'Ding'-Typs angegeben werden.  

## Schritt 2: Zusammensetzungsschemaressource erstellen  
{: #crt_composition_resource}  

Erstellen Sie eine Schemaressource, indem Sie die Schemadatei des 'Ding'-Typs hochladen, die im vorherigen Schritt erstellt wurde.  
Laden Sie diese Schemadatei unter Verwendung der folgenden API hoch:  
```
POST /schemas
```  
Folgende Parameter sind erforderlich:  
<table>
<tr>
<th>	Parameter	</th><th>	Beschreibung	</th>
</tr>
<tr>
<td>	name	</td><td>	Geben Sie einen Namen für das Zusammensetzungsschema an, das Sie erstellen.	</td>
</tr>
<tr>
<td>	schemaFile	</td><td>	Pfad zur lokalen JSON-Datei des Zusammensetzungsschemas.	</td>
</tr>
</table>

Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas).  

<!-- The following example shows how to use Python to create the thing type schema resource:  
```python
roomTypeSchemaFile = open(schemasDir + "roomType.json", "r");
roomTypeSchema = roomTypeSchemaFile.read();
roomTypeSchemaFile.close();
"roomTypeSchemaId", result = api.createSchema("Room Type Schema", "roomType.json", roomTypeSchema)
```  -->

## Schritt 3: 'Ding'-Typ erstellen  
{: #crt_thing_type}  

'Ding'-Typen werden zum Modellieren von 'Ding'-Instanzen verwendet. In einer Organisation muss ein 'Ding'-Typ erstellt werden, bevor eine 'Ding'-Instanz generiert werden kann. Erstellen Sie für diese Szenario einen 'Ding'-Typ.  
Das Schema, das mit einem 'Ding'-Typ verbunden ist, definiert den Typ von Objekten, die zu einer Instanz eines Dings zusammengefasst werden. Der 'Ding'-Typ muss die Schemaressource des 'Ding'-Typs referenzieren, die Sie im vorherigen Schritt erstellt haben.  
Erstellen Sie einen 'Ding'-Typ unter Verwendung der folgenden API:
```
POST /thing/types
```
Folgende Parameter sind erforderlich:  
<table>
<tr><th>Parameter</th><th>Beschreibung</th></tr>
<tr><td>Id</td><td>Geben Sie eine ID für den 'Ding'-Typ an, den Sie erstellen.</td></tr>
<tr><td>name</td><td>Geben Sie einen Namen für den 'Ding'-Typ an, den Sie erstellen.</td></tr>
<tr><td>schemaId</td><td>Die für die Zusammenfassungsschemaressource erstellte ID.</td></tr>
</table>

Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types).  

<!-- The following example shows how to use Python to create a thing type that is called *RoomType*.
```python
result = api.createThingType(thingType, "RoomType", "roomTypeSchemaId", "The Room Thing type")

```  -->

## Schritt 4: Anwendungsschnittstellenschemadatei erstellen  
{: #crt_ai_schema_file}
In Ihrer Anwendungsschnittstelle können Sie die Struktur der Daten definieren, die als 'Ding'-Status gespeichert sind. Erstellen Sie für dieses Szenario eine Anwendungsschnittstelle, die die Eigenschaften für Temperatur und Feuchtigkeit definiert. Verbinden Sie die Anwendungsschnittstelle mit dem 'Ding'-Typ *Raumtyp* durch das Referenzieren der Anwendungsschnittstellen-ID, die beim Erstellen der Anwendungsschnittstellenressource generiert wird.  
Das folgende Beispiel zeigt das Erstellen einer Anwendungsschnittstellenschemadatei mit dem Namen *Raumtypschema*.
```
{
   "$schema": "http://json-schema.org/draft-04/schema#",
   "type" : "object",
   "title" : "Raumtypschema",
   "description" : "JSON-Schema, das die kanoische Raumstatusstruktur definiert",
   "properties" : {
       "temperature" : {
           "description" : "Temperatur in Grad Celsius",
           "type" : "number",
           "minimum" : -273.15,
           "default" : 0.0
       },
       "humidity" : {
           "description" : "Prozentsatz Feuchtigkeit",
           "type" : "number",
           "minimum" : 0,
           "maximum" : 100,
           "default" : 0.0
       }
   },
   "required" : [
       "temperature",
       "humidity"
   ]
}
```  
## Schritt 5: Anwendungsschnittstellenschemaressource erstellen  
{: #crt_ai_schema_resource}  
Laden Sie die Anwendungsschnittstellenschemadatei hoch, die Sie im vorherigen Schritt erstellt haben, um eine Anwendungsschnittstellenschemaressource für Ihren 'Ding'-Typ zu erstellen. Verwenden Sie dazu die folgende API:  
```
POST /schemas
```  
Folgende Parameter sind erforderlich:  
<table>
<tr>
<th>Parameter</th><th>Beschreibung</th>
</tr>
<tr>
<td>name</td><td>Geben Sie einen Namen für das Anwendungsschnittstellenschema an, das Sie erstellen.</td>
</tr>
<tr>
<td>schemaFile</td><td>Pfad zur lokalen JSON-Datei des Anwendungsschnittstellenschemas.</td>
</tr>
</table>  

Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas).  

<!-- The following example shows how to use Python to create the thing type application interface schema resource:  
```python
roomSchemaFile = open(schemasDir + "room.json", "r");
roomSchema = roomSchemaFile.read();
roomSchemaFile.close();
"roomSchemaId", result = api.createSchema("Room Schema", "room.json", roomSchema)
```  -->

Verwenden Sie die Schema-ID, um die Anwendungsschnittstellenschemaressource zu der Anwendungsschnittstelle für den 'Ding'-Typ hinzuzufügen.  

## Schritt 6: Anwendungsschnittstelle für den 'Ding'-Typ erstellen  
{: #crt_thing_ai}  
Die Anwendungsschnittstelle muss die Anwendungsschnittstellenschemaressource referenzieren, die Sie im vorherigen Schritt erstellt haben.  
Verwenden Sie die folgende API, um eine Anwendungsschnittstelle zu erstellen:  
```
POST /applicationinterfaces
```  
Folgende Parameter sind erforderlich:  
<table>
<tr>
<th>	Parameter	</th><th>	Beschreibung	</th>
</tr>
<tr>
<td>	name	</td><td>	Geben Sie einen Namen für die Anwendungsschnittstelle an, die Sie erstellen.	</td>
</tr>
<tr>
<td>	description	</td><td>	Geben Sie eine Beschreibung der Anwendungsschnittstelle an.	</td>
</tr>
<tr>
<td>	schemaId	</td><td>	Pfad zur lokalen JSON-Datei des Anwendungsschnittstellenschemas.	</td>
</tr>
</table>  

Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Application_Interfaces).  
Verwenden Sie die Schema-ID, die in der vorherigen Antwort zurückgegeben wurde, um das Anwendungsschnittstellenschema zu der Anwendungsschnittstelle hinzuzufügen.  

<!-- The following example shows how to use Python to create an application interface:  
```python
"applicationInterfaceId", result = api.createApplicationInterface("IRoom", "roomSchemaId")
```  -->

Verwenden Sie die Anwendungsschnittstellen-ID, um Ihre Anwendungsschnittstelle zu Ihrem Gerätetyp hinzuzufügen. Diese ID wird auch verwendet, um ein eingehendes Geräteereignis einer Eigenschaft zuzuordnen, die von der Anwendungsschnittstelle definiert wird.  

## Schritt 7: Anwendungsschnittstelle zu einem 'Ding'-Typ hinzufügen  
{: #add_thing_ai}  
Verwenden Sie die folgende API, um eine Anwendungsschnittstelle zu einem 'Ding'-Typ hinzuzufügen:  
```
POST /thing/types/{thingtypeId}/applicationinterfaces
```  
Folgende Parameter sind erforderlich:  
<table>
<tr>
<th>	Parameter	</th><th>	Beschreibung	</th>
</tr>
<tr>
<td>	id	</td><td>	Die für den 'Ding'-Typ erstellte ID.	</td>
</tr>
<tr>
<td>	name	</td><td>	Geben Sie einen Namen für die Anwendungsschnittstelle an, die Sie erstellen.	</td>
</tr>
<tr>
<td>	schemaId	</td><td>	Die für die Anwendungsschnittstellenressource erstellte ID.	</td>
</tr>
<tr>
<td>	refs/schema	</td><td>	Der Pfad zur Anwendungsschnittstellenressource. Für gewöhnlich: /schemas/*schemaId*	</td>
</tr>
</table>  

Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types).  
In diesem Szenario ist die Anwendungsschnittstelle dem 'Ding'-Typ *Raumtyp* zugeordnet.

<!-- The following example shows how to use Python to add the thing application interface to the thing type *RoomType*:  
```python
result = api.addApplicationInterfaceToThingType(RoomType, "applicationInterfaceId", "roomSchemaId")
``` -->

## Schritt 8: Zuordnungen definieren
{: #define_Thing_type_mappings}

Definieren Sie die Zuordnungen für den 'Ding'-Typ, die beschreiben, wie Eigenschaften vom Status der zusammengefassten Geräte oder Dinge zu den Eigenschaften zugeordnet werden können, die für die Anwendungsschnittstelle des 'Ding'-Typs definiert sind.

Verwenden Sie die folgende API, um Ereignisse zuzuordnen:  
```
POST /thing/types/{thingtypeId}/mappings
```  

Folgende Parameter sind erforderlich:  
<table>
<tr>
<th>	Parameter	</th><th>	Beschreibung	</th>
</tr>
<tr>
<td>	applicationInterfaceId	</td><td>	Die für die Anwendungsschnittstelle erstellte ID.	</td>
</tr>
<tr>
<td>	propertyMappings	</td><td>	Eine gültige JSON-Struktur, die für die Anwendungsschnittstelle definierte Eigenschaften zu Eigenschaften der Ereignisnutzdaten des Geräts zuordnet.	</td>
</tr>
</table>  

Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types).

<!--  The following example shows how to use Python to add a mapping to thing type *RoomType*:

```python
mappings = {
     "humiditySensor": {
       "humidity": "$event.humidity"
     },
     "temperatureSensor": {
       "temperature": "$event.temperatureC"
     }
 }

 result = api.addMappingsToThingType(thingType, "applicationInterfaceId", mappings)
``` -->

Das folgende Beispiel zeigt einen Beispieleintrag für den Parameter "propertyMappings":

```
{
  "applicationInterfaceId": "58dd849752faff0001638851",
  "propertyMappings": {
       "humiditySensor": {
         "humidity": "$event.humidity"
       },
       "temperatureSensor": {
         "temperature": "$event.temperatureC"
       }
   }
}
```

Der *Feuchtigkeitssensor* ist im 'Ding'-Schema definiert. "$event.humidity" ist im Anwendungsschnittstellenschema mit der ID "58c135ea52faff0001678f06" definiert.
Der *Temperatursensor* ist im 'Ding'-Schema definiert. "$event.temperatureC" ist im Anwendungsschnittstellenschema mit der ID "58c135e352faff0001198a89" definiert.

## Schritt 9: Die Konfiguration implementieren, die dem 'Ding'-Typ zugeordnet ist  
{: #deploy_Thing_config}   
Implementieren Sie die Konfiguration, die sich auf die Aktualisierung des 'Ding'-Status für die einzelne 'Ding'-Typen bezieht. Diese Konfiguration enthält Schemas, Anwendungsschnittstellen und Zuordnungen.

Bevor Sie Instanzen des 'Ding'-Typs erstellen können, müssen Sie die Konfiguration des 'Ding'-Typs implementieren.

Verwenden Sie die folgende API, um die Konfiguration Ihres 'Ding'-Typs zu implementieren:

```
PATCH /thing/types/{thingtypeId}
```
Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types).

<!-- The following example shows how to use Python to deploy your configuration for thing type *Room*:

```python
result = api.deployThingTypeConfiguration(thingType)
``` -->

## Schritt 10: Instanz eines 'Ding'-Typs erstellen
{: #create_Thing_instances}

Ein 'Ding' ist eine Instanz eines 'Ding'-Typs. Mit einem Ding können Sie eine oder mehrere Instanzen eines Geräts oder Dinge in einem einzelnen Objekt zusammenfassen.

Verwenden Sie die folgende API, um ein Ding zu erstellen:

```
POST /thing/types/{thingTypeId}/things
```

Folgende Parameter sind erforderlich:  
<table>
<tr>
<th>	Parameter	</th><th>	Beschreibung	</th>
</tr>
<tr>
<td>	typeId	</td><td>		Die ID des von Ihnen zuvor erstellten 'Ding'-Typs.</td>
</tr>
<tr>
<td>	thingId	</td><td>	Geben Sie einen Namen für die 'Ding'-Instanz an, die Sie erstellen.	</td>
</tr>
</table>

Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Things).

Im vorliegenden Szenario müssen zwei 'Ding'-Instanzen mit dem 'Ding'-Typ *Raumtyp* erstellt werden. Eine 'Ding'-Instanz trägt die Bezeichnung *Besprechungsraum 1* und die andere 'Ding'-Instanz die Bezeichnung *Besprechungsraum 2*.

<!-- The following example shows how to use Python to create a thing instance that is called *meetingroom1*. *meetingroom1* is associated with the *temperatureSensor1* and *humiditySensor1* device instances.

```python
thingId = "meetingroom1"
 meetingroom1AggregatedObjects = {
   "temperatureSensor": {
     "type": "device",
     "typeId": "TemperatureSensor",
     "id": "temperatureSensor1"
   },
   "humiditySensor": {
     "type": "device",
     "typeId": "HumiditySensor",
     "id": "humiditySensor1"
   }
 }
 result = api.createThing(thingType, thingId, "Meeting Room 1", "The big meeting room!!!", aggregatedObjects = meetingroom1AggregatedObjects)
``` -->

Die erstellte 'Ding'-ID wird in der URL der POST-Methode verwendet, die aufgerufen wird, um ein Temperaturereignis zur 'Ding'-Anwendungsschnittstelle hinzuzufügen.

<!-- The following example shows how to use Python to create a thing instance that is called *meetingroom2*. *meetingroom2* is associated with the *temperatureSensor2* and *humiditySensor2* device instances.

```python
thingId = "meetingroom2"
   meetingroom2AggregatedObjects = {
    "temperatureSensor": {
      "type": "device",
      "typeId": "TemperatureSensor",
      "id": "temperatureSensor2"
    },
    "humiditySensor": {
      "type": "device",
      "typeId": "HumiditySensor",
      "id": "humiditySensor2"
    }
  }
result = api.createThing(thingType, thingId, "Meeting Room 2", "The little meeting room!!!", aggregatedObjects = meetingroom2AggregatedObjects)  
``` -->

## Schritt 11: Prüfen, dass zugeordnete Geräteereignisse in der Anwendungsschnittstelle publiziert werden  
{: #publish_event}  
Publizieren Sie die folgenden Ereignisse für Geräte, die in der 'Ding'-Instanz *Besprechungsraum 1* zusammengefasst werden:  
 - Ein Temperaturereignis von *Temperatursensor 1* für Topic `iot-2/evt/tevt/fmt/json`  
 - Ein Feuchtigkeitsereignis von *Feuchtigkeitssensor* für Topic `iot-2/evt/hevt/fmt/json`  
Publizieren Sie die folgenden Ereignisse für Geräte, die in der 'Ding'-Instanz *Besprechungsraum 2* zusammengefasst werden:  
 - Ein Temperaturereignis von *Temperatursensor 2* für Topic `iot-2/evt/tempevt/fmt/json`  
 - Ein Feuchtigkeitsereignis von *Feuchtigkeitssensor 1* für Topic `iot-2/evt/humevt/fmt/json`  
Informationen zum Publizieren eines eingehenden Ereignisses von einem Gerät finden Sie in [MQTT-Konnektivität für Anwendungen](../applications/mqtt.html#publishing_device_events).  

## Schritt 12: Überprüfen, ob der 'Ding'-Status geändert wird  
{: #verify_Thing_state}  
Verwenden Sie die folgende API, um den 'Ding'-Status zu prüfen:  
```
GET /thing/types/{thingTypeId}/things/{thingId}/state/{applicationInterfaceId}
```  

Folgende Parameter sind erforderlich:  
<table>
<tr>
<th>Parameter	</th><th>	Beschreibung</th>
</tr>
<tr>
<td>thingtypeId	</td><td>Die ID des 'Ding'-Typs.</td>
</tr>
<tr>
<td>thingId	</td><td>	Die 'Ding'-ID.</td>
</tr>
<tr>
<td>applicationInterfaceId</td><td>Die für die Anwendungsschnittstelle erstellte ID.</td>
</tr>
</table>  

Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types).  

<!-- The following example shows how to use Python to retrieve the current state of *meetingroom1* by referencing the identifier of the application interface that was created:  
```python
result = api.getThingStateForApplicationInterface("RoomType", "meetingroom1", applicationInterfaceId)
```  
The following example shows how to use Python to retrieve the current state of *meetingroom2* by referencing the identifier of the application interface that was created:  
```python
result = api.getThingStateForApplicationInterface("RoomType", "meetingroom2", applicationInterfaceId)
``` -->
