{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Swift-Laufzeit
{: #swift_runtime}
*Letzte Aktualisierung: 19. Februar 2016*

Die Laufzeit von Swift in {{site.data.keyword.Bluemix}} basiert auf dem Buildpack 'swift_buildpack'.
Das Buildpack 'swift_buildpack' bietet eine vollständige Laufzeitumgebung für Swift-Apps.
{: shortdesc}

Das Buildpack 'swift_buildpack' wird verwendet, wenn im Stammverzeichnis Ihrer App die Datei 'Package.swift' vorhanden ist.

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix}} stellt eine Swift-Starteranwendung bereit. Die Swift-Starter-App ist eine einfache Swift-App, mit der Sie Kenntnisse erwerben können, welche Typen von Serveranwendungen Sie mithilfe der Programmiersprache Swift entwickeln können. Diese Beispiel-App erstellt einen Basisserver, der eine HTML-Begrüßung an den Client zurückgibt.  

**Hinweis:** Diese Starter-App ist keine Anwendung, die für die Produktion einsatzbereit ist.  Sie ist stattdessen für Lernzwecke bestimmt.  Sie können mit der Starter-App experimentieren, Änderungen an der {{site.data.keyword.Bluemix}}-Umgebung vornehmen und diese mit einer Push-Operation übertragen. Hilfe zur Verwendung der Starteranwendung finden Sie in [Starteranwendungen verwenden](../../cfapps/starter_app_usage.html).

## Laufzeitversionen
{: #runtime_versions}

Sie können die Version von Swift, die von Ihrer App verwendet werden soll, mithilfe der Datei '`.swift`-version' im Stammverzeichnis Ihres Repositorys angeben:

```
cat .swift-version
swift-DEVELOPMENT-SNAPSHOT-2016-02-03-a
```
{: pre}

Eine vollständige Liste der von Swift unterstützten Versionen finden Sie in der Datei [manifest.yml](https://github.com/cloudfoundry-community/swift-buildpack/blob/master/manifest.yml) des Buildpacks.

Details zur aktuellen Version des Swift-Buildpacks, das in {{site.data.keyword.Bluemix}} installiert ist, finden Sie in den [Releaseinformationen](https://github.com/cloudfoundry-community/swift-buildpack/releases/tag/v1.0.3) des Buildpacks.

Da es häufige Wechsel bei der Sprache Swift gibt, sollten Sie die Datei '.swift-version' einschließen, sodass Ihre App auf die Swift-Version 'fixiert' ist, mit der Ihre Anwendung üblicherweise arbeitet.

# Zugehörige Links
## Allgemein
* [Cloud Foundry-Buildpack für Swift](https://github.com/cloudfoundry-community/swift-buildpack)
* [Dokumentation zur Sprache Swift](https://swift.org/)
