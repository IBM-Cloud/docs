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

#Informações sobre o ambiente VCAP_SERVICES
{: #vcap_services}


A variável de ambiente VCAP_SERVICES inclui informações que são necessárias para
usar a API REST do {{site.data.keyword.geospatialshort_Geospatial}}.
{:shortdesc}

##Descrição
{: #vcap_description}

A variável de
ambiente VCAP_SERVICES inclui informações semelhantes ao exemplo a seguir: 

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

A variável de ambiente VCAP_SERVICES inclui os itens a seguir:

* key: o nome do serviço {{site.data.keyword.geospatialshort_Geospatial}} [{{site.data.keyword.geospatialshort_Geospatial}}]. 
* name: o nome da instância de serviço. 
* label: o nome do serviço. 
* plan: o nome do plano de serviço. 
* start_path: o caminho que é usado pelo método de início da API de REST. 
* geo_host: o nome do host do servidor {{site.data.keyword.geospatialshort_Geospatial}}.
* status_path: o caminho que é usado pelo método de status da API de REST.
* remove_region_path: o caminho que é usado pelo método remove_region da API de REST.
* userid: o ID do usuário para autenticação no servidor do {{site.data.keyword.geospatialshort_Geospatial}}.
* stop_path: o caminho que é usado pelo método de parada da API de REST.
* dashboard_path: o caminho que é usado para imprimir informações no painel.
* restart_path: o caminho que é usado pelo método de reinício da API de REST.
* geo_port: o número da porta do servidor do {{site.data.keyword.geospatialshort_Geospatial}}
* password: a senha para autenticação no servidor do {{site.data.keyword.geospatialshort_Geospatial}}.
* add_region_path: o caminho que é usado pelo método add_region da API de REST.


##Exemplo: Recuperando informações da variável de ambiente VCAP_SERVICES
{: #vcap_example}

O código Node.js a seguir
recupera as informações do ambiente de serviço: 

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
