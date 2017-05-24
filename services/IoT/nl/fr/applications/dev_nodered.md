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

# Développement de {{site.data.keyword.iot_short_notm}} à l'aide de Node-RED
{: #dev_nodered}

Node-RED est un outil visuel que vous pouvez utiliser pour développer vos applications, vos terminaux et vos passerelles sur {{site.data.keyword.iot_full}}. Node-RED fournit des fonctionnalités permettant de connecter des terminaux matériels, des API et des services en ligne de façon inédite et intéressante. Node-RED est généré par dessus Node.js et exploite l'immense écosystème de module de noeuds pour fournir un outil capable d'intégrer un grand nombre de systèmes différents.
{:shortdesc}

IBM fournit des noeuds Node-RED afin de vous aider à connecter vos terminaux, passerelles et applications à {{site.data.keyword.iot_short_notm}} et à créer rapidement des solutions IoT.


## Watson IoT Node   
{: #watson_iot_node}  

![Image Watson IoT Node](../images/node-red-watson.png "Image Watson IoT Node")


Watson IoT Node est une paire de noeuds vous permettant de connecter vos terminaux ou passerelles à {{site.data.keyword.iot_short_notm}}. Les terminaux ou les passerelles peuvent utiliser ces noeuds pour envoyer des événements et pour recevoir des commandes de l'application.

Pour plus d'informations sur Watson IoT Node, voir les ressources suivantes :

- [Watson IoT Node sur GitHub ![Icône de lien externe](../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-nodered/tree/master/node-red-contrib-ibm-watson-iot){: new_window}
- [Documentation Watson IoT Node ![Icône de lien externe](../../../icons/launch-glyph.svg "External link icon")](https://www.npmjs.com/package/node-red-contrib-ibm-watson-iot){: new_window}


## IBM IoT App Node  
{: #watson_app_node}  


![Image IBM IoT App Node](../images/node-red-ibmiot.png "Image IBM IoT App Node")

IBM IoT App Node est une paire de noeuds permettant de connecter vos applications à {{site.data.keyword.iot_short_notm}}. Les applications peuvent utiliser les noeuds pour recevoir des événements de terminal et pour renvoyer des commandes au terminal.

Pour plus d'informations sur IBM IoT App Node, voir les ressources suivantes :

- [IBM IoT App Node sur GitHub ![Icône de lien externe](../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-nodered/tree/master/node-red-contrib-scx-ibmiotapp){: new_window}
- [Documentation IBM IoT App Node ![Icône de lien externe](../../../icons/launch-glyph.svg "External link icon")](http://flows.nodered.org/node/node-red-contrib-scx-ibmiotapp){: new_window}


## Informations complémentaires et exemples   
{: #more_info}


Pour vous aider à démarrer, utilisez les exemples de recette suivants :
- [Getting started with {{site.data.keyword.iot_short_notm}} by using Node-RED ![Icône de lien externe](../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/getting-started-with-watson-iot-platform-using-node-red/){: new_window}
- [Connecting Raspberry Pi as a device to {{site.data.keyword.iot_short_notm}} by using Node-RED ![Icône de lien externe](../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/deploy-watson-iot-node-on-raspberry-pi/){: new_window}

Pour plus d'informations, voir aussi [Creating apps with Node-RED Starter](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered).
