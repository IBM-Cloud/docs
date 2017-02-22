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

#VCAP_SERVICES environment information
{: #vcap_services}


The VCAP_SERVICES environment variable includes information that is required to use the {{site.data.keyword.geospatialshort_Geospatial}} REST API.
{:shortdesc}

##Description
{: #vcap_description}

The VCAP_SERVICES environment variable includes information similar to the following example: 

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

The VCAP_SERVICES environment variable includes the following items:

* key: The name of the {{site.data.keyword.geospatialshort_Geospatial}} service [{{site.data.keyword.geospatialshort_Geospatial}}]. 
* name: The name of the service instance. 
* label: The name of the service. 
* plan: The name of the service plan. 
* start_path: The path that is used by the start method of the REST API. 
* geo_host: The host name of the {{site.data.keyword.geospatialshort_Geospatial}} server.
* status_path: The path that is used by the status method of the REST API.
* remove_region_path: The path that is used by the remove_region method of the REST API.
* userid: The user ID for authentication to the {{site.data.keyword.geospatialshort_Geospatial}} server.
* stop_path: The path that is used by the stop method of the REST API.
* dashboard_path: The path that is used to print information to the dashboard.
* restart_path: The path that is used by the restart method of the REST API.
* geo_port: The port number of the {{site.data.keyword.geospatialshort_Geospatial}} server
* password: The password for authentication to the {{site.data.keyword.geospatialshort_Geospatial}} server.
* add_region_path: The path that is used by the add_region method of the REST API.


##Example: Retrieving VCAP_SERVICES environment variable information
{: #vcap_example}

The following Node.js code retrieves the service environment information: 

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
