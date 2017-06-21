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

# {{site.data.keyword.streamsshort}}-Anwendungen für die Cloud bereitstellen
{: #t_deploytocloud}

Sie können Ihre {{site.data.keyword.streamsshort}}-Anwendungen
für eine {{site.data.keyword.streaminganalyticsshort}}-Instanz bereitstellen, die in der
{{site.data.keyword.Bluemix_short}}-Cloud ausgeführt wird.
{:shortdesc}

{{site.data.keyword.streamsshort}}-Anwendungen werden in {{site.data.keyword.streamsshort}} Processing Language (SPL), Java, Scala oder Python in einer {{site.data.keyword.streamsshort}}-Umgebung geschrieben. Sie können jetzt Streams-Python-Anwendungen ohne {{site.data.keyword.streamsshort}}-Umgebung entwickeln. Weitere Informationen finden Sie im Abschnitt [Bereitstellung von {{site.data.keyword.streamsshort}}-Python-Anwendungen für die Cloud](docs/services/StreamingAnalytics/t_deploytocloud.html#t_deploypython)


{{site.data.keyword.streaminganalyticsshort}} enthält keine {{site.data.keyword.streamsshort}}-Entwicklungsumgebung in der Cloud, aber Sie können die Anwendungen, die Sie lokal entwickeln, in der Cloud bereitstellen.

Bevor Sie mit der Arbeit beginnen, müssen Sie den Popup-Blocker Ihres Browsers inaktivieren, um die {{site.data.keyword.streaminganalyticsshort}}-Konsole anzuzeigen.

Gehen Sie wie folgt vor, um Ihre {{site.data.keyword.streamsshort}}-Anwendungen für die Cloud bereitzustellen:

1. Richten Sie die Entwicklungsumgebung ein, um Ihre Anwendung zu entwickeln und zu testen.

	Wenn Sie eine {{site.data.keyword.streamsshort}}-Umgebung verwenden möchten, können Sie {{site.data.keyword.streamsshort}} Quick Start Edition gebührenfrei herunterladen. Rufen Sie die [Produktseite von IBM Streams](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window} auf und klicken Sie auf die Schaltfläche zum **Download der nativen Softwareinstallation**.

2. Entwickeln Sie Ihre Streaming-Anwendung in Ihrer Entwicklungsumgebung. In der {{site.data.keyword.streamsshort}}-Entwicklungsumgebung können Sie Streams Studio oder die Befehlszeilentools verwenden, um Ihre Anwendung zu entwickeln.

3. Stellen Sie sicher, dass Ihre Streaming-Anwendung in Ihrer Entwicklungsumgebung ordnungsgemäß ausgeführt wird.**Anmerkung:** Sie müssen Ihre Anwendung unter einem Red Hat Enterprise Linux (RHEL) 6.5-Betriebssystem oder einer entsprechenden CentOS-Version mit Intel-Prozessoren kompilieren. 

4. Übergeben Sie das Anwendungsbundle (die Datei mit der Erweiterung .sab), die Ihrer SPL-, Java-, Scala- oder Python-Anwendung zugeordnet ist, an die Serviceinstanz in der Cloud. Verwenden Sie dazu eine der folgenden Methoden:
	* Verwenden Sie die {{site.data.keyword.streaminganalyticsshort}}-Konsole, um das Anwendungsbundle zu übergeben.
  * Erstellen Sie eine {{site.data.keyword.Bluemix_short}}-Anwendung und fügen Sie ihr die {{site.data.keyword.streamsshort}}-Anwendung hinzu. Steuern Sie sie unter Verwendung der {{site.data.keyword.streaminganalyticsshort}}-REST-API.

Ihre Anwendung wurde jetzt in der Cloud bereitgestellt. Sie können Ihre Anwendung überwachen, indem Sie den {{site.data.keyword.streaminganalyticsshort}}-Service verwenden. Sie haben auch die Möglichkeit, mehr als eine Anwendung (Dateien mit der Erweiterung .sab) an die Serviceinstanz zu übergeben. Dies können beliebig viele sein.

{{site.data.keyword.streamsshort}} unterstützt auch verschiedene Java™-Entwicklungskits, die Sie zur Entwicklung Ihrer Anwendungen verwenden können. Weitere Informationen zur Java-Unterstützung in {{site.data.keyword.streamsshort}} finden Sie unter [Supported Java development kits for application development](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-prerequisites-java-supported-sdks.html){:new_window}.

## {{site.data.keyword.streamsshort}}-Python-Anwendungen in der Cloud bereitstellen
{: #t_deploypython}

Stellen Sie Ihre {{site.data.keyword.streamsshort}}-Python-Anwendungen für einen {{site.data.keyword.streaminganalyticsshort}}-Service bereit, der in der {{site.data.keyword.Bluemix_short}}-Cloud ausgeführt wird. Sie benötigen dafür keine {{site.data.keyword.streamsshort}}-Installation.{:shortdesc}

Mit der [{{site.data.keyword.streamsshort}}-Python-Anwendungs-API](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features), die im Lieferumfang des 'streamsx'-Pakets enthalten ist, können Sie Python-Anwendungen für den {{site.data.keyword.streaminganalyticsshort}}-Service bereitstellen. Im Lernprogramm [Entwicklung für den {{site.data.keyword.streaminganalyticsshort}}-Service](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html) wird anhand eines Beispiels veranschaulicht, wie eine einfache Python-Anwendung für den {{site.data.keyword.streaminganalyticsshort}}-Service erstellt und bereitgestellt werden kann.

IBM Data Science Experience (DSX) unterstützt auch die Bereitstellung von Python-Anwendungen in interaktiven Jupyter-Notebooks. Weitere Informationen finden Sie in [Entwicklung von Python-Anwendungen für {{site.data.keyword.streaminganalyticsshort}}](/docs/services/StreamingAnalytics/t_develop_apps_python.html).
