---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-30"
---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!--ATTENTION WRITERS: IMPORTANT. These two topics are closely related: iot500.md and start_iot.md. The reason is that start_iot is displayed as the Getting Started information within the Starter app and NOT in the product docs. UPDATES MIGHT BE NEEDED IN BOTH TOPICS.  -->

# Getting started with {{site.data.keyword.iot_short_notm}} Starter
{: #gettingstartedtemplate}

Get started with {{site.data.keyword.iot_full}} by using the {{site.data.keyword.iot_short_notm}} Starter boilerplate. By using the Starter, you can quickly simulate a device, create cards, generate data, and begin analyzing and displaying data in the {{site.data.keyword.iot_short_notm}} dashboard.
{:shortdesc}

The Starter automatically deploys and connects these services:

- **{{site.data.keyword.iot_short_notm}}** - An IoT toolkit that includes gateway management, device management, and application access. By using {{site.data.keyword.iot_short_notm}}, you can collect connected device data and run analytics on real-time data from your organization.

- **{{site.data.keyword.sdk4nodefull}}** - The runtime environment in which Node-RED runs.

- **{{site.data.keyword.cloudantfull}}** - The database in which Node-RED stores metadata.

- **Node-RED application** - An instance of the Node-RED application that includes nodes designed for {{site.data.keyword.iot_short_notm}}.

## Getting Around
{: #gettingaround}
To make moving between tasks easier, open the {{site.data.keyword.Bluemix_notm}} dashboard, the {{site.data.keyword.iot_short_notm}} dashboard, and the Node-RED application in three different tabs in your browser.
  - *{{site.data.keyword.Bluemix_notm}} dashboard* - See the state of your deployment, read documentation, and launch the dashboards.
  - *{{site.data.keyword.iot_short_notm}} dashboard* - Define device types, register devices, monitor incoming sensor data, create data visualization cards, and see live data visualizations.
  - *Node-RED* - Configure and run the device simulator flow and work with other flows to process data from {{site.data.keyword.iot_short_notm}}.

## Defining a simulated device in {{site.data.keyword.iot_short_notm}}
{: #definingsimdev}
Complete the following steps to simulate a scenario that uses a thermostat to monitor temperature, humidity, and location of a living room.

  1.	Launch the {{site.data.keyword.iot_short_notm}} dashboard.
    1. Scroll to the Services section and click the name of your {{site.data.keyword.iot_short_notm}} instance. The instance name usually ends with *-iotf-service*.
    2. Click **Launch Dashboard** to open the {{site.data.keyword.iot_short_notm}} dashboard in a new browser tab. The `All Boards` page is displayed by default.
  2. Create a device type.
    1.	From the main menu, select **Devices**, and then click **Add Device**.
    2.	In the Add Device page, click **Create device type**.
    3.	In the Create Device Type page, click **Create device type**.
    4. Enter a unique name and description for your device, and click Next.
    5. (optional) Defining a Template and Metadata on the next two pages is optional and can be safely skipped by clicking Next on each page.
    6.	Click Create to add the device type.
  3.	Add a device that uses the newly created device type.
    1. On the Add Device page, the device type that you just created is displayed in the list of device types. Click **Next** to add a device that uses that device type.
    2. Enter a unique device ID (for example, LivingRoomThermo1).
    3. (optional) Providing descriptive data on the Add Device page or entering device metadata on the next page is optional, and you can safely skip those pages by clicking Next on each page.
    4. On the Security page, click **Next** to generate an authentication token for your device.
    5. On the Summary page, verify that the information is correct and click **Add** to add the device. Click **Back** to return to a previous page.
  4.	Make a note of the information that is displayed in the Your Device Credentials page. You need the following information to configure the simulator and display the data:
      -	Organization ID
      -	Device Type
      -	Device ID
      - Authentication Method
      - Authentication Token

## Configuring and running the Node-RED device simulator.
{: #confignodered}
Configure the Node-RED device simulator. Use the device simulator to send MQTT device messages to {{site.data.keyword.iot_short_notm}}. The device simulator sends temperature and humidity information to {{site.data.keyword.iot_short_notm}}.

  1. Launch the Node-RED flow editor.
    1. From your {{site.data.keyword.Bluemix_notm}} dashboard, open your Node-RED instance by clicking the **Route** link that is listed for your {{site.data.keyword.iot_short_notm}} Starter app.  
    2. Click **Go to your Node-RED flow editor** to open the editor.
  2. Deploy your device.
    1. Double-click the blue **Send to {{site.data.keyword.iot_short_notm}}** node in the Device Simulator flow.
    2.	Verify that Authentication is set to **Bluemix Service**.
    3.	Enter the **Device Type** and **Device ID** of your device and click **Done**.
    4. Deploy the device by clicking **Deploy**.
  3. Configure the Node-RED Temperature Monitor flow.
    1.	Double-click the blue **IBM IoT App In** node in the Device Simulator flow.
    2.	In Authentication, select **Bluemix Service**.
    3.	Select **All** for Device Type, Device ID, Event, and Format.
    4.	Click **Done**.
    5.  Deploy your monitor by clicking **Deploy**.
  4. Validate the device connection.
    1.	Open the {{site.data.keyword.iot_short_notm}} dashboard.

      **Tip:** If the {{site.data.keyword.iot_short_notm}} dashboard is not already open in another tab, return to your {{site.data.keyword.Bluemix_notm}} dashboard, click the name of your {{site.data.keyword.iot_short_notm}} instance, and then click **Launch Dashboard**.

    2.	From the main menu, select **Devices**.
    3. Click the name of the device that you added. The device information displays the connection status of your device.
    4.	In your Node-RED flow editor, double-click the gray **Send Data** node, set the Repeat value to **Interval**, and set the frequency to every **3** seconds.
    5. Click **Done**.
    6. Deploy your changes by clicking **Deploy**.

      The payload contains data points, such as those shown in the following example:
  ```
  {"d":{"temp":15,"humidity":50,"location":{"longitude":-98.49,"latitude":29.42}}}
  ```
    7. (optional) Open the Debug tab to verify that messages are being created.
      1. From the menu that is located in the heading section, select **View**.
      2. Select **Show Sidebar**.
      3. Click the Debug tab to see messages.
    8.	In the {{site.data.keyword.iot_short_notm}} Device Information page, verify that you see data points from the device in the Sensor Information section.

## Display live data in {{site.data.keyword.iot_short_notm}}
{: #createcards}
Create a board and cards to display device data in the {{site.data.keyword.iot_short_notm}} dashboard. For more information about boards and cards, see [Visualizing real-time data by using boards and cards](https://console.ng.bluemix.net/docs/services/IoT/data_visualization.html).

### Create a board
{: #createboard}

  1.	Open the {{site.data.keyword.iot_short_notm}} dashboard.

  **Tip:** If the {{site.data.keyword.iot_short_notm}} dashboard is not already open in another tab, return to your {{site.data.keyword.Bluemix_notm}} dashboard, click the name of your {{site.data.keyword.iot_short_notm}} instance, and then click **Launch Dashboard**.  
  2. Create a board to contain the cards for your simulated devices.
    1. If the All Boards, page is not already displayed, select **Boards** from the {{site.data.keyword.iot_short_notm}} dashboard main menu, and then click **Create New Board**.
    2. Enter a name for the board (for example, Home Environment) and click **Next**.
    3. On the next page, click **Create**.  
  3. Double-click the board that you just created to open it.

### Create a card to display temperature
{: #cardtemp}
  1. Click **Add New Card**, and then select the **Line Chart** card type, which is located in the Devices section.
  2. Select your device from the list, then click **Next**.
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
  6. In the Card Information page, change the name of the card to **Temperature** and click **Submit**. The temperature card appears on the dashboard and includes a line chart of the live temperature data.

### Create a card to display humidity
{: #cardhumidity}
  1. Click **Add New Card**, and then select the **Gauge** card type, which is located in the Devices section.
  2. Select your device from the list, then click **Next**.
  3. Click **Connect new data set**.
  4. In the Create Value Card page, select or enter the following values and click **Next**.
     - Event: update
     - Property: humidity
     - Name: Humidity
     - Type: Float
     - Unit: %
     - Precision: 1
     - Min: 10
     - Max: 95
  5. In the Card Preview page, select **M** for the gauge size, and click **Next**.
  6. In the Card Information page, change the name of the card to **Humidity** and click **Submit**. The humidity card appears on the dashboard and includes a gauge that shows the live humidity data.  

### Create a card to display location
{: #cardlocation}
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
  7. In the Card Preview page, select **L** as the text size, and click **Next**.
  8. In the Card Information page, change the name of the card to **Location** and click **Submit**. The location card appears on the dashboard and shows the live latitude and longitude of the device.

## What's next?
{: #whatsnext}
Now that your simulated device is sending data to {{site.data.keyword.iot_short_notm}}, you can continue to iterate on your IoT project.

  - Watch your cards display the data that is generated by your node-RED flow. Node-Red continues to send data until you stop it. To stop the simulated data, perform the following steps:
    1.	In your Node-RED flow editor, double-click the gray **Send Data** node, set the Repeat value to **Interval**, and set the frequency to every **3** seconds.
    2. Click **Done**.
    3. Deploy your changes by clicking **Deploy**.

  - [Search the IoT Recipes](https://developer.ibm.com/recipes/?post_type=tutorials&s=watson+iot) to connect a physical device such as a Raspberry Pi and send data to {{site.data.keyword.iot_short_notm}}.

  - [Deploy a sample node.js application to visualize device data.](https://www.bluemix.net/docs/services/IoT/visualizingdata_sample.html)

  -	Password protect the Node-RED flow editor. By default, the editor is open for anyone to access and modify flows. To password-protect the editor, perform the following tasks:
    1.	In the {{site.data.keyword.Bluemix_notm}} dashboard, click the name of your Starter application to open the application pages.
    2. Click **Runtime** to display the Runtime page.
    3. Click **Environment variable** to display the Environment Variables page.
    4. In the **User Defined** section, click **Add** and then enter the following user-defined variables:
         -	NODE_RED_USERNAME - the user name to secure the editor
         -	NODE_RED_PASSWORD - the password to secure the editor
    3.	Click **Save**.

# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}
* [Recipes for connecting your devices](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window}
* [{{site.data.keyword.iot_short}} Play organization](https://play.internetofthings.ibmcloud.com/){:new_window}
* [Connecting an Intel Galileo to the {{site.data.keyword.iot_short}}](https://developer.ibm.com/recipes/tutorials/connect-an-intel-galileo-to-the-internet-of-things-foundation-connect/){:new_window}
* [Connecting an ARM&reg; mbed&trade; IoT Starter Kit](https://developer.ibm.com/recipes/tutorials/arm-mbed-iot-starter-kit-part-1/){:new_window}
* [Connecting a Raspberry Pi to {{site.data.keyword.iot_short}}](https://developer.ibm.com/recipes/tutorials/raspberry-pi-4/){:new_window}

## API Reference
{: #api}
* [{{site.data.keyword.iot_short}} API Documentation](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/){:new_window}


## Related Links
{: #general}
* [{{site.data.keyword.iot_short_notm}} Documentation](https://www.bluemix.net/docs/services/IoT/iotplatform_overview.html){:new_window}
* [{{site.data.keyword.sdk4nodefull}} starter documentation](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html){:new_window}
