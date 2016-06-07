---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# External service integrations
{: #ref-index}

## Overview
{: #overview}

External service integration allows you to bind metadata or function supported by another service to your {{site.data.keyword.iot_full}} account.

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


#### Extension enablement

To enable Jasper integration with your {{site.data.keyword.iot_short_notm}} organization, complete the following steps:

1. In the {{site.data.keyword.iot_short_notm}} dashboard, click the wrench icon on the right and then open Configuration Settings.
2. Scroll down the to the Extensions section, and set Jasper to 'On'.
3. Enter your Jasper user name, password, license key, and API endpoint.

#### Device configuration

You can configure the devices that are connected to both your {{site.data.keyword.iot_short_notm}} organization and your Jasper account to display data from Jasper in the {{site.data.keyword.iot_short_notm}} dashboard. Jasper configuration cannot be applied as part of the Add Device process, as only already connected devices can be configured with Jasper. To configure your Jasper-connected devices, complete the following steps:

1. In the devices tab of your {{site.data.keyword.iot_short_notm}} dashboard, find the Jasper-connected device to be configured.
2. Select the device to open the *Device Drilldown* view.
3. Scroll down to *Extension Configuration*.
4. Enter the extension configuration by using the following JSON format, and then click 'Confirm changes' to save your configuration.

```  
    {
        "jasper": {
            "iccid": "string"
        }
    }

```

When the organization is successfully configured, the *Extensions* section displays under the *Extensions Configuration* section in the *Device Drilldown* view.
