---

copyright:
  years: 2015, 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# External service integrations
{: #ref-index}
*Last updated: 18 July 2016*
{: .last-updated}

External service integration allows you to bind metadata or function supported by another service to your {{site.data.keyword.iot_full}} organization.

## Jasper
{: #jasper}

Jasper is an administration and management platform for SIM devices. Jasper is integrated into the {{site.data.keyword.iot_short_notm}} dashboard, making it possible to administer Jasper devices through your {{site.data.keyword.iot_short_notm}} organization dashboard.

**Important:** Jasper integration is currently available as part of a limited beta.  Future updates might include changes incompatible with the current version of this feature.

### Supported operations

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


### Configuration

In order to connect your {{site.data.keyword.iot_short_notm}} platform organization with your Jasper account, there are two stages of configuration that must first be done. Complete the the organization configuration and then configure your devices.


1. Enable the Jasper extension   
To enable Jasper integration with your {{site.data.keyword.iot_short_notm}} organization, complete the following steps:
 1. From the {{site.data.keyword.iot_short_notm}} dashboard select  ![Settings.](../../blockchain/images/platform_settings.png "Settings") in the menu side bar.
 2. Scroll down the to the Extensions section, and set Jasper to **On**.
 3. Enter your Jasper user name, password, license key, and API endpoint.
 4. Click **Save**

2. Configure your devices
You can configure the devices that are connected to both your {{site.data.keyword.iot_short_notm}} organization and your Jasper account to display data from Jasper in the {{site.data.keyword.iot_short_notm}} dashboard.  
**Important:** The Jasper configuration cannot be applied as part of the Add Device process, as only already connected devices can be configured with Jasper.  
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

<!-- ## Orange
{: #orange}
https://developer.ibm.com/iotplatform/2016/03/30/watson-iot-platform-integration-with-orange-beta/
The platform now has integration with Orange built in.

This means that with your Orange sim card installed in a device and configured you can see it’s properties in the device details.

### Supported operations
- Sim status
- Location

### Configuration
1. Enable the Jasper extension   
To enable Jasper integration with your {{site.data.keyword.iot_short_notm}} organization, complete the following steps:
 1. From the {{site.data.keyword.iot_short_notm}} dashboard select  ![Settings.](images/platform_settings.png "Settings") in the menu side bar.
 2. Scroll down the to the Extensions section, and set Orange to **On**.
 3. Enter your Orange user name and password.
 4. Click **Save**
2. Configure your Orange sim device
To configure your Orange-connected devices, complete the following steps:  
 1. In the devices tab of your {{site.data.keyword.iot_short_notm}} dashboard, find the Orange sim device to be configured.
 2. Select the device to open the *Device Drilldown* view.
 3. Scroll down to *Extension Configuration*.
 4. Enter the extension configuration by using the following JSON format, and then click **Confirm changes** to save your configuration.
```  
    {
        "orange": {
            "serialnumber": "numeric string"
        }
    }

```
When the organization is successfully configured, the *Extensions* section displays under the *Extensions Configuration* section in the *Device Drilldown* view.


## Device management
{: #device_management}


### Supported operations

### Configuration


-->

## Blockchain
{: #blockchain}

{{site.data.keyword.iot_short_notm}} with blockchain enables IoT devices to provide data to blockchain transactions, which stores the data in the blockchain's immutable ledger and uses it in smart contract business rules. {{site.data.keyword.iot_short_notm}} maps device data to the data format that is required by the blockchain's smart contract and passes it to a blockchain fabric to store in the blockchain ledger.

### Supported operations
- Trigger smart contract updates with device events.
- Run smart contract business logic to update ledger state with device event data.
- Monitor the blockchain, transactions, and ledger state with the monitoring UI.

### Configuration

{{site.data.keyword.iot_short_notm}} blockchain integration is a services offering  that is not activated by default in {{site.data.keyword.iot_short_notm}}. To activate the feature in your environment, complete the following steps:
 1. From the {{site.data.keyword.iot_short_notm}} dashboard click, ![Settings.](../../blockchain/images/platform_settings.png "Settings") in the menu side bar.
 2. Scroll down to the Extensions section.
 2. Click the **Tell me more** link next to the Blockchain extension to go to the IoT Blockchain Services Offering page.
 3. Fill out and submit the service request form.   
The service approval typically takes approximately one day. After your request is approved, you receive an email with instructions on how to activate blockchain integration in your {{site.data.keyword.iot_short_notm}} organization.
 5. Return to the {{site.data.keyword.iot_short_notm}} dashboard for your organization to complete the setup. For more information, see [{{site.data.keyword.iot_short_notm}} blockchain integration](../../bl_blockchain_integration.html).
