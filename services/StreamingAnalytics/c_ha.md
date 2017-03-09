---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-09"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#{{site.data.keyword.streaminganalyticsshort}} high availability
{: #c_ha}

{{site.data.keyword.streaminganalyticsshort}} enables high availability for your applications. If an issue is detected on one of your application nodes ({{site.data.keyword.streamsshort}} resources), the node is automatically replaced and any jobs running on that node are migrated. Jobs are only migrated and restarted if the instance contains multiple application nodes. You can resize the instance by using the [service dashboard](/docs/services/StreamingAnalytics/r_service_dashboard.html) or the [{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220){:new_window}.
{:shortdesc}
