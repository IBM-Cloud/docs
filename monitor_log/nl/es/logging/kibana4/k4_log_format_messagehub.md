---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Formato de registro de Kibana para Message Hub
{: #kibana_log_format_messagehub}

Puede configurar Kibana para que muestre los campos siguientes para cada entrada de registro en la página *Descubrir*:
{:shortdesc}

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
{: caption="Tabla 1. Campos para los sucesos de MessageHub " caption-side="top"}

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
