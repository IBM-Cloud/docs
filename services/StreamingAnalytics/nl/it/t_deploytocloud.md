---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Distribuzione delle applicazioni {{site.data.keyword.streamsshort}} al
cloud
{: #t_deploytocloud}

Puoi distribuire le tue applicazioni {{site.data.keyword.streamsshort}}
all'istanza {{site.data.keyword.streaminganalyticsshort}}
in esecuzione nel {{site.data.keyword.Bluemix_short}}
cloud.
{:shortdesc}

Le applicazioni {{site.data.keyword.streamsshort}} sono scritte in {{site.data.keyword.streamsshort}} Processing Language (SPL) in un ambiente {{site.data.keyword.streamsshort}}. {{site.data.keyword.streamsshort}} supporta inoltre diversi kit di sviluppo Java™ che puoi utilizzare per sviluppare le tue applicazioni. Per ulteriori informazioni sul supporto Java in  {{site.data.keyword.streamsshort}}, consulta [Supported Java development kits for application development](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-prerequisites-java-supported-sdks.html){:new_window}. 
{{site.data.keyword.streaminganalyticsshort}} non include un ambiente di sviluppo
{{site.data.keyword.streamsshort}} nel
cloud, ma puoi distribuire le applicazioni che sviluppi localmente al cloud.

Prima di iniziare, disabilita il Blocco popup del tuo browser per visualizzare la console Streaming Analytics.

Per distribuire le tue applicazioni {{site.data.keyword.streamsshort}}
al cloud:

1. Configura un ambiente {{site.data.keyword.streamsshort}} per lo sviluppo
e la verifica della tua applicazione. 

	Se non disponi di un ambiente {{site.data.keyword.streamsshort}}, puoi scaricare la
{{site.data.keyword.streamsshort}} Quick Start Edition,
gratuitamente. Vai alla [pagina del prodotto IBM Streams](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window} e fai clic su **Download the native software installation**.

2. Sviluppa la tua applicazione SPL o Java nel tuo ambiente {{site.data.keyword.streamsshort}} utilizzando Streams Studio o gli strumenti della riga di comando.
3. Verifica che la tua applicazione SPL o Java sia correttamente in esecuzione nel tuo ambiente di sviluppo.
4. Invia il bundle dell'applicazione (il file .sab) associato alla tua applicazione SPL o Java alla tua istanza del servizio nel cloud utilizzando uno dei seguenti metodi:
	* Utilizza la console {{site.data.keyword.streaminganalyticsshort}}
per inviare il bundle dell'applicazione.
    * Sviluppa un'applicazione {{site.data.keyword.Bluemix_short}} e aggiungi l'applicazione
{{site.data.keyword.streamsshort}} ad essa. Controllala utilizzando l'API REST {{site.data.keyword.streaminganalyticsshort}}.

La tua applicazione è ora distribuita nel cloud. Puoi monitorarla utilizzando il servizio
{{site.data.keyword.streaminganalyticsshort}}. Puoi anche inviare più di un'applicazione SPL o Java (file .sab) alla tua istanza del servizio. Puoi inviarne quante desideri.
