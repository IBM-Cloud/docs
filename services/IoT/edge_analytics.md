---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Edge analytics
{: #edge_analytics}

With edge analytics, you move the analytics rule-triggering process from the cloud to an edge analytics enabled gateway that might dramatically reduce the amount of device data traffic to the cloud by doing the analytics processing close to the device.
{:shortdesk}

Devices send their data to an edge analytics enabled gateway where edge analytics rules parse the data. Depending on your rule and its action, critical data and alerts might be sent to {{site.data.keyword.iot_full}}, trigger an alert on the gateway, or be written to a text file that is local to the gateway.

The following diagram illustrates the general architecture of an {{site.data.keyword.iot_full}} edge analytics environment.
![IBM Watson IoT Platform for edge analytics architecture](images/architecture_platform_edge.svg "IBM Watson IoT Platform withe edge analytics architecture")

## Before you begin
{: #byb}

Before you begin creating edge rules and actions:
- Make sure that your gateway is connected to {{site.data.keyword.iot_short}} and that device data is being transmitted. See [Connecting gateways](gateways/dashboard.html) for more information.
- Install the Edge Analytics Agent (EAA) on your gateway. For information, see [Installing the edge analytics agent](gateways/dashboard.html#edge). </br> **Tip:** EAA-enabled gateways provide EAA diagnostic data in the form of gateway device messages. For information, see [Edge Analytics Agent diagnostic metrics](#eaa_metrics).
- Make sure that the device properties that you want to use as conditions in your rules are mapped to schemas. See [Connecting devices](iotplatform_task.html) and [Creating schemas](im_schemas.html) for more information.
- Review Edge Analytics recipes  
In our Recipes portal, a couple of recipes describe the steps that are required to carry out IBM Edge Analytics. The recipes clearly describe about how to install and configure IBM Edge Analytics Agent on a device that is built on top of Apache Edgent to run analytics close to an IoT data source.
 - [Getting Started with Edge Analytics in IBM Watson IoT Platform ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/getting-started-with-edge-analytics-in-watson-iot-platform/){: new_window} recipe is the beginning of this series. This recipe describes setting up Cisco DSA Platform on a Laptop System and Raspberry Pi 3 Device, installing and configuring IBM Edge Analytics Agent to connect to {{site.data.keyword.iot_short}}, installing System DS Link and configuring it to connect to Edge Gateway on {{site.data.keyword.iot_short}} as an attached device, defining and Activating the Edge Rule on the Edge Gateway, and the management of the Edge Rule from {{site.data.keyword.iot_short}}.
 - To illustrate an advanced usage of Edge Analytics, the [Handling Alerts and Device Actions with Edge Analytics in IBM Watson IoT Platform ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/handling-alerts-and-device-actions-with-edge-analytics-in-ibm-watson-iot-platform/){: new_window} recipe showcases how to build your own DS Link to transfer data from a connected Arduino Uno device to a Raspberry Pi 3 device. The recipe also showcases data filtering and handling local device actions as part of the Edge Rule alert.

## Managing edge rules and actions  
{: #managing_rules}

Edge rules are managed by using the following:
- The **Rules** dashboard is used to create and edit cloud and edge rules and actions for your devices and gateways.
- The **Edge Rules Gateways** board is used to activate, deactivate, update, and remove an edge rule on your gateways. To access the Edge Rules Gateways board, from the Rules dashboard click **Manage Rule** for the edge rule that you want to manage. For more information, see [ Activating, deactivating, and managing edge rules for your gateways](#manage).

To get an overview of edge rules and alerts that have been triggered for your gateway-connected devices, use the following boards:

|Board Name | Description |  
 |:---|:---|  
  |Rule-Centric Analytics | Shows the rules for your organization, including edge rules. Additional cards list forwarded edge alerts, associated devices, device properties, and forwarded edge alert information. |  
 |Device-Centric Analytics | Shows the devices that are connected to your organization. Additional cards show forwarded alerts for a selected edge device, information for a selected device, device properties, and forwarded alert information. |

For more information about the default analytics boards, see [Visualizing real-time data by using boards and cards](data_visualization.html#default_boards).


## Creating edge rules
{: #rules}

Edge rules are condition-based decision points that match real-time device data with predefined threshold values or other property data to trigger an edge action if a condition is met.

**Important:** Before you can create rules for a device type, you must create a schema for the device type. For information, see [Create device type schemas](im_schemas.html).

To create a rule:
1. In the {{site.data.keyword.iot_short}} dashboard, go to **Rules**.
2. Click **Create Edge Rule**, give the rule a name, provide a description, select an edge device type that the rule applies to, and then click **Next**.  
3. Set up the rule logic.  
Add one or more IF conditions to use as triggers for the rule.  
You can add conditions in parallel rows to apply them as OR conditions, or you can add conditions in sequential columns to apply them as AND conditions.  
**Note:** To be able to select a device property as input for a rule, the property must be mapped to a schema. See [Creating schemas](im_schemas.html) for more information.  

**Important:** To trigger a condition that compares two properties or to trigger two or more property conditions that are combined sequentially by using AND, the triggering data points must be included in the same device message. If the data is received in more than one message, the condition or sequential conditions do not trigger.  

**Examples:**   
A simple rule might trigger an alert if a parameter value is larger than a specified value:  
`temp>80`  
A more complex rule might trigger when a combination of thresholds is met:  
`temp>60 AND capacity>50`   

4. Configure conditional trigger requirements for your rule.  
To control the number of alerts and actions that are triggered for a rule over a time period, you can configure conditional trigger requirements for your rule.  
**Important:** The conditional triggering acts on any condition in the rule. For example, if a rule has five different parallel conditions set by using OR, each condition that is true counts towards the conditional trigger count.
To set conditional triggering for a rule:
 1. In the rule editor, click the default **Trigger each time conditions are met** link to open the set frequency requirement dialog box.
 2. Select and configure the conditional trigger that you want to use in the rule.
 <ul>
 <li>Trigger every time conditions are met</li>
 <li>Trigger if conditions are met N times in M *Unit of time*</li>
 </ul>  
 For a more detailed description of the conditional triggers, see [Conditional rule triggering](cloud_analytics.html#conditional "Conditional triggering overview") in the cloud analytics section.
5. Create or select one or more actions that occur if the rule conditions are met.  
For more information about edge actions, see [Creating edge actions](#edge_actions "Create edge actions").   
 Example: An action can be to send device data to the cloud or write an alert to a local file.
3. **Optional:** Select an alert priority for the rule.  
 The priority is used to classify the alerts that are displayed in the **Rule-Based Analytics** board. The default priority is Low.
6. When you are satisfied with your rule, click **Save**.

Your rule is created and is added to the browse dashboard. You can now [activate](#manage) the rule from the **Edge Rules Gateways** board that opens.


## Creating edge actions
{: #edge_actions}

You can create actions directly in the rule editor or create the actions in the Actions tab and then select the actions when you create your rules.

To create an action on the Actions tab:
1. In the {{site.data.keyword.iot_short}} dashboard, go to **Rules**.
2. In the Rules dashboard, select the **Actions** tab.
2. Click **Create An Action**, give the action a name and a description and select an action type, then click **Next**.  
Edge analytics supports two action types:
<dl>
<dt>Forward event to cloud</dt>  
<dd>The device event is sent to {{site.data.keyword.iot_short}} where it can be used in boards and cards and with cloud analytics rules. For information, see [Integrating with cloud analytics](#integrate_with_cloud_analytics).    
**Tip:** Use the forward event cloud action to reduce the amount of device data that is sent to the cloud by filtering out the less important data directly at the gateway device. </dd>
<dt>Alert</dt>  
<dd>An alert is created on the gateway device.</dd>
</dl>
3. Provide the required parameters for the type of action that you selected.  
<dl>
<dt>Forward event to cloud</dt>  
<dd>Select the event data to forward to the cloud and provide the event name to use in the message. </br>
**Tip:** You can use the event and properties when setting up boards and cards and when creating cloud analytics rules.</br>
You can:
 <ul>
 <li>Include all device properties and virtual properties
 <li>Include only schema-defined properties and virtual properties  
 </ul>
 </dd>
<dt>Alert</dt>  
<dd>Specify an alert message and select at least one destination for the alert.
 <ul>
 <li>Forward to cloud  
 The alert is forwarded to {{site.data.keyword.iot_short}} where it is displayed in the Rule-Centric Analytics and Device-Centric Analytics boards.
 <li>Publish to gateway broker
 The alert is published to the gateway broker. The broker configuration determines how the alert is surfaced to a user.
 <li>Save to a local text file
 The alert is appended to the local *IBMEdgeAnalyticsAlerts.csv* text file on the gateway server.
 </ul>
 </dd>
</dl>
4. Click **OK** to create the new action.

The action is now available in the rule editor.


## Activating, deactivating, and managing edge rules for your gateways
{: #manage}

For a rule to trigger actions you must first activate it on one or more gateways. You use the **Edge Rules Gateways** board to activate, deactivate, update, and remove an edge rule on your gateways.

To activate an edge rule:
1. From the Rules dashboard, click the **Manage Rule** button for the edge rule that you want to manage.  
In the **Edge Rules Gateways** board that opens you see a list of all connected EAA-enabled gateways. The rule status for gateways where the rule is not uploaded and activated is *None*.
2. Locate the gateway on which you want to activate the rule, and select **Activate** from the menu in the Select operation column.  
The edge rule is uploaded to the gateway. When the upload is complete and the rule is active, the Rule status changes to **Active**.  

The rule is now active on the gateway, and the configured actions will trigger when the rule conditions are met.

**Tip:** To manage rules on multiple gateways you can select the select-all box next to the Gateway column header. Clear any gateways that you do not want to include and then pick an operation from the **Select operation** menu at the top of the column with the same name.

In addition to activating a rule you can perform the following rule management operations on your gateways:

Operation | Description
--- | ---
Activate | Uploads and activates the rule on the selected gateways. The rule status is set to *Active*.
Deactivate | Deactivates the rule on the selected gateways. The rule remains on the gateway and can be reactivated if needed. The rule status is set to *Inactive*.
Update | Uploads an updated version of the rule to the selected gateways. Use this operation to bring a gateway up to date if the rule status for the gateway is *Active (Older)*. The rule status is set to *Active*.
Remove | Removes the rule from the selected gateways. The rule status for the gateway reverts to *None*.


## Integrating with cloud analytics
{: #integrate_with_cloud_analytics}

Use the edge rule triggered actions that are run on the EAA-enabled gateway to filter the data that flows to the cloud and forward gateway generated alerts to the cloud to use with {{site.data.keyword.iot_short}} boards and cards.  

You can also use {{site.data.keyword.iot_short}} to do cloud analytics on device data that is sent to the cloud from the gateway. If you use the `Forward event to cloud` action in your edge rule, the created message can be used as input for a cloud analytics rule, just as if the device that provided the data that triggered the edge rule was connected directly to {{site.data.keyword.iot_short}}.

For more information on how to create cloud analytics rules and actions, see [Cloud Analytics](cloud_analytics.html).

## Edge Analytics Agent diagnostic metrics
{: #eaa_metrics}

A connected EAA-enabled gateway sends diagnostic information as device messages of the event type `gateway_xv-monitor-event`. </br> **Tip:** You can use [cloud analytics](cloud_analytics.html) rules to configure alert actions such as email notifications based on the diagnostic values that are sent back by the EAA-enabled gateway. For example, you can create a rule to alert you if the `SystemLoad` exceeds a certain threshold.

To see information about the state of the gateway:
1. In the {{site.data.keyword.iot_short}} dashboard select **Devices** in the menu side bar.
2. Click your gateway device to open the device details page.
3. Access the gateway diagnostic information:  
 - See the **Recent Events** section for a list of recent messages that were sent by the gateway.
 - See the **Diagnostic logs** section for any gateway warnings and other diagnostic messages.
 - See the **Sensor information** section for detailed diagnostic information from the gateway. The following table describes the different properties that might be included in the gateway device messages.


 Property | Description
 --- | ---
 `MsgInCount` |The number of messages that were sent to the Edge Analytics Agent (EAA).
 `MsgInRate` | The estimated number of messages per second that were sent to the EAA during the last time minute.  
 `LastHeartBeat` | The millisecond timestamp when the last heart beat message was generated. A heart beat message is generated every 10 seconds at minimum.
 `CurrentTimestamp` | The milliseconds timestamp when the current monitoring message was generated.
 `IsAlive` | This property is 0 if the difference between `LastHeartBeat` and `CurrentTimestamp` is greater than 20 seconds.
 `BytesOutCount` | The number of message bytes that are sent by the EAA to {{site.data.keyword.iot_short}}.
 `BytesOutRate` | The estimated number of message bytes per second that were sent by the EAA to {{site.data.keyword.iot_short}} during the last minute.
 `BytesInCount` | The number of message bytes that were sent by {{site.data.keyword.iot_short}} to the EAA.
 `BytesInRate` | The estimated number of message bytes per second that that were sent by {{site.data.keyword.iot_short}} to the EAA in the last minute.
 `RuleBytesInCount` |The number of message bytes that were sent to the EAA rule engine core. </br> **Note:** If no rule is set for a device type, messages for that device type are not sent to the rule engine core.
 `RuleBytesInRate` | The estimated number of message bytes per second that were sent to the EAA rule engine core during the last minute.
 `MsgOutCount` | The number of messages that were sent by the EAA to {{site.data.keyword.iot_short}}.
 `MsgOutRate` | The estimated number of messages bytes per second that are sent by the EAA to {{site.data.keyword.iot_short}} during the last minute.
 `MsgReducePercent` | The percentage difference between incoming and outgoing messages. </br>The following formula is used for the calculation: `(msgIn - msgOut) / msgIn`
 `BytesReducePercent` | The percentage difference between incoming and outgoing bytes. </br>The following formula is used for the calculation: `(bytesIn - bytesOut) / bytesIn`
 `MsgRateReduce` | The percentage difference between incoming and outgoing message rate. </br>The following formula is used for the calculation: `(msgInRate - msgOutRate) / msgInRate`
 `BytesRateReduce` | The percentage difference between incoming and outgoing messages bytes. </br>The following formula is used for the calculation: `(bytesInRate - bytesOutRate) / bytesInRate`
 `SystemLoad` | The current system load for the on the system where the EAA is running. **Note:** The CPU rate will be sent only if the `mpstat` command is available on the system where the EAA is running. Otherwise, the system load average for the last minute is sent. </br>“The system load average is the sum of the number of runnable entities queued to the available processors and the number of runnable entities running on the available processors averaged over a period of time. The way in which the load average is calculated is operating system specific but is typically a damped time-dependent average. If the load average is not available, a negative value is returned. ” - javadoc for _ManagementFactory.getOperatingSystemMXBean_.
 `FreeMemory` | The number of bytes of free memory for the Java™ Virtual Machine (JVM) where EAA is running.
 `MemoryUsed` | The number of bytes of JVM memory that is used by EAA.
 `InQueueSize` | The number of messages that are queued for EAA processing.
 `RuleNumber` | The number of defined rules in the rule engine core.
 `ProcessorNumber` | For debug use. The number of defined processors in the rule engine core. </br>**Note:** A processor is the minimal execution unit in the rule engine core.
 `DataPointsInWindow` | The total number of data points that are buffered in the time window. The byte size of a data point differs depending on its data type. For example, a float/int data point size is 8 bytes whereas a string data point size differs depending on its length.  In most cases you can estimate the memory usage of the time window by using the following formula: `DataPointsInWindow * 8`.

## Edge Analytics community
{: #eaa_community}

You can download the Edge Analytics SDK from the [IBM Edge Analytics community page](https://www.ibm.com/developerworks/community/groups/service/html/communitystart?communityUuid=3df173af-0c21-4b9c-9fd1-e8e5561ef460&ftHelpTip=true). The SDK includes the SDK JAR file, javadoc, sample code, recipe links, and README files. In the community, you can also watch videos to get up and running with Edge Analytics, and you can use the community forum to ask questions.
