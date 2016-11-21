---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Einführung in {{site.data.keyword.weather_short}}
{: #insights_weather_overview}

Verwenden Sie {{site.data.keyword.weatherfull}},
um Wetterdaten von "The Weather Company" (TWC) in Ihre {{site.data.keyword.Bluemix}}-Anwendungen einzubinden.
{:shortdesc}

**Achtung:** Derzeit kann der Service {{site.data.keyword.weather_short}} in folgenden Ländern
oder Regionen **nicht** erworben oder verwendet werden: Afghanistan, Armenien,
Aserbaidschan, Bahrain, Bangladesch, Bhutan, Brunei, Kambodscha, China, Zypern, Georgien,
Indonesien, Iran, Irak, Japan, Jordanien, Kasachstan,
Kuwait, Kirgistan, Laos, Libanon, Malaysia, Malediven, Mongolei,
Myanmar, Nepal, Oman, Pakistan, Philippinen, Katar, Russland, Saudi-Arabien,
Singapur, Südkorea, Sri Lanka, Syrien, Tadschikistan, Timor-Leste, Türkei,
Turkmenistan, Vereinigte Arabische Emirate, Usbekistan, Vietnam, Jemen. Diese Liste wird aktualisiert, sobald weitere Informationen verfügbar sind.

Wenn eine Ihrer vorhandenen Anwendungen den Service [Insights for Weather](https://console.{DomainName}/docs/services/InsightsWeather/index.html){: new_window} verwendet, funktioniert Ihre App nach der Einführung von {{site.data.keyword.weather_short}} weitere 90 Tage, ohne dass Änderungen vorgenommen werden müssen. Um die neu hinzugefügten APIs und das verbesserte Preismodell
nutzen zu können, können Sie Ihre Anwendung auf den neuen Service migrieren.

Bevor Sie starten, erstellen Sie im Dashboard eine {{site.data.keyword.Bluemix_notm}}-Web-App
mit einer Laufzeit, z. B. Liberty for Java. Warten Sie auf die Bereitstellung Ihrer App und fügen Sie dann den Service {{site.data.keyword.weather_short}} zu Ihrer App hinzu.

Wenn Sie Ihre App an {{site.data.keyword.weather_short}} binden, stellen Sie eine Serviceinstanz mit eindeutigen Berechtigungsnachweisen bereit. Ihre App
nutzt diese Berechtigungsnachweise mit den [REST-APIs](https://twcservice.{APPDomain}/rest-api/){:new_window}, um Wetterdaten abzurufen.

Befolgen Sie diese Schritte, um die Service-Berechtigungsnachweise aus `VCAP_SERVICES` abzurufen und die Serviceinstanz mit Ihrer App zu integrieren.

1. Navigieren Sie zur Übersichtsseite der Anwendung.
2. Rufen Sie den Abschnitt **Umgebungsvariablen** auf. Die `VCAP_SERVICES`-Informationen werden für jeden Ihrer Services angezeigt.
3. Notieren Sie die Werte für Benutzername und Kennwort des {{site.data.keyword.weather_short}}-Service.
Um die [REST-APIs](https://twcservice.{APPDomain}/rest-api/){:new_window} zu testen, müssen Sie diese Berechtigungsnachweise eingeben,
wenn Sie bei der Anmeldung dazu aufgefordert werden.
Ihre `VCAP_SERVICES` sehen ähnlich wie im folgenden Beispiel aus:

```
{
{
   "weatherinsights": [
      {
         "name": "Weather Company Data for IBM Bluemix",
         "label": "weatherinsights",
         "plan": "Free",
         "credentials": {
            "username": "d40845df-8125-441f-8e7c-e650726ce721",
            "password": "tDV0HGZz3O",
            "host": "twcservice.mybluemix.net",
            "port": 443,
            "url": "https://d40845df-8125-441f-8e7c-e650726ce721:tDV0HGZz3O@twcservice.mybluemix.net"
         }
      }
   ]
}
```

**Hinweis:** Alle Bereiche sind voneinander unabhängig. Sie können die Berechtigungsnachweise des Service,
die Ihnen in einer Region bereitgestellt wurden, nicht für die Authentifizierung
bei einem Service in einer anderen Region verwenden.
Wenn Sie keine gültigen Berechtigungsnachweise eingeben, wird im Antwortteil eine Nachricht über unberechtigten Zugriff ausgegeben.

# Zugehörige Links
{: #rellinks}
## Beispiele
{: #samples}
* [Demo-App für {{site.data.keyword.weather_short}}](http://weather-company-data-demo.{APPDomain}){: new_window}
* [Vertiefungsvideo für {{site.data.keyword.weather_short}}](https://youtu.be/pZHXIibziUo){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [Beispiel-App für {{site.data.keyword.Bluemix_notm}} + Weather](https://github.com/IBM-Bluemix/insights-weather){: new_window}
* [IBM Cloud - Bare Metal, NYC Taxi Data und Insights for Weather (YouTube-Lernprogramm)](https://www.youtube.com/watch?v=Uwmzpx9DZ5c){: new_window}

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
* [Hinzufügen eines Service zur Anwendung](/docs/services/reqnsi.html){: new_window}
* [End-to-End-Entwicklung](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} Preisliste](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} Voraussetzungen](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
