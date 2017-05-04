---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}

Die Laufzeit von PHP in {{site.data.keyword.Bluemix}} basiert auf dem Buildpack 'php_buildpack'.
Das Buildpack 'php_buildpack' stellt eine vollständige Laufzeitumgebung für PHP-Apps zur Verfügung.
{: shortdesc}

Das Buildpack 'php_buildpack' wird unter folgenden Bedingungen verwendet:
* Ihre App enthält die Datei 'composer.json' oder
* Ihre App enthält eine '*.php'-Datei oder
* Ihre App definiert die Variable ${WEBDIR} in ihrer Datei [options.json](https://docs.cloudfoundry.org/buildpacks/php/gsg-php-config.html) und als Einstellung für diese Variable ist ein in Ihrer App vorhandenes Verzeichnis festgelegt.

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix}} stellt eine PHP-Starter-App zur Verfügung.  Die PHP-Starteranwendung ist eine einfache PHP-App, die Sie als Schablone für Ihre App verwenden können. Sie können mit der Starter-App experimentieren, Änderungen an der {{site.data.keyword.Bluemix}}-Umgebung vornehmen und diese mit einer Push-Operation übertragen.  Hilfe zur Verwendung der Starter-App finden Sie in [Starteranwendungen verwenden](/docs/cfapps/starter_app_usage.html).

## Laufzeitversionen
{: #runtime_versions}

Sie können die Version von PHP, die von Ihrer App verwendet werden soll, in der Datei 'composer.json' angeben. Beispiel:

```
{
    "require": {
        "php": "7.0.*"
    }
}
```
{: codeblock}
Weitere Informationen finden Sie unter [Composer-Paktlinks ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://getcomposer.org/doc/04-schema.md#package-links).

Wenn keine Version angegeben ist, wird standardmäßig Version 5.5.34 ausgewählt.

### Verfügbare Versionen:
{: #available_versions}

Folgende PHP-Versionen stehen im [PHP-Buildpack](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.3.10) zur Verfügung, das zurzeit in {{site.data.keyword.Bluemix}} installiert ist:

* 5.5.33
* 5.5.34
* 5.6.19
* 5.6.20
* 7.0.4
* 7.0.5

Wenn für Ihre App eine PHP-Version erforderlich ist, die nicht aufgelistet ist, können Sie die App mit dem externen [PHP-Buildpack](https://github.com/cloudfoundry/php-buildpack.git) implementieren.

# Zugehörige Links
{: #rellinks notoc}
## Lernprogramme und Beispiele
{: #samples notoc}
* [REST-API erstellen und implementieren](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [Mobil einsetzbaren Kalorienzähler erstellen und implementieren](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)
## Allgemein
{: #general notoc}
* [Cloud Foundry-Buildpack für PHP](https://github.com/cloudfoundry/php-buildpack.git)
