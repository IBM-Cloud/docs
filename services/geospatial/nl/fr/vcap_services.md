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

#Information d'environnement VCAP_SERVICES
{: #vcap_services}


La variable d'environnement VCAP_SERVICES contient des informations requises pour l'utilisation de l'API REST {{site.data.keyword.geospatialshort_Geospatial}}.
{:shortdesc}

##Description
{: #vcap_description}

La variable d'environnement VCAP_SERVICES contient des informations similaires à l'exemple
suivant : 

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

La variable d'environnement VCAP_SERVICES inclut les éléments suivants :

* key: nom du service {{site.data.keyword.geospatialshort_Geospatial}} [{{site.data.keyword.geospatialshort_Geospatial}}]. 
* name: nom de l'instance de service.  
* label: nom du service. 
* plan: nom du plan de service. 
* start_path: chemin utilisé par la méthode start de l'API REST.  
* geo_host: nom d'hôte du serveur {{site.data.keyword.geospatialshort_Geospatial}}. 
* status_path: chemin utilisé par la méthode status de l'API REST. 
* remove_region_path: chemin utilisé par la méthode remove_region de l'API REST.
* userid: ID utilisateur pour l'authentification auprès du serveur {{site.data.keyword.geospatialshort_Geospatial}}. 
* stop_path: chemin utilisé par la méthode stop de l'API REST. 
* dashboard_path: chemin utilisé pour imprimer des informations sur le tableau de bord.
* restart_path: chemin utilisé par la méthode restart de l'API REST. 
* geo_port: numéro de port du serveur {{site.data.keyword.geospatialshort_Geospatial}}.
* password: mot de passe pour l'authentification auprès du serveur {{site.data.keyword.geospatialshort_Geospatial}}.
* add_region_path: chemin utilisé par la méthode add_region de l'API REST.


##Exemple : Extraction des informations de la variable d'environnement VCAP_SERVICES
{: #vcap_example}

Le code Node.js suivant extrait les informations d'environnement de service : 

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
