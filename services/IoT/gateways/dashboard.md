---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Connecting and using a gateway device with the {{site.data.keyword.iot_short_notm}} dashboard
{: #IoT_connectGateway}
*Last updated: 16 May 2016*

This task describes the process of connecting a gateway device, which connects itself, and devices behind the gateway, and sends data from itself and devices behind it to the {{site.data.keyword.iot_full}}.




Gateways can also subscribe to commands on behalf of devices connected to the gateway.
{:shortdesc}

## Prerequisites
{: #Prerequisites}

Before you can connect a gateway you must first set up an organization on the {{site.data.keyword.iot_short_notm}}. For more information, see [Getting started](../getting_started/register/index.html).


## Procedure
{: #Procedure}

1.  Creating a device type for your gateway: A gateway has more rights than a normal device, and can send and receive device data on behalf of other devices.

  In your organization dashboard ‘Devices’ tab, select the ‘Device Types’ sub-tab. Click ‘Create Type’. Click ‘Create gateway type’, and follow the instructions in the flow, including adding any device properties and metadata. Click ‘Create’ to complete the flow and create the device type.

2.  Creating a gateway device:

  In your organization dashboard ‘Devices’ tab, select the ‘Browse’ sub-tab and click ‘Add device’. Select the gateway device type created in the previous step. Follow the ‘Add device’ flow, entering the mandatory *deviceId* property, and any other optional properties.

  After creating a gateway device, the authentication token provided should be saved for use in configuring the gateway to connect to the {{site.data.keyword.iot_short_notm}}.

3.  Connecting the gateway to the {{site.data.keyword.iot_short_notm}}.

  There are a range of recipes available for connecting devices to the {{site.data.keyword.iot_short_notm}}. Connecting a gateway requires the same steps as connecting a normal device, with one exception. When you connect a normal device, the clientId uses the following format:

  `d:<orgId>:<typeId>:<deviceId>`

  When connecting a gateway device, the clientId replaces `d` with `g`:

  `g:<orgId>:<typeId>:<deviceId>`

4.  Setting up devices that are connected to the gateway and are to be connected to the {{site.data.keyword.iot_short_notm}}:

  Create a device type for the device or devices which are to connect through the gateway. The  *gatewayId* and *gatewayTypeId* properties of the devices must match the *deviceId* and *deviceTypeId* of the gateway that they are connecting through. Add the devices that are connected to the gateway to the {{site.data.keyword.iot_short_notm}}.

  When a device is successfully connected to your gateway, it displays on the dashboard of your {{site.data.keyword.iot_short_notm}} organization.
