---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Formato de registro de Kibana para contenedores Docker
{: #kibana_log_format_containers}

Puede configurar Kibana para que muestre los campos siguientes para cada entrada de registro en la página *Descubrir*:
{:shortdesc}

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


