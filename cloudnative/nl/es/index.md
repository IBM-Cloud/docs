---

copyright:
  years: 2016, 2017
lastupdated: "2016-04-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Creación de proyectos nativos en la nube
{: #web-mobile}

Puede gestionar apps nativas en cloud a través del concepto de [Proyectos](projects.html) de la {{site.data.keyword.dev_console}} de {{site.data.keyword.Bluemix}}. Puede crear un proyecto utilizando el [{{site.data.keyword.dev_console}}](devex.html) o [{{site.data.keyword.dev_cli_notm}}](dev_cli.html) para la CLI de {{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}}. La {{site.data.keyword.dev_console}} de {{site.data.keyword.Bluemix_notm}} ofrece las funcionalidades de servicio más comunes que son necesarias para un desarrollador móvil en una experiencia única y conectada que se ha optimizado para el desarrollador.

La {{site.data.keyword.dev_console}} de {{site.data.keyword.Bluemix_notm}} permite a un desarrollador de aplicaciones nativas en cloud crear un proyecto a partir de diversos [tipos de patrones](patterns.html) e [Iniciadores](starters.html), crear y conectar servicios optimizados clave de {{site.data.keyword.Bluemix_notm}} al proyecto, y descargar rápidamente código que funciona con los SDK. Los SDK se integran totalmente con las dependencias o credenciales de la prestación, que le permiten ejecutarla en unos minutos. Cuando la aplicación se esté ejecutando y haya configurado las funciones, puede volver al proyecto para supervisar y gestionar la colaboración con los usuarios de la aplicación. También puede configurar y gestionar los servicios a través de la {{site.data.keyword.dev_console}}.

<!--
While the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} provides an integrated development experience, some developers might still want to have finer-grained control and wire services together manually. If this is your preferred approach, you might want to consider using the [{{site.data.keyword.mobilefirstbp}} Starter boilerplate](try_mobile.html).
-->

<!--With {{site.data.keyword.Bluemix}} Mobile services, you can incorporate pre-built, managed, and scalable cloud services into your mobile applications. You can focus on building your mobile apps, instead of the complexities of managing the back-end infrastructure.

The Mobile dashboard provides an integrated experience on {{site.data.keyword.Bluemix_notm}} where you can create mobile projects easily from within the dashboard.
-->


## Proyectos
{: #projects}

La {{site.data.keyword.dev_console}} de {{site.data.keyword.Bluemix}} combina la interfaz de usuario, los datos y los servicios de la app en un *proyecto* completo. Al crear un proyecto, se mantienen todas las partes necesarias de la app y las prestaciones añadidas en el servidor de {{site.data.keyword.Bluemix_notm}}. Puede descargar el código de la app y las credenciales e iniciadores necesarios si los servicios están configurados en su proyecto. Puede ver todos sus proyectos seleccionando **Proyectos**.  

Para ver más información sobre un determinado proyecto, selecciónelo en la página **Proyectos**. Se abrirá la página **Visión general del proyecto**, que incluye los servicios configurados y disponibles para el proyecto. Los servicios son prestaciones independientes que amplían la app añadiendo una función. Debido a que se añaden individualmente, puede añadir los servicios que necesite, como los servicios push, de autenticación, datos y almacenamiento, entre otros. Cuando añade un servicio al proyecto en la página **Visión general del proyecto** y sigue las instrucciones para configurarlo, se asocia automáticamente a la app. Para obtener más información sobre la página Visión general del proyecto, consulte la [página Visión general del proyecto](project_overview_page.html).

Para crear el proyecto, debe seleccionar un [patrón](patterns.html), seguido por un [iniciador](starters.html).


### Página Visión general del proyecto
{: #project_overview}

Puede ver y trabajar con un único proyecto de la {{site.data.keyword.dev_console}} de {{site.data.keyword.Bluemix}} seleccionando el proyecto en la página **Proyectos**, que abre la página Visión general del proyecto. 
{: shortdesc}

La página **Visión general del proyecto** muestra un mosaico de cada prestación configurada o disponible para que se configure con el proyecto seleccionado. El mosaico muestra el tipo de prestación y un botón *acciones* con tres puntos alineados en vertical. Ejemplos de prestaciones que podrían estar disponibles o configuradas son {{site.data.keyword.mobilepushshort}}, Analytics, o Data and Storage. Las prestaciones compatibles dependen del tipo de proyecto y de las prestaciones disponibles en la región, de modo que no todas las prestaciones estarán disponibles para que se asocien con todos los proyectos. 

Cuando un tipo de prestación aún no está asociada al proyecto, se muestra el botón **Crear** en el mosaico. Las opciones del botón de acciones sirven para crear una instancia del servicio o para añadir una instancia de servicio existente cuando la prestación aún no está asociada. Si se selecciona **Añadir existentes**, se muestra una lista de instancias de servicio de dicho tipo en su espacio.

Si la prestación ya está asociada a este proyecto, el nombre de la instancia del servicio asociado se muestra en el mosaico tras el tipo de prestación. Esto facilita la búsqueda de la instancia de servicio relacionada con el proyecto en la {{site.data.keyword.dev_console}}. Las acciones que están disponibles en el botón de acciones son **Ver** y **Eliminar** cuando el servicio ya está asociado al proyecto. Cuando se elimina una instancia de servicio solo se elimina la asociación a este proyecto; no se suprime la instancia del servicio de la {{site.data.keyword.dev_console}}. Para suprimir una instancia de servicio, pulse la página **Web y móvil > Servicios** para ver y suprimir las instancias de servicio.

Seleccione **Obtener el código** en el mosaico **Código** para descargar el código correspondiente al proyecto. Para obtener más información sobre cómo descargar el código, consulte [Obtener código](get_code.html).


### Actualización del proyecto para utilizar un nuevo Iniciador
{: #update-starter}

1. Desde la página **Proyectos** o **Visión general del proyecto**, pulse el icono **Menú de desbordamiento** y seleccione **Actualizar iniciador**.

2. Elija un nuevo iniciador y pulse **Actualizar**.

3. Pulse **Obtener el código** en la página **Visión general del proyecto** para seleccionar el lenguaje.

   Como alternativa, pulse la página **Código**.


### Actualización del proyecto para generar un nuevo lenguaje
{: #update-language}

1. Desde las páginas **Proyectos** o **Visión general del proyecto**, pulse el icono **Menú de desbordamiento** y seleccione **Actualizar iniciador**.

2. Seleccione un nuevo lenguaje y pulse **Actualizar**.

3. Pulse **Obtener el código** en la página **Visión general del proyecto** para seleccionar el lenguaje.


## Tipos de patrón
{: #patterns}

Los patrones nativos en la nube son diseños probados que ayudan a garantizar una topología coherente, escalable y fiable para sus aplicaciones. Al crear un proyecto, se le presentan distintos tipos de patrón entre los que puede elegir. Seleccione el tipo de patrón y prestaciones que desea incorporar al proyecto. Después de definir las preferencias del proyecto, se genera un proyecto de iniciación para que edite, ejecute o depure y despliegue localmente o en {{site.data.keyword.Bluemix}}.


### App web
{: #web}

Los proyectos web añaden la capacidad de prestar contenido web, como HTML, JavaScript y hojas de estilo, al servidor web.

Están disponibles los siguientes iniciadores web:

* Basic Web: proporciona un archivo `index.html` estático, una hoja de estilo predeterminada y vacía y un archivo JavaScript.
* Webpack: crea un proyecto donde los archivos de origen de ECMAScript 6 (ES6) están en `src/client` y se compilan con WebPack para minificarlos y convertirlos para su uso en el navegador.
* Webpack + React: una infraestructura completa para crear interfaces de usuario. Los archivos de origen están en `src/client/app` y se compilarán con WebPack y se proporcionarán en el directorio público.


### App móvil
{: #mobile}

Los patrones de app móvil le ayudan a crear apps móviles que se conecten directamente a los servicios de fondo, como por ejemplo {{site.data.keyword.mobilepushshort}}, {{site.data.keyword.mobileanalytics_short}},
{{site.data.keyword.appid_short}}, etc. Los proyectos también se pueden añadir mediante sdkGen, como BFF y Microservicios.

Puede elegir entre una lista de iniciadores, como {{site.data.keyword.watson}} Conversation, {{site.data.keyword.visualrecognitionshort}}, {{site.data.keyword.openwhisk_short}}, etc.

Puede generar las apps móviles en Swift, Android o Cordova.


### Programa de fondo para programa de usuario (BFF)
{: #bff}

Los patrones de Programa de fondo para programa de usuario, normalmente conocidos como BFF, le ayudan a centrarse en exponer datos de negocio y servicios de una forma que coincida con los requisitos de interacción del usuario. Para optimizar un trayecto del usuario en su solución en la nube, puede que necesite un trayecto del usuario distinto para la aplicación móvil y un trayecto más rico y detallado para la aplicación web. Con la introducción de dispositivos controlados por voz como el servicio de [{{site.data.keyword.conversationfull}} ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://www.ibm.com/watson/developercloud/conversation.html), la interacción con un usuario se podría controlar mediante voz. Este canal digital necesitará un BFF muy distinto para gestionar estas interacciones basadas en intentos de voz.

Con {{site.data.keyword.Bluemix_notm}}, puede crear un BFF mediante un enfoque de programación políglota para definir el BFF. IBM recomienda utilizar Node.js, Swift, o Java y ejecutarlos en un patrón nativo de nube con Cloud Foundry, servicios de contenedor o sin servidor.

El BFF gestionará la integración con servicios para la persistencia, el almacenamiento en memoria caché y la integración de datos con servicios de alto valor como {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}}, y análisis de datos como {{site.data.keyword.sparks}}.

El BFF expondrá una API más comúnmente utilizando un patrón REST, pero puede diseñar el BFF para que funcione a partir de una arquitectura de mensajería utilizando {{site.data.keyword.messagehub}}.

Hay disponible un iniciador BFF Basic utilizando Node.js o Swift.


### Microservicio
{: #microservice}

Los proyectos de microservicio proporcionan la base para crear microservicios de fondo, incluyendo un punto final de estado básico y una API REST. Los proyectos generados contendrán todas las dependencias necesarias para el propio microservicio, así como para cualquier servicio en la nube adjunto.

Hay disponible un iniciador Microservice Basic utilizando Java.

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


### Lenguajes
{: #languages notoc}

Los lenguajes soportados son:

   * [Java ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](../runtimes/swift/getting-started.html){: new_window}


#### Java
{: #java notoc}

Java cuenta con prestaciones demostradas para crear aplicaciones empresariales. Pero las nuevas prestaciones de Java 8, combinadas con tiempos de ejecución más ligeros como Liberty e infraestructuras como Spring Boot, hacen que Java sea perfecto también para crear microservicios.


#### Node.js
{: #node notoc}

Node.js es un tiempo de ejecución de JavaScript que utiliza un modelo de E/S sin bloqueo y dirigido por sucesos, que lo hace ligero y eficiente, proporcionando un gran rendimiento y escalabilidad para aplicaciones web, patrones de programa de fondo para programa de usuario y microservicios. El ecosistema de paquetes de Node.js', npm, proporciona acceso a una gran recopilación de módulos de código abierto, con una amplia variedad de prestaciones para acelerar el desarrollo de las aplicaciones.


#### Swift
{: #swift notoc}

Swift es un lenguaje de programación moderno creado por Apple en 2014, que se ha diseñado para sustituir el uso de Objective C y el código abierto en diciembre de 2015. Actualmente, se utiliza para crear iOS, macOS, servicios web y software de sistemas en sistemas operativos Linux y macOS, que utilizan la arquitectura x86, ARM o Z. Escribe como un lenguaje de script pero se compila para obtener el alto rendimiento de C con una sobrecarga baja, lo que la convierte en la opción ideal para tiempos de ejecución en la nube. Utiliza un sistema de tipos estático y sólido que ve en Java, pero el estilo funcional y las rutinas asíncronas que ve en JavaScript. Ofrece un alto rendimiento, y el origen se compila en código nativo utilizando la cadena de herramientas del compilador LLVM y puede utilizar bibliotecas de sistemas externos escritas en C fácilmente.


## Iniciadores
{: #starters}

Con la {{site.data.keyword.dev_console}} de {{site.data.keyword.Bluemix}}, puede elegir entre una variedad de iniciadores para cada tipo de patrón.

Los iniciadores están optimizados para ser código del iniciador listo para la producción que se centra en demostrar una integración de {{site.data.keyword.Bluemix_notm}} clave con un servicio de alto valor. Cada iniciador se centra en un servicio y muestra la integración de los SDK del servicio en el código. En algunos casos, los iniciadores ofrecen una experiencia de usuario simple para resaltar la integración de los datos del servicio o de las interacciones con el usuario. Cada iniciador está configurado para habilitarse con Authentication, Data y posiblemente otras prestaciones, si decide configurarlas para el proyecto.
