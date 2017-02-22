---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-03"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Create device type schemas
{: #iotrtinsights_task}

To use {{site.data.keyword.iot_short}} features such as rules and actions, you must create a schema to map device properties to user-friendly properties names, set the data units for the properties, and specify a message type to use with the schema.
{: shortdesc}

**Important:** Schemas are required to use rules and actions. For information, see [Cloud Analytics](cloud_analytics.html#rules).

**Important:** The analytics features are merged in from the {{site.data.keyword.iotrtinsights_full}} service. If your {{site.data.keyword.iot_short_notm}} organization is used as a data source for an existing {{site.data.keyword.iotrtinsights_short}} instance, Cloud and Edge Analytics is not enabled until after the existing {{site.data.keyword.iotrtinsights_short}} instances have been migrated. Continue to use the {{site.data.keyword.iotrtinsights_short}} dashboard for your analytics needs until the migration is complete. For more information, see the [IBM Watson IoT Platform blog ![External link icon](../../icons/launch-glyph.svg)](https://developer.ibm.com/iotplatform/2016/04/28/iot-real-time-insights-and-watson-iot-platform-a-match-made-in-heaven/){: new_window} on IBM developerWorks and your existing {{site.data.keyword.iotrtinsights_short}} instance dashboards.  

## Adding a device schema
{: #add_schema}

To add a schema:  
1. Go to **Devices > Manage Schemas** and click **Add Schema**.  
2. Select a device type to associate with this message schema. **Important:** Only one schema can be defined for a device type.

3. Add one or more properties.  
    You can select properties from a connected device, create virtual properties that modify or combine existing properties, or add properties manually.  

    **Tip:** The available properties are defined in the payload of the messages that are sent by a device. For information about the {{site.data.keyword.iot_short}} payload format, see the [Message payload](reference/mqtt/index.html#message-payloadl "Message payload.") topic.   
  <dl>
  <dt>Add a property manually</dt>
  <p><b>Tip:</b> To create a nested property structure, first add a property that has the data type Parent. In the properties table, you can then click ![Add child icon.](images/add_child.png "Add child") to add one or more child properties.</p>
  <dd>
  <ol>
    <li>Select the **Manual** tab.</li>
    <li>Define the following property details:
    <ul>  
      <li>Name - A descriptive name for the property that is used in {{site.data.keyword.iot_short}} dashboards, menus, and wizards.</li>
      <li>Data type - The type of data of the property:  
   `String`, `Integer`, `Float`, or `Parent`.</li>
   <!--<li>Event - A specific event to collect data for. Leave blank to collect for all events.</li>-->
   <li>Property - The property identifier, for example:  
 `temp` or `speed`  </br> For information on how to identify the properties from the device messages, see [Identifying properties for your devices](#identify-datapoints "Identify properties.").</li>
  <li>Data unit - Optional: The unit of data of the property. For example:  
     `C` or `Mph`  </li>
     <li> Decimal places - Optional, float only: The number of decimals to include in the device data.</li>
    </ul>
    </li>
    <li>Click **Finish** to create the property.</li>
  </ol>
  </dd>
  <dt>Create a virtual property</dt>
  <dd> For example, if the device property temp returns a temperature value in Fahrenheit, and you want to use Celsius instead, you can create a virtual property *temp_c* that has the following function *temp_c=(temp-32)/1.8*. You can then use the virtual *temp_c* property instead of the real-time *temp* property in your rule conditions.  
  To create a virtual property:
  <ol>
    <li>Select the **Virtual Property** tab.</li>  
    <li>Define the following property details:
    <ul>
    <li>Name - A descriptive name for the property that is used in {{site.data.keyword.iot_short}} dashboards, menus, and wizards.</li>
    <li>Data type - The type of data of the property:  
 `Float` or `Integer`.</li>
 <li>Property - A property identifier for the virtual property. For example:  
`temp_virt`</li>
    <li>Calculation - Add one or more components to define a valid function. You can use properties, numerical values, and mathematical operators such as +, -, \*, /, (, and ).  
    Click **Advanced** for a set of formulas for use with series of datapoints on edge devices. For more information about the advanced formulas, see [Advanced calculations for edge virtual properties](im_vir_calculations.html).  
    **Important:** Rule conditions that compare virtual properties based on advanced formulas are not supported.</li>
    <li>Data unit - Optional: The unit of data of the property. For example: `C` or `Mph`</li>
    <li> Decimal places - Optional, float only: The number of decimals to include in the device data.</li>
   </ul>
   </li>
   <li>Click **Finish** to create the property.</li>
  </ol>
  </dd>
  <dt>Select properties from a connected device</dt>
  <dd>
  <ol>
    <li>Select the **From Connected** tab.</li>  
    <li>Select one or more properties to add to the schema. These properties can later be edited to set attributes, such as name and data unit.  
<!--**Important:** Each property must be unique for a schema. If you select multiple occurrences of the same property for different events, only one of the selected properties is added to the schema.</li>-->
  <li>Click **OK** to create the properties.</li>
  </ol>
  </dd>
    <dd>The selected properties are added and the description is set to the name of the property. Click the property in the list to edit it, and add additional attributes, such as sensor type, data type, and number of decimal places.</dd>
  </dl>
8. Click **Finish** to create the message schema.

## Identifying properties for your devices.
{: #identify-datapoints}
   The properties for a device can be found in the {{site.data.keyword.iot_short}} dashboard.

1. In the {{site.data.keyword.iot_short}} dashboard, go to **Devices**.
2. Click a device to open a page that shows details for the device.
3. Scroll down to the **Sensor Information** section to see a list of the available properties for a connected device.
