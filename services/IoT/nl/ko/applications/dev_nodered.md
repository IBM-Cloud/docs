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

# Node-RED를 사용하여 {{site.data.keyword.iot_short_notm}} 개발
{: #dev_nodered}

Node-RED는 {{site.data.keyword.iot_full}}에서 애플리케이션, 디바이스 및 게이트웨이를 개발하는 데 사용할 수 있는 시각적 도구입니다. Node-RED는 새롭고 흥미로운 방식으로 하드웨어 디바이스, API 및 온라인 서비스를 연결하기 위한 기능을 제공합니다. Node-RED는 Node.js 위에서 빌드되며, 대형 노드 모듈 에코시스템을 활용하여 여러 다양한 시스템을 통합할 수 있는 도구를 제공합니다.
{:shortdesc}

IBM에서는 디바이스, 게이트웨이 및 애플리케이션을 {{site.data.keyword.iot_short_notm}}에 연결하며 IoT 솔루션을 신속하게 작성하는 데 도움이 되는 Node-RED 노드를 제공합니다. 


## Watson IoT Node   
{: #watson_iot_node}  

![Watson IoT Node 이미지](../images/node-red-watson.png "Watson IoT Node 이미지")


Watson IoT Node는 디바이스 또는 게이트웨이를 {{site.data.keyword.iot_short_notm}}에 연결하기 위한 한 쌍의 노드입니다. 디바이스 또는 게이트웨이는 이러한 노드를 사용하여 이벤트를 전송하고 애플리케이션의 명령을 수신할 수 있습니다. 

Watson IoT Node에 대한 자세한 정보는 다음 자원을 참조하십시오. 

- [GitHub의 Watson IoT Node](https://github.com/ibm-watson-iot/iot-nodered/tree/master/node-red-contrib-ibm-watson-iot)
- [Watson IoT Node 문서](https://www.npmjs.com/package/node-red-contrib-ibm-watson-iot)


## IBM IoT App Node  
{: #watson_app_node}  


![IBM IoT App Node 이미지](../images/node-red-ibmiot.png "IBM IoT App Node 이미지")

IBM IoT App Node는 애플리케이션을 {{site.data.keyword.iot_short_notm}}에 연결하기 위한 한 쌍의 노드입니다. 애플리케이션은 노드를 사용하여 디바이스 이벤트를 수신하고 명령을 다시 디바이스로 전송할 수 있습니다. 

IBM IoT App Node에 대한 자세한 정보는 다음 자원을 참조하십시오. 

- [GitHub의 IBM IoT App Node](https://github.com/ibm-watson-iot/iot-nodered/tree/master/node-red-contrib-scx-ibmiotapp)
- [IBM IoT App Node 문서](http://flows.nodered.org/node/node-red-contrib-scx-ibmiotapp)


## 자세한 정보 및 샘플   
{: #more_info}


시작하는 데 도움을 받으려면 다음 샘플 레시피를 사용하십시오. 
- [Node-RED를 사용하여 {{site.data.keyword.iot_short_notm}} 시작하기](https://developer.ibm.com/recipes/tutorials/getting-started-with-watson-iot-platform-using-node-red/)
- [Node-RED를 사용하여 {{site.data.keyword.iot_short_notm}}에 디바이스로서 Raspberry Pi 연결](https://developer.ibm.com/recipes/tutorials/deploy-watson-iot-node-on-raspberry-pi/)

자세한 정보는 [Node-RED 스타터로 앱 작성](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered)도 참조하십시오. 
