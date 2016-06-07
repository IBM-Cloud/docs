---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Einführung in Insights for Weather
{: #insights_weather_overview}

*Letzte Aktualisierung: 19. Mai 2016*

Verwenden Sie {{site.data.keyword.weatherfull}},
um Wetterdaten von "The Weather Company" (TWC) in Ihre {{site.data.keyword.Bluemix}}-Anwendungen einzubinden.
{:shortdesc}

**Anmerkung:** Der Service 'Insights for Weather' ist in Japan derzeit nicht verfügbar.

Bevor Sie starten, erstellen Sie im Dashboard eine {{site.data.keyword.Bluemix_notm}}-Web-App
mit einer Laufzeit, z. B. Liberty for Java. Warten Sie auf die Bereitstellung Ihrer App und fügen Sie dann
den Service 'Insights for Weather' zu Ihrer App hinzu.

Wenn Sie Ihre App an Insights for Weather binden,
stellen Sie eine Serviceinstanz mit eindeutigen Berechtigungsnachweisen bereit. Ihre App
nutzt diese Berechtigungsnachweise mit den [REST-APIs](https://twcservice.{APPDomain}/rest-api/){:new_window}, um Wetterdaten abzurufen.

Befolgen Sie diese Schritte, um die Berechtigungsnachweise aus `VCAP_SERVICES` abzurufen und die Serviceinstanz mit Ihrer App zu integrieren.

1. Navigieren Sie zur Übersichtsseite der Anwendung.
2. Rufen Sie den Abschnitt **Umgebungsvariablen** auf. Die `VCAP_SERVICES`-Informationen werden für jeden Ihrer Services angezeigt.
3. Notieren Sie die Werte für Benutzername und Kennwort des Insights for Weather-Service.
Um die [REST-APIs](https://twcservice.{APPDomain}/rest-api/){:new_window} zu testen, müssen Sie diese Berechtigungsnachweise eingeben,
wenn Sie bei der Anmeldung dazu aufgefordert werden.
Ihre `VCAP_SERVICES` sehen ähnlich wie im folgenden Beispiel aus:

```
{
   "weatherinsights": [
     {
      "name": "Insights for Weather",
      "label": "weatherinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "twcservice.mybluemix.net",
         "password": "7abcxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }
   ]
}
```

**Hinweis:** Alle Bereiche sind voneinander unabhängig. Sie können die Berechtigungsnachweise des Service,
die Ihnen in einer Region bereitgestellt wurden, nicht für die Authentifizierung
bei einem Service in einer anderen Region verwenden.
Wenn Sie keine gültigen Berechtigungsnachweise eingeben, wird im
Antwortteil eine Nachricht über unberechtigten Zugriff ausgegeben. 

# Rellinks
{: #rellinks}
## Beispiele
{: #samples}
* [Demo: Insights for Weather](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [Wie ist das Wetter in Bluemix? ](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

## API
{: #api}
* [REST-API](https://twcservice.{APPDomain}/rest-api/){: new_window}

## Kompatible Laufzeiten
{: #buildpacks}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## Allgemeines
{: #general}
* [Hinzufügen eines Service zur Anwendung](../reqnsi.html){: new_window}
* [End-to-End-Entwicklung](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} Preisliste](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} Voraussetzungen](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
