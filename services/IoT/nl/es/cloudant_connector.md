---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Conexión y configuración de un servicio de historian mediante un {{site.data.keyword.cloudant_short_notm}}  
{: #cloudant_main}

La conexión de un servicio {{site.data.keyword.cloudantfull}} a {{site.data.keyword.iot_full}} le permite almacenar y acceder a los datos de dispositivo. Los datos de dispositivo se almacenan en bases de datos diarias, semanales o mensuales en función del intervalo de receptáculo seleccionado.

Al empezar a utilizar un {{site.data.keyword.cloudant_short_notm}} para almacenar datos de dispositivos, se crearán automáticamente tres bases de datos, una para el intervalo de receptáculo actual, otra para el próximo intervalo, y una base de datos de configuración. Los documentos de diseño se pueden añadir a la base de datos de configuración y se copiarán a las nuevas bases de datos a medida que se creen. Cuando se alcanza el final de un intervalo, los datos de dispositivo se almacenan en la base de datos de receptáculo para el nuevo intervalo, y se creará una nueva base de datos para el intervalo siguiente.

Cuando se envían datos de dispositivo a una base de datos, se pueden almacenar de una de estas dos formas. Si los datos son JSON válidos y el formato del suceso de dispositivos se establece en `JSON`, los datos del dispositivo se almacenarán en el formato siguiente:

```json

{
  "_id": "78bf4380-3311-11e6-a747-d7b140d1a70a",
  "_rev": "2-d13912b7c089f060a4ba7369fa86e46f",
  "typeId": "t",
  "deviceType": "0",
  "eventType": "json_payload",
  "format": "json",
  "timestamp": "2016-06-15T16:54:41.464+01",
  "data": {
    "a": 22
  }
}

```

Si los datos de dispositivo no son JSON válidos o si el formato no se establece en `JSON`, los datos de dispositivo se almacenarán como una serie codificada base64 en el campo `carga útil` en el formato siguiente:

```json

{
  "_id": "80f1ce10-3311-11e6-a747-d7b140d1a70a",
  "_rev": "1-bfcbf1e74389fe4188a9425c0cd2575a",
  "payload": "eHh4eHg=",
  "typeId": "t",
  "deviceType": "0",
  "eventType": "non_json_payload",
  "format": "notjson",
  "timestamp": "2016-06-15T16:54:55.217+01"
}

```

## Antes de empezar  
{: #byb}

Antes de conectar un {{site.data.keyword.cloudant_short_notm}} al servicio de {{site.data.keyword.iot_short}}, lleve a cabo las tareas siguientes:

- Configure un {{site.data.keyword.cloudant_short_notm}} en el mismo espacio de Bluemix como su {{site.data.keyword.iot_short_notm}} utilizando el Catálogo de Bluemix.

Asegúrese de que tenga privilegios de desarrollador en la organización de Bluemix y que haya iniciado sesión mediante Bluemix. Si no ha iniciado sesión a través de Bluemix, o no tiene privilegios de desarrollador en esta organización de Bluemix, no podrá autorizar el enlace de {{site.data.keyword.cloudant_short_notm}} y {{site.data.keyword.iot_short_notm}}.

Siga estos pasos para conectar un {{site.data.keyword.cloudant_short_notm}}:

1. En el panel de control de {{site.data.keyword.iot_short}}, pulse **Extensiones** en la barra de navegación.
2. En el mosaico Almacenamiento de datos históricos, pulse **Configuración**.
2. Todos los servicios disponibles de {{site.data.keyword.cloudant_short_notm}} del mismo espacio de Bluemix que el servicio de {{site.data.keyword.iot_short}} se listan en la sección Configurar el almacenamiento de datos históricos.
3. Seleccione el servicio de {{site.data.keyword.cloudant_short_notm}} que desea conectar.
4. Seleccione las opciones de configuración de {{site.data.keyword.cloudant_short_notm}}:

  a. Seleccione un intervalo de receptáculo. El intervalo del receptáculo controla la frecuencia con la que se crean las nuevas bases de datos para almacenar los datos de dispositivos. Se crean nuevos receptáculos a medianoche en el huso horario seleccionado utilizando el intervalo de receptáculo seleccionado.

  b. Seleccione un huso horario. La hora del huso horario seleccionado se utilizará para determinar qué datos de dispositivo de receptáculo se deben colocar, no la hora local en el dispositivo. Las indicaciones de fecha y hora en los datos de dispositivo que se envían al {{site.data.keyword.cloudant_short_notm}} se convertirán en el huso horario seleccionado a la hora de decidir en qué base de datos se especificarán los datos.

  c. Elija opciones que determinen el nombre de base de datos. El nombre de la base de datos será `iotp_<orgID>_<dbname>_<bucket_name>`, donde:

 +  * `<orgID>` es el ID de organización.
 +  * `<dbname>` es su opción para esta parte de nombre de base de datos controlados por el campo `Nombre de base de datos`.
 +  * `<bucket_name>` es una serie determinada por la selección para el campo `Intervalo de receptáculo`:
 +    * Para los intervalos de receptáculo `day`, `<bucket_name>` será `aaaa-mm-dd`.  Por ejemplo, `2016-07-06` para sucesos el 6 de julio de 2016.
 +    * Para intervalos de receptáculo `week`, `<bucket_name>` será `aaaa-'w'ww` donde `'w'ww` indica un número de semana.  Por ejemplo, `2016-w03` para sucesos en la tercera semana de 2016.
 +    * Para intervalos de receptáculos `month`, `<bucket_name>` será `aaaa-mm`.  Por ejemplo, `2016-07` para sucesos en julio de 2016.

5. Pulse en **Autorizar**.
6. Pulse **Confirmar** en el recuadro de diálogo de la autorización.

Sus datos de dispositivo están almacenados ahora en el {{site.data.keyword.cloudant}}.

## Recetas sobre la utilización del servicio histórico  
{: #recipes}

En las siguientes recetas se describe cómo utilizar {{site.data.keyword.cloudant_short_notm}} como almacén histórico para {{site.data.keyword.iot_short}}:

- En la receta sobre cómo [Configurar {{site.data.keyword.cloudant_short_notm}} como almacén de datos históricos para {{site.data.keyword.iot_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/cloudant-nosql-db-as-historian-data-storage-for-ibm-watson-iot-parti/){: new_window} se describe la forma en que se almacenan los datos en {{site.data.keyword.cloudant_short_notm}} y se muestra cómo configurar y almacenar datos de dispositivos en {{site.data.keyword.cloudant_short_notm}} como almacén de datos históricos. 

- En la receta sobre [Consulta y proceso de datos de dispositivos de {{site.data.keyword.iot_short}} desde {{site.data.keyword.cloudant_short_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/cloudant-nosql-db-as-historian-data-storage-for-ibm-watson-iot-partii){: new_window} se muestra cómo consultar y realizar operaciones de proceso de datos sobre datos de dispositivos almacenados en {{site.data.keyword.cloudant_short_notm}}.

- En la receta sobre cómo [Visualizar datos de dispositivos Watson IoT Device Data almacenados en una base de datos Cloudant NoSQL ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/?post_type=pnext_tutorial&p=27327){: new_window} se muestra cómo establecer un enlace entre las tarjetas de gráficos de líneas y el almacén de datos históricos para mostrar datos de dispositivos en el panel de control de la plataforma Watson IoT. 


## Creación de nuevos documentos de diseño  
{: #design_docs}

Los nuevos documentos de diseño se encuentran en la base de datos de configuración, y se copian a cada base de datos creada. El nombre de la base de datos de configuración es `iotp_<orgid>_<choice>_configuration
` que utiliza los mismos parámetros que los nombres de base de datos descritos en el paso 3b en la sección Antes de empezar.

Los documentos de diseño predeterminados contenidos en {{site.data.keyword.iot_short_notm}} implementan consultas disponibles en el historian actual, aparte de la función de resumen.

Se pueden añadir documentos de diseño adicionales a la base de datos de configuración, y se copiarán a las nuevas bases de datos de intervalo de receptáculo que se crean. Para añadir documentos de diseño a la base de datos de configuración, consulte la [Documentación de la API Cloudant ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.cloudant.com/document.html){: new_window}.

<!--  # Related links
{: #rellinks}
* [Querying your {{site.data.keyword.cloudant_short_notm}}](link) -->
