---

copyright:
years: 2016, 2017
lastupdated: "2017-04-10"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Anwendungsschnittstelle - Szenario 1 (Beta)
{: #scenario}

Erstellen Sie mithilfe der folgenden Informationen ein Szenario, in dem Ereignisse von zwei Temperatursensoren an {{site.data.keyword.iot_short_notm}} publiziert werden. Ein Sensor misst die Temperatur in Grad Celsius. Der andere Sensor misst die Temperatur in Grad Fahrenheit. Die gemessenen Werte werden einem einzigen Temperaturmesswert in Grad Celsius zugeordnet. Wenn diese Geräte einen neuen Temperaturmesswert ausgeben, wird der Wert der Eigenschaft geändert, die dem Gerätestatus zugeordnet ist.

## Voraussetzungen

Sie müssen über eine {{site.data.keyword.iot_short_notm}}-Organisationsinstanz und über einen API-Schlüssel oder ein Token für die Organisation verfügen. Weitere Informationen zu API-Schlüsseln und Token finden Sie in [HTTP-REST-API für Anwendungen](../applications/api.html#authentication).

## Informationen zu diesem Vorgang

In diesem Szenario werden zwei Geräte konfiguriert.

Ein Gerät trägt den Namen *Temperatursensor 1*. Dieses Gerät publiziert Temperaturereignisse, die in Grad Celsius gemessen werden. Das Temperaturereignis wird im Topic `iot-2/evt/tevt/fmt/json` publiziert und enthält die folgenden Beispielnutzdaten:
```
{
  “t” : 34.5
}
```

**Hinweis:** Die Ereignis-ID lautet *tevt*. Diese ID ist erforderlich, wenn Sie ein Temperaturereignis dieses Typs zur physischen Schnittstelle hinzufügen und Zuordnungen definieren, um eine zugehörige Eigenschaft für ein eingehendes Ereignis dieses Typs einer Eigenschaft in Ihrer Anwendungsschnittstelle zuzuordnen. Im vorliegenden Szenario trägt die in der Anwendungsschnittstelle definierte Eigenschaft den Namen **temperature**.

Das andere Gerät trägt den Namen *Temperatursensor 2*. Dieses Gerät publiziert Temperaturereignisse, die in Grad Fahrenheit gemessen werden. Das Temperaturereignis wird im Topic `iot-2/evt/tempevt/fmt/json` publiziert und enthält die folgenden Beispielnutzdaten:
```
{
  “temp” : 72.55
}
```

**Hinweis:** Die Ereignis-ID lautet *tempevt*. Diese ID ist erforderlich, wenn Sie ein Temperaturereignis dieses Typs zur physischen Schnittstelle hinzufügen und Zuordnungen definieren, um eine zugehörige Eigenschaft für ein eingehendes Ereignis dieses Typs einer Eigenschaft in Ihrer Anwendungsschnittstelle zuzuordnen. Im vorliegenden Szenario trägt die in der Anwendungsschnittstelle definierte Eigenschaft den Namen **temperature**.

Außerdem wird eine Anwendungsschnittstelle konfiguriert. Diese Anwendungsschnittstelle stellt den Status für Geräte dieses Typs in der folgenden Struktur dar:
```
{
  “temperature” : <aktuelle Temperatur in Celsius>
  }
```
Mithilfe dieser Konfiguration können Sie Ihre Anwendung so konfigurieren, dass der zugeordnete Wert für **temperature** verarbeitet wird, anstatt den zugeordneten Wert für **t** zu verarbeiten und den zugeordneten Wert für **temp** erst nach Umwandlung in Grad Celsius zu verarbeiten.

![Zuordnung zwischen Temperatursensorgeräten und einer Anwendung in {{site.data.keyword.iot_short_notm}}.](images/Information "Zuordnung zwischen Temperatursensorgeräten und einer Anwendung in {{site.data.keyword.iot_short_notm}}")  

Verwenden Sie das folgende Beispielszenario zum Einrichten Ihrer eigenen Schnittstellenumgebung.

## Fügen Sie bei Bedarf einen Gerätetyp und ein Gerät hinzu
{: #step14}

Im vorliegenden Szenario werden zwei Gerätetypen und zwei Geräteinstanzen angenommen. Die Geräteinstanz *Temperatursensor 1* ist dem Gerätetyp *EnvSensor1* zugeordnet. Die Geräteinstanz *Temperatursensor 2* ist dem Gerätetyp *EnvSensor2* zugeordnet.

Informationen zur Verwendung von REST-APIs zum Hinzufügen eines Gerätetyps finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Types).

## Schritt 1: Eine Ereignisschemadatei erstellen
{: #step1}

Erstellen Sie für das vorliegende Szenario zwei Ereignisschemadateien, um die Struktur der eingehenden Temperaturereignisse zu definieren.

**Wichtig:** Stellen Sie für Ereignisnutzdaten für strukturiertes [JSON ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://json-schema.org/){:new_window} sicher, dass jede Verschachtelungsebene ordnungsgemäß in einen Eintrag `"properties"` eingeschlossen ist. Wenn die Nutzdaten beispielsweise `{"d":{"t":<temp>}}` lauten, verwenden Sie:
```
 "properties" : {
    "d" : {
      "properties" : {
        "t" : {
          "description" : "Temperature in degrees Celsius",
          "type" : "number",
          "minimum" : -273.15,
          "default" : 0.0
        }
      },
      "required" : ["t"]
    }
  },
  "required" : ["d"]
```

Das folgende Beispiel zeigt das Erstellen einer Schemadatei mit dem Namen *tEventSchema.json*. In dieser Datei wird die Struktur eines eingehenden Ereignisses von einem Temperatursensor definiert, der die Temperatur in Grad Celsius misst:

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor1 tEvent Schema",
  "description" : “defines the structure of a temperature event in degrees Celsius",
  "properties" : {
    "t" : {
      "description" : "temperature in degrees Celsius",
      "type" : "number",
      "minimum" : -273.15,
      "default" : 0.0
    }
  },
  "required" : ["t"]
}
  ```
**Tipp:** Verwenden Sie den Parameter "required", um eine oder mehrere Eigenschaften als erforderlich zu markieren. Erforderliche Eigenschaften müssen in einer Gerätenachricht enthalten sein, damit Watson IoT Platform den Gerätestatus mit den Gerätedaten aktualisieren kann. Eine Nachricht, die die erforderliche Eigenschaft nicht enthält, wird nicht verarbeitet.   

Der Schemadateiname *tEventSchema* wird verwendet, wenn Sie eine Ereignisschemaressource für Ihren Ereignistyp erstellen.

Das folgende Beispiel zeigt das Erstellen einer Schemadatei mit dem Namen *tempEventSchema.json*. In dieser Datei wird die Struktur eines eingehenden Ereignisses von einem Temperatursensor definiert, der die Temperatur in Grad Fahrenheit misst.

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor2 tempEvent Schema",
  "description" : “defines the structure of a temperature event in degrees Fahrenheit",
  "properties" : {
    "temp" : {
      "description" : "temperature in degrees Fahrenheit",
      "type" : "number",
      "minimum" : −459.67,
      "default" : 0.0
    }
  },
  "required" : ["temp"]
}
  ```
Der Schemadateiname *tempEventSchema* wird verwendet, wenn Sie eine Ereignisschemaressource für Ihren Ereignistyp erstellen.   

## Schritt 2: Ereignisschemaressource für den Ereignistyp erstellen
{: #step2}

Verwenden Sie die folgende API, um eine Ereignisschemaressource zu erstellen:

```
POST /schemas
```

Folgende Parameter sind erforderlich:  

Parameter	|	Beschreibung  
------	|	-----  
name	|	Geben Sie einen Namen für das Ereignisschema an, das Sie erstellen.  
schemaFile	|	Pfad zur lokalen JSON-Datei des Ereignisschemas.  



Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas).

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Erstellen der Ereignisschemaressource *tEventSchema.json*:

```curl
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=tEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tEventSchema.json'
```

Das folgende Beispiel zeigt eine Antwort auf die POST-Methode:

```
{
  "name" : “tEventSchema",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "contentType" : "application/octet-stream",
  "updated" : "2016-12-06T14:38:52Z",
  "schemaFileName" : "tEventSchema.json",
  "created" : "2016-12-06T14:38:52Z",
  "id" : "5846cd7c6522050001db0e0d",
  "refs" : {
      "content" : "/schemas/5846cd7c6522050001db0e0d/content"
  },
  "schemaType" : "json-schema",
  "updatedBy" : "a-8x7nmj-9iqt56kfil"
}
```
Die Schema-ID *5846cd7c6522050001db0e0d*, die als Antwort auf die POST-Methode zurückgegeben wird, ist erforderlich, wenn Sie ein Ereignisschema zu Ihrem Ereignistyp hinzufügen.

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Erstellen der Ereignisschemaressource *tempEventSchema.json*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: multipart/form-data’ \
  --form name=tempEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tempEventSchema.json"'
```

Das folgende Beispiel zeigt eine Antwort auf die POST-Methode:

```
{
  "schemaType" : "json-schema",
  "schemaFileName" : "tempEventSchema.json",
  "updated" : "2016-12-06T14:44:51Z",
  "name" : "tempEventSchema",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "created" : "2016-12-06T14:44:51Z",
  "id" : "5846cee36522050001db0e0e",
  "refs" : {
      "content" : "/schemas/5846cee36522050001db0e0e/content"
  },
  "contentType" : "application/octet-stream",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```
Die Schema-ID *5846cee36522050001db0e0e*, die als Antwort auf die POST-Methode zurückgegeben wird, ist erforderlich, wenn Sie ein Ereignisschema zu Ihrem Ereignistyp hinzufügen.

## Schritt 3: Einen Ereignistyp erstellen, der das Ereignisschema referenziert
{: #step3}

Jeder Ereignistyp verwendet zum Verweisen auf das Ereignisschema, das im vorherigen Beispiel erstellt wurde, die in der Antwort auf die POST-Methode zum Erstellen der Ereignisschemaressource zurückgegebene Schema-ID.

Verwenden Sie die folgende API, um einen Ereignistyp zu erstellen:

```
POST /event/types
```

Folgende Parameter sind erforderlich:  

Parameter	|	Beschreibung
------	|	-----
name	|	Geben Sie einen Namen für den Ereignistyp an, den Sie erstellen.
schemaId	|	Die für die Ereignisschemaressource erstellte ID.


Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Event_Types).


Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Erstellen eines Ereignistyps für ein Temperaturereignis, das in Grad Celsius gemessen wird:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tEvent", "schemaId" : "5846cd7c6522050001db0e0d”}'
```

Die Schema-ID *5846cd7c6522050001db0e0d* wird verwendet, um das Ereignisschema zu dem Ereignistyp hinzuzufügen. Diese ID wurde als Antwort auf die POST-Methode zurückgegeben, die zum Erstellen der Ereignisschemaressource *tEventSchema.json* verwendet wurde.

Das folgende Beispiel zeigt eine Antwort auf die POST-Methode:

```
{
  "updated" : "2016-12-06T14:53:49Z",
  "schemaId" : "5846cd7c6522050001db0e0d",
  "refs" : {
    "schema" : "/schemas/5846cd7c6522050001db0e0d"
  },
  "name" : "tEvent",
  "created" : "2016-12-06T14:53:49Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "id" : "5846d0fd6522050001db0e0f",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

Die Ereignistyp-ID *5846d0fd6522050001db0e0f*, die als Antwort auf die POST-Methode zurückgegeben wird, wird verwendet, um einen Ereignistyp zu der physischen Schnittstelle hinzuzufügen.

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Erstellen eines Ereignistyps für ein Temperaturereignis, das in Grad Fahrenheit gemessen wird:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tempEvent", "schemaId" : "5846cee36522050001db0e0e"}'
```
Die Schema-ID *5846cee36522050001db0e0e* wird verwendet, um das Ereignisschema zu dem Ereignistyp hinzuzufügen. Diese ID wurde als Antwort auf die POST-Methode zurückgegeben, die zum Erstellen der Ereignisschemaressource *tempEventSchema.json* verwendet wurde.

Das folgende Beispiel zeigt eine Antwort auf die POST-Methode:

```
{
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "schemaId" : "5846cee36522050001db0e0e",
  "created" : "2016-12-06T15:00:20Z",
  "id" : "5846d2846522050001db0e10",
  "updated" : "2016-12-06T15:00:20Z",
  "name" : “tempEvent”,
  "refs" : {
    "schema" : "/schemas/5846cee36522050001db0e0e"
  },
  "updatedBy" : "a-8x7nmj-9iqt56kfil"
}
```
Die Ereignistyp-ID *5846d2846522050001db0e10*, die als Antwort auf die POST-Methode zurückgegeben wird, wird verwendet, um einen Ereignistyp zu der physischen Schnittstelle hinzuzufügen.

## Schritt 4: Physische Schnittstelle erstellen
{: #step7}

Verwenden Sie die folgende API, um eine physische Schnittstelle zu erstellen:

```
POST /physicalinterfaces
```

Folgende Parameter sind erforderlich:  

Parameter	|	Beschreibung
------	|	-----
name	|	Geben Sie einen Namen für die physische Schnittstelle an, die Sie erstellen.


Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces).

Für das vorliegende Szenario sind zwei physische Schnittstellen erforderlich (eine für jeden Ereignistyp).

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Erstellen der ersten physischen Schnittstelle:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Env sensor physical interface 1"}'
```

Das folgende Beispiel zeigt eine Antwort auf die POST-Methode:

```
{
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
    "events" : "/physicalinterfaces/5847d1df6522050001db0e1a/events"
  },
  "id" : "5847d1df6522050001db0e1a",
  "name" : "Env sensor physical interface 1",
  "created" : "2016-12-07T09:09:51Z",
  "updated" : "2016-12-07T09:09:51Z",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

Die in der Antwort zurückgegebene ID der physischen Schnittstelle (*5847d1df6522050001db0e1a*) wird in der URL der POST-Methode verwendet, die aufgerufen wird, um ein Temperaturereignis zur physischen Schnittstelle hinzuzufügen, das in Grad Celsius gemessen wird.

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Erstellen der zweiten physischen Schnittstelle:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Env sensor physical interface 2"}'
```

Das folgende Beispiel zeigt eine Antwort auf die POST-Methode:

```
{
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
    "events" : "/physicalinterfaces/5847d1df6522050001db0e1b/events"
  },
  "id" : "5847d1df6522050001db0e1b",
  "name" : "Env sensor physical interface 2",
  "created" : "2016-12-07T09:19:51Z",
  "updated" : "2016-12-07T09:19:51Z",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

Die in der Antwort zurückgegebene ID der physischen Schnittstelle (*5847d1df6522050001db0e1b*), wird in der URL der POST-Methode verwendet, die aufgerufen wird, um ein Temperaturereignis zur physischen Schnittstelle hinzuzufügen, das in Grad Fahrenheit gemessen wird.   

## Schritt 5: Ereignistyp zur physischen Schnittstelle hinzufügen
{: #step8}

Verwenden Sie die folgende API, um einen Ereignistyp zu Ihrer physischen Schnittstelle hinzuzufügen:

```
POST /physicalinterfaces/{physicalInterfaceId}/events
```

Folgende Parameter sind erforderlich:  

Parameter	|	Beschreibung
------	|	-----
eventId	|	Geben Sie den Ereignisnamen von den Ereignisnutzdaten Ihres Geräts ein.
eventTypeId	|	Die für den Ereignistyp erstellte ID.


Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces).

Im vorliegenden Szenario werden die folgenden Ereignistypen zu den angegebenen physischen Schnittstellen hinzugefügt:
- Das Temperaturereignis in Grad Celsius (*tevt*) wird zur physischen Schnittstelle mit der ID *5847d1df6522050001db0e1a* unter Verwendung von *eventId* aus dem Topic und von *eventTypeId* aus der Erstellung der Ereignisschemaressource hinzugefügt.
- Das Temperaturereignis in Grad Fahrenheit (*tempevt*) wird zur physischen Schnittstelle mit der ID *5847d1df6522050001db0e1b* unter Verwendung von *eventId* aus dem Topic und von *eventTypeId* aus der Erstellung der Ereignisschemaressource hinzugefügt.


Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Hinzufügen des Temperaturereignisses *tevt* zur physischen Schnittstelle mit der ID *5847d1df6522050001db0e1a*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1a/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : “tevt", "eventTypeId" : "5846d0fd6522050001db0e0f"}'
```

Das folgende Beispiel zeigt eine Antwort auf die POST-Methode:

```
{
  "eventTypeId" : "5846d0fd6522050001db0e0f",
  "eventId" : "tevt"
}
```

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Hinzufügen des Temperaturereignisses *tempevt* zur physischen Schnittstelle mit der ID *5847d1df6522050001db0e1b*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1b/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : "tempevt", "eventTypeId" : "5846d2846522050001db0e10"}'
```

Das folgende Beispiel zeigt eine Antwort auf die POST-Methode:

```
{
  "eventTypeId" : "5846d2846522050001db0e10",
  "eventId" : “tempevt"
}
```

## Schritt 6: Gerätetyp für die Verbindung mit der physischen Schnittstelle aktualisieren
{: #step9}

Verwenden Sie die folgende API, um einen Gerätetyp zu aktualisieren:

```
PUT /device/types/{typeId}
```

Folgende Parameter sind erforderlich:  

Parameter	|	Beschreibung
------	|	-----
physicalInterfaceId	|	Die für die physische Schnittstelle erstellte ID.


Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

In diesem Szenario wird der Gerätetyp *EnvSensor1* zum Verbinden mit der physischen Schnittstelle *5847d1df6522050001db0e1a* und der Gerätetyp *EnvSensor2* zum Verbinden mit der physischen Schnittstelle *5847d1df6522050001db0e1b* aktualisiert.

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Aktualisieren des Gerätetyps *EnvSensor1*:

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an environment sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1a”}’
```

Das folgende Beispiel zeigt eine Antwort auf die POST-Methode:

```
{
  "deviceInfo" : {},
  "physicalInterfaceId" : "5847d1df6522050001db0e1a",
  "updatedDateTime" : "2016-12-07T09:49:52+00:00",
  "refs" : {
    "mappings" : "/device/types/EnvSensor1/mappings",
    "applicationInterfaces" : "/device/types/EnvSensor1/applicationinterfaces",
    "physicalInterface" : "/physicalinterfaces/5847d1df6522050001db0e1a"
   },
  "id" : "EnvironmentSensor",
  "description" : "an environment sensor",
  "metadata" : {},
  "classId" : "Device",
  "createdDateTime" : "2016-12-07T09:49:52+00:00"
}
```
Die Geräte-ID *EnvSensor1* ist erforderlich, wenn Sie Ihre physische Schnittstelle und Ihre Anwendungsschnittstelle hinzufügen.

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Aktualisieren des Gerätetyps *EnvSensor2*:

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an env sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1b”}’
```

Das folgende Beispiel zeigt eine Antwort auf die POST-Methode:

```
{
  "deviceInfo" : {},
  "physicalInterfaceId" : "5847d1df6522050001db0e1b",
  "updatedDateTime" : "2016-12-07T09:59:52+00:00",
  "refs" : {
    "mappings" : "/device/types/EnvSensor2/mappings",
    "applicationInterfaces" : "/device/types/EnvSensor2/applicationinterfaces",
    "physicalInterface" : "/physicalinterfaces/5847d1df6522050001db0e1b"
   },
  "id" : "EnvironmentSensor",
  "description" : "an environment sensor",
  "metadata" : {},
  "classId" : "Device",
  "createdDateTime" : "2016-12-07T09:49:52+00:00"
}
```
Die Geräte-ID *EnvSensor2* ist erforderlich, wenn Sie Ihre physische Schnittstelle und Ihre Anwendungsschnittstelle hinzufügen.



## Schritt 7: Anwendungsschnittstellenschemadatei erstellen
{: #step4}

Das folgende Beispiel zeigt das Erstellen einer Anwendungsschnittstellenschemadatei mit dem Namen *envSensor.json*.

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
    "type" : "object",
    "title" : "Environment Sensor Schema",
    "description" : "Schema to represent a canonical environment sensor device",
    "properties" : {
        "temperature" : {
            "description" : "temperature in degrees Celsius",
            "type" : "number",
            "minimum" : -273.15,
            "default" : 0.0
        }
    },
    "required" : ["temperature"]
}
```

## Schritt 8: Anwendungsschnittstellenschemaressource erstellen
{: #step5}

Verwenden Sie die folgende API, um eine Anwendungsschnittstellenschemaressource zu erstellen:

```
POST /schemas
```

Folgende Parameter sind erforderlich:  

Parameter	|	Beschreibung
------	|	-----
name	|	Geben Sie einen Namen für das Anwendungsschnittstellenschema an, das Sie erstellen.
schemaFile	|	Pfad zur lokalen JSON-Datei des Anwendungsschnittstellenschemas.


Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas).

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Erstellen des Anwendungsschnittstellenschemas:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=temperatureEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/envSensor.json"'
```

Das folgende Beispiel zeigt eine Antwort auf die POST-Methode:

```
{
  "created" : "2016-12-06T16:51:14Z",
  "name" : "temperatureEventSchema",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "updated" : "2016-12-06T16:51:14Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "schemaType" : "json-schema",
  "contentType" : "application/octet-stream",
  "schemaFileName" : "envSensor.json",
  "refs" : {
    "content" : "/schemas/5846ec826522050001db0e11/content"
  },
  "id" : "5846ec826522050001db0e11"
}
```
Verwenden Sie die Schema-ID *5846ec826522050001db0e11*, die in der Antwort auf die POST-Methode zurückgegeben wird, um das Anwendungsschnittstellenschema zu der Anwendungsschnittstelle hinzuzufügen.

## Schritt 9: Anwendungsschnittstelle erstellen, die ein Anwendungsschnittstellenschema referenziert
{: #step6}

Verwenden Sie die folgende API, um eine Anwendungsschnittstelle zu erstellen:

```
POST /applicationinterfaces
```

Folgende Parameter sind erforderlich:  

Parameter	|	Beschreibung
------	|	-----
name	|	Geben Sie einen Namen für die Anwendungsschnittstelle an, die Sie erstellen.
schemaId	|	Die für die Anwendungsschnittstellenschemaressource erstellte ID.


Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Application_Interfaces).

Verwenden Sie in diesem Szenario die Schema-ID *5846ec826522050001db0e11*, die in der vorherigen Antwort zurückgegeben wurde, um das Anwendungsschnittstellenschema zu der Anwendungsschnittstelle hinzuzufügen.

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Erstellen einer Anwendungsschnittstelle:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "environment sensor interface", "schemaId" : "5846ec826522050001db0e11"}'
```

Das folgende Beispiel zeigt eine Antwort auf die POST-Methode:

```
{
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "schemaId" : "5846ec826522050001db0e11",
  "created" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "id" : "5846ed076522050001db0e12",
  "updated" : "2016-12-06T16:53:27Z",
  "name" : "environment sensor interface"
}
```
Verwenden Sie in diesem Szenario die Anwendungsschnittstellen-ID *5846ed076522050001db0e12*, die in der Antwort auf die POST-Methode zurückgegeben wird, um Ihre Anwendungsschnittstelle zu Ihrem Gerätetyp hinzuzufügen. Diese ID wird auch verwendet, um ein eingehendes Geräteereignis einer Eigenschaft zuzuordnen, die von der Anwendungsschnittstelle definiert wird.

## Schritt 10: Anwendungsschnittstelle zu einem Gerätetyp hinzufügen
{: #step10}

Verwenden Sie die folgende API, um eine Anwendungsschnittstelle zu einem Gerätetyp hinzuzufügen:

```
POST /device/types/{typeId}/applicationinterfaces
```

Folgende Parameter sind erforderlich:  

Parameter	|	Beschreibung
------	|	-----
id	|	Die für die Anwendungsschnittstelle erstellte ID.
name	|	Der Name des Gerätetyps.
schemaId	|	Die für die Anwendungsschnittstellenressource erstellte ID.
refs/schema	|	Der Pfad zur Anwendungsschnittstellenressource. Für gewöhnlich: /schemas/*schemaId*


Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

Im vorliegenden Szenario ist die Anwendungsschnittstelle dem Gerätetyp *EnvSensor1* und dem Gerätetyp *EnvSensor2* zugeordnet.

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Hinzufügen der Anwendungsschnittstelle *5846ed076522050001db0e12*, die auf die Anwendungsschema-ID *5846ec826522050001db0e11* verweist, zu dem Gerätetyp *EnvSensor1*:

```
curl --request POST \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/applicationinterfaces \
--header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
--header 'content-type: application/json' \
--data '{"createdBy" : "a-8x7nmj-9iqt56kfil", \
          "refs" : {
              "schema" : "/schemas/5846ec826522050001db0e11"
          },
          "schemaId" : "5846ec826522050001db0e11", "created" : "2016-12-06T16:53:27Z", \
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface”
        }'
```

Das folgende Beispiel zeigt eine Antwort auf die POST-Methode:

```
{
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "updated" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "name" : "environment sensor interface",
  "created" : "2016-12-06T16:53:27Z",
  "id" : "5846ed076522050001db0e12",
  "schemaId" : "5846ec826522050001db0e11"
}
```

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Hinzufügen der Anwendungsschnittstelle *5846ed076522050001db0e12*, die der Anwendungsschema-ID *5846ec826522050001db0e11* zugeordnet ist, zu dem Gerätetyp *EnvSensor2*:

```
curl --request POST \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/applicationinterfaces \
--header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
--header 'content-type: application/json' \
--data '{"createdBy" : "a-8x7nmj-9iqt56kfil", \
          "refs" : {
              "schema" : "/schemas/5846ec826522050001db0e11"
          },
          "schemaId" : "5846ec826522050001db0e11", "created" : "2016-12-06T16:53:27Z", \
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface”
        }'
```


Das folgende Beispiel zeigt eine Antwort auf die POST-Methode:

```
{
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "updated" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "name" : "environment sensor interface",
  "created" : "2016-12-06T16:53:27Z",
  "id" : "5846ed076522050001db0e12",
  "schemaId" : "5846ec826522050001db0e11"
}
```

## Schritt 11: Zuordnungen definieren, um Eigenschaften im eingehenden Ereignis zu Eigenschaften in der Anwendungsschnittstelle zuzuordnen
{: #step11}

Verwenden Sie die folgende API, um Ereignisse zuzuordnen:

```
POST /device/types/{typeId}/mappings
```

Folgende Parameter sind erforderlich:  

Parameter	|	Beschreibung
------	|	-----
applicationInterfaceId	|	Die für die Anwendungsschnittstelle erstellte ID.
propertyMappings	|	Eine gültige JSON-Struktur, die für die Anwendungsschnittstelle definierte Eigenschaften zu Eigenschaften der Ereignisnutzdaten des Geräts zuordnet. Siehe folgende Beispiele.


Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

In diesem Szenario werden Zuordnungen für den Gerätetyp *EnvSensor1* definiert, um die Eigenschaft **t** im eingehenden Ereignis *tevt* der Eigenschaft **temperature** in der Anwendungsschnittstelle zuzuordnen. Außerdem werden Zuordnungen für den Gerätetyp *EnvSensor2* definiert, um die Eigenschaft **temp** im eingehenden Ereignis *tempevt* der Eigenschaft **temperature** in der Anwendungsschnittstelle zuzuordnen.

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Hinzufügen einer Zuordnung zum Gerätetyp *EnvSensor1*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/mappings \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"applicationInterfaceId" : "5846ed076522050001db0e12","propertyMappings" : {
              "tevt" : {
                  "temperature" : "$event.t"
              }
            }
          }'
```

**Wichtig:** Stellen Sie für Ereignisnutzdaten für strukturiertes [JSON ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://json-schema.org/){:new_window} sicher, dass der Eintrag "$event.*property*" der JSON-Struktur Ihrer Eigenschaften entspricht. Wenn die Nutzdaten beispielsweise `{"d":{"t":<temp>}}` lauten, verwenden Sie `$event.d.t`.

Geben Sie die Anwendungsschnittstellen-ID *5846ed076522050001db0e12* an, die in der Antwort auf die POST-Methode zum Erstellen der Anwendungsschnittstelle und des Gerätetyps *EnvSensor1* zurückgegeben wurde.

Das folgende Beispiel zeigt eine Antwort auf die POST-Methode:

```
{
  "propertyMappings" : {
      "tevt" : {
       "temperature" : "$event.t"
    }
  },
  "applicationInterfaceId" : "5846ed076522050001db0e12"
}
```
Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Hinzufügen einer Zuordnung zum Gerätetyp *EnvSensor2*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/mappings \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"applicationInterfaceId" : "5846ed076522050001db0e12","propertyMappings" : {
              "tempevt" : {
                  "temperature" : "($event.temp - 32) / 1.8"
              }
            }
          }'
```

Geben Sie die Anwendungsschnittstellen-ID *5846ed076522050001db0e12* an, die in der Antwort auf die POST-Methode zum Erstellen der Anwendungsschnittstelle und des Gerätetyps *EnvSensor2* zurückgegeben wurde.
Durch eine Umwandlung wird der Messwert von Grad Fahrenheit in Grad Celsius geändert.


Das folgende Beispiel zeigt eine Antwort auf die POST-Methode:

```
{
  "propertyMappings" : {
    "tempevt" : {
      "temperature" : "($event.temp - 32) / 1.8"
    }
  },
  "applicationInterfaceId" : "5846ed076522050001db0e12"
}
```

## Schritt 12: Konfiguration implementieren
{: #step15}

Implementieren Sie die Konfiguration, die sich auf die Aktualisierung des Gerätestatus für die einzelne Gerätetypen bezieht. Diese Konfiguration enthält Ihre Schemas, Ereignistypen, physischen Schnittstellen, Anwendungsschnittstellen und Zuordnungen.

Verwenden Sie die folgende API, um Ihre Gerätetypkonfiguration zu implementieren:

```
PATCH /device/types/{typeId}
```

Folgende Parameter sind erforderlich:  

Parameter	|	Beschreibung
------	|	-----
typeId	|	Die Gerätetyp-ID.

Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

Im vorliegenden Szenario muss die Konfiguration für zwei Gerätetypen implementiert werden.

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Implementieren Ihrer Konfiguration für den Gerätety *EnvSensor1*:

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy-configuration"
          }'
```

Das folgende Beispiel zeigt eine Antwort auf die PATCH-Methode:

```
{
 "message": "CUDRS0520I: State update configuration for device type 'EnvSensor1' has been successfully submitted for deployment",
  "details": {
    "id": "CUDRS0520I",
    "properties": ["EnvSensor1"]
  },
 "failures": []
}
```

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Implementieren Ihrer Konfiguration für den Gerätetyp *EnvSensor2*:

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
          }'
```

Das folgende Beispiel zeigt eine Antwort auf die PATCH-Methode:

```
{
 "message": "CUDRS0520I: State update configuration for device type 'EnvSensor2' has been successfully submitted for deployment",
  "details": {
    "id": "CUDRS0520I",
    "properties": ["EnvSensor2"]
  },
 "failures": []
}
```

## Schritt 13: Ein eingehendes Geräteereignis publizieren
{: #step12}

Publizieren Sie ein Temperaturereignis von *Temperatursensor 1* an das Topic `iot-2/evt/tevt/fmt/json` und ein Temperaturereignis von *Temperatursensor 2* an das Topic `iot-2/evt/tempevt/fmt/json`.

Informationen zum Publizieren eines eingehenden Ereignisses von einem Gerät finden Sie in [MQTT-Konnektivität für Anwendungen](../applications/mqtt.html#publishing_device_events).


## Schritt 14: Überprüfen, ob der Gerätestatus geändert wird
{: #step13}

Verwenden Sie die folgende API, um den Gerätestatus zu prüfen:
```
GET /device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
```

Folgende Parameter sind erforderlich:  

Parameter	|	Beschreibung
------	|	-----
typeId	|	Die Gerätetyp-ID.
deviceId	|	Die Geräte-ID.
applicationInterfaceId	|	Die für die Anwendungsschnittstelle erstellte ID.

Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Abrufen des aktuellen Status von *Temperatursensor 1* durch Verweisen auf die ID der erstellten Anwendungsschnittstelle.
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/devices/TemperatureSensor1/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

Die Anwendungsschnittstellen-ID *5846ed076522050001db0e12* wird in der GET-Methode verwendet. Diese ID wird in der Antwort auf die POST-Methode zurückgegeben, die zum Erstellen der Anwendungsschnittstelle verwendet wurde.
Das folgende Beispiel zeigt eine Antwort auf die GET-Methode:
```
{
  "temperature":34.5
}
```
Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Abrufen des aktuellen Status von *Temperatursensor 2* durch Verweisen auf die ID der erstellten Anwendungsschnittstelle.
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/devices/TemperatureSensor2/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

Die Anwendungsschnittstellen-ID *5846ed076522050001db0e12* wird in der GET-Methode verwendet. Diese ID wird in der Antwort auf die POST-Methode zurückgegeben, die zum Erstellen der Anwendungsschnittstelle verwendet wurde.
Das folgende Beispiel zeigt eine Antwort auf die GET-Methode:
```
{
  "temperature":22.5
}
```
Beachten Sie, dass der Temperaturmesswert in Grad Celsius zurückgegeben wird und nicht in Grad Fahrenheit.

Ihre Anwendung kann diese normalisierten Daten nutzen, ohne über eine Konfiguration zum Erkennen oder Umwandeln der verschiedenen Temperaturmaßeinheiten zu verfügen.


**Hinweis:** Verwenden Sie die folgende API, um die aktuell implementierte Konfiguration abzurufen:

```
GET /device/types/<typeId>/deployedconfiguration
```
Verwenden Sie diese API, um die Konfiguration abzurufen, die implementiert wurde, als die PATCH-Bereitstellungsoperation zum letzten Mal erfolgreich durchgeführt wurde. Um die Konfiguration für eine Ressource abzurufen, die zwar geändert, aber nicht implementiert wird, verwenden Sie die reguläre GET-Methode, die der abzufragenden Ressource zugeordnet ist.

Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}} HTTP-REST-API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Abrufen der aktuell implementierten Konfiguration:
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/deployedconfiguration \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```
Das folgende Beispiel zeigt eine Antwort auf die GET-Methode:

```
{
    "schemas": [
        {
          "name" : “tEventSchema",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "contentType" : "application/octet-stream",
  "updated" : "2016-12-06T14:38:52Z",
  "schemaFileName" : "tEventSchema.json",
  "created" : "2016-12-06T14:38:52Z",
  "id" : "5846cd7c6522050001db0e0d",
  "refs" : {
              "content" : "/schemas/5846cd7c6522050001db0e0d/content"
          },
          "schemaType" : "json-schema",
          "updatedBy" : "a-8x7nmj-9iqt56kfil",
          "content": "ew0KICAiJHNjaGVtYSI6ICJodHRwOi8vanNvbi1zY2hlbWEub3JnL2RyYWZ0LTA0L3NjaGVtYSMiLA0KICAidHlwZSIgOiAib2JqZWN0IiwNCiAgInRpdGxlIiA6ICJFbnZTZW5zb3IxIHRFdmVudCBTY2hlbWEiLA0KICAiZGVzY3JpcHRpb24iIDog4oCcZGVmaW5lcyB0aGUgc3RydWN0dXJlIG9mIGEgdGVtcGVyYXR1cmUgZXZlbnQgaW4gZGVncmVlcyBDZWxzaXVzIiwNCiAgInByb3BlcnRpZXMiIDogew0KICAgICJ0IiA6IHsNCiAgICAgICJkZXNjcmlwdGlvbiIgOiAidGVtcGVyYXR1cmUgaW4gZGVncmVlcyBDZWxzaXVzIiwNCiAgICAgICJ0eXBlIiA6ICJudW1iZXIiLA0KICAgICAgIm1pbmltdW0iIDogLTI3My4xNSwNCiAgICAgICJkZWZhdWx0IiA6IDAuMA0KICAgIH0NCiAgfSwNCiAgInJlcXVpcmVkIiA6IFsidCJdDQp9"
        }
    ],
    "eventTypes": [
        {
          "updated" : "2016-12-06T14:53:49Z",
  "schemaId" : "5846cd7c6522050001db0e0d",
  "refs" : {
            "schema" : "/schemas/5846cd7c6522050001db0e0d"
          },
  "name" : "tEvent",
  "created" : "2016-12-06T14:53:49Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "id" : "5846d0fd6522050001db0e0f",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
        },
        {
          "createdBy" : "a-8x7nmj-9iqt56kfil",
  "schemaId" : "5846cee36522050001db0e0e",
  "created" : "2016-12-06T15:00:20Z",
  "id" : "5846d2846522050001db0e10",
  "updated" : "2016-12-06T15:00:20Z",
  "name" : “tempEvent”,
  "refs" : {
            "schema" : "/schemas/5846cee36522050001db0e0e"
          },
          "updatedBy" : "a-8x7nmj-9iqt56kfil"
        }
    ],
    "physicalInterface": {
          "events":[
            {
                  "eventTypeId" : "5846d0fd6522050001db0e0f",
  "eventId" : "tevt"
            },
            {
                "eventTypeId" : "5846d2846522050001db0e10",
                "eventId" : “tempevt"
            }
          ],
        "updatedBy" : "a-8x7nmj-9iqt56kfil",
          "refs" : {
            "events" : "/physicalinterfaces/5847d1df6522050001db0e1a/events"
          },
  "id" : "5847d1df6522050001db0e1a",
  "name" : "Env sensor physical interface 1",
  "created" : "2016-12-07T09:09:51Z",
  "updated" : "2016-12-07T09:09:51Z",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
    },
    "applicationInterfaces": [
        {
          "createdBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
              "schema" : "/schemas/5846ec826522050001db0e11"
          },
          "schemaId" : "5846ec826522050001db0e11",
          "created" : "2016-12-06T16:53:27Z",
          "updatedBy" : "a-8x7nmj-9iqt56kfil",
          "id" : "5846ed076522050001db0e12",
          "updated" : "2016-12-06T16:53:27Z",
          "name" : "environment sensor interface"
        }
    ],
    "mappings": [
        {
          "propertyMappings" : {
            "tevt" : {
               "temperature" : "$event.t"
            },
            "tempevt" : {
                  "temperature" : "($event.temp - 32) / 1.8"
    }
          },
          "applicationInterfaceId" : "5846ed076522050001db0e12"
        }
    ]
}
```
