---

copyright:
  years: 2016
lastupdated: "2016-10-18"

---
{:new_window: target="_blank"}

# Neuerungen im Mobile Dashboard
{: #what_is_new}

Letzte Aktualisierung: 18. Oktober 2016
{: .last-updated}

Mit der Oktober-Aktualisierung der {{site.data.keyword.Bluemix}} Mobile-Dashboards wurden folgende Änderungen eingeführt:

   * Sie können Ihrem Projekt jetzt die Push Notifications- und Analytics-Funktionen direkt über das Dashboard hinzufügen.
   * Es stehen jetzt [Code-Starter](starters.html#Code_Starter) zur Verfügung.
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


# Zugehörige Links
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Beta)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## Blogbeiträge
{: #general}
* [Blogbeitrag: Einführung in das Bluemix Mobile-Dashboard](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [Blogbeitrag: Einführung in die nächste Generation des Bluemix Mobile-Dashboards](https://ibm.com/blogs/bluemix/2016/10/introducing-the-next-generation-of-the-bluemix-mobile-dashboard/){: new_window}
* [Blogbeitrag: Einführung in Code-Starter für Bluemix Mobile](https://www.ibm.com/blogs/bluemix/2016/10/rapid-dev-with-mobile-code-starters/){: new_window}
* [Blogbeitrag: Bluemix Mobile, Teil 1: App 'Store Catalog' erstellen](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [Blogbeitrag: Bluemix Mobile, Teil 2: Angepasstes Bluemix-Back-End in die App 'Store Catalog' integrieren](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}

## Lernprogramme und Beispiele
{: #samples}
* [Mobiles Back-End für Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
