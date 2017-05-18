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

#{{site.data.keyword.streaminganalyticsshort}} 高可用性
{: #c_ha}

{{site.data.keyword.streaminganalyticsshort}} 使得您的应用程序具有高可用性。
如果在其中一个应用程序节点（{{site.data.keyword.streamsshort}} 资源）上检测到问题，那么会自动替换该节点，且会迁移在该节点上运行的任何作业。
仅当实例包含多个应用程序节点时，才会迁移和重新启动作业。
您可以使用[服务仪表板](/docs/services/StreamingAnalytics/r_service_dashboard.html)或 [{{site.data.keyword.streaminganalyticsshort}}REST API](https://console.ng.bluemix.net/apidocs/220){:new_window} 来调整实例的大小。
{:shortdesc}
