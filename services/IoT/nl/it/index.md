---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introduzione a {{site.data.keyword.iot_short_notm}}
{: #gettingstartedtemplate}
Ultimo aggiornamento: 26 agosto 2016
{: .last-updated}

{{site.data.keyword.iot_full}} per {{site.data.keyword.Bluemix_notm}} ti fornisce un toolkit versatile che include i dispositivi gateway, la gestione del dispositivo e l'accesso all'applicazione potente. Utilizzando {{site.data.keyword.iot_short_notm}}, puoi collegare i dati dei dispositivi connessi ed eseguire analisi dei dati in tempo reale per la tua organizzazione.
{:shortdesc}

## Prima di cominciare
{: #byb}

Prima di collegare i dispositivi utilizzando i dati, deve esistere un'istanza del servizio {{site.data.keyword.iot_short_notm}} nella tua organizzazione {{site.data.keyword.Bluemix_notm}}. Puoi crearla direttamente dalla pagina [{{site.data.keyword.iot_short_notm}} nel catalogo dei servizi Bluemix](https://console.{DomainName}/catalog/services/internet-of-things-platform/).  

## Passo 1: Collega i tuoi dispositivi
{: #up_and_running}

Per essere operativo con il servizio, esplora le seguenti opzioni in base alla tua situazione.

   |   Il servizio è stato distribuito | Il servizio non è stato distribuito
  ------------- | -------------
  **Ho un dispositivo da collegare** | [Collega il tuo dispositivo a {{site.data.keyword.iot_short_notm}}](iotplatform_task.html#iotplatform_task).| Esplora la connessione del dispositivo nella demo [Play organization](http://discover-iot.eu-gb.mybluemix.net/?cm_mc_uid=44491599487314618721024&cm_mc_sid_50200000=1462798151#/play){:new_window}.
  **Non ho un dispositivo da collegare** | [Crea e collega un simulatore del dispositivo Node-RED](nodereddevice_sample.html){:new_window}. | Introduzione a [Watson IoT Platform Starter](https://new-console.stage1.ng.bluemix.net/docs/starters/IoT/iot500.html){:new_window}.
Per ulteriori informazioni su come collegare tipi di dispositivi specifici a {{site.data.keyword.iot_short_notm}}, consulta [developerWorks recipes](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window}.  

Per la documentazione dello sviluppatore per la connessione del dispositivo, consulta:
- [Connettività MQTT per i dispositivi](devices/mqtt.html).
- [Connettività MQTT per i gateway](gateways/mqtt.html).

## Passo 2: Analizza i dati del tuo dispositivo
{: #analyzing_data}

Inizia l'esplorazione dei dati in tempo reale che il dispositivo sta inviando a {{site.data.keyword.iot_short_notm}}.

{{site.data.keyword.iot_short_notm}} include i seguenti strumenti di analisi:  
- [Tabelle e schede](data_visualization.html) per visualizzare i tuoi dati del dispositivo in tempo reale.
- [Regole e azioni](analytics.html) che vengono attivate dai dati del dispositivo in tempo reale.

Per un esempio di introduzione rapida, consulta la ricetta [Using Rules and Actions with IBM Watson IoT Platform Cloud Analytics](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){:new_window} developerWorks.

## Passo 3: Crea applicazioni che utilizzano i tuoi dati del dispositivo
{: #develop_applications}

Estendi le funzioni di analisi dati di {{site.data.keyword.iot_short_notm}} creando le tue proprie applicazioni per utilizzare i dati del dispositivo cronologici e in tempo reale.

Per ulteriori informazioni, consulta i seguenti argomenti:   
- Esplora la [documentazione dello sviluppatore dell'applicazione](applications/api.html) e la documentazione API [{{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/){:new_window}.
- Esplora le [librerie client {{site.data.keyword.iot_short_notm}}](iot_platform_client_lib.html) che forniscono gli strumenti e i file per creare e sviluppare il codice per l'integrazione e la connettività dei tuoi dispositivi e applicazioni.
- [Collega il servizio {{site.data.keyword.cloudantfull}}](cloudant_connector.html) al tuo {{site.data.keyword.iot_short_notm}} per archiviare i dati del dispositivo cronologici.




# Link correlati 
{: #rellinks}
## Esercitazioni ed esempi
{: #samples}
* [Recipes for connecting your devices](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window}
* [{{site.data.keyword.iot_short_notm}} Play organization](https://play.internetofthings.ibmcloud.com/){:new_window}
* [Connecting an Intel Galileo to the {{site.data.keyword.iot_short_notm}}](https://developer.ibm.com/recipes/tutorials/connect-an-intel-galileo-to-the-internet-of-things-foundation-connect/){:new_window}
* [Connecting an ARM® mbed™ IoT Starter Kit](https://developer.ibm.com/recipes/tutorials/arm-mbed-iot-starter-kit-part-1/){:new_window}
* [Connecting a Raspberry Pi to {{site.data.keyword.iot_short_notm}}](https://developer.ibm.com/recipes/tutorials/raspberry-pi-4/){:new_window}

## Guida di riferimento API
{: #api}
* Documentazione API [{{site.data.keyword.iot_short_notm}}
* [Documentazione sviluppatore](developer_doc_overview.html)(https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/)]
