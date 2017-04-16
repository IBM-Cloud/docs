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

# Données d'identification de service et variable d'environnement VCAP_SERVICES
{: #vcap_services}

Les données d'identification de service {{site.data.keyword.streaminganalyticsshort}} et la variable d'environnement VCAP_SERVICES incluent les informations VCAP qui sont requises pour utiliser l'API REST de service {{site.data.keyword.streaminganalyticsshort}}. Les informations VCAP fournissent l'URL REST, l'ID instance de service, l'ID liaison et les données d'identification pour chaque API REST de service {{site.data.keyword.streaminganalyticsshort}}.  
{:shortdesc}


Le service {{site.data.keyword.streaminganalyticsshort}} suit le comportement et les interactions de service {{site.data.keyword.Bluemix_short}} typiques. Quand une instance de service {{site.data.keyword.streaminganalyticsshort}} est provisionnée et liée à une application {{site.data.keyword.Bluemix_short}}, les informations VCAP d'instance de service sont disponibles dans l'environnement d'application Bluemix via la variable d'environnement VCAP_SERVICES. Quand une instance de service {{site.data.keyword.streaminganalyticsshort}} est provisionnée sans spécification d'une application {{site.data.keyword.Bluemix_short}} à laquelle se lier, les données d'authentification de service sont automatiquement créées. Les données d'authentification de service {{site.data.keyword.streaminganalyticsshort}} sont accessibles depuis le tableau de bord de service.


Les données d'identification de service {{site.data.keyword.streaminganalyticsshort}} et la variable d'environnement VCAP_SERVICES incluent des informations, comme celles présentées dans l'exemple suivant :

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

Pour plus d'informations sur l'API REST, voir la [documentation sur les API REST {{site.data.keyword.streaminganalyticsshort}}](https://console.ng.bluemix.net/apidocs/220). 
