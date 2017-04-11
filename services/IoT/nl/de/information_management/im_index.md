---

copyright:
years: 2016, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gerätedaten mithilfe von Schnittstellen zuordnen (Beta)
{: #im_index}

Mit der Funktion für Schnittstellenzuordnung in {{site.data.keyword.iot_full}} können Sie eingehende und ausgehende Gerätedaten organisieren und integrieren.
{:shortdesc}

**Wichtig:** Die Funktion für Schnittstellenzuordnung ist derzeit nur als Betaversion verfügbar. Vor der endgültigen Freigabe enthalten Betaversionen möglicherweise Änderungen, die mit der aktuellen Version nicht kompatibel sind. Es wird dringend empfohlen, Betafunktionen nicht in Produktionsanwendungen einzusetzen, bis die endgültige Freigabe erfolgt ist. Um zusätzliche Informationen zu erhalten und Feedback zu dieser Betaversion zu geben, [registrieren Sie sich für das IM Beta-Programm ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/software/support/trial/cst/forms/nomination.wss?id=7050){: new_window} und teilen Sie uns Ihre Meinung mit.

## Übersicht
{: #overview}

Sie können die Funktion für Schnittstellenzuordnung verwenden, um Schnittstellen für Ihre Anwendungen zu entwickeln. Möglicherweise möchten Sie verschiedene Typen, Marken oder Modelle von Geräten oder Sensoren mit {{site.data.keyword.iot_short_notm}} verbinden, die Daten in verschiedenen Formaten publizieren. Mit der Funktion für Schnittstellenzuordnung können Sie eingehende Daten normalisieren und Ihre Anwendungen vereinfachen, indem Sie sie von der Komplexität der Verbindungsvorgänge für bestimmte Geräte entkoppeln.

Angenommen, Sie verwenden zwei Temperatursensoren. Der eine Sensor misst die Temperatur in Grad Celsius und der andere Sensor misst die Temperatur in Grad Fahrenheit.

![Zuordnung zwischen Temperatursensorgeräten und einer Anwendung in {{site.data.keyword.iot_short_notm}}.](images/Information "Zuordnung zwischen Temperatursensorgeräten und einer Anwendung in {{site.data.keyword.iot_short_notm}}")

Der Temperatursensor 1 meldet einen Temperaturmesswert von `{ "t" : 34.5 }` an {{site.data.keyword.iot_short_notm}}. Dieser Temperaturmesswert ist in Grad Celsius angegeben. Der Temperatursensor 2 meldet einen Temperaturmesswert von `{ "temp" : 72.55 }` an {{site.data.keyword.iot_short_notm}}. Dieser Temperatursensortyp gibt einen Messwert in Grad Fahrenheit aus. Die Temperaturmesswerte werden als separate Ereignisse an {{site.data.keyword.iot_short_notm}} gemeldet.

Mithilfe der Funktion für Schnittstellenzuordnung können Sie diese Messwerte für die Verarbeitung in ein konsistentes Format bringen. Sie müssen in Ihre Anwendung keinen Code einfügen, der verschiedene Temperaturmaßeinheiten erkennt und umwandelt. Die Anwendung empfängt eine einzige normalisierte Ansicht und kann sofort die Verbindung zu **temperature** herstellen, anstatt die Verbindung zu **t** und **temp** herzustellen.

## Datenfluss zwischen Geräten und Anwendungen
{: #mapping}

Das folgende Ablaufdiagramm zeigt, wie verschiedene Ressourcen in der Funktion für Schnittstellenzuordnung verwendet werden:

![Der Datenfluss zwischen einem Gerät und einer Anwendung in {{site.data.keyword.iot_short_notm}}.](images/Information "Der Datenfluss zwischen einem Gerät und einer Anwendung in {{site.data.keyword.iot_short_notm}}")

Das folgende Diagramm veranschaulicht die Verwendung von Schemas in diesem Datenfluss:

![Der Datenfluss zwischen einem Gerät und einer Anwendung in {{site.data.keyword.iot_short_notm}}.](images/Information "Der Datenfluss zwischen einem Gerät und einer Anwendung in {{site.data.keyword.iot_short_notm}}")

Zum Definieren und Überprüfen des Formats von eingehenden Ereignissen und des [Gerätestatus](#key_concepts) werden JSON-Schemas verwendet. Weitere Informationen zu diesen Schemas finden Sie in [Schemas](#resources).

## Wichtige Konzepte
{: #key_concepts}

Die Funktion für Schnittstellenzuordnung erweitert das aktuelle Konzept für [Gerätetyp](#resources) durch das Hinzufügen einer physischen Schnittstellenressource und einer Anwendungsschnittstellenressource, um die Steuerung des Datenflusses in {{site.data.keyword.iot_short_notm}} zu verbessern.

Das folgende Diagramm veranschaulicht die logische Zuordnung zwischen Geräten und Anwendungen in {{site.data.keyword.iot_short_notm}} unter Verwendung von [Ressourcen](#resources):

![Die logische Zuordnung zwischen einem Gerät und einer Anwendung in {{site.data.keyword.iot_short_notm}}.](images/im_mapping.svg "Die logische Zuordnung zwischen einem Gerät und einer Anwendung in {{site.data.keyword.iot_short_notm}}")

Die Schnittstellenzuordnung bezieht sich auf das Konzept des Gerätestatus. Der Gerätestatus besteht aus einer Gruppe von Eigenschaften, die von der Anwendungsschnittstelle definiert werden. Die letzten Werte dieser Eigenschaften werden in {{site.data.keyword.iot_short_notm}} gespeichert und der Anwendung auf Anfrage mithilfe einer HTTP-API zur Verfügung gestellt.

Um Daten aus eingehenden Ereignissen zu verarbeiten und Eigenschaften in dem eingehenden Ereignis den Eigenschaften in der Anwendungsschnittstelle zuzuordnen, müssen die folgenden Informationen konfiguriert werden:

- Die Struktur für ein oder mehrere eingehende Ereignisse. Diese Informationen werden im Ereignisschema definiert.  Jedes Ereignisschema definiert die Struktur für ein eingehenden Ereignis und ist einem Ereignistyp zugeordnet. Die physische Schnittstelle ordnet einen oder mehrere Ereignistypen einer Gruppe zu.

    Die Struktur und das Format der Daten, die in einem eingehenden Geräteereignis enthalten sind, wird durch eine Ereignisschemadatei definiert, die ein JSON-Schemaformat aufweist. Zum Hochladen der Ereignisschemadatei in {{site.data.keyword.iot_short_notm}} können Sie eine POST-Methode verwenden, die eine benannte Schemaressource erstellt. In der Betaversion müssen alle eingehenden Ereignisse im JSON-Format vorliegen.

- Die Struktur des gewünschten Gerätestatus. Diese Informationen werden im Schnittstellenschema definiert.

    Der Gerätestatus ist eine Darstellung der Datenstruktur und der Daten, die Ihre Anwendung als Daten von dem Gerät empfangen soll. Die im Gerätestatus gespeicherten Eigenschaftswerte werden als Reaktion auf ein eingehendes Geräteereignis aktualisiert. Die neuesten Gerätestatuswerte werden einer Anwendung auf Anforderung mithilfe einer HTTP-API bereitgestellt.

- Informationen zum Zuordnen eingehender Ereignisse zu dem bevorzugten Gerätestatus. Diese Informationen werden in Zuordnungen definiert.

    Damit die in den Eigenschaften eines eingehenden Ereignisses enthaltenen Daten den entsprechenden Eigenschaften in der Anwendungsschnittstelle zugeordnet werden können, müssen Sie eine Zuordnung erstellen. Diese Zuordnung beschreibt, wie die in einer bestimmten Anwendungsschnittstelle definierten Eigenschaften als Reaktion auf ein eingehendes Ereignis von einem Gerät aktualisiert werden.


## Ressourcen
{: #resources}

Die in den vorherigen Diagrammen dargestellten Ressourcen können mithilfe von REST-APIs verwaltet werden. Informationen zu den REST-APIs finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}}-HTTP-REST-API ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html){: new_window}.

Ressource                        | Beschreibung       
------------- | ------------- | -------------  
Schemas                         | Mithilfe von JSON-Schemas wird die Struktur eingehender Ereignisse definiert, die von Geräten in {{site.data.keyword.iot_short_notm}} publiziert werden, sowie der gewünschte Gerätestatus. Weitere Informationen zum JSON-Schema finden Sie in [JSON-Schema ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://json-schema.org/){: new_window}. In der Schnittstellenzuordnung werden zwei JSON-Schemas referenziert: Ereignisschemas und Anwendungsschnittstellenschemas. Mithilfe von Ereignisschemas wird die Struktur der Ereignisse definiert, die von einem Gerät in {{site.data.keyword.iot_short_notm}} publiziert werden. Anwendungsschnittstellenschemas werden von der Anwendungsschnittstelle referenziert und sie definieren die Struktur des [Gerätestatus](#key_concepts), der in {{site.data.keyword.iot_short_notm}} gespeichert wird.
Ereignistyp                         | Sie müssen innerhalb Ihrer Organisation einen Ereignistyp erstellen, damit {{site.data.keyword.iot_short_notm}} die in einem bestimmten Ereignis enthaltenen Daten verarbeiten kann. Alle Ereignistypen müssen auf ein Ereignisschema verweisen. In der Beataversion müssen alle eingehenden Ereignisse im JSON-Format vorliegen.   
Physische Schnittstelle                         | Die physische Schnittstelle kann mindestens einem Ereignistyp zugeordnet werden und sie definiert, welche Ereignisse einem Gerätetyp zugeordnet werden.  
Gerätetyp                         | Jedem Gerät, das mit Watson IoT Platform verbunden ist, wird ein Gerätetyp zugeordnet. Gerätetypen sind Gruppen von Geräten, die gemeinsame Merkmale haben oder gleiches Verhalten zeigen. Bei der Schnittstellenzuordnung wird der Gerätetyp um eine physische Schnittstelle für ein Gerät und eine Anwendungsschnittstelle erweitert, die verwendet werden kann, um den Gerätestatus abzurufen. Für einen Gerätetyp können mehrere Anwendungsschnittstellen konfiguriert werden. Weitere Informationen zu Gerätetypen finden Sie im Abschnitt über Kennungen und Gerätetypen in [Gerätemodell](../reference/device_model.html#id_and_device_types).
Anwendungsschnittstelle                         | Die Anwendungsschnittstelle muss auf ein Anwendungsschnittstellenschema verweisen. In Ihrer Anwendungsschnittstelle können Sie die Struktur der Daten definieren, die als Gerätestatus gespeichert werden. Der Gerätestatus ist eine Darstellung der Datenstruktur und der Daten, die eine Anwendung als Daten von dem Gerät empfangen soll. Eine Gerätetyp muss mindestens eine Anwendungsschnittstelle zugeordnet werden, damit Zuordnungen definiert werden können.
Zuordnungen                         | Zuordnungen definieren, wie zugehörige Eigenschaften für eingehende Ereignisse den Eigenschaften zugeordnet werden, die in einer bestimmten Anwendungsschnittstelle definiert sind. Eine Zuordnung muss die ID der Anwendungsschnittstelle angeben, auf die sie angewendet wird, und die betreffende Anwendungsschnittstelle muss dem Gerätetyp zugeordnet sein, dem die Zuordnung hinzugefügt wird.


## Allgemeiner Workflow
{: #workflow}



### Informationen zu diesem Vorgang

Die folgenden Schritte sollen Sie beim Konfigurieren der erforderlichen Ressourcen unterstützen, die zum Zuordnen Ihrer Gerätedaten mithilfe von Schnittstellen erforderlich sind.

Details zur API finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}}-HTTP-REST-API ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html){: new_window}.
Ausführlichere Informationen zu den einzelnen Schritten finden Sie im [Beispielszenario](#scenario) oder in den Links zum Aufrufen bestimmter Schritte im Beispielszenario.

### Konfigurieren Sie Ihre Umgebung für die Verwendung von Schnittstellen zum Zuordnen von Gerätedaten

1.  Fügen Sie bei Bedarf einen Gerätetyp und ein Gerät hinzu

  1. Erstellen Sie einen Gerätetyp unter Verwendung der POST-Methode der REST-API mit dem folgenden URI:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types
      ```
  2.  Fügen Sie ein Gerät hinzu, falls erforderlich.  
Weitere Informationen zum Hinzufügen eines Gerätetyps und eines Geräts finden Sie in [Geräte verbinden](../iotplatform_task.html#devices).

2. Erstellen Sie eine physische Schnittstelle

  1. [Erstellen Sie eine Ereignisschemadatei](#step1). Bei der Ereignisschemadatei handelt es sich um eine lokale .JSON-Datei, in der die Struktur und das Format eines eingehenden Ereignisses definiert ist.

  2. [Erstellen Sie eine Ereignisschemaressource für Ihren Ereignistyp](#step2) unter Verwendung der POST-Methode der REST-API mit dem folgenden URI:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
      ```  

  3. [Erstellen Sie einen Ereignistyp, der auf das Ereignisschema verweist](#step3), unter Verwendung der POST-Methode der REST-API mit dem folgenden URI:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/event/types
      ```
      Fügen Sie den Ereignistyp Ihrem Ereignisschema hinzu, indem Sie die Schemakennung verwenden, die als Antwort auf die zum Erstellen der Ereignisschemaressource verwendeten POST-Methode zurückgegeben wurde.

  4. [Erstellen Sie eine physische Schnittstelle](#step7) unter Verwendung der POST-Methode der REST-API mit dem folgenden URI:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces
        ```

   5. [Fügen Sie den Ereignistyp zur physischen Schnittstelle hinzu](#step8), indem Sie die POST-Methode der REST-API mit dem folgenden URI verwenden:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/{physicalInterfaceId}/events
        ```

       Fügen Sie unter Verwendung der Ereigniskennung *eventId* aus dem Abschnitt und der Ereignistypkennung *eventTypeId*, die als Antwort auf die POST-Methode zum Erstellen des Ereignistyps zurückgegeben wurde, den Ereignistyp zu Ihrer physischen Schnittstelle hinzu.       

3. Fügen Sie Ihre physische Schnittstelle zu Ihrem Gerätetyp hinzu       

      [Aktualisieren Sie den Gerätetyp zum Verbinden der physischen Schnittstelle](#step9) unter Verwendung der PUT-Methode der REST-API mit dem folgenden URI:
     ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
     ```

4. Erstellen Sie eine Anwendungsschnittstelle

  1. [Erstellen Sie eine Schemadatei für die Anwendungsschnittstelle](#step4). Bei einer Anwendungsschnittstellenschemadatei handelt es sich um eine lokale .JSON-Datei, die den Gerätestatus definiert.

  2. [Erstellen Sie eine Schemaressource für die Anwendungsschnittstelle](#step5) unter Verwendung der POST-Methode der REST-API mit dem folgenden URI:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
        ```     

  3. [Erstellen Sie eine Anwendungsschnittstelle, die auf ein Anwendungsschnittstellenschema verweist](#step6), unter Verwendung der POST-Methode der REST-API mit dem folgenden URI:
         ```
         https://**orgId**.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces
         ```  

        Die Anwendungsschnittstelle verweist mithilfe der Schemakennung, die als Antwort auf die POST-Methode zum Erstellen der Schemaressource für die Anwendungsschnittstelle zurückgegeben wurde, auf das Anwendungsschnittstellenschema.

  4. [Fügen Sie die Anwendungsschnittstelle zu einem Gerätetyp hinzu](#step10), indem Sie die POST-Methode der REST-API mit dem folgenden URI verwenden:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/types/{typeId}/applicationinterfaces
        ```

        Fügen Sie Ihre Anwendungsschnittstelle mithilfe der Antwort auf die POST-Methode, die zum Erstellen der Anwendungsschnittstelle verwendet wurde, zu Ihrem Gerätetyp hinzu.

5. Definieren Sie die Zuordnungen für den Gerätetyp

  [Definieren Sie Zuordnungen, um Eigenschaften des eingehenden Ereignisses den Eigenschaften der Anwendungsschnittstelle zuzuordnen](#step11), indem Sie die POST-Methode der REST-API mit dem folgenden URI verwenden:       
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/mappings/{applicationInterfaceId}
      ```

6. Stellen Sie die zugehörige Konfiguration für Ihren Gerätetyp bereit

  [Stellen Sie die Konfiguration](#step15) in {{site.data.keyword.iot_short_notm}} unter Verwendung der PATCH-Methode der REST-API mit dem folgenden URI bereit:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
      ```

7. Überprüfen Sie, dass die Ereignisse des zugeordneten Geräts an die Anwendungsschnittstelle publiziert werden

  1. [Publizieren Sie ein eingehendes Geräteereignis](#step12).

  2. [Überprüfen Sie, dass der Gerätestatus geändert wird](#step13), indem Sie die GET-Methode der REST-API mit dem folgenden URI verwenden:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
        ```

## Beispielszenario
{: #scenario}

Erstellen Sie mithilfe der folgenden Informationen ein Szenario, in dem Ereignisse von zwei Temperatursensoren an {{site.data.keyword.iot_short_notm}} publiziert werden. Ein Sensor misst die Temperatur in Grad Celsius. Der andere Sensor misst die Temperatur in Grad Fahrenheit. Die gemessenen Werte werden einem einzigen Temperaturmesswert in Grad Celsius zugeordnet. Wenn diese Geräte einen neuen Temperaturmesswert ausgeben, wird der Wert der Eigenschaft geändert, die dem Gerätestatus zugeordnet ist.

### Voraussetzungen

Sie müssen über eine {{site.data.keyword.iot_short_notm}}-Organisationsinstanz und über einen API-Schlüssel oder ein Token für die Organisation verfügen. Weitere Informationen zu API-Schlüsseln und Token finden Sie in [HTTP-REST-API für Anwendungen](../applications/api.html#authentication).

### Informationen zu diesem Szenario

In diesem Szenario werden zwei Geräte konfiguriert.

Ein Gerät trägt den Namen *TemperatureSensor1*. Dieses Gerät publiziert Temperaturereignisse, die in Grad Celsius gemessen werden. Das Temperaturereignis wird im Topic `iot-2/evt/tevt/fmt/json` publiziert und enthält die folgenden Beispielnutzdaten:
```
{
  "t" : 34.5
}
```

**Hinweis:** Die Ereignis-ID lautet *tevt*. Diese ID ist erforderlich, wenn Sie ein Temperaturereignis dieses Typs zur physischen Schnittstelle hinzufügen und Zuordnungen definieren, um eine zugehörige Eigenschaft für ein eingehendes Ereignis dieses Typs einer Eigenschaft in Ihrer Anwendungsschnittstelle zuzuordnen. Im vorliegenden Szenario trägt die in der Anwendungsschnittstelle definierte Eigenschaft den Namen **temperature**.

Das andere Gerät trägt den Namen *TemperatureSensor2*. Dieses Gerät publiziert Temperaturereignisse, die in Grad Fahrenheit gemessen werden. Das Temperaturereignis wird im Topic `iot-2/evt/tempevt/fmt/json` publiziert und enthält die folgenden Beispielnutzdaten:
```
{
  "temp" : 72.55
}
```

**Hinweis:** Die Ereignis-ID lautet *tempevt*. Diese ID ist erforderlich, wenn Sie ein Temperaturereignis dieses Typs zur physischen Schnittstelle hinzufügen und Zuordnungen definieren, um eine zugehörige Eigenschaft für ein eingehendes Ereignis dieses Typs einer Eigenschaft in Ihrer Anwendungsschnittstelle zuzuordnen. Im vorliegenden Szenario trägt die in der Anwendungsschnittstelle definierte Eigenschaft den Namen **temperature**.

Außerdem wird eine Anwendungsschnittstelle konfiguriert. Diese Anwendungsschnittstelle stellt den Status für Geräte dieses Typs in der folgenden Struktur dar:
```
{
  "temperature" : <aktueller Temperaturwert in Celsius>
  }
```
Mithilfe dieser Konfiguration können Sie Ihre Anwendung so konfigurieren, dass der zugeordnete Wert für **temperature** verarbeitet wird, anstatt den zugeordneten Wert für **t** zu verarbeiten und den zugeordneten Wert für **temp** erst nach Umwandlung in Grad Celsius zu verarbeiten.

## Schritte

Verwenden Sie die folgenden Informationen, um das Beispielszenario mithilfe von Schnittstellen zu konfigurieren.

### Fügen Sie bei Bedarf einen Gerätetyp und ein Gerät hinzu
{: #step14}

Im vorliegenden Szenario werden zwei Gerätetypen und zwei Geräteinstanzen angenommen. Die Geräteinstanz *TemperatureSensor1* ist dem Gerätetyp *EnvSensor1* zugeordnet. Die Geräteinstanz *TemperatureSensor2* ist dem Gerätetyp *EnvSensor2* zugeordnet.

Informationen zur Verwendung von HTTP-APIs zum Hinzufügen eines Gerätetyps finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}}-HTTP-REST-API ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html#!/Device_Type_Configuration){: new_window}.

### Erstellen Sie eine Ereignisschemadatei
{: #step1}

Erstellen Sie für das vorliegende Szenario zwei Ereignisschemadateien, um die Struktur der eingehenden Temperaturereignisse zu definieren.

Das folgende Beispiel zeigt das Erstellen einer Schemadatei mit dem Namen *tEventSchema.json*. In dieser Datei wird die Struktur eines eingehenden Ereignisses von einem Temperatursensor definiert, der die Temperatur in Grad Celsius misst:

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor1 tEvent Schema",
  "description" : "defines the structure of a temperatur event in degress Celsius",
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

Der Schemadateiname *tEventSchema* wird verwendet, wenn Sie eine Ereignisschemaressource für Ihren Ereignistyp erstellen.

Das folgende Beispiel zeigt das Erstellen einer Schemadatei mit dem Namen *tempEventSchema.json*. In dieser Datei wird die Struktur eines eingehenden Ereignisses von einem Temperatursensor definiert, der die Temperatur in Grad Fahrenheit misst.

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor2 tempEvent Schema",
  "description" : "definies the structure of a temperature event in degress Fahrenheit",
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

### Erstellen Sie eine Ereignisschemaressource für Ihren Ereignistyp
{: #step2}

Verwenden Sie die folgende API, um eine Ereignisschemaressource zu erstellen:

```
POST /schemas
```
Weitere Details finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}}-HTTP-REST-API ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas){: new_window}.

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Erstellen der Ereignisschemaressource *tEventSchema.json*:

```
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
  "name" : "tEventSchema",
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
Die Schemakennung *5846cd7c6522050001db0e0d*, die als Antwort auf die POST-Methode zurückgegeben wird, ist erforderlich, wenn Sie ein Ereignisschema zu Ihrem Ereignistyp hinzufügen.

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
Die Schemakennung *5846cee36522050001db0e0e*, die als Antwort auf die POST-Methode zurückgegeben wird, ist erforderlich, wenn Sie ein Ereignisschema zu Ihrem Ereignistyp hinzufügen.

### Erstellen Sie einen Ereignistyp, der auf das Ereignisschema verweist
{: #step3}

Jeder Ereignistyp verwendet zum Verweisen auf das Ereignisschema, das im vorherigen Beispiel erstellt wurde, die in der Antwort auf die POST-Methode zum Erstellen der Ereignisschemaressource zurückgegebene Schemakennung.

Verwenden Sie die folgende API, um einen Ereignistyp zu erstellen:

```
POST /event/types
```

Weitere Details finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}}-HTTP-REST-API ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Event_Types){: new_window}.




Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Erstellen eines Ereignistyps für ein Temperaturereignis, das in Grad Celsius gemessen wird:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tEvent", "schemaId" : "5846cd7c6522050001db0e0d"}'
```

Die Schemakennung *5846cd7c6522050001db0e0d* wird verwendet, um das Ereignisschema zu dem Ereignistyp hinzuzufügen. Diese Kennung wurde als Antwort auf die POST-Methode zurückgegeben, die zum Erstellen der Ereignisschemaressource *tEventSchema.json* verwendet wurde.

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

Die Ereignistypkennung *5846d0fd6522050001db0e0f*, die als Antwort auf die POST-Methode zurückgegeben wird, wird verwendet, um einen Ereignistyp zu der physischen Schnittstelle hinzuzufügen.

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Erstellen eines Ereignistyps für ein Temperaturereignis, das in Grad Fahrenheit gemessen wird:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tempEvent", "schemaId" : "5846cee36522050001db0e0e"}'
```
Die Schemakennung *5846cee36522050001db0e0e* wird verwendet, um das Ereignisschema zu dem Ereignistyp hinzuzufügen. Diese Kennung wurde als Antwort auf die POST-Methode zurückgegeben, die zum Erstellen der Ereignisschemaressource *tempEventSchema.json* verwendet wurde.

Das folgende Beispiel zeigt eine Antwort auf die POST-Methode:

```
{
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "schemaId" : "5846cee36522050001db0e0e",
  "created" : "2016-12-06T15:00:20Z",
  "id" : "5846d2846522050001db0e10",
  "updated" : "2016-12-06T15:00:20Z",
  "name" : "tempEvent",
  "refs" : {
    "schema" : "/schemas/5846cee36522050001db0e0e"
  },
  "updatedBy" : "a-8x7nmj-9iqt56kfil"
}
```
Die Ereignistypkennung *5846d2846522050001db0e10*, die als Antwort auf die POST-Methode zurückgegeben wird, wird verwendet, um einen Ereignistyp zu der physischen Schnittstelle hinzuzufügen.

### Erstellen Sie eine physische Schnittstelle
{: #step7}

Verwenden Sie die folgende API, um eine physische Schnittstelle zu erstellen:

```
POST /physicalinterfaces
```
Weitere Details finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}}-HTTP-REST-API ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Physical_Interfaces){: new_window}.

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

Die in der Antwort zurückgegebene Kennung der physischen Schnittstelle (*5847d1df6522050001db0e1a*) wird in der URL der POST-Methode verwendet, die aufgerufen wird, um ein Temperaturereignis zur physischen Schnittstelle hinzuzufügen, das in Grad Celsius gemessen wird.

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

Die in der Antwort zurückgegebene Kennung der physischen Schnittstelle (*5847d1df6522050001db0e1b*), wird in der URL der POST-Methode verwendet, die aufgerufen wird, um ein Temperaturereignis zur physischen Schnittstelle hinzuzufügen, das in Grad Fahrenheit gemessen wird.   

### Fügen Sie den Ereignistyp zur physischen Schnittstelle hinzu
{: #step8}

Verwenden Sie die folgende API, um einen Ereignistyp zu Ihrer physischen Schnittstelle hinzuzufügen:

```
POST /physicalinterfaces/{physicalInterfaceId}/events
```
Weitere Details finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}}-HTTP-REST-API ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Physical_Interfaces){: new_window}.

Im vorliegenden Szenario werden die folgenden Ereignistypen zu den angegebenen physischen Schnittstellen hinzugefügt:
- Das Temperaturereignis in Grad Celsius (*tevt*) wird zur physischen Schnittstelle mit der Kennung *5847d1df6522050001db0e1a* unter Verwendung von *eventId* aus dem Topic und von *eventTypeId* aus der Erstellung der Ereignisschemaressource hinzugefügt.
- Das Temperaturereignis in Grad Fahrenheit (*tempevt*) wird zur physischen Schnittstelle mit der Kennung *5847d1df6522050001db0e1b* unter Verwendung von *eventId* aus dem Topic und von *eventTypeId* aus der Erstellung der Ereignisschemaressource hinzugefügt.


Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Hinzufügen des Temperaturereignisses *tevt* zur physischen Schnittstelle mit der Kennung *5847d1df6522050001db0e1a*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1a/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : "tevt", "eventTypeId" : "5846d0fd6522050001db0e0f"}'
```

Das folgende Beispiel zeigt eine Antwort auf die POST-Methode:

```
{
  "eventTypeId" : "5846d0fd6522050001db0e0f",
  "eventId" : "tevt"
}
```

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Hinzufügen des Temperaturereignisses *tempevt* zur physischen Schnittstelle mit der Kennung *5847d1df6522050001db0e1b*:

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
  "eventId" : "tempevt"
}
```

### Aktualisieren Sie den Gerätetyp zum Verbinden der physischen Schnittstelle
{: #step9}

Verwenden Sie die folgende API, um einen Gerätetyp zu aktualisieren:

```
PUT /device/types/{typeId}
```

Weitere Details finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}}-HTTP-REST-API ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types){: new_window}.



In diesem Szenario wird der Gerätetyp *EnvSensor1* zum Verbinden mit der physischen Schnittstelle *5847d1df6522050001db0e1a* und der Gerätetyp *EnvSensor2* zum Verbinden mit der physischen Schnittstelle *5847d1df6522050001db0e1b* aktualisiert.

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Aktualisieren des Gerätetyps *EnvSensor1*:

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an environment sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1a"}’
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
Die Gerätekennung *EnvSensor1* ist erforderlich, wenn Sie Ihre physische Schnittstelle und Ihre Anwenungsschnittstelle hinzufügen.

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Aktualisieren des Gerätetyps *EnvSensor2*:

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an env sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1b"}’
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
Die Gerätekennung *EnvSensor2* ist erforderlich, wenn Sie Ihre physische Schnittstelle und Ihre Anwendungsschnittstelle hinzufügen.



### Erstellen Sie eine Schemadatei für die Anwendungsschnittstelle
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

### Erstellen Sie eine Schemadatei für die Anwendungsschnittstelle
{: #step5}

Verwenden Sie die folgende API, um eine Anwendungsschnittstellenschemaressource zu erstellen:

```
POST /schemas
```
Weitere Details finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}}-HTTP-REST-API ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas){: new_window}.

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
Verwenden Sie die Schemakennung *5846ec826522050001db0e11*, die in der Antwort auf die POST-Methode zurückgegeben wird, um das Anwendungsschnittstellenschema zu der Anwendungsschnittstelle hinzuzufügen.

### Erstellen Sie eine Anwendungsschnittstelle, die auf ein Anwendungsschnittstellenschema verweist
{: #step6}

Verwenden Sie die folgende API, um eine Anwendungsschnittstelle zu erstellen:

```
POST /applicationinterfaces
```
Weitere Details finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}}-HTTP-REST-API ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Application_Interfaces){: new_window}.

Verwenden Sie in diesem Szenario die Schemakennung *5846ec826522050001db0e11*, die in der vorherigen Antwort zurückgegeben wurde, um das Anwendungsschnittstellenschema zu der Anwendungsschnittstelle hinzuzufügen.

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
Verwenden Sie in diesem Szenario die Anwendungsschnittstellenkennung *5846ed076522050001db0e12*, die in der Antwort auf die POST-Methode zurückgegeben wird, um Ihre Anwendungsschnittstelle zu Ihrem Gerätetyp hinzuzufügen. Diese Kennung wird auch verwendet, um ein eingehendes Geräteereignis einer Eigenschaft zuzuordnen, die von der Anwendungsschnittstelle definiert wird.

### Fügen Sie die Anwendungsschnittstelle zu einem Gerätetyp hinzu
{: #step10}

Verwenden Sie die folgende API, um eine Anwendungsschnittstelle zu einem Gerätetyp hinzuzufügen:

```
POST /device/types/{typeId}/applicationinterfaces
```
Weitere Details finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}}-HTTP-REST-API ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types){: new_window}.

Im vorliegenden Szenario ist die Anwendungsschnittstelle dem Gerätetyp *EnvSensor1* und dem Gerätetyp *EnvSensor2* zugeordnet.

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Hinzufügen der Anwendungsschnittstelle *5846ed076522050001db0e12*, die auf die Anwendungsschemakennung *5846ec826522050001db0e11* verweist, zu dem Gerätetyp *EnvSensor1*:

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
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface"
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

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Hinzufügen der Anwendungsschnittstelle *5846ed076522050001db0e12*, die der Anwendungsschemakennung *5846ec826522050001db0e11* zugeordnet ist, zu dem Gerätetyp *EnvSensor2*:

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
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface"
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

### Definieren Sie Zuordnungen, um Eigenschaften des eingehenden Ereignisses den Eigenschaften der Anwendungsschnittstelle zuzuordnen
{: #step11}

Verwenden Sie die folgende API, um Ereignisse zuzuordnen:

```
POST /device/types/{typeId}/mappings
```
Weitere Details finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}}-HTTP-REST-API ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types){: new_window}.

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

Geben Sie die Anwendungsschnittstellenkennung *5846ed076522050001db0e12* an, die in der Antwort auf die POST-Methode zum Erstellen der Anwendungsschnittstelle und des Gerätetyps *EnvSensor1* zurückgegeben wurde.

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

Geben Sie die Anwendungsschnittstellenkennung *5846ed076522050001db0e12* an, die in der Antwort auf die POST-Methode zum Erstellen der Anwendungsschnittstelle und des Gerätetyps *EnvSensor2* zurückgegeben wurde.
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

### Implementieren Sie die Konfiguration
{: #step15}

Implementieren Sie die Konfiguration der Gerätestatusaktualisierung für jeden Gerätetyp. Diese Konfiguration enthält Ihre Schemas, Ereignistypen, physischen Schnittstellen, Anwendungsschnittstellen und Zuordnungen.

Verwenden Sie die folgende API, um Ihre Gerätetypkonfiguration zu implementieren:

```
PATCH /device/types/{typeId}
```
Weitere Details finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}}-HTTP-REST-API ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types){: new_window}.

Im vorliegenden Szenario muss die Konfiguration für zwei Gerätetypen implementiert werden.

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Implementieren Ihrer Konfiguration für den Gerätety *EnvSensor1*:

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
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

### Publizieren Sie ein eingehendes Geräteereignis
{: #step12}

Publizieren Sie ein Temperaturereignis von *TemperatureSensor1* an das Topic `iot-2/evt/tevt/fmt/json` und ein Temperaturereignis von *TemperatureSensor2* an das Topic `iot-2/evt/tempevt/fmt/json`.

Informationen zum Publizieren eines eingehenden Ereignisses von einem Gerät finden Sie in [MQTT-Konnektivität für Anwendungen](../applications/mqtt.html#publishing_device_events).


### Überprüfen Sie, dass der Gerätestatus geändert wird
{: #step13}

Verwenden Sie die folgende API, um den Gerätestatus zu prüfen:
```
GET /device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
```
Weitere Details finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}}-HTTP-REST-API ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types){: new_window}.

Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Abrufen des aktuellen Status von *TemperatureSensor1* durch Verweisen auf die Kennung der erstellten Anwendungsschnittstelle.
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/devices/TemperatureSensor1/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

Die Anwendungsschnittstellenkennung *5846ed076522050001db0e12* wird in der GET-Methode verwendet. Diese Kennung wird in der Antwort auf die POST-Methode zurückgegeben, die zum Erstellen der Anwendungsschnittstelle verwendet wurde.
Das folgende Beispiel zeigt eine Antwort auf die GET-Methode:
```
{
  "temperature":34.5
}
```
Das folgende Beispiel zeigt die Verwendung von 'cURL' zum Abrufen des aktuellen Status von *TemperatureSensor2* durch Verweisen auf die Kennung der erstellten Anwendungsschnittstelle.
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/devices/TemperatureSensor2/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

Die Anwendungsschnittstellenkennung *5846ed076522050001db0e12* wird in der GET-Methode verwendet. Diese Kennung wird in der Antwort auf die POST-Methode zurückgegeben, die zum Erstellen der Anwendungsschnittstelle verwendet wurde.
Das folgende Beispiel zeigt eine Antwort auf die GET-Methode:
```
{
  "temperature":22.5
}
```
Beachten Sie, dass der Temperaturmesswert in Grad Celsius zurückgegeben wird und nicht in Grad Fahrenheit.

Ihre Anwendung kann diese normalisierten Daten nutzen, ohne über eine Konfiguration zum Erkennen oder Umwandeln der verschiedenen Temperaturmaßeinheiten zu verfügen.
