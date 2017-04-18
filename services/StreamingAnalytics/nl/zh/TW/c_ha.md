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

# {{site.data.keyword.streaminganalyticsshort}} 高可用性
{: #c_ha}

{{site.data.keyword.streaminganalyticsshort}} 可啟用您應用程式的高可用性。如果在其中一個應用程式節點（{{site.data.keyword.streamsshort}} 資源）上偵測到問題，則會自動更換該節點，並移轉在該節點上執行的任何工作。如果實例包含多個應用程式節點，則只會移轉及重新啟動工作。您可以使用[服務儀表板](/docs/services/StreamingAnalytics/r_service_dashboard.html)或 [{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220){:new_window} 來調整實例大小。
{:shortdesc}
