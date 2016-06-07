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

*Letzte Aktualisierung: 6. April 2016*

Verwenden Sie {{site.data.keyword.weatherfull}},
um Wetterdaten von "The Weather Company" (TWC) in Ihre {{site.data.keyword.Bluemix}}-Anwendungen einzubinden.
{:shortdesc}

In den nachfolgenden Anweisungen finden Sie Informationen darüber, wie Sie eine Anwendung erstellen,
sie an den Insights for Weather-Service binden und
die Serviceberechtigungsnachweise für die Interaktion mit den [REST-APIs](https://twcservice.{APPDomain}/rest-api/) abrufen können.

### Erstellen einer Anwendung
{: #create_an_app}

Zu Demonstrationszwecken erstellen Sie eine Anwendung, indem Sie die Liberty for
Java-Laufzeit verwenden. Der nachfolgende allgemeine
Prozess kann jedoch auch auf andere Laufzeiten angewendet werden. 

1. Wenn keine Anwendung vorhanden ist, klicken Sie im Dashboard auf **App erstellen**.
2. Wenn Sie zur Auswahl einer App-Vorlage aufgefordert werden, klicken Sie auf **Web**.
3. Wenn Sie zur Auswahl eines Starters aufgefordert werden, klicken Sie auf **Liberty for Java**.
4. Klicken Sie auf **Weiter**.
5. Geben Sie im Feld **App-Name** den Namen Ihrer App ein.
6. Klicken Sie auf **Fertigstellen**. Warten Sie, bis die Anwendung bereitgestellt ist.

### Hinzufügen des Insights for Weather-Service
{: #add_insights_for_weather_service}

Führen Sie die folgenden Schritte aus, um den Insights for Weather-Service zu Ihrer Anwendung hinzuzufügen.
1. Öffnen Sie das Menü **Katalog**.
2. Klicken Sie im Abschnitt **Data & Analytics** auf die Kachel **Insights for Weather**.
3. Wählen Sie in der Dropdown-Liste **App** die gewünschte App aus.
4. Klicken Sie auf **Verwenden**.
5. Wenn Sie dazu aufgefordert werden, klicken Sie auf
**Erneutes Staging**, um die Anwendung erneut zu starten.

### Abrufen der Insights for Weather-Berechtigungsnachweise
{: #retrieve_weather_credentials}

Wenn Sie Ihre Anwendung an Insights for Weather binden,
stellen Sie eine Serviceinstanz mit eindeutigen Berechtigungsnachweisen bereit. Diese Berechtigungsnachweise
werden in der Umgebungsvariablen `VCAP_SERVICES` der jeweiligen Anwendung gespeichert und sind für die Interaktion zwischen den Services erforderlich.

1. Navigieren Sie zur Übersichtsseite der Anwendung.
2. Rufen Sie den Abschnitt **Umgebungsvariablen** auf. Die `VCAP_SERVICES`-Informationen werden für jeden Ihrer Services angezeigt. 
3. Notieren Sie die Werte für Benutzername und Kennwort des Insights for Weather-Service.
Um die [REST-APIs](https://twcservice.{APPDomain}/rest-api/){:new_window} zu testen, müssen Sie diese Berechtigungsnachweise eingeben, wenn Sie bei der Anmeldung dazu aufgefordert werden.
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

# Rellinks
## Beispiele
* [Demo: Insights for Weather](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [Wie ist das Wetter in Bluemix? ](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

## API
* [REST-API](https://twcservice.{APPDomain}/rest-api/){: new_window}

## Kompatible Laufzeiten{:id="buildpacks"}
* [Liberty for Java](https://console.{DomainName}/docs/starters/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## Allgemeines
* [Informationen zu Insights for Weather](https://console.{DomainName}/docs/services/Weather/weather_overview.html){: new_window}
* [Hinzufügen eines Service zur Anwendung](https://console.{DomainName}/docs/services/reqnsi.html#add_service){: new_window}
* [End-to-End-Entwicklung](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} Preisliste](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} Voraussetzungen](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
