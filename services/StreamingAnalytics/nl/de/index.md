---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

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

Sie können sofort mit der Verwendung von {{site.data.keyword.streaminganalyticsshort}} beginnen, indem Sie die [Starteranwendungen](/docs/services/StreamingAnalytics/c_starterapps.html){:new_window} ausführen.

Als ersten Schritt bei der Arbeit mit {{site.data.keyword.streaminganalyticsshort}} verwenden Sie eine der folgenden Methoden, um die Anwendungsbundledatei (die Datei mit der Erweiterung .sab) zu übergeben, die Ihrer SPL-, Java™-, Python- oder Scala Streams-Anwendung zugeordnet ist:
* Verwenden Sie die Schaltfläche **Job übergeben** in der {{site.data.keyword.streaminganalyticsshort}}-Konsole.
* Entwickeln Sie eine {{site.data.keyword.Bluemix_short}}-Anwendung und fügen Sie ihr die {{site.data.keyword.streamsshort}}-Anwendung hinzu. Steuern Sie sie unter Verwendung der [{{site.data.keyword.streaminganalyticsshort}}-REST-API](https://console.ng.bluemix.net/apidocs/220).


Sie können {{site.data.keyword.streaminganalyticsshort}} zusammen mit anderen {{site.data.keyword.Bluemix_short}}-Services verwenden, z. B. mit {{site.data.keyword.cloudant}} und {{site.data.keyword.messagehub}}. In den [Lernprogrammen für die Integration mit anderen {{site.data.keyword.Bluemix_short}}-Services](/docs/services/StreamingAnalytics/r_integrating_cloudant_rest.html){:new_window} finden Sie Beispiele, die Ihnen beim Einstieg helfen.

Wenn Sie Ihre eigenen Anwendungen noch weitergehend einsetzen wollen, können Sie eine {{site.data.keyword.streamsshort}}-Entwicklungsumgebung einrichten und Sie müssen Ihre Anwendung für die Cloud vorbereiten. Wenn Sie nicht über eine {{site.data.keyword.streamsshort}}-Umgebung verfügen, können Sie die {{site.data.keyword.streamsshort}} Quick Start Edition gebührenfrei von der [{{site.data.keyword.streamsshort}}-Produktseite herunterladen.](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)

Wenn Sie keine Erfahrung mit der Entwicklung von {{site.data.keyword.streamsshort}}-Anwendungen haben,
können Sie sich hierüber anhand der zur Verfügung stehenden Ressourcen informieren. Weitere Informationen finden Sie im [{{site.data.keyword.streamsshort}} Knowledge Center.](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}

Wenn Sie bereits über eine SPL-Anwendung verfügen, die Sie lokal (on premise) ausführen, müssen Sie [Ihre Anwendung für die Cloud vorbereiten.](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud/){:new_window}

**Anmerkung:** Sie müssen Ihre Anwendungen unter Red Hat Enterprise Linux (RHEL) 6.5 oder einer entsprechenden CentOS-Version mit Intel-Prozessoren kompilieren. 

## {{site.data.keyword.streamsshort}}-Python-Apps für {{site.data.keyword.streaminganalyticsshort}}
{: #gettingstarted_py notoc}

Sie können jetzt Streams-Apps in einer Python-Umgebung, wie z. B. IBM Data Science Experience (DSX), erstellen und diese Apps an die {{site.data.keyword.streaminganalyticsshort}}-Instanz übergeben, damit sie in der Bluemix-Cloud bereitgestellt werden. Sie müssen {{site.data.keyword.streamsshort}} nicht mehr lokal installieren, um eine Streams-Python-App zu kompilieren und bereitzustellen.

Beginnen Sie, indem Sie Streams-Python-Beispielapps mithilfe von Jupyter-Notebooks in DSX erstellen und diese Apps direkt von DSX an die Serviceinstanz übergeben. Weitere Informationen finden Sie in [Entwicklung von Streams-Python-Apps in DSX](/docs/services/StreamingAnalytics/t_develop_apps_python.html#t_develop_python_dsx).

{{site.data.keyword.streaminganalyticsshort}} unterstützt auch die Bereitstellung von Streams-Apps von der lokalen Python-Umgebung. Sie müssen die [{{site.data.keyword.streamsshort}}-Python-Anwendungs-API](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features), die im 'streamsx'-Paket enthalten ist, verwenden, um Ihre Streams-Python-Apps lokal zu entwickeln und sie an die Serviceinstanz zu übergeben. Zuerst führen Sie die beschriebenen Schritte im Lernprogramm [Entwicklung für den {{site.data.keyword.streaminganalyticsshort}}-Service](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html) aus.
