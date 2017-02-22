---

copyright:
  years: 2016, 2017
lastupdated: "2016-09-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Iniciación a {{site.data.keyword.openwhisk_short}}


{{site.data.keyword.openwhisk}} es un servicio de computación dirigido por sucesos, también conocido como Computación sin servidor o Function as a Service (FaaS), {{site.data.keyword.openwhisk_short}} ejecuta lógica de aplicación en respuesta a sucesos o invocaciones directas desde aplicaciones web o móvil a través de HTTP. Los sucesos se pueden
proporcionar desde servicios de Bluemix como Cloudant, así como desde orígenes externos. Los desarrolladores se pueden centrar en escribir
lógica de aplicación y crear acciones que se ejecutan a demanda. La tasa de ejecución de acciones siempre coincide con la tasa de sucesos,
teniendo como resultado un escalado y capacidad de recuperación inherente y una utilización óptima. Se paga solo por lo que se usa,
y no tiene que gestionar un servidor. También puede obtener el [código fuente](https://github.com/openwhisk/openwhisk)
y ejecutar el sistema usted mismo.
{: shortdesc}

Para obtener más detalles sobre como funciona {{site.data.keyword.openwhisk_short}}, consulte [Acerca de {{site.data.keyword.openwhisk_short}}](./openwhisk_about.html).

Puede utilizar el navegador o la CLI para desarrollar sus aplicaciones de {{site.data.keyword.openwhisk_short}}.
Ambos tienen prestaciones similares para desarrollar aplicaciones; la CLI ofrece más control sobre el despliegue y las operaciones.


## Desarrollar en el navegador
{: #openwhisk_start_editor}

Pruebe {{site.data.keyword.openwhisk_short}} en el [Navegador](https://console.{DomainName}/openwhisk/editor){: new_window} para crear acciones, automatizar acciones utilizando desencadenantes, y explorar paquetes públicos.
Visite la página [más información](https://console.{DomainName}/openwhisk/learn){: new_window} para realizar una visita rápida de la interfaz de usuario de OpenWhisk.

## Configuración de la CLI de {{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_configure_cli}

Puede utilizar la interfaz de línea de mandatos (CLI) de {{site.data.keyword.openwhisk_short}} para configurar su espacio de nombres y clave de autorización.
Acceda a [Configurar CLI](https://new-console.{DomainName}/openwhisk/cli){: new_window} y
siga las instrucciones para instalarlo.

### Configure la CLI para utilizar un proxy HTTPS
{: #openwhisk_configure_https_proxy_cli}

La CLI se puede configurar para utilizar un proxy HTTPS. Para configurar un proxy HTTPS, se debe crear una variable de entorno llamada `HTTPS_PROXY`. La variable se debe establecer en la dirección del proxy HTTPS y el puerto correspondiente utilizando el siguiente formato:
`{PROXY IP}:{PROXY PORT}`.

Una vez que {{site.data.keyword.openwhisk_short}} esté configurado con la CLI, puede empezar a usarlo desde la línea de mandatos.

## Uso de la CLI de {{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_using_cli}

Tras haber [configurado su entorno](https://new-console.{DomainName}/openwhisk/cli){: new_window}, puede empezar a usar la CLI de {{site.data.keyword.openwhisk_short}} para hacer lo siguiente:

* Ejecutar sus fragmentos de código, o acciones, en {{site.data.keyword.openwhisk_short}}. Consulte
[Creación e invocación de acciones](./openwhisk_actions.html).
* Usar desencadenantes y reglas para permitir a sus acciones responder ante sucesos. Consulte
[Creación de desencadenantes y reglas](./openwhisk_triggers_rules.html).
* Aprenda a los paquetes agrupan acciones y configure orígenes de sucesos externos. Consulte [Uso y
creación de paquetes](./openwhisk_packages.html).
* Explore el catálogo de paquetes y mejore sus aplicaciones con servicios externos como un
[Origen de sucesos de Cloudant](./openwhisk_catalog.html#openwhisk_catalog_cloudant). Consulte [Uso de servicios habilitados para {{site.data.keyword.openwhisk_short}}](./openwhisk_catalog.html).


## Uso de {{site.data.keyword.openwhisk_short}} desde una app de iOS
{: #openwhisk_start_using_ios}

Puede usar {{site.data.keyword.openwhisk_short}} desde su app de móvil iOS o Apple Watch usando el SDK de iOS de {{site.data.keyword.openwhisk_short}}. Para obtener más detalles, consulte la
[Documentación de iOS](./openwhisk_mobile_sdk.html).

## Uso de las API REST con {{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_using_restapi}

Tras habilitar su entorno {{site.data.keyword.openwhisk_short}}, puede usar
{{site.data.keyword.openwhisk_short}} con sus apps web o apps móviles con llamadas a la API REST.
Para obtener más detalles
sobre las API para acciones, activaciones, paquetes, reglas y desencadenantes, consulte la
[Documentación de la API de {{site.data.keyword.openwhisk_short}}](https://new-console.{DomainName}/apidocs/98).

## Ejemplo Hello World de {{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_hello_world}
Para empezar con {{site.data.keyword.openwhisk_short}}, intente el ejemplo de código JavaScript siguiente.

```
/**
 * Hello world as an OpenWhisk action.
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

    ```
    {
        "payload": "Hello, World!"
    }
    ```
    {: screen}

    ```
    wsk action invoke hello --blocking --result --param name Fred
    ```
    {: pre}  

    Este mandato genera la salida siguiente:

    ```
    {
        "payload": "Hello, Fred!"
    }
    ```
    {: screen}

También puede utilizar las capacidades dirigidas por sucesos en {{site.data.keyword.openwhisk_short}} para invocar
esta acción en respuesta a sucesos. Siga el ejemplo
[alarm service example](./openwhisk_packages.html#openwhisk_packages_trigger) para configurar un origen de sucesos para
invocar la acción `hello` cada vez que se genere un suceso periódico.


## Detalles del sistema
{: #openwhisk_system_details}

Puede encontrar información adicional sobre {{site.data.keyword.openwhisk_short}} en los temas siguientes:

* [Nombre de entidad](./openwhisk_reference.html#openwhisk_entities)
* [Semánticas de acción](./openwhisk_reference.html#openwhisk_semantics)
* [Límites](./openwhisk_reference.html#openwhisk_syslimits)
* [API REST](https://new-console.{DomainName}/apidocs/98)

# Enlaces relacionados
{: #rellinks}

## Referencia de API
{: #api}
* [Documentación de API REST](./openwhisk_reference.html#openwhisk_ref_restapi)
* [API REST](https://new-console.{DomainName}/apidocs/98){:new_window}

## Enlaces relacionados
{: #general}
* [Descubrir: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [{{site.data.keyword.openwhisk_short}} en IBM developerWorks](https://developer.ibm.com/openwhisk/){:new_window}
