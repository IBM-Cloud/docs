{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*Última actualización: 12 de enero de 2016*

# Tiempo de ejecución de Python
{: #python_runtime}

El tiempo de ejecución de Python en {{site.data.keyword.Bluemix}} está basado en python_buildpack.
python_buildpack proporciona un entorno de tiempo de ejecución completo para las apps de Python.
{: shortdesc}

python_buildpack se utilizará si el directorio raíz de la app contiene un archivo requirements.txt o un archivo setup.py.

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una aplicación de inicio de Python. La aplicación de inicio de Python es una app Python sencilla que proporciona una plantilla que puede utilizar para la app. Puede experimentar con la app de iniciador, y realizar y enviar por push cambios en el entorno de {{site.data.keyword.Bluemix}}. Consulte [Utilización de las aplicaciones de inicio](../../cfapps/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de inicio.

## Versiones de tiempo de ejecución
{: #runtime_versions}

Puede especificar la versión de Python que utilizará la app estableciendo python-versionnumber en el archivo runtime.txt de la raíz de la aplicación. Por ejemplo:

```
python-3.4.3
```
{: codeblock}


### Versiones disponibles:
{: #available_versions}

Las siguientes versiones de Python están disponibles en el
[paquete de compilación de Python](https://github.com/cloudfoundry/python-buildpack/releases/tag/v1.5.1)
instalado actualmente en {{site.data.keyword.Bluemix}}:

* 2.7.9
* 2.7.10
* 3.3.5
* 3.3.6
* 3.4.2
* 3.4.3
* 3.5.0

Si la aplicación necesita una versión de Python que no está en la lista,
puede utilizar el
[paquete de compilación de Python](https://github.com/cloudfoundry/python-buildpack) externo para
desplegar la app.

## ENLACES RELACIONADOS
{: #related_links}
* [Paquete de compilación de Cloud Foundry for Python](https://github.com/cloudfoundry/python-buildpack)
