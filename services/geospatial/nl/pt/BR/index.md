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


#Introdução ao {{site.data.keyword.geospatialshort_Geospatial}}
{: #gettingstarted}

O {{site.data.keyword.geospatialfull}} monitora a movimentação de dispositivos a partir de seu aplicativo
{{site.data.keyword.Bluemix_notm}}. 

Antes de iniciar, certifique-se de que atenda aos requisitos a seguir:

* Decide sobre um ambiente de tempo de execução do {{site.data.keyword.Bluemix_notm}} para o aplicativo, como SDK for Node.js. Todos os exemplos de código que são mostrados aqui usam Node.js. O aplicativo iniciador também é escrito em Node.js.
* Instale a [interface da linha de comandos (CLI) de cf](/docs/starters/install_cli.html){:new_window} para interagir com o {{site.data.keyword.Bluemix_notm}} por meio da linha de comandos.
* Certifique-se de que tenha um message broker [MQTT](http://mqtt.org/){:new_window} para fornecer dados do dispositivo geoespacial e receber notificações de eventos para dispositivos. O aplicativo iniciador aponta para um message broker que gera informações sobre o dispositivo simulado. O serviço [Plataforma Internet das Coisas](https://console.ng.bluemix.net/catalog/services/internet-of-things-platform/){:new_window} no {{site.data.keyword.Bluemix_notm}} é uma solução para atender à necessidade de um message broker MQTT. Para obter mais informações sobre como usar o {{site.data.keyword.geospatialshort_Geospatial}} com o serviço Internet of Things Platform, consulte [Construir um app IoT conectado ao carro com o {{site.data.keyword.geospatialshort_Geospatial}}](http://www.ibm.com/developerworks/mobile/library/mo-connectedcar-app/index.html){:new_window}.

Consulte [Requisitos de serviço](/docs/services/geospatial/requirements.html){:new_window} para obter informações sobre os requisitos e a configuração de mensagem do dispositivo MQTT.


Para iniciar o {{site.data.keyword.geospatialshort_Geospatial}}:

1. Crie o seu aplicativo no {{site.data.keyword.Bluemix_notm}} com um dos tempos de execução compatíveis. O SDK for Node.js™ funciona com os fragmentos de código fornecidos aqui.
 
	Também é possível iniciar com o {{site.data.keyword.geospatialshort_Geospatial}} rapidamente executando o aplicativo iniciador.
 
2. Inclua um serviço {{site.data.keyword.geospatialshort_Geospatial}} em seu aplicativo.
3. Grave o código do aplicativo e inclua as ações a seguir:
	
	1. No aplicativo, obtenha as informações da variável de ambiente VCAP_SERVICES para {{site.data.keyword.geospatialshort_Geospatial}}. O seu aplicativo precisa dessas informações para usar a API REST. O fragmento de código a seguir é um exemplo de como analisar a [variável de ambiente VCAP_SERVICES.](/docs/services/geospatial/vcap_services.html)
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
	2. Configure e controle o serviço geo-espacial por meio da API REST. No mínimo, deve-se definir uma região geográfica e iniciar o serviço. A [referência de API REST](https://console.ng.bluemix.net/apidocs/246) inclui exemplos de código para mais recursos do que você pode usar para construir um aplicativo mais complexo. Fragmento do código:
                                Defina uma
                                região.
	<pre><code>
	
		// 		// Begin - PUT addRegion 		// 		console.log("About to call REST PUT-addRegion api");  
		
		// Create the JSON object
		jsonObject = JSON.stringify({
		  "regions" : [
		  {"region_type" : "regular", "name" : "Kiosk 3", "notifyOnExit" : "false", "center_latitude" : "36.229531", "center_longitude" : "-115.277874", "number_of_sides" : "10", "distance_to_vertices" : "150"}
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
	3. Inicie o serviço para começar a receber mensagens do dispositivo do MQTT. Fragmento do código: Inicie o
                                serviço.
	
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
		
4. Envie por push seu aplicativo para {{site.data.keyword.Bluemix_notm}}
                    com comandos da linha de comandos. Localize mais informações sobre como fazer para implementar seu
                    aplicativo na seção intitulada [Enviando por push
                        o aplicativo iniciador para {{site.data.keyword.Bluemix_notm}}](/docs/services/geospatial/pushing_starter_app.html).

5. Acesse o aplicativo em seu navegador. É possível localizar a URL do aplicativo (ou "rota") na página de visão geral do aplicativo, que é acessível pelo painel do {{site.data.keyword.Bluemix_notm}}.

# Links relacionados
{: #rellinks}

## Tutoriais e amostras
{: #samples}
* [Download do aplicativo iniciador {{site.data.keyword.geospatialshort_Geospatial}}](https://hub.jazz.net/project/streamscloud/geo-starter/overview){:new_window}
* [Tutoriais do {{site.data.keyword.geospatialshort_Geospatial}} sobre o IBM developerWorks](http://www.ibm.com/developerworks/topics/geospatial%20analytics%20service){:new_window}
* [Quem e onde – descubra com o {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.geospatialshort_Geospatial}}](https://developer.ibm.com/bluemix/2014/12/17/find-bluemix-geospatial-analytics){:new_window}


## Referência da API
{: #api}
* [{{site.data.keyword.geospatialshort_Geospatial}} API REST](https://console.ng.bluemix.net/apidocs/246){:new_window}

## Tempos de execução compatíveis
{: #buildpacks}
* [Liberty for Java](/docs/runtimes/liberty/index.html#liberty)
* [Node.js](/docs/runtimes/nodejs/index.html#nodejs)

## Links relacionados
{: #general}
* [Documentação do {{site.data.keyword.streamsshort}}](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}
* [MQTT.org](http://mqtt.org/)
