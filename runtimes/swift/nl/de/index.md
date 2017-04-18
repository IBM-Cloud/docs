{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# IBM Bluemix Runtime for Swift
{: #swift_runtime}
Letzte Aktualisierung: 19. September 2016
{: .last-updated}

Die Swift Runtime unter {{site.data.keyword.Bluemix}} wird vom [IBM Bluemix-Buildpack für Swift](https://github.com/IBM-Swift/swift-buildpack) (d. h. swift_buildpack) bereitgestellt. Dieses Buildpack stellt eine vollständige Laufzeitumgebung für Swift-Anwendungen bereit.
{: shortdesc}

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix}} stellt eine Kitura-basierte Swift-[Starteranwendung](https://github.com/IBM-Swift/Kitura-Starter-Bluemix) bereit. Bei der Kitura-Starter-App handelt es sich um eine einfache Swift-App, mit deren Hilfe Sie sich über die Typen von Serveranwendungen informieren können, die Sie mit der Programmiersprache Swift entwickeln können. Durch diese Beispiel-App wird ein Kitura-HTTP-Basisserver erstellt, der HTML-Inhalt an den Client zurückgibt.

**Anmerkung:** Die Kitura-Starter-App dient nur zu Lernzwecken. Sie können die Starter-App ausprobieren und funktionale Erweiterungen vornehmen und diese Änderungen per Push-Operation an die {{site.data.keyword.Bluemix}}-Umgebung übertragen. Hilfe zur Verwendung der Starteranwendung finden Sie im Abschnitt zur [Verwendung der Starteranwendungen](../../cfapps/starter_app_usage.html).

## App umbenennen
{: #renaming_your_app}

Wenn Sie Ihre App umbenennen möchten, sei es über den Kitura-Starter oder eher allgemein, müssen ein paar Änderungen durchgeführt werden. Dadurch werden Unklarheiten vermieden und es wird eine fehlerfreie Bereitstellung sichergestellt.

- Benennen Sie den Projektordner der App um, damit er dem Namen Ihrer App entspricht.
- `Package.swift` - Ändern Sie die folgenden Einträge:
    - `name` - Muss mit dem Namen der App übereinstimmen
    - `targets[Target(name:)]` - Muss mit dem Namen der App übereinstimmen
- `manifest.yml` - Ändern Sie die folgenden Einträge:
    - `name` - Muss mit dem Namen der App übereinstimmen
    - `host` - Stellt das Segment für den primären Host der App-URL dar
- `Procfile` - Der Wert für `web` muss mit dem Verzeichnisnamen der App übereinstimmen. Dies ist der Befehl, der nach der Kompilierung zum Starten der Web-App ausgeführt wird.


## Laufzeitversionen
{: #runtime_versions}

Standardmäßig verwendet die unter {{site.data.keyword.Bluemix}} gehostete Swift Runtime (swift_buildpack) die neueste GA-Version der Swift-Binärdateien. Dies ist die einzige Version von Swift, die direkt von IBM unterstützt wird; zudem ist sie die für Ihre App empfohlene Version. Sie können diese unterstützte Version ermitteln, indem Sie die [aktuellen Releaseinformationen](https://github.com/IBM-Swift/swift-buildpack/releases) des Swift-Buildpacks (swift_buildpack) lesen. Im Buildpack werden möglicherweise andere Swift-Versionen aufgeführt wie in der Datei [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml). Diese allgemeinen, jedoch nicht unterstützten Versionen von Swift werden in dem Buildpack vorab in den Cache gestellt; dies führt zu einer reduzierten Bereitstellungszeit.

Wenn Sie für Ihre Anwendung eine andere Version von Swift unter {{site.data.keyword.Bluemix}} verwenden möchten, können Sie die Version mit einer Datei des Typs `.swift-version` im Stammverzeichnis Ihres Repositorys angeben. Diese Datei des Typs `.swift-version` definiert, welche Swift-Version vom Swift-Buildpack (swift_buildpack) verwendet werden soll.

```
$ cat .swift-version
3.0
```
{: pre}

Da es häufig Aktualisierungen zur Swift-Sprache gibt, müssen Sie immer eine Datei des Typs `.swift-version` aufnehmen, damit Ihre App an die Swift-Version "geheftet" ist, von der Ihre Anwendung weiß, dass sie sie nutzen soll.

Beachten Sie, dass Sie jede beliebige gültige Version von Swift in Ihrer Datei des Typs `.swift-version` angeben können. Diese alternativen Versionen müssen mit der Benennungskonvention von [Swift.org](https://swift.org/download/) übereinstimmen und werden direkt dort abgerufen. Im Gegensatz zur Nicht-Cache-Version, bei der die Bereitstellung etwas länger dauert, gibt es für die Swift-App keine Unterschiede in der Laufzeitleistung.

Das Standard-Swift-Buildpack (swift_buildpack) in {{site.data.keyword.Bluemix}} wird verwendet, wenn Ihr App-Stammverzeichnis eine Datei des Typs `Package.swift` enthält.  Wenn Sie ein alternatives Buildpack verwenden möchten, müssen Sie dies durch Hinzufügen des Eintrags `buildpack: {buildpackUrl}` zur Datei manifest.yml Ihrer App angeben. Alternativ dazu können Sie dies zur Zeit der Bereitstellung mit dem Befehlsargument `cf push -b {buildpackUrl}` definieren.


## Entwicklerumgebungen

Entwickler haben mehrere Möglichkeiten für die Erstellung serverseitiger Anwendungen mit Swift. Diejenigen, die ein MacOS-Gerät von Apple verwenden, bevorzugen möglicherweise die Xcode-IDE, auch wenn dies keine Voraussetzung ist.  Für Swift-basierte Apps, die unter {{site.data.keyword.Bluemix}} bereitgestellt und ausgeführt werden, kann ein beliebiger Programmierungseditor oder eine beliebige IDE verwendet werden.  Die Syntaxhervorhebung und das Linting für Swift sind für viele gängige Editoren verfügbar. Das Swift-REPL-Befehlszeilentool, das in den Binärdateien aus [Swift.org](https://swift.org/) enthalten ist, ermöglicht eine lokale Kompilierung und Testdurchläufe vor der Bereitstellung in {{site.data.keyword.Bluemix}}.

Für MaxOS-Benutzer können Sie [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/) nutzen, wodurch Erstellung, Bereitstellung, Management und Steuerung serverseitiger Swift-Apps, die unter {{site.data.keyword.Bluemix}} ausgeführt werden, vereinfacht werden.  


## Erweiterte Integration

Das Arbeiten mit dem [Kitura-Web-Framework](http://ibm-swift.github.io/Kitura/) birgt eine Vielzahl von Funktionen. Kitura ist eine modulare Komponente, deren Funktionalität Sie bald mit den Paket-SDKs erweitern möchten; so können Features wie Authentifizierung, Zugriff auf Watson-basierte Services und eine große Vielzahl von Datenbanken bereitgestellt werden.  Kitura bietet für viele Datenbanken direkte Unterstützung, andere Open-Source-Projekte hingegen bieten außerdem SDKs für eine Vielzahl von Datenbankplattformen. Im Folgenden sehen Sie eine unvollständige Liste der von Kitura bereitgestellten SDKs für das Arbeiten mit externen Ressourcen.

- [IBM Watson](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/swift-watson-sdk)
- [IBM DB2 und DashDB](https://swiftpkgs.ng.bluemix.net/package/IBM-DTeam/swift-for-db2)
- [IBM Cloudant und Couchbase](https://swiftpkgs.ng.bluemix.net/package/cloudant/swift-cloudant)
- [IBM ObjectStorage](https://swiftpkgs.ng.bluemix.net/package/ibm-bluemix-mobile-services/bluemix-objectstorage-serversdk-swift)
- [Apache Cassandra](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Kassandra)
- [Aphid MQTT](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Aphid)

Im [IBM Swift-Paketkatalog](https://swiftpkgs.ng.bluemix.net/) finden Sie weitere Swift-Pakete für Ihre Anwendung; führen Sie dort eine Suche für Ihren Zielservice oder Ihre Datenbank durch. Im Paketkatalog ist eine einfache Suche nach Paketen möglich, die Sie in Ihre Swift-Anwendungen einbinden können. Pakete können zu einer Swift-Anwendung hinzugefügt werden, indem die Git-URL und die Versionsdetails des Pakets in die Datei `Package.swift` der App aufgenommen werden. Weitere Details zum Paketmanagement finden Sie im [Abschnitt zum Paketmanager in Swift.org](https://swift.org/package-manager/).


## Zugehörige Informationen

Für Swift-Entwickler sind noch weitere IBM Online-Tools verfügbar.
- [IBM Swift DevCenter](https://developer.ibm.com/swift/) - Haupt-Landing-Site für alle IBM Swift-Informationen. Dort finden Sie Informationen zu unseren Angeboten, Blogs, Social Events, Dokumentation usw..
- [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/) - Auf dieser Site finden Sie eine Umgebung, in der Sie schnell und unkompliziert Swift-Codefragmente mit unterschiedlichen Versionen von Swift und selbst auf unterschiedlichen Swift-Laufzeitplattformen ausprobieren können. Sie können Codebeispiele auch speichern und mit anderen Benutzern gemeinsam nutzen oder gängige Beispiele testen, die von anderen Benutzern bereitgestellt werden.


# Zugehörige Links
{: #rellinks}
## Allgemein
{: #general}
* [IBM Swift DevCenter](https://developer.ibm.com/swift/)
* [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)
* [IBM Swift-Paketkatalog](https://swiftpkgs.ng.bluemix.net/)
* [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/)
* [Kitura-Dokumentation und APIs](http://ibm-swift.github.io/Kitura/)
* [Kitura-Starter-App für Bluemix](https://github.com/IBM-Swift/Kitura-Starter-Bluemix)
* [IBM Bluemix-Buildpack für Swift](https://github.com/IBM-Swift/swift-buildpack)
* [IBM Bluemix-Buildpack für Swift - Releaseinformationen](https://github.com/IBM-Swift/swift-buildpack/releases)
* [Swift.org](https://swift.org/)
* [Dokumentation zur Swift-Sprache](https://swift.org/documentation)
