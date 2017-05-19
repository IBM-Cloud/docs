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

#Alta disponibilidad de {{site.data.keyword.streaminganalyticsshort}}
{: #c_ha}

{{site.data.keyword.streaminganalyticsshort}} permite una alta disponibilidad para las aplicaciones. Si se detecta un problema en uno de los nodos de la aplicación (recursos de {{site.data.keyword.streamsshort}}), el nodo se sustituye automáticamente y los trabajos que estén en ejecución en el nodo en cuestión se migran. Los trabajos solo se migran y se reinician si la instancia contiene varios nodos de aplicación. Puede redimensionar la instancia mediante el [panel de control de servicio](/docs/services/StreamingAnalytics/r_service_dashboard.html) o la [API REST de {{site.data.keyword.streaminganalyticsshort}}](https://console.ng.bluemix.net/apidocs/220){:new_window}.
{:shortdesc}
