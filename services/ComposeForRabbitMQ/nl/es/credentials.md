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

Para conectar una app al servicio, utilice las credenciales creadas junto con el servicio. La app de ejemplo [compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs) muestra cómo utilizar Node.js para conectar a un servicio de {{site.data.keyword.composeForRabbitMQ}} utilizando las credenciales.

Nombre de campo|Descripción
----------|-----------
`uri`|El URI que se utilizará al conectarse al servicio. Incluye el esquema (`amqps:), el nombre de usuario y la contraseña del administrador, el nombre de host del servidor, el número de puerto al que se conecta y el nombre de vhost.
`uri_direct_1`|Un URI alternativo que se puede utilizar al conectarse al servicio. Formateado según `uri`.
`uri_admin`|Un URI que se debería visitar en un navegador para acceder a la interfaz de administración de la base de datos. El acceso requiere el nombre de usuario y la contraseña del administrador desde el campo `uri`.
`uri_admin_1`|Un URI de administración alternativo - consulte `uri_admin`.
`uri_admin_2`|Un URI de administración alternativo - consulte `uri_admin`.
`uri_admin_3`|Un URI de administración alternativo - consulte `uri_admin`.
`uri_admin_4`|Un URI de administración alternativo - consulte `uri_admin`.
`ca_certificate_base64`|Un certificado firmado automáticamente que se utiliza para confirmar que una aplicación se está conectando al servidor apropiado. Está codificado como base64. Debe decodificar la clave antes de utilizarla, como se muestra en la aplicación de ejemplo.
`deployment_id`|Un identificador interno para el servicio, tal como se ha creado en Compose.
`db_type`|El tipo de base de datos que ofrece el servicio; en este caso, `rabbitmq`.
`name`|El nombre del despliegue de la base de datos.
{: caption="Tabla 1. Credenciales de Compose for RabbitMQ" caption-side="top"}
