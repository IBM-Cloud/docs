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


#開始使用 {{site.data.keyword.geospatialshort_Geospatial}}
{: #gettingstarted}

{{site.data.keyword.geospatialfull}} 會從 {{site.data.keyword.Bluemix_notm}} 應用程式監視移動中的裝置。 

開始之前，請確定您符合下列需求：

* 選定應用程式的 {{site.data.keyword.Bluemix_notm}} 運行環境，例如 SDK for Node.js。這裡顯示的程式碼範例都是使用 Node.js。入門範本應用程式也是使用 Node.js 所撰寫。
* 安裝 [cf 指令行介面 (CLI)](/docs/starters/install_cli.html){:new_window}，可透過指令行與 {{site.data.keyword.Bluemix_notm}} 互動。
* 確定您具有 [MQTT](http://mqtt.org/){:new_window} 訊息分配管理系統，可提供地理空間裝置資料，以及接收裝置的事件通知。入門範本應用程式指向產生模擬裝置資訊的訊息分配管理系統。{{site.data.keyword.Bluemix_notm}} 中的 [Internet of Things Platform](https://console.ng.bluemix.net/catalog/services/internet-of-things-platform/){:new_window} 服務是滿足 MQTT 訊息分配管理系統需要的解決方案。如需如何使用 {{site.data.keyword.geospatialshort_Geospatial}} 與 Internet of Things Platform 服務的相關資訊，請參閱 [Build a connected-car IoT app with {{site.data.keyword.geospatialshort_Geospatial}}](http://www.ibm.com/developerworks/mobile/library/mo-connectedcar-app/index.html){:new_window}。

如需 MQTT 裝置訊息需求與配置的相關資訊，請參閱[服務需求](/docs/services/geospatial/requirements.html){:new_window}。


若要開始使用 {{site.data.keyword.geospatialshort_Geospatial}}，請執行下列動作：

1. 使用其中一個相容的運行環境，在 {{site.data.keyword.Bluemix_notm}} 中建立應用程式。SDK for Node.js™ 與這裡提供的程式碼 Snippet 搭配運作。
 
	您也可以執行入門範本應用程式，立即開始使用 {{site.data.keyword.geospatialshort_Geospatial}}。
 
2. 將 {{site.data.keyword.geospatialshort_Geospatial}} 服務新增至應用程式。
3. 撰寫應用程式碼，並包含下列動作：
	
	1. 在應用程式內，取得 {{site.data.keyword.geospatialshort_Geospatial}} 的 VCAP_SERVICES 環境變數資訊。您的應用程式需要此資訊，才能使用 REST API。下列程式碼 Snippet 是如何剖析 [VCAP_SERVICES 環境變數](/docs/services/geospatial/vcap_services.html)的範例。
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
	2. 透過 REST API 配置及控制地理空間服務。您必須至少定義一個地理區域並且啟動服務。[REST API 參考資料](https://console.ng.bluemix.net/apidocs/246)包括可用來建置更複雜應用程式的其他特性的程式碼範例。程式碼 Snippet：定義地區。
	<pre><code>
	
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
	3. 啟動服務，以開始接收來自 MQTT 的裝置訊息。程式碼 Snippet：啟動服務。
	
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
		
4. 使用指令行指令，將應用程式推送至 {{site.data.keyword.Bluemix_notm}}。如何部署應用程式的相關資訊位於標題為[將入門範本應用程式推送到 {{site.data.keyword.Bluemix_notm}}](/docs/services/geospatial/pushing_starter_app.html) 的小節。

5. 在瀏覽器存取應用程式。您可以在應用程式概觀頁面上找到應用程式的 URL（或「路徑」），此頁面可從 {{site.data.keyword.Bluemix_notm}} 儀表板存取。

# 相關鏈結
{: #rellinks}

## 指導教學及範例
{: #samples}
* [{{site.data.keyword.geospatialshort_Geospatial}} 入門範本應用程式下載](https://hub.jazz.net/project/streamscloud/geo-starter/overview){:new_window}
* [IBM developerWorks 上的 {{site.data.keyword.geospatialshort_Geospatial}} 指導教學](http://www.ibm.com/developerworks/topics/geospatial%20analytics%20service){:new_window}
* [Who & Where – Find out with {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.geospatialshort_Geospatial}}](https://developer.ibm.com/bluemix/2014/12/17/find-bluemix-geospatial-analytics){:new_window}


## API 參考資料
{: #api}
* [{{site.data.keyword.geospatialshort_Geospatial}} REST API](https://console.ng.bluemix.net/apidocs/246){:new_window}

## 相容的運行環境
{: #buildpacks}
* [Liberty for Java](/docs/runtimes/liberty/index.html#liberty)
* [Node.js](/docs/runtimes/nodejs/index.html#nodejs)

## 相關鏈結
{: #general}
* [{{site.data.keyword.streamsshort}} 文件](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}
* [MQTT.org](http://mqtt.org/)
