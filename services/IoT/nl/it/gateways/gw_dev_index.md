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

# Sviluppo dei gateway su {{site.data.keyword.iot_short_notm}}
{: #gw_dev_index}

Se i tuoi dispositivi non possono collegarsi direttamente a internet, puoi creare un dispositivo gateway per richiamare e inviare dati per le applicazioni nella tua organizzazione {{site.data.keyword.iot_full}}. Vengono forniti esempi, librerie client e informazioni per aiutarti nel collegamento dei gateway del dispositivo alla tua organizzazione e applicazioni {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Protocolli di connessione
Gateway collegati a {{site.data.keyword.iot_short_notm}} utilizzando il protocollo di messaggistica MQTT. Connessione dei gateway a {{site.data.keyword.iot_short_notm}} utilizzando la messaggistica HTTP non è supportata. Solo i dispositivi si possono collegare utilizzando la messaggistica HTTP.

## Librerie client
Le librerie client per lo sviluppo dei gateway che possono collegarsi a {{site.data.keyword.iot_short_notm}} sono disponibili nelle seguenti lingue:

|Libreria client |Link alla libreria per ulteriore documentazione
|:---|:---
|C++|[https://github.com/ibm-watson-iot/iot-cpp ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-watson-iot/iot-cpp){: new_window}
|C#|[https://github.com/ibm-watson-iot/iot-csharp ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-watson-iot/iot-csharp){: new_window}
|Embedded C| [https://github.com/ibm-watson-iot/iot-embeddedc ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-watson-iot/iot-embeddedc){: new_window}
|Java™|[https://github.com/ibm-watson-iot/iot-java ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-watson-iot/iot-java){: new_window}
|mBed C++|[https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/ ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/){: new_window}
|Node.js|[https://github.com/ibm-watson-iot/iot-nodejs ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-watson-iot/iot-nodejs){: new_window}
|Node-RED|[https://github.com/ibm-watson-iot/iot-nodered ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-watson-iot/iot-nodered){: new_window}
|Python|[https://github.com/ibm-watson-iot/iot-python ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-watson-iot/iot-python){: new_window}

Per ulteriori informazioni e link alle librerie client disponibili, consulta [Librerie client per lo sviluppo {{site.data.keyword.iot_short_notm}}](../iot_platform_client_lib.html).

## Analisi edge
{: #eaa_community}

La funzione {{site.data.keyword.iot_short_notm}} Edge Analytics ti consente di eseguire {{site.data.keyword.iot_short_notm}} Analytics su un dispositivo gateway. Utilizza Edge Analytics per analizzare e rispondere ai dati raccolti ai margini della rete. Puoi anche inviare i dati del dispositivo a {{site.data.keyword.iot_short_notm}} per un'ulteriore elaborazione analitica, per la visualizzazione del dashboard, come input per altre analisi o per memorizzarli in un repository cronologico basato su cloud.

Puoi scaricare l'SDK Edge Analytics dalla [pagina della community di IBM Edge Analytics ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/developerworks/community/groups/service/html/communitystart?communityUuid=3df173af-0c21-4b9c-9fd1-e8e5561ef460&ftHelpTip=true){: new_window}. L'SDK include il file JAR SDK, javadoc, il codice di esempio, link alle "ricette" e i file README. Nella community, potrai anche guardare i video per essere subito operativo con Edge Analytics e puoi utilizzare il forum per chiedere informazioni.
