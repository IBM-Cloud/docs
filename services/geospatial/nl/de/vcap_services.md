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

#Umgebungsinformationen in VCAP_SERVICES
{: #vcap_services}


Die Umgebungsvariable VCAP_SERVICES enthält Informationen, die für die Verwendung der REST-API von {{site.data.keyword.geospatialshort_Geospatial}} erforderlich sind.
{:shortdesc}

##Beschreibung
{: #vcap_description}

Die Umgebungsvariable VCAP_SERVICES enthält Informationen, die den Informationen im folgenden Beispiel ähneln: 

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

Die Umgebungsvariable VCAP_SERVICES enthält die folgenden Elemente:

* key: Der Name des {{site.data.keyword.geospatialshort_Geospatial}}-Service [{{site.data.keyword.geospatialshort_Geospatial}}]. 
* name: Der Name der Serviceinstanz. 
* plan: Der Name des Service. 
* plan: Der Name des Serviceplans. 
* start_path: Der Pfad, der von der Methode 'start' der REST-API verwendet wird. 
* geo_host: Der Hostname des {{site.data.keyword.geospatialshort_Geospatial}}-Servers.
* status_path: Der Pfad, der von der Methode 'status' der REST-API verwendet wird.
* remove_region_path: Der Pfad, der von der Methode 'remove_region' der REST-API verwendet wird.
* userid: Die Benutzer-ID für die Authentifizierung beim {{site.data.keyword.geospatialshort_Geospatial}}-Server.
* stop_path: Der Pfad, der von der Methode 'stop' der REST-API verwendet wird.
* dashboard_path: Der Pfad, der zum Ausgeben von Informationen an das Dashboard verwendet wird.
* restart_path: Der Pfad, der von der Methode 'restart' der REST-API verwendet wird.
* geo_port: Die Portnummer des {{site.data.keyword.geospatialshort_Geospatial}}-Servers
* password: Das Kennwort für die Authentifizierung beim {{site.data.keyword.geospatialshort_Geospatial}}-Server.
* add_region_path: Der Pfad, der von der Methode 'add_region' der REST-API verwendet wird.


##Beispiel: Abrufen der Informationen aus der Umgebungsvariablen VCAP_SERVICES
{: #vcap_example}

Vom folgenden Node.js-Code werden Informationen zur Serviceumgebung abgerufen. 

<pre><code>
var geo_props = {};

// Analysieren von VCAP_SERVICES bei Ausführung in Bluemix
if (process.env.VCAP_SERVICES)
{
	var env = JSON.parse(process.env.VCAP_SERVICES);

	// Debugging
	for (var svcName in env) {
		console.log(svcName);
	}
	console.log(env);
	// Suchen des Service
	if (env['Geospatial Analytics']) {
		geo_props = env['Geospatial Analytics'][0]['credentials'];
	}
	else {
 console.log('You must bind the Geospatial Analytics service to this application');
	}
} 
</code></pre>
