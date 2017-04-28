---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Code abrufen
{: #Get_Code}

Wenn Sie die Konfiguration und die Einrichtung Ihres Projekts mit Ihren ausgewählten Funktionen abgeschlossen haben, können Sie den Code herunterladen, mit dem Sie die Anwendung ausführen können. Ihr heruntergeladenes Projekt ist mit den erforderlichen SDK-Abhängigkeiten und Berechtigungsnachweisen für jede von Ihnen konfigurierte Funktion vorkonfiguriert.

Für Services in Ihrem heruntergeladenen Projekt, die nicht konfigurierbar sind, müssen Sie die Berechtigungsnachweise für Services ausfüllen. Die `README.md`-Datei für das Starter-Projekt enthält entsprechende Anweisungen. Zeigen Sie die `README.md`-Datei in einem Markdown-Viewer an und vervollständigen Sie die Einrichtung.

## Vorausgesetzte Entwicklertools
{: #prereq-dev-tools}

Für die Arbeit mit generiertem Code über die {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} sind folgende Entwicklertools erforderlich:


### Allgemein
{: #general notoc}

* [Homebrew ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://brew.sh/)
	* Befehlszeilentool zur Unterstützung der Installation anderer Tools und Laufzeiten, z. B. CocoaPods und Carthage, für Apple-Entwickler.

* [Docker ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.docker.com/get-docker)
	* Open-Source-Projekt zur Unterstützung bei der Ausführung und beim Debugging von Anwendungen in Containern. Nur für nicht mobile Projekte erforderlich.

### {{site.data.keyword.Bluemix_notm}}
{: #bluemix notoc}

* Node.js (Node- und NPM-Laufzeiten) zur Unterstützung des aktiven {{site.data.keyword.apiconnect_short}}-Loopback und anderer {{site.data.keyword.Bluemix_notm}}-Produktivitätstools.

	Zur lokalen Ausführung von {{site.data.keyword.apiconnect_short}}-Tools verwenden Sie Node 5.x:
	
	```
	$ brew install Node5
	```

* [Bluemix CLI-Tools ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://clis.ng.bluemix.net/ui/home.html)

   Befehlszeilentools für die Bereitstellung von Cloud Foundry-Laufzeiten über eine Befehlszeilenschnittstelle mit {{site.data.keyword.Bluemix_notm}}.  

* [{{site.data.keyword.dev_cli_notm}} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](dev_cli.html)

	{{site.data.keyword.Bluemix_notm}} CLI-Plug-in zum Erstellen, Ausführen, Testen und Bereitstellen von Webprojekten und mobilen Projekten.
	
* [SDK Generator-Plug-in ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](sdk_cli.html)

	{{site.data.keyword.Bluemix_notm}} CLI-Plug-in zum Generieren von SDKs aus der REST-API-Definition, die mit der [Open API-Spezifikation ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.openapis.org/) kompatibel ist.

### Android
{: #android notoc}

* [Android Studio 2.2 oder aktueller![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.android.com/studio)
	* Installieren Sie die aktuelle [Android 7.0 ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.android.com/versions/nougat-7-0/)-Laufzeit.

### iOS
{: #ios notoc}

* [Xcode 8 ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.apple.com/xcode/) (empfohlen)

<!-- * Install the latest [iOS 10 ![External link icon](../icons/launch-glyph.svg "External link icon")](http://www.apple.com/ios/ios-10/) runtime.
-->
* [CocoaPods ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://cocoapods.org/)-Abhängigkeitsmanager zum Installieren von iOS-SDK-Abhängigkeiten. Verwenden Sie die aktuelle Version:

	```
	$ sudo gem install cocoapods --pre
	```
* [Carthage ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/Carthage/Carthage)-Abhängigkeitsmanager zum Installieren der {{site.data.keyword.watson}} Developer Cloud-SDKs.

	```
	$ brew install carthage
	```
