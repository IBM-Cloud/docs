---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# Neuerungen im Mobile Dashboard
{: #what_is_new}

### Neu ab Dezember 2016
{: #dec-2016}

Mit der Aktualisierung des {{site.data.keyword.Bluemix}} Mobile-Dashboards im Dezember 2016 wurden die folgenden Änderungen eingeführt:

   * Sie können einen verbundenen Service aus einem Projekt entfernen, um ihn zu löschen oder mit einem anderen Projekt wiederzuverwenden. 
   * Sie können einen vorhandenen Service zu einem Projekt hinzufügen.
   * Sie können einen CloudantNoSQL-Service als Datenquelle erstellen (oder einen vorhandenen Service verbinden), wenn Sie einen Code-Starter verwenden.
   * Falls dies unterstützt wird, können Sie einen Object Storage-Service als Datenquelle für Ihr Projekt erstellen (oder einen vorhandenen Service verbinden).
   * Sie können das Navigationsdesign der App, die Sie erstellen, mit einem Benutzerschnittstellenstarter anpassen. 
   

### Neu ab November 2016
{: #nov-2016}

Mit der November-Aktualisierung des {{site.data.keyword.Bluemix}} Mobile-Dashboards wurden folgende Änderungen eingeführt:

   * Sie können jetzt SDK-Artefakte für Ihre Projekte auf der Seite **Code** generieren.
   * Cordova wird jetzt für den Basis-Code-Starter (Basic Code Starter) unterstützt.
   * Sie können jetzt [Netzereignisse auflisten ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobileanalytics/sdk.html#network-requests "Symbol für externen Link"){: new_window} und [Netzanforderungen überwachen ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobileanalytics/app-monitoring.html#monitor-network-requests "Symbol für externen Link"){: new_window} (auf der Seite **Netzanforderungen** der {{site.data.keyword.mobileanalytics_short}}-Konsole).
   * Sie können jetzt [Daten in dashDB exportieren![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobileanalytics/app-monitoring.html#dashdb "Symbol für externen Link"){: new_window} (in der {{site.data.keyword.mobileanalytics_short}}-Konsole).


### Neu ab Oktober 2016
{: #oct-2016}

Mit der Aktualisierung des {{site.data.keyword.Bluemix_notm}} Mobile-Dashboards im Oktober 2016 wurden folgende Änderungen eingeführt:

   * Sie können Ihrem Projekt jetzt {{site.data.keyword.mobilepushshort}}- und Analytics-Funktionen direkt über das Dashboard hinzufügen.
   * Es stehen jetzt [Code-Starter](starters.html#Code_Starter) zur Verfügung.
   * Sie können Ihren Projekten, die Sie mit einem Code-Starter erstellt haben, die Funktion 'Authentication' hinzufügen.
   * Swift wird jetzt unterstützt.


#### Analytics
{: #analytics}

   * Der Demo-Modus ist standardmäßig aktiviert, wenn Sie die Analytics-Funktion hinzufügen. Sie können den Demo-Modus ausschalten, um Ihre Analyse anzuzeigen, nachdem Sie Ihre App ausgeführt haben.


#### Benutzerschnittstellenbuilder
{: #ui_builder}

   * Auf die Funktion für **{{site.data.keyword.mobilepushshort}}** wird jetzt über das Projekt zugegriffen.
   * Die Registerkarte **Projekteinstellungen** wurde in **Einstellungen** umbenannt.
   * Die Registerkarte **Authentifizierung** wurde in **Benutzerzugriff** umbenannt.


#### Code
{: #code}

   * Der generierte Objective-C- und Swift-Code für iOS verwendet für die Verwaltung von Abhängigkeiten jetzt CocoaPods. Das bedeutet, dass Sie CocoaPods installieren müssen. Für die Installation führen Sie `sudo gem install cocoapods` aus. Nach der Installation von CocoaPods führen Sie `pod setup` aus, um es zu konfigurieren (wenn es nicht bereits konfiguriert ist). Zum Schluss führen Sie `pod install` aus, um die erforderlichen Projektabhängigkeiten vor dem Öffnen Ihrer `.xcworkspace`-Datei in Xcode herunterzuladen und zu installieren. Weitere Einzelheiten stehen in der `README.md`-Datei im heruntergeladenen Code-Archiv zur Verfügung. Weitere Informationen erhalten Sie unter [Vorausgesetzte Entwicklertools](get_code.html#prereq-dev-tools).

Prüfen Sie regelmäßig nach, ob neue Aktualisierungen zur Verfügung stehen.
