---

copyright:
years: 2016, 2017
lastupdated: "2017-01-17"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Utilización de interfaces para correlacionar datos de dispositivo (Beta)
{: #im_index}

Utilice la característica de correlación de interfaces de {{site.data.keyword.iot_full}} para organizar e integrar los datos entrantes y salientes del dispositivo.
{:shortdesc}

**Importante:** la característica de correlación de interfaces solo está disponible actualmente como característica Beta. Antes del release final, es probable que las actualizaciones de la versión Beta incluyan cambios que no son compatibles con la versión actual. Se recomienda encarecidamente que las características Beta no se utilicen en aplicaciones de producción hasta el release final. Para recibir información adicional y proporcionar comentarios sobre esta versión Beta, [regístrese para el programa IM Beta](https://www.ibm.com/software/support/trial/cst/forms/nomination.wss?id=7050) y que díganos lo que piensa.

## Visión general
{: #overview}

Puede utilizar la característica de correlación de interfaces para desarrollar interfaces para las aplicaciones. Es posible que tenga tipos o modelos diferentes de dispositivo o sensor que desee conectar a {{site.data.keyword.iot_short_notm}} y puede que estos dispositivos publiquen datos en distintos formatos. Utilice la característica de correlación de interfaces para normalizar los datos de entrada y para simplificar las aplicaciones eliminando la complejidad que plantea el método de la conexión de dispositivos específicos.

Por ejemplo, es posible que tenga dos sensores de temperatura. Un sensor mide la temperatura en grados centígrados y un sensor la mide en grados Fahrenheit.

![Correlación entre dispositivos sensores de temperatura y una aplicación de {{site.data.keyword.iot_short_notm}}.](images/Information "Mapping between temperature sensor devices and an application on {{site.data.keyword.iot_short_notm}}")

El sensor de temperatura 1 publica la lectura de temperatura `{ "t" : 34.5 }` en {{site.data.keyword.iot_short_notm}}. Es una lectura de temperatura con un valor en grados centígrados. El sensor de temperatura 2 publica la lectura de temperatura `{ "temp" : 72.55 }` en {{site.data.keyword.iot_short_notm}}. Se trata de otro tipo de sensor de temperatura que tiene una lectura con un valor en Fahrenheit. Las lecturas de temperatura se publican como sucesos separados en {{site.data.keyword.iot_short_notm}}.

Mediante la característica de correlación de interfaces, puede normalizar estas lecturas en un formato coherente para su proceso. No es necesario que escriba la aplicación para entender o convertir distintas escalas de temperatura. La aplicación recibe una única vista normalizada y se puede conectar a **temperature** en lugar de hacerlo a **t** y **temp**.

## Flujo de datos entre dispositivos y aplicaciones
{: #mapping}

El siguiente diagrama de flujo muestra cómo se utilizan los distintos recursos de la característica de correlación de interfaces:

![El flujo entre un dispositivo y una aplicación en {{site.data.keyword.iot_short_notm}}.](images/Information "The flow between a device and an application on {{site.data.keyword.iot_short_notm}}")

El siguiente diagrama muestra cómo se utilizan los esquemas en este flujo:

![El flujo entre un dispositivo y una aplicación en {{site.data.keyword.iot_short_notm}}.](images/Information "The flow between a device and an application on {{site.data.keyword.iot_short_notm}}")

Los esquemas JSON se utilizan para definir y validar el formato de los sucesos entrantes y el [estado del dispositivo](#key_concepts). Para obtener más información sobre estos esquemas, consulte [Esquemas](#resources).

## Conceptos clave
{: #key_concepts}

La característica de correlación de interfaces amplía el concepto actual de [tipo de dispositivo](#resources) añadiendo un recurso de interfaz física y un recurso de interfaz de aplicación para controlar mejor los flujos de datos a través de {{site.data.keyword.iot_short_notm}}.

En el diagrama siguiente se muestra la correlación lógica entre dispositivos y aplicaciones en {{site.data.keyword.iot_short_notm}} mediante el uso de [recursos](#resources):

![La correlación lógica entre un dispositivo y una aplicación en {{site.data.keyword.iot_short_notm}}.](images/im_mapping.svg "The logical mapping between a device and an application on {{site.data.keyword.iot_short_notm}}")

Correlación de interfaz hace referencia al concepto de estado de un dispositivo. El estado del dispositivo consta de un conjunto de propiedades que se han definido mediante la interfaz de la aplicación. Los valores más recientes de estas propiedades se almacenan en {{site.data.keyword.iot_short_notm}}, y se ponen a disponibilidad de la aplicación según demanda utilizando una API HTTP.

Para procesar los datos de los sucesos de entrada y correlacionar las propiedades del suceso de entrada con las propiedades de la interfaz de la aplicación, debe estar configurada la siguiente información:

- La estructura de uno o varios sucesos de entrada. El esquema del suceso define esta información.  Cada esquema de suceso define la estructura de un suceso de entrada y está asociado a un tipo de suceso. La interfaz física agrupa uno o varios tipos de suceso.

    La estructura y el formato de los datos contenidos en un suceso de dispositivo de entrada se definen mediante un archivo de esquema de sucesos que está en formato de esquema JSON. Puede cargar el archivo de esquema de suceso en {{site.data.keyword.iot_short_notm}} mediante un método POST para crear un recurso de esquema determinado. Para la versión Beta, todos los sucesos de entrada deben estar en formato JSON.

- La estructura del estado del dispositivo deseado. El esquema de la interfaz de la aplicación define esta información.

    El estado del dispositivo es una representación de la estructura de datos y los datos que recibirá la aplicación según su configuración como datos procedentes del dispositivo. Los valores de propiedades almacenados en el estado del dispositivo se actualizan como respuesta a un suceso de dispositivo de entrada. Se proporcionan los valores de estado del dispositivo más reciente según demanda mediante una API HTTP.

- Información sobre cómo correlacionar los sucesos de entrada con el estado del dispositivo preferido. Las correlaciones definen esta información.

    Para correlacionar los datos contenidos en las propiedades de un suceso de entrada con las propiedades correspondientes en la interfaz de la aplicación, debe crear una correlación. La correlación describe cómo actualizar las propiedades definidas por una interfaz de aplicación específica como respuesta a un suceso de entrada procedente de un dispositivo.


## Recursos
{: #resources}

Puede gestionar los recursos que se ilustran en los diagramas anteriores mediante API REST. Para obtener información sobre las API REST, consulte la documentación de la [{{site.data.keyword.iot_short_notm}} API REST HTTP](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html).

Recurso                        | Descripción       
------------- | ------------- | -------------  
Esquemas                         | Los esquemas JSON se utilizan para definir la estructura de los sucesos de entrada que se publican en {{site.data.keyword.iot_short_notm}} procedentes de los dispositivos y el estado de dispositivo deseado. Para obtener más información sobre el esquema JSON, consulte [Esquema JSON](http://json-schema.org/). En la correlación de interfaces, se hace referencia a dos esquemas JSON: esquemas de sucesos y esquemas de interfaz de aplicación. Los esquemas de sucesos se utilizan para definir la estructura de los sucesos que publica en {{site.data.keyword.iot_short_notm}} un dispositivo. La interfaz de aplicación hace referencia a los esquemas de interfaz de aplicación y se utilizan para definir la estructura del [estado del dispositivo](#key_concepts) que se almacena en {{site.data.keyword.iot_short_notm}}.
Tipo de suceso                         | Debe crear un tipo de suceso dentro de la organización para que {{site.data.keyword.iot_short_notm}} pueda procesar los datos contenidos en un suceso específico. Todos los tipos de suceso deben hacer referencia a un esquema de suceso. Para la versión Beta, todos los sucesos de entrada deben estar en formato JSON.   
Interfaz física                         | La interfaz física puede estar asociada a uno o varios tipos de suceso y define los tipos de suceso que están asociados con un tipo de dispositivo.  
Tipo de dispositivo                         | Cada dispositivo que está conectado a la plataforma Watson IoT está asociado a un tipo de dispositivo. Los tipos de dispositivos son grupos de dispositivos que comparten características o comportamientos. En la correlación de interfaces, el tipo de dispositivo se amplía para incluir una interfaz física para un dispositivo y una interfaz de aplicación que se puede utilizar para recuperar el estado del dispositivo. Un tipo de dispositivo se puede configurar con varias interfaces de aplicación. Para obtener más información sobre los tipos de dispositivo, consulte la sección sobre "Identificadores y tipos de dispositivo" de [Modelo de dispositivo](../reference/device_model.html#id_and_device_types).
Interfaz de aplicación                         | La interfaz de aplicación debe hacer referencia a un esquema de interfaz de aplicación. Dentro de la interfaz de aplicación, puede definir la estructura de los datos que se almacena como estado del dispositivo. El estado del dispositivo es una representación de la estructura de datos y los datos que recibirá la aplicación según su configuración como datos procedentes del dispositivo. Debe haber como mínimo una interfaz de aplicación asociada a un tipo de dispositivo para que se puedan definir correlaciones.
Correlaciones                         | Las Correlaciones definen la forma en que las propiedades asociadas con sucesos de entrada se correlacionan con las propiedades que se han definido en una determinada interfaz de aplicación. Una correlación debe especificar el identificador de la interfaz de aplicación a la que se aplica y dicha interfaz de aplicación debe estar asociada con el tipo de dispositivo al que se añade la correlación.


## Flujo de trabajo de alto nivel
{: #workflow}



### Acerca de esta tarea

Siga los pasos siguientes como ayuda para configurar los recursos que necesita empezar a correlacionar los datos del dispositivo mediante las interfaces.

Para ver detalles acerca de la API, consulte la documentación de la [{{site.data.keyword.iot_short_notm}} API REST HTTP](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html).
Para obtener más información sobre cada uno de los pasos, consulte el [Caso de ejemplo](#scenario) o utilice los enlaces para ir directamente a un paso específico del caso de ejemplo.

### Configure el entorno para empezar a utilizar interfaces para correlacionar datos del dispositivo

1.  Si es necesario, añada un tipo de dispositivo y un dispositivo

  1. Para crear un tipo de dispositivo, utilice el método POST de la API REST con el URI siguiente:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types
      ```
  2.  Añada un dispositivo si es necesario.  
Para obtener más información sobre cómo añadir un tipo de dispositivo y un dispositivo, consulte [Conexión de dispositivos](../iotplatform_task.html#devices)

2. Cree una interfaz física

  1. [Cree un archivo de esquema de suceso](#step1). El archivo de esquema de suceso es un archivo .JSON local que define la estructura y el formato de un suceso de entrada.

  2. [Cree un recurso de esquema de suceso para el tipo de suceso](#step2) mediante el método POST de la API REST con el URI siguiente:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
      ```  

  3. [Cree un tipo de suceso que haga referencia al esquema de suceso](#step3) mediante el método POST de la API REST con el URI siguiente:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/event/types
      ```
      Añada el tipo de suceso al esquema de suceso utilizando el identificador de esquema que se ha devuelto como respuesta al método POST utilizado para crear el recurso de esquema de suceso.

  4. [Cree una interfaz física](#step7) utilizando el método POST de la API REST con el URI siguiente:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces
        ```

   5. [Añada el tipo de suceso a la interfaz física](#step8) utilizando el método POST de la API REST con el URI siguiente:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/{physicalInterfaceId}/events
        ```

       Añada el tipo de suceso a la interfaz física utilizando el valor *eventId* del tema y el identificador de tipo de suceso *eventTypeId* que se ha devuelto como respuesta al método POST utilizado para crear el tipo de suceso.       

3. Añada la interfaz física al tipo de dispositivo       

      [Actualice el tipo de dispositivo para que se conecte a la interfaz física](#step9) utilizando el método PUT de la API REST con el URI siguiente:
     ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
     ```

4. Cree una interfaz de aplicación

  1. [Cree un archivo de esquema de interfaz de aplicación](#step4). Un archivo de esquema de interfaz de aplicación es un archivo .JSON local que define el estado del dispositivo.

  2. [Cree un recurso de esquema de interfaz de aplicación](#step5) utilizando el método POST de la API REST con el URI siguiente:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
        ```     

  3. [Cree una interfaz de aplicación que haga referencia al esquema de interfaz de aplicación](#step6) mediante el método POST de la API REST con el URI siguiente:
         ```
         https://**orgId**.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces
         ```  

        La interfaz de aplicación hace referencia al esquema de interfaz de aplicación utilizando el identificador de esquema que se ha devuelto como respuesta al método POST utilizado para crear el recurso de esquema de la interfaz de aplicación.

  4. [Añada la interfaz de aplicación a un tipo de dispositivo](#step10) utilizando el método POST de la API REST con el URI siguiente:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/types/{typeId}/applicationinterfaces
        ```

        Añada la interfaz de aplicación al tipo de dispositivo utilizando la respuesta al método POST utilizado para crear la interfaz de la aplicación.

5. Defina las correlaciones para el tipo de dispositivo

  [Defina las correlaciones para correlacionar las propiedades del suceso de entrada con las propiedades de la interfaz de aplicación](#step11) utilizando el método POST de la API REST con el URI siguiente:       
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/mappings/{applicationInterfaceId}
      ```

6. Despliegue la configuración asociada con el tipo de dispositivo

  [Despliegue la configuración](#step15) en {{site.data.keyword.iot_short_notm}} utilizando el método PATCH de la API REST con el URI siguiente:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
      ```

7. Compruebe que los sucesos del dispositivo correlacionado se publican en la interfaz de la aplicación

  1. [Publique un suceso de dispositivo de entrada](#step12).

  2. [Compruebe que el estado del dispositivo ha cambiado](#step13) utilizando el método GET de la API REST con el URI siguiente:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
        ```

## Caso de ejemplo
{: #scenario}

Utilice la siguiente información para crear un caso de ejemplo en el que dos sensores de temperatura publican sucesos en {{site.data.keyword.iot_short_notm}}. Uno sensor mide la temperatura en grados centígrados. El otro sensor mide la temperatura en grados Fahrenheit. Estas lecturas se correlacionan con una única lectura de temperatura que está en grados centígrados. Cuando estos dispositivos publican una nueva lectura de temperatura, el valor de la propiedad asociada al estado del dispositivo se modifica.

### Requisitos previos

Debe tener una instancia de organización de {{site.data.keyword.iot_short_notm}} y una clave de API o una señal correspondiente a la organización. Para obtener más información sobre claves de API y señales, consulte [API REST HTTP para aplicaciones](../applications/api.html#authentication).

### Acerca de este caso de ejemplo

En este caso de ejemplo, se configuran dos dispositivos.

Uno dispositivo se denomina *TemperatureSensor1*. Este dispositivo publica los sucesos de temperatura que se miden en grados centígrados. El suceso de temperatura se publica en el tema `iot-2/evt/tevt/fmt/json` y tiene la siguiente carga útil de ejemplo:
```
{
  "t" : 34.5
}
```

**Nota:** el identificador de suceso es *tevt*. Este identificador es necesario cuando se añade un suceso de temperatura de este tipo a la interfaz física y cuando se definen las correlaciones para correlacionar una propiedad asociada a un suceso de entrada de este tipo a una propiedad de la interfaz de aplicación. En este caso de ejemplo, la propiedad definida en la interfaz de la aplicación se denomina **temperature**.

El otro dispositivo se denomina *TemperatureSensor2*. Este dispositivo publica los sucesos de temperatura que se miden en grados Fahrenheit. El suceso de temperatura se publica en el tema `iot-2/evt/tempevt/fmt/json` y tiene la siguiente carga útil de ejemplo:
```
{
  "temp" : 72.55
}
```

**Nota:** el identificador de suceso es *tempevt*. Este identificador es necesario cuando se añade un suceso de temperatura de este tipo a la interfaz física y cuando se definen las correlaciones para correlacionar una propiedad asociada a un suceso de entrada de este tipo a una propiedad de la interfaz de aplicación. En este caso de ejemplo, la propiedad definida en la interfaz de la aplicación se denomina **temperature**.

También se configura una interfaz de aplicación. Esta interfaz de aplicación representa el estado de los dispositivos de este tipo en la estructura siguiente:
```
{
  "temperature" : <valor temperatura actual en grados centígrados>
  }
```
Esta configuración significa que puede configurar la aplicación para que procese el valor asociado con **temperature** en lugar de configurar la aplicación para que procese el valor asociado con **t** y procese el valor asociado con **temp** después de convertir dicho valor a grados centígrados.

## Pasos

Utilice la siguiente información para configurar el caso de ejemplo utilizando interfaces.

### Si es necesario, añada un tipo de dispositivo y un dispositivo
{: #step14}

En este caso de ejemplo, se presupone que hay dos tipos de dispositivo y dos instancias de dispositivo. La instancia de dispositivo *TemperatureSensor1* está asociado al tipo de dispositivo *EnvSensor1*. La instancia de dispositivo *TemperatureSensor2* está asociado al tipo de dispositivo *EnvSensor2*.

Para obtener información sobre cómo utilizar las API REST para añadir un tipo de dispositivo, consulte la documentación de la [{{site.data.keyword.iot_short_notm}} API REST HTTP](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Types).

### Cree un archivo de esquema de suceso
{: #step1}

Para este caso de ejemplo, cree dos archivos de esquema de suceso para definir la estructura de cada uno de los sucesos de temperatura de entrada.

En el siguiente ejemplo se muestra cómo crear un archivo de esquema denominado *tEventSchema.json*. Este archivo define la estructura de un suceso de entrada procedente de un sensor de temperatura que mide la temperatura en grados centígrados:

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor1 tEvent Schema",
  "description" : "define la estructura de un suceso de temperatura en grados centígrados",
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

### Cree un recurso de esquema de suceso para el tipo de suceso
{: #step2}

Para crear un recurso de esquema de suceso, utilice la siguiente API:

```
POST /schemas
```
Para ver más detalles, consulte la documentación de la [{{site.data.keyword.iot_short_notm}} API REST HTTP](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas).

En el siguiente ejemplo se muestra cómo utilizar cURL para crear el recurso de esquema de suceso *tEventSchema.json*:

```
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

### Cree un tipo de suceso que haga referencia al esquema de suceso
{: #step3}

Cada tipo de suceso hace referencia al esquema de suceso relevante que se ha creado en el ejemplo anterior utilizando el identificador de esquema devuelto como respuesta al método POST utilizado para crear el recurso de esquema de suceso.

Para crear un tipo de suceso, utilice la siguiente API:

```
POST /event/types
```

Para ver más detalles, consulte la documentación de la [{{site.data.keyword.iot_short_notm}} API REST HTTP](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Event_Types).


El siguiente ejemplo muestra cómo utilizar cURL para crear un tipo de suceso para un suceso de temperatura que se mide en grados centígrados:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tEvent", "schemaId" : "5846cd7c6522050001db0e0d"}'
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
  "name" : "tempEvent",
  "refs" : {
    "schema" : "/schemas/5846cee36522050001db0e0e"
  },
  "updatedBy" : "a-8x7nmj-9iqt56kfil"
}
```
El identificador de tipo de suceso *5846d2846522050001db0e10* que se devuelve como respuesta al método POST se utiliza para añadir un tipo de suceso a la interfaz física.

### Cree una interfaz física
{: #step7}

Para crear una interfaz física, utilice la siguiente API:

```
POST /physicalinterfaces
```
Para ver más detalles, consulte la documentación de la [{{site.data.keyword.iot_short_notm}} API REST HTTP](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces).

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

### Añada el tipo de suceso a la interfaz física
{: #step8}

Para añadir un tipo de suceso a la interfaz física, utilice la siguiente API:

```
POST /physicalinterfaces/{physicalInterfaceId}/events
```
Para ver más detalles, consulte la documentación de la [{{site.data.keyword.iot_short_notm}} API REST HTTP](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces).

En este caso de ejemplo, se añaden los siguientes tipos de suceso a las interfaces físicas especificadas:
- El suceso de temperatura en grados centígrados *tevt* se añade a la interfaz física con el identificador *5847d1df6522050001db0e1a* utilizando el *eventId* procedente del tema y el valor de *eventTypeId* procedente de la creación del recurso de esquema de suceso.
- El suceso de temperatura en grados Fahrenheit *tempevt* se añade a la interfaz física con el identificador *5847d1df6522050001db0e1b* utilizando el *eventId* procedente del tema y el valor de *eventTypeId* procedente de la creación del recurso de esquema de suceso.


En el siguiente ejemplo se muestra cómo utilizar cURL para añadir el suceso de temperatura *tevt* a la interfaz física con el identificador *5847d1df6522050001db0e1a*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1a/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : "tevt", "eventTypeId" : "5846d0fd6522050001db0e0f"}'
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
  "eventId" : "tempevt"
}
```

### Actualice el tipo de dispositivo para que se conecte a la interfaz física
{: #step9}

Para actualizar un tipo de dispositivo, utilice la siguiente API:

```
PUT /device/types/{typeId}
```

Para ver más detalles, consulte la documentación de la [{{site.data.keyword.iot_short_notm}} API REST HTTP](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

En este caso de ejemplo, el tipo de dispositivo *EnvSensor1* se actualiza para conectarse a la interfaz física *5847d1df6522050001db0e1a* y el tipo de dispositivo *EnvSensor2* se actualiza para conectarse a la interfaz física *5847d1df6522050001db0e1b*.

En el siguiente ejemplo se muestra cómo utilizar cURL para actualizar el tipo de dispositivo *EnvSensor1*:

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "un sensor ambiental","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1a"}’
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
  --data '{"description" : "un sensor amb","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1b"}’
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



### Cree un archivo de esquema de interfaz de aplicación
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

### Cree un recurso de esquema de interfaz de aplicación
{: #step5}

Para crear un recurso de esquema de interfaz de aplicación, utilice la siguiente API:

```
POST /schemas
```
Para ver más detalles, consulte la documentación de la [{{site.data.keyword.iot_short_notm}} API REST HTTP](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas).

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

### Cree una interfaz de aplicación que haga referencia al esquema de interfaz de aplicación
{: #step6}

Para crear una interfaz de aplicación, utilice la siguiente API:

```
POST /applicationinterfaces
```
Para ver más detalles, consulte la documentación de la [{{site.data.keyword.iot_short_notm}} API REST HTTP](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Application_Interfaces).

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

### Añada la interfaz de aplicación a un tipo de dispositivo
{: #step10}

Para añadir una interfaz de aplicación a un tipo de dispositivo, utilice la siguiente API:

```
POST /device/types/{typeId}/applicationinterfaces
```
Para ver más detalles, consulte la documentación de la [{{site.data.keyword.iot_short_notm}} API REST HTTP](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

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
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "interfaz de sensor ambiental"
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
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "interfaz de sensor ambiental"
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

### Defina las correlaciones para correlacionar las propiedades del suceso de entrada con las propiedades de la interfaz de aplicación
{: #step11}

Para correlacionar sucesos, utilice la siguiente API:

```
POST /device/types/{typeId}/mappings
```
Para ver más detalles, consulte la documentación de la [{{site.data.keyword.iot_short_notm}} API REST HTTP](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

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

### Despliegue la configuración
{: #step15}

Despliegue la configuración relacionada con la actualización de estado de dispositivo para cada tipo de dispositivo. Esta configuración incluye esquemas, tipos de suceso, interfaces físicas, interfaces de aplicación y correlaciones.

Para desplegar la configuración del tipo de dispositivo, utilice la siguiente API:

```
PATCH /device/types/{typeId}
```
Para ver más detalles, consulte la documentación de la [{{site.data.keyword.iot_short_notm}} API REST HTTP](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

En este caso de ejemplo, debemos desplegar la configuración para dos tipos de dispositivo.

En el siguiente ejemplo se muestra cómo utilizar cURL para desplegar la configuración para el tipo de dispositivo *EnvSensor1*:

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
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
 "message": "CUDRS0520I: La configuración de actualización de estado para tipo de dispositivo 'Envsensor2' se ha enviado correctamente para su despliegue", "details": {
    "id": "CUDRS0520I",
    "properties": ["EnvSensor2"]
  },
 "failures": []
}
```

### Publique un suceso de dispositivo de entrada
{: #step12}

Publique un suceso de temperatura *TemperatureSensor1* en el tema `iot-2/evt/tevt/fmt/json` y un suceso de temperatura *TemperatureSensor2* en el tema `iot-2/evt/tempevt/fmt/json`.

Para obtener información sobre cómo publicar un suceso de entrada procedente de un dispositivo, consulte [Conectividad de MQTT para las aplicaciones](../applications/mqtt.html#publishing_device_events).


### Compruebe que el estado del dispositivo se ha cambiado
{: #step13}

Para comprobar el estado del dispositivo, utilice la siguiente API:
```
GET /device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
```
Para ver más detalles, consulte la documentación de la [{{site.data.keyword.iot_short_notm}} API REST HTTP](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

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
