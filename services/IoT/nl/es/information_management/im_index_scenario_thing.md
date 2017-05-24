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

# Caso de ejemplo 2 de interfaz de aplicación (Beta)
{: #scenario}

La interfaz de aplicación se utiliza para eliminar el requisito de aplicación de comprender cómo está configurado un dispositivo o una cosa. Por ejemplo, supongamos que desea medir la temperatura de una sala utilizando un único dispositivo, o que quiera calcular la temperatura de la sala tomando la lectura media de varios dispositivos. La aplicación necesita información sobre el estado de una sala o salas, uno de cuyos componentes es la propiedad temperatura. No importa cómo se ha calculado el valor de temperatura que recibe la aplicación.

En este caso de ejemplo, los sensores de temperatura y los sensores de humedad publican datos ambientales que se recopilan en dos salas de reuniones. Los datos del sensor de temperatura y de humedad se correlacionan por separado con dos interfaces de aplicación de tipo de dispositivo, una para el tipo de dispositivo termómetro y otra para el tipo de dispositivo higrómetro. Se crea un tipo de cosa denominado *RoomType*, junto con dos instancias de cosa: *meetingroom1* y *meetingroom2*.

Este caso de ejemplo se configura una composición que incluye las interfaces de aplicación de termómetro y de higrómetro y luego se correlacionan los sensores ambientales correctos con cada una de las instancias de sala; por ejemplo, *temperatureSensor1* y *humiditySensor1* se correlacionan con *meetingroom1*.

## Requisitos previos
{: #pre_req}

Este caso de ejemplo se basa en el [Caso de ejemplo 1 de interfaz de aplicación](im_index_scenario) anterior.

Antes de continuar, asegúrese de que:
- Utiliza la misma instancia de organización de {{site.data.keyword.iot_short_notm}} y una clave de API o una señal correspondiente a la organización. Para obtener más información sobre claves de API y señales, consulte [API REST HTTP para aplicaciones](../applications/api.html#authentication).
- Ha creado dos interfaces de aplicación, una para un sensor de temperatura y otra para un sensor de humedad. Para obtener información sobre cómo configurar una interfaz de aplicación para un sensor de temperatura, consulte [Caso de ejemplo de interfaz de aplicación de tipo de dispositivo](../information_management/im_index_scenario).

## Acerca de esta tarea
{: #about}

En {{site.data.keyword.iot_short_notm}}, una cosa puede constar de varios dispositivos y cosas. Un tipo de cosa define cómo se componen las instancias de una cosa. Una interfaz de aplicación puede estar asociada a un tipo de cosa. Esta asociación define la estructura del estado que se genera para una instancia de tipo de cosa. Se utilizan correlaciones para definir la forma en que se correlacionan las propiedades procedentes de los dispositivos y cosas agregados con las propiedades de un estado de cosa.

En este caso de ejemplo, dos sensores de temperatura y dos sensores de humedad publican sucesos en {{site.data.keyword.iot_short_notm}}. Un sensor de temperatura y un sensor de humedad están en la sala de reuniones 1 de un bloque de oficinas. Los otros sensores de temperatura y humedad están en la sala de reuniones 2.

![Correlación entre sensores de temperatura y de humedad y una aplicación en {{site.data.keyword.iot_short_notm}}.](images/Information "Correlación entre varios sensores ambientales de una sala y una aplicación en {{site.data.keyword.iot_short_notm}}")

Se utiliza un tipo de cosa denominado *RoomType* para definir la composición de las instancias de las salas. Se asocia una interfaz de aplicación con *RoomType* y se define que los sucesos de entrada se correlacionen con una sola lectura que muestre tanto temperatura como humedad. Esta lectura única es el estado de la cosa. Se utilizan correlaciones para definir la forma en que se correlacionan las propiedades de los sensores de temperatura y de humedad con este estado de la cosa. Cuando estos sensores publican una nueva lectura, el valor de la propiedad asociada al estado de la cosa se modifica.

Se incluyen estos cuatro dispositivos:

Dispositivo/Tipo | Suceso | Carga de trabajo/Propiedad del suceso
------------- |  ------------- | -------------
*temperatureSensor1*/Thermometer (meetingroom1) | `iot-2/evt/`*`tevt`*`/fmt/json` | `{ “t” : 34.5 }`/ **temperature1**
*temperatureSensor2*/Thermometer (meetingroom2) | `iot-2/evt/`*`tempevt`*`/fmt/json` | `{ “temp” : 34.5 }`/ **temperature2**  
*humiditySensor1*/Hygrometer (meetingroom1) | `iot-2/evt/`*`hevt`*`/fmt/json` | `{  “h” : "75%" }`/ **humidity1**
*humiditySensor2*/Hygrometer (meetingroom2) |`iot-2/evt/`*`humevt`*`/fmt/json` | `{  “hum” : "75%"}`/ **humidity2**

La interfaz de aplicación de tipo de cosa representa el estado de la cosa en la estructura siguiente:
```
{
  “temperature” : <valor temperatura actual en grados centígrados>
  "humidity" : <valor humedad actual>
  }
```

<!--
The code that is used in this example is available in the updated {{site.data.keyword.iot_short_notm}} [[Python library ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-python){: new_window} in GitHub, in the **thingDataTransform** sample.
-->  

Utilice el siguiente caso de ejemplo para configurar su propio entorno de interfaces.  

## Si es necesario, añada un tipo de dispositivo y un dispositivo  
{: #add_device}  
En este caso de ejemplo, se utilizan dos tipos de dispositivo y cuatro instancias de dispositivo. Las instancias de dispositivo *temperatureSensor1* y *temperatureSensor2* están asociadas al tipo de dispositivo *Thermometer*. Las instancias de dispositivo *humiditySensor1* y *humiditySensor2* están asociadas al tipo de dispositivo *Hygrometer*.

Para obtener información sobre cómo utilizar las API REST para añadir un tipo de dispositivo, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofThings.ibmcloud.com/swagger/v0002.html#!/Device_Types).  

## Paso 1. Cree un archivo de esquema de composición.  
{: #crt_composition_file}  
Cree un archivo de esquema de composición que haga referencia a los identificadores de la interfaz de aplicación para cada tipo de dispositivo de temperatura y de humedad.  

En el siguiente ejemplo se muestra cómo crear un archivo de esquema de composición denominado *Room Type Schema*.  
```
{
   "$schema": "http://json-schema.org/draft-04/schema#",
   "type" : "object",
   "title" : "Room Type Schema",
   "description" : "Esquema JSON que define la estructura de Room Thing Type.",
   "properties" : {
       "temperatureSensor": {
           "description": "El dispositivo sensor de temperatura",
           "$applicationInterfaceRef": "58c135e352faff0001198a89"
       },
       "humiditySensor": {
           "description": "El dispositivo sensor de humedad",
           "$applicationInterfaceRef": "58c135ea52faff0001678f06"
       }
   },
   "required" : [
       "temperatureSensor",
       "humiditySensor"
   ]
}
```
**Consejo:** Utilice el parámetro “required” para marcar una o varias propiedades como obligatorias. Las propiedades obligatorias se deben incluir en un mensaje de dispositivo para que Watson IoT Platform actualice el estado del dispositivo con los datos del dispositivo. Un mensaje que no incluya la propiedad obligatoria no se procesa.   
**Nota:** se debe especificar el identificador de esquema que se genera cuando se crea un archivo de esquema de tipo de cosa cuando se crea el tipo de cosa.  

## Paso 2. Cree un recurso de esquema de composición.  
{: #crt_composition_resource}  

Para crear el recurso de esquema, cargue el archivo de esquema de tipo cosa generado en el paso anterior.  
Para cargar el archivo de esquema de tipo de cosa, utilice la siguiente API:  
```
POST /schemas
```  
Los parámetros siguientes son obligatorios:  
<table>
<tr>
<th>	Parámetro	</th><th>	Descripción	</th>
</tr>
<tr>
<td>	name	</td><td>	Especifique un nombre para el esquema de composición que va a crear.	</td>
</tr>
<tr>
<td>	schemaFile	</td><td>	Vía de acceso al archivo JSON del esquema de composición.	</td>
</tr>
</table>

Para ver más detalles, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas).  

<!-- The following example shows how to use Python to create the thing type schema resource:  
```python
roomTypeSchemaFile = open(schemasDir + "roomType.json", "r");
roomTypeSchema = roomTypeSchemaFile.read();
roomTypeSchemaFile.close();
"roomTypeSchemaId", result = api.createSchema("Room Type Schema", "roomType.json", roomTypeSchema)
```  -->

## Paso 3: Crear un tipo de cosa  
{: #crt_thing_type}  

Los tipos de cosa se utilizan para modelar las instancias de una cosa. Se debe crear un tipo de cosa en una organización para que se pueda crear una instancia de la cosa. Para este caso de ejemplo, cree un tipo de cosa.  
El esquema que está asociado a un tipo de cosa define el tipo de objetos que se agregan juntos para crear una instancia de una cosa. El tipo de cosa debe hacer referencia al recurso de esquema de tipo de cosa que ha creado en el paso anterior.  
Para crear un tipo de cosa, utilice la siguiente API:
```
POST /thing/types
```
Los parámetros siguientes son obligatorios:  
<table>
<tr><th>Parámetro</th><th>Descripción</th></tr>
<tr><td>Id</td><td>Especifique un ID para el tipo de cosa que va a crear.</td></tr>
<tr><td>name</td><td>Especifique un nombre para el tipo de cosa que va a crear.</td></tr>
<tr><td>schemaId</td><td>El ID creado para el recurso del esquema de composición.</td></tr>
</table>

Para obtener más información, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types).  

<!-- The following example shows how to use Python to create a thing type that is called *RoomType*.
```python
result = api.createThingType(thingType, "RoomType", "roomTypeSchemaId", "The Room Thing type")

```  -->

## Paso 4. Cree un archivo de esquema de interfaz de aplicación  
{: #crt_ai_schema_file}
En la interfaz de aplicación, puede definir la estructura de los datos que se almacena como estado de la cosa. Para este caso de ejemplo, cree una interfaz de aplicación que defina las propiedades de temperatura y humedad. Asocie la interfaz de aplicación con el tipo de cosa *RoomType* haciendo referencia al identificador de la interfaz de aplicación que se genera cuando se crea el recurso de la interfaz de aplicación.  
En el siguiente ejemplo se muestra cómo crear un archivo de esquema de interfaz de aplicación denominado *RoomType Schema*.
```
{
   "$schema": "http://json-schema.org/draft-04/schema#",
   "type" : "object",
   "title" : "RoomType Schema",
   "description" : "Esquema JSON que define la estructura canónica del estado de la sala",
   "properties" : {
       "temperature" : {
           "description" : "Temperatura en grados centígrados",
           "type" : "number",
           "minimum" : -273.15,
           "default" : 0.0
       },
       "humidity" : {
           "description" : "Porcentaje de humedad",
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
## Paso 5. Cree un recurso de esquema de interfaz de aplicación.  
{: #crt_ai_schema_resource}  
Cargue el archivo de esquema de la interfaz de aplicación que ha creado en el paso anterior para crear un recurso de esquema de interfaz de aplicación para el tipo de cosa utilizando la siguiente API:  
```
POST /schemas
```  
Los parámetros siguientes son obligatorios:  
<table>
<tr>
<th>Parámetro</th><th>Descripción</th>
</tr>
<tr>
<td>name</td><td>Especifique un nombre para el esquema de la interfaz de aplicación que va a crear.</td>
</tr>
<tr>
<td>schemaFile</td><td>Vía de acceso al archivo JSON del esquema de la interfaz de aplicación local.</td>
</tr>
</table>  

Para ver más detalles, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas).  

<!-- The following example shows how to use Python to create the thing type application interface schema resource:  
```python
roomSchemaFile = open(schemasDir + "room.json", "r");
roomSchema = roomSchemaFile.read();
roomSchemaFile.close();
"roomSchemaId", result = api.createSchema("Room Schema", "room.json", roomSchema)
```  -->

Utilice el identificador de esquema para añadir el recurso de esquema de la interfaz de aplicación correspondiente al tipo de cosa.  

## Paso 6. Cree una interfaz de aplicación para el tipo de cosa.  
{: #crt_thing_ai}  
La interfaz de aplicación debe hacer referencia al recurso de esquema de la interfaz de aplicación que ha creado en el paso anterior.  
Para crear una interfaz de aplicación, utilice la siguiente API:  
```
POST /applicationinterfaces
```  
Los parámetros siguientes son obligatorios:  
<table>
<tr>
<th>	Parámetro	</th><th>	Descripción	</th>
</tr>
<tr>
<td>	name	</td><td>	Especifique un nombre para la interfaz de aplicación que va a crear.	</td>
</tr>
<tr>
<td>	description	</td><td>	Especifique una descripción de la interfaz de aplicación.	</td>
</tr>
<tr>
<td>	schemaId	</td><td>	Vía de acceso al archivo JSON del esquema de la interfaz de aplicación local.	</td>
</tr>
</table>  

Para obtener más información, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Application_Interfaces).  
Utilice el identificador de esquema que se ha devuelto en la respuesta anterior para añadir el esquema de interfaz de aplicación a la interfaz de aplicación.  

<!-- The following example shows how to use Python to create an application interface:  
```python
"applicationInterfaceId", result = api.createApplicationInterface("IRoom", "roomSchemaId")
```  -->

Utilice el identificador de la interfaz de aplicación para añadir la interfaz de aplicación al tipo de dispositivo. También utilizará este identificador para correlacionar un suceso de dispositivo de entrada a una propiedad definida por la interfaz de aplicación.  

## Paso 7. Añada la interfaz de aplicación al tipo de cosa.  
{: #add_thing_ai}  
Para añadir una interfaz de aplicación a un tipo de cosa, utilice la siguiente API:  
```
POST /thing/types/{thingtypeId}/applicationinterfaces
```  
Los parámetros siguientes son obligatorios:  
<table>
<tr>
<th>	Parámetro	</th><th>	Descripción	</th>
</tr>
<tr>
<td>	id	</td><td>	El ID creado para el tipo de cosa.	</td>
</tr>
<tr>
<td>	name	</td><td>	Especifique un nombre para la interfaz de aplicación que va a crear.	</td>
</tr>
<tr>
<td>	schemaId	</td><td>	El ID creado para el recurso de la interfaz de aplicación.	</td>
</tr>
<tr>
<td>	refs/schema	</td><td>	La vía de acceso al recurso de la interfaz de aplicación. Suele ser: /schemas/*schemaId*	</td>
</tr>
</table>  

Para obtener más información, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types).  
En este caso de ejemplo, la interfaz de aplicación está asociada al tipo de cosa *RoomType*.

<!-- The following example shows how to use Python to add the thing application interface to the thing type *RoomType*:  
```python
result = api.addApplicationInterfaceToThingType(RoomType, "applicationInterfaceId", "roomSchemaId")
``` -->

## Paso 8: Defina correlaciones
{: #define_Thing_type_mappings}

Defina las correlaciones para el tipo de cosa que describan cómo se deben correlacionar las propiedades entre el estado de los dispositivos o cosas agregados y las propiedades definidas en la interfaz de aplicación del tipo de cosa.

Para correlacionar sucesos, utilice la siguiente API:  
```
POST /thing/types/{thingtypeId}/mappings
```  

Los parámetros siguientes son obligatorios:  
<table>
<tr>
<th>	Parámetro	</th><th>	Descripción	</th>
</tr>
<tr>
<td>	applicationInterfaceId	</td><td>	El ID creado para la interfaz de la aplicación.	</td>
</tr>
<tr>
<td>	propertyMappings	</td><td>	Una estructura JSON válida que correlaciona las propiedades definidas para la interfaz de aplicación con las propiedades de la carga útil del suceso de dispositivo.	</td>
</tr>
</table>  

Para obtener más información, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types).

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

El siguiente ejemplo muestra un ejemplo de entrada del parámetro propertyMappings:

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

El valor *humiditySensor* se define en el esquema de la cosa. El valor "$event.humidity" se define en el esquema de la interfaz de aplicación con el identificador "58c135ea52faff0001678f06".
El valor *temperatureSensor* se define en el esquema de la cosa. El valor "$event.temperatureC" se define en el esquema de la interfaz de aplicación con el identificador "58c135e352faff0001198a89".

## Paso 9. Despliegue la configuración asociada con el tipo de cosa  
{: #deploy_Thing_config}   
Despliegue la configuración relacionada con la actualización de estado de cosa para cada tipo de cosa. Esta configuración incluye esquemas, interfaces de aplicación y correlaciones.

Debe desplegar la configuración del tipo de cosa para poder crear instancias del tipo de cosa.

Para desplegar la configuración del tipo de cosa, utilice la siguiente API:

```
PATCH /thing/types/{thingtypeId}
```
Para obtener más información, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types).

<!-- The following example shows how to use Python to deploy your configuration for thing type *Room*:

```python
result = api.deployThingTypeConfiguration(thingType)
``` -->

## Paso 10: Cree una instancia de un tipo de cosa
{: #create_Thing_instances}

Una cosa es una instancia de un tipo de cosa. Una cosa le permite añadir una o varias instancias de un dispositivo o cosa juntos en un único objeto.

Para crear una cosa, utilice la siguiente API:

```
POST /thing/types/{thingTypeId}/things
```

Los parámetros siguientes son obligatorios:  
<table>
<tr>
<th>	Parámetro	</th><th>	Descripción	</th>
</tr>
<tr>
<td>	typeId	</td><td>		El ID del tipo de cosa que ha creado anteriormente.</td>
</tr>
<tr>
<td>	thingId	</td><td>	Especifique un nombre para la instancia de la cosa que va a crear.	</td>
</tr>
</table>

Para obtener más información, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Things).

En este caso de ejemplo, tenemos que crear dos instancias que sean del tipo de cosa *RoomType*. Una instancia de cosa se denomina *meetingroom1* y la otra instancia de cosa se denomina *meetingroom2*.

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

El identificador de cosa que se crea se utiliza en el URL del método POST al que se llama para añadir un suceso de temperatura a la interfaz de aplicación de la cosa.

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

## Paso 11: Compruebe que los sucesos del dispositivo correlacionado se publican en la interfaz de la aplicación  
{: #publish_event}  
Publique los siguientes sucesos para los dispositivos que se agregan a la cosa *meetingroom1*:  
 - un suceso de temperatura de *temperatureSensor1* en el tema `iot-2/evt/tevt/fmt/json`  
 - un suceso de humedad de *humiditySensor1* en el tema `iot-2/evt/hevt/fmt/json`  
Publique los siguientes sucesos para los dispositivos que se agregan a la cosa *meetingroom2*:  
 - un suceso de temperatura de *temperatureSensor2* en el tema `iot-2/evt/tempevt/fmt/json`  
 - un suceso de humedad de *humiditySensor2* en el tema `iot-2/evt/humevt/fmt/json`  
Para obtener información sobre cómo publicar un suceso de entrada procedente de un dispositivo, consulte [Conectividad de MQTT para las aplicaciones](../applications/mqtt.html#publishing_device_events).  

## Paso 12. Compruebe que el estado de la cosa se ha cambiado.  
{: #verify_Thing_state}  
Para comprobar el estado de la cosa, utilice la siguiente API:  
```
GET /thing/types/{thingTypeId}/things/{thingId}/state/{applicationInterfaceId}
```  

Los parámetros siguientes son obligatorios:  
<table>
<tr>
<th>Parámetro	</th><th>	Descripción</th>
</tr>
<tr>
<td>thingtypeId	</td><td>El ID del tipo de cosa</td>
</tr>
<tr>
<td>thingId	</td><td>	El ID de cosa.</td>
</tr>
<tr>
<td>applicationInterfaceId</td><td>El ID creado para la interfaz de la aplicación.</td>
</tr>
</table>  

Para obtener más información, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types).  

<!-- The following example shows how to use Python to retrieve the current state of *meetingroom1* by referencing the identifier of the application interface that was created:  
```python
result = api.getThingStateForApplicationInterface("RoomType", "meetingroom1", applicationInterfaceId)
```  
The following example shows how to use Python to retrieve the current state of *meetingroom2* by referencing the identifier of the application interface that was created:  
```python
result = api.getThingStateForApplicationInterface("RoomType", "meetingroom2", applicationInterfaceId)
``` -->
