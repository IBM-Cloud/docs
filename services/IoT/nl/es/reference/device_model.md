---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Modelo del dispositivo
{: #device_model}
Última actualización: 13 de septiembre de 2016 {: .last-updated}

El modelo de dispositivo describe los metadatos y las características de gestión de un dispositivo. La base de datos del dispositivo del {{site.data.keyword.iot_full}} es el origen maestro de la información del dispositivo. Las aplicaciones y los dispositivos gestionados pueden enviar actualizaciones, incluidos los cambios de ubicación, o el progreso de una actualización de firmware, a la base de datos. Tan pronto como {{site.data.keyword.iot_short_notm}} reciba estas actualizaciones, se actualizará la base de datos del dispositivo y la información estará disponible para las aplicaciones.

**Nota:** Con la excepción de la ampliación de gestión, todo el modelo del dispositivo estará disponible para los dispositivos gestionados y no gestionados. Sin embargo, un dispositivo no gestionado no puede actualizar directamente su modelo de dispositivo en la base de datos.

## Identificación de dispositivo
{: #device_id}

Cada dispositivo tiene un atributo `typeId` y `deviceId`. Normalmente, el `typeId` representa el modelo del dispositivo, mientras que `deviceId` puede representar su número de serie. Dentro de su organización
{{site.data.keyword.iot_short_notm}}, la combinación de `typeId` y de `deviceId` debe ser exclusiva para cada dispositivo.

Además, el {{site.data.keyword.iot_short_notm}} construye otro identificador para cada dispositivo, que se denomina `clientId`. El `clientId` se basa en su `organizationId` y también los valores `typeId` y `deviceId` del dispositivo, y proporciona una forma de identificar inequívocamente un dispositivo individual.

Los caracteres que se pueden utilizar en estos identificadores están restringidos, de modo que sean compatibles con protocolos de comunicación y API REST. Los siguientes identificadores de dispositivos opcionales
también se utilizan con el protocolo de gestión de dispositivos:

- deviceInfo.manufacturer
- deviceInfo.serialNumber
- deviceInfo.model
- deviceInfo.deviceClass
- deviceInfo.description

Para obtener más información sobre los identificadores y las descripciones de sus identificadores comparativos en otros estándares de gestión de dispositivos, consulte [Atributos](#attributes).


## Tipos de identificadores y dispositivos
{: #id_and_device_types}

Cada dispositivo que esté conectado al {{site.data.keyword.iot_short_notm}} se asocia con un tipo de dispositivo. Los tipos de dispositivos son grupos de dispositivos que comparten características o comportamiento.

Un tipo de dispositivo tiene un conjunto de atributos. Cuando se añade un dispositivo al {{site.data.keyword.iot_short_notm}}, los atributos de su tipo de dispositivo se utilizan como una plantilla sustituida por atributos específicos del dispositivo. Por ejemplo, el tipo de dispositivo podría tener un valor para el atributo `deviceInfo.fwVersion`, que refleja la versión de firmware en el momento de la fabricación, y este valor se copiaría del tipo de dispositivo a los dispositivos a medida que se añaden. Cuando se añade un dispositivo, si el valor `deviceInfo.fwVersion` ya existe, no lo sustituirá el tipo de dispositivo.

Cuando se actualiza un tipo de dispositivo, sólo los nuevos dispositivos registrados heredan modificaciones en la plantilla de tipo de dispositivos. Los dispositivos existentes de un tipo de dispositivo no se ven afectados y permanecen
sin cambios.

## Atributos
{: #attributes}

La tabla siguiente muestra la lista de atributos que se pueden aplicar a dispositivos en el {{site.data.keyword.iot_short_notm}}. Asimismo, los atributos en cursiva pueden aplicarse también a tipos de dispositivo.

- API/DMA: Puede actualizarse mediante API/Agente de gestión de dispositivo

  - R: De solo lectura
  - W: Grabación y lectura
  - A: Anexo

Atributo                        | Tipo       | Descripción                                       | API | DMA   
------------- | ------------- | ------------- | ------------- | -------------  
 clientId                         | serie     | El ID de cliente utilizado con las conexiones MQTT          |  R  |     
 *typeId*                         | serie     | Tipo de dispositivo                                       |  R  |     
 deviceId                         | serie     | ID de dispositivo                                         |  R  |     
 classId                          | serie     | Clase de dispositivo ("Dispositivo" o "Pasarela")           |  R  |     
 gatewayTypeId                    | serie     | El ID de tipo de la pasarela que este dispositivo utiliza       |  R  |     
 gatewayId                        | serie     | El ID de dispositivo de la pasarela que este dispositivo utiliza     |  R  |     
 status.alert                     | booleano    | Si el dispositivo tiene una alerta                   |  W  |     
 *deviceInfo.serialNumber*        | serie     | Número de serie del dispositivo                   |  W  |  W    
 *deviceInfo.manufacturer*        | serie     | Fabricante del dispositivo                    |  W  |  W   
 *deviceInfo.model*               | serie     | Modelo del dispositivo                           |  W  |  W  
 *deviceInfo.deviceClass*         | serie     | Clase del dispositivo                           |  W  |  W  
 *deviceInfo.description*         | serie     | Nombre descriptivo del dispositivo                |  W  |  W  
 *deviceInfo.fwVersion*           | serie     | Versión de firmware que se sabe que está actualmente en el dispositivo    |  W  |  W  
 *deviceInfo.hwVersion*           | serie     | Versión de hardware del dispositivo                |  W  |  W  
 *deviceInfo.descriptiveLocation* | serie     | La ubicación descriptiva, como por ejemplo una sala, número de edificio o una región geográfica      |  W  |  W  
 *metadata*                       | complejo    | Metadatos de formato libre                                |  W  |  W  
 added.auth.id                    | serie     | ID que ha añadido el dispositivo                          |  R  |     
 added.dateTime                   | serie     | ISO8601 date-time: Fecha y hora a la que se ha añadido el dispositivo |  R  |     
 refs.diag.errorCodes             | serie     | URI de extensión diag para los códigos de error, si está presente |  R  |     
 refs.diag.logs                   | serie     | URI de extensión diag para los registros, si está presente        |  R  |     
 refs.location                    | serie     | URI de extensión de ubicación, si está presente             |  R  |     
 refs.mgmt                        | serie     | URI de extensión mgmt, si está presente                 |  R  |     



## Atributos ampliados
{: #extended_attributes}

Además de los atributos principales mencionados anteriormente en la sección Atributos, hay atributos adicionales que se tratan
como extensiones al modelo de dispositivo principal. Las consultas simples sobre el dispositivo devuelven información del modelo básico de dispositivo, pero no las ampliaciones. La información sobre las ampliaciones debe solicitarse de forma específica.


Nombre de extensión    | Prefijo de atributos | Objetivo      
------------- | ------------- | -------------                                         
 Diagnóstico       | diag                 | Registros de errores e información de diagnóstico                 
  Ubicación          | ubicación             | Ubicación del dispositivo, potencialmente actualizado de forma regular
 Gestión de dispositivos | gest                 | Acciones de gestión de dispositivos, por ejemplo, actualización de firmware       


### Ampliación de diagnóstico


Los atributos de diagnóstico son opcionales y solo están presentes en dispositivos con información de registro de errores. Estos atributos están pensados para diagnosticar problemas de los dispositivos, sin resolver problemas de conectividad en el {{site.data.keyword.iot_short_notm}}. Para poder recuperar la información en estos atributos, deben consultarse por separado, porque la información almacenada en estos atributos puede ser potencialmente muy grande.

La información de registro de diagnóstico es una matriz de entradas que puede tener entradas anexadas mediante una API; sin embargo, esto puede hacer que se pierdan las entradas anteriores para que el tamaño de los registros de diagnóstico siga siendo manejable. Cada entrada consta de un mensaje, una indicación de la gravedad, una indicación de fecha y hora y una matriz de bytes de datos opcional.


Atributo            | Tipo       | Descripción                                                 | API | DMA
------------- | ------------- | ------------- | ------------- | -------------
 diag.errorCodes[]    | matriz de </br> entero(s)  | Matriz de códigos de error                                        |  A  |  A  
 diag.log[]           | matriz      | Matriz de datos de diagnóstico                                    |  A  |  A  
 diag.log[].message   | serie     | Mensaje de diagnóstico                                          |     |     
 diag.log[].timestamp | serie     | ISO8601 date-time: fecha y hora de la entrada de registro               |     |     
 diag.log[].logData   | serie     | byte: Datos de diagnóstico, codificados en base64                      |     |     
 diag.log[].severity  | número     | Gravedad del mensaje 0: informativo, 1: aviso, 2: error |     |     


### Ampliación de ubicación

Estos atributos son opcionales y sólo están presentes para los dispositivos con información de ubicación. La información de ubicación se almacena de forma independiente para permitir el uso de mecanismos de almacenamiento más adaptados a la información dinámica en el caso de la información que se actualiza con frecuencia, por ejemplo, en el caso de un dispositivo móvil.

Para las soluciones que toman importancia significativa en actualizaciones de ubicación frecuentes, se espera que la ubicación se trate como parte de la carga útil de sucesos del dispositivo, lo que permite tasas de actualización superiores, almacenamiento histórico simple y análisis.


Atributo                 | Tipo   | Descripción                                             | API | DMA
------------- | ------------- | ------------- | ------------- | -------------
 location.longitude        | número | Longitud en grados decimales con WGS84                |  W  |  W  
 location.latitude         | número | Latitud en grados decimales con WGS84                 |  W  |  W  
 location.elevation        | número | Elevación en metros con WGS84                         |  W  |  W  
 location.measuredDateTime | serie |ISO8601 date-time: Fecha y hora de la medición de ubicación |  W  |  W  
 location.updatedDateTime  | serie | ISO8601 date-time: Fecha y hora                        |  R  |     
 location.accuracy         | número | Exactitud de la posición en metros                      |  W  |  W  


### Ampliación de gestión de dispositivos

Los atributos `mgmt.` sólo están presentes para dispositivos gestionados. Cuando un dispositivo gestionado pasa a estar inactivo, se convierte en no gestionado y se suprimen los atributos `mgmt.`. Los atributos `mgmt.` los establece {{site.data.keyword.iot_short_notm}} como resultado de procesar solicitudes de gestión de dispositivos. Estos atributos no se pueden grabar directamente utilizando la API.

Los dispositivos tienen un ciclo de vida de gestión, que está definido por su estado como dispositivos gestionados. El agente de gestión de dispositivos en el dispositivo se encarga de enviar una solicitud de gestión de dispositivo utilizando el protocolo de gestión de dispositivos. Para tratar con dispositivos anómalos en grandes poblaciones de dispositivos, se puede establecer un dispositivo gestionado para enviar una solicitud Gestionar dispositivo de forma regular, lo que permite al {{site.data.keyword.iot_short_notm}} tener en cuenta cuando un dispositivo pasa a estar inactivo. Para facilitar esta funcionalidad, la solicitud Gestionar dispositivo tiene un parámetro de ciclo de vida opcional. Cuando el {{site.data.keyword.iot_short_notm}} reciba una solicitud Gestionar dispositivo con un ciclo de vida, calcula el tiempo antes del cual se necesita otra solicitud Gestionar dispositivo y la almacena en el atributo `mgmt.dormantDateTime`.


Atributo                      | Tipo    | Descripción                                            | API | DMA
------------- | ------------- | ------------- | ------------- | -------------
 mgmt.dormant                   | booleano | Si el dispositivo se ha vuelto inactivo                  |  R  |     
 mgmt.dormantDateTime           | serie  | ISO8601 date-time: Fecha y hora a las que el dispositivo gestionado pasará a estar inactivo   |  R  |     
 mgmt.lastActivityDateTime      | serie  | ISO8601 date-time: Fecha y hora de la actividad más reciente, actualizado de forma periódica    |  R  |     
 mgmt.supports.deviceActions    | booleano | Si el dispositivo admite las acciones de reinicio y restauración a configuración de fábrica  |  R  |     
 mgmt.supports.firmwareActions  | booleano | Si el dispositivo admite las acciones de descarga de firmware y actualización de firmware    |  R  |     
 mgmt.firmware.version          | serie  | Versión del firmware en el dispositivo              |  R  |  W  
 mgmt.firmware.name             | serie  | Nombre del firmware que se va a utilizar en el dispositivo      |  R  |  W  
 mgmt.firmware.uri              | serie  | URI desde el que se puede descargar la imagen de firmware |  R  |  W  
 mgmt.firmware.verifier         | serie  | Verificador, como una suma de comprobación, de la imagen de firmware para validar su integridad |  R  |  W  
 mgmt.firmware.state            | número  | Indica el estado de la descarga de firmware               |  R  |  W  
 mgmt.firmware.updateStatus     | número  | Indica el estado de la actualización                     |  R  |  W  
 mgmt.firmware.updatedDateTime  | serie  | ISO8601 date-time: Fecha de la actualización más reciente                 |  R  |     
