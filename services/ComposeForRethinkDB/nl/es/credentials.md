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

Para conectar una app al servicio, utilice las credenciales creadas junto con el servicio. La app de ejemplo [compose-rethinkdb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rethinkdb-helloworld-nodejs) muestra cómo utilizar Node.js para conectar a un servicio de {{site.data.keyword.composeForRethinkDB}} utilizando las credenciales.

Nombre de campo|Descripción
----------|-----------
`uri`|El URI que se utilizará al conectarse al servicio. Incluye el esquema (rethinkdb:), el nombre de usuario y la contraseña del administrador, el nombre de host del servidor y el número de puerto al que se conecta.
`uri_admin`|Un URI que se debería visitar en un navegador para acceder a la interfaz de administración de la base de datos. El acceso requiere el nombre de usuario y la contraseña del administrador desde el campo `uri`.
`ca_certificate_base64`|Un certificado firmado automáticamente que se utiliza para confirmar que una aplicación se está conectando al servidor apropiado. Está codificado como base64. Debe decodificar la clave antes de utilizarla, como se muestra en la aplicación de ejemplo.
`deployment_id`|Un identificador interno para el servicio, tal como se ha creado en Compose.
`db_type`|El tipo de base de datos que ofrece el servicio; en este caso, `rethink`.
`name`|El nombre del despliegue de la base de datos.
{: caption="Tabla 1. Credenciales de Compose for RethinkDB" caption-side="top"}
