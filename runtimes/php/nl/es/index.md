---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}

El tiempo de ejecución de PHP en {{site.data.keyword.Bluemix}} está basado en el php_buildpack.
El php_buildpack proporciona un entorno de ejecución completo para aplicaciones PHP.
{: shortdesc}

El php_buildpack se utiliza en las condiciones siguientes:
* Su app contiene un archivo composer.json, o
* su app contiene un archivo *.php, o
* su app define una variable ${WEBDIR} en su archivo [options.json](https://github.com/cloudfoundry/php-buildpack/blob/master/docs/config.md), y dicha variable se establece en un directorio existente dentro de su app.

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una app de inicio PHP. La aplicación de inicio PHP es una sencilla app PHP que proporciona una plantilla que puede utilizar para su app. Puede experimentar con la app de inicio y realizar y transferir cambios al entorno {site.data.keyword.Bluemix}}. Consulte [Utilización de las aplicaciones de inicio](/docs/cfapps/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de inicio.

## Versiones de tiempo de ejecución
{: #runtime_versions}

Puede especificar la versión de PHP que utilizará la aplicación en el archivo composer.json. Por ejemplo:

```
{
    "require": {
        "php": "7.0.*"
    }
}
```
{: codeblock}
Para obtener más información, consulte [enlaces de Composer Package](https://getcomposer.org/doc/04-schema.md#package-links).

Cuando no se especifica la versión, se selecciona la versión 5.5.34 de forma predeterminada.

### Versiones disponibles:
{: #available_versions}

Las siguientes versiones de PHP están disponibles en el
[paquete de compilación de PHP](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.3.10)
actualmente instalado en {{site.data.keyword.Bluemix}}:

* 5.5.33
* 5.5.34
* 5.6.19
* 5.6.20
* 7.0.4
* 7.0.5

Si la app requiere una versión de PHP que no aparece en la lista,
puede utilizar el
[paquete de compilación de PHP](https://github.com/cloudfoundry/php-buildpack.git) externo para
desplegar la app.

# rellinks
{: #rellinks}
## Guías de aprendizaje y ejemplos
{: #samples}
* [Crear y desplegar una API REST](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [Crear y desplegar un contador de calorías adaptado a los dispositivos móviles](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)
## general
* [Paquete de compilación de Cloud Foundry for PHP](https://github.com/cloudfoundry/php-buildpack.git)
