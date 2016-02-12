{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*Letzte Aktualisierung: 12. Januar 2016*

# Python-Laufzeit
{: #python_runtime}

Die Python-Laufzeit unter {{site.data.keyword.Bluemix}} basiert auf dem Python-Buildpack (python_buildpack).
Das Python-Buildpack (python_buildpack) stellt eine vollständige Laufzeitumgebung für
Python-Apps bereit.
{: shortdesc}

Das Python-Buildpack wird verwendet, wenn das Stammverzeichnis Ihrer App eine Datei mit der Bezeichnung requirements.txt oder eine Datei mit der Bezeichnung setup.py enthält.

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix}} stellt eine Python-Starteranwendung zur Verfügung.  Die Python-Starteranwendung ist eine einfache Python-App, die eine Vorlage bereitstellt, die Sie für Ihre App nutzen können. Sie können die Starter-App ausprobieren und Änderungen vornehmen und diese dann per Push-Operation an die {{site.data.keyword.Bluemix}}-Umgebung übertragen.  Hilfeinformationen zur Verwendung der Starteranwendung finden Sie im Thema zur [Verwendung der Starteranwendungen](../../cfapps/starter_app_usage.html).

## Laufzeitversionen
{: #runtime_versions}

Sie können die von Ihrer App zu verwendende Python-Version angeben; legen Sie hierfür die Python-Versionsnummer in der Datei runtime.txt im Stammverzeichnis Ihrer Anwendung fest. Beispiel:

```
python-3.4.3
```
{: codeblock}


### Verfügbare Versionen:
{: #available_versions}

Im derzeit in {{site.data.keyword.Bluemix}} installierten
[Python-Buildpack](https://github.com/cloudfoundry/python-buildpack/releases/tag/v1.5.1)
sind die folgenden Python-Versionen verfügbar:

* 2.7.9
* 2.7.10
* 3.3.5
* 3.3.6
* 3.4.2
* 3.4.3
* 3.5.0

Wenn für Ihre Anwendung eine Python-Version erforderlich ist, die nicht
aufgeführt ist, können Sie das externe
[Python-Buildpack](https://github.com/cloudfoundry/python-buildpack)
verwenden, um die App bereitzustellen.

## ZUGEHÖRIGE LINKS
{: #related_links}
* [Cloud Foundry-Buildpack für Python](https://github.com/cloudfoundry/python-buildpack)
