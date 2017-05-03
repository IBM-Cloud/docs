---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# IBM Bluemix Runtime for Swift
{: #swift_runtime}

Runtime for Swift en {{site.data.keyword.Bluemix}} está basado en el [paquete de compilación de IBM Bluemix for Swift](https://github.com/IBM-Swift/swift-buildpack) (es decir, swift_buildpack).
El paquete de compilación proporciona un entorno de ejecución completo para aplicaciones Swift.
{: shortdesc}

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una [aplicación de inicio](https://github.com/IBM-Bluemix/Kitura-Starter) Swift basada en Kitura. La app de inicio de Kitura es una app de Swift sencilla que puede utilizar para obtener más información sobre los tipos de aplicaciones de servidor que puede desarrollar utilizando el lenguaje de programación Swift. Esta app de ejemplo crea un servidor HTTP Kitura básico que devuelve el contenido HTML al cliente.

**Nota:** la aplicación de inicio de Kitura está pensada para utilizarse para fines educativos. Puede experimentar con la app de inicio realizando mejoras y enviar por push dichos cambios al entorno de {{site.data.keyword.Bluemix}}. Consulte [Utilización de las aplicaciones de inicio](../../cfapps/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de inicio.

## Cambiar el nombre de la app
{: #renaming_your_app}

Si desea cambiar el nombre de la app, desde el iniciador de Kitura, o en general, es necesario llevar a cabo unos pocos cambios. Esto evitará confusión y garantizará un despliegue sin errores.

- Cambie el nombre de la carpeta de proyecto de la app para que coincida con el nombre de su app.
- `Package.swift`: cambie las siguientes entradas:
    - `name`: debe coincidir con el nombre de la app.
    - `targets[Target(name:)]`: debe coincidir con el nombre de la app.
- `manifest.yml`: cambie las siguientes entradas:
    - `name`: debe coincidir con el nombre de la app.
    - `command` - El nombre del ejecutable para iniciar la app (debe coincidir con el nombre especificado en el archivo Package.swift).

## Versiones de tiempo de ejecución
{: #runtime_versions}

De forma predeterminada, Runtime for Swift (swift_buildpack) alojado en {{site.data.keyword.Bluemix}} utiliza la última versión de GA de los binarios de Swift. Esta es la única versión de Swift soportada directamente por IBM, y es la versión que se recomienda utilizar en su app. Puede determinar esta versión soportada examinando la [información del último release](https://github.com/IBM-Swift/swift-buildpack/releases) de swift_buildpack. El paquete de compilación puede listar otras versiones de Swift tal como se muestra en su archivo [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml). Estas versiones comunes, pero no soportadas, de Swift se han almacenado en memoria caché previamente dentro del paquete de compilación, lo que proporciona un tiempo de suministro reducido.

Si desea utilizar una versión distinta de Swift en {{site.data.keyword.Bluemix}} para la aplicación, puede especificar la versión con un archivo `.swift-version` en la raíz del repositorio. Este archivo `.swift-version` define qué versión de Swift va a utilizar swift_buildpack.

```
$ cat .swift-version
3.0
```
{: pre}

Puesto que hay frecuentes actualizaciones en el idioma de Swift, siempre debe incluir un archivo `.swift-version` para que la app se "ancle" a la versión de Swift con la que normalmente funciona la aplicación.

Tenga en cuenta que puede especificar cualquier versión válida de Swift en el archivo `.swift-version`. These alternate versions must match the naming of and are pulled directly from [Swift.org![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://swift.org/download/) Aunque al utilizar una versión no almacenada en memoria caché se tardará más en el suministro, no hay diferencia de rendimiento del tiempo de ejecución de la app Swift.

Se utiliza el swift_buildpack predeterminado en {{site.data.keyword.Bluemix}} si el directorio raíz de la app contiene un archivo `Package.swift`.  Si desea utilizar un paquete de compilación alternativo, debe especificarlo añadiendo una entrada `buildpack: {buildpackUrl}` en el archivo manifest.yml de la app. De forma alternativa, puede definirlo en el momento del despliegue utilizando el argumento de mandatos `cf push -b {buildpackUrl}`.


## Entornos de desarrollador

Los desarrolladores tienen varias opciones al crear aplicaciones del lado del servidor con Swift. Los que utilizan un dispositivo MacOS de Apple pueden preferir utilizar el IDE de Xcode, aunque esto no es un requisito.  Las apps basadas en Swift que se desplegarán y ejecutarán en {{site.data.keyword.Bluemix}} pueden utilizar cualquier editor de programación o IDE.  El realce y la comprobación de la sintaxis para Swift está disponible para muchos editores populares. La herramienta de línea de mandatos REPL de Swift que se incluye en los binarios desde [Swift.org![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://swift.org/), permite una compilación y comprobación local antes de desplegar en {{site.data.keyword.Bluemix}}.

Para usuarios MaxOS, puede utilizar [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/) que simplifica la creación, el despliegue, la gestión y el control de apps de Swift del lado del servidor que se ejecutan en {{site.data.keyword.Bluemix}}.  


## Integración mejorada

Trabajar con la [infraestructura web de Kitura](http://ibm-swift.github.io/Kitura/) proporciona muchas prestaciones. Kitura es modular por naturaleza y pronto verá ampliada su funcionalidad con SDK empaquetados, para proporcionar características tales como la autenticación, el acceso a servicios basados en Watson y una amplia variedad de bases de datos.  Kitura proporciona soporte para muchas bases de datos directamente, aunque otros proyectos de código abierto también proporcionan SDK para muchas plataformas de base de datos. A continuación encontrará una lista no exhaustiva de los SDK proporcionados por Kitura para trabajar con recursos externos.

- [IBM Watson](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/swift-watson-sdk)
- [IBM DB2 y DashDB](https://swiftpkgs.ng.bluemix.net/package/IBM-DTeam/swift-for-db2)
- [IBM Cloudant y CouchDB](https://swiftpkgs.ng.bluemix.net/package/cloudant/swift-cloudant)
- [IBM ObjectStorage](https://swiftpkgs.ng.bluemix.net/package/ibm-bluemix-mobile-services/bluemix-objectstorage-serversdk-swift)
- [Apache Cassandra](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Kassandra)
- [Aphid MQTT](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Aphid)

Para encontrar más paquetes Swift para incluir en la aplicación, vaya al [Catálogo de paquetes de IBM Swift](https://swiftpkgs.ng.bluemix.net/) y realice una búsqueda sobre la base de datos o el servicio de destino. El Catálogo de paquetes proporciona una forma fácil de localizar paquetes que puede incluir en las aplicaciones Swift. Los paquetes pueden añadirse a una aplicación Swift incluyendo los detalles de versión y el URL de Git del paquete en el archivo `Package.swift` de la app. Para obtener más detalles sobre la gestión de paquetes, consulte la [sección de Package Manager de Swift.org](https://swift.org/package-manager/).


## Información relacionada

También hay otras herramientas en línea disponibles en IBM para el desarrollador de Swift.
- [IBM Swift DevCenter](https://developer.ibm.com/swift/): sitio de destino principal para toda la información de IBM Swift. Puede encontrar información sobre nuestras ofertas, blogs, eventos sociales, documentación y más.
- [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/): este sitio proporciona un entorno para probar rápidamente y fácilmente fragmentos de código de Swift frente a varias versiones de Swift e incluso en distintas plataformas de tiempo de ejecución de  Swift. También puede guardar y compartir ejemplos de código con otros, así como explorar ejemplos populares proporcionados por otros.


# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [IBM Swift DevCenter](https://developer.ibm.com/swift/)
* [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)
* [IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/)
* [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/)
* [Documentación y API de Kitura](http://ibm-swift.github.io/Kitura/)
* [App de inicio de Kitura para Bluemix](https://github.com/IBM-Bluemix/Kitura-Starter)
* [Paquete de compilación de IBM Bluemix for Swift](https://github.com/IBM-Swift/swift-buildpack)
* [Notas del release del paquete de compilación de IBM Bluemix for Swift](https://github.com/IBM-Swift/swift-buildpack/releases)
* [Swift.org ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://swift.org/)
* [Documentación del lenguaje Swift ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://swift.org/documentation)
