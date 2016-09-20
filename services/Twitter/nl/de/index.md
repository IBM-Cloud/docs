{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Einführung in Insights for Twitter {: #insights_twitter_overview}

*Letzte Aktualisierung: 13. Mai 2016*
{: .last-updated}

Mithilfe von {{site.data.keyword.twitterfull}} können Sie Twitter-Inhalte aus den Twitter [Decahose](http://support.gnip.com/apis/firehose/overview.html){: new_window}- oder [PowerTrack](http://support.gnip.com/apis/powertrack/overview.html){: new_window}-Streams in Ihre {{site.data.keyword.Bluemix}}-Anwendungen integrieren.{:shortdesc}

Um mit der Verwendung von {{site.data.keyword.twittershort}} zu beginnen, müssen Sie zunächst Ihre Bluemix-Webanwendung mit einer Laufzeit erstellen, z. B. Liberty for Java, und anschließend den Service {{site.data.keyword.twittershort}} zu Ihrer App hinzufügen. Ist der Service {{site.data.keyword.twittershort}} an Ihre App gebunden, wird die Serviceinstanz mit eindeutigen Berechtigungsnachweisen bereitgestellt. Ihre App verwendet diese Berechtigungsnachweise in Kombination mit den REST-APIs, um den Twitter-Inhalt zu durchsuchen und zu nutzen.  Führen Sie diese Schritte durch, um die Berechtigungsnachweise aus VCAP_SERVICES abzurufen und die Serviceinstanz mit Ihrer App zu integrieren.

1. Navigieren Sie zur Übersichtsseite der Anwendung.
2. Rufen Sie den Abschnitt **Umgebungsvariablen** auf. Die Informationen in `VCAP_SERVICES` werden für die einzelnen Services angezeigt.
3. Notieren Sie die Werte für Benutzername und Kennwort des {{site.data.keyword.twittershort}}-Service. Zum Testen von Operationen in der REST-API-Referenzdokumentation müssen Sie diese Berechtigungsnachweise eingeben. `VCAP_SERVICES` kann beispielsweise in etwa wie folgender Ausschnitt aussehen:

```
{  
   "twitterinsights": [    
     {      
      "name": "IBM Insights for Twitter-x3",
      "label": "twitterinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "cdeservice.mybluemix.net",
         "password": "7cunxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }  
   ]
}
```

<!--
## Adding Insights for Twitter to your application {: #adding_twitter}

The following instructions guide you through the process of creating an application, binding the application to the {{site.data.keyword.twittershort}} service, and retrieving the service credentials to interact with REST API operations in the provided API reference documentation.

### Create an application
For demonstration purposes, you'll create an application using the Liberty for Java&trade;  runtime, but the general process described below can be applied to other runtimes. If you don't have an existing application, click **CREATE AN APP** in the dashboard. When asked to confirm the type of app, click **WEB**.

1. Open the **Catalog** menu.
2. From the **Runtimes** section, click **Liberty for Java**.
3. Click **Create**.
4. In the **App Name** field, specify the name of your app.
5. Click **Finish**. Wait for your application to provision.

### Add the Insights for Twitter service
Follow these steps to add the {{site.data.keyword.twittershort}} service to your app.

1. Open the **Catalog** menu.
2. From the **Data & Analytics** section, click the {{site.data.keyword.twittershort}} tile.
3. In the **App** field, select the name of your app.
4. Click **Create**.
5. When prompted, click **Restage** to restart your application.
-->

# Zugehörige Links
## Beispiele
* [Interaktive Demo für Decahose-Suche](https://cdetestapp.mybluemix.net/){: new_window}
* [developerWorks: Lernprogramm und Quellcode für Demo zur Decahose-Suche](http://www.ibm.com/developerworks/cloud/library/cl-twitter-search-insights-bluemix-trs/index.html){: new_window}
* [Analysieren der Verkaufszahlen für "American Sniper" (YouTube)](https://www.youtube.com/watch?v=Gfk5quglXvI){: new_window}
* [Places Insights - Praktische Anwendung](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}

## API
* [REST-API](https://cdeservice.{APPDomain}/rest-api/){: new_window}

## Kompatible Laufzeiten{:id="buildpacks"}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Swift](https://console.{DomainName}/docs/runtimes/swift/index.html){: new_window}
* [Tomcat](https://console.{DomainName}/docs/runtimes/tomcat/index.html){: new_window}

## Allgemeines
* [Neuerungen bei den {{site.data.keyword.Bluemix_notm}}-Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){: new_window}
* [Service zur Anwendung hinzufügen](../reqnsi.html){: new_window}
* [Umfassende Entwicklung](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}}-Preisliste](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}}-Voraussetzungen](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}

