{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*Letzte Aktualisierung: 12. Januar 2016*

# Go-Laufzeit
{: #go_runtime}

Die Go-Laufzeit unter {{site.data.keyword.Bluemix}} basiert auf dem Go-Buildpack (go_buildpack).
Das Go-Buildpack (go_buildpack) stellt eine vollständige Laufzeitumgebung für
Go-Apps bereit.
{: shortdesc}

Das Go-Buildpack wird verwendet, wenn Ihre Anwendung eine Datei mit der Erweiterung *.go enthält.

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix}} stellt eine Go-Starteranwendung zur Verfügung.  Die Go-Starteranwendung ist eine einfache Go-App, die eine Vorlage bereitstellt, die Sie für Ihre App nutzen können. Sie können die Starter-App ausprobieren und Änderungen vornehmen und diese dann per Push-Operation an die Bluemix-Umgebung übertragen.  Hilfeinformationen zur Verwendung der Starter-App finden Sie im Thema zur [Verwendung der Starteranwendungen](../../cfapps/starter_app_usage.html).

## Laufzeitversionen
{: #runtime_versions}

Sie können die von Ihrer App zu verwendende Go-Version angeben, indem Sie in der Datei Godeps/Godeps.json im Stammverzeichnis Ihrer Anwendung die Eigenschaft 'GoVersion' festlegen. Beispiel:

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.3.3",
	"Deps": []
}
```
{: codeblock}
Weitere Informationen finden Sie unter [godep](https://github.com/tools/godep).

### Verfügbare Versionen:
{: #available_versions}

Im derzeit in {{site.data.keyword.Bluemix}} installierten
[Go-Buildpack](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.6.2)
sind die folgenden Go-Versionen verfügbar:

* 1.2.1
* 1.2.2
* 1.3.2
* 1.3.3
* 1.4.2
* 1.4.3
* 1.5
* 1.5.1

Wenn für Ihre App eine Go-Version erforderlich ist, die nicht aufgeführt ist,
können Sie das externe
[Go-Buildpack](https://github.com/cloudfoundry/go-buildpack.git)
verwenden, um die Anwendung bereitzustellen.

## ZUGEHÖRIGE LINKS
{: #related_links}
* [GoLang](http://golang.org/)
* [Cloud Foundry-Buildpack für Go](https://github.com/cloudfoundry/go-buildpack)
