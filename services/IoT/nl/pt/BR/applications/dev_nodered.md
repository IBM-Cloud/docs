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

# Desenvolvendo no {{site.data.keyword.iot_short_notm}} usando o Node-RED
{: #dev_nodered}

O Node-RED é uma ferramenta visual que é possível usar para desenvolver seus aplicativos, dispositivos e gateways no {{site.data.keyword.iot_full}}. O Node-RED fornece recursos para conectar dispositivos de hardware, APIs (interfaces de programação de aplicativos) e serviços on-line de maneiras novas e interessantes. O Node-RED é construído com base no Node.js e tira proveito do enorme ecossistema do módulo de nós para fornecer uma ferramenta que pode integrar muitos sistemas diferentes.
{:shortdesc}

A IBM fornece nós do Node-RED para ajudá-lo a conectar seus dispositivos, gateways e aplicativos ao {{site.data.keyword.iot_short_notm}} e para criar soluções IoT (Internet of Things) rapidamente.


## Nó Watson IoT   
{: #watson_iot_node}  

![Imagem do Watson IoT Node](../images/node-red-watson.png "Imagem do Watson IoT Node")


O Watson IoT Node é um par de nós para conectar seus dispositivos ou gateways ao {{site.data.keyword.iot_short_notm}}. Os dispositivos ou gateways podem usar esses nós para enviar eventos e receber comandos do aplicativo.

Para obter mais informações sobre o Watson IoT Node, consulte os recursos a seguir:

- [Watson IoT Node no GitHub ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-watson-iot/iot-nodered/tree/master/node-red-contrib-ibm-watson-iot){: new_window}
- [Documentação do Watson IoT Node ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://www.npmjs.com/package/node-red-contrib-ibm-watson-iot){: new_window}


## Nó do app IBM IoT  
{: #watson_app_node}  


![Imagem do IBM IoT App Node](../images/node-red-ibmiot.png "Imagem do IBM IoT App Node")

O IBM IoT App Node é um pare de nós para conectar seus aplicativos ao {{site.data.keyword.iot_short_notm}}. Os aplicativos podem usar os nós para receber eventos do dispositivo e enviar comandos de volta ao dispositivo.

Para obter mais informações sobre o IBM IoT App Node, consulte os recursos a seguir:

- [IBM IoT App Node no GitHub ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-watson-iot/iot-nodered/tree/master/node-red-contrib-scx-ibmiotapp){: new_window}
- [Documentação do IBM IoT App Node ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](http://flows.nodered.org/node/node-red-contrib-scx-ibmiotapp){: new_window}


## Mais informações e amostras   
{: #more_info}


Para ajudá-lo a começar, use as receitas de amostra a seguir:
- [Introdução ao {{site.data.keyword.iot_short_notm}} usando o Node-RED ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/recipes/tutorials/getting-started-with-watson-iot-platform-using-node-red/){: new_window}
- [Conectando o Raspberry Pi como um dispositivo ao {{site.data.keyword.iot_short_notm}} usando o Node-RED ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/recipes/tutorials/deploy-watson-iot-node-on-raspberry-pi/){: new_window}

Para obter mais informações, consulte também [Criando aplicativos com o Node-RED Starter](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered).
