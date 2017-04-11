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

#Serviceberechtigungsnachweise und Umgebungsvariable VCAP_SERVICES
{: #vcap_services}

Die {{site.data.keyword.streaminganalyticsshort}}-Serviceberechtigungsnachweise und die Umgebungsvariable
VCAP_SERVICES enthalten die VCAP-Informationen, die zur Verwendung der {{site.data.keyword.streaminganalyticsshort}}-Service-REST-API
benötigt werden. Die VCAP-Informationen umfassen die REST-URL, die Serviceinstanz-ID, die Bindungs-ID und
die Berechtigungsnachweise für jede {{site.data.keyword.streaminganalyticsshort}}-Service-REST-API.  
{:shortdesc}


Der {{site.data.keyword.streaminganalyticsshort}}-Service zeigt das Verhalten und die Interaktion,
die für {{site.data.keyword.Bluemix_short}}-Services typisch sind. Wenn eine {{site.data.keyword.streaminganalyticsshort}}-Serviceinstanz eingerichtet und an eine {{site.data.keyword.Bluemix_short}}-Anwendung gebunden wird, stehen die Serviceinstanz-VCAP-Informationen der Bluemix-Anwendungsumgebung über die Umgebungsvariable VCAP_SERVICES zur Verfügung. Wenn eine {{site.data.keyword.streaminganalyticsshort}}-Serviceinstanz
ohne Angabe einer {{site.data.keyword.Bluemix_short}}-Anwendung eingerichtet wird,
an die die Instanz gebunden werden kann, werden die Serviceberechtigungsnachweise automatisch erstellt. Der Zugriff auf die {{site.data.keyword.streaminganalyticsshort}}-Serviceberechtigungsnachweise
ist über das Service-Dashboard möglich.


Das folgende Beispiel zeigt die Informationen, die in den
{{site.data.keyword.streaminganalyticsshort}}-Serviceberechtigungsnachweisen und
in der Umgebungsvariable VCAP_SERVICES enthalten sind:

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

Weitere Informationen zu der REST-API finden Sie in der [Dokumentation zur {{site.data.keyword.streaminganalyticsshort}}-REST-API](https://console.ng.bluemix.net/apidocs/220). 
