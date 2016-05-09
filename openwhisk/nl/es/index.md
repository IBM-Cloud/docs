---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Iniciación a {{site.data.keyword.openwhisk_short}}
*Última actualización: 17 de febrero de 2016*

{{site.data.keyword.openwhisk}} es un servicio distribuido de cálculo dirigido por sucesos. {{site.data.keyword.openwhisk_short}} ejecuta lógica de aplicación en respuesta a sucesos o invocaciones directas desde la web o apps móviles sobre HTTP. Los sucesos se pueden
proporcionar desde servicios de Bluemix como Cloudant, y desde orígenes externos. Los desarrolladores se pueden centrar en escribir
lógica de aplicación y crear acciones que se ejecutan a demanda. La tasa de ejecución de acciones siempre coincide con la tasa de sucesos,
teniendo como resultado un escalado y capacidad de recuperación inherente, y una utilización óptima. Se paga solo por lo que se usa,
y no tiene que gestionar un servidor. También puede obtener el [código fuente](https://github.com/openwhisk/openwhisk)
y ejecutar el sistema usted mismo.
{: shortdesc}

Para obtener más detalles sobre como funciona {{site.data.keyword.openwhisk_short}}, consulte [Acerca de {{site.data.keyword.openwhisk_short}}](./openwhisk_about.html).

## Configuración de {{site.data.keyword.openwhisk_short}}
Puede utilizar la interfaz de línea de mandatos (CLI) de {{site.data.keyword.openwhisk_short}} para configurar su espacio de nombres y clave de autorización. Acceda a [Configurar CLI](https://console.{DomainName}/openwhisk/cli){: new_window} y
siga la experiencia guiada para instalarlo. Tenga en cuenta que debe tener instalado Python 2.7 en su
sistema para poder usar la CLI.

Una vez que {{site.data.keyword.openwhisk_short}} esté configurado con la CLI, puede empezar a usarlo desde la línea de mandatos
o por medio de las API de REST.

## Uso de la CLI de {{site.data.keyword.openwhisk_short}}
Tras haber configurado su entorno, puede empezar a usar la CLI de {{site.data.keyword.openwhisk_short}} para hacer lo siguiente:

* Ejecutar sus fragmentos de código, o acciones, en {{site.data.keyword.openwhisk_short}}. Consulte
[Creación e invocación de acciones](./openwhisk_actions.html).
* Usar desencadenantes y reglas para permitir a sus acciones responder ante sucesos. Consulte
[Creación de desencadenantes y reglas](./openwhisk_triggers_rules.html).
* Aprenda a los paquetes agrupan acciones y configure orígenes de sucesos externos. Consulte [Uso y
creación de paquetes](./openwhisk_packages.html).
* Explore el catálogo de paquetes y mejore sus aplicaciones con servicios externos como un
[Origen de sucesos de Cloudant](./openwhisk_catalog.html#openwhisk_catalog_cloudant). Consulte [Uso de servicios habilitados para {{site.data.keyword.openwhisk_short}}](./openwhisk_catalog.html).


## Uso de {{site.data.keyword.openwhisk_short}} desde una app de iOS
Puede usar {{site.data.keyword.openwhisk_short}} desde su app de móvil iOS o Apple Watch usando el SDK de iOS de {{site.data.keyword.openwhisk_short}}. Para obtener más detalles, consulte la
[Documentación de iOS](./openwhisk_mobile_sdk.html).

## Uso de las API de REST con {{site.data.keyword.openwhisk_short}}
Tras habilitar su entorno {{site.data.keyword.openwhisk_short}}, puede usar
{{site.data.keyword.openwhisk_short}} con sus apps web o apps móviles con llamadas a la API de REST. Para obtener más detalles
sobre las API para acciones, activaciones, paquetes, reglas y desencadenantes, consulte la
[Documentación de la API de {{site.data.keyword.openwhisk_short}}](https://new-console.{DomainName}/apidocs/98).

## Ejemplo Hello World de {{site.data.keyword.openwhisk_short}}
Para empezar con {{site.data.keyword.openwhisk_short}}, intente el ejemplo de código JavaScript siguiente.

```
/**
 * Hello world como acción OpenWhisk.
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
invocar la acción `hello` cada vez que se genere un  suceso periódico.


## Detalles del sistema

Puede encontrar información adicional sobre {{site.data.keyword.openwhisk_short}} en los temas siguientes:

* [Nombre de entidad](./openwhisk_reference.html#openwhisk_entities)
* [Semánticas de acción](./openwhisk_reference.html#openwhisk_semantics)
* [Límites](./openwhisk_reference.html#openwhisk_syslimits)
* [API de REST](https://new-console.{DomainName}/apidocs/98)

# rellinks
## api
* [Documentación de API de REST](https://new-console.{DomainName}/apidocs/98){:new_window}

## general
* [Descubrir: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [{{site.data.keyword.openwhisk_short}} en IBM developerWorks](https://developer.ibm.com/openwhisk/){:new_window}
