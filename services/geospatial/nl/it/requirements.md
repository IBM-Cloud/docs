---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Requisiti del servizio
{: #requirements}


##Requisiti per i messaggi del dispositivo MQTT

* Il broker dei messaggi MQTT deve fornire i messaggi del dispositivo in formato JSON
su uno o più argomenti MQTT.
* I messaggi del dispositivo possono ottenere un qualsiasi numero di attributi, ma
i tre seguenti attributi sono sempre richiesti:
	* Un attributo che identifica in modo univoco il dispositivo.
	* Un attributo che specifica la latitudine della posizione corrente del
dispositivo.
	* Un attributo che specifica la longitudine della posizione corrente del
dispositivo.
* Sono supportate due modalità di messaggio:
	* Un messaggio MQTT può contenere un oggetto JSON con informazioni su un
singolo dispositivo.
	* Un messaggio MQTT può contenere un array di oggetti JSON con informazioni su un
insieme di dispositivi.

##Eventi MQTT e configurazione del servizio

La tua
applicazione sottoscrive i messaggi MQTT e controlla {{site.data.keyword.geospatialshort_Geospatial}} attraverso
la sua [API REST](https://console.ng.bluemix.net/apidocs/246). Mediante le chiamate dell'API REST,
sono disponibili le seguenti azioni:

* Configurare e avviare il servizio.
* Aggiungere e rimuovere regioni geografiche da monitorare.
* Richiamare informazioni sullo stato del servizio e sull'insieme di regioni
attualmente definite.
* Arresta il servizio.
* Riavviare un servizio già configurato.

