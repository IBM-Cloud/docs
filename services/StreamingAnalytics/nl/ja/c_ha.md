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

#{{site.data.keyword.streaminganalyticsshort}} の高可用性
{: #c_ha}

{{site.data.keyword.streaminganalyticsshort}} では、アプリケーションの高可用性を実現します。いずれかのアプリケーション・ノード ({{site.data.keyword.streamsshort}} リ
ソース) で問題が発生すると、そのノードは自動的に置き換えられ、そのノードで実行されていたジ
ョブはすべてマイグレーションされます。インスタンスに複数のアプリケーション・ノードが含まれている場合、ジョブはマイグレーションされ、再開されるだけです。インスタンスは、[サービス・ダッシュボード](/docs/services/StreamingAnalytics/r_service_dashboard.html)または [{{site.data.keyword.streaminganalyticsshort}} REST
API](https://console.ng.bluemix.net/apidocs/220){:new_window} を使用してサイズ変更できます。
{:shortdesc}
