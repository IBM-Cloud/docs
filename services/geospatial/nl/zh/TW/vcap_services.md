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

#VCAP_SERVICES 環境資訊
{: #vcap_services}


VCAP_SERVICES 環境變數包括使用 {{site.data.keyword.geospatialshort_Geospatial}} REST API 所需的資訊。
{:shortdesc}

##說明
{: #vcap_description}

VCAP_SERVICES 環境變數包括與下列範例類似的資訊： 

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

VCAP_SERVICES 環境變數包括下列項目：

* key：{{site.data.keyword.geospatialshort_Geospatial}} 服務的名稱 [{{site.data.keyword.geospatialshort_Geospatial}}]。 
* name：服務實例的名稱。 
* label：服務的名稱。 
* plan：服務方案的名稱。 
* start_path：REST API 的 start 方法所使用的路徑。 
* geo_host：{{site.data.keyword.geospatialshort_Geospatial}} 伺服器的主機名稱。
* status_path：REST API 的 status 方法所使用的路徑。
* remove_region_path：REST API 的 remove_region 方法所使用的路徑。
* userid：向 {{site.data.keyword.geospatialshort_Geospatial}} 伺服器鑑別用的使用者 ID。
* stop_path：REST API 的 stop 方法所使用的路徑。
* dashboard_path：用來將資訊列印至儀表板的路徑。
* restart_path：REST API 的 restart 方法所使用的路徑。
* geo_port：{{site.data.keyword.geospatialshort_Geospatial}} 伺服器的埠號。
* password：向 {{site.data.keyword.geospatialshort_Geospatial}} 伺服器鑑別用的密碼。
* add_region_path：REST API 的 add_region 方法所使用的路徑。


##範例：擷取 VCAP_SERVICES 環境變數資訊
{: #vcap_example}

下列 Node.js 程式碼會擷取服務環境資訊： 

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
