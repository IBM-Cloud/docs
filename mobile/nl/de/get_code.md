---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Code abrufen
{: #Get_Code}

Wenn Sie die Konfiguration und die Einrichtung Ihres mobilen Projekts mit Ihren ausgewählten Funktionen abgeschlossen haben, können Sie den Code herunterladen, mit dem Sie den Code in Xcode oder Android Studio ausführen können. Ihr heruntergeladenes Projekt ist mit den erforderlichen SDK-Abhängigkeiten und Berechtigungsnachweisen für jede von Ihnen konfigurierte Funktion vorkonfiguriert.

Für Services in Ihrem heruntergeladenen Projekt, die nicht konfigurierbar sind, müssen Sie die Berechtigungsnachweise für Services ausfüllen. Die `README.md`-Datei für das Starter-Projekt enthält entsprechende Anweisungen. Zeigen Sie die `README.md`-Datei in einem Markdown-Viewer an und vervollständigen Sie die Einrichtung.

### Vorausgesetzte Entwicklertools
{: #prereq-dev-tools}

Für die Arbeit mit generiertem Code über das {{site.data.keyword.Bluemix_notm}} Mobile-Dashboard sind folgende Entwicklertools erforderlich:

#### Android
* [Android Studio 2.2 ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.android.com/studio "Symbol für externen Link")
	* Installieren Sie die aktuelle [Android 7.0 ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.android.com/versions/nougat-7-0/ "Symbol für externen Link ")-Laufzeit.

#### iOS
* [Xcode 8.0 ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.apple.com/xcode/ "Symbol für externen Link") (empfohlen)
	* Installieren Sie die aktuelle [iOS 10 ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://www.apple.com/ios/ios-10/ "Symbol für externen Link")-Laufzeit.
* [Homebrew ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://brew.sh/ "Symbol für externen Link")
	* Befehlszeilentool zur Unterstützung der Installation anderer Tools und Laufzeiten, z. B. CocoaPods und Carthage, für Apple-Entwickler.
* [CocoaPods ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://cocoapods.org/ "Symbol für externen Link")-Abhängigkeitenmanager zum Installieren von iOS-SDK-Abhängigkeiten. Verwenden Sie die aktuelle Version:

	```
	$ sudo gem install cocoapods --pre
	```
* [Carthage ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/Carthage/Carthage "Symbol für externen Link")-Abhängigkeitenmanager zum Installieren von Watson Developer Cloud-SDKs.

	```
	$ brew install carthage
	```

#### {{site.data.keyword.Bluemix_notm}}
* NodeJS (Node- und NPM-Laufzeiten) zur Unterstützung des aktiven API Connect-Loopbacks und anderer Bluemix-Produktivitätstools.

	Zur lokalen Ausführung von API Connect-Tools verwenden Sie Node 5.x:
	```
	$ brew install Node5
	```

* [Bluemix CLI-Tools ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://clis.ng.bluemix.net/ui/home.html "Symbol für externen Link").
Befehlszeilentools für die einfache Bereitstellung von Cloud Foundry-Laufzeiten über eine Befehlszeilenschnittstelle mit Bluemix.  
