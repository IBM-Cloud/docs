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

#Credenziali del servizio e variabile di ambiente VCAP_SERVICES
{: #vcap_services}

Le credenziali del servizio {{site.data.keyword.streaminganalyticsshort}}
e la variabile di ambiente VCAP_SERVICES includono le informazioni VCAP
necessarie per utilizzare l'API REST del
servizio {{site.data.keyword.streaminganalyticsshort}}. Le informazioni VCAP forniscono l'URL REST,
l'ID dell'istanza del servizio, l'ID di bind e le credenziali per ogni
API REST del servizio {{site.data.keyword.streaminganalyticsshort}}.  
{:shortdesc}


Il servizio {{site.data.keyword.streaminganalyticsshort}}
segue il tipico comportamento e interazione del
servizio {{site.data.keyword.Bluemix_short}}. Quando un'istanza del servizio {{site.data.keyword.streaminganalyticsshort}} viene fornita e associata a un'applicazione {{site.data.keyword.Bluemix_short}}, le informazioni VCAP dell'istanza del servizio sono disponibili nell'ambiente dell'applicazione Bluemix tramite la variabile di ambiente VCAP_SERVICES. Quando un'istanza del servizio {{site.data.keyword.streaminganalyticsshort}}
viene fornita senza specificare un'applicazione {{site.data.keyword.Bluemix_short}} a cui eseguire il binding, le credenziali del servizio vengono create automaticamente. È possibile accedere alle credenziali del servizio {{site.data.keyword.streaminganalyticsshort}}
dal dashboard del servizio.


Le credenziali del servizio {{site.data.keyword.streaminganalyticsshort}}
e la variabile di ambiente VCAP_SERVICES includono informazioni come sono presentate nel seguente esempio:

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

Per ulteriori informazioni sull'API REST, vedi la [Documentazione API REST {{site.data.keyword.streaminganalyticsshort}}](https://console.ng.bluemix.net/apidocs/220). 
