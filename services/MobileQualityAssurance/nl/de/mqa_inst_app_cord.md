---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# MQA mit einer Cordova-App instrumentieren (veraltet)
{: #instrumentcord}

Zur Verwendung von {{site.data.keyword.mqafull}} mit Ihrer Cordova-App müssen Sie das SDK herunterladen und es instrumentieren, indem Sie mithilfe der Befehlszeilenschnittstelle einige Änderungen vornehmen.
{: shortdesc}

Bevor Sie eine App instrumentieren mit {{site.data.keyword.mqa}} instrumentieren können, müssen Sie über ein {{site.data.keyword.Bluemix}}-Konto und die ordnungsgemäß installierte Version der Entwicklungsumgebung für die Plattformen der App verfügen, die Sie instrumentieren.

Führen Sie die folgenden Tasks aus, um {{site.data.keyword.mqa}} für die Arbeit mit Ihrer Cordova-App zu instrumentieren:

1. Fügen Sie die erforderlichen Berechtigungen und das heruntergeladene SDK zu Ihrem Cordova-Projekt hinzu.

	1. Öffnen Sie eine Eingabeaufforderung und navigieren Sie zu dem Verzeichnis mit Ihren Projektdateien.

	2. Fügen Sie das {{site.data.keyword.mqa}}-Plug-in zu Ihrem Cordova-Projekt hinzu; führen Sie hierfür in Abhängigkeit von Ihrer Umgebung die folgenden Schritte aus:

		**Wichtig**: Bei der Verwendung von Xcode 7.x unter iOS 9 müssen Sie die Einstellung 'Enable Bitcode' bei den Xcode-Buildeinstellungen auf 'No' setzen. Sie können diese Einstellung durch Öffnen von Xcode mit der Cordova-Projektdatei '.xcodeproj' ändern; diese befidnet sich im Ordner 'platform\iPhone'.

		* IBM MobileFirst™ Platform Foundation Version 7.1:

			1. Geben Sie den folgenden Befehl ein, um das {{site.data.keyword.mqa}}-Plug-in zu installieren:

				```
				mfp cordova plugin add plugin_location
				```
				{: codeblock}

			Dabei ist *plugin_location* der Pfad zu dem Verzeichnis mit dem extrahierten {{site.data.keyword.mqa}}-Plug-in, das Sie heruntergeladen haben.

			2. Wenn Ihre App unter Android ausgeführt wird, müssen Sie die Datei `project_name/app_name/platforms/android/custom_rules.xml` in `custom_rules.xml.bak` umbenennen.

		* Apache Cordova vor Version 4.0:
			1. Geben Sie den folgenden Befehl ein, um das {{site.data.keyword.mqa}}-Plug-in zu installieren:

				```
				cordova plugin add plugin_location
				```
				{: codeblock}

			Dabei ist *plugin_location* der Pfad zu dem Verzeichnis mit dem extrahierten {{site.data.keyword.mqa}}-Plug-in, das Sie heruntergeladen haben.

			2. Geben Sie den folgenden Befehl ein, um ein zusätzliches erforderliches Plug-in hinzuzufügen:

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

			3. Wenn Ihre App unter Android ausgeführt wird, müssen Sie die Datei `project_name/app_name/platforms/android/custom_rules.xml` in `custom_rules_bak.xml` umbenennen.

		* Apache Cordova ab Version 4.0:

			1. Geben Sie den folgenden Befehl ein:

				```
				cordova plugin add plugin_location
				```
				{: codeblock}

			Dabei ist *plugin_location* der Pfad zu dem Verzeichnis mit dem extrahierten {{site.data.keyword.mqa}}-Cordova-Plug-in, das Sie heruntergeladen haben.

			2. Geben Sie den folgenden Befehl ein, um ein zusätzliches erforderliches Plug-in hinzuzufügen:

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

2. Starten Sie bei jeder Anmeldung eine neue Sitzung von {{site.data.keyword.mqa}}.

	1. Öffnen Sie die Datei `index.js`, die sich im folgenden Verzeichnis befindet: `Eigener Projektname\www\js`.

	2. Fügen Sie die folgende Funktion und die folgenden Parameter innerhalb der Funktion `onDeviceReady()` in der Datei `index.js` hinzu. Platzieren Sie die Funktion vor der geschweiften Endeklammer der Funktion.

	Einschränkung: Für eine App, die bereits für Mobile Quality Assurance mit einer älteren Version des Plug-ins für Cordova zur Verwendung der im Mobile Quality Assurance-Plug-in für Cordova Version 3.0.18 und höhere Versionen enthaltenen Features instrumentiert ist, müssen Sie Ihren App-Schlüssel neu generieren und ersetzen. Weitere Informationen zur Neugenerierung Ihres App-Schlüssels finden Sie im Abschnitt zur Verwaltung der App-Einstellungen. App-Schlüssel, die vor Februar 2016 generiert wurde, funktionieren zwar weiterhin mit dem älteren Plug-in, aber nicht mehr mit dem Plug-in-Upgrade Version 3.0.18 (oder höher).

		```
		MQA.startNewSession(
			{
				mode: "QA",
				// or mode: "MARKET" for production mode.
			android: {
				appKey: "your_MQA_Android_appKey" ,
				notificationsEnabled: true},
			ios: {
				appKey: "your_MQA_iOS_appKey" ,
				screenShotsFromGallery: true,}
			},
			{
			success: function () {console.log("Session
			   Started successfully");},
			error: function (string) { console.log("Session
			   error" + string);}
			}
			);
		```
		{: codeblock}

	3. Fahren Sie mit den Schritten in [Einführung in {{site.data.keyword.mqa}}](index.html) fort.



# Zugehörige Links
{: #rellinks notoc}

## Zugehörige Links
{: #general notoc}
* [Einführung in {{site.data.keyword.mqa}}](index.html){:new_window}
