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

Para conectar una app al servicio, utilice las credenciales creadas junto con el servicio. La app de ejemplo [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) muestra cómo utilizar Node.js para conectar a un servicio de {{site.data.keyword.composeForEtcd}} utilizando las credenciales.

Nombre de campo|Descripción
----------|-----------
`ca_certificate_base64`|Un certificado firmado automáticamente que se utiliza para confirmar que una app se está conectando al servidor apropiado. El certificado tiene el código base64. Debe decodificar la clave antes de utilizarla, como se muestra en la app de ejemplo.
`deployment_id`|Un identificador interno para el servicio, tal como se ha creado en Compose.
`db_type`|El tipo de base de datos que ofrece el servicio; en este caso, `etcd`.
`name`|El nombre del despliegue de la base de datos.
`uri`|El URI que se utilizará al conectarse al servicio. `uri` incluye el esquema (`amqps:), el nombre de usuario y la contraseña del administrador, el nombre de host del servidor, el número de puerto al que se conecta y el nombre de `vhost.
{: caption="Tabla 1. Credenciales de Compose for etcd" caption-side="top"}
