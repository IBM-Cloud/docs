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


#{{site.data.keyword.geospatialshort_Geospatial}} 概説
{: #gettingstarted}

{{site.data.keyword.geospatialfull}} を使用すると、 移動中のデバイスを
{{site.data.keyword.Bluemix_notm}} アプリケーションからモニターできます。 

始める前に、以下の要件に適合していることを確認してください。

* アプリケーション用の {{site.data.keyword.Bluemix_notm}} ランタイム環境 (例えば、SDK for Node.js) を決定します。ここで示されるすべてのコード例は Node.js を使用しています。スターター・アプリケーションも Node.js を使用して作成されています。
* コマンド・ラインから {{site.data.keyword.Bluemix_notm}} と対話できるように、[cf コマンド・ライン・インターフェース (CLI)](/docs/starters/install_cli.html){:new_window} をインストールします。
* デバイスの地理情報データを供給し、デバイスに関するイベント通知を受信するための、[MQTT](http://mqtt.org/){:new_window} メッセージ・ブローカーがあることを確認します。スターター・アプリケーションは、シミュレートされたデバイスの情報を生成するメッセージ・ブローカーをポイントします。
{{site.data.keyword.Bluemix_notm}} の
[Internet of Things Platform](https://console.ng.bluemix.net/catalog/services/internet-of-things-platform/){:new_window} サービス
は、MQTT メッセージ・ブローカーのニーズを満たすソリューションです。{{site.data.keyword.geospatialshort_Geospatial}} を Internet of Things Platform サービスと共に使用する方法について詳しくは、[Build a connected-car IoT app with {{site.data.keyword.geospatialshort_Geospatial}}](http://www.ibm.com/developerworks/mobile/library/mo-connectedcar-app/index.html){:new_window} を参照してください。

MQTT デバイス・メッセージの要件および構成について詳しくは、[サービス要件](/docs/services/geospatial/requirements.html){:new_window}を参照してください。


{{site.data.keyword.geospatialshort_Geospatial}} の使用を開始するには、以下のようにします。

1. 互換性のあるランタイムの 1 つを使用して {{site.data.keyword.Bluemix_notm}} にアプリケーションを作成します。SDK for Node.js™ を以下のコード・スニペットと共に使用することができます。
 
	スターター・アプリケーションを実行することにより、直ちに {{site.data.keyword.geospatialshort_Geospatial}} を開始することもできます。
 
2. アプリケーションに {{site.data.keyword.geospatialshort_Geospatial}} サービスを追加します。
3. アプリケーション・コードをコーディングして、以下のアクションを組み込みます。
	
	1. アプリケーション内で、{{site.data.keyword.geospatialshort_Geospatial}} の VCAP_SERVICES 環境変数情報を取得します。アプリケーションは、REST API を使用するためにこの情報を必要とします。以下のコード・スニペットは、[VCAP_SERVICES 環境変数](/docs/services/geospatial/vcap_services.html)の解析方法を示す例です。<pre><code>		 	
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
	2. REST API を通して地理情報サービスを構成および制御します。最小限、1 つの地域を定義し、サービスを開始する必要があります。『[REST API リファレンス](https://console.ng.bluemix.net/apidocs/246)』に、より複雑なアプリケーションを作成するために使用できる、さらに多くのフィーチャーについてのコード例が含まれています。コード・スニペット: 地域を定義します。
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
	3. サービスを開始して、MQTT からのデバイス・メッセージの受信を開始します。コード・スニペット: サービスを開始します。
	
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
		
4. コマンド・ライン・コマンドを使用して、アプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュします。アプリケーションのデプロイ方法について詳しくは、[{{site.data.keyword.Bluemix_notm}} にスターター・アプリケーションをプッシュする](/docs/services/geospatial/pushing_starter_app.html)というタイトルのセクションを参照してください。

5. ブラウザーでアプリケーションにアクセスします。アプリケーションの URL (または「経路」) は、{{site.data.keyword.Bluemix_notm}} ダッシュボードからアクセス可能なアプリケーション概要ページにあります。

# 関連リンク
{: #rellinks}

## チュートリアルおよびサンプル
{: #samples}
* [{{site.data.keyword.geospatialshort_Geospatial}} スターター・アプリケーションのダウンロード](https://hub.jazz.net/project/streamscloud/geo-starter/overview){:new_window}
* [IBM developerWorks 上の {{site.data.keyword.geospatialshort_Geospatial}} チュートリアル](http://www.ibm.com/developerworks/topics/geospatial%20analytics%20service){:new_window}
* [Who & Where – Find out with {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.geospatialshort_Geospatial}}](https://developer.ibm.com/bluemix/2014/12/17/find-bluemix-geospatial-analytics){:new_window}


## API リファレンス
{: #api}
* [{{site.data.keyword.geospatialshort_Geospatial}} REST API](https://console.ng.bluemix.net/apidocs/246){:new_window}

## 互換性のあるランタイム
{: #buildpacks}
* [Liberty for Java](/docs/runtimes/liberty/index.html#liberty)
* [Node.js](/docs/runtimes/nodejs/index.html#nodejs)

## 関連リンク
{: #general}
* [{{site.data.keyword.streamsshort}} 資料](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}
* [MQTT.org](http://mqtt.org/)
