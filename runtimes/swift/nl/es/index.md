{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# IBM Bluemix Runtime for Swift
{: #swift_runtime}
Última actualización: 19 de septiembre de 2016
{: .last-updated}

Runtime for Swift en {{site.data.keyword.Bluemix}} está basado en el paquete de compilación [IBM Bluemix para Swift](https://github.com/IBM-Swift/swift-buildpack) (es decir, swift_buildpack).
Este paquete de compilación proporciona un entorno de tiempo de ejecución completo para aplicaciones Swift.
{: shortdesc}

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una [aplicación de inicio](https://github.com/IBM-Swift/Kitura-Starter-Bluemix) Swift basada en Kitura. La app de inicio Kitura es una sencilla aplicación Swift que se puede utilizar para conocer los tipos de aplicaciones de servidor que se pueden desarrollar utilizando el lenguaje de programación Swift. Esta app de ejemplo crea un servidor HTTP Kitura básico que devuelve contenido HTML al cliente.

**Nota:** la app de inicio Kitura se ha diseñado con finalidades formativas. Puede practicar con la app de inicio aplicando mejoras y enviando los cambios al entorno de {{site.data.keyword.Bluemix}}. Consulte [Utilización de las aplicaciones de inicio](../../cfapps/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de inicio.

## Cambio de nombre de una app
{: #renaming_your_app}

Si desea cambiar el nombre de su app, desde la aplicación de inicio Kitura o de forma más general, es necesario aplicar algunos cambios. De este modo, se evitarán confusiones y se garantizará un despliegue sin errores.

- Cambie el nombre de la carpeta de proyecto de la app para que coincida con el nombre de la app.
- `Package.swift`: cambie las siguientes entradas:
    - `name`: debe coincidir con el nombre de la app
    - `targets[Target(name:)]`: debe coincidir con el nombre de la app
- `manifest.yml`: cambie las siguientes entradas;
    - `name`: debe coincidir con el nombre de la app
    - `host`: representa el segmento del host primario del URL de la app
- `Procfile`: el valor de `web` debe coincidir con el nombre del directorio de la app. Es el mandato que se ejecuta después de la compilación para iniciar la app web.


## Versiones de Runtime
{: #runtime_versions}

De forma predeterminada, el Runtime for Swift (swift_buildpack) alojado en {{site.data.keyword.Bluemix}} utiliza la versión de GA más reciente de los binarios de Swift. Esta es la única versión a la que da soporte directo IBM y es la versión recomendada para utilizar en su app. Puede comprobar la versión consultando la [información del último](https://github.com/IBM-Swift/swift-buildpack/releases) de swift_buildpack. El paquete de compilación puede listar otras versiones de Swift, tal como se indica en el archivo [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml). Estas versiones de Swift, comunes pero no soportadas, se almacenan previamente en la memoria caché dentro del paquete de compilación, que proporciona un tiempo de suministro reducido.

Si desea utilizar otra versión de Swift en {{site.data.keyword.Bluemix}} para su aplicación, especifíquela con un archivo `.swift-version` en la raíz del repositorio. El archivo `.swift-version` define la versión de Swift que debe utilizar el paquete swift_buildpack.

```
$ cat .swift-version
3.0
```
{: pre}

Como hay frecuentes actualizaciones de idioma de Swift, se recomienda incluir siempre un archivo `.swift-version` para que la app esté marcada junto con la versión de Swift que se sabe que funciona con su aplicación.

Tenga en cuenta que puede especificar cualquier versión válida de Swift en el archivo `.swift-version`. Las versiones alternativas deben coincidir con la denominación de [Swift.org](https://swift.org/download/), desde donde se obtienen directamente. Al utilizar una versión no almacenada en la memoria caché, el tiempo de suministro será superior, pero no hay diferencia de rendimiento de tiempo de ejecución en la app Swift.

Se utiliza el swift_buildpack predeterminado en {{site.data.keyword.Bluemix}} si el directorio raíz de la app contiene un archivo `Package.swift`.  Si desea utilizar un paquete de compilación alternativo, especifíquelo añadiendo una entrada `buildpack: {buildpackUrl}` al archivo manifest.yml de la app. Si lo prefiere, puede definir esta opción durante el tiempo de despliegue, utilizando el argumento de mandato `cf push -b {buildpackUrl}`.


## Entornos de desarrollador

Los desarrolladores tienen varias opciones al crear aplicaciones de lado de servidor con Swift. Es posible que aquellos que utilicen un dispositivo MacOS de Apple prefieran usar Xcode IDE, aunque no es obligatorio. Las apps basadas en Swift que se desplieguen y ejecuten en {{site.data.keyword.Bluemix}} pueden utilizar cualquier editor de programación o IDE.  El realce y la elevación de la sintaxis de Swift están disponibles para muchos editores conocidos. La herramienta de línea de mandatos Swift REPL incluida en los binarios de [Swift.org](https://swift.org/) permiten la compilación y realización de pruebas local antes del despliegue en {{site.data.keyword.Bluemix}}.

Los usuarios de MaxOS pueden utilizar [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/) para simplificar la creación, el despliegue, la gestión y el control de las apps Swift que se ejecuten en {{site.data.keyword.Bluemix}}.  


## Mejora de la integración

Trabajar con la [infraestructura web Kitura](http://ibm-swift.github.io/Kitura/) ofrece multitud de prestaciones. Kitura es modular por naturaleza y pronto deseará ampliar su funcionalidad con SDK empaquetados para obtener funciones como la autenticación, el acceso a servicios basados en Watson y una amplia variedad de bases de datos. Kitura ofrece soporte directo para muchas bases de datos, mientras que otros proyectos de código abierto también ofrecen SDK para numerosas plataformas de bases de datos. A continuación, se muestra una lista no exhaustiva de SDK proporcionados por Kitura para trabajar con recursos externos.

- [IBM Watson](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/swift-watson-sdk)
- [IBM DB2 and DashDB](https://swiftpkgs.ng.bluemix.net/package/IBM-DTeam/swift-for-db2)
- [IBM Cloudant and Couchbase](https://swiftpkgs.ng.bluemix.net/package/cloudant/swift-cloudant)
- [IBM ObjectStorage](https://swiftpkgs.ng.bluemix.net/package/ibm-bluemix-mobile-services/bluemix-objectstorage-serversdk-swift)
- [Apache Cassandra](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Kassandra)
- [Aphid MQTT](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Aphid)

Para obtener más información sobre los paquetes Swift que se pueden incluir en la aplicación, vaya al [Catálogo de paquetes de IBM Swift](https://swiftpkgs.ng.bluemix.net/) y busque el servicio de destino o la base de datos. El catálogo de paquetes permite buscar fácilmente los paquetes que desea incluir en las aplicaciones Swift. Los paquetes se pueden añadir a una aplicación Swift incluyendo el URL de Git del paquete y la información de versión en el archivo `Package.swift` de la app. Para obtener más información sobre la gestión de paquetes, consulte la sección [Gestor de paquetes de Swift.org](https://swift.org/package-manager/).


## Información relacionada

Existen otras herramientas en línea disponibles desde IBM para el desarrollador de Swift.
- [IBM Swift DevCenter](https://developer.ibm.com/swift/): sitio de inicio principal para toda la información de IBM Swift. Encontrará información sobre ofertas, blogs, eventos sociales, documentación, etc.
- [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/): este sitio proporciona un entorno donde probar rápida y fácilmente fragmentos de código Swift en varias versiones de Swift e incluso en otras plataformas de tiempo de ejecución de Swift. También puede guardar y compartir ejemplos de código con otros usuarios y explorar ejemplos populares proporcionados por otras personas.


# rellinks
{: #rellinks}
## general
{: #general}
* [IBM Swift DevCenter](https://developer.ibm.com/swift/)
* [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)
* [Catálogo de paquetes de IBM Swift](https://swiftpkgs.ng.bluemix.net/)
* [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/)
* [Documentación y API de Kitura](http://ibm-swift.github.io/Kitura/)
* [App de inicio de Kitura para Bluemix](https://github.com/IBM-Swift/Kitura-Starter-Bluemix)
* [Paquete de compilación de IBM Bluemix para Swift](https://github.com/IBM-Swift/swift-buildpack)
* [Notas de release del paquete de compilación de IBM Bluemix para Swift](https://github.com/IBM-Swift/swift-buildpack/releases)
* [Swift.org](https://swift.org/)
* [Documentación del idioma de Swift](https://swift.org/documentation)
