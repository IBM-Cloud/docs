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

#Informazioni di ambiente VCAP_SERVICES
{: #vcap_services}


La variabile di ambiente VCAP_SERVICES include informazioni
richieste per l'utilizzo dell'API REST
{{site.data.keyword.geospatialshort_Geospatial}}.
{:shortdesc}

##Descrizione
{: #vcap_description}

La
variabile di ambiente VCAP_SERVICES include informazioni simili al
seguente esempio: 

<pre><code>
"Geospatial Analytics": {
    "name": "Geospatial Analytics-g1",
    "label": "Geospatial Analytics",
    "plan": "Standard",
    "credentials": {
      "start_path": "/jax-rs/geo/start/service_instances/684a4ede-d142-4a55-93b5-68b80d8ee33d/service_bindings/e49ed552-9201-4ed7-b850-5eeaadd3859b",
      "geo_host": "streams-broker.ng.bluemix.net",
      "status_path": "/jax-rs/geo/status/service_instances/684a4ede-d142-4a55-93b5-68b80d8ee33d/service_bindings/e49ed552-9201-4ed7-b850-5eeaadd3859b",
      "remove_region_path": "/jax-rs/geo/removeRegion/service_instances/684a4ede-d142-4a55-93b5-68b80d8ee33d/service_bindings/e49ed552-9201-4ed7-b850-5eeaadd3859b",
      "userid": "**********************",
      "stop_path": "/jax-rs/geo/stop/service_instances/684a4ede-d142-4a55-93b5-68b80d8ee33d/service_bindings/e49ed552-9201-4ed7-b850-5eeaadd3859b",
      "dashboard_path": "/jax-rs/dashboard/684a4ede-d142-4a55-93b5-68b80d8ee33d",
      "restart_path": "/jax-rs/geo/restart/service_instances/684a4ede-d142-4a55-93b5-68b80d8ee33d/service_bindings/e49ed552-9201-4ed7-b850-5eeaadd3859b",
      "geo_port": 443,
      "password": "**********************",
      "add_region_path": "/jax-rs/geo/addRegion/service_instances/684a4ede-d142-4a55-93b5-68b80d8ee33d/service_bindings/e49ed552-9201-4ed7-b850-5eeaadd3859b"
    }
  }
</code></pre>

La variabile di ambiente  VCAP_SERVICES include
i seguenti elementi:

* key: il nome del servizio {{site.data.keyword.geospatialshort_Geospatial}} [{{site.data.keyword.geospatialshort_Geospatial}}]. 
* name: il nome dell'istanza del servizio. 
* label: il nome del servizio. 
* plan: il nome del piano di servizio. 
* start_path: il percorso utilizzato dal metodo start dell'API REST. 
* geo_host: il nome host del server {{site.data.keyword.geospatialshort_Geospatial}}.
* status_path: il percorso utilizzato dal metodo status dell'API REST.
* remove_region_path: il percorso utilizzato dal metodo remove_region dell'API REST.
* userid: l'ID utente per l'autenticazione al server {{site.data.keyword.geospatialshort_Geospatial}}.
* stop_path: il percorso utilizzato dal metodo stop dell'API REST.
* dashboard_path: l percorso utilizzato per stampare le informazioni nel dashboard.
* restart_path: il percorso utilizzato dal metodo restart dell'API REST.
* geo_port: il numero di porta del server {{site.data.keyword.geospatialshort_Geospatial}}
* password: la password per l'autenticazione al server {{site.data.keyword.geospatialshort_Geospatial}}.
* add_region_path: l percorso utilizzato dal metodo add_region dell'API REST.


##Esempio: richiamo di informazioni della variabile di ambiente
VCAP_SERVICES
{: #vcap_example}

Il seguente codice Node.js
richiama le informazioni sull'ambiente del servizio: 

<pre><code>
var geo_props = {};

// Parse VCAP_SERVICES if running in Bluemix
if (process.env.VCAP_SERVICES)
{
	var env = JSON.parse(process.env.VCAP_SERVICES);

	// Debugging
	for (var svcName in env) {
		console.log(svcName);
	}
	console.log(env);
	// Find the service
	if (env['Geospatial Analytics']) {
		geo_props = env['Geospatial Analytics'][0]['credentials'];
	}
	else {
		console.log('You must bind the Geospatial Analytics service to this application');
	}
} 
</code></pre>
