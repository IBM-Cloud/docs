---

copyright:
  years: 2016
lastupdated: "2016-06-29"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}} Feature Overview
{: #feature_overview}

The {{site.data.keyword.iot_full}} is built on the following key areas:

  1. Connect - Connect devices and develop applications.
  2. Information Management - Store and review device data and integrate your {{site.data.keyword.iot_short_notm}} with other services.
  3. Analytics - Visualize real-time device data by using the {{site.data.keyword.iot_short_notm}} dashboard.
  4. Risk Management - Configure secure connectivity and architecture with access control for users and applications.

## Connect
{: #connect}

{{site.data.keyword.iot_short_notm}} Connect is the starting point for any {{site.data.keyword.iot_short_notm}} service. Connecting devices, creating applications, controlling your devices, and interacting with third-party services are all available under {{site.data.keyword.iot_short_notm}} Connect.

### Gateway devices

By using a gateway, you can connect devices to the {{site.data.keyword.iot_short_notm}} that otherwise cannot connect to the Internet. Gateway devices combine the function of a device and an application. Gateways can receive commands and send device data in the same way as a device, but they can also send commands to other devices that are connected to it, in the same way as an application can.

Devices that cannot connect directly to the Internet can be connected to a gateway device, and their device data can be sent to the gateway device, which can then send it to your {{site.data.keyword.iot_short_notm}} service.

### Device management

Device management capabilities are provided through the combination of a device management API and a device management agent that is installed on devices. Managed devices can perform device management actions, which can be triggered through the main {{site.data.keyword.iot_short_notm}} dashboard.

Device management gives you the capability to reboot, download and install firmware updates, and reset devices to factory settings remotely, all from within the {{site.data.keyword.iot_short_notm}} user interface.

### Third-party service integrations

Third-party service integration is built into the {{site.data.keyword.iot_short_notm}}, including support for The Weather Company weather location services, which allows you to find the current weather at a device location.

---

## Information Management
{: #information_management}

{{site.data.keyword.iot_short_notm}} Information Management controls the data that is sent by devices after it reaches your {{site.data.keyword.iot_short_notm}} service. Information management includes data storage and transformation.

### Device last event cache

By using the {{site.data.keyword.iot_short_notm}} Last Event Cache API, you can retrieve the last event that was sent by a device. This works whether the device is online or offline, which allows you to retrieve device status regardless of the device's physical location or use status. Last event data of a device can be retrieved for any specific event that occurred up to 365 days ago.

### Device event data storage

Device event data from your {{site.data.keyword.iot_short_notm}} service can be stored for later use. Data storage is an essential first step towards performing insightful analytics to gain insights from that data.  For example, you can track changes over longer periods of time and store sets of data for use with powerful analytics tools, including use with Watson APIs and cognitive computing.

---

## Analytics
{: #analytics}

### Visualize real-time device data

You can visualize and display real-time device data by using dashboard cards. Dashboard cards monitor and display device data in real-time, which allows you to keep track of key devices or device data. These visualizations are displayed on the main {{site.data.keyword.iot_short_notm}} dashboard to give you rapid access to the context and status of real-time device data.

---

## Risk Management
{: #risk_management}

### Secure connectivity and architecture

The architecture of the {{site.data.keyword.iot_short_notm}} is designed to prevent devices from impersonating other devices, which maintains the integrity of your device data. Devices connect to the {{site.data.keyword.iot_short_notm}} by using a combination of a client ID and authentication token, which only you know. After the devices are registered or the API keys are generated, the authentication token is salted and hashed to maintain the security of your credentials. Connectivity over TLS v1.2 is fully supported.

---
