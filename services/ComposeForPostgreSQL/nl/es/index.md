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

# Iniciación a Compose for PostgreSQL
{: #getting-started-with-compose-for-postgreSQL}

{{site.data.keyword.composeForPostgreSQL}} proporciona una potente base de datos relacional de objetos de código abierto que se puede personalizar mucho. Con Postgres, el desarrollo es rápido y fácilmente escalable. Puede desarrollar en un lenguaje con el que esté cómodo, como por ejemplo C/C++, Perl, Python, TCL/TK, Delphi/Kylix, VB, PHP, ASP y Java. Obtendrá una base de datos empresarial rica en características con soporte de JSON, que le proporciona lo mejor de los mundos SQL y NoSQL.
{:shortdesc}

**Nota:** Cualquier instancia de servicio de Compose proporcionada antes del 14 de septiembre de 2016 que siga activa se puede seguir utilizando y se puede acceder a ella directamente en [https://www.compose.com/](https://www.compose.com). Se puede acceder directamente a cualquier instancia de servicio de Compose que se proporcione desde este momento en adelante y se utilizará dentro de la cuenta de Bluemix.

Siga estos pasos para iniciarse a Compose for PostgreSQL:

1. [Cree una instancia de {{site.data.keyword.composeForPostgreSQL}}](https://console.ng.bluemix.net/catalog/services/compose-for-postgresql/).

  Al crear una instancia del servicio, asegúrese de que elige un nombre para el servicio y un nombre de credencial. Deje el servicio desenlazado; puede conectar una aplicación al servicio más adelante utilizando las credenciales proporcionadas cuando se proporcione el servicio. Los distintos valores de credenciales se listan en la sección *Credenciales disponibles*.

2. Conéctese al servicio de {{site.data.keyword.composeForPostgreSQL}}.

  Para conectar una app al servicio, utilice las [credenciales](./credentials.html) creadas junto con el servicio. La app de ejemplo muestra cómo utilizar Node.js para conectar a un servicio de {{site.data.keyword.composeForPostgreSQL}}.

  Descargue la app de ejemplo [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs) y siga las instrucciones del archivo readme. A continuación, en la página de detalles de la aplicación en Bluemix, pulse **Ver APP** para ver el contenido de la tabla *ejemplos*.
