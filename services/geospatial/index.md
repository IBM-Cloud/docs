---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-09"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


#Getting started with {{site.data.keyword.geospatialshort_Geospatial}}
{: #gettingstarted}

{{site.data.keyword.geospatialfull}}  monitors moving devices from your {{site.data.keyword.Bluemix_notm}} application.

Before you begin, make sure that you meet the following requirements:

* Decide on a {{site.data.keyword.Bluemix_notm}} runtime environment for the application, such as SDK for Node.js. The code examples that are shown here all use Node.js. The starter application is also written in Node.js.
* Install the [cf command-line interface (CLI)](/docs/starters/install_cli.html){:new_window} to interact with {{site.data.keyword.Bluemix_notm}} from the command line.
* Ensure that you have an [MQTT](http://mqtt.org/){:new_window} message broker to supply geospatial device data and receive event notifications for devices. The starter application points to a message broker that generates simulated device information. The [Internet of Things Platform](https://console.ng.bluemix.net/catalog/services/internet-of-things-platform/){:new_window} service in {{site.data.keyword.Bluemix_notm}} is a solution to fulfill the need of an MQTT message broker. For more information on how to use {{site.data.keyword.geospatialshort_Geospatial}} with the Internet of Things Platform  service, see [Build a connected-car IoT app with {{site.data.keyword.geospatialshort_Geospatial}}](http://www.ibm.com/developerworks/mobile/library/mo-connectedcar-app/index.html){:new_window}.

See [Service requirements](/docs/services/geospatial/requirements.html){:new_window} for information about the MQTT device message requirements and configuration.


To get started with {{site.data.keyword.geospatialshort_Geospatial}}:

1. Create your application in {{site.data.keyword.Bluemix_notm}} with one of the compatible runtimes. SDK for Node.js™ works with the code snippets provided here.

	You can also get started with {{site.data.keyword.geospatialshort_Geospatial}} right away by running the starter application.

2. Add a {{site.data.keyword.geospatialshort_Geospatial}} service to your application.
3. Write your application code and include the following actions:

	1. Within your application, obtain the VCAP_SERVICES environment variable information for {{site.data.keyword.geospatialshort_Geospatial}}. Your application needs this information to use the REST API. The following code snippet is an example of how to parse the [VCAP_SERVICES environment variable.](/docs/services/geospatial/vcap_services.html)
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
	2. Configure and control the geospatial service through the REST API. At a minimum, you must define a geographic region and start the service. The [REST API reference](https://console.ng.bluemix.net/apidocs/246) includes code examples for more features that you can use to build a more complex application. Code snippet: Define a region.
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
	3. Start the service to begin receiving device messages from MQTT. Code snippet: Start the service.

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
4. Push your application to {{site.data.keyword.Bluemix_notm}} with command-line commands. Find more information on how to do deploy your application in the section titled [Pushing the starter application to {{site.data.keyword.Bluemix_notm}}](/docs/services/geospatial/pushing_starter_app.html).

5. Access the application in your browser.You can find your application's URL (or "route") on the application overview page, which is accessible from the {{site.data.keyword.Bluemix_notm}} dashboard.

# Related Links
{: #rellinks notoc}

## Tutorials and Samples
{: #samples notoc}
* [{{site.data.keyword.geospatialshort_Geospatial}} starter application download](https://hub.jazz.net/project/streamscloud/geo-starter/overview){:new_window}
* [{{site.data.keyword.geospatialshort_Geospatial}} tutorials on IBM developerWorks](http://www.ibm.com/developerworks/topics/geospatial%20analytics%20service){:new_window}
* [Who & Where – Find out with {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.geospatialshort_Geospatial}}](https://developer.ibm.com/bluemix/2014/12/17/find-bluemix-geospatial-analytics){:new_window}
*

## API Reference
{: #api notoc}
* [{{site.data.keyword.geospatialshort_Geospatial}} REST API](https://console.ng.bluemix.net/apidocs/246){:new_window}

## Compatible Runtimes
{: #buildpacks notoc}
* [Liberty for Java](/docs/runtimes/liberty/index.html#liberty)
* [Node.js](/docs/runtimes/nodejs/index.html#nodejs)

## Related Links
{: #general notoc}
* [{{site.data.keyword.streamsshort}} documentation](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}
* [MQTT.org](http://mqtt.org/)
* * [Real-time hangout detection with {{site.data.keyword.streaminganalyticsshort}}](https://developer.ibm.com/bluemix/2016/05/27/real-time-hangout-detection/){:new_window}
