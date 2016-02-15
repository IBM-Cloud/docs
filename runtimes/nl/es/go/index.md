{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*Última actualización: 12 de enero de 2016*

# Tiempo de ejecución de Go
{: #go_runtime}

El tiempo de ejecución de Go en {{site.data.keyword.Bluemix}} está basado en go_buildpack.
go_buildpack proporciona un entorno de tiempo de ejecución completo para las apps de Go.
{: shortdesc}

go_buildpack se utiliza si la aplicación contiene un archivo denominado *.go.

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una aplicación de inicio de Go. La aplicación de inicio de Go es una app de Go simple que proporciona una plantilla que puede utilizar para la app. Puede experimentar con la app de inicio, y realizar y enviar por push cambios al entorno de Bluemix. Consulte [Utilización de las aplicaciones de iniciador](../../cfapps/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de iniciador.

## Versiones de tiempo de ejecución
{: #runtime_versions}

Puede especificar la versión de Go que utilizará la app estableciendo la propiedad de GoVersion en el archivo Godeps/Godeps.json en la raíz de la aplicación. Por ejemplo:

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.3.3",
	"Deps": []
}
```
{: codeblock}
Para obtener más información,
consulte [godep](https://github.com/tools/godep).

### Versiones disponibles:
{: #available_versions}

Las siguientes versiones de Go están disponibles en el
[paquete de compilación de Go](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.6.2)
instalado actualmente en {{site.data.keyword.Bluemix}}:

* 1.2.1
* 1.2.2
* 1.3.2
* 1.3.3
* 1.4.2
* 1.4.3
* 1.5
* 1.5.1

Si la app requiere una versión de Go que no aparece en la lista,
puede utilizar el
[paquete de compilación de Go](https://github.com/cloudfoundry/go-buildpack.git) externo para desplegar
la aplicación.

## ENLACES RELACIONADOS
{: #related_links}
* [GoLang](http://golang.org/)
* [Paquete de compilación de Cloud Foundry para Go](https://github.com/cloudfoundry/go-buildpack)
