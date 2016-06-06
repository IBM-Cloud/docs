---

copyright:
  years: 2016

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

# Visualizing Device Data
{: #visualizingdata_data}
*Last updated: 20 April 2016*

This sample helps you visualize real-time and historic data from registered devices in your {{site.data.keyword.iot_full}} organization.
{:shortdesc}

## Before you begin

Before you can visualize your data, your must take the following actions:

- Register your devices to your {{site.data.keyword.iot_short_notm}} organization.
- Ensure that your devices are sending events to the {{site.data.keyword.iot_short_notm}}.
- [Download the visualization sample](https://github.com/ibm-messaging/iot-visualization/archive/v0.2.0.zip) from the github repository and extract the .zip file.
- [Install the cf command-line tool](../../starters/install_cli.html) from {{site.data.keyword.Bluemix_notm}}.

## Running the sample in {{site.data.keyword.Bluemix_notm}}

1. Create an application in {{site.data.keyword.Bluemix_notm}} using the Node.js SDK. Note the application name and hostname of the application, this information is required to upload the application to {{site.data.keyword.Bluemix_notm}}.
2. Bind the node.JS application to your {{site.data.keyword.iot_short_notm}} instance in your {{site.data.keyword.Bluemix_notm}} dashboard by completing the following steps:

  a. In your {{site.data.keyword.Bluemix_notm}} dashboard, click on the Node.JS application you have created.

  b. Click **Bind a service or API** and then select your {{site.data.keyword.iot_short_notm}} service and click **Add**.
3. Using the cf command-line tool, change your directory to the extracted visualization sample package and run the following command to connect to {{site.data.keyword.Bluemix_notm}}.
```
cf api https://api.ng.bluemix.net
```
4. Next, login to {{site.data.keyword.Bluemix_notm}} using:
```
cf login -u <your_bluemix_login_id>
```
If you are not using the default organization and space, you can use:
```
cf target-o <your_bluemix_org> -s dev
```

5. Edit the `manifest.yml` file and update the host and application names using the following format:
```
applications:
 - disc quota: 1024M
   host: <your_bluemix_hostname>
   name: <your_bluemix_appname>
   command: node ap.js
   path:
   domain: mybluemix.net
   instances: 1
   memory: 128M
```
6. Deploy your visualization sample by using the following command:
```
cf push <your_application_name>
```
7. In your browser, enter the following URL:
```
http://<your_application_name>.mybluemix.net
```

All devices in your organization are listed in the device drop down menu. When selected, you should see the real-time visualization of the data that device is sending to your {{site.data.keyword.iot_short_notm}} service. To see the historic data, click the **Historic Data** button.

### Customizing the sample

This sample application is a stand-alone web application, written on the node.js framework. The sample visualizes events that are sent by registered devices in your {{site.data.keyword.iot_short_notm}}. The sample uses the following tools:

- Express: Node.js web application framework
- JQuery: UI and Ajax calls
- Rickshaw: Graphical visualization tool
- Paho: MQTT client

The sample application is structured with the following directories:

- Public
- CSS: Stylesheets
- Images
- JS: main JavaScript logic files
- Historian: code for historian visualization
- Realtime: code for real-time visualization
- Uicontroller.js: code for controlling the user interface
- Routes: routing logic and the web application
- Utils: utility functions, used for making HTTP calls
- Views: user interface files, written in Jade
- The Rickshaw charting library is used to plot the graph for both real-time and historic data.

### Customizing real-time data display

The directory containing the graphical visualization code for real-time data is `public/ja/realtime`. The graphing logic can be customized by editing `public/js/historian/realtimeGraph.js`.

The file that references the Paho MQTT library to subscribe to device topics and receive device events from the {{site.data.keyword.iot_short_notm}} can be found at `public/js/historian/realtime.js`.

Device events are passed to the `realtimeGraph.js` file to plot the graph.

### Customizing the historic data display

The directory containing graphical visualization code for historic device data is `public/js/historian`. The graphing logic can be customized by editing `public/js/historian/historianGraph.js`.

The file that controls ReST API calls to collect historic device data is `public/js/historian/historian.js`.

Historic data is passed to the `historianGraph.js` file to plot the graph.

A more detailed developer's guide is available from the Github iot-visualization wiki.
