---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Python
{: #python_runtime}

El tiempo de ejecución de Python en {{site.data.keyword.Bluemix}} está basado en el python_buildpack.
El python_buildpack proporciona un entorno de ejecución completo para aplicaciones Python 2 y Python 3.
{: shortdesc}

El python_buildpack se utilizará si el directorio raíz de la aplicación contiene un archivo requirements.txt o un archivo setup.py.

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una aplicación de inicio Python.  La aplicación de inicio Python es una sencilla app Python que ofrece una plantilla que puede utilizar para su app. Puede experimentar con la app de inicio, y realizar y enviar los cambios al entorno de {{site.data.keyword.Bluemix}}. Consulte [Utilización de las aplicaciones de inicio](/docs/cfapps/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de inicio.

## Versiones de tiempo de ejecución
{: #runtime_versions}

Puede especificar la versión de Python que va a utilizar la app estableciendo python-versionnumber en el archivo runtime.txt en la raíz de la aplicación. Por ejemplo:

```
python-3.5.0
```
{: codeblock}

Cuando no se especifique una versión, se elegirá la versión 2.7.11 de forma predeterminada.

### Versiones disponibles:
{: #available_versions}

Las siguientes versiones de Python están disponibles en el
[paquete de compilación de Python](https://github.com/cloudfoundry/python-buildpack/releases/tag/v1.5.5)
actualmente instalado en {{site.data.keyword.Bluemix}}:

* 2.7.10
* 2.7.11
* 3.3.5
* 3.3.6
* 3.4.3
* 3.4.4
* 3.5.0
* 3.5.1

Si la aplicación requiere una versión de Python que no aparece en la lista,
puede utilizar el
[paquete de compilación de Python](https://github.com/cloudfoundry/python-buildpack) externo para
desplegar la app.

# rellinks
## general
* [Paquete de compilación de Cloud Foundry for Python](https://github.com/cloudfoundry/python-buildpack)
