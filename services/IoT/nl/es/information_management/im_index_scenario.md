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


# Caso de ejemplo 1 de interfaz de aplicación (Beta)
{: #scenario}

Utilice la siguiente información para crear un caso de ejemplo en el que dos sensores de temperatura publican sucesos en {{site.data.keyword.iot_short_notm}}. Uno sensor mide la temperatura en grados centígrados. El otro sensor mide la temperatura en grados Fahrenheit. Estas lecturas se correlacionan con una única lectura de temperatura que está en grados centígrados. Cuando estos dispositivos publican una nueva lectura de temperatura, el valor de la propiedad asociada al estado del dispositivo se modifica.

## Requisitos previos

Debe tener una instancia de organización de {{site.data.keyword.iot_short_notm}} y una clave de API o una señal correspondiente a la organización. Para obtener más información sobre claves de API y señales, consulte [API REST HTTP para aplicaciones](../applications/api.html#authentication).

## Acerca de esta tarea

En este caso de ejemplo, se configuran dos dispositivos.

Uno dispositivo se denomina *TemperatureSensor1*. Este dispositivo publica los sucesos de temperatura que se miden en grados centígrados. El suceso de temperatura se publica en el tema `iot-2/evt/tevt/fmt/json` y tiene la siguiente carga útil de ejemplo:
```
{
  “t” : 34.5
}
```

**Nota:** el identificador de suceso es *tevt*. Este identificador es necesario cuando se añade un suceso de temperatura de este tipo a la interfaz física y cuando se definen las correlaciones para correlacionar una propiedad asociada a un suceso de entrada de este tipo a una propiedad de la interfaz de aplicación. En este caso de ejemplo, la propiedad definida en la interfaz de la aplicación se denomina **temperature**.

El otro dispositivo se denomina *TemperatureSensor2*. Este dispositivo publica los sucesos de temperatura que se miden en grados Fahrenheit. El suceso de temperatura se publica en el tema `iot-2/evt/tempevt/fmt/json` y tiene la siguiente carga útil de ejemplo:
```
{
  “temp” : 72.55
}
```

**Nota:** el identificador de suceso es *tempevt*. Este identificador es necesario cuando se añade un suceso de temperatura de este tipo a la interfaz física y cuando se definen las correlaciones para correlacionar una propiedad asociada a un suceso de entrada de este tipo a una propiedad de la interfaz de aplicación. En este caso de ejemplo, la propiedad definida en la interfaz de la aplicación se denomina **temperature**.

También se configura una interfaz de aplicación. Esta interfaz de aplicación representa el estado de los dispositivos de este tipo en la estructura siguiente:
```
{
  “temperature” : <valor temperatura actual en grados centígrados>
  }
```
Esta configuración significa que puede configurar la aplicación para que procese el valor asociado con **temperature** en lugar de configurar la aplicación para que procese el valor asociado con **t** y procese el valor asociado con **temp** después de convertir dicho valor a grados centígrados.

![Correlación entre dispositivos sensores de temperatura y una aplicación de {{site.data.keyword.iot_short_notm}}.](images/Information "Correlación entre dispositivos sensores de temperatura y una aplicación en {{site.data.keyword.iot_short_notm}}")  

Utilice el siguiente caso de ejemplo para configurar su propio entorno de interfaces.

## Si es necesario, añada un tipo de dispositivo y un dispositivo
{: #step14}

En este caso de ejemplo, se presupone que hay dos tipos de dispositivo y dos instancias de dispositivo. La instancia de dispositivo *TemperatureSensor1* está asociado al tipo de dispositivo *EnvSensor1*. La instancia de dispositivo *TemperatureSensor2* está asociado al tipo de dispositivo *EnvSensor2*.

Para obtener información sobre cómo utilizar las API REST para añadir un tipo de dispositivo, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Types).

## Paso 1. Cree un archivo de esquema de suceso
{: #step1}

Para este caso de ejemplo, cree dos archivos de esquema de suceso para definir la estructura de cada uno de los sucesos de temperatura de entrada.

**Importante:** para cargas útiles estructuradas de sucesos [JSON ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://json-schema.org/){:new_window}, asegúrese de que cada nivel de anidación esté correctamente acomodado en una entrada `"properties"`. Por ejemplo, si la carga útil es `{"d":{"t":<temp>}}`, puede utilizar:
```
 "properties" : {
    "d" : {
      "properties" : {
        "t" : {
          "description" : "Temperatura en grados centígrados",
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

En el siguiente ejemplo se muestra cómo crear un archivo de esquema denominado *tEventSchema.json*. Este archivo define la estructura de un suceso de entrada procedente de un sensor de temperatura que mide la temperatura en grados centígrados:

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor1 tEvent Schema",
  "description" : “define la estructura de un suceso de temperatura en grados centígrados",
  "properties" : {
    "t" : {
      "description" : "temperatura en grados centígrados",
      "type" : "number",
      "minimum" : -273.15,
      "default" : 0.0
    }
  },
  "required" : ["t"]
}
  ```
**Consejo:** Utilice el parámetro “required” para marcar una o varias propiedades como obligatorias. Las propiedades obligatorias se deben incluir en un mensaje de dispositivo para que Watson IoT Platform actualice el estado del dispositivo con los datos del dispositivo. Un mensaje que no incluya la propiedad obligatoria no se procesa.   

El archivo de esquema llamado *tEventSchema* se utiliza al crear un suceso de recurso de esquema para el tipo de suceso.

En el siguiente ejemplo se muestra cómo crear un archivo de esquema denominado *tempEventSchema.json*. Este archivo define la estructura de un suceso de entrada procedente de un sensor de temperatura que mide la temperatura en grados Fahrenheit:

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor2 tempEvent Schema",
  "description" : "define la estructura de un suceso de temperatura en grados Fahrenheit",
  "properties" : {
    "temp" : {
      "description" : "temperatura en grados Fahrenheit",
      "type" : "number",
      "minimum" : −459.67,
      "default" : 0.0
    }
  },
  "required" : ["temp"]
}
  ```
El archivo de esquema llamado *tempEventSchema* se utiliza al crear un suceso de recurso de esquema para el tipo de suceso.   

## Paso 2. Cree un recurso de esquema de suceso para el tipo de suceso
{: #step2}

Para crear un recurso de esquema de suceso, utilice la siguiente API:

```
POST /schemas
```

Los parámetros siguientes son obligatorios:  

Parámetro	|	Descripción  
------	|	-----  
name	|	Especifique un nombre para el esquema de suceso que va a crear.  
schemaFile	|	Vía de acceso al archivo JSON del esquema de suceso.  



Para obtener más información, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas).

En el siguiente ejemplo se muestra cómo utilizar cURL para crear el recurso de esquema de suceso *tEventSchema.json*:

```curl
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=tEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tEventSchema.json'
```

El ejemplo siguiente muestra una respuesta al método POST:

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
El identificador de esquema *5846cd7c6522050001db0e0d* que se devuelve como respuesta al método POST es necesario cuando se añade un esquema de suceso al tipo de suceso.

En el siguiente ejemplo se muestra cómo utilizar cURL para crear el recurso de esquema de suceso *tempEventSchema.json*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: multipart/form-data’ \
  --form name=tempEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tempEventSchema.json"'
```

El ejemplo siguiente muestra una respuesta al método POST:

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
El identificador de esquema *5846cee36522050001db0e0e* que se devuelve como respuesta al método POST es necesario cuando se añade un esquema de suceso al tipo de suceso.

## Paso 3. Cree un tipo de suceso que haga referencia al esquema de suceso
{: #step3}

Cada tipo de suceso hace referencia al esquema de suceso relevante que se ha creado en el ejemplo anterior utilizando el identificador de esquema devuelto como respuesta al método POST utilizado para crear el recurso de esquema de suceso.

Para crear un tipo de suceso, utilice la siguiente API:

```
POST /event/types
```

Los parámetros siguientes son obligatorios:  

Parámetro	|	Descripción
------	|	-----
name	|	Especifique un nombre para el tipo de suceso que va a crear.
schemaId	|	El ID creado para el recurso del esquema de suceso.


Para obtener más información, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Event_Types).


El siguiente ejemplo muestra cómo utilizar cURL para crear un tipo de suceso para un suceso de temperatura que se mide en grados centígrados:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tEvent", "schemaId" : "5846cd7c6522050001db0e0d”}'
```

El identificador de esquema *5846cd7c6522050001db0e0d* se utiliza para añadir el esquema de suceso al tipo de suceso. Este identificador se ha devuelto como respuesta al método POST utilizado para crear el recurso de esquema de suceso *tEventSchema.json*

El ejemplo siguiente muestra una respuesta al método POST:

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

El identificador de tipo de suceso *5846d0fd6522050001db0e0f* que se devuelve como respuesta al método POST se utiliza para añadir un tipo de suceso a la interfaz física.

El siguiente ejemplo muestra cómo utilizar cURL para crear un tipo de suceso para un suceso de temperatura que se mide en grados Fahrenheit:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tempEvent", "schemaId" : "5846cee36522050001db0e0e"}'
```
El identificador de esquema *5846cee36522050001db0e0e* se utiliza para añadir el esquema de suceso al tipo de suceso. Este identificador se ha devuelto como respuesta al método POST utilizado para crear el recurso de esquema de suceso *tempEventSchema.json*

El ejemplo siguiente muestra una respuesta al método POST:

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
El identificador de tipo de suceso *5846d2846522050001db0e10* que se devuelve como respuesta al método POST se utiliza para añadir un tipo de suceso a la interfaz física.

## Paso 4. Cree una interfaz física
{: #step7}

Para crear una interfaz física, utilice la siguiente API:

```
POST /physicalinterfaces
```

Los parámetros siguientes son obligatorios:  

Parámetro	|	Descripción
------	|	-----
name	|	Especifique un nombre para la interfaz física que va a crear.


Para obtener más información, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces).

En este caso de ejemplo, necesitamos dos interfaces físicas, una para cada tipo de suceso.

En el siguiente ejemplo se muestra cómo utilizar cURL para crear la primera interfaz física:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Interfaz física 1 de sensor amb"}'
```

El ejemplo siguiente muestra una respuesta al método POST:

```
{
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
    "events" : "/physicalinterfaces/5847d1df6522050001db0e1a/events"
  },
  "id" : "5847d1df6522050001db0e1a",
  "name" : "Interfaz física 1 de sensor amb",
  "created" : "2016-12-07T09:09:51Z",
  "updated" : "2016-12-07T09:09:51Z",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

El identificador de la interfaz física *5847d1df6522050001db0e1a* que se devuelve como respuesta se utiliza en el URL del método POST al que se llama para añadir un suceso de temperatura que se mide en grados centígrados a la interfaz física.

En el siguiente ejemplo se muestra cómo utilizar cURL para crear la segunda interfaz física:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Interfaz física 2 de sensor amb"}'
```

El ejemplo siguiente muestra una respuesta al método POST:

```
{
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
    "events" : "/physicalinterfaces/5847d1df6522050001db0e1b/events"
  },
  "id" : "5847d1df6522050001db0e1b",
  "name" : "Interfaz física 2 de sensor amb",
  "created" : "2016-12-07T09:19:51Z",
  "updated" : "2016-12-07T09:19:51Z",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

El identificador de la interfaz física *5847d1df6522050001db0e1b* que se devuelve como respuesta se utiliza en el URL del método POST al que se llama para añadir un suceso de temperatura que se mide en grados Fahrenheit a la interfaz física.   

## Paso 5. Añada el tipo de suceso a la interfaz física
{: #step8}

Para añadir un tipo de suceso a la interfaz física, utilice la siguiente API:

```
POST /physicalinterfaces/{physicalInterfaceId}/events
```

Los parámetros siguientes son obligatorios:  

Parámetro	|	Descripción
------	|	-----
eventId	|	Especifique el nombre de suceso de la carga útil del suceso del dispositivo.
eventTypeId	|	El ID creado para el tipo de suceso.


Para obtener más información, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces).

En este caso de ejemplo, se añaden los siguientes tipos de suceso a las interfaces físicas especificadas:
- El suceso de temperatura en grados centígrados *tevt* se añade a la interfaz física con el identificador *5847d1df6522050001db0e1a* utilizando el *eventId* procedente del tema y el valor de *eventTypeId* procedente de la creación del recurso de esquema de suceso.
- El suceso de temperatura en grados Fahrenheit *tempevt* se añade a la interfaz física con el identificador *5847d1df6522050001db0e1b* utilizando el *eventId* procedente del tema y el valor de *eventTypeId* procedente de la creación del recurso de esquema de suceso.


En el siguiente ejemplo se muestra cómo utilizar cURL para añadir el suceso de temperatura *tevt* a la interfaz física con el identificador *5847d1df6522050001db0e1a*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1a/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : “tevt", "eventTypeId" : "5846d0fd6522050001db0e0f"}'
```

El ejemplo siguiente muestra una respuesta al método POST:

```
{
  "eventTypeId" : "5846d0fd6522050001db0e0f",
  "eventId" : "tevt"
}
```

En el siguiente ejemplo se muestra cómo utilizar cURL para añadir el suceso de temperatura *tempevt* a la interfaz física con el identificador *5847d1df6522050001db0e1b*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1b/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : "tempevt", "eventTypeId" : "5846d2846522050001db0e10"}'
```

El ejemplo siguiente muestra una respuesta al método POST:

```
{
  "eventTypeId" : "5846d2846522050001db0e10",
  "eventId" : “tempevt"
}
```

## Paso 6. Actualice el tipo de dispositivo para que se conecte a la interfaz física
{: #step9}

Para actualizar un tipo de dispositivo, utilice la siguiente API:

```
PUT /device/types/{typeId}
```

Los parámetros siguientes son obligatorios:  

Parámetro	|	Descripción
------	|	-----
physicalInterfaceId	|	El ID creado para la interfaz física.


Para obtener más información, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

En este caso de ejemplo, el tipo de dispositivo *EnvSensor1* se actualiza para conectarse a la interfaz física *5847d1df6522050001db0e1a* y el tipo de dispositivo *EnvSensor2* se actualiza para conectarse a la interfaz física *5847d1df6522050001db0e1b*.

En el siguiente ejemplo se muestra cómo utilizar cURL para actualizar el tipo de dispositivo *EnvSensor1*:

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an environment sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1a”}’
```

El ejemplo siguiente muestra una respuesta al método POST:

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
  "description" : "un sensor ambiental",
  "metadata" : {},
  "classId" : "Device",
  "createdDateTime" : "2016-12-07T09:49:52+00:00"
}
```
El identificador del dispositivo *EnvSensor1* es necesario cuando se añade la interfaz física y la interfaz de aplicación.

En el siguiente ejemplo se muestra cómo utilizar cURL para actualizar el tipo de dispositivo *EnvSensor2*:

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an env sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1b”}’
```

El ejemplo siguiente muestra una respuesta al método POST:

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
  "description" : "un sensor ambiental",
  "metadata" : {},
  "classId" : "Device",
  "createdDateTime" : "2016-12-07T09:49:52+00:00"
}
```
El identificador del dispositivo *EnvSensor2* es necesario cuando se añade la interfaz física y la interfaz de aplicación.



## Paso 7. Cree un archivo de esquema de interfaz de aplicación
{: #step4}

En el siguiente ejemplo se muestra cómo crear un archivo de esquema de interfaz de aplicación denominado *envSensor.json*.

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
    "type" : "object",
    "title" : "Esquema de sensor ambiental",
    "description" : "Esquema que representa un dispositivo sensor ambiental canónico",
    "properties" : {
        "temperature" : {
            "description" : "temperatura en grados centígrados",
            "type" : "number",
            "minimum" : -273.15,
            "default" : 0.0
        }
    },
    "required" : ["temperature"]
}
```

## Paso 8. Cree un recurso de esquema de interfaz de aplicación
{: #step5}

Para crear un recurso de esquema de interfaz de aplicación, utilice la siguiente API:

```
POST /schemas
```

Los parámetros siguientes son obligatorios:  

Parámetro	|	Descripción
------	|	-----
name	|	Especifique un nombre para el esquema de la interfaz de aplicación que va a crear.
schemaFile	|	Vía de acceso al archivo JSON del esquema de la interfaz de aplicación local.


Para obtener más información, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas).

En el siguiente ejemplo se muestra cómo utilizar cURL para crear el esquema de interfaz de aplicación:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=temperatureEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/envSensor.json"'
```

El ejemplo siguiente muestra una respuesta al método POST:

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
Utilice el identificador de esquema *5846ec826522050001db0e11* que se devuelve como respuesta al método POST para añadir el esquema de interfaz de aplicación a la interfaz de aplicación.

## Paso 9. Cree una interfaz de aplicación que haga referencia al esquema de interfaz de aplicación
{: #step6}

Para crear una interfaz de aplicación, utilice la siguiente API:

```
POST /applicationinterfaces
```

Los parámetros siguientes son obligatorios:  

Parámetro	|	Descripción
------	|	-----
name	|	Especifique un nombre para la interfaz de aplicación que va a crear.
schemaId	|	El ID creado para el recurso del esquema de interfaz de aplicación.


Para obtener más información, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Application_Interfaces).

En este caso de ejemplo, utilice el identificador de esquema *5846ec826522050001db0e11* que se ha devuelto en la respuesta anterior para añadir el esquema de interfaz de aplicación a la interfaz de aplicación.

En el siguiente ejemplo se muestra cómo utilizar cURL para una interfaz de aplicación:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "interfaz de sensor ambiental", "schemaId" : "5846ec826522050001db0e11"}'
```

El ejemplo siguiente muestra una respuesta al método POST:

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
  "name" : "interfaz de sensor ambiental"
}
```
En este caso de ejemplo, utilice el identificador de interfaz de aplicación *5846ed076522050001db0e12* que se devuelve como respuesta al método POST para añadir la interfaz de aplicación al tipo de dispositivo. También utilizará este identificador para correlacionar un suceso de dispositivo de entrada a una propiedad definida por la interfaz de aplicación.

## Paso 10. Añada la interfaz de aplicación a un tipo de dispositivo
{: #step10}

Para añadir una interfaz de aplicación a un tipo de dispositivo, utilice la siguiente API:

```
POST /device/types/{typeId}/applicationinterfaces
```

Los parámetros siguientes son obligatorios:  

Parámetro	|	Descripción
------	|	-----
id	|	El ID creado para la interfaz de la aplicación.
name	|	El nombre del tipo de dispositivo.
schemaId	|	El ID creado para el recurso de la interfaz de aplicación.
refs/schema	|	La vía de acceso al recurso de la interfaz de aplicación. Suele ser: /schemas/*schemaId*


Para obtener más información, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

En este caso de ejemplo, la interfaz de aplicación está asociada al tipo de dispositivo *EnvSensor1* y al tipo de dispositivo *EnvSensor2*.

En el siguiente ejemplo se muestra cómo utilizar cURL para añadir la interfaz de aplicación *5846ed076522050001db0e12* que hace referencia al identificador de esquema de aplicación *5846ec826522050001db0e11* al tipo de dispositivo *EnvSensor1*:

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

El ejemplo siguiente muestra una respuesta al método POST:

```
{
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "updated" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "name" : "interfaz de sensor ambiental",
  "created" : "2016-12-06T16:53:27Z",
  "id" : "5846ed076522050001db0e12",
  "schemaId" : "5846ec826522050001db0e11"
}
```

En el siguiente ejemplo se muestra cómo utilizar cURL para añadir la interfaz de aplicación *5846ed076522050001db0e12* asociada al identificador de esquema de aplicación *5846ec826522050001db0e11* al tipo de dispositivo *EnvSensor2*:

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


El ejemplo siguiente muestra una respuesta al método POST:

```
{
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "updated" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "name" : "interfaz de sensor ambiental",
  "created" : "2016-12-06T16:53:27Z",
  "id" : "5846ed076522050001db0e12",
  "schemaId" : "5846ec826522050001db0e11"
}
```

## Paso 11. Defina las correlaciones para correlacionar las propiedades del suceso de entrada con las propiedades de la interfaz de aplicación
{: #step11}

Para correlacionar sucesos, utilice la siguiente API:

```
POST /device/types/{typeId}/mappings
```

Los parámetros siguientes son obligatorios:  

Parámetro	|	Descripción
------	|	-----
applicationInterfaceId	|	El ID creado para la interfaz de la aplicación.
propertyMappings	|	Una estructura JSON válida que correlaciona las propiedades definidas para la interfaz de aplicación con las propiedades de la carga útil del suceso de dispositivo. Consulte los ejemplos siguientes.


Para obtener más información, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

En este caso de ejemplo, se definen correlaciones para el tipo de dispositivo *EnvSensor1* para correlacionar la propiedad **t** del suceso de entrada *tevt* con la propiedad **temperature** de la interfaz de aplicación. También se definen correlaciones para el tipo de dispositivo *EnvSensor2* para correlacionar la propiedad **temp** del suceso de entrada *tempevt* con la propiedad **temperature** de la interfaz de aplicación.

En el siguiente ejemplo se muestra cómo utilizar cURL para añadir una correlación al tipo de dispositivo *EnvSensor1*:

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

**Importante:** para cargas útiles estructuradas de sucesos [JSON ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://json-schema.org/){:new_window}, asegúrese que la entrada $event.*property* coincide correctamente con la estructura JSON de sus propiedades. Por ejemplo, si la carga útil es `{"d":{"t":<temp>}}`, utilice `$event.d.t`

Especifique el identificador de interfaz de aplicación *5846ed076522050001db0e12* que se devuelve como respuesta al método POST utilizado para crear la interfaz de aplicación y el tipo de dispositivo *EnvSensor1*.

El ejemplo siguiente muestra una respuesta al método POST:

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
En el siguiente ejemplo se muestra cómo utilizar cURL para añadir una correlación al tipo de dispositivo *EnvSensor2*:

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

Especifique el identificador de interfaz de aplicación *5846ed076522050001db0e12* que se devuelve como respuesta al método POST utilizado para crear la interfaz de aplicación y el tipo de dispositivo *EnvSensor2*.
Se aplica una conversión para cambiar el valor de una medida en grados Fahrenheit a una medida en grados centígrados.


El ejemplo siguiente muestra una respuesta al método POST:

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

## Paso 12. Despliegue la configuración
{: #step15}

Despliegue la configuración relacionada con la actualización de estado de dispositivo para cada tipo de dispositivo. Esta configuración incluye esquemas, tipos de suceso, interfaces físicas, interfaces de aplicación y correlaciones.

Para desplegar la configuración del tipo de dispositivo, utilice la siguiente API:

```
PATCH /device/types/{typeId}
```

Los parámetros siguientes son obligatorios:  

Parámetro	|	Descripción
------	|	-----
typeId	|	El ID de tipo de dispositivo

Para obtener más información, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

En este caso de ejemplo, debemos desplegar la configuración para dos tipos de dispositivo.

En el siguiente ejemplo se muestra cómo utilizar cURL para desplegar la configuración para el tipo de dispositivo *EnvSensor1*:

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy-configuration"
          }'
```

El ejemplo siguiente muestra una respuesta al método PATCH:

```
{
 "message": "CUDRS0520I: La configuración de actualización de estado para tipo de dispositivo 'EnvSensor1' se ha enviado correctamente para su despliegue", "details": {
    "id": "CUDRS0520I",
    "properties": ["EnvSensor1"]
  },
 "failures": []
}
```

En el siguiente ejemplo se muestra cómo utilizar cURL para desplegar la configuración para el tipo de dispositivo *EnvSensor2*:

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
          }'
```

El ejemplo siguiente muestra una respuesta al método PATCH:

```
{
 "message": "CUDRS0520I: La configuración de actualización de estado para tipo de dispositivo 'EnvSensor2' se ha enviado correctamente para su despliegue", "details": {
    "id": "CUDRS0520I",
    "properties": ["EnvSensor2"]
  },
 "failures": []
}
```

## Paso 13. Publique un suceso de dispositivo de entrada
{: #step12}

Publique un suceso de temperatura *TemperatureSensor1* en el tema `iot-2/evt/tevt/fmt/json` y un suceso de temperatura *TemperatureSensor2* en el tema `iot-2/evt/tempevt/fmt/json`.

Para obtener información sobre cómo publicar un suceso de entrada procedente de un dispositivo, consulte [Conectividad de MQTT para las aplicaciones](../applications/mqtt.html#publishing_device_events).


## Paso 14. Compruebe que el estado del dispositivo se ha cambiado
{: #step13}

Para comprobar el estado del dispositivo, utilice la siguiente API:
```
GET /device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
```

Los parámetros siguientes son obligatorios:  

Parámetro	|	Descripción
------	|	-----
typeId	|	El ID del tipo de dispositivo
deviceId	|	El ID de dispositivo.
applicationInterfaceId	|	El ID creado para la interfaz de la aplicación.

Para obtener más información, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

En el siguiente ejemplo se muestra cómo utilizar cURL para recuperar el estado actual de *TemperatureSensor1* haciendo referencia al identificador de la interfaz de aplicación que se ha creado:
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/devices/TemperatureSensor1/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

Se utiliza el identificador de interfaz de aplicación *5846ed076522050001db0e12* en el método GET. Este identificador se ha devuelto como respuesta al método POST utilizado para crear la interfaz de aplicación.
El ejemplo siguiente muestra una respuesta al método GET:
```
{
  "temperature":34.5
}
```
En el siguiente ejemplo se muestra cómo utilizar cURL para recuperar el estado actual de *TemperatureSensor2* haciendo referencia al identificador de la interfaz de aplicación que se ha creado:
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/devices/TemperatureSensor2/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

Se utiliza el identificador de interfaz de aplicación *5846ed076522050001db0e12* en el método GET. Este identificador se ha devuelto como respuesta al método POST utilizado para crear la interfaz de aplicación.
El ejemplo siguiente muestra una respuesta al método GET:
```
{
  "temperature":22.5
}
```
Observe que la lectura de temperatura que se devuelve está en grados centígrados, no en grados Fahrenheit.

La aplicación puede procesar estos datos normalizados sin que haya que realizar ninguna configuración para comprender o convertir las distintas escalas de temperatura.


**Nota:** para recuperar la última configuración desplegada, utilice la siguiente API:

```
GET /device/types/<typeId>/deployedconfiguration
```
Utilice esta API para recuperar la configuración que se ha desplegado la última vez que la operación de despliegue PATCH ha finalizado correctamente. Para recuperar la configuración correspondiente a un recurso que se ha modificado pero no desplegado, utilice el método GET normal asociado al recurso que desea consultar.

Para obtener más información, consulte la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

En el siguiente ejemplo se muestra cómo utilizar cURL para recuperar la última configuración desplegada:
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/deployedconfiguration \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```
El ejemplo siguiente muestra una respuesta al método GET:

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
  "name" : "Interfaz física 1 de sensor amb",
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
