---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Iniciación a {{site.data.keyword.openwhisk_short}}


{{site.data.keyword.openwhisk}} es un servicio de computación dirigido por sucesos, también conocido como Computación sin servidor o Function as a Service (FaaS), {{site.data.keyword.openwhisk_short}} ejecuta lógica de aplicación en respuesta a sucesos o invocaciones directas desde aplicaciones web o móvil a través de HTTP. Los sucesos se pueden
proporcionar desde servicios de Bluemix como Cloudant, así como desde orígenes externos. Los desarrolladores se pueden centrar en escribir
lógica de aplicación y crear acciones que se ejecutan a demanda.
Las ventajas de este nuevo paradigma son que el usuario no debe suministrar servidores explícitamente ni preocuparse del escalado automático ni de la alta disponibilidad, actualizaciones ni mantenimiento, ni pagar por horas de procesador cuando el servidor se está ejecutando pero no sirviendo solicitudes.
El código se ejecuta siempre que hay una llamada HTTP, un cambio de estado de base de datos u otro tipo de suceso que active la ejecución del código.
Se le facturará por milisegundo de tiempo de ejecución (redondeado hacia arriba hasta la siguiente unidad de 100ms), no por hora de utilización de VM independientemente de si dicha VM ha realizado o no trabajo útil.
{: shortdesc}

Este modelo de programación es el complemento perfecto para microservicios, servicios móviles, IoT y muchas otras apps; el cliente obtiene funciones inherentes de escalado automático y de equilibrio de carga de forma inmediata sin tener que configurar manualmente clústeres, equilibradores de carga, plug-ins HTTP, etc. Si trabaja con {{site.data.keyword.openwhisk}}, también se beneficiará de administración cero, lo que significa que todo el hardware, software y sistema de red lo mantiene IBM. Lo único que tiene que hacer es para proporcionar el código que desea ejecutar a {{site.data.keyword.openwhisk}}. El resto es “magia”. Encontrará una buena introducción al modelo de programación sin servidor en el [blog de Martin Fowler](https://martinfowler.com/articles/serverless.html).

También puede obtener el [código abierto de Apache OpenWHisk](https://github.com/openwhisk/openwhisk) y ejecutar usted mismo el sistema.

Para obtener más detalles sobre como funciona {{site.data.keyword.openwhisk_short}}, consulte [Acerca de {{site.data.keyword.openwhisk_short}}](./openwhisk_about.html).

Puede utilizar el navegador o la CLI para desarrollar sus aplicaciones de {{site.data.keyword.openwhisk_short}}.
Ambos tienen prestaciones similares para desarrollar aplicaciones; la CLI ofrece más control sobre el despliegue y las operaciones.

## Desarrollar en el navegador
{: #openwhisk_start_editor}

Pruebe {{site.data.keyword.openwhisk_short}} en el [Navegador](https://console.{DomainName}/openwhisk/editor){: new_window} para crear acciones, automatizar acciones utilizando desencadenantes, y explorar paquetes públicos. 
Visite la página [más información](https://console.{DomainName}/openwhisk/learn){: new_window} para realizar una visita rápida de la interfaz de usuario de OpenWhisk.

## Desarrollo mediante la CLI
{: #openwhisk_start_configure_cli}

Puede utilizar la interfaz de línea de mandatos (CLI) de {{site.data.keyword.openwhisk_short}} para configurar su espacio de nombres y clave de autorización.
Acceda a [Configurar CLI](https://new-console.{DomainName}/openwhisk/cli){: new_window} y
siga las instrucciones para instalarlo.

## Visión general
{: #openwhisk_start_overview}
- [Cómo funciona OpenWhisk](./openwhisk_about.html)
- [Casos de uso comunes para aplicaciones sin servidor](./openwhisk_use_cases.html)
- [Configuración y utilización de la CLI de OpenWhisk](./openwhisk_cli.html)
- [Utilización de OpenWhisk desde una app iOS](./openwhisk_mobile_sdk.html)

## Modelo de programación
{: #openwhisk_start_programming}
- [Detalles del sistema](./openwhisk_reference.html)
- [Catálogo de servicios proporcionados por OpenWhisk](./openwhisk_catalog.html)
- [Acciones](./openwhisk_actions.html)
- [Desencadenantes y reglas](./openwhisk_triggers_rules.html)
- [Canales de información](./openwhisk_feeds.html)
- [Paquetes](./openwhisk_packages.html)
- [Anotaciones](./openwhisk_annotations.html)
- [Acciones de la web](./openwhisk_webactions.html)
- [API Gateway](./openwhisk_apigateway.html)
- [Nombre de entidad](./openwhisk_reference.html#openwhisk_entities)
- [Semánticas de acción](./openwhisk_reference.html#openwhisk_semantics)
- [Límites](./openwhisk_reference.html#openwhisk_syslimits)

## Ejemplo Hello World de {{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_hello_world}
Para empezar con {{site.data.keyword.openwhisk_short}}, intente el ejemplo de código JavaScript siguiente.

```javascript
/**
 * Hello world como acción de OpenWhisk.
 */
function main(params) {
    var name = params.name || 'World';
    return {payload:  'Hello, ' + name + '!'};
}
```
{: codeblock}

Para utilizar este ejemplo, siga estos pasos:

1. Guardar el código en un archivo. Por ejemplo, *hello.js*.

2. Desde la línea de mandatos de la CLI de {{site.data.keyword.openwhisk_short}}, cree la acción especificando este mandato:

    ```
    wsk action create hello hello.js
    ```
    {: pre}

3. A continuación invoque la acción especificando los mandatos siguientes.

    ```
    wsk action invoke hello --blocking --result
    ```
    {: pre}  

    Este mandato genera la salida siguiente:

    ```json
    {
        "payload": "Hello, World!"
    }
    ```
    
    ```
    wsk action invoke hello --blocking --result --param name Fred
    ```
    {: pre}  

    Este mandato genera la salida siguiente:

    ```json
    {
        "payload": "Hello, Fred!"
    }
    ```

También puede utilizar las capacidades dirigidas por sucesos en {{site.data.keyword.openwhisk_short}} para invocar
esta acción en respuesta a sucesos. Siga el ejemplo
[alarm service example](./openwhisk_packages.html#openwhisk_packages_trigger) para configurar un origen de sucesos para
invocar la acción `hello` cada vez que se genere un suceso periódico.


## Referencia de API
{: #openwhisk_start_api notoc}
* [Documentación de API REST](./openwhisk_reference.html#openwhisk_ref_restapi)
* [API REST](https://new-console.{DomainName}/apidocs/98){:new_window}

## Enlaces relacionados
{: #general notoc}
* [Descubrir: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [{{site.data.keyword.openwhisk_short}} en IBM developerWorks](https://developer.ibm.com/openwhisk/){:new_window}
* [Sitio web del proyecto Apache {{site.data.keyword.openwhisk_short}}](http://openwhisk.org){:new_window}
