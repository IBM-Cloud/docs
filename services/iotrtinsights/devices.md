{:shortdesc: .shortdesc}

# Connecting and viewing your devices {: #devices}

IoT Real-Time Insights uses IoT Foundation for device access and data retrieval. Devices that you connect to IoT Foundation are automatically connected to IoT Real-Time Insights.
{: shortdesc}

If you are connecting a new type of device, you must also configure the message schema to map the device data points, set the units, and name the device type. If your devices are of an already configured device type, their data automatically shows up in the dashboard.

To add a new device:  
Adding a new device is a two-step process. First, you add the device to IoT Foundation, and then you configure how IoT Real-Time Insights consumes and displays the device data.
1. Add devices to your IoT Foundation.
> **Tip:** If you deployed the Internet of Things phone application, an iotphone device is already added to the *iot-phone-iotf-service* IoT Foundation and you can skip this step.  

  To add new devices to your IoT Foundation, see the [Internet of Things Foundation documentation](https://www.ng.bluemix.net/docs/services/IoT/index.html) and the [IoT Foundation device connection recipes](https://developer.ibm.com/recipes/?post_type=tutorials&s=IoTF).
2. Configure your device in IoT Real-Time Insights.  
  1. Log in to the IoT Real-Time Insights console as an administrator user.
  9. Go to **Devices > Browse devices** and verify that your newly added device is listed.
  3. Go to **Devices > Manage Schemas** and click **Add new message schema**.  
  4. Enter a name for the message schema, for example:  
  `New message schema`.
  5. Click **Link new data source** and select the data source and device type that corresponds to your IoT Foundation instance and device. Optionally, enter an event name to collect data for that event only, or leave the `+` wild card to collect all events. More information about how to identify event types for your device is [here](#identify-datapoints "Identify datapoints.").
  6. Add one or more data points that you want to show up in the device dashboards.  
    You can select data points from a connected device, or add data points manually.  
  <dl>
  <dt>Select from connected device</dt>
  <dd>
  <ol>
    <li>Click **Select from connected device**.</li>  
    <li>In the Add data points dialog, select one or more data points to add, and then click **OK**.</li>   
    <li>The selected data points are added with the description set to the name of the data point. Click the data point in the list to edit it, and add additional attributes such as sensor type, data type, and number of decimal places.</li>
  </ol>
  </dd>
  <dt>Add manually</dt>
  <dd>
  <ol>
    <li>Click **Add manually**.</li>
    <li>Define the following data point information:
    <ul>  
    <li> Data point - The data point identifier that you [located in the IoT Foundation dashboard](#identify-datapoints "Identify datapoints."). For example:  
   `id`, `ts`, `lat`  </li>
   <li>Description - A short description of the data point. This description is used when displaying the data points in dashboards.</li>
   <li>Data type - The type of data of the data point:  
   `String`, `Integer`, or `Float`</li>
     <li>Sensor type - Optionally select how to interpret the data point in the dashboards. Depending on the type and sensor type combination, additional visualization options might be available for your dashboard widgets. For more information about sensor types and visualization options, see [Dashboard widgets](dashboards.html#dashboard-widget "Dashboard widgets").</li>
    <li>Data point icon - Optionally select an icon to represent the data point in the dashboard widgets.</li>
    <li>Min value/Max value - Optional, integer and Float only: If a max and min value is entered, device data can be displayed as a gauge in the dashboards.</li>
    <li>Data unit - Optional: The unit of data of the data point. For example:  
     `C`, `Mph`  </li>
     <li> Decimal places - Optional, float only: The number of decimals to include in the device data.</li>
     </ul></li>
     </ol>
    </dd>
  </dl>
   8. Click ![Create icon.](images/create.png "Create icon") to create the message schema.
   9. Go to **Devices > Browse devices** and click your newly added device to  
  verify that real-time device data is displayed and that the data points are correctly mapped.

## Identifying data points and events in the IoT Foundation dashboard. {: #identify-datapoints}
The data points and event types for a device can be found in the IoT Foundation dashboard.
>**Tip:** If you are using the Internet of Things phone application as your IoT device, you can use the the sensorData event and the following data points to configure the message schema:
>- id - Device ID
>- ts - Timestamp
>- lat - Latitude
>- lng - Longitude
>- ax - X acceleration
>- ay - Y acceleration
>- az - Z acceleration
>- oa - Alpha movement
>- ob - Beta movement
>- og - Gamma movement

1. From the Bluemix dashboard, click the Internet of Things tile.  
>**Note:**  If you are using the Internet of Things phone application, click the the *iot-phone-iotf-service* tile.  
2. Click **Launch dashboard** to open the Internet of Things Foundation dashboard.
3. Go to the **Devices** page.
4. Click your device to open the device details page.  
  Scroll down to the **Sensor Information** section to see a list of the available events and data points for the device. This information is required when you configure the device in IoT Real-Time Insights.
