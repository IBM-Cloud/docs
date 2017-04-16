---

copyright:
  years: 2016
lastupdated: "2016-12-09"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Guía de inicio con Compose for Elasticsearch
{: #getting-started-with-compose-for-elasticsearch}

{{site.data.keyword.composeForElasticsearch_full}} combina la potencia de un motor de búsqueda de texto completo con la fuerza de indexación de una base de datos de documentos JSON. Juntos, crean una herramienta potente para el análisis de datos enriquecidos en grandes volúmenes de datos. Con Elasticsearch, su búsqueda se puede puntuar para su exactitud, permitiéndole indagar en el conjunto de datos para las coincidencias casi exactas que no puede conseguir.
{:shortdesc}

**Nota:** Cualquier instancia de servicio de Compose proporcionada antes del 14 de septiembre de 2016 que siga activa se puede seguir utilizando y se puede acceder a ella directamente en [https://www.compose.com/](https://www.compose.com). Se puede acceder directamente a cualquier instancia de servicio de Compose que se proporcione desde este momento en adelante y se utilizará dentro de la cuenta de Bluemix.

Siga estos pasos para iniciarse a {{site.data.keyword.composeForElasticsearch}}:

1. [Cree una instancia de {{site.data.keyword.composeForElasticsearch}}](https://console.ng.bluemix.net/catalog/services/compose-for-elasticsearch/).

  Al crear una instancia del servicio, asegúrese de que elige un nombre para el servicio y un nombre de credencial. Deje el servicio desenlazado; puede conectar una aplicación al servicio más adelante utilizando las credenciales proporcionadas cuando se proporcione el servicio. Los distintos valores de credenciales se listan en la sección *Credenciales disponibles*.

2. Conéctese al servicio de {{site.data.keyword.composeForElasticsearch}}.

  Para conectar una app al servicio, utilice las credenciales creadas junto con el servicio. La app de ejemplo muestra cómo utilizar Node.js para conectar a un servicio de {{site.data.keyword.composeForElasticsearch}}.

  Descargue la app de ejemplo [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) y siga las instrucciones del archivo readme. A continuación, en la página de detalles de la aplicación en Bluemix, pulse **Ver APP** para ver el contenido del índice de *ejemplos*.

## Credenciales disponibles

Nombre de campo|Descripción
----------|-----------
`uri`|El URI que se utilizará al conectarse al servicio. Incluye el esquema (`https:`), el nombre de usuario y la contraseña del administrador, el nombre de host del servidor y el número de puerto al que se conecta.
`uri_direct_1`|Un URI alternativo que se puede utilizar al conectarse al servicio. Formateado en cuanto a `uri`.
`uri_health`|Un mandato `curl` que solicita el estado del clúster desde el primer haproxy.
`uri_health_1`|Un mandato `curl` que solicita el estado del clúster desde el segundo haproxy.
`ca_certificate_base64`|Un certificado firmado automáticamente que se utiliza para confirmar que una aplicación se está conectando al servidor apropiado. Está codificado como base64. Debe decodificar la clave antes de utilizarla, como se muestra en la aplicación de ejemplo.
`deployment_id`|Un identificador interno para el servicio, tal como se ha creado en Compose.
`db_type`|El tipo de base de datos que ofrece el servicio; en este caso, `elastic_search`.
`name`|El nombre del despliegue de la base de datos.
{: caption="Table 1. {{site.data.keyword.composeForElasticsearch}} credentials" caption-side="top"}

**Nota:** Dos portales `haproxy` proporcionan acceso al clúster Elasticsearch. Tanto `uri` como `uri_direct_1` pueden utilizarse para conectarse al clúster. En las aplicaciones, conmute entre `uri` y `uri_direct_1` para gestionar respuestas a fallos de conexión.

# Enlaces relacionados
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Artículos de Compose](https://www.compose.com/articles/){:new_window}

## Guías de aprendizaje y ejemplos
{: #samples}
* [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs){:new_window}

## Enlaces relacionados
{: #general}
* [Ayuda de Compose](https://help.compose.com/docs){:new_window}
