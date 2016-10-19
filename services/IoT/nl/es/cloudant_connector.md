---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Conexión y configuración de un servicio de historian mediante un {{site.data.keyword.cloudant}}  
{: #cloudant_main}
Última actualización: 16 de septiembre de 2016
{: .last-updated}

La conexión de un servicio {{site.data.keyword.cloudantfull}} a {{site.data.keyword.iot_full}} le permite almacenar y acceder a los datos de dispositivo. Los datos de dispositivo se almacenan en bases de datos diarias, semanales o mensuales en función del intervalo de receptáculo seleccionado.

Al empezar a utilizar un {{site.data.keyword.cloudant}} para almacenar datos de dispositivos, se crearán automáticamente tres bases de datos, una para el intervalo de receptáculo actual, otra para el próximo intervalo, y una base de datos de configuración. Los documentos de diseño se pueden añadir a la base de datos de configuración y se copiarán a las nuevas bases de datos a medida que se creen. Cuando se alcanza el final de un intervalo, los datos de dispositivo se almacenan en la base de datos de receptáculo para el nuevo intervalo, y se creará una nueva base de datos para el intervalo siguiente.

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

Antes de conectar un {{site.data.keyword.cloudant}} al servicio de {{site.data.keyword.iot_short}}, lleve a cabo las tareas siguientes:

- Configure un {{site.data.keyword.cloudant}} en el mismo espacio de Bluemix como su {{site.data.keyword.iot_short_notm}} utilizando el Catálogo de Bluemix.

Asegúrese de que tenga privilegios de desarrollador en la organización de Bluemix y que haya iniciado sesión mediante Bluemix. Si no ha iniciado sesión a través de Bluemix, o no tiene privilegios de desarrollador en esta organización de Bluemix, no podrá autorizar el enlace de {{site.data.keyword.cloudant}} y {{site.data.keyword.iot_short_notm}}.

Siga estos pasos para conectar un {{site.data.keyword.cloudant}}:

1. En el panel de control de {{site.data.keyword.iot_short}}, pulse **Extensiones** en la barra de navegación.
2. En el mosaico Almacenamiento de datos históricos, pulse **Configuración**.
2. Todos los servicios disponibles de {{site.data.keyword.cloudant}} del mismo espacio de Bluemix que el servicio de {{site.data.keyword.iot_short}} se listan en la sección Configurar el almacenamiento de datos históricos.
3. Seleccione el servicio de {{site.data.keyword.cloudant}} que desea conectar.
4. Seleccione las opciones de configuración de {{site.data.keyword.cloudant}}:

  a. Seleccione un intervalo de receptáculo. El intervalo del receptáculo controla la frecuencia con la que se crean las nuevas bases de datos para almacenar los datos de dispositivos. Se crean nuevos receptáculos a medianoche en el huso horario seleccionado utilizando el intervalo de receptáculo seleccionado.

  b. Seleccione un huso horario. La hora del huso horario seleccionado se utilizará para determinar qué datos de dispositivo de receptáculo se deben colocar, no la hora local en el dispositivo. Las indicaciones de fecha y hora en los datos de dispositivo que se envían al {{site.data.keyword.cloudant}} se convertirán en el huso horario seleccionado a la hora de decidir en qué base de datos se especificarán los datos.

  c. Elija un nombre de base de datos. El nombre de la base de datos será `Iotp_<orgID>_<choice>_<bucket_name>` donde `<orgID>` es el ID de la organización, `<choice>` es su opción de nombre de base de datos, y `<bucket_name>` es una serie que define si la base de datos utiliza un intervalo de receptáculo diario, semanal o mensual. El `<bucket_name>` utiliza el formato siguiente.

  Para intervalos de receptáculo diarios, `<bucket_name>` será `aaaa-mm-dd`.
  Para intervalos de receptáculos semanales, `<bucket_name>` será `aaaa-www`, donde `www` indica un número de semana, por ejemplo `2016-w03`
  Para intervalos de receptáculo mensual, `<bucket_name>` será `aaaa-mm`.

5. Pulse en **Autorizar**.
6. Pulse **Confirmar** en el recuadro de diálogo de la autorización.

Sus datos de dispositivo están almacenados ahora en el {{site.data.keyword.cloudant}}.

## Creación de nuevos documentos de diseño  
{: #design_docs}

Los nuevos documentos de diseño se encuentran en la base de datos de configuración, y se copian a cada base de datos creada. El nombre de la base de datos de configuración es `Iotp_<orgid>_<choice>_configuration
` que utiliza los mismos parámetros que los nombres de base de datos descritos en el paso 3b en la sección Antes de empezar.

Los documentos de diseño predeterminados contenidos en {{site.data.keyword.iot_short_notm}} implementan consultas disponibles en el historian actual, aparte de la función de resumen.

Se pueden añadir documentos de diseño adicionales a la base de datos de configuración, y se copiarán a las nuevas bases de datos de intervalo de receptáculo que se crean. Para añadir documentos de diseño a la base de datos de configuración, consulte la [Documentación de la API Cloudant](https://docs.cloudant.com/document.html).

<!--  # Related links
{: #rellinks}
* [Querying your {{site.data.keyword.cloudant}}](link) -->
