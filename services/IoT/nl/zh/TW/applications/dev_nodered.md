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

# 使用 Node-RED 開發 {{site.data.keyword.iot_short_notm}}
{: #dev_nodered}

Node-RED 是一種視覺化工具，您可以用來在 {{site.data.keyword.iot_full}} 上開發應用程式、裝置及閘道。Node-RED 可讓您以全新且有趣的方式來連接硬體裝置、API 及線上服務。Node-RED 以 Node.js 為建置基礎，充分運用巨型 node 模組生態系統，提供一種可以整合許多不同系統的工具。
{:shortdesc}

IBM 提供 Node-RED 節點，以協助您將裝置、閘道及應用程式連接至 {{site.data.keyword.iot_short_notm}}，以及快速建立 IoT 解決方案。


## Watson IoT Node   
{: #watson_iot_node}  

![Watson IoT Node 影像](../images/node-red-watson.png "Watson IoT Node 影像")


Watson IoT Node 是一對節點，用於將您的裝置或閘道連接至 {{site.data.keyword.iot_short_notm}}。裝置或閘道可以使用這些節點來傳送事件，以及從應用程式接收指令。

如需 Watson IoT Node 的相關資訊，請參閱下列資源：

- [GitHub 上的 Watson IoT Node](https://github.com/ibm-watson-iot/iot-nodered/tree/master/node-red-contrib-ibm-watson-iot)
- [Watson IoT Node 文件](https://www.npmjs.com/package/node-red-contrib-ibm-watson-iot)


## IBM IoT App Node  
{: #watson_app_node}  


![IBM IoT App Node 影像](../images/node-red-ibmiot.png "IBM IoT App Node 影像")

IBM IoT App Node 是一對節點，用於將您的應用程式連接至 {{site.data.keyword.iot_short_notm}}。應用程式可以使用節點來接收裝置事件，以及將指令傳回至裝置。

如需 IBM IoT App Node 的相關資訊，請參閱下列資源：

- [GitHub 上的 IBM IoT App Node](https://github.com/ibm-watson-iot/iot-nodered/tree/master/node-red-contrib-scx-ibmiotapp)
- [IBM IoT App Node 文件](http://flows.nodered.org/node/node-red-contrib-scx-ibmiotapp)


## 相關資訊及範例   
{: #more_info}


為協助您開始使用，請使用下列範例秘訣：
- [使用 Node-RED 開始使用 {{site.data.keyword.iot_short_notm}}](https://developer.ibm.com/recipes/tutorials/getting-started-with-watson-iot-platform-using-node-red/)
- [使用 Node-RED 將 Raspberry Pi 當作裝置連接至 {{site.data.keyword.iot_short_notm}}](https://developer.ibm.com/recipes/tutorials/deploy-watson-iot-node-on-raspberry-pi/)

如需相關資訊，另請參閱[使用 Node-RED 入門範本建立應用程式](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered)。
