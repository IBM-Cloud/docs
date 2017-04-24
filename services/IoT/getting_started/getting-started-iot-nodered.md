---

copyright:
  years: 2017
lastupdated: "2017-04-24"
---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with {{site.data.keyword.iot_short_notm}} starter
{: #gettingstartedtemplate}
<!-- Provide an appropriate ID above -->

Get started with {{site.data.keyword.iot_full}} by using the {{site.data.keyword.iot_short_notm}} Starter GitHub project. By using the Starter, you can quickly simulate a device, create cards, generate data, and begin analyzing and displaying data in the {{site.data.keyword.iot_short_notm}} dashboard.  
{:shortdesc}

## Overview
{: #overview}  

The starter automatically deploys and connects these services:
<dl>
<dt>**{{site.data.keyword.iot_short_notm}}**</dt>
<dd>An IoT web service that includes gateway management, device management, and application access. By using {{site.data.keyword.iot_short_notm}}, you can collect connected device data and run analytics on real-time data from your organization.</dd>
<dt>**{{site.data.keyword.sdk4nodefull}}**</dt>
<dd>The runtime environment in which Node-RED runs. </br>For more information, see the [{{site.data.keyword.sdk4nodefull}} starter documentation](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html).</dd>
<dd>Node-RED is a tool for wiring together hardware devices, APIs, and online services in new and interesting ways.  You can use Node-RED to create a simulated thermostat that sends simulated data to your {{site.data.keyword.iot_short_notm}} service. You can create cards to display real-time data in the {{site.data.keyword.iot_short_notm}} dashboard. </br>For more information, see the [Node-RED documentation](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered).</dd>
<dt>**{{site.data.keyword.cloudantfull}}**</dt><dd>The database in which Node-RED stores metadata.</dd>
</dl>

## Before you begin
{: #byb}  

- Required accounts  
Before you begin, you'll need an [IBM Bluemix account](https://bluemix.net/registration) .

- Getting around  
To make moving between tasks easier in the process that follows, open the {{site.data.keyword.Bluemix_notm}} dashboard, the {{site.data.keyword.iot_short_notm}} dashboard, and the Node-RED application in different tabs in your browser.
<dl>
<dt>*{{site.data.keyword.Bluemix_notm}} dashboard*</dt>
<dd>See the state of your deployment, read documentation, and launch the dashboards.</dd>
<dt>*{{site.data.keyword.iot_short_notm}} dashboard*</dt>
<dd>Define device types, register devices, monitor incoming sensor data, create data visualization cards, and see live data visualizations.</dd>
<dt>*Node-RED*</dt>
<dd>Configure and run the device simulator flow and work with other flows to process data from {{site.data.keyword.iot_short_notm}}.</dd>
</dl>

## Step 1: Deploy the {{site.data.keyword.iot_short_notm}} Starter
{: #deployStarter}

Perform the following steps to deploy the Starter sample application:

1. Deploy the starter application.
 1. Click <a href="https://bluemix.net/devops/setup/deploy?repository=https://github.com/ibm-watson-iot/iot-platform-bluemix-starter"><img src="https://bluemix.net/devops/graphics/create_toolchain_button.png" height=25></a> to create a new Continuous Delivery Toolchain in Bluemix:  (via Continuous Delivery)  
 **Tip:** If you'd rather deploy from the command line, you can [find the {{site.data.keyword.iot_short_notm}} starter](https://github.com/ibm-watson-iot/iot-platform-bluemix-starter) in the IBM Watson IoT organization in GitHub.
 2. When prompted, log in to IBM Bluemix.
 3. If needed, select the Bluemix Organization where you want to deploy the starter application.
 4. Keep the Toolchain name, or update it as needed. It is used as the default app name and the root of your app's URL: `<app-name>.mybluemix.net`
 5. Click **Create**.  
**Tip:** Click the **Delivery Pipeline** tile to monitor the progress for your first deployment.
 6. When the deployment is complete, click **View App** to open your new Node-RED application in a new tab.
2. Locate the starter app services.
 1. From the Bluemix menu, select **Dashboard**.
 2. Locate the following services under *All services*:
    - iot-starter
    - iotp-starter-cloudantNoSQLDB
 3. Locate the toolchain under *All Apps*:
    - default-toolchain-{id}}


## Step 2: Define a simulated device in {{site.data.keyword.iot_short_notm}}
{: #definingsimdev}

Complete the following steps to simulate a scenario that uses a thermostat to monitor temperature, humidity, and location of a living room.

1.	Launch the {{site.data.keyword.iot_short_notm}} dashboard.
  1. In the Bluemix dashboard, under *All services*, click the name of your {{site.data.keyword.iot_short_notm}} instance.
**Tip:** The instance name usually includes `iotp-starter`.
  2. Click **Launch** to open the {{site.data.keyword.iot_short_notm}} dashboard in a new browser tab.   
The `All Boards` page is displayed by default.
2. Create a device type.
  1.	From the main menu, select **Devices**, and then click **Add Device**.
  2.	In the Add Device page, click **Create device type**.
  3.	In the Create Device Type page, click **Create device type**.
  4. Enter a unique name (for example `Thermostat`) for your device type, and click **Next**.
  5. Optional: Defining a template and metadata on the next two pages is optional and can be safely skipped by clicking **Next** on each page.
  6.	Click **Create** to add the device type.
3.	Add a device that uses the newly created device type.
  1. On the Add Device page, the device type that you just created is displayed in the list of device types. Click **Next** to add a device that uses that device type.
  2. Enter a unique device ID (for example `LivingRoomThermo1`).
  3. Optional: Providing descriptive data on the Add Device page or entering device metadata on the next page is optional, and you can safely skip those pages by clicking **Next** on each page.
  4. On the Security page, click **Next** to generate an authentication token for your device.
  5. On the Summary page, verify that the information is correct and click **Add** to add the device. Click **Back** to return to a previous page.
4.	Make a note of the information that is displayed in the Your Device Credentials page.   
You need the following information to configure the simulator and display the data:
 - Organization ID
 - Device Type
 - Device ID
 - Authentication Method
 - Authentication Token

## Sep 3: Configure and run the Node-RED device simulator.  
{: #confignodered}  
Configure the Node-RED device simulator to send MQTT device messages with temperature and humidity information to {{site.data.keyword.iot_short_notm}}.

1. Launch the Node-RED flow editor.
  1. In the Bluemix dashboard, under *All apps*, click the name of your toolchain.  
**Tip:** The toolchain name usually includes `default-toolchain...`.
  2. From the toolchain dashboard, open your Node-RED instance by clicking **Routes** and selecting the route link.  
  2. Click **Go to your Node-RED flow editor** to open the editor.
2. Deploy your device.
  1. In the Device Simulator flow, double-click the blue **Send to IBM IoT Platform** node.
  2. Verify that Authentication is set to **Bluemix Service**.
  3. Enter the **Device Type** and **Device ID** of your device and click **Done**.
  4. Deploy the device by clicking **Deploy**.
3. Configure the Node-RED Temperature Monitor flow.
  1. In the Device Simulator flow, double-click the blue **IBM IoT App In** node .
  2. In Authentication, select **Bluemix Service**.
  3.	Select **All** for Device Type, Device ID, Event, and Format.
  4.	Click **Done**.
  5.  Deploy your monitor by clicking **Deploy**.
4. Validate the device connection.
  1.	Open the {{site.data.keyword.iot_short_notm}} dashboard.  
**Tip:** If the {{site.data.keyword.iot_short_notm}} dashboard is not already open in another tab, return to your {{site.data.keyword.Bluemix_notm}} dashboard, click the name of your {{site.data.keyword.iot_short_notm}} instance, and then click **Launch Dashboard**.
  2. From the main menu, select **Devices**.
  3. Click the name of the device that you added.   
The device information displays the connection status of your device.
  4.	In your Node-RED flow editor, double-click the **Send Data** node, set the Repeat value to **Interval**, and set the frequency to every `3` seconds.
  5. Click **Done**.
  6. Deploy your changes by clicking **Deploy**.  
The payload contains data points, such as those shown in the following example:
```
{"d":{"temp":15,"humidity":50,"location":{"longitude":-98.49,"latitude":29.42}}}
```
  7. Optional: Open the Debug tab to verify that messages are being created.
    1. From the menu that is located in the heading section, select **View**.
    2. Select **Show Sidebar**.
    3. Click the Debug tab to see messages.
  8. In the {{site.data.keyword.iot_short_notm}} Device Information page, verify that you see data points from the device in the Sensor Information section.


## Step 4: Create cards in {{site.data.keyword.iot_short_notm}} to show live data  
{: #createcards}  
Create a board and cards to display device data in the {{site.data.keyword.iot_short_notm}} dashboard. For more information about boards and cards, see [Visualizing real-time data by using boards and cards](https://console.ng.bluemix.net/docs/services/IoT/data_visualization.html).

1. Create a board
  1. Open the {{site.data.keyword.iot_short_notm}} dashboard.  
  **Tip:** If the {{site.data.keyword.iot_short_notm}} dashboard is not already open in another tab, return to your {{site.data.keyword.Bluemix_notm}} dashboard, click the name of your {{site.data.keyword.iot_short_notm}} instance, and then click **Launch Dashboard**.  
  2. Create a board to contain the cards for your simulated devices.
    1. If the All Boards, page is not already displayed, select **Boards** from the {{site.data.keyword.iot_short_notm}} dashboard main menu, and then click **Create New Board**.
    2. Enter a name for the board (for example `Home Environment`) and click **Next**.
    3. On the next page, click **Submit**.  
  3. Click the board that you just created to open it.
2. Create a card to display temperature
  1. Click **Add New Card**, and then select the **Line chart** card type from the Devices section.
  2. Select your device from the devices list, then click **Next**.
  3. Click **Connect new data set**.
  4. In the Create Value Card page, select or enter the following values and click **Next**.
    - Event: update
    - Property: temp
    - Name: Temperature
    - Type: Float
    - Unit: °C
    - Precision: 2
    - Min: 0
    - Max: 50
  5. In the Card Preview page, select **L** for the line chart size, and click **Next**.
  6. In the Card Information page, change the name of the card to **Temperature** and click **Submit**.   
The temperature card appears on the dashboard and includes a line chart of the live temperature data.
3. Create a card to display humidity
  1. Click **Add New Card**, and then select the **Gauge** card type from the Devices section.
  2. Select your device from the list, then click **Next**.
  3. Click **Connect new data set**.
  4. In the Create Value Card page, select or enter the following values and click **Next**.
  Event: update
     - Property: humidity
     - Name: Humidity
     - Type: Float
     - Unit: %
     - Precision: 1
     - Min: 10
     - Max: 95
  5. In the Card Preview page, select **M** for the gauge size, and click **Next**.
  6. In the Card Information page, change the name of the card to **Humidity** and click **Submit**.   
The humidity card appears on the dashboard and includes a gauge that shows the live humidity data.  

<!-- 4. Create a card to display location
  1. Click **Add New Card**, and then select the **Value** card type, which is located in the Devices section.
  2. Select your device from the list, then click **Next**.
  3. Click **Connect new data set**.
  4. In the Create Value Card page, select or enter the following values.
     - Event: update
     - Property: location.latitude
     - Name: Latitude
     - Type: Float
     - Unit: "°N"
     - Precision: 2
     - Min: -180
     - Max: 180
  5. Click **Connect new data set**.
  6. In the Create Value Card page, select or enter the following values and click **Next**.
     - Event: update
     - Property: location.longitude
     - Name: Longitude
     - Type: Float
     - Unit: "°E"
     - Precision: 2
     - Min: -180
     - Max: 180
  7. In the Card Preview page, select **M** as the text size, and click **Next**.
  8. In the Card Information page, change the name of the card to **Location** and click **Submit**.   
The location card appears on the dashboard and shows the live latitude and longitude of the device.-->

## What's next  
{: #whats-next}  
Now that your simulated device is sending data to {{site.data.keyword.iot_short_notm}}, you can continue to iterate on your IoT project.
 - Watch your cards display the data that is generated by your node-RED flow.  
Node-Red continues to send data until you stop it. To stop the simulated data, perform the following steps:
    1.	In your Node-RED flow editor, double-click the gray **Send Data** node, set the Repeat value to **Interval**, and set the frequency to every **3** seconds.
    2. Click **Done**.
    3. Deploy your changes by clicking **Deploy**.

 - Connect a physical device.  
[Search the IoT Recipes](https://developer.ibm.com/recipes/?post_type=tutorials&s=watson+iot) to connect a physical device such as a Raspberry Pi and send data to {{site.data.keyword.iot_short_notm}}.

 - Explore visualization options.  
[Deploy a sample node.js application to visualize device data.](https://www.bluemix.net/docs/services/IoT/visualizingdata_sample.html).

 -	Password protect the Node-RED flow editor.   
By default, the editor is open for anyone to access and modify flows. To password-protect the editor, perform the following tasks:
    1.	In the {{site.data.keyword.Bluemix_notm}} dashboard, click the name of your Starter application to open the application pages.
    2. Click **Runtime** to display the Runtime page.
    3. Click **Environment variable** to display the Environment Variables page.
    4. In the **User Defined** section, click **Add** and then enter the following user-defined variables:
         -	NODE_RED_USERNAME - the user name to secure the editor
         -	NODE_RED_PASSWORD - the password to secure the editor
    3.	Click **Save**.
