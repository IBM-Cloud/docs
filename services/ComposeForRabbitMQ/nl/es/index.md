---

copyright:
  years: 2016,2017
lastupdated: "2017-04-027"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Iniciación a Compose for RabbitMQ
{: #getting-started-with-compose-for-rabbitmq}

RabbitMQ maneja los mensajes de forma asíncrona entre las aplicaciones y las bases de datos, permitiendo la separación de los datos y de las capas de aplicación. RabbitMQ permite a los desarrolladores direccionar, realizar un seguimiento y poner en cola mensajes con niveles de persistencia personalizables, valores de entrega y publicación confirmada. Al utilizar {{site.data.keyword.composeForRabbitMQ_full}}, obtendrá acceso a la interfaz administrativa fácil de utilizar con un host de características de gestión como por ejemplo la supervisión de despliegue, el escalado de pulsación de un botón, la configuración de usuarios y el acceso de archivos de registro.
{:shortdesc}

**Nota:** Cualquier instancia de servicio de Compose proporcionada antes del 14 de septiembre de 2016 que siga activa se puede seguir utilizando y se puede acceder a ella directamente en [https://www.compose.com/](https://www.compose.com). Se puede acceder directamente a cualquier instancia de servicio de Compose que se proporcione desde este momento en adelante y se utilizará dentro de la cuenta de Bluemix.

Siga estos pasos para iniciarse a {{site.data.keyword.composeForRabbitMQ}}.

1. [Cree una instancia de {{site.data.keyword.composeForRabbitMQ}}](https://console.ng.bluemix.net/catalog/services/compose-for-rabbitmq/).

  Al crear una instancia del servicio, asegúrese de que elige un nombre para el servicio y un nombre de credencial. Deje el servicio desenlazado; puede conectar una aplicación al servicio más adelante utilizando las credenciales proporcionadas cuando se proporcione el servicio.  Los distintos valores de credenciales se listan en la sección *Credenciales disponibles*.

2. Conéctese al servicio de {{site.data.keyword.composeForRabbitMQ}}.

  Para conectar una app al servicio, utilice las [credenciales](./credentials.html) creadas junto con el servicio. La app de ejemplo muestra cómo utilizar Node.js para conectar a un servicio de {{site.data.keyword.composeForRabbitMQ}}.

  Descargue la app de ejemplo [compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs) y siga las instrucciones del archivo readme. A continuación, en la página de detalles de la aplicación en Bluemix, pulse **Ver APP**.
