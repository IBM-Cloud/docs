{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Tiempo de ejecución de Swift
{: #swift_runtime}
*Última actualización: 19 de febrero de 2016*

El tiempo de ejecución de Swift en {{site.data.keyword.Bluemix}} está basado en el swift_buildpack.
El swift_buildpack proporciona un entorno de ejecución completo para apps Swift.
{: shortdesc}

El swift_buildpack se utiliza si el directorio raíz de la aplicación contiene un archivo Package.swift.

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una aplicación de inicio Swift. La app de inicio de Swift es una app de Swift sencilla que puede utilizar para obtener más información sobre los tipos de aplicaciones de servidor que puede desarrollar utilizando el lenguaje de programación Swift. Esta app de ejemplo crea un servidor básico que devuelve un mensaje de bienvenida HTML al cliente.  

**Nota:** esta app de inicio no es una aplicación lista para producción.  En su lugar, está pensada para utilizarse para fines educativos.  Puede experimentar con la app de inicio, y realizar y enviar por push los cambios al entorno de {{site.data.keyword.Bluemix}}. Consulte [Utilización de las aplicaciones de inicio](../../cfapps/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de inicio.

## Versiones de tiempo de ejecución
{: #runtime_versions}

Puede especificar la versión de Swift que va a utilizar la app con un archivo `.swift`-version en la raíz del repositorio:

```
cat .swift-version
swift-DEVELOPMENT-SNAPSHOT-2016-02-03-a
```
{: pre}

Para obtener una lista completa de las versiones soportadas por Swift, consulte el archivo [manifest.yml](https://github.com/cloudfoundry-community/swift-buildpack/blob/master/manifest.yml) del paquete de compilación.

Para obtener detalles sobre la versión actual del paquete de compilación de Swift instalado en {{site.data.keyword.Bluemix}}, consulte la [información de release](https://github.com/cloudfoundry-community/swift-buildpack/releases/tag/v1.0.3) del paquete de compilación.

Puesto que hay frecuentes cambios en el idioma de Swift, debe incluir un archivo .swift-version para que la app se "ancle" a la versión de Swift con la que normalmente funciona la aplicación.

# rellinks
## general
* [Paquete de compilación de Cloud Foundry para Swift](https://github.com/cloudfoundry-community/swift-buildpack)
* [Documentación del idioma de Swift](https://swift.org/)
