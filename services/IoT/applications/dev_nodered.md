---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-09-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Developing {{site.data.keyword.iot_short_notm}} by using Node-RED
{: #dev_nodered}

Node-RED is a visual tool that you can use to develop your applications, devices, and gateways on {{site.data.keyword.iot_full}}. Node-RED provides capabilities for connecting hardware devices, APIs, and online services in new and interesting ways. Node-RED is built on top of Node.js and takes advantage of the huge node module ecosystem to provide a tool that can integrate many different systems.
{:shortdesc}

IBM provides Node-RED nodes to help you to connect your devices, gateways, and applications to {{site.data.keyword.iot_short_notm}} and to create IoT solutions quickly.


## Watson IoT Node   
{: #watson_iot_node}  

![Watson IoT Node image](../images/node-red-watson.png "Watson IoT node image")


Watson IoT Node is a pair of nodes for connecting your devices or gateways to the {{site.data.keyword.iot_short_notm}}. Devices or gateways can use these nodes to send events and to receive commands from the application.

For more information about Watson IoT Node, see the following resources:

- [Watson IoT Node on GitHub](https://github.com/ibm-watson-iot/iot-nodered/tree/master/node-red-contrib-ibm-watson-iot)
- [Watson IoT Node documentation](https://www.npmjs.com/package/node-red-contrib-ibm-watson-iot)


## IBM IoT App Node  
{: #watson_app_node}  


![IBM IoT App Node image](../images/node-red-ibmiot.png "IBM IoT App node image")

IBM IoT App Node is a pair of nodes for connecting your applications to {{site.data.keyword.iot_short_notm}}. Applications can use the nodes to receive device events and send commands back to the device.

For more information about IBM IoT App Node, see the following resources:

- [IBM IoT App Node on GitHub](https://github.com/ibm-watson-iot/iot-nodered/tree/master/node-red-contrib-scx-ibmiotapp)
- [IBM IoT App Node documentation](http://flows.nodered.org/node/node-red-contrib-scx-ibmiotapp)


## More information and samples   
{: #more_info}


To help you to get started, use the following sample recipes:
- [Getting started with {{site.data.keyword.iot_short_notm}} by using Node-RED](https://developer.ibm.com/recipes/tutorials/getting-started-with-watson-iot-platform-using-node-red/)
- [Connecting Raspberry Pi as a device to {{site.data.keyword.iot_short_notm}} by using Node-RED](https://developer.ibm.com/recipes/tutorials/deploy-watson-iot-node-on-raspberry-pi/)

For more information, see also [Creating apps with Node-RED Starter](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered).
