---

copyright:
  years: 2016
lastupdated: "2016-12-09"
---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be --- surrounded by 3 dashes ---
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Iniciación a {{site.data.keyword.composeForPostgreSQL}}
{: #getting-started-with-compose-for-postgreSQL}

{{site.data.keyword.composeForPostgreSQL}} proporciona una potente base de datos relacional de objetos de código abierto que se puede personalizar mucho. Con Postgres, el desarrollo es rápido y fácilmente escalable. Puede desarrollar en un lenguaje con el que esté cómodo, como por ejemplo C/C++, Perl, Python, TCL/TK, Delphi/Kylix, VB, PHP, ASP y Java. Obtendrá una base de datos empresarial rica en características con soporte de JSON, que le proporciona lo mejor de los mundos SQL y NoSQL.
{:shortdesc}

**Nota:** Cualquier instancia de servicio de Compose proporcionada antes del 14 de septiembre de 2016 que siga activa se puede seguir utilizando y se puede acceder a ella directamente en [https://www.compose.com/](https://www.compose.com). Se puede acceder directamente a cualquier instancia de servicio de Compose que se proporcione desde este momento en adelante y se utilizará dentro de la cuenta de Bluemix.

Siga estos pasos para iniciarse a Compose for PostgreSQL:

1. [Cree una instancia de {{site.data.keyword.composeForPostgreSQL}}](https://console.ng.bluemix.net/catalog/services/compose-for-postgresql/).

  Al crear una instancia del servicio, asegúrese de que elige un nombre para el servicio y un nombre de credencial. Deje el servicio desenlazado; puede conectar una aplicación al servicio más adelante utilizando las credenciales proporcionadas cuando se proporcione el servicio. Los distintos valores de credenciales se listan en la sección *Credenciales disponibles*.

2. Conéctese al servicio de {{site.data.keyword.composeForPostgreSQL}}.

  Para conectar una app al servicio, utilice las credenciales creadas junto con el servicio. La app de ejemplo muestra cómo utilizar Node.js para conectar a un servicio de {{site.data.keyword.composeForPostgreSQL}}.

  Descargue la app de ejemplo [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs) y siga las instrucciones del archivo readme. A continuación, en la página de detalles de la aplicación en Bluemix, pulse **Ver APP** para ver el contenido de la tabla *ejemplos*.

## Credenciales disponibles

Nombre de campo|Descripción
----------|-----------
`uri`|El URI que se utilizará al conectarse al servicio. Incluye el esquema (`postgres:`), el nombre de usuario y la contraseña del administrador, el nombre de host del servidor, el número de puerto al que se conecta, el nombre de la base de datos y "?ssl=true" para habilitar las conexiones SSL.
`uri_cli`|Una línea de mandatos de shell `psql` que se conecta a la instancia de la base de datos.
`ca_certificate_base64`|Un certificado firmado automáticamente que se utiliza para confirmar que una aplicación se está conectando al servidor apropiado. Está codificado como base64. Debe decodificar la clave antes de utilizarla, como se muestra en la aplicación de ejemplo.
`deployment_id`|Un identificador interno para el servicio, tal como se ha creado en Compose.
`db_type`|El tipo de base de datos que ofrece el servicio; en este caso, `postgresql`.
`name`|El nombre del despliegue de la base de datos.
{: caption="Table 1. {{site.data.keyword.composeForPostgreSQL}} credentials" caption-side="top"}

# Enlaces relacionados
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Artículos de Compose](https://www.compose.com/articles/){:new_window}

## Guías de aprendizaje y ejemplos
{: #samples}
* [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs){:new_window}

## Enlaces relacionados
{: #general}
* [Ayuda de Compose](https://help.compose.com/docs){:new_window}
