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

# Sviluppo {{site.data.keyword.iot_short_notm}} utilizzando Node-RED
{: #dev_nodered}

Node-RED è uno strumento visuale che puoi utilizzare per sviluppare le tue applicazioni, dispositivi e gateway su {{site.data.keyword.iot_full}}. Node-RED fornisce le funzionalità per la connessione dei dispositivi hardware, delle API e dei servizi online in nuovi interessanti modi. Node-RED è creato con Node.js e trae vantaggio dall'immenso ecosistema del modulo del nodo per fornire uno strumento che si possa integrare in molti sistemi diversi.
{:shortdesc}

IBM fornisce i nodi Node-RED per aiutarti nella connessione ai tuoi dispositivi, gateway e applicazioni di {{site.data.keyword.iot_short_notm}} e per creare soluzioni IoT velocemente.


## Watson IoT Node   
{: #watson_iot_node}  

![Immagine Watson IoT Node](../images/node-red-watson.png "Immagine Watson IoT node")


Watson IoT Node è una coppia di nodi per la connessione dei tuoi dispositivi o gateway a {{site.data.keyword.iot_short_notm}}. I dispositivi o i gateway possono utilizzare questi nodi per inviare eventi e per ricevere comandi dall'applicazione.

Per ulteriori informazioni su Watson IoT Node, consulta le seguenti risorse:

- [Watson IoT Node su GitHub](https://github.com/ibm-watson-iot/iot-nodered/tree/master/node-red-contrib-ibm-watson-iot)
- [Documentazione Watson IoT Node](https://www.npmjs.com/package/node-red-contrib-ibm-watson-iot)


## IBM IoT App Node  
{: #watson_app_node}  


![Immagine IBM IoT App Node](../images/node-red-ibmiot.png "Immagine IBM IoT App node")

IBM IoT App Node è una coppia di nodi per la connessione delle tue applicazioni a {{site.data.keyword.iot_short_notm}}. Le applicazioni possono utilizzare i nodi per ricevere gli eventi del dispositivo e per restituire i comandi al dispositivo.

Per ulteriori informazioni su IBM IoT App Node, consulta le seguenti risorse:

- [IBM IoT App Node su GitHub](https://github.com/ibm-watson-iot/iot-nodered/tree/master/node-red-contrib-scx-ibmiotapp)
- [Documentazione IBM IoT App Node](http://flows.nodered.org/node/node-red-contrib-scx-ibmiotapp)


## Ulteriori informazioni e esempi   
{: #more_info}


Per un'introduzione, utilizza le seguenti 'ricette':
- [Getting started with {{site.data.keyword.iot_short_notm}} by using Node-RED](https://developer.ibm.com/recipes/tutorials/getting-started-with-watson-iot-platform-using-node-red/)
- [Connecting Raspberry Pi as a device to {{site.data.keyword.iot_short_notm}} by using Node-RED](https://developer.ibm.com/recipes/tutorials/deploy-watson-iot-node-on-raspberry-pi/)

Per ulteriori informazioni, consulta anche [Creating apps with Node-RED Starter](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered).
