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

#서비스 신임 정보 및 VCAP_SERVICES 환경 변수
{: #vcap_services}

{{site.data.keyword.streaminganalyticsshort}}
서비스 신임 정보 및 VCAP_SERVICES 환경 변수는 {{site.data.keyword.streaminganalyticsshort}} 서비스 REST API를 사용하기 위해 필요한 VCAP 정보를 포함합니다. VCAP 정보는 각 {{site.data.keyword.streaminganalyticsshort}} 서비스 REST API에 대한 신임 정보, 바인딩 ID, 서비스 인스턴스 ID, REST URL을 제공합니다.   
{:shortdesc}


{{site.data.keyword.streaminganalyticsshort}} 서비스는 일반적인 {{site.data.keyword.Bluemix_short}} 서비스 동작과 상호작용을 따릅니다. {{site.data.keyword.streaminganalyticsshort}} 서비스 인스턴스가 프로비저닝되고 {{site.data.keyword.Bluemix_short}} 애플리케이션에 바인드되면, 서비스 인스턴스 VCAP 정보가 VCAP_SERVICES 환경 변수를 통해 Bluemix 애플리케이션 환경에서 사용 가능해집니다. {{site.data.keyword.streaminganalyticsshort}} 서비스 인스턴스가 바인드할 대상인 {{site.data.keyword.Bluemix_short}} 애플리케이션을 지정하지 않고 프로비저닝되면 서비스 신임 정보가 자동으로 작성됩니다.{{site.data.keyword.streaminganalyticsshort}} 서비스 신임 정보는 서비스 대시보드에서 액세스할 수 있습니다.


{{site.data.keyword.streaminganalyticsshort}} 서비스 신임 정보와 VCAP_SERVICES 환경 변수는 다음 예제에서 제공되는 정보를 포함합니다. 

<pre><code>
{
"streaming-analytics": [
    {
"name": "NYCTrafficStreaming Analytics-t6",
"label": "streaming-analytics",
"plan": "Standard",
"credentials": {
"status_path": "/jax-rs/streams/status/service_instances/9e86b8e6-f606-4a1a-9800-26b96d2bc923/service_bindings/83c9d52e-3069-46bf-a1e3-655cf95fb627",
"start_path": "/jax-rs/streams/start/service_instances/9e86b8e6-f606-4a1a-9800-26b96d2bc923/service_bindings/83c9d52e-3069-46bf-a1e3-655cf95fb627",
"stop_path": "/jax-rs/streams/stop/service_instances/9e86b8e6-f606-4a1a-9800-26b96d2bc923/service_bindings/83c9d52e-3069-46bf-a1e3-655cf95fb627",
"resources_path": "/jax-rs/resources/service_instances/9e86b8e6-f606-4a1a-9800-26b96d2bc923/service_bindings/83c9d52e-3069-46bf-a1e3-655cf95fb627",
"jobs_path": "/jax-rs/jobs/service_instances/9e86b8e6-f606-4a1a-9800-26b96d2bc923/service_bindings/83c9d52e-3069-46bf-a1e3-655cf95fb627",
"rest_host": "streams-app-service.ng.bluemix.net",
"rest_port": "443",
"rest_url": "https://streams-app-service.ng.bluemix.net",
"userid": "xxx",
"password": "yyy"
      }
    }
  ]
}	  
</code></pre>

REST API에 대한 자세한 정보는 [{{site.data.keyword.streaminganalyticsshort}} REST API 문서](https://console.ng.bluemix.net/apidocs/220)를 참조하십시오. 
