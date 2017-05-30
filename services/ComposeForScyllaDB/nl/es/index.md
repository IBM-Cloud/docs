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

# Iniciación a Compose for ScyllaDB
{: #getting-started-with-compose-for-scylladb}

ScyllaDB es un sustituto de la base de datos distribuida de columna ancha Cassandra. ScyllaDB está escrito en C++, en lugar de Java de Cassandra, para conseguir una mejor utilización de recursos, que puede llegar a un rendimiento diez veces superior en las pruebas de referencia. Además de mantener la compatibilidad con la herramienta Cassandra y los archivos de datos, ScyllaDB añade capacidades de ajuste automático. {{site.data.keyword.composeForScyllaDB_full}} amplía las capacidades de ScyllaDB gestionándolo para los usuarios, ofreciendo un sistema de despliegue sencillo y de escalado automático que proporcione alta disponibilidad y redundancia, además de copias de seguridad automatizadas.
{:shortdesc}

**Nota:** {{site.data.keyword.composeForScyllaDB_full}} no da acceso a la IU de Compose. Consulte [Componer en Bluemix Support](https://help.compose.com/docs/bluemix-compose-support) para obtener más detalles.

Siga estos pasos para iniciarse a {{site.data.keyword.composeForScyllaDB}}:

1. [Cree una instancia de {{site.data.keyword.composeForScyllaDB}}](https://console.ng.bluemix.net/catalog/services/compose-for-scylladb/).

   Al crear una instancia del servicio, seleccione un nombre para el servicio y un nombre de credencial. Deje el servicio desenlazado; puede conectar una aplicación al servicio más adelante utilizando las credenciales proporcionadas cuando se proporcione el servicio. Los distintos valores de credenciales se listan en la sección "Credenciales disponibles".

2. Conéctese al servicio de {{site.data.keyword.composeForScyllaDB}}.

   Para conectar una aplicación al servicio, utilice las [credenciales](./credentials.html) creadas junto con el servicio.

   Descargue la aplicación de ejemplo [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) y siga las instrucciones del archivo readme. A continuación, en la página de detalles de la aplicación en la consola de Bluemix, pulse **Ver APP**.

   La aplicación de ejemplo muestra cómo utilizar Node.js para conectar a un servicio de {{site.data.keyword.composeForScyllaDB}}.
