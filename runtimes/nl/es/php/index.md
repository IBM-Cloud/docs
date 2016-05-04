---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}
*Última actualización: 16 de marzo de 2016*

El tiempo de ejecución de PHP en {{site.data.keyword.Bluemix}} está basado en el php_buildpack.
El php_buildpack proporciona un entorno de ejecución completo para aplicaciones PHP.
{: shortdesc}

El php_buildpack se utiliza en las condiciones siguientes:
* Su app contiene un archivo composer.json, o
* su app contiene un archivo *.php, o
* su app define una variable ${WEBDIR} en su archivo [options.json](https://github.com/cloudfoundry/php-buildpack/blob/master/docs/config.md), y dicha variable se establece en un directorio existente dentro de su app.

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una aplicación de inicio PHP.  La aplicación de inicio PHP es una aplicación PHP sencilla que proporciona una plantilla que puede utilizar para la app. Puede experimentar con la aplicación de inicio, y realizar y enviar por push los cambios al entorno {site.data.keyword.Bluemix}}.  Consulte [Utilización de las aplicaciones de inicio](../../cfapps/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de inicio.

## Versiones de tiempo de ejecución
{: #runtime_versions}

Puede especificar la versión de PHP que utilizará la aplicación en el archivo composer.json. Por ejemplo:

```
{
    "version": "1.5"
}
```
{: codeblock}
Para obtener más información, consulte [Paquetes de Composer Platform](https://getcomposer.org/doc/02-libraries.md#platform-packages).

Cuando no se especifique una versión, se elegirá la versión 5.5.30 de forma predeterminada.

### Versiones disponibles:
{: #available_versions}

Las siguientes versiones de PHP están disponibles en el
[paquete de compilación de PHP](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.1.5)
actualmente instalado en {{site.data.keyword.Bluemix}}:

* 5.4.44
* 5.4.45
* 5.5.29
* 5.5.30
* 5.6.30
* 5.6.13
* 5.6.14

Si la app requiere una versión de PHP que no aparece en la lista,
puede utilizar el
[paquete de compilación de PHP](https://github.com/cloudfoundry/php-buildpack.git) externo para
desplegar la app.

# rellinks
## muestras
* [Crear y desplegar una API REST](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [Crear y desplegar un contador de calorías adaptado a los dispositivos móviles](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)
## general
* [Paquete de compilación de Cloud Foundry for PHP](https://github.com/cloudfoundry/php-buildpack.git)
