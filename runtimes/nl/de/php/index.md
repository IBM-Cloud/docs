---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}
*Letzte Aktualisierung: 16. März 2016*

Die Laufzeit von PHP in {{site.data.keyword.Bluemix}} basiert auf dem Buildpack 'php_buildpack'.
Das Buildpack 'php_buildpack' stellt eine vollständige Laufzeitumgebung für PHP-Apps zur Verfügung.
{: shortdesc}

Das Buildpack 'php_buildpack' wird unter folgenden Bedingungen verwendet:
* Ihre App enthält die Datei 'composer.json' oder
* Ihre App enthält eine '*.php'-Datei oder
* Ihre App definiert die Variable ${WEBDIR} in ihrer Datei [options.json](https://github.com/cloudfoundry/php-buildpack/blob/master/docs/config.md) und als Einstellung für diese Variable ist ein in Ihrer App vorhandenes Verzeichnis festgelegt.

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix}} stellt eine PHP-Starter-App zur Verfügung.  Die PHP-Starteranwendung ist eine einfache PHP-App, die Sie als Schablone für Ihre App verwenden können. Sie können mit der Starter-App experimentieren, Änderungen an der Bluemix-Umgebung vornehmen und diese mit einer Push-Operation übertragen.  Hilfe zur Verwendung der Starter-App finden Sie in [Starteranwendungen verwenden](../../cfapps/starter_app_usage.html).

## Laufzeitversionen
{: #runtime_versions}

Sie können die Version von PHP, die von Ihrer App verwendet werden soll, in der Datei 'composer.json' angeben. Beispiel:

```
{
    "version": "1.5"
}
```
{: codeblock}
Weitere Informationen finden Sie in [Composer Platform packages](https://getcomposer.org/doc/02-libraries.md#platform-packages).

Wenn keine Version angegeben ist, wird standardmäßig Version 5.5.30 ausgewählt.

### Verfügbare Versionen:
{: #available_versions}

Folgende PHP-Versionen stehen im [PHP-Buildpack](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.1.5) zur Verfügung, das zurzeit in {{site.data.keyword.Bluemix}} installiert ist:

* 5.4.44
* 5.4.45
* 5.5.29
* 5.5.30
* 5.6.30
* 5.6.13
* 5.6.14

Wenn für Ihre App eine PHP-Version erforderlich ist, die nicht aufgelistet ist, können Sie die App mit dem externen [PHP-Buildpack](https://github.com/cloudfoundry/php-buildpack.git) implementieren.

# Zugehörige Links
## Beispiele
* [REST-API erstellen und implementieren](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [Mobil einsetzbaren Kalorienzähler erstellen und implementieren](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)
## Allgemein
* [Cloud Foundry-Buildpack für PHP](https://github.com/cloudfoundry/php-buildpack.git)
