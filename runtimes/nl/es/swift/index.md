{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Tiempo de ejecución de Swift
{: #swift_runtime}
*Última actualización: 10 de junio de 2016*
{: .last-updated}

El tiempo de ejecución de Swift en {{site.data.keyword.Bluemix}} está basado en el región propietaria del archivo de Swift para Bluemix (esto es, swift_buildpack).
swift_buildpack proporciona un entorno de ejecución completo para aplicaciones Swift.
{: shortdesc}

El swift_buildpack se utiliza si el directorio raíz de la aplicación contiene un archivo Package.swift.

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una aplicación de inicio Swift. La app de inicio de Swift es una app de Swift sencilla que puede utilizar para obtener más información sobre los tipos de aplicaciones de servidor que puede desarrollar utilizando el lenguaje de programación Swift. Esta app de ejemplo crea un servidor HTTP básico que devuelve el contenido HTML al cliente.

**Nota:** esta app de inicio no es una aplicación lista para producción.  En su lugar, está pensada para utilizarse para fines educativos.  Puede experimentar con la app de inicio, y realizar y enviar por push los cambios al entorno de {{site.data.keyword.Bluemix}}. Consulte [Utilización de las aplicaciones de inicio](../../cfapps/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de inicio.

## Versiones de tiempo de ejecución
{: #runtime_versions}

El swift_buildpack instalado en Bluemix da soporte a la versión  `DEVELOPMENT-SNAPSHOT-2016-05-03-a` de los binarios de Swift. Si desea utilizar una versión distinta de Swift en Bluemix para la aplicación, puede especificar la versión con un archivo `.swift-version` en la raíz del repositorio:

```
cat .swift-version
swift-DEVELOPMENT-SNAPSHOT-2016-04-25-a
```
{: pre}

Además de incluir un archivo `.swift-version`, también será necesario añadir el parámetro `-b https://github.com/IBM-Swift/swift-buildpack` al mandato `cf push` tal como se indica a continuación: 

```
cf push -b https://github.com/IBM-Swift/swift-buildpack
```

Para obtener una lista completa de las versiones soportadas por Swift, consulte el archivo [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/bluemix-buildpack/manifest.yml) del paquete de compilación.

Para obtener detalles sobre la versión actual del paquete de compilación de Swift instalado en {{site.data.keyword.Bluemix}}, consulte la [información de release](https://github.com/IBM-Swift/swift-buildpack/releases/tag/1.1.1) del paquete de compilación.

Puesto que hay frecuentes cambios en el idioma de Swift, debe incluir un archivo `.swift-version` para que la app se "ancle" a la versión de Swift con la que normalmente funciona la aplicación. Recuerde también que si está utilizando una versión de Swift distinta de `DEVELOPMENT-SNAPSHOT-2016-05-03-a`, deberá especificar el parámetro `-b https://github.com/IBM-Swift/swift-buildpack` cuando envíe por push la app (como se muestra a continuación). 

# rellinks
{: #rellinks}
## general
{: #general}
* [Paquete de compilación de Swift para Bluemix](https://github.com/IBM-Swift/swift-buildpack)
* [Documentación del idioma de Swift](https://swift.org/)
