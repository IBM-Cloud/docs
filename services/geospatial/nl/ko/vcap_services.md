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

#VCAP_SERVICES 환경 정보
{: #vcap_services}


VCAP_SERVICES 환경 변수에는 {{site.data.keyword.geospatialshort_Geospatial}} REST API를 사용하는 데 필요한 정보가 포함되어 있습니다.
{:shortdesc}

##설명
{: #vcap_description}

VCAP_SERVICES 환경 변수에는 다음 예제와 유사한 정보가 포함되어 있습니다.  

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

VCAP_SERVICES 환경 변수에는 다음 항목이 포함되어 있습니다. 

* key: {{site.data.keyword.geospatialshort_Geospatial}} 서비스의 이름입니다[{{site.data.keyword.geospatialshort_Geospatial}}].  
* name: 서비스 인스턴스의 이름입니다.  
* label: 서비스의 이름입니다.  
* plan: 서비스 플랜의 이름입니다.  
* start_path: REST API의 start 메소드에서 사용되는 경로입니다.  
* geo_host: {{site.data.keyword.geospatialshort_Geospatial}} 서버의 호스트 이름입니다. 
* status_path: REST API의 status 메소드에서 사용되는 경로입니다. 
* remove_region_path: REST API의 remove_region 메소드에서 사용되는 경로입니다. 
* userid: {{site.data.keyword.geospatialshort_Geospatial}} 서버 인증에 사용되는 사용자 ID입니다. 
* stop_path: REST API의 stop 메소드에서 사용되는 경로입니다. 
* dashboard_path: 대시보드에 정보를 인쇄하는 데 사용되는 경로입니다. 
* restart_path: REST API의 restart 메소드에서 사용되는 경로입니다. 
* geo_port: {{site.data.keyword.geospatialshort_Geospatial}} 서버의 포트 번호입니다. 
* password: {{site.data.keyword.geospatialshort_Geospatial}} 서버 인증에 사용되는 비밀번호입니다. 
* add_region_path: REST API의 add_region 메소드에서 사용되는 경로입니다. 


##예제: VCAP_SERVICES 환경 변수 정보 검색
{: #vcap_example}

다음 Node.js 코드에서는 서비스 환경 정보를 검색합니다. 

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
