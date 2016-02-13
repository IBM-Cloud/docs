{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*Letzte Aktualisierung: 04. Januar 2016*

# PHP-Laufzeit
{: #php_runtime}

Die PHP-Laufzeit unter {{site.data.keyword.Bluemix}} basiert auf dem PHP-Buildpack (php_buildpack).
Das PHP-Buildpack (php_buildpack) stellt eine vollständige Laufzeitumgebung für
PHP-Apps bereit.
{: shortdesc}

Das PHP-Buildpack wird verwendet, wenn die folgenden Bedingungen gelten:
* Ihre App enthält eine Datei mit der Bezeichnung composer.json oder
* Ihre App enthält eine Datei mit der Erweiterung *.php oder
* Ihre App definiert eine Variable des Typs $ {WEBDIR} in ihrer Datei [options.json](https://github.com/cloudfoundry/php-buildpack/blob/master/docs/config.md) und diese Variable wird auf ein in Ihrer App vorhandenes Verzeichnis festgelegt.

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix}} stellt eine PHP-Starter-App zur Verfügung.  Die PHP-Starteranwendung ist eine einfache PHP-App, die eine Vorlage bereitstellt, die Sie für Ihre App nutzen können. Sie können die Starter-App ausprobieren und Änderungen vornehmen und diese dann per Push-Operation an die {site.data.keyword.Bluemix}}-Umgebung
übertragen.  Hilfeinformationen zur Verwendung der Starter-App finden Sie im Thema zur [Verwendung der Starteranwendungen](../../cfapps/starter_app_usage.html).

## Laufzeitversionen
{: #runtime_versions}

Sie können die von Ihrer App zu verwendende PHP-Version in der Datei composer.json angeben. Beispiel:

```
{
    "version": "1.5"
}
```
{: codeblock}
Weitere Informationen hierzu finden Sie unter [Composer Platform packages](https://getcomposer.org/doc/02-libraries.md#platform-packages).

Wenn keine Version angegeben ist, wird standardmäßig Version 5.5.30 ausgewählt.

### Verfügbare Versionen:
{: #available_versions}

Im derzeit in {{site.data.keyword.Bluemix}} installierten
[PHP-Buildpack](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.1.5)
sind die folgenden PHP-Versionen verfügbar:

* 5.4.44
* 5.4.45
* 5.5.29
* 5.5.30
* 5.6.30
* 5.6.13
* 5.6.714

Wenn für Ihre App eine PHP-Version erforderlich ist, die nicht aufgeführt ist, können Sie das externe
[PHP-Buildpack](https://github.com/cloudfoundry/php-buildpack.git)
verwenden, um die App bereitzustellen.

## LERNPROGRAMME UND BEISPIELE
{: #tutorials_and_samples}
* [REST-API erstellen und bereitstellen](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [Für Mobilgeräte geeigneten Kalorienzähler erstellen und bereitstellen](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)

## ZUGEHÖRIGE LINKS
{: #related_links}
* [Cloud Foundry-Buildpack für PHP](https://github.com/cloudfoundry/php-buildpack.git)
