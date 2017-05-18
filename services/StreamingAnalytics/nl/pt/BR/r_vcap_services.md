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

# Credenciais de serviço e a variável de ambiente VCAP_SERVICES
{: #vcap_services}

As credenciais de serviço e a variável de ambiente VCAP_SERVICES do {{site.data.keyword.streaminganalyticsshort}} incluem as informações de VCAP que são
necessárias para usar a API REST do serviço {{site.data.keyword.streaminganalyticsshort}}. As informações de VCAP fornecem a URL REST, o ID da instância de
serviço, o ID de ligação e as credenciais de cada API REST do serviço {{site.data.keyword.streaminganalyticsshort}}.  
{:shortdesc}


O serviço {{site.data.keyword.streaminganalyticsshort}} segue o comportamento e a interação de serviço típicos do
{{site.data.keyword.Bluemix_short}}. Quando uma instância de serviço do {{site.data.keyword.streaminganalyticsshort}} for
provisionada e ligada a um aplicativo {{site.data.keyword.Bluemix_short}}, as informações de VCAP da instância de serviço ficarão disponíveis para o ambiente de
aplicativo do Bluemix por meio da variável de ambiente VCAP_SERVICES. Quando uma instância de serviço do {{site.data.keyword.streaminganalyticsshort}} for
provisionada sem especificar um aplicativo {{site.data.keyword.Bluemix_short}} ao qual ligar, as credenciais de serviço serão criadas automaticamente. As
credenciais de serviço do {{site.data.keyword.streaminganalyticsshort}} podem ser acessadas por meio do painel de serviços.


As credenciais de serviço e a variável de ambiente VCAP_SERVICES do {{site.data.keyword.streaminganalyticsshort}} incluem informações, conforme
apresentado no exemplo a seguir:

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

Para obter mais informações sobre a API de REST, veja a documentação da API de REST do
[{{site.data.keyword.streaminganalyticsshort}}](https://console.ng.bluemix.net/apidocs/220).
