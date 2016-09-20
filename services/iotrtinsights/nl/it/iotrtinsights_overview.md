---

copyright:
  years: 2015,2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Informazioni su {{site.data.keyword.iotrtinsights_short}}
{: #iotrtinsights_overview}
*Ultimo aggiornamento: 11 febbraio 2016*

{{site.data.keyword.iotrtinsights_short}} fornisce un motore di analisi in tempo reale e una funzionalità di creazione di analisi che abilita la contestualizzazione e il monitoraggio di dati dispositivo IoT, accelera la comprensione delle condizioni correnti e migliora i processi decisionali e le risposte ai problemi emergenti.
{:shortdesc}

## {{site.data.keyword.iotrtinsights_full}}
{: #iotrtinsights_concept}
{{site.data.keyword.iotrtinsights_short}} utilizza un semplice modello di composizione basato sulle regole e un framework estensibile per aiutarti ad avvalerti dei dati Internet delle cose (o IoT, Internet of Things), combinarli con i dati risorsa master, analizzare le situazioni in contesto e automatizzare le risposte per migliorare le operazioni, la disponibilità e i livelli di servizio.

{{site.data.keyword.iotrtinsights_short}} stabilisce una connessione a Internet delle cose ({{site.data.keyword.iot_short}}) di {{site.data.keyword.bluemix}} per dei feed di dati dispositivo in tempo reale. I dati in entrata sono interpretati mediante un modello di dati virtuale che può essere incrementato con i dati master di risorsa da un sistema di gestione risorse come IBM Maximo&reg; Asset Management.

Al flusso di dati vengono inoltre applicate le regole definite dall'utente per identificare le condizioni che richiedono attenzione. Il motore delle azioni ti consente di definire delle risposte automatizzate alle condizioni rilevate, come l'invio di una email, l'attivazione di una ricetta IFTTT, l'esecuzione di un flusso di lavoro Node-RED o l'utilizzo dei webhook per stabilire una connessione a una gamma di servizi web.  

Infine, i dati in tempo reale sono visualizzati anche in un dashboard configurabile per una vista immediata di ubicazione, dati, metriche e avvisi per i tuoi dispositivi IoT.

![L'architettura di {{site.data.keyword.iotrtinsights_short}}.](images/iota.svg "{{site.data.keyword.iotrtinsights_short}} architecture")
