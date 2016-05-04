---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Ir
{: #go_runtime}
*Última actualización: 16 de marzo de 2016*

El tiempo de ejecución de Go en {{site.data.keyword.Bluemix}} está basado en go_buildpack.
El go_buildpack proporciona un entorno de ejecución completo para aplicaciones Go.
{: shortdesc}

El go_buildpack se utiliza si la aplicación contiene un archivo denominado *.go.

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una aplicación de inicio Go.  La aplicación de inicio Go es una aplicación sencilla Go que proporciona una plantilla que puede utilizar para la app. Puede experimentar con la app de inicio, y realizar y enviar los cambios al entorno de Bluemix. Consulte [Utilización de las aplicaciones de iniciador](../../cfapps/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de inicio.

## Versiones de tiempo de ejecución
{: #runtime_versions}

Puede especificar la versión de Go que utilizará la app estableciendo la propiedad GoVersion en el archivo Godeps/Godeps.json en la raíz de la aplicación. Por ejemplo:

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.3.3",
	"Deps": []
}
```
{: codeblock}
Para obtener más información, consulte [godep](https://github.com/tools/godep){: new_window}.

### Versiones disponibles:
{: #available_versions}

Las siguientes versiones de Go están disponibles en el
[paquete de compilación de Go](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.6.2){: new_window}
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
[paquete de compilación de Go](https://github.com/cloudfoundry/go-buildpack.git){: new_window} externo para
desplegar la aplicación.

# rellinks
## general
* [GoLang](http://golang.org/){: new_window}
* [Paquete de compilación de Cloud Foundry para Go](https://github.com/cloudfoundry/go-buildpack){: new_window}
