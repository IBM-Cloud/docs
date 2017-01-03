---

copyright:
  years: 2016
lastupdated: "2016-10-13"

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
* [Android Studio 2.2](https://developer.android.com/studio)
	* Installieren Sie die aktuelle [Android 7.0](https://www.android.com/versions/nougat-7-0/)-Laufzeit.

#### iOS
* [Xcode 8.0](https://developer.apple.com/xcode/) (empfohlen)
	* Installieren Sie die aktuelle [iOS 10](http://www.apple.com/ios/ios-10/)-Laufzeit.
* [Homebrew](http://brew.sh/)
	* Befehlszeilentool zur Unterstützung der Installation anderer Tools und Laufzeiten, z. B. CocoaPods und Carthage, für Apple-Entwickler.
* [CocoaPods](https://cocoapods.org/)-Abhängigkeitenmanager für die Installation von iOS-SDK-Abhängigkeiten. Verwenden Sie die aktuelle Version:

	```
	$ sudo gem install cocoapods --pre
	```
* [Carthage](https://github.com/Carthage/Carthage)-Abhängigkeitenmanager für die Installation von Watson Developer Cloud-SDKs.

	```
	$ brew install carthage
	```

#### {{site.data.keyword.Bluemix_notm}}
* NodeJS (Node- und NPM-Laufzeiten) zur Unterstützung des aktiven API Connect-Loopbacks und anderer Bluemix-Produktivitätstools.

	Zur lokalen Ausführung von API Connect-Tools verwenden Sie Node 5.x:
	```
	$ brew install Node5
	```

* [Bluemix-CLI-Tools](http://clis.ng.bluemix.net/ui/home.html).
Befehlszeilentools für die einfache Bereitstellung von Cloud Foundry-Laufzeiten über eine Befehlszeilenschnittstelle mit Bluemix.  
