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

#Alta disponibilidade do {{site.data.keyword.streaminganalyticsshort}}
{: #c_ha}

O {{site.data.keyword.streaminganalyticsshort}} permite alta disponibilidade para seus aplicativos. Se for detectado um problema em um de seus nós do aplicativo (recursos do {{site.data.keyword.streamsshort}}), o nó será substituído automaticamente e qualquer tarefa em execução nesse nó será migrada. As tarefas serão migradas e reiniciadas somente se a instância contiver múltiplos nós de aplicativo. É possível redimensionar a instância usando o [painel de serviço](/docs/services/StreamingAnalytics/r_service_dashboard.html) ou a [ API de REST do {{site.data.keyword.streaminganalyticsshort}}](https://console.ng.bluemix.net/apidocs/220){:new_window}.
{:shortdesc}
