---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-25"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} CLI

{{site.data.keyword.openwhisk_short}} ofrece una potente interfaz de línea de mandatos que permite la gestión completa de todos los aspectos del sistema.

## Configuración de la CLI de {{site.data.keyword.openwhisk_short}} 

Puede utilizar la interfaz de línea de mandatos (CLI) de {{site.data.keyword.openwhisk_short}} para configurar su espacio de nombres y clave de autorización.
Acceda a [Configurar CLI](https://console.{DomainName}/openwhisk/cli) y
siga las instrucciones para instalarlo.

Hay dos propiedades que se deben configurar para poder utilizar la interfaz de línea de mandatos:

1. **Host de API** (nombre o dirección IP) del despliegue de {{site.data.keyword.openwhisk_short}} que desea utilizar.
2. **Clave de autorización** (nombre de usuario y contraseña) que le garantiza acceso a la API de {{site.data.keyword.openwhisk_short}}.

Ejecute el siguiente mandato para definir el host de API:

```
wsk property set --apihost openwhisk.ng.bluemix.net
```
{: pre} 

Si conoce su clave de autorización, puede configurar la CLI para que la utilice. 

Ejecute el siguiente mandato para definir la clave de autorización:

```
wsk property set --auth <authorization_key>
```
{: pre}

**Consejo:** la CLI de OpenWhisk guarda las propiedades definidas en `~/.wskprops` de forma predeterminada. La ubicación de este archivo se puede modificar mediante la variable de entorno `WSK_CONFIG_FILE`. 

Para comprobar la configuración de la CLI, intente [crear y ejecutar una acción](./index.html#openwhisk_start_hello_world).

## Uso de la CLI de {{site.data.keyword.openwhisk_short}}

Tras haber configurado su entorno, puede empezar a usar la CLI de {{site.data.keyword.openwhisk_short}} para hacer lo siguiente:

* Ejecutar sus fragmentos de código, o acciones, en {{site.data.keyword.openwhisk_short}}. Consulte
[Creación e invocación de acciones](./openwhisk_actions.html).
* Usar desencadenantes y reglas para permitir a sus acciones responder ante sucesos. Consulte
[Creación de desencadenantes y reglas](./openwhisk_triggers_rules.html).
* Aprenda a los paquetes agrupan acciones y configure orígenes de sucesos externos. Consulte [Uso y
creación de paquetes](./openwhisk_packages.html).
* Explore el catálogo de paquetes y mejore sus aplicaciones con servicios externos como un
[Origen de sucesos de Cloudant](./openwhisk_cloudant.html). Consulte [Utilización de servicios habilitados para OpenWhisk](./openwhisk_catalog.html).

## Configure la CLI para utilizar un proxy HTTPS

La CLI se puede configurar para utilizar un proxy HTTPS. Para configurar un proxy HTTPS, se debe crear una variable de entorno llamada `HTTPS_PROXY`. La variable se debe establecer en la dirección del proxy HTTPS y el puerto correspondiente utilizando el siguiente formato:
`{PROXY IP}:{PROXY PORT}`.
