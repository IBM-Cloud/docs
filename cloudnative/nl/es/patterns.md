
---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Tipos de patrón
{: #patterns}

Los patrones nativos en la nube son diseños probados que ayudan a garantizar una topología coherente, escalable y fiable para sus aplicaciones. Al crear un proyecto, se le presentan distintos tipos de patrón entre los que puede elegir. Seleccione el tipo de patrón y prestaciones que desea incorporar al proyecto. Después de definir las preferencias del proyecto, se genera un proyecto de iniciación para que edite, ejecute o depure y despliegue localmente o en {{site.data.keyword.Bluemix}}.

## Aplicación web
{: #web}

Los proyectos web añaden la capacidad de prestar contenido web, como HTML, JavaScript y hojas de estilo, al servidor web.

Están disponibles los siguientes iniciadores web:

* Basic Web: proporciona un archivo `index.html` estático, una hoja de estilo predeterminada y vacía y un archivo JavaScript.
* Webpack: crea un proyecto donde los archivos de origen de ECMAScript 6 (ES6) están en `src/client` y se compilan con WebPack para minificarlos y convertirlos para su uso en el navegador. 
* Webpack + React: una infraestructura completa para crear interfaces de usuario. Los archivos de origen están en `src/client/app` y se compilarán con WebPack y se proporcionarán en el directorio público.


## App móvil
{: #mobile}

Los patrones de app móvil le ayudan a crear aplicaciones móviles que se conecten directamente a los servicios de fondo, como por ejemplo {{site.data.keyword.mobilepushshort}}, {{site.data.keyword.mobileanalytics_short}},
{{site.data.keyword.appid_short}}, etc. Los proyectos también se pueden añadir mediante sdkGen, como BFF y Microservicios.

Puede elegir entre una lista de iniciadores, como {{site.data.keyword.watson}} Conversation, {{site.data.keyword.visualrecognitionshort}}, {{site.data.keyword.openwhisk_short}}, etc.

Puede generar las apps móviles en Swift, Android o Cordova.


## Programa de fondo para programa de usuario (BFF)
{: #bff}

Los patrones de Programa de fondo para programa de usuario, normalmente conocidos como BFF, le ayudan a centrarse en exponer datos de negocio y servicios de una forma que coincida con los requisitos de interacción del usuario. Para optimizar un trayecto del usuario en su solución en la nube, puede que necesite un trayecto del usuario distinto para la aplicación móvil y un trayecto más rico y detallado para la aplicación web. Con la introducción de dispositivos controlados por voz como el servicio de [{{site.data.keyword.conversationfull}} ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://www.ibm.com/watson/developercloud/conversation.html), la interacción con un usuario se podría controlar mediante voz. Este canal digital necesitará un BFF muy distinto para gestionar estas interacciones basadas en intentos de voz.

Con {{site.data.keyword.Bluemix_notm}}, puede crear un BFF mediante un enfoque de programación políglota para definir el BFF. IBM recomienda utilizar Node.js, Swift, o Java y ejecutarlos en un patrón nativo de nube con Cloud Foundry, servicios de contenedor o sin servidor.

El BFF gestionará la integración con servicios para la persistencia, el almacenamiento en memoria caché y la integración de datos con servicios de alto valor como {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}}, y análisis de datos como {{site.data.keyword.sparks}}.

El BFF expondrá una API más comúnmente utilizando un patrón REST, pero puede diseñar el BFF para que funcione a partir de una arquitectura de mensajería utilizando {{site.data.keyword.messagehub}}.

Hay disponible un iniciador BFF Basic utilizando Node.js o Swift.


## Microservicio
{: #microservice}

Los proyectos de microservicio proporcionan la base para crear microservicios de fondo, incluyendo una terminal de estado básica y una API REST. Los proyectos generados contendrán todas las dependencias necesarias para el propio microservicio, así como para cualquier servicio en la nube adjunto.

Hay disponible un iniciador Microservice Basic utilizando Java.

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


## Lenguajes
{: #languages notoc}

Los lenguajes soportados son:

   * [Java ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](../runtimes/swift/getting-started.html){: new_window}


### Java
{: #java notoc}

Java cuenta con prestaciones demostradas para crear aplicaciones empresariales. Pero las nuevas prestaciones de Java 8, combinadas con tiempos de ejecución más ligeros como Liberty e infraestructuras como Spring Boot, hacen que Java sea perfecto también para crear microservicios.


### Node.js
{: #node notoc}

Node.js es un tiempo de ejecución de JavaScript que utiliza un modelo de E/S sin bloqueo y dirigido por sucesos, que lo hace ligero y eficiente, proporcionando un gran rendimiento y escalabilidad para aplicaciones web, patrones de programa de fondo para programa de usuario y microservicios. El ecosistema de paquetes de Node.js', npm, proporciona acceso a una gran recopilación de módulos de código abierto, con una amplia variedad de prestaciones para acelerar el desarrollo de las aplicaciones.


### Swift
{: #swift notoc}

Swift es un lenguaje de programación moderno creado por Apple en 2014, que se ha diseñado para sustituir el uso de Objective C y el código abierto en diciembre de 2015. Actualmente, se utiliza para crear iOS, macOS, servicios web y software de sistemas en sistemas operativos Linux y macOS, que utilizan la arquitectura x86, ARM o Z. Escribe como un lenguaje de script pero se compila para obtener el alto rendimiento de C con una sobrecarga baja, lo que la convierte en la opción ideal para tiempos de ejecución en la nube. Utiliza un sistema de tipos estático y sólido que ve en Java, pero el estilo funcional y las rutinas asíncronas que ve en JavaScript. Ofrece un alto rendimiento, y el origen se compila en código nativo utilizando la cadena de herramientas del compilador LLVM y puede utilizar bibliotecas de sistemas externos escritas en C fácilmente. 
