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

# Iniciación a {{site.data.keyword.composeForRabbitMQ}}
{: #getting-started-with-compose-for-rabbitmq}

RabbitMQ maneja los mensajes de forma asíncrona entre las aplicaciones y las bases de datos, permitiendo la separación de los datos y de las capas de aplicación. RabbitMQ permite a los desarrolladores direccionar, realizar un seguimiento y poner en cola mensajes con niveles de persistencia personalizables, valores de entrega y publicación confirmada. Al utilizar {{site.data.keyword.composeForRabbitMQ_full}}, obtendrá acceso a la interfaz administrativa fácil de utilizar con un host de características de gestión como por ejemplo la supervisión de despliegue, el escalado de pulsación de un botón, la configuración de usuarios y el acceso de archivos de registro.
{:shortdesc}

**Nota:** Cualquier instancia de servicio de Compose proporcionada antes del 14 de septiembre de 2016 que siga activa se puede seguir utilizando y se puede acceder a ella directamente en [https://www.compose.com/](https://www.compose.com). Se puede acceder directamente a cualquier instancia de servicio de Compose que se proporcione desde este momento en adelante y se utilizará dentro de la cuenta de Bluemix.

Siga estos pasos para iniciarse a {{site.data.keyword.composeForRabbitMQ}}.

1. [Cree una instancia de {{site.data.keyword.composeForRabbitMQ}}](https://console.ng.bluemix.net/catalog/services/compose-for-rabbitmq/).

  Al crear una instancia del servicio, asegúrese de que elige un nombre para el servicio y un nombre de credencial. Deje el servicio desenlazado; puede conectar una aplicación al servicio más adelante utilizando las credenciales proporcionadas cuando se proporcione el servicio.  Los distintos valores de credenciales se listan en la sección *Credenciales disponibles*.

2. Conéctese al servicio de {{site.data.keyword.composeForRabbitMQ}}.

  Para conectar una app al servicio, utilice las credenciales creadas junto con el servicio. La app de ejemplo muestra cómo utilizar Node.js para conectar a un servicio de {{site.data.keyword.composeForRabbitMQ}}.

  Descargue la app de ejemplo [compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs) y siga las instrucciones del archivo readme. A continuación, en la página de detalles de la aplicación en Bluemix, pulse **Ver APP**.

## Credenciales disponibles

Nombre de campo|Descripción
----------|-----------
``uri``|El URI que se utilizará al conectarse al servicio. Incluye el esquema (`amqps:), el nombre de usuario y la contraseña del administrador, el nombre de host del servidor, el número de puerto al que se conecta y el nombre de vhost.
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
{: caption="Table 1. {{site.data.keyword.composeForRabbitMQ}} credentials" caption-side="top"}

# Enlaces relacionados
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Artículos de Compose](https://www.compose.com/articles/){:new_window}

## Guías de aprendizaje y ejemplos
{: #samples}
[compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs){:new_window}

## Enlaces relacionados
{: #general}
* [Ayuda de Compose](https://help.compose.com/docs){:new_window}
