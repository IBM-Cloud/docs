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

#VCAP_SERVICES 环境信息
{: #vcap_services}


VCAP_SERVICES 环境变量包含使用 {{site.data.keyword.geospatialshort_Geospatial}} REST API 所需的信息。
{:shortdesc}

##描述
{: #vcap_description}

VCAP_SERVICES 环境变量包含类似以下示例的信息： 

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

VCAP_SERVICES 环境变量包含以下项：

* key：{{site.data.keyword.geospatialshort_Geospatial}} 服务 [{{site.data.keyword.geospatialshort_Geospatial}}] 的名称。 
* name：服务实例的名称。 
* label：服务的名称。 
* plan：服务套餐的名称。 
* start_path：REST API 的 start 方法使用的路径。 
* geo_host：{{site.data.keyword.geospatialshort_Geospatial}} 服务器的主机名。
* status_path：REST API 的 status 方法使用的路径。
* remove_region_path：REST API 的 remove_region 方法使用的路径。
* userid：用于对 {{site.data.keyword.geospatialshort_Geospatial}} 服务器进行认证的用户标识。
* stop_path：REST API 的 stop 方法使用的路径。
* dashboard_path：用于将信息打印到仪表板的路径。
* restart_path：REST API 的 restart 方法使用的路径。
* geo_port：{{site.data.keyword.geospatialshort_Geospatial}} 服务器的端口号。
* password：用于对 {{site.data.keyword.geospatialshort_Geospatial}} 服务器进行认证的密码。
* add_region_path：REST API 的 add_region 方法使用的路径。


##示例：检索 VCAP_SERVICES 环境变量信息
{: #vcap_example}

以下 Node.js 代码检索服务环境信息： 

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
