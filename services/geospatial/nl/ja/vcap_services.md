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

#VCAP_SERVICES 環境情報
{: #vcap_services}


VCAP_SERVICES 環境変数には、{{site.data.keyword.geospatialshort_Geospatial}} REST API を使用するために必要な情報が含まれています。
{:shortdesc}

##説明
{: #vcap_description}

VCAP_SERVICES 環境変数には、以下の例のような情報が含まれています。 

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

VCAP_SERVICES 環境変数には、以下の項目が含まれています。

* key: {{site.data.keyword.geospatialshort_Geospatial}} サービスの名前 [{{site.data.keyword.geospatialshort_Geospatial}}]。 
* name: サービス・インスタンスの名前。 
* label: サービスの名前。 
* plan: サービス・プランの名前。 
* start_path: REST API の start メソッドで使用されるパス。 
* geo_host: {{site.data.keyword.geospatialshort_Geospatial}} サーバーのホスト名。
* status_path: REST API の status メソッドで使用されるパス。
* remove_region_path: REST API の remove_region メソッドで使用されるパス。
* userid: {{site.data.keyword.geospatialshort_Geospatial}} サーバーへの認証用のユーザー ID。
* stop_path: REST API の stop メソッドで使用されるパス。
* dashboard_path: ダッシュボードに情報を表示するために使用されるパス。
* restart_path: REST API の restart メソッドで使用されるパス。
* geo_port: {{site.data.keyword.geospatialshort_Geospatial}} サーバーのポート番号。
* password: {{site.data.keyword.geospatialshort_Geospatial}} サーバーへの認証用のパスワード。
* add_region_path: REST API の add_region メソッドで使用されるパス。


##例: VCAP_SERVICES 環境変数情報を取得する
{: #vcap_example}

次の Node.js コードは、サービス環境情報を取得します。 

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
