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

#{{site.data.keyword.streaminganalyticsshort}}
alta disponibilità
{: #c_ha}

{{site.data.keyword.streaminganalyticsshort}} abilita
l'alta disponibilità per le tue applicazioni. Se viene rilevato un problema su uno dei nodi della tua applicazione,
(risorse {{site.data.keyword.streamsshort}}), il nodo viene
automaticamente sostituito e ogni lavoro in esecuzione su tale nodo viene migrato. I lavori vengono migrati e riavviati
solo se l'istanza contiene più nodi di applicazione. Puoi ridimensionare l'istanza utilizzando il [dashboard del servizio](/docs/services/StreamingAnalytics/r_service_dashboard.html) o l'[API REST {{site.data.keyword.streaminganalyticsshort}}](https://console.ng.bluemix.net/apidocs/220){:new_window}.
{:shortdesc}
