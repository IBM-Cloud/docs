---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Cálculo
{: #compute}

Al crear una aplicación de canal digital nativo de la nube para móvil y mobile, la práctica recomendada es tener un BFF (Backend for Frontend, Programa de fondo para programa de usuario) que esté dedicado a su canal digital o que ofrezca el mismo soporte de integración lógica y de datos para las apps de clientes móviles y web. Para obtener más información sobre esta arquitectura, consulte [Microservicios para web y móvil ![icono de enlace externo](../icons/launch-glyph.svg)](https://www.ibm.com/devops/method/content/architecture/omnichannelArchitecture).

El siguiente diagrama muestra una visión general de la arquitectura de BFF.

![Arquitectura de BFF](images/bff-arch.png)

Figura 1: Arquitectura de BFF

El concepto de un BFF es omitir la lógica empresarial y de integración común de los servicios en la nube de {{site.data.keyword.Bluemix}} de microservicios o de alto valor.

Con esta arquitectura, puede desplegar y lanzar actualizaciones en su aplicación Web o móvil y desplegar versiones nuevas de su BFF utilizando Delivery Pipelines continuos con el servicio de devops.

Si tiene un BFF para iOS y un BFF independiente para Android, los equipos de ingeniería que entregan la función para estas apps no se restringen a características de release mediante una planificación de release de API centralizada. Este es un objetivo común para las arquitecturas de canal digital y de microservicio: permitir a los equipos que lancen funciones y características con frecuencia, sin estar completamente ligados a la planificación de release de otro equipo.

<!--
## Backend for Frontends (BFF)
{: #bff}

Backend for Frontend patterns, commonly known as BFFs, really help you to focus on exposing business data and services in a form that matches the user interaction requirements. To optimize a user journey to your cloud solution, it may require a different user journey for the mobile application and a richer, more detailed journey for the Web application. With the introduction of voice-controlled devices like the [{{site.data.keyword.conversationfull}} ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/conversation.html) service, the interaction with a user could be controlled by voice. This digital channel will require a very different BFF for managing these voice intent-based interactions.

With {{site.data.keyword.Bluemix_notm}}, you can build a BFF by using polyglot programming approach to define the BFF. IBM recommends using Node, Swift, or Java and running them in a cloud native pattern with either Cloud Foundry, Container services, or serverless.

The BFF will manage the integration with services for data persistence, caching, and integration with high-value services like {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}}, and data analytics like {{site.data.keyword.sparks}}.

The BFF will expose an API most commonly using a REST pattern, but you can design your BFF to work from a messaging architecture using {{site.data.keyword.messagehub}}.
-->


## Integración de un cliente móvil con un Programa de fondo para programa de usuario
{: #integration}

Para habilitar la integración sencilla entre un cliente móvil y un BFF, {{site.data.keyword.Bluemix_notm}} da soporte a la generación de SDK del cliente móvil para iOS y Android en los lenguajes Swift y Java, respectivamente. Para habilitar esta característica, debe exponer la integración de BFF con un documento de especificación de Open API (Swagger). Este documento puede estar en la forma de JSON o YAML.

El generador de SDK del cliente utiliza el archivo de definición de Open API para definir un SDK de desarrollador optimizado por el cliente que sea sencillo de consumir en la aplicación móvil nativa. Acelerará la integración del BFF en la aplicación móvil.


## Definición de una API
{: #definition}

El BFF debe exponer un archivo de definición de API que se ajuste a la especificación de Open API que se está ejecutando en un punto final de servidor activo. Para habilitar la Experiencia de desarrollador de {{site.data.keyword.Bluemix_notm}} y la CLI (Command Line Interface, Interfaz de línea de mandatos) de SDK de {{site.data.keyword.Bluemix_notm}} para descubrir este punto final, debe añadir una variable de entorno a la aplicación de Cloud Foundry denominada `OPENAPI_SPEC`. Esta variable de entorno debe hacer referencia a la especificación utilizando una vía de acceso relativa.

Para añadir la variable de entorno `OPENAPI_SPEC` en {{site.data.keyword.Bluemix_notm}}, siga estos pasos:

1. Inicie sesión en [{{site.data.keyword.Bluemix_notm}} ![icono de enlace externo](../icons/launch-glyph.svg)](http://bluemix.net).
2. Seleccione una app de Cloud Foundry.
3. Seleccione **Tiempo de ejecución**.
4. Seleccione **Variables de entorno**.
5. Pulse **Añadir** en la sección **Definido por el usuario**.
6. Especifique `OPENAPI_SPEC` para **NAME** y una vía de acceso de URL relativo en su archivo de definición de Open API.
7. Pulse **Guardar**.

<!--
To add the `OPENAPI_SPEC` environment variable locally and push your changes to {{site.data.keyword.Bluemix_notm}} with the [Cloud Foundry CLI ![External link icon](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli#getting-started), follow these steps:

1. Open Terminal and navigate to your project directory.
2. Add the following code to the `manifest.yml` file.

   ```
   env:
       "OPENAPI_SPEC": "<relative URL path to your Open API definition file>"
   ```
   {: codeblock}
3. Save your changes to the `manifest.yml` file.
4. Run `cf push` to deploy the changes to {{site.data.keyword.Bluemix_notm}}.
-->

Por ejemplo:

```
OPENAPI_SPEC='/explorer/swagger.json'
```
{: codeblock}

{{site.data.keyword.apiconnect_long}} y las aplicaciones Loopback funcionan particularmente bien utilizando este enfoque. Puede utilizar Loopback y {{site.data.keyword.apiconnect_short}} para definir un modelo persistente y exponer la operación CRUD (Create, Read, Update, and Delete - crear, recuperar, actualizar y suprimir) mediante el archivo de definición de Open API.

También puede definir operaciones de lógica empresarial.


### Elementos soportados de la especificación de Open API
{: #supported-elements notoc}

La única parte de la especificación de Open API que no está completamente soportada en la estructura de archivos. La especificación permite que se dividan partes de la definición en distintos archivos y que se haga referencia a ellas mediante el archivo `$ref` de json. Toda su definición debe estar contenida en un único archivo.


## Programa de fondo para programa de usuario de ejemplo utilizando Bluegen
{: #bff-bluegen}

{{site.data.keyword.Bluemix_notm}} ha creado un BFF de referencia utilizando {{site.data.keyword.apiconnect_short}} y Strongloop, que correlaciona un modelo de producto en un {{site.data.keyword.cloudant}} y una API de imagen para hacer referencia a imágenes en {{site.data.keyword.objectstorageshort}}.

Puede utilizar este patrón de BFF para iniciarse rápidamente con el suministro de un BFF que funcione completamente en {{site.data.keyword.Bluemix_notm}} y utilizarlo para ayudar a comprender la facilidad con que se integra un BFF en un proyecto móvil y se generan SDK nativos para iOS y Android en Swift y Java, respectivamente.

Siga las instrucciones de [README ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/backend-for-frontend-node) para crear un proyecto e instalarlo.


## Uso de Programa de fondo para programa de usuario con un proyecto de experiencia de desarrollador
{: #bff-devex}

La experiencia de desarrollador móvil de {{site.data.keyword.Bluemix_notm}} está diseñada para simplificar la definición de un proyecto móvil con varios servicios en la nube asociados. Puede añadir de forma sencilla [{{site.data.keyword.mobilepushshort}} ![icono de enlace externo](../icons/launch-glyph.svg)](/docs/services/mobilepush/index.html), [Analytics ![icono de enlace externo](../icons/launch-glyph.svg)](/docs/services/mobileanalytics/index.html), y servicios de Datos o Almacenamiento.

La {{site.data.keyword.dev_console}} de {{site.data.keyword.Bluemix_notm}} ha introducido la capacidad de integrar un BFF en un proyecto móvil en la página **Cálculo**. Puede añadir instancias de servicio de Cálculo existentes en su proyecto móvil. Una vez que se añadan, puede generar un SDK nativo para su elección de idioma o puede generar el proyecto completo y el SDK se integrará en el paquete de origen del proyecto en la página **Código**. Esto es particularmente útil cuando se integra con BFF que ya están bien definidas.

Una vez que haya descargado el proyecto, podrá abrirlo con Xcode o Android Studio y compilar el proyecto con el SDK de cliente.


## Utilización de la CLI
{: #cli}

A medida que desarrolle su BFF, la especificación de la API podría cambiar. Para admitir estos cambios, tiene las dos siguientes opciones.

* Volver a generar todo el proyecto en una rama nueva de GitHub y fusionar los cambios en la rama de desarrollo.
* Volver a generar el SDK directamente utilizando la herramienta de línea de mandatos (CLI) y actualizar sólo la parte del SDK del proyecto móvil.

Para utilizar la CLI, debe [instalarla](sdk_cli.html#installation).

Utilice el siguiente mandato para listar las acciones que puede realizar.

```
bluemix sdk
```
{: codeblock}

Utilice el siguiente mandato para listar las instancias de Cloud Foundry en ejecución en el espacio actual de {{site.data.keyword.Bluemix_notm}}.

```
bluemix sdk list
```
{: codeblock}

Cada app está listada y la API se validará si está establecida la variable de entorno `OPENAPI_SPEC`. En la columna `VALID`, verá una marca de selección verde o una `X` roja. Una marca de selección en la columna `VALID` para la aplicación significa que hay una definición de Open API válida. Una `X` en la columna `VALID` para la aplicación significa una de dos cosas:

* una variable de entorno `OPENAPI_SPEC` no está definida para su aplicación O
* la definición de la API no es válida con respecto a la especificación de Open API

Utilice el siguiente mandato para ver el URL completamente formado para la API. Se lista la ruta y el URI completamente formados en la especificación de la API. Puede ver la especificación sin procesar en un navegador, consumirla directamente en la CLI, o verificar que la variable de entorno de `OPENAPI_SPEC` de BFF se haya establecido correctamente.

```
bluemix sdk list --url
```
{: codeblock}

Utilice el siguiente mandato para validar el archivo de definición de Open API del `<Nombre_App>` para determinar si se puede utilizar para generar un SDK. El mandato busca `<Nombre_App>` en el espacio actual y utiliza la vía de acceso relativa en la variable de entorno `OPENAPI_SPEC` para localizar la especificación para la validación.

```
bluemix sdk validate <AppName>
```
{: codeblock}

Utilice el siguiente mandato para generar un SDK para la `<Plataforma>` nativa que elija y coloque un archivo comprimido en el directorio de trabajo actual.

```
bluemix sdk generate <AppName> <SDKName> --<Platform>
```
{: codeblock}

El uso de la opción `--unzip` extraerá automáticamente el SDK en el directorio de trabajo actual. Opcionalmente, puede especificar la ubicación en la que se extraerá el SDK utilizando la opción `--output`. Puede gestionar su código fuente con GitHub y crear una rama nueva específicamente para actualizar el SDK. El uso de este enfoque facilita la visualización de los cambios y la fusión en el SDK actualizado en la rama de desarrollo.


## Cómo trabajar con modelos generados por SDK y API
{: #models-apis}

Ahora que BFF está integrado en la app móvil utilizando un SDK generado, puede empezar a trabajar con él.

El SDK se proporciona con documentación totalmente generada en los directorios `docs` y `source`. Puede abrir el archivo `README.html` para una vista web de los documentos o puede abrir el archivo `README.md` para una vista Markdown de los documentos. Los documentos de Markdown son útiles al publicar el SDK en Cocoapods o en Maven Central.

En la documentación, podrá ver una lista de API generadas. Puede pulsar en la API para ver un fragmento de código que pueda pegar directamente en la app para móvil.
