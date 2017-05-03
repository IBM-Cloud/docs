---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# IBM Bluemix Runtime für Swift
{: #swift_runtime}

Die Swift-Laufzeit auf {{site.data.keyword.Bluemix}} wird durch das [IBM Bluemix-Buildpack für Swift](https://github.com/IBM-Swift/swift-buildpack) (i.e. swift_buildpack) angetrieben.
Dieses Buildpack bietet eine vollständige Laufzeitumgebung für Swift-Anwendungen.
{: shortdesc}

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix}} stellt eine Kitura-basierte Swift-[Starteranwendung](https://github.com/IBM-Bluemix/Kitura-Starter) bereit. Die Kitura-Starter-App ist eine einfache Swift-App, mit der Sie erfahren können, welche Typen von Serveranwendungen Sie mithilfe der Programmiersprache Swift entwickeln können. Diese Beispielapp erstellt einen Kitura HTTP-Basisserver, der HTML-Inhalte an den Client zurückgibt.

**Hinweis:** Die Kitura-Starter-App ist für Lernzwecke bestimmt. Sie können mit der Starter-App experimentieren, indem Sie Erweiterungen hinzufügen und diese Änderungen mit einer Push-Operation an die {{site.data.keyword.Bluemix}}-Umgebung übertragen. Hilfe zur Verwendung der Starteranwendung finden Sie in [Starteranwendungen verwenden](../../cfapps/starter_app_usage.html).

## Ihre App umbenennen
{: #renaming_your_app}

Wenn Sie Ihre App umbenennen möchten (entweder vom Kitura-Starter oder allgemeiner), gibt es einige Änderungen, die berücksichtigt werden müssen. Dadurch werden sowohl Unklarheiten vermieden als auch eine fehlerfreie Bereitstellung sichergestellt.

- Benennen Sie den Projektordner der App um, damit er mit dem Namen Ihrer App übereinstimmt. 
- `Package.swift` - Ändern Sie die folgenden Einträge:
    - `name` - Sollte mit dem Namen der App übereinstimmen. 
    - `targets[Target(name:)]` - Sollte mit dem Namen der App übereinstimmen. 
- `manifest.yml` - Ändern Sie die folgenden Einträge: 
    - `name` - Sollte mit dem Namen der App übereinstimmen. 
    - `command` - Der Name der ausführbaren Datei, die Ihre App startet (sollte mit dem Namen übereinstimmen, der in der Datei 'Package.swift' angegeben ist).

## Laufzeitversionen
{: #runtime_versions}

Standardmäßig verwendet die Laufzeit für Swift (swift_buildpack), die auf {{site.data.keyword.Bluemix}} gehostet ist, die aktuellste GA-Version der Swift-Binärdateien. Dies ist die einzige Version von Swift, die direkt von IBM unterstützt wird, und es wird empfohlen, diese Version in Ihrer App zu verwenden. Sie können diese unterstützte Version bestimmen, indem Sie die [aktuellsten Releaseinformationen](https://github.com/IBM-Swift/swift-buildpack/releases) von swift_buildpack lesen. Das Buildpack kann andere Swiftversionen auflisten, wie dies in der zugehörigen Datei [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml) dargestellt ist. Diese allgemeinen aber nicht unterstützten Versionen von Swift sind bereits innerhalb des Buildpacks vorab zwischengespeichert, wodurch sich die Bereitstellungszeit verkürzt. 

Wenn Sie für Ihre Anwendung eine andere Version von Swift in {{site.data.keyword.Bluemix}} verwenden möchten, können Sie die Version mithilfe einer `.swift-version`-Datei im Stammverzeichnis Ihres Repositorys angeben. Diese `.swift-version`-Datei definiert, welche Swift-Version vom swift_buildpack verwendet werden soll.

```
$ cat .swift-version
3.0
```
{: pre}

Da es häufig Aktualisierungen an der Sprache Swift gibt, sollten Sie stets eine `.swift-version`-Datei einbeziehen, damit Ihre App auf die Swift-Version 'fixiert' ist, mit der Ihre Anwendung üblicherweise arbeitet.

Bitte beachten Sie, dass Sie jede gültige Version von Swift in Ihrer `.swift-version`-Datei angeben können. Dise alternativen Versionen müssen mit der Benennung von [Swift.org ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://swift.org/download/) übereinstimmen und werden direkt von dort extrahiert. Bei der Verwendung einer Nicht-Cache-Version dauert die Bereitstellung ein wenig länger. Es gibt jedoch keinen Unterschied bei der Laufzeitleistung Ihrer Swift-App.

Das Standardversion von swift_buildpack in {{site.data.keyword.Bluemix}} wird verwendet, wenn das Stammverzeichnis Ihrer App die Datei `Package.swift` enthält.  Falls Sie ein alternatives Buildpack verwenden möchten, müssen Sie dieses durch Hinzufügen eines Eintrags `buildpack: {buildpackUrl}` zu der Datei 'manifest.yml' Ihrer App angeben. Alternativ können Sie dies zum Zeitpunkt der Bereitstellung definieren, indem Sie das Befehlsargument `cf push -b {buildpackUrl}` verwenden.


## Entwicklerumgebungen

Entwickler haben verschiedene Optionen bei der Erstellung von serverseitigen Anwendungen mit Swift. Diejenigen, die Geräte mit MacOS von Apple verwenden, bevorzugen wahrscheinlich die Verwendung der Xcode-IDE, obwohl dies keine Voraussetzung ist.  Swift-basierte Apps, die unter {{site.data.keyword.Bluemix}} bereitgestellt und ausgeführt werden, können jeden Programmierungseditor und jede IDE verwenden.  Syntaxhervorhebung und Linten stehen für Swift für zahlreiche gängige Editoren zur Verfügung. Das Befehlszeilentool Swift REPL, das in den Binärdateien von [Swift.org ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://swift.org/) enhalten ist, ermöglicht vor der Bereitstellung von {{site.data.keyword.Bluemix}} die lokale Kompilierung und lokale Tests.

Benutzer von MaxOS können die [IBM Cloud Tools für Swift](http://cloudtools.bluemix.net/) verwenden, die die Erstellung, Bereitstellung, Verwaltung und Steuerung von serverseitigen Swift-Apps vereinfachen, die unter {{site.data.keyword.Bluemix}} ausgeführt werden.  


## Erweiterte Integration

Die Arbeit mit dem [Kitura-Web-Framework](http://ibm-swift.github.io/Kitura/) bietet eine ganze Reihe von Möglichkeiten. Kitura ist modular aufgebaut und Sie werden sehr bald seine Funktionalität mit gepackten SDKs erweitern wollen, um Features wie Authentifizierung, Zugriff auf Watson-basierte Services und eine breite Palette von Datenbanken zur Verfügung zu haben.  Kitura bietet direkte Unterstützung für zahlreiche Datenbanken, während andere Open-Source-Projekte auch SDKs für viele Datenbankplattformen zur Verfügung stellen. Im Folgenden finden Sie eine nicht vollständige Liste der durch Kitura zur Verfügung gestellten SDKs für die Arbeit mit externen Ressourcen. 

- [IBM Watson](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/swift-watson-sdk)
- [IBM DB2 und DashDB](https://swiftpkgs.ng.bluemix.net/package/IBM-DTeam/swift-for-db2)
- [IBM Cloudant und CouchDB](https://swiftpkgs.ng.bluemix.net/package/cloudant/swift-cloudant)
- [IBM ObjectStorage](https://swiftpkgs.ng.bluemix.net/package/ibm-bluemix-mobile-services/bluemix-objectstorage-serversdk-swift)
- [Apache Cassandra](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Kassandra)
- [Aphid MQTT](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Aphid)

Weitere Swift-Pakete, die Sie in Ihre Anwendung integrieren können, finden Sie im [IBM Swift-Paketkatalog](https://swiftpkgs.ng.bluemix.net/). Führen Sie eine Suche für Ihren Zielservice oder Ihre Datenbank aus. Der Paketkatalog bietet eine einfache Möglichkeit, Pakete zu finden, die Sie in Ihre Swift-Anwendung einbeziehen können. Pakete können zu einer Swift-Anwendung hinzugefügt werden, indem die Git-URL des Pakets und Versionsdetails in die Datei `Package.swift` der App einbezogen werden. Weitere Details zum Paketmanagement finden Sie im [Abschnitt zum Paketmanager (Package Manager) von Swift.org](https://swift.org/package-manager/).


## Zugehörige Informationen

Es gibt auch andere Online-Tools, die von IBM für Swift-Entwickler zur Verfügung gestellt werden.
- [IBM Swift DevCenter](https://developer.ibm.com/swift/) - Die Hauptseite für alle Informationen zu IBM Swift. Sie können Informationen zu unseren Produktangeboten, Blogs, soziale Ereignisse, Dokumentation und Vieles mehr finden.
- [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/) - Diese Site bietet Ihnen eine Umgebung für schnelle und einfache Tests von Swift-Codefragmenten mit verschiedenen Versionen von Swift sowie sogar auf unterschiedlichen Swift-Laufzeitplattformen. Sie können Codebeispiele auch speichern und mit anderen teilen sowie gängige Beispiele, die von anderen bereitgestellt werden, untersuchen.


# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}
* [IBM Swift DevCenter](https://developer.ibm.com/swift/)
* [IBM Cloud Tools für Swift](http://cloudtools.bluemix.net/)
* [IBM Swift-Paketkatalog](https://swiftpkgs.ng.bluemix.net/)
* [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/)
* [Kitura-Dokumentation und APIs](http://ibm-swift.github.io/Kitura/)
* [Kitura-Starter-App für Bluemix](https://github.com/IBM-Bluemix/Kitura-Starter)
* [IBM Bluemix-Buildpack für Swift](https://github.com/IBM-Swift/swift-buildpack)
* [Releaseinformationen für IBM Bluemix-Buildpack für Swift](https://github.com/IBM-Swift/swift-buildpack/releases)
* [Swift.org ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://swift.org/)
* [Dokumentation zur Sprache Swift ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://swift.org/documentation)
