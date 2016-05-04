---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Python
{: #python_runtime}
*Última actualización: 16 de marzo de 2016*

El tiempo de ejecución de Python en {{site.data.keyword.Bluemix}} está basado en el python_buildpack.
El python_buildpack proporciona un entorno de ejecución completo para aplicaciones Python.
{: shortdesc}

El python_buildpack se utilizará si el directorio raíz de la aplicación contiene un archivo requirements.txt o un archivo setup.py.

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una aplicación de inicio Python.  La aplicación de inicio Python es una app Python sencilla que proporciona una plantilla que puede utilizar para la app. Puede experimentar con la app de inicio, y realizar y enviar por push los cambios al entorno de {{site.data.keyword.Bluemix}}.  Consulte [Utilización de las aplicaciones de inicio](../../cfapps/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de inicio.

## Versiones de tiempo de ejecución
{: #runtime_versions}

Puede especificar la versión de Python que va a utilizar la app estableciendo python-versionnumber en el archivo runtime.txt en la raíz de la aplicación. Por ejemplo:

```
python-3.4.3
```
{: codeblock}

Cuando no se especifique una versión, se elegirá la versión 2.7.10 de forma predeterminada.

### Versiones disponibles:
{: #available_versions}

Las siguientes versiones de Python están disponibles en el
[paquete de compilación de Python](https://github.com/cloudfoundry/python-buildpack/releases/tag/v1.5.1)
actualmente instalado en {{site.data.keyword.Bluemix}}:

* 2.7.9
* 2.7.10
* 3.3.5
* 3.3.6
* 3.4.2
* 3.4.3
* 3.5.0

Si la aplicación requiere una versión de Python que no aparece en la lista,
puede utilizar el
[paquete de compilación de Python](https://github.com/cloudfoundry/python-buildpack) externo para
desplegar la app.

# rellinks
## general
* [Paquete de compilación de Cloud Foundry for Python](https://github.com/cloudfoundry/python-buildpack)
