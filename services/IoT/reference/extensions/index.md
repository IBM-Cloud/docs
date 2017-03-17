---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-15"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# External service integrations
{: #ref-index}

External service integration allows you to access data and operations from third-party or external services within your {{site.data.keyword.iot_full}} organization.

## Jasper
{: #jasper}

Jasper is an administration and management platform for SIM devices. Jasper is integrated into the {{site.data.keyword.iot_short_notm}} dashboard, making it possible to administer Jasper devices through your {{site.data.keyword.iot_short_notm}} organization dashboard.

### Supported operations for Jasper

The built-in Jasper integration that is provided by our platform provides support for the following Jasper operations:

- View overall Jasper data
  - Shows: Status, Rate Plan, month-to-date data usage, month-to-date SMS usage, month-to-date voice usage, overage limits, date added, and date modified.
- Change SIM activation state.
  - Select from: Inventory, Activation Ready, Activated, Deactivated, and Retired.
- View SIM Usage
  - Shows: Cycle start date, billable and total data, billable and total SMS, billable and total voice.
  - The cycle start date can be set using a YYYY-MM-DD format.
- Send SMS to SIM
- Change rate plan

You can access the supported operations in the device drilldown of a Jasper connected device after the following configuration steps are completed.

### REST APIs for Jasper
To access the REST API for Jasper, see the Jasper Extension section in the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Jasper_Extension){: new_window} documentation.

### Configuration for Jasper

In order to connect your Jasper service to your {{site.data.keyword.iot_short_notm}} organization there are two stages of configuration that must first be done. First, your {{site.data.keyword.iot_short_notm}} must be connected to your Jasper service, then your {{site.data.keyword.iot_short_notm}} devices must be configured.


1. Enable the Jasper extension. To enable Jasper integration with your {{site.data.keyword.iot_short_notm}} organization, complete the following steps:
  1. From the {{site.data.keyword.iot_short_notm}} dashboard, select **Extensions**.
  2. In the **Extensions** page, click **Add Extension**.
  3. Click **Add** next to Jasper.
  4. Enter your Jasper username, password, access key and domain ID.
  5. Click **Done**.

2. Configure your devices
You can configure the devices that are connected to both your {{site.data.keyword.iot_short_notm}} organization and your Jasper account to display data from Jasper in the {{site.data.keyword.iot_short_notm}} dashboard.  
**Important:** The Jasper configuration cannot be applied as part of the Add Device process, only previously connected devices can be configured with Jasper.  
To configure your Jasper-connected devices, complete the following steps:
 1. In the devices tab of your {{site.data.keyword.iot_short_notm}} dashboard, find the Jasper-connected device to be configured.
 2. Select the device to open the *Device Drilldown* view.
 3. Scroll down to *Extension Configuration*.
 4. Enter the extension configuration by using the following JSON format, and then click **Confirm changes** to save your configuration.  

```json  
    {
        "jasper": {
            "iccid": "string"
        }
    }

```

When the organization is successfully configured, the *Extensions* section displays under the *Extensions Configuration* section in the *Device Drilldown* view.

## AT&T
{: #att}

### Supported operations for AT&T

The AT&T extension enables the following AT&T operations:

- View overall AT&T data
  - Shows: Status, Rate Plan, month-to-date data usage, month-to-date SMS usage, month-to-date voice usage, overage limits, date added, and date modified.
- Change SIM activation state.
  - Select from: Inventory, Activation Ready, Activated, Deactivated, and Retired.
- View SIM Usage
  - Shows: Cycle start date, billable and total data, billable and total SMS, billable and total voice.
  - The cycle start date can be set using a YYYY-MM-DD format.
- Send SMS to SIM
- Change rate plan

### REST APIs for AT&T
To access the REST API for AT&T, see the AT&T Extension section in the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/AT&T_Extension){: new_window} documentation.

### Configuration for AT&T

In order to connect your {{site.data.keyword.iot_short_notm}} organization to AT&T you must complete organization configuration and device configuration.

To configure your {{site.data.keyword.iot_short_notm}} platform, complete the following steps.

1. Enable the AT&T extension. To enable AT&T integration with your {{site.data.keyword.iot_short_notm}} organization, complete the following steps:
  1. From the {{site.data.keyword.iot_short_notm}} dashboard, select **Extensions**.
  2. In the **Extensions** page, click **Add Extension**.
  3. Click **Add** next to AT&T.
  4. Enter your AT&T username, password, access key and domain ID.
  5. Click **Done**.

In order to connect your {{site.data.keyword.iot_short_notm}} organization with your AT&T account, there are two stages of configuration that must first be done. Complete the the organization configuration and then configure your devices.


2. Configure your devices
You can configure the devices that are connected to both your {{site.data.keyword.iot_short_notm}} organization and your AT&T account to display data from AT&T in the {{site.data.keyword.iot_short_notm}} dashboard.  
**Important:** The AT&T configuration cannot be applied as part of the Add Device process, only previously connected devices can be configured with AT&T.  
To configure your AT&T-connected devices, complete the following steps:
 1. In the devices tab of your {{site.data.keyword.iot_short_notm}} dashboard, find the AT&T-connected device to be configured.
 2. Select the device to open the *Device Drilldown* view.
 3. Scroll down to *Extension Configuration*.
 4. Enter the extension configuration by using the following JSON format, and then click **Confirm changes** to save your configuration.  

```json  
    {
        "atnt": {
            "iccid": "string"
        }
    }

```

When the organization is successfully configured, the *Extensions* section displays under the *Extensions Configuration* section in the *Device Drilldown* view.

## ARM mbed connector
{: #arm}

The ARM mbed connector allows you to connect your ARM mbed device to your {{site.data.keyword.iot_short_notm}}. The ARM mbed extension is allows the ARM mbed portal and the {{site.data.keyword.iot_short_notm}} to send and receive data from the ARM mbed portal.

### Setup Configuration


1. Enable the ARM mbed connector extension. To enable the ARM mbed connector extension complete the following steps:
  1. From the {{site.data.keyword.iot_short_notm}} dashboard, select **Settings** and navigate to **Extensions**.
  2. In the **Extensions** menu, click **Add Extension**.
  3. Click **Add** next to ARM mbed connector extension.
  4. Enter your ARM mbed access key and domain ID. You can find these by using the ARM mbed portal at https://connector.mbed.com.
  5. Check the credentials are correct by clicking the **Check Connection** button.
  6. Click **Done**.

### Payload Format

There are two types of incoming messages from the ARM mbed platform, notifications and asynchronous responses. The {{site.data.keyword.iot_short_notm}} can send commands to devices that are connected to the ARM mbed platform.

#### Notifications

Notifications are generated by changes in device or sensor data. After the {{site.data.keyword.iot_short_notm}} processes the message, it is to the device event topic in the same way as a device connected directly to the {{site.data.keyword.iot_short_notm}}. The event type used for notifications originating on devices connected to the ARM mbed platform is `notify`.

The following code sample shows the payload format for a notification sent by the ARM mbed platform API:

```
{
  "ep":<endpoint/deviceID>,
  "path":<resource path>,
  "ct":<content type>,
  "payload":<Base64 encoded payload>,
  "max-age":<how long the payload is valid, in seconds>
}
```

#### Asynchronous responses

When the {{site.data.keyword.iot_short_notm}} sends a command to a device connected to the ARM mbed platform, the device sends a confirmation message back to the {{site.data.keyword.iot_short_notm}}. This confirmation message is called an _asynchronous response_ and uses the event type `asyncResponse`.

The following code sample shows the payload format for an asynchronous response sent by the ARM mbed cloud service:

```
{
  "id":<transaction id>,
  "status":<200 is command was sucessfully executed. Check other HTTP response codes>,
  "ct":<content type>,
  "max-age":<how long the payload is valid, in seconds>,
  "payload":<base64 encoded payload>,
  "ep":<endpoint/deviceID affected by the command>,
  "path":<resource path affected by the command>
}
```

#### Sending commands to the ARM mbed platform

The {{site.data.keyword.iot_short_notm}} can send commands to devices connected to the ARM mbed platform. Commands sent to the ARM mbed platform must use the following JSON format.

```
{
  "method":<PUT or POST>,
  "deviceId":<endpoint/deviceId>,
  "resourceId":<resource path>,
  "payload": <Base64 encoded payload>
}
```
The method chosen is case sensitive. The initial '/' of the resource path must be skipped.


The payload should be published to the following topic:

```
iot-2/type/<device_type>/id/<deviceId>/cmd/<command_type>/fmt/<command_format>
```


## Orange
{: #orange}

The Orange extension allows you to view SIM card data from devices which are connected to your {{site.data.keyword.iot_short_notm}} and have an Orange SIM card installed.

https://developer.ibm.com/iotplatform/2016/03/30/watson-iot-platform-integration-with-orange-beta/

### Supported operations for Orange

If you have a device which is connected to your {{site.data.keyword.iot_short_notm}} service and has an Orange SIM card, you can use the Orange extension to view the following SIM card data:

- SIM serial number
- Activation status
- Last status change
- Last status refresh
- Location status

### REST APIs for Orange
To access the REST API for Orange, see the Orange Extension section in the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Orange_Extension){: new_window} documentation.

### Configuration for Orange

To enable the Orange extension:

1. From the {{site.data.keyword.iot_short_notm}} dashboard, select **Extensions**.
2. In the **Extensions** page, click **Add Extension**.
3. Click **Add** next to the Orange extension.
4. Enter your Orange user name and password.
6. Click **Done**.

After the Orange extension has been enabled, each device with an Orange SIM card must be configured to display Orange SIM data.

1. In the devices tab of your {{site.data.keyword.iot_short_notm}} dashboard, find the Orange SIM device to be configured.
2. Select the device and scroll down to *Extension Configuration*.
3. Enter the extension configuration by using the following JSON format, and then click **Confirm changes** to save your configuration.

```  
    {
        "orange": {
            "serialnumber": "<serial number of Orange SIM>"
        }
    }

```
When the organization is successfully configured, the *Extensions* section displays under the *Extensions Configuration* section in the *Device Drilldown* view.

## Historical Data Storage
{: #historical_data}

The historical data storage extension lets you locate and configure compatible message storage services such as [{{site.data.keyword.cloudantfull}}](../../cloudant_connector.html) or [{{site.data.keyword.messagehub_full}}](../../message_hub.html) for your IoT data.

## Custom device management packages
{: #device_mgmt}

Device management is a core feature of the {{site.data.keyword.iot_short_notm}}, however, it can be extended to develop additional functionality. Custom device management packages must consist of valid JSON and define at least one custom device management action.

For more information on custom device management functions, including an example of the required JSON format, see [device management custom extensions](../../devices/device_mgmt/custom_actions.html){: new_window}.

### Adding a custom device management package

Custom device management packages can be added either by using the {{site.data.keyword.iot_short_notm}} dashboard, or by using the API.

To add a custom device management package by using the {{site.data.keyword.iot_short_notm}} dashboard:

1. From your {{site.data.keyword.iot_short_notm}} dashboard, click **Settings** from the navigation bar.
2. Click **Custom Device Management Packages**.
3. Click the **Add Package** button.
4. Select your package file and click **Open**.

To add a custom device management package by using the API, see the [{{site.data.keyword.iot_short_notm}} API documentation ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.

## Blockchain
{: #blockchain}

{{site.data.keyword.iot_short_notm}} with blockchain enables IoT devices to provide data to blockchain transactions, which stores the data in the blockchain's immutable ledger and uses it in smart contract business rules. {{site.data.keyword.iot_short_notm}} maps device data to the data format that is required by the blockchain's smart contract and passes it to a blockchain fabric to store in the blockchain ledger.

### Supported operations for Blockchain
- Trigger smart contract updates with device events.
- Run smart contract business logic to update ledger state with device event data.
- Monitor the blockchain, transactions, and ledger state with the monitoring UI.

### Configuration for Blockchain

{{site.data.keyword.iot_short_notm}} blockchain integration is a services offering  that is not activated by default in {{site.data.keyword.iot_short_notm}}. To activate the feature in your organization, complete the following steps:
 1. From the {{site.data.keyword.iot_short_notm}} dashboard, select **Extensions**.
 2. In the **Extensions** page, click **Add Extension**.
 3. Click **Add** next to the Blockchain extension.
 4. In the Blockchain tile, click **Setup**.
 3. In the **Activate Blockchain** section, click the **Learn more** link to go to the [IoT Blockchain Services Offering page ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/internet-of-things/iot-news/announcements/private-blockchain/){: new_window}.
 4. Click **Kick-start your blockchain project** to fill out and submit the *Explore the potential of IoT and Blockchain* form.  
 5. After your request is approved, IBM will contact you to enable blockchain integration for your organization.
 6. Return to the {{site.data.keyword.iot_short_notm}} dashboard for your organization to complete the setup by following the steps in [{{site.data.keyword.iot_short_notm}} blockchain integration](../../bl_blockchain_integration.html).

<!-- ## The Weather Company
{: #weathercompany}

The Weather Company extension combines weather data with your existing {{site.data.keyword.iot_short_notm}} devices. Weather data from The Weather Company appears in the device details view if an update location request has been made by using the API, or if the device has already set its location by using a device management message.

**Note:** Only managed devices can set their own locations. All unmanaged devices must have their locations set manually by using the API. For more information on setting a device location, see [Update Location requests](../../devices/device_mgmt/index.html#update-location).

### REST APIs for The Weather Company
To access the REST API for The Weather Company, see the
Device Location Weather section in the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Location_Weather){: new_window} documentation.

### Weather Data

To view the weather data retrieved for a device location, find the device in the **Devices** pane and click it. In the detailed device view scroll down to the **Extensions** section. The following weather data is listed:

- Current weather.
- Current temperature.
- Predicted maximum and minimum temperature.
- Relative humidity.
- Pressure.
- Visibility.
- Wind speed.
- Wind direction.
- Latitude.
- Longitude.
-->

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html){: new_window}. -->

## Email
{: #email}

Users can be added to the {{site.data.keyword.iot_short_notm}} by using email invitations. For information, see  [Managing user access](../../add_users.html).

To use the email invitation feature, an email extension must be configured to use the SendGrid online service or a Simple Mail Transfer Protocol (SMTP) service. The extension can also use the SendGrid {{site.data.keyword.Bluemix_notm}} application.

### SendGrid online service

To configure the email extension for use with the SendGrid online service, follow these steps:

1. Retrieve the authorized API key from your SendGrid online account.
2. In your {{site.data.keyword.iot_short_notm}} dashboard, click **Extensions** from the navigation bar.
3. In the **Email** section, click **Setup**.
4. Select **SendGrid with API key**
5. Enter the name and email address of your site administrator, and the authorized API key.

### SMTP service

To configure the email extension for use with an SMTP service, follow these steps:

1. In your {{site.data.keyword.iot_short_notm}} dashboard, click **Extensions** from the navigation bar.
2. In the **Email** section, click **Setup**.
3. Select **SMTP**.
4. Enter the configuration details of your SMTP service.

### SendGrid {{site.data.keyword.Bluemix_notm}} application

To configure the email extension for use with the SendGrid {{site.data.keyword.Bluemix_notm}} application, follow these steps:

1. Create a dummy application and bind the SendGrid service.  
In order to retrieve the configuration credentials, add and bind the SendGrid service to a dummy app.

 1. From your {{site.data.keyword.Bluemix_notm}} dashboard, click **Create Service**.
 2. Select the SendGrid service from the catalog and click **Create**.
 3. From the {{site.data.keyword.Bluemix_notm}} dashboard add the {{site.data.keyword.sdk4nodefull}} application.
 4. Click the {{site.data.keyword.sdk4nodefull}} application from the {{site.data.keyword.Bluemix_notm}} dashboard and click **Bind a service or API**.
 5. Select the SendGrid service and click **Add**.
 6. The {{site.data.keyword.sdk4nodefull}} application must now be restaged.
2. Prepare to configure the {{site.data.keyword.iot_short_notm}} service.  
The {{site.data.keyword.iot_short_notm}} can be configured by using the {{site.data.keyword.iot_short_notm}} dashboard or by using the {{site.data.keyword.iot_short_notm}} API.  
 1. Click the {{site.data.keyword.sdk4nodefull}} application from the {{site.data.keyword.Bluemix_notm}} dashboard.
 2. Click **Environment Variables** from the navigation bar.
 3. Copy the displayed JSON to a temporary text file.  
 The JSON should have the following format:
```
{
  "name": "SendGridServiceName",
  "label": "user-provided",
  "credentials": {
    "password": "xxx",
    "hostname": "smtp.sendgrid.net",
    "username": "username"
  }
}
```
3. Add the configuration data to the {{site.data.keyword.iot_short_notm}} organization.
 1. Open the {{site.data.keyword.iot_short_notm}} dashboard.
 2. Click **Extensions** from the navigation bar.
 3. Click **Setup** under the **Email** icon.
 4. Select **SendGrid with username**.
 5. Enter the configuration data from the temporary text file.
 6. Click **Done**.
