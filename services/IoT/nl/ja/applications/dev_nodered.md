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

# Node-RED による {{site.data.keyword.iot_short_notm}} の開発
{: #dev_nodered}

Node-RED は、{{site.data.keyword.iot_full}} のアプリケーション、デバイス、ゲートウェイの開発に使用できるビジュアル・ツールです。Node-RED を使用すると、新しく興味深い方法でハードウェア・デバイス、API、オンライン・サービスを接続できます。Node.js をベースとする Node-RED は、大規模なノード・モジュール・エコシステムを活用して、多様なシステムを統合できるツールを提供します。
{:shortdesc}

IBM は、デバイス、ゲートウェイ、アプリケーションを {{site.data.keyword.iot_short_notm}} に接続したり、IoT ソリューションを素早く作成したりできるように、Node-RED ノードを用意しています。


## Watson IoT Node   
{: #watson_iot_node}  

![Watson IoT Node イメージ](../images/node-red-watson.png "Watson IoT Node イメージ")


Watson IoT Node は、デバイスまたはゲートウェイを {{site.data.keyword.iot_short_notm}} に接続するための 1 組のノードです。デバイスまたはゲートウェイはこれらのノードを使用して、イベントを送信したり、アプリケーションからコマンドを受信したりできます。

Watson IoT Node について詳しくは、次のリソースを参照してください。

- [GitHub の Watson IoT Node](https://github.com/ibm-watson-iot/iot-nodered/tree/master/node-red-contrib-ibm-watson-iot)
- [Watson IoT Node 資料](https://www.npmjs.com/package/node-red-contrib-ibm-watson-iot)


## IBM IoT App Node  
{: #watson_app_node}  


![IBM IoT App Node イメージ](../images/node-red-ibmiot.png "IBM IoT App Node イメージ")

IBM IoT App Node は、アプリケーションを {{site.data.keyword.iot_short_notm}} に接続するための 1 組のノードです。アプリケーションはこれらのノードを使用して、デバイス・イベントを受信し、対象デバイスにコマンドを戻すことができます。

IBM IoT App Node について詳しくは、次のリソースを参照してください。

- [GitHub の IBM IoT App Node](https://github.com/ibm-watson-iot/iot-nodered/tree/master/node-red-contrib-scx-ibmiotapp)
- [IBM IoT App Node 資料](http://flows.nodered.org/node/node-red-contrib-scx-ibmiotapp)


## 詳細とサンプル   
{: #more_info}


初めて使用する場合は、次のサンプル・レシピを使用すると役に立ちます。
- [Getting started with {{site.data.keyword.iot_short_notm}} by using Node-RED](https://developer.ibm.com/recipes/tutorials/getting-started-with-watson-iot-platform-using-node-red/)
- [Connecting Raspberry Pi as a device to {{site.data.keyword.iot_short_notm}} by using Node-RED](https://developer.ibm.com/recipes/tutorials/deploy-watson-iot-node-on-raspberry-pi/)

詳しくは、[Node-RED Starter によるアプリの作成](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered)も参照してください。
