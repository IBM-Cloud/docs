---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Informazioni
{: #about}

Puoi eseguire un'analisi in tempo reale sui dati dinamici come parte della tua applicazione {{site.data.keyword.Bluemix_short}} utilizzando
			{{site.data.keyword.streaminganalyticsfull}}.
{:shortdesc}

Nuovo utente di {{site.data.keyword.streaminganalyticsshort}}? Ottieni una [veloce introduzione al servizio](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix-2/){:new_window}.

Il servizio {{site.data.keyword.streaminganalyticsshort}}
fornisce le seguenti funzionalità che ti abilitano a distribuire, analizzare e monitorare i tuoi dati
nel cloud:

**Utilizzo programmatico e interattivo del servizio:**

Puoi utilizzare il servizio in modo interattivo tramite la [console {{site.data.keyword.streaminganalyticsshort}}](/docs/services/StreamingAnalytics/c_streams_console.html) o in modo programmatico tramite l'[API REST {{site.data.keyword.streaminganalyticsshort}}](https://console.ng.bluemix.net/apidocs/220){:new_window}.

**Distribuzione e monitoraggio di applicazioni SPL, Java, Scala e Python:**

Puoi scrivere applicazioni {{site.data.keyword.streamsshort}} in SPL, Java, Scala e Python. [Distribuisci e monitora queste applicazioni](/docs/services/StreamingAnalytics/t_deploytocloud.html) utilizzando la console {{site.data.keyword.streaminganalyticsshort}}.

Se vuoi scrivere le tue applicazioni in SPL, dovresti sapere che SPL ({{site.data.keyword.streamsfull}} Processing Language) è un linguaggio di programmazione utilizzato per creare applicazioni di elaborazione dei flussi. Se vuoi fare ancora di più con le tue applicazioni SPL, puoi ottenere un ambiente di sviluppo {{site.data.keyword.streamsshort}} e devi preparare le tue applicazioni SPL per il cloud.

Per creare e distribuire applicazioni Python senza un ambiente di sviluppo {{site.data.keyword.streamsshort}}, utilizza i nostri notebook in IBM DSX (Data Science Experience) oppure la API {{site.data.keyword.streamsshort}} Python. Per ulteriori informazioni, consulta [Sviluppo di applicazioni Python per {{site.data.keyword.streaminganalyticsshort}}](/docs/services/StreamingAnalytics/t_develop_apps_python.html).

**Compatibilità con gli operatori {{site.data.keyword.streamsshort}}:**

Gli operatori {{site.data.keyword.streamsshort}} nel toolkit standard [{{site.data.keyword.streamsshort}} Processing Language (SPL) dovrebbero essere compatibili](/docs/services/StreamingAnalytics/c_beta_adapters.html) con {{site.data.keyword.streaminganalyticsshort}}.

## Responsabilità
{{site.data.keyword.streaminganalyticsfull}}
{: #responsibilities notoc}

### Responsabilità del cliente
{: #clientresponsibilities notoc}

Il cliente è responsabile di:

* Successivamente alla configurazione iniziale di IBM di {{site.data.keyword.streamsshort}}, di monitorare, configurare e gestire
i lavori {{site.data.keyword.streamsshort}} in esecuzione della loro istanza. Il cliente ha la flessibilità di avviare e arrestare l'istanza e di avviare e arrestare i lavori in esecuzione
sull'istanza.
* Sviluppare, quando necessario o richiesto, programmi e applicazioni sul servizio per l'analisi dei dati
e ottenere i relativi approfondimenti. Il Cliente è inoltre responsabile della qualità e delle prestazioni
di tali programmi o applicazioni sviluppati. I programmi possono essere sviluppati in SPL, Java o altri linguaggi
supportati utilizzando la funzione {{site.data.keyword.streamsshort}}
Topology. Devono essere compilati utilizzando {{site.data.keyword.streamsshort}} Developer Edition o {{site.data.keyword.streamsshort}} Quick Start Edition con lo stesso sistema operativo adoperato per {{site.data.keyword.streaminganalyticsshort}}.
* Controllare periodicamente il seguente link per essere informati su un tempo di inattività continuato o interrotto pianificato - [https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window}  
* Eseguire il backup di tutti i dati, metadati, file di configurazione e parametri di ambiente in base ai requisiti
aziendali per garantire la continuità.
* Ripristinare tutti i dati, metadati, file di configurazione e parametri di ambiente da qualsiasi backup
per garantire la continuità, in caso di eventuale malfunzionamento di qualsiasi genere, tra cui
un malfunzionamento del data center, del pod, del server, del disco rigido o del software.

### Responsabilità di IBM
{: #ibmresponsibilities notoc}

Come parte di {{site.data.keyword.streaminganalyticsfull}}, IBM provvederà a:

* Fornire e gestire i server, l'archiviazione e l'infrastruttura di rete per l'istanza del cliente.
* Fornire una configurazione iniziale di {{site.data.keyword.streamsshort}} sul numero di nodi selezionato.
* Fornire e gestire l'infrastruttura per il firewall interno e verso Internet per la protezione e
l'isolamento.
* Monitorare e gestire i seguenti componenti su {{site.data.keyword.streaminganalyticsfull}}:
	* Componenti di rete
	* I server e la relativa archiviazione locale
	* Sistemi operativi dell'infrastruttura
	* Servizi di gestione {{site.data.keyword.streamsshort}}
	* Istanze {{site.data.keyword.streamsshort}}
* Fornire le patch per la manutenzione, incluse le patch di sicurezza appropriate per i sistemi
operativi dell'infrastruttura e {{site.data.keyword.streamsshort}}.
* La manutenzione periodica per cui non è richiesto alcun tempo di inattività del sistema (manutenzione “continuata”) e la manutenzione per cui è richiesto un tempo di inattività del sistema e il riavvio (manutenzione “interrotta”), saranno eseguite in base ad orari pianificati pubblicati in [https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window}
* Qualsiasi modifica agli orari della manutenzione pianificata sarà pubblicata con adeguato preavviso.
