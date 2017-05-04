---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Neuerungen in der {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}}
{: #what-is-new}


## Neu ab März 2017
{: #mar-2017}

Mit der Aktualisierung der {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} im März 2017 wurden folgende Änderungen eingeführt:

   * Das {{site.data.keyword.Bluemix_notm}} Mobile-Dashboard ist jetzt die {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}}.
   * Die Projekterstellung wurde überarbeitet und schließt jetzt Web-App-, BFF- und Microservice-Servermustertypen mit Unterstützung für Node.js, Java und Swift ein.
   * Die Integration in den neuen und verbesserten {{site.data.keyword.appid_full}}-Service ermöglicht die Authentifizierung für Mobile and Web-Projekte.
   * Jetzt können Sie SDKs für Ihre Projekte mit dem [SDK Generator-Plug-in](sdk_cli.html) generieren. Die SDK-Generierung in der {{site.data.keyword.dev_console}} ist nur für mobile Projekte verfügbar.
   * Jetzt können Sie Projekte mit dem [{{site.data.keyword.dev_cli_short}}](dev_cli.html) erstellen.


## Neu ab Januar 2017
{: #jan-2017}

Mit der Aktualisierung des {{site.data.keyword.Bluemix_notm}} Mobile-Dashboards im Januar 2017 wurden folgende Änderungen eingeführt:

   * Ab dem 31. Januar gelten Benutzerschnittstellenstarter als veraltet. Vorhandene Projekte, die mit einem Benutzerschnittstellenstarter erstellt wurden, können bis 30. April 2017 verwendet werden. Weitere Informationen zu den Migrationsschritten und zum Entfernungsdatum finden Sie im [Blogbeitrag mit den Ankündigungen für die Einstellung der Unterstützung ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2017/01/bluemix-mobile-dashboard-update/).
{: deprecated}
   * Sie können den Startertyp Ihres Projekts jetzt aktualisieren, anstatt das Projekt zu löschen und ein neues Projekt zu erstellen.
   * Sie können jetzt ein Projekt mit einem [Watson Conversation](tutorial_conversation.html)-Code-Starter erstellen.
   * Falls dies unterstützt wird, können Sie jetzt ein SDK für Ihr Projekt erstellen.
   * Sie können jetzt Ihre vorhandenen [Compute](sdk_compute.html)-Instanzen hinzufügen und Client-SDKs generieren, die dann zu Ihrem Projekt hinzugefügt werden.


## Neu ab Dezember 2016
{: #dec-2016}

Mit der Aktualisierung des {{site.data.keyword.Bluemix_notm}} Mobile-Dashboards im Dezember 2016 wurden die folgenden Änderungen eingeführt:

   * Sie können jetzt einen verbundenen Service aus einem Projekt entfernen, um ihn zu löschen oder mit einem anderen Projekt wiederzuverwenden. 
   * Sie können jetzt einen vorhandenen Service zu einem Projekt hinzufügen.
   * Sie können jetzt einen CloudantNoSQL-Service als Datenquelle erstellen oder einen vorhandenen Service verbinden, wenn Sie einen Code-Starter verwenden.
   * Falls dies unterstützt wird, können Sie jetzt einen Object Storage-Service als Datenquelle für Ihr Projekt erstellen oder einen vorhandenen Service verbinden.
   * Sie können jetzt das Navigationsdesign der App, die Sie erstellen, mit einem Benutzerschnittstellenstarter anpassen. 
   

## Neu ab November 2016
{: #nov-2016}

Mit der November-Aktualisierung des {{site.data.keyword.Bluemix_notm}} Mobile-Dashboards wurden folgende Änderungen eingeführt:

   * Sie können jetzt SDK-Artefakte für Ihre Projekte auf der Seite **Code** generieren.
   * Cordova wird jetzt für den Basic Code Starter unterstützt.
   * Sie können jetzt [Netzwerkereignisse auflisten ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobileanalytics/sdk.html#network-requests){: new_window} und [Netzanforderungen überwachen ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobileanalytics/app-monitoring.html#monitor-network-requests){: new_window} (auf der Seite **Netzanforderungen** der {{site.data.keyword.mobileanalytics_short}}-Konsole).
   * Sie können jetzt [Daten in dashDB exportieren ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobileanalytics/app-monitoring.html#dashdb){: new_window} (in der {{site.data.keyword.mobileanalytics_short}}-Konsole).


## Neu ab Oktober 2016
{: #oct-2016}

Mit der Aktualisierung des {{site.data.keyword.Bluemix_notm}} Mobile-Dashboards im Oktober 2016 wurden folgende Änderungen eingeführt:

   * Sie können Ihrem Projekt jetzt {{site.data.keyword.mobilepushshort}}- und Analytics-Funktionen direkt über das Dashboard hinzufügen.
   * Es stehen jetzt [Code-Starter](starters.html#Code_Starter) zur Verfügung.
   * Sie können Ihren Projekten, die Sie mit einem Code-Starter erstellt haben, die Funktion 'Authentication' hinzufügen.
   * Swift wird jetzt unterstützt.


### Analytics
{: #analytics notoc}

   * Der Demo-Modus ist standardmäßig aktiviert, wenn Sie die Analytics-Funktion hinzufügen. Sie können den Demo-Modus ausschalten, um Ihre Analyse anzuzeigen, nachdem Sie Ihre App ausgeführt haben.


### Benutzerschnittstellenbuilder
{: #ui_builder notoc}

   * Auf die Funktion für **{{site.data.keyword.mobilepushshort}}** wird jetzt über das Projekt zugegriffen.
   * Die Registerkarte **Projekteinstellungen** wurde in **Einstellungen** umbenannt.
   * Die Registerkarte **Authentifizierung** wurde in **Benutzerzugriff** umbenannt.


### Code
{: #code notoc}

   * Der generierte Objective-C- und Swift-Code für iOS verwendet für die Verwaltung von Abhängigkeiten jetzt CocoaPods. Das bedeutet, dass Sie CocoaPods installieren müssen. Für die Installation führen Sie `sudo gem install cocoapods` aus. Nach der Installation von CocoaPods führen Sie `pod setup` aus, um es zu konfigurieren (wenn es nicht bereits konfiguriert ist). Zum Schluss führen Sie `pod install` aus, um die Projektabhängigkeiten vor dem Öffnen Ihrer `.xcworkspace`-Datei in Xcode herunterzuladen und zu installieren. Weitere Einzelheiten stehen in der `README.md`-Datei im heruntergeladenen Code-Archiv zur Verfügung. Weitere Informationen erhalten Sie unter [Vorausgesetzte Entwicklertools](get_code.html#prereq-dev-tools).

Prüfen Sie regelmäßig nach, ob neue Aktualisierungen zur Verfügung stehen.
