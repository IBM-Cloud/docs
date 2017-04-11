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

#服务凭证和 VCAP_SERVICES 环境变量
{: #vcap_services}

{{site.data.keyword.streaminganalyticsshort}} 服务凭证和 VCAP_SERVICES 环境变量包括使用 {{site.data.keyword.streaminganalyticsshort}} 服务 REST API 所需的 VCAP 信息。VCAP 信息为每一个 {{site.data.keyword.streaminganalyticsshort}} 服务 REST API 提供 REST URL、服务实例标识、绑定标识和凭证。  
{:shortdesc}


{{site.data.keyword.streaminganalyticsshort}} 服务遵循典型 {{site.data.keyword.Bluemix_short}} 服务行为和交互。
当 {{site.data.keyword.streaminganalyticsshort}} 服务实例供应并绑定到 {{site.data.keyword.Bluemix_short}} 应用程序时，Bluemix 应用程序环境可通过 VCAP_SERVICES 环境变量，使用服务实例 VCAP 信息。当未指定要绑定到的 {{site.data.keyword.Bluemix_short}} 应用程序即供应 {{site.data.keyword.streaminganalyticsshort}} 服务实例时，会自动创建服务凭证。从服务仪表板可访问 {{site.data.keyword.streaminganalyticsshort}} 服务凭证。



{{site.data.keyword.streaminganalyticsshort}} 服务凭证和 VCAP_SERVICES 环境变量包括以下示例中所呈现的信息：

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

有关 REST API 的更多信息，请参阅 [{{site.data.keyword.streaminganalyticsshort}} REST API 文档](https://console.ng.bluemix.net/apidocs/220)。 
