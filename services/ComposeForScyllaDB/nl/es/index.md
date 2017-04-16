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

# Iniciación a Compose for ScyllaDB
{: #getting-started-with-compose-for-scylladb}

ScyllaDB es un sustituto de la base de datos distribuida de columna ancha Cassandra. ScyllaDB está escrito en C++, en lugar de Java de Cassandra, para conseguir una mejor utilización de recursos, que puede llegar a un rendimiento diez veces superior en las pruebas de referencia. Además de mantener la compatibilidad con la herramienta Cassandra y los archivos de datos, ScyllaDB añade capacidades de ajuste automático. {{site.data.keyword.composeForScyllaDB_full}} amplía las capacidades de ScyllaDB gestionándolo para los usuarios, ofreciendo un sistema de despliegue sencillo y de escalado automático que proporcione alta disponibilidad y redundancia, además de copias de seguridad automatizadas.
{:shortdesc}

**Nota:** {{site.data.keyword.composeForScyllaDB_full}} no da acceso a la IU de Compose. Consulte [Componer en Bluemix Support](https://help.compose.com/docs/bluemix-compose-support) para obtener más detalles.

Siga estos pasos para iniciarse a {{site.data.keyword.composeForScyllaDB}}:

1. [Cree una instancia de {{site.data.keyword.composeForScyllaDB}}](https://console.ng.bluemix.net/catalog/services/compose-for-scylladb/).

   Al crear una instancia del servicio, seleccione un nombre para el servicio y un nombre de credencial. Deje el servicio desenlazado; puede conectar una aplicación al servicio más adelante utilizando las credenciales proporcionadas cuando se proporcione el servicio. Los distintos valores de credenciales se listan en la sección "Credenciales disponibles".

2. Conéctese al servicio de {{site.data.keyword.composeForScyllaDB}}.

   Para conectar una aplicación al servicio, utilice las credenciales creadas junto con el servicio.

   Descargue la aplicación de ejemplo [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) y siga las instrucciones del archivo readme. A continuación, en la página de detalles de la aplicación en la consola de Bluemix, pulse **Ver APP**.

   La aplicación de ejemplo muestra cómo utilizar Node.js para conectar a un servicio de {{site.data.keyword.composeForScyllaDB}}.


## Credenciales disponibles

Nombre de campo|Descripción
----------|-----------
`db_type`|El tipo de base de datos que ofrece el servicio, en este caso `scylla`.
`uri_cli_1`|Una línea de mandatos de shell `cqlsh` alternativa que se conecta a la instancia de la base de datos.
`maps`|Un mapa de conexión de ScyllaDB que proporciona la información que necesitan varios controladores para asociar direcciones IP internas con los nombres DNS externos de una base de datos de ScyllaDB.
`name`|El nombre del despliegue de la base de datos.
`uri_cli`|Una línea de mandatos de shell `cqlsh` que se conecta a la instancia de la base de datos.
`uri_direct_2`|Un URI alternativo que se puede utilizar para conectarse al servicio. Formateado en cuanto a `uri`.
`uri_direct_1`|Un URI alternativo que se puede utilizar para conectarse al servicio. Formateado en cuanto a `uri`.
`ca_certificate_base64`|Un certificado firmado automáticamente que se utiliza para confirmar que una aplicación se está conectando al servidor apropiado. El certificado está codificado como base64.
`deployment_id`|Un identificador interno para el servicio, tal como se ha creado en Compose.
`uri_cli_2`|Una línea de mandatos de shell `cqlsh` alternativa que se conecta a la instancia de la base de datos.
`uri`|El URI que se utiliza al conectarse al servicio, que incluye el esquema (`scylla:`), la contraseña, el nombre de host del servidor, el número de puerto al que se conecta y el nombre de la base de datos.
{: caption="Table 1. {{site.data.keyword.composeForScyllaDB}} credentials" caption-side="top"}


# Enlaces relacionados
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Artículos de Compose](https://www.compose.com/articles/){:new_window}

## Guías de aprendizaje y ejemplos
{: #samples}
* [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs){:new_window}

## Enlaces relacionados
{: #general}
* [Ayuda de Compose](https://help.compose.com/docs){:new_window}
