---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Formatos de registro de Kibana
{: #kibana_formats}

Puede configurar Kibana para que visualice en la página *Descubrir* distintos campos para cada entrada de registro.
{:shortdesc}



## Formato de registro de Kibana para aplicaciones de Cloud Foundry
{: #kibana_log_format_cf}

Puede configurar Kibana para que muestre los campos siguientes para cada entrada de registro en la página *Descubrir*:

| Campo | Descripción |
|-------|-------------|
| @timestamp | `aaaa-MM-ddTHH:mm:ss:SS-0500`  <br> La hora del suceso registrado. <br> La indicación de fecha y hora se define hasta en milisegundos. |
| @version | Versión del suceso. |
| ALCH_TENANT_ID | ID del espacio de {{site.data.keyword.Bluemix_notm}}. |
| \_id | El ID exclusivo del documento de registro. |
| \_index | El índice de la entrada de registro. |
| \_type | El tipo de registro; por ejemplo, *syslog*. |
| nombre_app | El nombre de la aplicación de {{site.data.keyword.Bluemix_notm}}. |
| application_id | El ID exclusivo de la aplicación de {{site.data.keyword.Bluemix_notm}}. |
| host | El nombre de la aplicación que ha generado los datos del registro. |
| instance_id | El ID de instancia de la instancia de aplicación que ha generado los datos de registro. |
| loglevel | La gravedad del suceso registrado. |
| message | Mensaje emitido por el componente. <br> El mensaje varía en función del contexto. |
| message_type | La secuencia en la que se escribe el mensaje de registro. <br> * **OUT** se refiere a la secuencia de stdout <br> * **ERR** se refiere a la secuencia de stderr. |
| org_id | El ID exclusivo de la organización de {{site.data.keyword.Bluemix_notm}} |
| org_name | El nombre de la organización de {{site.data.keyword.Bluemix_notm}} en la que se transfiere la app. |
| origin | Componente en el que se ha originado el suceso. |
| source_id | El componente que genera registros. <br> En la siguiente lista se describen los registros de cada componente: <br> * **API**: Respuestas registradas a llamadas de API que solicitan un cambio en el estado de la app. <br> * **APP**: Respuestas registradas procedentes de la app. <br> * **CELL**: Respuestas registradas procedentes de la célula de Diego que indican cuándo se inicia, se detiene o se cuelga una app <br> * **LGR**: Respuestas registradas de loggregator que indican problemas con el proceso de registro. <br> * **RTR**: Respuestas registradas del componente direccionador cuando direcciona solicitudes HTTP a la app. <br> * **SSH**: Respuestas registradas procedentes de la célula de Diego cuando un usuario accede a un contenedor de app con el mandato `cf ssh`. <br> * **STG**: Respuestas registradas procedentes de la célula de Diego o de Droplet Execution Agent cuando la app se transfiere o se vuelve a transferir. |
| nombre_espacio | El nombre del espacio de {{site.data.keyword.Bluemix_notm}} en el que se transfiere la app. |
| timestamp | La hora del suceso registrado. La indicación de fecha y hora se define hasta en milisegundos. |
{: caption="Tabla 1. Campos para apps de CF" caption-side="top"}



## Formato de registro de Kibana para contenedores Docker
{: #kibana_log_format_containers}

Puede configurar Kibana para que muestre los campos siguientes para cada entrada de registro en la página *Descubrir*:

| Campo | Descripción |
|-------|-------------|
| @timestamp | `aaaa-MM-ddTHH:mm:ss:SS-0500`  <br> La hora del suceso registrado. <br> La indicación de fecha y hora se define hasta en milisegundos. |
| @version | Versión del suceso. |
| ALCH_TENANT_ID | ID del espacio de {{site.data.keyword.Bluemix_notm}}. |
| \_id | El ID exclusivo del documento de registro. |
| \_index | El índice de la entrada de registro. |
| \_type | El tipo de registro; por ejemplo, *logs*. |
| group_id | ID de grupo <br> * Para un único contenedor, el valor es **0000**. <br> * Para un grupo de contenedores, el valor es el GUID del grupo.  |
| host | Nombre del host en el que se ejecuta el contenedor. |
| instance | GUID de la instancia para un único contenedor. Lista de los ID de instancia para un grupo de contenedores.|
| log | Mensaje abreviado. |
| message | Mensaje completo. |
| path | Vía de acceso y nombre de registro en el que se encuentra el registro dentro del contenedor. |
| stream | Especifica el tipo de registro: stdout, stderr |
| time | La fecha y hora en que se ha producido el suceso. La indicación de fecha y hora se define hasta en milisegundos.|
| timestamp | La fecha y hora del suceso registrado. La indicación de fecha y hora se define hasta en milisegundos. |
{: caption="Tabla 1. Campos para contenedores Docker" caption-side="top"}


## Formato de registro de Kibana para Message Hub
{: #kibana_log_format_messagehub}

Puede configurar Kibana para que muestre los campos siguientes para cada entrada de registro en la página *Descubrir*:

| Campo | Descripción |
|-------|-------------|
| @timestamp | `aaaa-MM-ddTHH:mm:ss:SS-0500`  <br> La hora del suceso registrado. <br> La indicación de fecha y hora se define hasta en milisegundos. |
| @version | Versión del suceso. |
| ALCH_TENANT_ID | ID del espacio de {{site.data.keyword.Bluemix_notm}}. |
| \_id | El ID exclusivo del documento de registro. |
| \_index | El índice de la entrada de registro. |
| \_type | El tipo de registro; por ejemplo, *syslog*. |
| loglevel | La gravedad del suceso registrado; por ejemplo, **Info**. |
| module | Este campo se establece en **MessageHub**. |
{: caption="Tabla 1. Campos para los sucesos de MessageHub" caption-side="top"}

Ejemplo de una entrada de registro:

```
March 8th 2017, 17:15:16.454	

message:
    Creating topic ABC
@version:
    1
@timestamp:
    March 8th 2017, 17:15:16.454
loglevel:
    Info
module:
    MessageHub
ALCH_TENANT_ID:
    3d8d2eae-f3f0-44f6-9717-126113a00b51
&#95;id:
    AVqu6vJl1zcfr8KYMI95
&#95;type:
    logs
&#95;index:
    logstash-2017.03.08
```
