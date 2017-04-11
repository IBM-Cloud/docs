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


#{{site.data.keyword.geospatialshort_Geospatial}} 入门
{: #gettingstarted}

{{site.data.keyword.geospatialfull}} 可从 {{site.data.keyword.Bluemix_notm}} 应用程序监视移动中的设备。 

开始之前，请先确保满足下列要求：

* 决定应用程序的 {{site.data.keyword.Bluemix_notm}} 运行时环境，如 SDK for Node.js。此处显示的代码示例全都使用 Node.js。入门模板应用程序也使用 Node.js 编写。
* 安装 [cf 命令行界面 (CLI)](/docs/starters/install_cli.html){:new_window} 以通过命令行与 {{site.data.keyword.Bluemix_notm}} 交互。
* 确保您有 [MQTT](http://mqtt.org/){:new_window} 消息代理，以提供地理空间设备数据和接收设备的事件通知。入门模板应用程序指向生成模拟设备信息的消息代理。{{site.data.keyword.Bluemix_notm}} 中的 [Internet of Things Platform](https://console.ng.bluemix.net/catalog/services/internet-of-things-platform/){:new_window} 服务是用于实现 MQTT 消息代理需求的解决方案。有关如何搭配使用 {{site.data.keyword.geospatialshort_Geospatial}} 和 Internet of Things Platform 服务的更多信息，请参阅 [Build a connected-car IoT app with {{site.data.keyword.geospatialshort_Geospatial}}](http://www.ibm.com/developerworks/mobile/library/mo-connectedcar-app/index.html){:new_window}。

请参阅[服务需求](/docs/services/geospatial/requirements.html){:new_window}，了解有关 MQTT 设备消息需求和配置的信息。


要开始使用 {{site.data.keyword.geospatialshort_Geospatial}}，请执行以下操作：

1. 使用一个兼容运行时在 {{site.data.keyword.Bluemix_notm}} 中创建应用程序。SDK for Node.js™ 使用下面提供的代码片段。
 
	此外，还可以通过运行入门模板应用程序立即开始使用 {{site.data.keyword.geospatialshort_Geospatial}}。
 
2. 将 {{site.data.keyword.geospatialshort_Geospatial}} 服务添加到应用程序。
3. 编写应用程序代码并包含以下操作：
	
	1. 在应用程序内，获取 {{site.data.keyword.geospatialshort_Geospatial}} 的 VCAP_SERVICES 环境变量信息。应用程序需要此信息才能使用 REST API。以下代码片段举例说明了如何解析 [VCAP_SERVICES 环境变量。](/docs/services/geospatial/vcap_services.html)
	<pre><code>		 	
		var geo_props = {};
		// Parse VCAP_SERVICES if running in Bluemix
		if (process.env.VCAP_SERVICES)
		{
			var env = JSON.parse(process.env.VCAP_SERVICES);
		
			//debugging
			for (var svcName in env) {
				console.log(svcName);
			}
			console.log(env);
			//find the Streams Geo service
			if (env['Geospatial Analytics']) {
				geo_props = env['Geospatial Analytics'][0]['credentials'];
			}
			else {
				console.log('You must bind the Streams Geo service to this application');
			}
		}
	</code></pre>
	2. 通过 REST API 配置和控制地理空间服务。必须至少定义一个地理区域并启动服务。[REST API 参考](https://console.ng.bluemix.net/apidocs/246)包含可在构建更复杂应用程序时使用的多个功能部件的代码示例。代码片段：定义区域。<pre><code>
	
		//
		// Begin - PUT addRegion
		//
		console.log("About to call REST PUT-addRegion api");  
		
		// Create the JSON object
		jsonObject = JSON.stringify({
		  "regions" : [
		  {"region_type" : "regular", "name" : "Kiosk 3", 
		   "notifyOnExit" : "false", 
		   "center_latitude" : "36.229531", 
		   "center_longitude" : "-115.277874", 
		   "number_of_sides" : "10", 
		   "distance_to_vertices" : "150"
		 }
		  ]
		});
		
		putheaders = {
'Content-Type' : 'application/json',
		    'Content-Length' : Buffer.byteLength(jsonObject, 'utf8'),
		    'Authorization' : authbuf
		};
		 
		// The PUT options
		optionsput = {
		    host : geo_props.geo_host,
		    port : geo_props.geo_port,
		    path : geo_props.add_region_path,
		    method : 'PUT',
		    headers : putheaders
		};
		 
		console.info('Options prepared:');
		console.info(optionsput);
		console.info('Do the PUT-addRegion call');
		 
		// Do the PUT call
		reqPut = https.request(optionsput, function(res) {
		    console.log("statusCode: ", res.statusCode);

		
		    if (res.statusCode != 200)
runError = 1;

		 
		    res.on('data', function(d) {
console.info('PUT result:\n');
		        process.stdout.write(d);
		        console.info('\n\nPUT completed');
		    });
		});
		 
		// Write the JSON data
		reqPut.write(jsonObject);
		reqPut.end();
		reqPut.on('error', function(e) {
		    console.error(e);
		});
		
		//
		// PUT-addRegion end
		//

		</code></pre>
	3. 启动服务，以开始从 MQTT 接收设备消息。代码片段：启动服务。
	
		<pre><code>							
				//
				// Begin - PUT start
				//
				console.log("About to call REST PUT-start api");  
				
				// Create the JSON object
				jsonObject = JSON.stringify({
				  "mqtt_uid" : "iamuser",
				  "mqtt_pw" : "thepass",
				  "mqtt_uri" :  "mqtt.myplace.com:1883",
				  "mqtt_input_topics" : "mytopic/cars/json/#",
				  "mqtt_notify_topic" : "demo-car-events",
				  "device_id_attr_name" : "ID",
				  "latitude_attr_name" : "lat",
				  "longitude_attr_name" : "lon"
				});
								
				// Prepare the header
				var authbuf = 'Basic ' + new Buffer(geo_props.userid + ':' + geo_props.password).toString('base64');
								
				var putheaders = {
				    'Content-Type' : 'application/json',
				    'Content-Length' : Buffer.byteLength(jsonObject, 'utf8'),
				    'Authorization' : authbuf
				};
				 
				// The PUT options
				var optionsput = {
				    host : geo_props.geo_host,
				    port : geo_props.geo_port,
				    path : geo_props.start_path,
				    method : 'PUT',
				    headers : putheaders
				};
				 
				console.info('Options prepared:');
				console.info(optionsput);
				console.info('Do the PUT-start call');
				 
				// Do the PUT call
				var reqPut = https.request(optionsput, function(res) {
				 
				    res.on('data', function(d) {
				        console.info('PUT result:\n');
				        process.stdout.write(d);
				        console.info('\n\nPUT completed');
				        console.log("statusCode: ", res.statusCode);
				    });
				    if (res.statusCode != 200)
				        runError = 1;
				
				});
				 
				// Write the JSON data
				reqPut.write(jsonObject);
				reqPut.end();
				reqPut.on('error', function(e) {
				    console.error(e);
				});
				
				//
				// PUT-start end
				//
		
		</code></pre>
		
4. 使用命令行命令将应用程序推送至 {{site.data.keyword.Bluemix_notm}}。在标题为[将入门模板应用程序推送至 {{site.data.keyword.Bluemix_notm}}](/docs/services/geospatial/pushing_starter_app.html) 的部分中，查找有关如何部署应用程序的更多信息。

5. 在浏览器中访问应用程序。您可以在应用程序概述页面上找到应用程序的 URL（或“路径”），可以从 {{site.data.keyword.Bluemix_notm}} 仪表板访问概述页面。

# 相关链接
{: #rellinks}

## 教程和样本
{: #samples}
* [{{site.data.keyword.geospatialshort_Geospatial}} 入门模板应用程序下载](https://hub.jazz.net/project/streamscloud/geo-starter/overview){:new_window}
* IBM developerWorks 上的 [{{site.data.keyword.geospatialshort_Geospatial}} 教程](http://www.ibm.com/developerworks/topics/geospatial%20analytics%20service){:new_window}
* [Who & Where – Find out with {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.geospatialshort_Geospatial}}](https://developer.ibm.com/bluemix/2014/12/17/find-bluemix-geospatial-analytics){:new_window}


## API 参考
{: #api}
* [{{site.data.keyword.geospatialshort_Geospatial}} REST API](https://console.ng.bluemix.net/apidocs/246){:new_window}

## 兼容运行时
{: #buildpacks}
* [Liberty for Java](/docs/runtimes/liberty/index.html#liberty)
* [Node.js](/docs/runtimes/nodejs/index.html#nodejs)

## 相关链接
{: #general}
* [{{site.data.keyword.streamsshort}} 文档](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}
* [MQTT.org](http://mqtt.org/)
