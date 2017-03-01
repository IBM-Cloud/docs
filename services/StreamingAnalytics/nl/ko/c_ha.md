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

#{{site.data.keyword.streaminganalyticsshort}} 고가용성
{: #c_ha}

{{site.data.keyword.streaminganalyticsshort}}는 애플리케이션의
고가용성을 사용 가능하게 합니다. 애플리케이션 노드({{site.data.keyword.streamsshort}} 리소스) 중 하나에서 문제가 발견되면 노드가
자동으로 대체되고 해당 노드에서 실행 중인 작업은 마이그레이션됩니다. 인스턴스에 여러 애플리케이션 노드가 있는 경우에만 작업이 마이그레이션 및 재시작됩니다. [서비스 대시보드](/docs/services/StreamingAnalytics/r_service_dashboard.html) 또는 [{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220){:new_window}를 사용하여 인스턴스의 크기를 조정할 수 있습니다.
{:shortdesc}
