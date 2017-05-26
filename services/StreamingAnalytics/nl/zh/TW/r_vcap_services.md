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

# 服務認證和 VCAP_SERVICES 環境變數
{: #vcap_services}

{{site.data.keyword.streaminganalyticsshort}} 服務認證和 VCAP_SERVICES 環境變數包括使用 {{site.data.keyword.streaminganalyticsshort}} 服務 REST API 所需的 VCAP 資訊。VCAP 資訊提供每一個 {{site.data.keyword.streaminganalyticsshort}} 服務 REST API 的 REST URL、服務實例 ID、連結 ID 和認證。  
{:shortdesc}


{{site.data.keyword.streaminganalyticsshort}} 服務遵循一般 {{site.data.keyword.Bluemix_short}} 服務行為和互動。佈建 {{site.data.keyword.streaminganalyticsshort}} 服務實例並將其連結至 {{site.data.keyword.Bluemix_short}} 應用程式時，可透過 VCAP_SERVICES 環境變數將服務實例 VCAP 資訊提供給 Bluemix 應用程式環境。佈建 {{site.data.keyword.streaminganalyticsshort}} 服務實例但未指定要連結的 {{site.data.keyword.Bluemix_short}} 應用程式時，會自動建立服務認證。您可以從服務儀表板存取 {{site.data.keyword.streaminganalyticsshort}} 服務認證。


{{site.data.keyword.streaminganalyticsshort}} 服務認證和 VCAP_SERVICES 環境變數包括下列範例中所呈現的資訊：

<pre><code>
{
"streaming-analytics": [
    {
"name": "NYCTrafficStreaming Analytics-t6",
"label": "streaming-analytics",
"plan": "Standard",
"credentials": {
"status_path": "/jax-rs/streams/status/service_instances/9e86b8e6-f606-4a1a-9800-26b96d2bc923/service_bindings/83c9d52e-3069-46bf-a1e3-655cf95fb627",
        "size_path": "/jax-rs/streams/size/service_instances/0fb17393-90eb-4066-96b6-df1ac9860743/service_bindings/b37b89df-b0d7-464e-b7d9-3db607a26550",
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

如需 REST API 的相關資訊，請參閱 [{{site.data.keyword.streaminganalyticsshort}} REST API 文件](https://console.ng.bluemix.net/apidocs/220)。
