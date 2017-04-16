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

# Iniciación a Compose for MySQL
{: #getting-started-with-compose-for-mysql}

Con un subconjunto amplio de ANSI SQL 99 y un gran conjunto de sus propias extensiones, incluido el documento de JSON, la búsqueda de texto completo y las vistas actualizables, MySQL ofrece una paleta rica para que los desarrolladores exploten sus aplicaciones. Los administradores también pueden encontrar una amplia selección de herramientas de gestión de bases de datos que pueden funcionar con MySQL. {{site.data.keyword.composeForMySQL_full}} hace que MySQL amplíe las capacidades de MySQL gestionándolo para los usuarios, ofreciendo un sistema de despliegue sencillo y de escalado automático que proporcione alta disponibilidad y redundancia, y copias de seguridad automatizadas.
{:shortdesc}

**Nota:** {{site.data.keyword.composeForMySQL_full}} no da acceso a la IU de Compose. Consulte [Componer en Bluemix Support](https://help.compose.com/docs/bluemix-compose-support) para obtener más detalles.

Siga estos pasos para iniciarse a {{site.data.keyword.composeForMySQL}}:

1. [Cree una instancia de {{site.data.keyword.composeForMySQL}}](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/).

   Al crear una instancia del servicio, seleccione un nombre para el servicio y un nombre de credencial. Deje el servicio desenlazado; puede conectar una aplicación al servicio más adelante utilizando las credenciales proporcionadas cuando se proporcione el servicio. Los distintos valores de credenciales se listan en la sección "Credenciales disponibles".

2. Conéctese al servicio de {{site.data.keyword.composeForMySQL}}.

  Para conectar una aplicación al servicio, utilice las credenciales creadas junto con el servicio.

  Descargue la aplicación de ejemplo [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) y siga las instrucciones del archivo readme. A continuación, en la página de detalles de la aplicación en la consola de Bluemix, pulse **Ver APP**.

  La aplicación de ejemplo muestra cómo utilizar Node.js para conectar a un servicio de {{site.data.keyword.composeForMySQL}}.


## Credenciales disponibles

Nombre de campo|Descripción
----------|-----------
`db_type`|El tipo de base de datos que ofrece el servicio, en este caso `mysql`.
`name`|El nombre del despliegue de la base de datos.
`uri_cli`|Una línea de mandatos de `mysql` que se conecta a la instancia de la base de datos.
`ca_certificate_base64`|Un certificado firmado automáticamente que se utiliza para confirmar que una aplicación se está conectando al servidor apropiado. El certificado está codificado como base64.
`deployment_id`|Un identificador interno para el servicio, tal como se ha creado en Compose.
`uri`|El URI que se utiliza al conectarse al servicio, que incluye el esquema (`mysql:`), el nombre de usuario y la contraseña del administrador, el nombre de host del servidor, el número de puerto al que se conecta y el nombre de vhost.
{: caption="Table 1. {{site.data.keyword.composeForMySQL}} credentials" caption-side="top"}


# Enlaces relacionados
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Artículos de Compose](https://www.compose.com/articles/){:new_window}

## Guías de aprendizaje y ejemplos
{: #samples}
* [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs){:new_window}

## Enlaces relacionados
{: #general}
* [Ayuda de Compose](https://help.compose.com/docs){:new_window}
