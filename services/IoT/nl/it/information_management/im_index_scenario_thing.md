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

# Scenario di interfaccia dell'applicazione 2 (Beta)
{: #scenario}

L'interfaccia dell'applicazione viene utilizzata in modo che non sia necessario che l'applicazione comprenda come sono configurati un dispositivo o un oggetto. Ad esempio, puoi misurare la temperatura di una stanza utilizzando un singolo dispositivo oppure puoi calcolare la temperatura della stanza prendendo la lettura media di diversi dispositivi. L'applicazione richiede informazioni sullo stato di una o più stanze, uno dei cui componenti è una proprietà di temperatura. Non importa il modo in cui viene calcolato il valore della temperatura ricevuto dall'applicazione.

In questo scenario, i sensori di temperatura e umidità pubblicano i dati ambientali che vengono raccolti in due sale riunioni. I dati dei sensori di temperatura e umidità sono associati separatamente a due interfacce dell'applicazione di tipo dispositivo, uno per il tipo dispositivo termometro e uno per il tipo dispositivo igrometro. Viene quindi creato un tipo oggetto denominato *RoomType*, insieme a due istanze oggetto stanza: *meetingroom1* e *meetingroom2*.

Questo scenario configura una composizione che include le interfacce dell'applicazione termometro e igrometro e che associa quindi i sensori ambientali corretti a ciascuna delle istanze stanza, ad esempio *temperatureSensor1* e *humiditySensor1* sono associate a *meetingroom1*.

## Prerequisiti
{: #pre_req}

Questo scenario sviluppa ulteriormente quanto fatto nel precedente [Scenario di interfaccia dell'applicazione 1](im_index_scenario).

Prima di continuare, assicurati di:
- Utilizzare la stessa istanza dell'organizzazione {{site.data.keyword.iot_short_notm}} e un token o una chiave API per tale organizzazione. Per ulteriori informazioni sui token e sulle chiavi API, consulta [API REST HTTP per le applicazioni](../applications/api.html#authentication).
- Aver creato due interfacce dell'applicazione, una per un sensore temperatura e una per un sensore umidità. Per informazioni sulla configurazione di un'interfaccia dell'applicazione per un sensore temperatura, vedi lo [scenario dell'interfaccia dell'applicazione di tipo dispositivo](../information_management/im_index_scenario).

## Informazioni su quest'attività
{: #about}

In {{site.data.keyword.iot_short_notm}}, un oggetto può consistere in diversi dispositivi e oggetti. Un tipo oggetto definisce come sono composte le istanze di un oggetto. Un'interfaccia dell'applicazione può essere associata a un tipo oggetto. Questa associazione definisce la struttura dello stato generato per un'istanza di tipo oggetto. Le associazioni vengono utilizzate per definire in che modo le proprietà dai dispositivi e dagli oggetti aggregati vengono associate alle proprietà di uno stato di oggetto.

In questo scenario, due sensori di temperatura e due sensori di umidità pubblicano gli eventi su {{site.data.keyword.iot_short_notm}}. Un sensore di temperatura e un sensore di umidità si trovano nella sala riunioni 1 di un complesso di uffici. L'altro sensore di temperatura e umidità si trova nella sala riunioni 2.

![Associazione tra oggetti di temperatura e umidità e un'applicazione su {{site.data.keyword.iot_short_notm}}.](images/Information "Associazione tra più sensori ambientali in una singola stanza e un'applicazione su {{site.data.keyword.iot_short_notm}}")

Un tipo oggetto denominato *RoomType* viene utilizzato per definire come sono composte le istanze delle stanze. Un'interfaccia dell'applicazione è associata al *RoomType* e definisce che gli eventi in entrata sono associati a una singola lettura che mostra sia la temperatura che l'umidità. Questa singola lettura è lo stato oggetto. Le associazioni sono utilizzate per definire in che modo le proprietà dai sensori di temperatura e di umidità sono associate a questo stato oggetto. Quando una nuova lettura viene pubblicata da questi sensori, il valore della proprietà associata allo stato oggetto viene modificato.

Sono inclusi i seguenti quattro dispositivi:

Tipo/dispositivo | Evento | Payload evento/Proprietà
------------- |  ------------- | -------------
*temperatureSensor1*/Thermometer (meetingroom1) | `iot-2/evt/`*`tevt`*`/fmt/json` | `{ “t” : 34.5 }`/ **temperature1**
*temperatureSensor2*/Thermometer (meetingroom2) | `iot-2/evt/`*`tempevt`*`/fmt/json` | `{ “temp” : 34.5 }`/ **temperature2**  
*humiditySensor1*/Hygrometer (meetingroom1) | `iot-2/evt/`*`hevt`*`/fmt/json` | `{  “h” : "75%" }`/ **humidity1**
*humiditySensor2*/Hygrometer (meetingroom2) |`iot-2/evt/`*`humevt`*`/fmt/json` | `{  “hum” : "75%"}`/ **humidity2**

L'interfaccia dell'applicazione di tipo oggetto rappresenta lo stato oggetto nella seguente struttura:
```
{
  “temperature” : <current temperature value in Celsius>
  "humidity" : <current humidity value>
  }
```

<!--
The code that is used in this example is available in the updated {{site.data.keyword.iot_short_notm}} [[Python library ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-python){: new_window} in GitHub, in the **thingDataTransform** sample.
-->  

Utilizza il seguente scenario di esempio per configurare il tuo ambiente di interfaccia.  

## Se necessario, aggiungi un tipo dispositivo e un dispositivo  
{: #add_device}  
In questo scenario, vengono utilizzati due tipi dispositivo e quattro istanze dispositivo. Le istanze dispositivo *temperatureSensor1* e *temperatureSensor2* sono associate al tipo dispositivo *Thermometer*. Le istanze dispositivo *humiditySensor1* e *humiditySensor2* sono associate al tipo dispositivo *Hygrometer*.

Per informazioni sull'utilizzo delle API REST per aggiungere un tipo dispositivo, consulta la documentazione [API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofThings.ibmcloud.com/swagger/v0002.html#!/Device_Types).  

## Passo 1: crea un file di schema composizione.  
{: #crt_composition_file}  
Crea un file di schema composizione che fa riferimento agli identificativi dell'interfaccia dell'applicazione dispositivo per ciascun tipo dispositivo di temperatura e umidità.  

Il seguente esempio mostra come creare un file di schema composizione denominato *Room Type Schema*.  
```
{
   "$schema": "http://json-schema.org/draft-04/schema#",
   "type" : "object",
   "title" : "Room Type Schema",
   "description" : "JSON Schema that defines the structure of the Room Thing Type.",
   "properties" : {
       "temperatureSensor": {
           "description": "The temperature sensor device",
           "$applicationInterfaceRef": "58c135e352faff0001198a89"
       },
       "humiditySensor": {
           "description": "The humidity sensor device",
           "$applicationInterfaceRef": "58c135ea52faff0001678f06"
       }
   },
   "required" : [
       "temperatureSensor",
       "humiditySensor"
   ]
}
```
**Suggerimento:** usa il parametro “required” per contrassegnare una o più proprietà come obbligatorie. Le proprietà obbligatorie devono essere incluse nel messaggio di dispositivo perché Watson IoT Platform aggiorni lo stato del dispositivo con i dati del dispositivo. Un messaggio che non include la proprietà obbligatoria non viene elaborato.   
**Nota:** l'identificativo di schema generato quando crei un file di schema di tipo oggetto deve essere specificato quando crei il tuo tipo oggetto.  

## Passo 2: crea una risorsa di schema di composizione.  
{: #crt_composition_resource}  

Crea la risorsa di schema caricando il file di schema di tipo oggetto che era stato generato nel passo precedente.  
Carica il file di schema di tipo oggetto utilizzando la seguente API:  
```
POST /schemas
```  
I seguenti parametri sono obbligatori:  
<table>
<tr>
<th>	Parametro	</th><th>	Descrizione	</th>
</tr>
<tr>
<td>	name	</td><td>	Fornisci un nome per lo schema di composizione che stai creando.	</td>
</tr>
<tr>
<td>	schemaFile	</td><td>	Percorso al file JSON dello schema di composizione locale.	</td>
</tr>
</table>

Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas).  

<!-- The following example shows how to use Python to create the thing type schema resource:  
```python
roomTypeSchemaFile = open(schemasDir + "roomType.json", "r");
roomTypeSchema = roomTypeSchemaFile.read();
roomTypeSchemaFile.close();
"roomTypeSchemaId", result = api.createSchema("Room Type Schema", "roomType.json", roomTypeSchema)
```  -->

## Passo 3: crea un tipo oggetto  
{: #crt_thing_type}  

I tipi oggetto sono utilizzati per modellare le istanze oggetto. Un tipo oggetto deve essere creato in un'organizzazione prima che possa essere creata un'istanza oggetto. Per questo scenario, crea un singolo tipo oggetto.  
Lo schema associato a un tipo oggetto definisce il tipo di oggetti aggregati insieme per creare un'istanza di un oggetto. Il tipo oggetto deve fare riferimento allo schema di tipo oggetto che hai creato nel passo precedente.  
Crea un tipo oggetto utilizzando la seguente API:
```
POST /thing/types
```
I seguenti parametri sono obbligatori:  
<table>
<tr><th>Parametro</th><th>Descrizione</th></tr>
<tr><td>Id</td><td>Fornisci un ID per il tipo oggetto che stai creando.</td></tr>
<tr><td>name</td><td>Fornisci un nome per il tipo oggetto che stai creando.</td></tr>
<tr><td>schemaId</td><td>L'ID creato per la risorsa di schema composizione.</td></tr>
</table>

Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types).  

<!-- The following example shows how to use Python to create a thing type that is called *RoomType*.
```python
result = api.createThingType(thingType, "RoomType", "roomTypeSchemaId", "The Room Thing type")

```  -->

## Passo 4: crea un file di schema dell'interfaccia dell'applicazione  
{: #crt_ai_schema_file}
Nella tua interfaccia dell'applicazione, puoi definire la struttura dei dati memorizzati come lo stato oggetto. Per questo scenario, crea un'interfaccia dell'applicazione che definisce le proprietà di temperatura e umidità. Associa l'interfaccia dell'applicazione al tipo oggetto *RoomType* facendo riferimento all'identificativo dell'interfaccia dell'applicazione generato quando crei la risorsa di interfaccia dell'applicazione.  
Il seguente esempio mostra come creare un file di schema dell'interfaccia dell'applicazione denominato *RoomType Schema*.
```
{
   "$schema": "http://json-schema.org/draft-04/schema#",
   "type" : "object",
   "title" : "RoomType Schema",
   "description" : "JSON Schema that defines the canonical room state structure",
   "properties" : {
       "temperature" : {
           "description" : "Temperature in degrees celsius",
           "type" : "number",
           "minimum" : -273.15,
           "default" : 0.0
       },
       "humidity" : {
           "description" : "Percentage humidity",
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
## Passo 5: crea una risorsa dello schema dell'interfaccia dell'applicazione.  
{: #crt_ai_schema_resource}  
Carica il file di schema dell'interfaccia dell'applicazione che hai creato nel passo precedente per creare una risorsa di schema dell'interfaccia dell'applicazione per il tuo tipo oggetto utilizzando la seguente API:  
```
POST /schemas
```  
I seguenti parametri sono obbligatori:  
<table>
<tr>
<th>Parametro</th><th>Descrizione</th>
</tr>
<tr>
<td>name</td><td>Fornisci un nome per lo schema dell'interfaccia dell'applicazione che stai creando.</td>
</tr>
<tr>
<td>schemaFile</td><td>Percorso al file JSON dello schema dell'interfaccia dell'applicazione locale.</td>
</tr>
</table>  

Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas).  

<!-- The following example shows how to use Python to create the thing type application interface schema resource:  
```python
roomSchemaFile = open(schemasDir + "room.json", "r");
roomSchema = roomSchemaFile.read();
roomSchemaFile.close();
"roomSchemaId", result = api.createSchema("Room Schema", "room.json", roomSchema)
```  -->

Utilizza l'identificativo schema per aggiungere la risorsa di schema dell'interfaccia dell'applicazione all'interfaccia dell'applicazione per il tuo tipo oggetto.  

## Passo 6: crea un'interfaccia dell'applicazione per il tipo oggetto.  
{: #crt_thing_ai}  
L'interfaccia dell'applicazione deve fare riferimento alla risorsa dello schema dell'interfaccia dell'applicazione che hai creato nel passo precedente.  
Per creare un'interfaccia dell'applicazione, utilizza la seguente API:  
```
POST /applicationinterfaces
```  
I seguenti parametri sono obbligatori:  
<table>
<tr>
<th>	Parametro	</th><th>	Descrizione	</th>
</tr>
<tr>
<td>	name	</td><td>	Fornisci un nome per l'interfaccia dell'applicazione che stai creando.	</td>
</tr>
<tr>
<td>	description	</td><td>	Fornisci una descrizione dell'interfaccia dell'applicazione.	</td>
</tr>
<tr>
<td>	schemaId	</td><td>	Percorso al file JSON dello schema dell'interfaccia dell'applicazione locale.	</td>
</tr>
</table>  

Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Application_Interfaces).  
Utilizza l'identificativo schema che era stato restituito nella risposta precedente per aggiungere lo schema dell'interfaccia dell'applicazione all'interfaccia dell'applicazione.  

<!-- The following example shows how to use Python to create an application interface:  
```python
"applicationInterfaceId", result = api.createApplicationInterface("IRoom", "roomSchemaId")
```  -->

Utilizza l'identificativo dell'interfaccia dell'applicazione per aggiungere la tua interfaccia dell'applicazione al tuo tipo dispositivo. Puoi anche utilizzare questo identificativo per associare un evento del dispositivo in entrata a una proprietà definita dall'interfaccia dell'applicazione.  

## Passo 7: aggiungi l'interfaccia dell'applicazione al tipo oggetto.  
{: #add_thing_ai}  
Per aggiungere un'interfaccia dell'applicazione a un tipo oggetto, utilizza la seguente API:  
```
POST /thing/types/{thingtypeId}/applicationinterfaces
```  
I seguenti parametri sono obbligatori:  
<table>
<tr>
<th>	Parametro	</th><th>	Descrizione	</th>
</tr>
<tr>
<td>	id	</td><td>	L'ID creato per il tipo oggetto.	</td>
</tr>
<tr>
<td>	name	</td><td>	Fornisci un nome per l'interfaccia dell'applicazione che stai creando.	</td>
</tr>
<tr>
<td>	schemaId	</td><td>	L'ID creato per la risorsa di interfaccia dell'applicazione.	</td>
</tr>
<tr>
<td>	refs/schema	</td><td>	Il percorso alla risorsa di interfaccia dell'applicazione. Di norma: /schemas/*Idschema*	</td>
</tr>
</table>  

Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types).  
In questo scenario, l'interfaccia dell'applicazione è associata al tipo oggetto *RoomType*.

<!-- The following example shows how to use Python to add the thing application interface to the thing type *RoomType*:  
```python
result = api.addApplicationInterfaceToThingType(RoomType, "applicationInterfaceId", "roomSchemaId")
``` -->

## Passo 8: definisci le associazioni
{: #define_Thing_type_mappings}

Definisci le associazioni per il tipo oggetto che descrivono come associare le proprietà dallo stato degli oggetti o dei dispositivi aggregati alle proprietà definite sull'interfaccia dell'applicazione di tipo oggetto.

Per associare gli eventi, utilizza la seguente API:  
```
POST /thing/types/{thingtypeId}/mappings
```  

I seguenti parametri sono obbligatori:  
<table>
<tr>
<th>	Parametro	</th><th>	Descrizione	</th>
</tr>
<tr>
<td>	applicationInterfaceId	</td><td>	L'ID creato per l'interfaccia dell'applicazione.	</td>
</tr>
<tr>
<td>	propertyMappings	</td><td>	Una struttura JSON valida che associa le proprietà definite per l'interfaccia dell'applicazione alle proprietà del payload di evento di dispositivo.	</td>
</tr>
</table>  

Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types).

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

Il seguente esempio mostra una voce di parametro propertyMappings di esempio:

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

*humiditySensor* è definito nello schema oggetto. "$event.humidity" è definito nello schema dell'interfaccia dell'applicazione con l'identificativo "58c135ea52faff0001678f06".
Il *temperatureSensor* è definito nello schema oggetto. "$event.temperatureC" è definito nello schema dell'interfaccia dell'applicazione con l'identificativo "58c135e352faff0001198a89".

## Passo 9: distribuisci la configurazione associata al tipo oggetto  
{: #deploy_Thing_config}   
Distribuisci la configurazione correlata all'aggiornamento dello stato oggetto per ciascun tipo oggetto. Questa configurazione include schemi, interfacce dell'applicazione e associazioni.

Devi distribuire la configurazione del tipo oggetto prima di poter creare qualsiasi istanza del tipo oggetto.

Per distribuire la tua configurazione del tipo oggetto, utilizza la seguente API:

```
PATCH /thing/types/{thingtypeId}
```
Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types).

<!-- The following example shows how to use Python to deploy your configuration for thing type *Room*:

```python
result = api.deployThingTypeConfiguration(thingType)
``` -->

## Passo 10: crea un'istanza di un tipo oggetto
{: #create_Thing_instances}

Un oggetto è un'istanza di un tipo oggetto. Un oggetto ti consente di aggregare insieme una o più istanze di un dispositivo o un oggetto in un singolo oggetto.

Per creare un oggetto, utilizza la seguente API:

```
POST /thing/types/{thingTypeId}/things
```

I seguenti parametri sono obbligatori:  
<table>
<tr>
<th>	Parametro	</th><th>	Descrizione	</th>
</tr>
<tr>
<td>	typeId	</td><td>		L'ID del tipo oggetto che hai creato in precedenza.</td>
</tr>
<tr>
<td>	thingId	</td><td>	Fornisci un nome per l'istanza oggetto che stai creando.	</td>
</tr>
</table>

Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Things).

In questo scenario, dobbiamo creare due istanze oggetto che sono di tipo oggetto *RoomType*. Una istanza oggetto è denominata *meetingroom1* e l'altra istanza oggetto è denominata *meetingroom2*.

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

L'identificativo dell'oggetto creato viene utilizzato nell'URL del metodo POST richiamato per aggiungere un evento temperatura all'interfaccia dell'applicazione di oggetto.

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

## Passo 11: verifica che gli eventi dispositivo associati siano pubblicati sull'interfaccia dell'applicazione  
{: #publish_event}  
Pubblica i seguenti eventi per i dispositivi aggregati nell'oggetto *meetingroom1*:  
 - un evento temperatura da *temperatureSensor1* sull'argomento `iot-2/evt/tevt/fmt/json`  
 - un evento umidità da *humiditySensor1* sull'argomento `iot-2/evt/hevt/fmt/json`  
Pubblica i seguenti eventi per i dispositivi aggregati nell'oggetto *meetingroom2*:  
 - un evento temperatura da *temperatureSensor2* sull'argomento `iot-2/evt/tempevt/fmt/json`  
 - un evento umidità da *humiditySensor2* sull'argomento `iot-2/evt/humevt/fmt/json`  
Per informazioni sulla pubblicazione di un evento in entrata da un dispositivo, consulta [Connettività MQTT per le applicazioni](../applications/mqtt.html#publishing_device_events).  

## Passo 12: controlla che lo stato dell'oggetto sia cambiato.  
{: #verify_Thing_state}  
Per controllare lo stato dell'oggetto, utilizza la seguente API:  
```
GET /thing/types/{thingTypeId}/things/{thingId}/state/{applicationInterfaceId}
```  

I seguenti parametri sono obbligatori:  
<table>
<tr>
<th>Parametro	</th><th>	Descrizione</th>
</tr>
<tr>
<td>thingtypeId	</td><td>L'ID del tipo oggetto</td>
</tr>
<tr>
<td>thingId	</td><td>	L'ID oggetto.</td>
</tr>
<tr>
<td>applicationInterfaceId</td><td>L'ID creato per l'interfaccia dell'applicazione.</td>
</tr>
</table>  

Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types).  

<!-- The following example shows how to use Python to retrieve the current state of *meetingroom1* by referencing the identifier of the application interface that was created:  
```python
result = api.getThingStateForApplicationInterface("RoomType", "meetingroom1", applicationInterfaceId)
```  
The following example shows how to use Python to retrieve the current state of *meetingroom2* by referencing the identifier of the application interface that was created:  
```python
result = api.getThingStateForApplicationInterface("RoomType", "meetingroom2", applicationInterfaceId)
``` -->
