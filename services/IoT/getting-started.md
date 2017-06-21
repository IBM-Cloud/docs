---

copyright:
  years: 2015, 2017
lastupdated: "2017-06-01"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Getting started tutorial
{: #getting-started-with-iotp}

In this {{site.data.keyword.iot_full}} getting started tutorial, we connect an IoT device to {{site.data.keyword.iot_short_notm}} and set up analytics to explore real-time data.
{:shortdesc}

<div id="prerequisites"></div>

## Before you begin
{: #prereqs}

You'll need a [Bluemix account ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/registration/){: new_window},
an instance of the {{site.data.keyword.iot_short_notm}} service, and a device that meets the following requirements:

*	Your device must be able to communicate by using HTTP or MQTT protocols.

* The device messages must conform to the {{site.data.keyword.iot_short_notm}} message payload requirements.

For more information, see [Developing devices on Watson IoT Platform](/docs/services/IoT/devices/device_dev_index.html).

## Step 1: Register your device

You can add devices one at a time from the {{site.data.keyword.iot_short_notm}} dashboard, or you can use the [Watson IoT Platform API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/org-admin.html#!/Device_Bulk_Configuration/post_bulk_devices_add){: new_window} to add multiple devices.

To add a device from the {{site.data.keyword.iot_short_notm}} dashboard:

1. In the {{site.data.keyword.Bluemix_notm}} console, click **Launch** on the {{site.data.keyword.iot_short_notm}} service details page.

    The {{site.data.keyword.iot_short_notm}} web console opens in a new browser tab at the following URL:

    ```
    https://org_id.internetofthings.ibmcloud.com/dashboard/#/overview
    ```

    Where *org_id* is the ID of [your {{site.data.keyword.iot_short_notm}} organization](iotplatform_overview.html#organizations){: new_window}.

2. In the Overview dashboard, from the menu pane, select **Devices** and then click **Add Device**.

3. Create a device type for the device that you are adding.

    Each device that is connected to the {{site.data.keyword.iot_short_notm}} must be associated with a device type. Device types are groups of devices that share common characteristics.

    1. Click **Create device type**.
    2. Enter a device name, such as `my_device_type`, and a description for the device type.
    
        > **Note:** The device type name must be no more than 36 characters and can contain only alpha-numeric characters (a-z, A-Z, 0-9) and any of the following characters: `_`, `.`, and `-`.

    3. Optional: Enter device type attributes and metadata.

        You can add and edit attributes and metadata later.
        {: tip}

4. Click **Next** to begin the process of adding your device with the selected device type.

5. Enter a device ID, for example `my_first_device`.

    The device ID is used to identify the device in the {{site.data.keyword.iot_short_notm}} dashboard and is also a required parameter for connecting your device to {{site.data.keyword.iot_short_notm}}.

    > **Note:** The device type name must be no more than 36 characters and can contain only alpha-numeric characters (a-z, A-Z, 0-9) and any of the following characters: `_`, `.`, and `-`.

    For network connected devices, the device ID could be the device MAC address without any separating colons.

5. Click **Next** to complete the process.

6. Provide an authentication token, or accept an automatically generated token. If you choose to create your own token, make sure that it is between 8 and 36 characters long and consists only of alpha-numerical characters and the following characters: `_`, `.`, `!`, `&`, `@`, `?`, `\*`, `+`, `(`, `)`, and `-`.

    The token must not contain repeated character sequences, dictionary words, user names, or other predefined sequences.

7. Verify the summary information is correct, and then click **Add** to add the connection.

8. In the device information page, copy and save the following details:

    * Organization ID
    * Device Type
    * Device ID
    * Authentication Method
    * Authentication Token

    You'll need Organization ID, Device Type, Device ID, and Authentication Token configure your device to connect to {{site.data.keyword.iot_short_notm}}.

## Step 2: Connect your device to {{site.data.keyword.iot_short_notm}}

1. Set up your device for MQTT messaging and authenticate by using Organization ID, Device Type, Device ID, and Authentication Token.

2. Send device messages to your {{site.data.keyword.iot_short_notm}} organization by using the MQTT protocol.

    The following information is required when connecting your device:

    * URL: *org_id*.messaging.internetofthings.ibmcloud.com

      Where *org_id* is the ID of your {{site.data.keyword.iot_short_notm}} organization.

    * Port:
      * 1883
      * 8883 (encrypted)
      * 443 (websockets)
    * Device ID: d:_org_id:device_type:device_id_
    * User name: use-token-auth
    * Password: _Authentication token_
    * Event topic format: iot-2/evt/_event_id/fmt/format_string_

      Where _event_id_ specifies the event name that's shown in {{site.data.keyword.iot_short_notm}}, and _format_string_ is the format of the event, such as JSON.

    * Message format: JSON

  For more information, see [MQTT connectivity for devices](/docs/services/IoT/devices/mqtt.html).

## Step 3: Create boards and cards to keep track of device data

By using boards and cards, you can view graphics that represent data set values from one or more devices for a quick overview and understanding of the device data.

1. In your {{site.data.keyword.iot_short_notm}} dashboard, click **Create New Board**.

2. Enter a name and description for the board.

3. Click **Next** and then **Create**.

4. Click the board you just created, and then click **Add New Card**. Select Devices as the card type. The following table describes the visualization options you can choose from.

| Type | Data that is dispalyed |
|---------------|---------------|
| Generic visualization | The value of one or more data sets. Choose the large widget size to see up to three data point values in a small table. |
| Line chart | One or more data sets in a real-time scrolling chart. Use the Settings menu to set the data range and retention, the look and feel of the graphs, and more. |
| Bar chart | Data set values in labeld bars. Use the Settings menu to toggle horizontal or vertical bar direction. |
| Donut chart | Two or more data sets in a circular representation. |
| Value | The raw value of one or more data sets. |
| Gauge | The value of a data set shown as a gauge. Use the Settings menu to optionally set gauge thresholds for lower, middle, and upper data ranges. |
| Device properties | Specific properties for one or more devices. |
| All device properties | All properties for one or more devices. |
| Device list | A list to monitor multiple devices. A list can be used as a data source for other cards. |
| Device info | Basic information for a single device. |
| Device map | The location of devices in a device list. |

{: caption="Table 1. Visualization options" caption-side="top"}

## Step 4: Create device type schemas

At this point, you need to create a device type schema and map device properties to then create rules that are triggered based on the datapoints from your mapped device properties.

1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Devices > Manage Schemas** and click **Add Schema**.

2. Select a device type to associate with the message schema. Only one schema can be defined for a device type.

3. Click **Add property** and add one or more properties.

    You can select properties from a connected device, create virtual properties that modify or combine existing properties, or add properties manually.

    The available properties are defined in the payload of the messages that are sent by a device.
    {: tip}

    * To add a property manually, select the **Manual tab** and define the following property details:
        * Name
        * Data type
        * Property
        * Data unit (optional)
        * Decimal places (optional)

    * To create a virtual property, select the **Virtual Property** tab and define the following property details:
        * Name
        * Data type
        * Property
        * Calculation
        * Data unit (optional)
        * Decimal places

    * To select properties from a connected device, select the **From Connected** tab, and then select one or more properties to add to the schema. The selected properties are added and the description is set to the name of the property.

4. Click **Finish** to create the properties.

## Step 5: Create rules and actions

Rules are condition-based decision points that match real-time device data with predefined threshold values or other property data to trigger an alert if a condition is met. In addition to the alert that's displayed in the {{site.data.keyword.iot_short_notm}} dashboard, you can add one or more actions to run business logic when a rule is triggered.

1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Rules** and click **Create Cloud Rule**.

2. Enter a name and description for the rule, select a device type that the rule applies to, and click **Next**.

3. To set up the rule logic, add one or more IF conditions to use as triggers for the rule.

    You can add conditions in parallel rows to apply them as OR conditions, or you can add conditions in sequential columns to apply them as AND conditions. Take a look at the following examples:

      * A simple rule might trigger an alert if a parameter value is larger than a specified value: Condition = `temp_cpu>80`
      * A more complex rule might trigger when a combination of thresholds are met: Condition = `temp_cpu>60 AND cpu_load>90`

    To trigger a condition that compares two properties, or to trigger two or more property conditions that are combined sequentially by using AND, include the triggering data points in the same device message. If the data is received in more than one message, the condition or sequential conditions don't trigger.
    {: tip}

4. Configure conditional trigger requirements for your rule.

    You can use conditional trigger requirements to control the number of alerts that are triggered for a rule over a time period. The conditional triggering acts on any condition in the rule. For example, if a rule has five parallel conditions set by using OR, each condition that's true counts towards the conditional trigger count.

      1. In the rule editor, click the default **Trigger each time conditions are met** link to open the set frequency requirement dialog.
      2. Select and configure the conditional trigger you want to use in the rule.

        * Trigger every time conditions are met
        * Trigger if conditions are met N times in M _Unit of time_

5. Create or select one or more actions that occur if the rule conditions are met.

    For example, an action can be to send an email or post a webhook.

6. Optional: Select an alert priority for the rule.

    The priority is used to classify the alerts that are displayed in the **Boards > Rule-Based Analytics** board. The default priority is Low.

7. Click **Save** to save without activating,  or click **Activate** to save and activate your rule.

    When you activate the rule, an alert is added to the **Rule-Based Analytics** board when the conditions are met, and any rule action is run.

## Next steps

Extend the data analytics features by creating and connecting your own apps to consume real-time and historical device data.

  * Check out the [client libraries](/docs/services/IoT/iot_platform_client_lib.html) for tools to build code for integrating and connecting your devices and apps.

  * Explore the [Watson IoT Platform recipes ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/){: new_window} for more tutorials on embedding advanced analytics into your connected devices and apps.
