{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Swift-Laufzeit
{: #swift_runtime}
*Letzte Aktualisierung: 10. Juni 2016*
{: .last-updated}

Die Swift-Laufzeit in {{site.data.keyword.Bluemix}} basiert auf dem Swift-Buildpack für Bluemix (das heißt swift_buildpack').
Das Buildpack 'swift_buildpack' bietet eine vollständige Laufzeitumgebung für Swift-Anwendungen.
{: shortdesc}

Das Buildpack 'swift_buildpack' wird verwendet, wenn im Stammverzeichnis Ihrer App die Datei 'Package.swift' vorhanden ist.

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix}} stellt eine Swift-Starteranwendung bereit. Die Swift-Starter-App ist eine einfache Swift-App, mit der Sie Kenntnisse erwerben können, welche Typen von Serveranwendungen Sie mithilfe der Programmiersprache Swift entwickeln können. Diese Beispiel-App erstellt einen HTTP-Basisserver, der HTML-Inhalte an den Client zurückgibt.

**Hinweis:** Diese Starter-App ist keine Anwendung, die für die Produktion einsatzbereit ist.  Sie ist stattdessen für Lernzwecke bestimmt.  Sie können mit der Starter-App experimentieren, Änderungen an der {{site.data.keyword.Bluemix}}-Umgebung vornehmen und diese mit einer Push-Operation übertragen. Hilfe zur Verwendung der Starteranwendung finden Sie in [Starteranwendungen verwenden](../../cfapps/starter_app_usage.html).

## Laufzeitversionen
{: #runtime_versions}

Das in Bluemix installierte Buildpack 'swift_buildpack' unterstützt die Version `DEVELOPMENT-SNAPSHOT-2016-05-03-a` der Swift-Binärdateien. Wenn Sie in Bluemix eine andere Version von Swift für Ihre Anwendung verwenden möchten, können Sie die Version mit einer Datei `.swift-version` im Stammverzeichnis Ihres Repositorys angeben:

```
cat .swift-version
swift-DEVELOPMENT-SNAPSHOT-2016-04-25-a
```
{: pre}

Neben der Angabe einer Datei `.swift-version` müssen Sie den Parameter `-b https://github.com/IBM-Swift/swift-buildpack` dem Befehl `cf push` wie folgt hinzufügen:

```
cf push -b https://github.com/IBM-Swift/swift-buildpack
```

Eine vollständige Liste der von Swift unterstützten Versionen finden Sie in der Datei [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/bluemix-buildpack/manifest.yml) des Buildpacks.

Details zur aktuellen Version des Swift-Buildpacks, das in {{site.data.keyword.Bluemix}} installiert ist, finden Sie in den [Releaseinformationen](https://github.com/IBM-Swift/swift-buildpack/releases/tag/1.1.1) des Buildpacks.

Da es häufig Änderungen bei der Sprache Swift gibt, sollten Sie eine Datei `.swift-version` angeben, sodass Ihre App auf die Swift-Version 'fixiert' ist, mit der Ihre Anwendung üblicherweise arbeitet. Wenn Sie eine andere Version von Swift als `DEVELOPMENT-SNAPSHOT-2016-05-03-a` verwenden, sollten Sie den Parameter `-b https://github.com/IBM-Swift/swift-buildpack` angeben, wenn Sie für Ihre App eine Push-Operation durchführen (siehe oben).

# Zugehörige Links
{: #rellinks}
## Allgemein
{: #general}
* [Swift-Buildpack für Bluemix](https://github.com/IBM-Swift/swift-buildpack)
* [Dokumentation zur Sprache Swift](https://swift.org/)
