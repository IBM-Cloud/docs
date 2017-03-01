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

#Haute disponibilité {{site.data.keyword.streaminganalyticsshort}}
{: #c_ha}

{{site.data.keyword.streaminganalyticsshort}} permet une haute disponibilité dans vos applications. Si un problème est détecté sur l'un de vos noeuds d'application (ressources {{site.data.keyword.streamsshort}}), le noeud est automatiquement remplacé et tous les noeuds s'exécutant sur ce noeud sont migrés. Les travaux ne sont migrés et redémarrés que si l'instance comporte des noeuds d'applications multiples. Vous pouvez redimensionner l'instance en utilisant le [tableau de bord du service](/docs/services/StreamingAnalytics/r_service_dashboard.html) ou l'[API REST {{site.data.keyword.streaminganalyticsshort}}](https://console.ng.bluemix.net/apidocs/220){:new_window}.
{:shortdesc}
