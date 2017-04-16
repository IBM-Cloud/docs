---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Einführung in {{site.data.keyword.streaminganalyticsshort}}
{: #gettingstarted}

{{site.data.keyword.streaminganalyticsshort}} basiert auf der Technologie von {{site.data.keyword.streamsshort}},
einer zukunftsweisenden Analyseplattform, die Sie verwenden können, um Informationen zu erfassen, zu analysieren und zu korrelieren,
die in Echtzeit aus verschiedenen Arten von Datenquellen abgerufen werden. Wenn Sie eine Instanz des {{site.data.keyword.streaminganalyticsshort}}-Service erstellen,
erhalten Sie so eine eigene Instanz von {{site.data.keyword.streamsshort}}, die in der
{{site.data.keyword.Bluemix_short}}-Cloud ausgeführt wird und somit bereit ist,
Ihre {{site.data.keyword.streamsshort}}-Anwendungen auszuführen.
{:shortdesc}

Sie können Ihre Anwendungen für eine {{site.data.keyword.streaminganalyticsshort}}-Instanz
bereitstellen, die in der
{{site.data.keyword.Bluemix_short}}-Cloud ausgeführt wird.

Sie können die Arbeit mit {{site.data.keyword.streaminganalyticsshort}} direkt beginnen, indem Sie die
[Starteranwendungen](/docs/services/StreamingAnalytics/c_starterapps.html){:new_window} ausführen. Wenn Sie Ihre eigenen Anwendungen noch weitergehend einsetzen wollen, benötigen Sie eine {{site.data.keyword.streamsshort}}-Entwicklungsumgebung und Sie müssen Ihre SPL für die Cloud vorbereiten.

Um die Arbeit mit {{site.data.keyword.streaminganalyticsshort}} zu beginnen, verwenden Sie eine der folgenden Methoden, um die Anwendungsbundledatei (die Datei mit der Erweiterung .sab) zu übergeben, die Ihrer SPL- oder Java™-Anwendung zugeordnet ist:
* Verwenden Sie die {{site.data.keyword.streaminganalyticsshort}}-Konsole.
* Entwickeln Sie eine {{site.data.keyword.Bluemix_short}}-Anwendung und fügen Sie ihr die {{site.data.keyword.streamsshort}}-Anwendung hinzu. Steuern Sie sie unter Verwendung der [{{site.data.keyword.streaminganalyticsshort}}-REST-API](https://console.ng.bluemix.net/apidocs/220). Stellen Sie sicher, dass Ihre SPL- oder Java-Anwendung in Ihrer Entwicklungsumgebung ordnungsgemäß ausgeführt wird.

Sie können {{site.data.keyword.streaminganalyticsshort}} jetzt mit anderen {{site.data.keyword.Bluemix_short}}-Services verwenden,
einschließlich {{site.data.keyword.cloudant}} und {{site.data.keyword.messagehub}}. In den [Lernprogrammen für die Integration mit anderen {{site.data.keyword.Bluemix_short}}-Services](/docs/services/StreamingAnalytics/r_integrating_cloudant_rest.html){:new_window}
finden Sie Beispiele, die Ihnen beim Einstieg helfen.

Um eine {{site.data.keyword.streamsshort}}-Anwendung zu entwickeln,
müssen Sie über eine {{site.data.keyword.streamsshort}}-Entwicklungsumgebung verfügen. Wenn Sie nicht über eine {{site.data.keyword.streamsshort}}-Umgebung verfügen, können Sie die {{site.data.keyword.streamsshort}} Quick Start Edition gebührenfrei von der [{{site.data.keyword.streamsshort}}-Produktseite herunterladen.](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)

Wenn Sie keine Erfahrung mit der Entwicklung von {{site.data.keyword.streamsshort}}-Anwendungen haben,
können Sie sich hierüber anhand der zur Verfügung stehenden Ressourcen informieren. Weitere Informationen finden Sie im [{{site.data.keyword.streamsshort}} Knowledge Center.](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}

Wenn Sie bereits über eine SPL-Anwendung verfügen, die Sie lokal (on premise) ausführen, müssen Sie [Ihre Anwendung für die Cloud vorbereiten.](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud/){:new_window}

# Zugehörige Links
{: #rellinks}

## Lernprogramme und Beispiele
{: #samples}
* [Einführung in {{site.data.keyword.streaminganalyticsshort}}](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix){:new_window}
* [{{site.data.keyword.streaminganalyticsshort}} SDK for Node.js™ - Starteranwendung](http://bit.ly/1iR1bzu){:new_window}
* [{{site.data.keyword.streaminganalyticsshort}} Liberty for Java™ - Starteranwendung](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-starter-application/){:new_window}
* [SPL-Anwendung für die Cloud vorbereiten](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud){:new_window}
* [Bluemix {{site.data.keyword.streaminganalyticsshort}} Development Guide](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-development-guide/){:new_window}
* [Weitere Lernprogramme](StreamingAnalytics.html#r_integrating_cloudant_rest){:new_window}


## API-Referenz
{: #api}
* [{{site.data.keyword.streaminganalyticsshort}}-REST-API](https://console.ng.bluemix.net/apidocs/220){:new_window}
* [{{site.data.keyword.streaminganalyticsshort}}-Metriken, die die {{site.data.keyword.streamsshort}}-REST-API nutzen](https://developer.ibm.com/bluemix/2016/07/25/streaming-analytics-metrics-using-rest-api/){:new_window}

## Kompatible Laufzeitumgebungen
{: #buildpacks}
* [Liberty for Java](/docs/runtimes/liberty/index.html#liberty)
* [Node.js](/docs/runtimes/nodejs/index.html#nodejs)

## Zugehörige Links
{: #general}
* [{{site.data.keyword.streamsshort}}-Dokumentation](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}
* [{{site.data.keyword.streamsshort}}Quick
Start Edition](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window}
