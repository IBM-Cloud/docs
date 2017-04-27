---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Formato de registro de Kibana para aplicaciones de Cloud Foundry
{: #kibana_log_format_cf}

Puede configurar Kibana para que muestre los campos siguientes para cada entrada de registro en la página *Descubrir*:{:shortdesc}

| Campo | Descripción |
|-------|-------------|
| @timestamp | `aaaa-MM-ddTHH:mm:ss:SS-0500`  <br> La hora del suceso registrado. <br> La indicación de fecha y hora se define hasta en milisegundos. |
| @version | Versión del suceso. |
| ALCH_TENANT_ID | ID del espacio de {{site.data.keyword.Bluemix_notm}}.  |
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
| source_id | El componente que genera registros. <br> En la siguiente lista se describen los registros de cada componente: <br> * **API**: Respuestas registradas a llamadas de API que solicitan un cambio en el estado de la app.<br> * **APP**: Respuestas registradas procedentes de la app.<br> * **CELL**: Respuestas registradas procedentes de la célula de Diego que indican cuándo se inicia, se detiene o se cuelga una app<br> * **LGR**: Respuestas registradas de loggregator que indican problemas con el proceso de registro.<br> * **RTR**: Respuestas registradas del componente direccionador cuando direcciona solicitudes HTTP a la app.<br> * **SSH**: Respuestas registradas procedentes de la célula de Diego cuando un usuario accede a un contenedor de app con el mandato `cf ssh`. <br> * **STG**: Respuestas registradas procedentes de la célula de Diego o de Droplet Execution Agent cuando la app se transfiere o se vuelve a transferir. |
| nombre_espacio | El nombre del espacio de {{site.data.keyword.Bluemix_notm}} en el que se transfiere la app. |
| timestamp | La hora del suceso registrado. La indicación de fecha y hora se define hasta en milisegundos. |




