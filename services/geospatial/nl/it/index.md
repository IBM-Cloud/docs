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


#Introduzione a {{site.data.keyword.geospatialshort_Geospatial}}
{: #gettingstarted}

{{site.data.keyword.geospatialfull}} monitora
i dispositivi in movimento dalla tua applicazione {{site.data.keyword.Bluemix_notm}}. 

Prima di iniziare, assicurati di soddisfare i seguenti requisiti:

* Scegli un ambiente di runtime {{site.data.keyword.Bluemix_notm}} per l'applicazione, ad esempio SDK for Node.js. Gli esempi
di codice che vengono mostrati qui utilizzano tutti Node.js. Anche l'applicazione starter
è scritta in Node.js.
* Installa la [CLI (command-line interface) cf](/docs/starters/install_cli.html){:new_window} per interagire con {{site.data.keyword.Bluemix_notm}} dalla riga comandi.
* Assicurati di disporre di un broker dei messaggi [MQTT](http://mqtt.org/){:new_window}
per fornire i dati del dispositivo geospaziale e ricevere notifiche sugli eventi
 per i dispositivi. L'applicazione starter punta a un broker dei messaggi che genera informazioni sul dispositivo simulato. Il
servizio [Internet of Things Platform](https://console.ng.bluemix.net/catalog/services/internet-of-things-platform/){:new_window} in {{site.data.keyword.Bluemix_notm}} è una soluzione per soddisfare l'esigenza di un
broker di messaggi MQTT. Per ulteriori informazioni su come utilizzare {{site.data.keyword.geospatialshort_Geospatial}} con il servizio Piattaforma Internet delle cose, vedi [Build a connected-car IoT app with {{site.data.keyword.geospatialshort_Geospatial}}](http://www.ibm.com/developerworks/mobile/library/mo-connectedcar-app/index.html){:new_window}.

Per informazioni sui requisiti e la configurazione dei messaggi del
dispositivo MQTT, vedi [Requisiti di sistema](/docs/services/geospatial/requirements.html){:new_window}.


Per iniziare a lavorare con {{site.data.keyword.geospatialshort_Geospatial}}:

1. Crea la tua applicazione in {{site.data.keyword.Bluemix_notm}} con
uno dei runtime disponibili. SDK for Node.js™ funziona con i frammenti di codice qui forniti.
 
	Puoi anche iniziare a utilizzare {{site.data.keyword.geospatialshort_Geospatial}} immediatamente eseguendo l'applicazione starter.
 
2. Aggiungi un servizio {{site.data.keyword.geospatialshort_Geospatial}}
alla tua applicazione.
3. Scrivi il tuo codice applicativo e includi le seguenti azioni:
	
	1. All'interno della tua applicazione, ottieni le informazioni della variabile di ambiente VCAP_SERVICES
per {{site.data.keyword.geospatialshort_Geospatial}}. L'applicazione necessita di queste informazioni per
utilizzare l'API REST. Il seguente frammento di codice è un esempio di come analizzare la [variabile di ambiente VCAP_SERVICES.](/docs/services/geospatial/vcap_services.html)
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
	2. Configura e controlla il servizio geospaziale tramite l'API
REST. Come minimo, devi definire una regione geografica
e avviare il servizio. Il [riferimento all'API REST](https://console.ng.bluemix.net/apidocs/246) include
esempi di codice per altre funzioni che puoi
utilizzare per creare un'applicazione più complessa. Frammento di codice:
                           Definire una
  regione.
	<pre><code>
	
		//
		// Begin - PUT addRegion
		//
		console.log("About to call REST PUT-addRegion api");  
		
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
	3. Avvia il servizio per iniziare a ricevere messaggi del dispositivo da MQTT. Frammento di
codice: Avviare il servizio.
	
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
		
4. Distribuisci la tua applicazione a {{site.data.keyword.Bluemix_notm}}
  con i comandi della riga di comando. Per ulteriori informazioni
su come distribuire la tua applicazione, consulta la sezione
intitolata [Distribuzione
dell'applicazione starter a {{site.data.keyword.Bluemix_notm}}](/docs/services/geospatial/pushing_starter_app.html).

5. Accedi all'applicazione nel tuo browser. Puoi trovare l'URL (o "rotta") della tua applicazione nella pagina della panoramica dell'applicazione, accessibile dal dashboard {{site.data.keyword.Bluemix_notm}}.

# Link correlati
{: #rellinks}

## Esercitazioni ed esempi
{: #samples}
* [Download dell'applicazione starter {{site.data.keyword.geospatialshort_Geospatial}}](https://hub.jazz.net/project/streamscloud/geo-starter/overview){:new_window}
* [Esercitazioni {{site.data.keyword.geospatialshort_Geospatial}} su IBM developerWorks](http://www.ibm.com/developerworks/topics/geospatial%20analytics%20service){:new_window}
* [Who & Where – Find out with {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.geospatialshort_Geospatial}}](https://developer.ibm.com/bluemix/2014/12/17/find-bluemix-geospatial-analytics){:new_window}


## Riferimento API
{: #api}
* [{{site.data.keyword.geospatialshort_Geospatial}} API
                                        REST](https://console.ng.bluemix.net/apidocs/246){:new_window}

## Runtime compatibili
{: #buildpacks}
* [Liberty for Java](/docs/runtimes/liberty/index.html#liberty)
* [Node.js](/docs/runtimes/nodejs/index.html#nodejs)

## Link correlati
{: #general}
* [Documentazione {{site.data.keyword.streamsshort}}](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}
* [MQTT.org](http://mqtt.org/)
