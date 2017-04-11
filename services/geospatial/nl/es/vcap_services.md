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

#Información de entorno VCAP_SERVICES
{: #vcap_services}


La variable de entorno VCAP_SERVICES incluye información que es necesaria para utilizar la API REST de {{site.data.keyword.geospatialshort_Geospatial}}.{:shortdesc}

##Descripción
{: #vcap_description}

La variable de entorno VCAP_SERVICES incluye información similar al ejemplo siguiente:  

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

La variable de entorno VCAP_SERVICES incluye los siguientes elementos:

* key: El nombre del servicio {{site.data.keyword.geospatialshort_Geospatial}} [{{site.data.keyword.geospatialshort_Geospatial}}]. 
* name: El nombre de la instancia de servicio. 
* label: El nombre del servicio. 
* plan: El nombre del plan de servicio. 
* start_path: La vía de acceso que utiliza el método start de la API REST. 
* geo_host: El nombre de host del servidor {{site.data.keyword.geospatialshort_Geospatial}}.
* status_path: La vía de acceso que utiliza el método status de la API REST.
* remove_region_path: La vía de acceso que utiliza el método remove_region de la API REST.
* userid: El ID de usuario para la autenticación en el servidor {{site.data.keyword.geospatialshort_Geospatial}}.
* stop_path: La vía de acceso que utiliza el método stop de la API REST.
* dashboard_path: La vía de acceso que se utiliza para imprimir información en el panel de control.
* restart_path: La vía de acceso que utiliza el método restart de la API REST.
* geo_port: El número de puerto del servidor {{site.data.keyword.geospatialshort_Geospatial}}.
* password: La contraseña para la autenticación en el servidor {{site.data.keyword.geospatialshort_Geospatial}}.
* add_region_path: La vía de acceso que utiliza el método add_region de la API REST.


##Ejemplo: recuperación de información de la variable de entorno VCAP_SERVICES
{: #vcap_example}

El siguiente código Node.js recupera información del entorno del servicio:  

<pre><code>
var geo_props = {};

// Analizar VCAP_SERVICES si se ejecuta en Bluemix
if (process.env.VCAP_SERVICES)
{
var env = JSON.parse(process.env.VCAP_SERVICES);

// Depuración
for (var svcName in env) {
console.log(svcName);
	}
console.log(env);
// Buscar el servicio
if (env['Geospatial Analytics']) {
		geo_props = env['Geospatial Analytics'][0]['credentials'];
	}
	else {
console.log('Debe enlazar el servicio Geospatial Analytics a esta aplicación');
	}
} 
</code></pre>
