---

copyright:
  years: 2016
lastupdated: "2016-10-21"

---
{:new_window: target="_blank"}

# Neuerungen im Mobile Dashboard
{: #what_is_new}

Mit der Oktober-Aktualisierung der {{site.data.keyword.Bluemix}} Mobile-Dashboards wurden folgende Änderungen eingeführt:

   * Sie können Ihrem Projekt jetzt die Push Notifications- und Analytics-Funktionen direkt über das Dashboard hinzufügen.
   * Es stehen jetzt [Code-Starter](starters.html#Code_Starter) zur Verfügung.
   * Sie können Ihren Projekten, die Sie mit einem Code-Starter erstellt haben, die Funktion 'Authentication' hinzufügen.
   * Swift wird jetzt unterstützt.


### Analytics
{: #analytics}

   * Der Demo-Modus ist standardmäßig aktiviert, wenn Sie die Analytics-Funktion hinzufügen. Sie können den Demo-Modus ausschalten, um Ihre Analyse anzuzeigen, nachdem Sie Ihre App ausgeführt haben.


### Benutzerschnittstellenbuilder
{: #ui_builder}

   * Auf die **Push Notifications**-Funktion wird jetzt über das Projekt zugegriffen.
   * Die Registerkarte **Projekteinstellungen** wurde in **Einstellungen** umbenannt.
   * Die Registerkarte **Authentifizierung** wurde in **Benutzerzugriff** umbenannt.


### Code
{: #code}

   * Der generierte Objective-C- und Swift-Code für iOS verwendet für die Verwaltung von Abhängigkeiten jetzt CocoaPods. Das bedeutet, dass Sie CocoaPods installieren müssen. Für die Installation führen Sie `sudo gem install cocoapods` aus. Nach der Installation von CocoaPods führen Sie `pod setup` aus, um es zu konfigurieren (wenn es nicht bereits konfiguriert ist). Zum Schluss führen Sie `pod install` aus, um die erforderlichen Projektabhängigkeiten vor dem Öffnen Ihrer `.xcworkspace`-Datei in Xcode herunterzuladen und zu installieren. Weitere Einzelheiten stehen in der `README.md`-Datei im heruntergeladenen Code-Archiv zur Verfügung. Weitere Informationen erhalten Sie unter [Vorausgesetzte Entwicklertools](get_code.html#prereq-dev-tools).

Prüfen Sie regelmäßig nach, ob neue Aktualisierungen zur Verfügung stehen.
