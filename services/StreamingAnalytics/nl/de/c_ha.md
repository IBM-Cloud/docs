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

#{{site.data.keyword.streaminganalyticsshort}} für hohe Verfügbarkeit
{: #c_ha}

{{site.data.keyword.streaminganalyticsshort}} ermöglicht eine hohe Verfügbarkeit Ihrer Anwendungen. Wenn bei einem Ihrer Anwendungsknoten ({{site.data.keyword.streamsshort}}-Ressourcen) ein Problem festgestellt wird, wird der Knoten automatisch ersetzt und alle auf dem Knoten ausgeführten Jobs werden migriert. Jobs werden nur dann migriert und neu gestartet, wenn die Instanz mehrere Anwendungsknoten aufweist. Sie können die Größe der Instanz mithilfe des 	[Service-Dashboards](/docs/services/StreamingAnalytics/r_service_dashboard.html) oder der [{{site.data.keyword.streaminganalyticsshort}}-REST-API](https://console.ng.bluemix.net/apidocs/220){:new_window} ändern.
{:shortdesc}
