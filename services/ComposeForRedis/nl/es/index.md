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

# Iniciación a Compose for Redis
{: #getting-started-with-compose-for-redis}

Redis es un almacén de valor de clave, en memoria, de código abierto. Los valores de Redis pueden ser cadenas sencillas, hash, listas y conjuntos o mapas de bits potentes, registros de hyperlog e índices geoespaciales. Redis es ideal como memoria caché de aplicaciones o como almacén de datos de respuesta rápida. {{site.data.keyword.composeForRedis_full}} le proporciona una configuración preajustada para alta disponibilidad y persistencia en disco, bloqueados con características de seguridad adicionales.
{:shortdesc}

**Nota:** Cualquier instancia de servicio de Compose proporcionada antes del 14 de septiembre de 2016 que siga activa se puede seguir utilizando y se puede acceder a ella directamente en [https://www.compose.com/](https://www.compose.com). Se puede acceder directamente a cualquier instancia de servicio de Compose que se proporcione desde este momento en adelante y se utilizará dentro de la cuenta de Bluemix.

Siga estos pasos para iniciarse a {{site.data.keyword.composeForRedis}}.

1. [Cree una instancia de {{site.data.keyword.composeForRedis}}](https://console.ng.bluemix.net/catalog/services/compose-for-redis/).

  Al crear una instancia del servicio, asegúrese de que elige un nombre para el servicio y un nombre de credencial. Deje el servicio desenlazado; puede conectar una aplicación al servicio más adelante utilizando las credenciales proporcionadas cuando se proporcione el servicio. Los distintos valores de credenciales se listan en la sección *Credenciales disponibles*.

2. Conéctese al servicio de {{site.data.keyword.composeForRedis}}.

  Para conectar una app al servicio, utilice las [credenciales](./credentials.html) creadas junto con el servicio. La app de ejemplo muestra cómo utilizar Node.js para conectar a un servicio de {{site.data.keyword.composeForRedis}}.

  Descargue la app de ejemplo [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs) y siga las instrucciones del archivo readme. A continuación, en la página de detalles de la aplicación en Bluemix, pulse **Ver APP**.
