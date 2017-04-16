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

# Guía de inicio con Compose for MongoDB
{: #getting-started-with-compose-for-mongodb}

{{site.data.keyword.composeForMongoDB_full}} utiliza la potente indexación y consulta, agregación y soporte de controlador amplio de MongoDB que lo ha convertido en el almacén de datos JSON preferido para muchas empresas y nuevas empresas. {{site.data.keyword.composeForMongoDB}} ofrece un sistema de despliegue sencillo y de escalado automático. Entrega alta disponibilidad y redundancia, copias de seguridad automatizadas y a demanda sin parar, herramientas de supervisión, integración en sistemas de alerta, rendimiento de vistas de análisis, y mucho más, en una interfaz de usuario sencilla y clara.
{:shortdesc}

**Nota:** Cualquier instancia de servicio de Compose proporcionada antes del 14 de septiembre de 2016 que siga activa se puede seguir utilizando y se puede acceder a ella directamente en [https://www.compose.com/](https://www.compose.com). Se puede acceder directamente a cualquier instancia de servicio de Compose que se proporcione desde este momento en adelante y se utilizará dentro de la cuenta de Bluemix.

Siga estos pasos para iniciarse a {{site.data.keyword.composeForMongoDB}}:

1. [Cree una instancia de {{site.data.keyword.composeForMongoDB}}](https://console.ng.bluemix.net/catalog/services/compose-for-mongodb/).

   Al crear una instancia del servicio, asegúrese de que elige un nombre para el servicio y un nombre de credencial. Deje el servicio desenlazado; puede conectar una aplicación al servicio más adelante utilizando las credenciales proporcionadas cuando se proporcione el servicio.  Los distintos valores de credenciales se listan en la sección *Credenciales disponibles*.

2. Conéctese al servicio de {{site.data.keyword.composeForMongoDB}}.

   Para conectar una app al servicio, utilice las credenciales creadas junto con el servicio. La app de ejemplo muestra cómo utilizar Node.js para conectar a un servicio de {{site.data.keyword.composeForMongoDB}}.

   Descargue la app de ejemplo [compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs) y siga las instrucciones del archivo readme. A continuación, en la página de detalles de la aplicación en Bluemix, pulse **Ver APP**.


## Credenciales disponibles

Nombre de campo|Descripción
----------|-----------
`uri`|El URI que se utilizará al conectarse al servicio. `uri` incluye el esquema (`mongodb:`), el nombre de usuario y la contraseña del administrador, el nombre de host del servidor, el número de puerto al que se conecta, el nombre de la base de datos y `?ssl=true` para habilitar las conexiones SSL.
`uri_cli`|Una línea de mandatos de shell `mongo` que se conecta a la instancia de la base de datos.
`ca_certificate_base64`|Un certificado firmado automáticamente que se utiliza para confirmar que una aplicación se está conectando al servidor apropiado. El certificado tiene el código base64. Debe decodificar la clave antes de utilizarla, como se muestra en la aplicación de ejemplo.
`deployment_id`|Un identificador interno para el servicio, tal como se ha creado en Compose.
`db_type`|El tipo de base de datos que ofrece el servicio: en este caso, `mongodb`.
`name`|El nombre del despliegue de la base de datos.
{: caption="Table 1. {{site.data.keyword.composeForMongoDB}} credentials" caption-side="top"}

# Enlaces relacionados
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Artículos de Compose](https://www.compose.com/articles/){:new_window}

## Guías de aprendizaje y ejemplos
{: #samples}
* [compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs){:new_window}

## Enlaces relacionados
{: #general}
* [Ayuda de Compose](https://help.compose.com/docs){:new_window}
