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

#{{site.data.keyword.streamsshort}}-Anwendungen für die Cloud bereitstellen
{: #t_deploytocloud}

Sie können Ihre {{site.data.keyword.streamsshort}}-Anwendungen
für eine {{site.data.keyword.streaminganalyticsshort}}-Instanz bereitstellen, die in der
{{site.data.keyword.Bluemix_short}}-Cloud ausgeführt wird.
{:shortdesc}

{{site.data.keyword.streamsshort}}-Anwendungen werden in einer {{site.data.keyword.streamsshort}}-Umgebung in SPL ({{site.data.keyword.streamsshort}} Processing Language) geschrieben. {{site.data.keyword.streamsshort}} unterstützt auch verschiedene Java™-Entwicklungskits, die Sie zur Entwicklung Ihrer Anwendungen verwenden können. Weitere Informationen zur Java-Unterstützung in {{site.data.keyword.streamsshort}} finden Sie unter [Supported Java development kits for application development](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-prerequisites-java-supported-sdks.html){:new_window}.
{{site.data.keyword.streaminganalyticsshort}} enthält keine {{site.data.keyword.streamsshort}}-Entwicklungsumgebung in der Cloud, aber Sie können die Anwendungen, die Sie entwickeln, lokal für die Cloud bereitstellen.

Bevor Sie mit der Arbeit beginnen, müssen Sie den Popup-Blocker Ihres Browsers inaktivieren, um die Streaming Analytics-Konsole anzuzeigen.

Gehen Sie wie folgt vor, um Ihre {{site.data.keyword.streamsshort}}-Anwendungen für die Cloud bereitzustellen:

1. Richten Sie eine {{site.data.keyword.streamsshort}}-Umgebung ein, um Ihre Anwendung zu entwickeln und zu testen. 

	Wenn Sie nicht über eine {{site.data.keyword.streamsshort}}-Umgebung verfügen, können Sie {{site.data.keyword.streamsshort}} Quick Start Edition kostenlos herunterladen. Rufen Sie die [Produktseite von IBM Streams](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window} auf und klicken Sie auf **Download the native software installation**.

2. Entwickeln Sie Ihre SPL- oder Java-Anwendung in Ihrer {{site.data.keyword.streamsshort}}-Umgebung und verwenden Sie dazu Streams Studio oder die Befehlszeilentools.
3. Stellen Sie sicher, dass Ihre SPL- oder Java-Anwendung in Ihrer Entwicklungsumgebung ordnungsgemäß ausgeführt wird.
4. Übergeben Sie das Anwendungsbundle (die Datei mit der Erweiterung .sab), die Ihrer SPL- oder Java-Anwendung zugeordnet ist, an Ihre Serviceinstanz in der Cloud. Verwenden Sie dazu eine der folgenden Methoden:
	* Verwenden Sie die {{site.data.keyword.streaminganalyticsshort}}-Konsole, um das Anwendungsbundle zu übergeben.
    * Entwickeln Sie eine {{site.data.keyword.Bluemix_short}}-Anwendung
und fügen Sie ihr die {{site.data.keyword.streamsshort}}-Anwendung hinzu. Steuern Sie sie unter Verwendung der {{site.data.keyword.streaminganalyticsshort}}-REST-API.

Ihre Anwendung wurde jetzt in der Cloud bereitgestellt. Sie können Ihre Anwendung überwachen, indem Sie den {{site.data.keyword.streaminganalyticsshort}}-Service verwenden. Sie haben auch die Möglichkeit, mehr als eine SPL- oder Java-Anwendung (Dateien mit der Erweiterung .sab) an Ihre Serviceinstanz zu übergeben. Dies können beliebig viele sein.
