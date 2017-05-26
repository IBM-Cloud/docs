---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connessione e configurazione di un servizio storico utilizzando {{site.data.keyword.messagehub}}  
{: #messagehub_main}

La connessione di {{site.data.keyword.messagehub_full}} a {{site.data.keyword.iot_short}} fornisce un bus di messaggi scalabile, di velocità elevata per l'archiviazione dei dati cronologici. {{site.data.keyword.messagehub}} è creato con Apache Kafka, che è un sistema di messaggistica open-source, di velocità elevata che fornisce una piattaforma a bassa latenza per la gestione dei feed di dati in tempo reale.

## Prima di cominciare  
{: #byb}

Prima del collegamento di {{site.data.keyword.messagehub}} al tuo servizio {{site.data.keyword.iot_short}} , completa le seguenti attività:

- Configura {{site.data.keyword.messagehub}} nello stesso spazio {{site.data.keyword.Bluemix_notm}} del tuo {{site.data.keyword.iot_short_notm}} utilizzando il catalogo {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni su {{site.data.keyword.messagehub}}, consulta [Getting started with {{site.data.keyword.messagehub}}](https://console.{DomainName}/docs/services/MessageHub/index.html).

- Assicurati di disporre dei privilegi da sviluppatore nell'organizzazione {{site.data.keyword.Bluemix_notm}} e di essere registrato tramite {{site.data.keyword.Bluemix_notm}}. Se non sei registrato con {{site.data.keyword.Bluemix_notm}} o non disponi dei privilegi da sviluppatore in questa organizzazione {{site.data.keyword.Bluemix_notm}}, non sarai in grado di autorizzare il bind di {{site.data.keyword.messagehub}} e di {{site.data.keyword.iot_short_notm}}.

## Collegamento

Per collegare {{site.data.keyword.messagehub}} all'archivio dei dati cronologici:

1. Nel tuo dashboard {{site.data.keyword.iot_short}} fai clic su **Extensions** nella barra di navigazione.
2. Nel tile Historical Data Storage, fai clic su **Setup**.
4. Seleziona il servizio {{site.data.keyword.messagehub}} che desideri collegare.  
Vengono elencati tutti i servizi {{site.data.keyword.messagehub}} disponibili nello stesso spazio {{site.data.keyword.Bluemix_notm}} del tuo servizio {{site.data.keyword.iot_short}} nella sezione Configure historical data storage.
5. Seleziona le tue opzioni di configurazione {{site.data.keyword.messagehub}}:
 1. Seleziona un fuso orario.  
 Le date/ore nei dati del dispositivo inviati a {{site.data.keyword.messagehub}} sono convertiti nel fuso orario selezionato.
 2. Seleziona un argomento predefinito.  
 Gli eventi del dispositivo vengono inviati all'argomento predefinito se ne è stato definito uno. Per utilizzare più assegnazioni dell'argomento granulari, lascia vuoto l'argomento predefinito e aggiungi delle regole di inoltro personalizzate.
 3. Facoltativo: specifica le regole di inoltro personalizzate.  
 Specifica ulteriori regole per l'inoltro degli eventi del dispositivo. Solo gli eventi che corrispondono alle regole di inoltro personalizzate vengono inoltrate.  
 **Nota:** un evento può avere più regole di inoltro e può essere inoltrato a più argomenti {{site.data.keyword.messagehub}}.
 4. Facoltativo: configura gli argomenti.  
 Per creare gli argomenti con più di due partizioni predefinite, puoi specificare la configurazione della partizione.
 5. Fai clic su **Done**.
5. Fai clic su **Authorize**.
6. Nella finestra di dialogo dell'autorizzazione, fai clic su **Confirm**.

I tuoi dati del dispositivo sono ora archiviati nel tuo {{site.data.keyword.messagehub}}.
