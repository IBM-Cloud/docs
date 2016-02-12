{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*Última actualización: 04 de enero de 2016*

# Tiempo de ejecución de PHP
{: #php_runtime}

El tiempo de ejecución de PHP en {{site.data.keyword.Bluemix}} está basado en php_buildpack.
php_buildpack proporciona un entorno de tiempo de ejecución completo para las apps de PHP.
{: shortdesc}

php_buildpack se utiliza en las siguientes condiciones:
* La app contiene un archivo composer.json, o
* la app contiene un archivo *.php, o
* la app define una variable ${WEBDIR} en su archivo [options.json](https://github.com/cloudfoundry/php-buildpack/blob/master/docs/config.md), y dicha variable se establece en un directorio existente dentro de la app.

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una aplicación de inicio de PHP. La aplicación de inicio de PHP es una app de PHP simple que proporciona una plantilla que puede utilizar para la app. Puede experimentar con la app de iniciador, y realizar y enviar por push cambios al entorno de {site.data.keyword.Bluemix}}. Consulte [Utilización de las aplicaciones de iniciador](../../cfapps/starter_app_usage.html) para obtener ayuda con el uso de la app de iniciador.

## Versiones de tiempo de ejecución
{: #runtime_versions}

Puede especificar la versión de PHP que utilizará la app en el archivo composer.json. Por ejemplo:

```
{
    "version": "1.5"
}
```
{: codeblock}
Para obtener más información, consulte [Paquetes de Composer
Platform](https://getcomposer.org/doc/02-libraries.md#platform-packages). 

Cuando no se especifique una versión, se elegirá la versión 5.5.30 de forma predeterminada.

### Versiones disponibles:
{: #available_versions}

Las siguientes versiones de PHP están disponibles en el
[paquete de compilación PHP](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.1.5)
instalado actualmente en {{site.data.keyword.Bluemix}}:

* 5.4.44
* 5.4.45
* 5.5.29
* 5.5.30
* 5.6.30
* 5.6.13
* 5.6.714

Si la app requiere una versión de PHP que no aparece en la lista,
puede utilizar el
[paquete de compilación PHP](https://github.com/cloudfoundry/php-buildpack.git) externo para
desplegar la app.

## GUÍAS DE APRENDIZAJE Y EJEMPLOS
{: #tutorials_and_samples}
* [Crear y desplegar una API REST](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [Crear y desplegar un contador de calorías adaptada a los dispositivos móviles ](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)

## ENLACES RELACIONADOS
{: #related_links}
* [Paquete de compilación de Cloud Foundry for PHP](https://github.com/cloudfoundry/php-buildpack.git)
