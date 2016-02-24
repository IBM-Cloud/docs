{:shortdesc: .shortdesc}

# Connecting and viewing your devices {: #devices}

{{site.data.keyword.iotrtinsights_short}} uses {{site.data.keyword.iot_short}} for device access and data retrieval. Devices that you connect to {{site.data.keyword.iot_short}} are automatically connected to {{site.data.keyword.iotrtinsights_short}}.
{: shortdesc}

If you are connecting a new type of device, you must also configure the message schema to map the device data points, set the units, and name the device type. If your devices are of an already configured device type, their data automatically shows up in the dashboard.

To add a new device:  
Adding a new device is a two-step process. First, you add the device to {{site.data.keyword.iot_short}}, and then you configure how {{site.data.keyword.iotrtinsights_short}} consumes and displays the device data.
1. Add devices to your {{site.data.keyword.iot_short}}.
> **Tip:** If you deployed the Internet of Things phone application, an iotphone device is already added to the *iot-phone-iotf-service* {{site.data.keyword.iot_short}} and you can skip this step.  

  To add new devices to your {{site.data.keyword.iot_short}}, see the [{{site.data.keyword.iot_full}} documentation](https://www.ng.bluemix.net/docs/services/IoT/index.html) and the [{{site.data.keyword.iot_short}} device connection recipes](https://developer.ibm.com/recipes/?post_type=tutorials&s=IoTF).
2. Configure your device in {{site.data.keyword.iotrtinsights_short}}.  
  1. Log in to the {{site.data.keyword.iotrtinsights_short}} console as an administrator user.
  9. Go to **Devices > Browse devices** and verify that your newly added device is listed.
  > **Tip:** The devices list is refreshed from you data source once per minute. Click **Refresh** to update the devices list right away.
  3. Go to **Devices > Manage Schemas** and click **Add new message schema**.  
  4. Enter a name for the message schema, for example:  
  `New message schema`.
  5. Click **Link new data source** and select the data source and device type that corresponds to your {{site.data.keyword.iot_short}} instance and device. Optionally, enter an event name to collect data for that event only, or leave the `+` wild card to collect all events. More information about how to identify event types for your device is [here](#identify-datapoints "Identify datapoints.").  
  >**Important:** Each message schema must have a unique combination of data source, device type, and event name. To create more than one schema for a specific data source and device type combination, specify a unique event name for each message schema instead of using the default `+` wild card.   
  6. Add one or more data points that you want to include in the device dashboards.  
    You can select data points from a connected device, or add data points manually. The available data points are defined in the payload of the messages that are sent by a device. For information about the {{site.data.keyword.iot_short}} payload format, see the [Message Payload](https://docs.internetofthings.ibmcloud.com/messaging/payload.html "Message Payload.") topic in the {{site.data.keyword.iot_short}} documentation.   
    > **Tip:** You can manually create virtual data points that modify or combine existing data points that are type integer or float. For example, if the device data point temp returns a temperature value in Fahrenheit, and you want to use Celsius instead, you can create a virtual data point *temp_c* with the following function *temp_c=(temp-32)/1.8*. You can then use the virtual *temp_c* data point instead of the real-time *temp* data point in your rule conditions. In the dashboards, virtual data points are identified by a dashed underline.    

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
  <p><b>Tip:</b> To create a [nested data point structure](schemas.html), first add a data point that has the data type Parent. In the data points table, you can then click ![Add child icon.](images/add_child.png "Add child") to add one or more child data points.</p>
  <ol>
    <li>Click **Add manually**.</li>
    <li>Select **Real-time data point** or **Virtual data point**</br></li>
    <li>Define the following data point information:<ul>
    <li> Data point - The data point identifier that you [located in the {{site.data.keyword.iot_short}} dashboard](#identify-datapoints "Identify datapoints."). For example:  
   `id`, `ts`, `lat`  </li>
   <li>Description - A short description of the data point. This description is used when displaying the data points in dashboards.</li>
   <li>Virtual data point function - Add one or more components to define a valid function. You can use data points, numerical values, and mathematical operators such as +, -, \*, /, (, and ) to build your function. </li>
   <li>Data type - The type of data of the data point:  
   `String`, `Integer`, `Float`, or `Parent`.</li>
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
   8. Click **OK** to create the message schema.
   9. Go to **Devices > Browse devices** and click your newly added device to verify that real-time device data is displayed and that the data points are correctly mapped.

## Identifying data points and events in the {{site.data.keyword.iot_short}} dashboard. {: #identify-datapoints}
The data points and event types for a device can be found in the {{site.data.keyword.iot_short}} dashboard.
>**Tip:** If you are using the Internet of Things phone application as your IoT device, you can use the sensorData event and the following data points to configure the message schema:
>- d.id - Device ID
>- d.ts - Timestamp
>- d.lat - Latitude
>- d.lng - Longitude
>- d.ax - X acceleration
>- d.ay - Y acceleration
>- d.az - Z acceleration
>- d.oa - Alpha movement
>- d.ob - Beta movement
>- d.og - Gamma movement  
>Where d.*datapoint* indicates that the data point is nested under a parent type d data point in the message payload.

1. From the Bluemix dashboard, click the Internet of Things tile.  
>**Note:**  If you are using the Internet of Things phone application, click the the *iot-phone-iotf-service* tile.  
2. Click **Launch dashboard** to open the {{site.data.keyword.iot_short}} dashboard.
3. Go to the **Devices** page.
4. Click your device to open the device details page.  
  Scroll down to the **Sensor Information** section to see a list of the available events and data points for the device. This information is required when you configure the device in {{site.data.keyword.iotrtinsights_short}}.
