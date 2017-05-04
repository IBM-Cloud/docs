---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-25"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Python
{: #python_runtime}

Die Laufzeit von Python in {{site.data.keyword.Bluemix}} basiert auf dem Buildpack 'python_buildpack'.
Das Buildpack 'python_buildpack' bietet eine vollständige Laufzeitumgebung für die Python-Apps 2 und 3.
{: shortdesc}

Das Buildpack 'python_buildpack' wird verwendet, wenn das Stammverzeichnis Ihrer App die Datei 'requirements.txt' oder die Datei 'setup.py' enthält.

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix}} stellt eine Python-Starteranwendung bereit.  Die Python-Starteranwendung ist eine einfache Python-App, die Sie als Schablone für Ihre App verwenden können. Sie können mit der Starter-App experimentieren, Änderungen an der {{site.data.keyword.Bluemix}}-Umgebung vornehmen und diese mit einer Push-Operation übertragen.  Hilfe zur Verwendung der Starteranwendung finden Sie in [Starteranwendungen verwenden](/docs/cfapps/starter_app_usage.html).

## Laufzeitversionen
{: #runtime_versions}

Sie können die Version von Python, die von Ihrer App verwendet werden soll, durch Festlegen von 'python-versionnumber' in der Datei 'runtime.txt' im Stammverzeichnis Ihrer Anwendung angeben. Beispiel:

```
python-3.5.0
```
{: codeblock}

Wenn keine Version angegeben ist, wird standardmäßig Version 2.7.11 ausgewählt.

### Verfügbare Versionen:
{: #available_versions}

Folgende Python-Versionen stehen im [Python-Buildpack](https://github.com/cloudfoundry/python-buildpack/releases/tag/v1.5.5) zur Verfügung, das zurzeit in {{site.data.keyword.Bluemix}} installiert ist:

* 2.7.10
* 2.7.11
* 3.3.5
* 3.3.6
* 3.4.3
* 3.4.4
* 3.5.0
* 3.5.1

Wenn für Ihre Anwendung eine Python-Version erforderlich ist, die nicht aufgelistet ist, können Sie die App mit dem externen [Python-Buildpack](https://github.com/cloudfoundry/python-buildpack) implementieren.

# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}
* [Cloud Foundry-Buildpack für Python](https://github.com/cloudfoundry/python-buildpack)
