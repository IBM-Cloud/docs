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

# Service credentials and VCAP_SERVICES environment variable
{: #vcap_services}

The {{site.data.keyword.streaminganalyticsshort}} service credentials and VCAP_SERVICES environment variable includes the VCAP information that is required to use the {{site.data.keyword.streaminganalyticsshort}} service REST API. The VCAP information provides the REST URL, service instance ID, binding ID, and credentials for each {{site.data.keyword.streaminganalyticsshort}} service REST API.  
{:shortdesc}


The {{site.data.keyword.streaminganalyticsshort}} service follows the typical {{site.data.keyword.Bluemix_short}} service behavior and interaction. When a {{site.data.keyword.streaminganalyticsshort}} service instance is provisioned and bound to a {{site.data.keyword.Bluemix_short}} application, the service instance VCAP information is available to the Bluemix application environment via the VCAP_SERVICES environment variable. When a {{site.data.keyword.streaminganalyticsshort}} service instance is provisioned without specifying a {{site.data.keyword.Bluemix_short}} application to bind to, service credentials are automatically created. {{site.data.keyword.streaminganalyticsshort}} service credentials can be accessed from the service dashboard.


The {{site.data.keyword.streaminganalyticsshort}} service credentials and VCAP_SERVICES environment variable includes information as presented in the following example:

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

For more information about the REST API, see the  [{{site.data.keyword.streaminganalyticsshort}} REST API documentation](https://console.ng.bluemix.net/apidocs/220).
