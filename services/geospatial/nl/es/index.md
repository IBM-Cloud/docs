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


#Iniciación a {{site.data.keyword.geospatialshort_Geospatial}}
{: #gettingstarted}

{{site.data.keyword.geospatialfull}} supervisa dispositivos en movimiento desde la aplicación {{site.data.keyword.Bluemix_notm}}. 

Antes de comenzar, asegúrese de que cumple los requisitos siguientes:

* Elija un entorno de tiempo de ejecución de {{site.data.keyword.Bluemix_notm}} para la aplicación como, por ejemplo, SDK for Node.js. Los ejemplos de código que se muestran aquí utilizan todos Node.js. La aplicación de inicio también está escrita en Node.js.
* Instale la [interfaz de línea de mandatos (CLI) de cf](/docs/starters/install_cli.html){:new_window} para interactuar con {{site.data.keyword.Bluemix_notm}} desde la línea de mandatos.
* Asegúrese de tener un intermediario de mensajes [MQTT](http://mqtt.org/){:new_window} para facilitar datos de dispositivos geoespaciales y recibir notificaciones de sucesos para dispositivos. La aplicación del iniciador apunta a un intermediario de mensajes que genera información de dispositivo simulada. El servicio [Internet of Things Platform](https://console.ng.bluemix.net/catalog/services/internet-of-things-platform/){:new_window} de {{site.data.keyword.Bluemix_notm}} es una solución que satisface la necesidad de un intermediario de mensajes MQTT. Para obtener más información sobre cómo utilizar {{site.data.keyword.geospatialshort_Geospatial}} con el servicio Internet of Things Platform, consulte [Crear una aplicación IoT con conexión al automóvil con {{site.data.keyword.geospatialshort_Geospatial}}](http://www.ibm.com/developerworks/mobile/library/mo-connectedcar-app/index.html){:new_window}.

Consulte
[Requisitos del servicio](/docs/services/geospatial/requirements.html){:new_window} para obtener información sobre los requisitos y la configuración de mensajes de dispositivo MQTT.


Para empezar con {{site.data.keyword.geospatialshort_Geospatial}}:

1. Cree la aplicación en {{site.data.keyword.Bluemix_notm}} mediante uno de los tiempos de ejecución compatibles. SDK for Node.js™ funciona con los fragmentos de código que se proporcionan aquí.
 
	También puede empezar a utilizar {{site.data.keyword.geospatialshort_Geospatial}} directamente ejecutando la aplicación de inicio.
 
2. Añada un servicio {{site.data.keyword.geospatialshort_Geospatial}} a la aplicación.
3. Escriba el código de su aplicación e incluya las acciones siguientes:
	
	1. Dentro de la aplicación, obtenga la información de la variable de entorno VCAP_SERVICES para {{site.data.keyword.geospatialshort_Geospatial}}. La aplicación necesita esta información para utilizar la API REST. El siguiente fragmento de código es un ejemplo de cómo analizar la [variable de entorno VCAP_SERVICES.](/docs/services/geospatial/vcap_services.html)
	<pre><code>		 	
		var geo_props = {};
		// Analizar VCAP_SERVICES si se ejecuta en Bluemix
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
				console.log('Debe enlazar el servicio Streams Geo a esta aplicación');
			}
		}
	</code></pre>
	2. Configure y controle el servicio geoespacial a través de la API REST. Como mínimo, debe definir una región geográfica e iniciar el servicio. La [referencia de API REST](https://console.ng.bluemix.net/apidocs/246) incluye ejemplos de código para más características que puede utilizar para crear una aplicación más compleja. Fragmento de código: Definir una región.
	<pre><code>
	
		//
		// Comenzar - PUT addRegion
		//
		console.log("A punto de llamar a la api PUT-addRegion de REST");  
		
		// Crear el objeto JSON
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
		 
		// Las opciones PUT
		optionsput = {
		    host : geo_props.geo_host,
		    port : geo_props.geo_port,
		    path : geo_props.add_region_path,
		    method : 'PUT',
		    headers : putheaders
		};
		 
		console.info('Opciones preparadas:');
		console.info(optionsput);
		console.info('Realizar la llamada PUT-addRegion');
		 
		// Realizar la llamada PUT
		reqPut = https.request(optionsput, function(res) {
		    console.log("statusCode: ", res.statusCode);
		
		    if (res.statusCode != 200)
		        runError = 1;
		 
		    res.on('data', function(d) {
		        console.info('PUT result:\n');
		        process.stdout.write(d);
		        console.info('\n\nPUT completado');
		    });
		});
		 
		// Escribir los datos JSON
		reqPut.write(jsonObject);
		reqPut.end();
		reqPut.on('error', function(e) {
		    console.error(e);
		});
		
		//
		// Finalizar PUT-addRegion
		//

		</code></pre>
	3. Inicie el servicio para empezar a recibir mensajes de dispositivo de MQTT. Fragmento de código: Iniciar el servicio.
	
		<pre><code>							
				//
				// Begin - PUT start
				//
				console.log("A punto de llamar a la api PUT-start de REST");  
				
				// Crear el objeto JSON
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
								
				// Preparar la cabecera
				var authbuf = 'Basic ' + new Buffer(geo_props.userid + ':' + geo_props.password).toString('base64');
								
				var putheaders = {
				    'Content-Type' : 'application/json',
				    'Content-Length' : Buffer.byteLength(jsonObject, 'utf8'),
				    'Authorization' : authbuf
				};
				 
				// Las opciones PUT
				var optionsput = {
				    host : geo_props.geo_host,
				    port : geo_props.geo_port,
				    path : geo_props.start_path,
				    method : 'PUT',
				    headers : putheaders
				};
				 
				console.info('Opciones preparadas:');
				console.info(optionsput);
				console.info('Realizar la llamada PUT-start');
				 
				// Realizar la llamada PUT
				var reqPut = https.request(optionsput, function(res) {
				 
				    res.on('data', function(d) {
				        console.info('PUT result:\n');
				        process.stdout.write(d);
				        console.info('\n\nPUT completado');
				        console.log("statusCode: ", res.statusCode);
				    });
				    if (res.statusCode != 200)
				        runError = 1;
				
				});
				 
				// Escribir los datos JSON
				reqPut.write(jsonObject);
				reqPut.end();
				reqPut.on('error', function(e) {
				    console.error(e);
				});
				
				//
				// Finalizar con PUT-start
				//
		
		</code></pre>
		
4. Envíe por push la aplicación a {{site.data.keyword.Bluemix_notm}} con los mandatos de la línea de mandatos. Encontrará más información sobre cómo desplegar la aplicación en la sección sobre [Envío de la aplicación de inicio a {{site.data.keyword.Bluemix_notm}}](/docs/services/geospatial/pushing_starter_app.html).

5. Acceda a la aplicación en su navegador. Encontrará el URL de la aplicación (o "route") en la página de visión general de la aplicación, a la que se puede acceder desde el panel de control de {{site.data.keyword.Bluemix_notm}}.

# Enlaces relacionados
{: #rellinks}

## Guías de aprendizaje y ejemplos
{: #samples}
* [Descarga de la aplicación de inicio {{site.data.keyword.geospatialshort_Geospatial}}](https://hub.jazz.net/project/streamscloud/geo-starter/overview){:new_window}
* [Guías de aprendizaje de {{site.data.keyword.geospatialshort_Geospatial}} en IBM developerWorks](http://www.ibm.com/developerworks/topics/geospatial%20analytics%20service){:new_window}
* [Quién y dónde – Descúbralo con {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.geospatialshort_Geospatial}}](https://developer.ibm.com/bluemix/2014/12/17/find-bluemix-geospatial-analytics){:new_window}


## Referencia de API
{: #api}
* [{{site.data.keyword.geospatialshort_Geospatial}} API REST](https://console.ng.bluemix.net/apidocs/246){:new_window}

## Tiempos de ejecución compatibles
{: #buildpacks}
* [Liberty for Java](/docs/runtimes/liberty/index.html#liberty)
* [Node.js](/docs/runtimes/nodejs/index.html#nodejs)

## Enlaces relacionados
{: #general}
* [Documentación de {{site.data.keyword.streamsshort}}](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}
* [MQTT.org](http://mqtt.org/)
