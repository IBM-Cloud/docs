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


#Einführung in {{site.data.keyword.geospatialshort_Geospatial}}
{: #gettingstarted}

Mit {{site.data.keyword.geospatialfull}} werden
sich bewegende Geräte über Ihre {{site.data.keyword.Bluemix_notm}}-Anwendung überwacht. 

Stellen Sie vor Beginn sicher, dass die folgenden Voraussetzungen erfüllt sind:

* Entscheiden Sie sich für eine {{site.data.keyword.Bluemix_notm}}-Laufzeitumgebung für Ihre Anwendung, zum Beispiel SDK for Node.js. In allen nachfolgend aufgeführten Codebeispielen wird Node.js verwendet. Auch die Starteranwendung ist in Node.js geschrieben.
* Installieren Sie die [cf-Befehlszeilenschnittstelle](/docs/starters/install_cli.html){:new_window} für die Interaktion mit {{site.data.keyword.Bluemix_notm}} in der Befehlszeile.
* Stellen Sie sicher, dass Sie über einen [MQTT](http://mqtt.org/){:new_window}-Nachrichtenbroker zur Bereitstellung von Geogerätedaten und zum Empfangen von Ereignisbenachrichtigungen für Einheiten verfügen. Von der Starteranwendung wird auf einen Nachrichtenbroker verwiesen, von dem simulierte Gerätedaten generiert werden. Der Service [Internet of Things Platform](https://console.ng.bluemix.net/catalog/services/internet-of-things-platform/){:new_window} in {{site.data.keyword.Bluemix_notm}} ist eine
Lösung, mit der der Bedarf eines MQTT-Nachrichtenbrokers abgedeckt wird. Weitere Informationen zur Verwendung von {{site.data.keyword.geospatialshort_Geospatial}} mit dem Service 'Internet of Things Platform' finden Sie unter [Build a connected-car IoT app with {{site.data.keyword.geospatialshort_Geospatial}}](http://www.ibm.com/developerworks/mobile/library/mo-connectedcar-app/index.html){:new_window}.

Im Abschnitt zu den [Serviceanforderungen](/docs/services/geospatial/requirements.html){:new_window} finden Sie Informationen zu den Voraussetzungen für Nachrichten von MQTT-Geräten sowie zur entsprechenden Konfiguration.


Gehen Sie wie folgt vor, um mit {{site.data.keyword.geospatialshort_Geospatial}} zu arbeiten zu beginnen:

1. Erstellen Sie eine Anwendung in {{site.data.keyword.Bluemix_notm}} mit kompatiblen Laufzeiten. SDK for Node.js™ kann mit den hier bereitgestellten Code-Snippets verwendet werden.
 
	Sie können auch unmittelbar mit der Verwendung von {{site.data.keyword.geospatialshort_Geospatial}} beginnen, indem Sie die Starteranwendung ausführen.
 
2. Fügen Sie einen {{site.data.keyword.geospatialshort_Geospatial}}-Service zur Anwendung hinzu.
3. Schreiben Sie den Anwendungscode und schließen Sie die folgenden Aktionen ein:
	
	1. Rufen Sie in der Anwendung die Informationen zur Umgebungsvariable VCAP_SERVICES für {{site.data.keyword.geospatialshort_Geospatial}} ab. Für die Anwendung sind diese Informationen zur Verwendung der REST-API erforderlich. Das folgende Code-Snippet ist ein Beispiel dafür, wie die [Umgebungsvariable VCAP_SERVICES](/docs/services/geospatial/vcap_services.html) geparst wird.
	<pre><code>		 	
		var geo_props = {};
		// Analysieren von VCAP_SERVICES bei Ausführung in Bluemix
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
	2. Konfigurieren und steuern Sie den Geodatenservice über die REST-API. Sie müssen mindestens eine geografische Region definieren und den Service starten. Der [Verweis auf die REST-API](https://console.ng.bluemix.net/apidocs/246) umfasst Codebeispiele für mehrere Features, mit denen Sie eine komplexere Anwendung erstellen können. Code-Snippet: Definieren einer Region.
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
	3. Starten Sie den Service, um mit dem Empfangen von Gerätenachrichten von MQTT zu beginnen. Code-Snippet: Starten des Service.
	
		<pre><code>							
				//
				// Anfang - PUT start
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
		
4. Übertragen Sie die Anwendung mit einer Push-Operation mithilfe von Befehlen in der Befehlszeile an {{site.data.keyword.Bluemix_notm}}. Weitere Informationen zum Bereitstellen Ihrer Anwendung finden Sie im Abschnitt [Starteranwendung mit Push-Operation an {{site.data.keyword.Bluemix_notm}}](/docs/services/geospatial/pushing_starter_app.html) übertragen.

5. Greifen Sie auf die Anwendung im Browser zu. Sie finden die URL (oder "Route") der Anwendung auf der Übersichtsseite der Anwendung, die im {{site.data.keyword.Bluemix_notm}}-Dashboard verfügbar ist.

# Zugehörige Links
{: #rellinks}

## Lerntexte und Beispiele
{: #samples}
* [Starteranwendung von {{site.data.keyword.geospatialshort_Geospatial}} - Download](https://hub.jazz.net/project/streamscloud/geo-starter/overview){:new_window}
* [Lernprogramme zu {{site.data.keyword.geospatialshort_Geospatial}} unter IBM developerWorks](http://www.ibm.com/developerworks/topics/geospatial%20analytics%20service){:new_window}
* [Wer & Wo – Finden Sie es heraus mit {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.geospatialshort_Geospatial}}](https://developer.ibm.com/bluemix/2014/12/17/find-bluemix-geospatial-analytics){:new_window}


## API-Referenz
{: #api}
* [{{site.data.keyword.geospatialshort_Geospatial}} REST-API](https://console.ng.bluemix.net/apidocs/246){:new_window}

## Kompatible Laufzeiten
{: #buildpacks}
* [Liberty for Java](/docs/runtimes/liberty/index.html#liberty)
* [Node.js](/docs/runtimes/nodejs/index.html#nodejs)

## Zugehörige Links
{: #general}
* [{{site.data.keyword.streamsshort}}-Dokumentation](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}
* [MQTT.org](http://mqtt.org/)
