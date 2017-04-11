---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 使用 Node-RED 开发 {{site.data.keyword.iot_short_notm}}
{: #dev_nodered}

Node-RED 是一种可视工具，可用于在 {{site.data.keyword.iot_full}} 上开发应用程序、设备和网关。Node-RED 能够以全新且有趣的方式，将硬件设备、API 和在线服务连接在一起。Node-RED 基于 Node.js 构建，充分利用巨型节点模块生态系统来提供一个可以集成大量不同系统的工具。
{:shortdesc}

IBM 提供的 Node-RED 节点，用于帮助您将设备、网关和应用程序连接到 {{site.data.keyword.iot_short_notm}}，并迅速创建 IoT 解决方案。


## Watson IoT 节点   
{: #watson_iot_node}  

![Watson IoT 节点图像](../images/node-red-watson.png "Watson IoT 节点图像")


Watson IoT 节点是一对节点，用于将设备或网关连接到 {{site.data.keyword.iot_short_notm}}。设备或网关可以使用这些节点向应用程序发送事件以及从应用程序接收命令。

有关 Watson IoT 节点的更多信息，请参阅以下资源：

- [GitHub 上的 Watson IoT 节点 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-watson-iot/iot-nodered/tree/master/node-red-contrib-ibm-watson-iot){: new_window}
- [Watson IoT 节点文档 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.npmjs.com/package/node-red-contrib-ibm-watson-iot){: new_window}


## IBM IoT 应用程序节点  
{: #watson_app_node}  


![IBM IoT 应用程序节点图像](../images/node-red-ibmiot.png "IBM IoT 应用程序节点图像")

IBM IoT 应用程序节点是一对节点，用于将应用程序连接到 {{site.data.keyword.iot_short_notm}}。应用程序可以使用这对节点从设备接收设备事件以及将命令发送回设备。

有关 IBM IoT 应用程序节点的更多信息，请参阅以下资源：

- [GitHub 上的 IBM IoT 应用程序节点 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-watson-iot/iot-nodered/tree/master/node-red-contrib-scx-ibmiotapp){: new_window}
- [IBM IoT 应用程序节点文档 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://flows.nodered.org/node/node-red-contrib-scx-ibmiotapp){: new_window}


## 更多信息和样本   
{: #more_info}


为了帮助您入门，请使用以下样本诀窍：
- [Getting started with {{site.data.keyword.iot_short_notm}} by using Node-RED ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/recipes/tutorials/getting-started-with-watson-iot-platform-using-node-red/){: new_window}
- [Connecting Raspberry Pi as a device to {{site.data.keyword.iot_short_notm}} by using Node-RED ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/recipes/tutorials/deploy-watson-iot-node-on-raspberry-pi/){: new_window}

有关更多信息，另请参阅 [Creating apps with Node-RED Starter](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered)。
