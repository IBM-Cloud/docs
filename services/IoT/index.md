---

copyright:
  years: 2016

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Deploying and configuring {{site.data.keyword.iot_short}} for your organization
{: #gettingstartedtemplate}
*Last updated: 11 May 2016*

{{site.data.keyword.iot_full}} for {{site.data.keyword.Bluemix_notm}} gives you a versatile IoT toolkit, that includes gateway devices, device management, and powerful application access. By using {{site.data.keyword.iot_short}}, you can collect connected device data and perform analytics on real-time data from your organization.
{:shortdesc}

## Before you begin

Before connecting devices and utilizing data, an instance of the {{site.data.keyword.iot_short}} service must exist in your {{site.data.keyword.Bluemix_notm}} organization. You can create it directly from the [{{site.data.keyword.iot_short}} page in the Bluemix Services Catalog](https://console.ng.bluemix.net/catalog/services/internet-of-things-platform/).  

## Up and running with {{site.data.keyword.iot_short}}

To get up and running with the service, explore the following options depending on your situation:

   |   The service is deployed | The service is not deployed
  ------------- | -------------
  **I have a device to connect** | [Connect your device to {{site.data.keyword.iot_short}}](iotplatform_task.html#iotplatform_task).| Explore device connection in the [Play organization demo](http://discover-iot.eu-gb.mybluemix.net/?cm_mc_uid=44491599487314618721024&cm_mc_sid_50200000=1462798151#/play){:new_window}.
  **I do not have a device to connect** | [Create and connect a Node-RED device simulator](nodereddevice_sample.html){:new_window}.
**Tip:** For additional information on how to connect specific device types to {{site.data.keyword.iot_short}}, see [developerWorks recipes](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window}.  

<!--
## IoT Quickstart
{: #quickstart}  
Follow these steps to see a Quickstart example of how an IoT device can connect to {{site.data.keyword.iot_short}} and to optionally create a simulated device in Node-RED to connect to your own service.

1. Open the [simulated IoT Sensor page](https://quickstart.internetofthings.ibmcloud.com/iotsensor) page.  
This sensor represents an IoT-connected sensor. The sensor has adjustable **Temperature**, **Humidity**, and **Object Temperature** tabs.
2. In the IoT Sensor page title bar, click the sensor's device ID.  
The device ID should be a 12 character alphanumeric string. Clicking the device ID opens a data visualization in a new tab.
3. Explore the device sensor data.  
The visualization has several graphs to show the incoming data. Change graphs by selecting a different datapoint.
4. In the IoT Sensor page, adjust the temperature, humidity, or object temperature by using the up and down arrows.  
As the values for these variables are adjusted, the visualization changes to show the new information. Changing the variables simulates changes in the data that is flowing from a device to the {{site.data.keyword.iot_short}}, where it can be stored or used for analytics.

To test your simulated device with your own {{site.data.keyword.iot_short}} organization you can follow the instructions to [create a Node-RED application](nodereddevice_sample.html) and import the device as a node flow.

-->

# Related Links
{: #rellinks}
## Tutorials and Samples
{: #samples}
* [Recipes for connecting your devices](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window}
* [{{site.data.keyword.iot_short}} Play organization](https://play.internetofthings.ibmcloud.com/){:new_window}
* [Connecting an Intel Galileo to the {{site.data.keyword.iot_short}}](https://developer.ibm.com/recipes/tutorials/connect-an-intel-galileo-to-the-internet-of-things-foundation-connect/){:new_window}
* [Connecting an ARM® mbed™ IoT Starter Kit](https://developer.ibm.com/recipes/tutorials/arm-mbed-iot-starter-kit-part-1/){:new_window}
* [Connecting a Raspberry Pi to {{site.data.keyword.iot_short}}](https://developer.ibm.com/recipes/tutorials/raspberry-pi-4/){:new_window}

## API Reference
{: #api}
* [{{site.data.keyword.iot_short}} API Documentation](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/){:new_window}
* [Developer documentation](http://docs.internetofthings.ibmcloud.com){:new_window}
