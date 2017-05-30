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

# Iniciación a Compose for MySQL
{: #getting-started-with-compose-for-mysql}

Con un subconjunto amplio de ANSI SQL 99 y un gran conjunto de sus propias extensiones, incluido el documento de JSON, la búsqueda de texto completo y las vistas actualizables, MySQL ofrece una paleta rica para que los desarrolladores exploten sus aplicaciones. Los administradores también pueden encontrar una amplia selección de herramientas de gestión de bases de datos que pueden funcionar con MySQL. {{site.data.keyword.composeForMySQL_full}} hace que MySQL amplíe las capacidades de MySQL gestionándolo para los usuarios, ofreciendo un sistema de despliegue sencillo y de escalado automático que proporcione alta disponibilidad y redundancia, y copias de seguridad automatizadas.
{:shortdesc}

**Nota:** {{site.data.keyword.composeForMySQL_full}} no da acceso a la IU de Compose. Consulte [Componer en Bluemix Support](https://help.compose.com/docs/bluemix-compose-support) para obtener más detalles.

Siga estos pasos para iniciarse a {{site.data.keyword.composeForMySQL}}:

1. [Cree una instancia de {{site.data.keyword.composeForMySQL}}](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/).

   Al crear una instancia del servicio, seleccione un nombre para el servicio y un nombre de credencial. Deje el servicio desenlazado; puede conectar una aplicación al servicio más adelante utilizando las credenciales proporcionadas cuando se proporcione el servicio. Los distintos valores de credenciales se listan en la sección "Credenciales disponibles".

2. Conéctese al servicio de {{site.data.keyword.composeForMySQL}}.

  Para conectar una aplicación al servicio, utilice las [credenciales](./credentials.html) creadas junto con el servicio.

  Descargue la aplicación de ejemplo [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) y siga las instrucciones del archivo readme. A continuación, en la página de detalles de la aplicación en la consola de Bluemix, pulse **Ver APP**.

  La aplicación de ejemplo muestra cómo utilizar Node.js para conectar a un servicio de {{site.data.keyword.composeForMySQL}}.
