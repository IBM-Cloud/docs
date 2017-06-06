---

copyright:
  years: 2016,2017
lastupdated: "2017-04-27"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Credenciales disponibles
{: #available-credentials}

Para conectar una app al servicio, utilice las credenciales creadas junto con el servicio. La app de ejemplo [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) muestra cómo utilizar Node.js para conectar a un servicio de {{site.data.keyword.composeForScyllaDB}} utilizando las credenciales.

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
{: caption="Tabla 1. Credenciales de Compose for ScyllaDB" caption-side="top"}
