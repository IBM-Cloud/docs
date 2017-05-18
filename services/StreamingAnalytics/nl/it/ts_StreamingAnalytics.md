---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Risoluzione dei problemi di {{site.data.keyword.streaminganalyticsshort}}
{: #ts_StreamingAnalytics}

Puoi trovare le risposte a domande comuni sull'utilizzo di {{site.data.keyword.streaminganalyticsshort}} in {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

##Quando avvio il servizio, mi vengono richieste le credenziali per accedere alla console
{: #log_in_console}

Quando avvii {{site.data.keyword.streaminganalyticsshort}}, ti vengono richieste le credenziali
per accedere alla console del servizio.
{:shortdesc}

Avvii un servizio {{site.data.keyword.streaminganalyticsshort}} creato in precedenza e, invece di accedere direttamente alla console del servizio, viene visualizzata una pagina di accesso in cui ti vengono richieste le credenziali.
{: tsSymptoms}

L'infrastruttura del servizio è stata aggiornata e la cache del tuo browser impedisce
al servizio di eseguire l'aggiornamento.
{: tsCauses}

Pulisci la cache del browser per essere sicuro di ottenere l'ultima versione della console del servizio.
{: tsResolve}

##La mia applicazione è in uno stato di "unhealthy" (non integro)
{: #app_unhealthy}

Non puoi eseguire la tua applicazione correttamente e lo stato di integrità è `unhealthy`.
{:shortdesc}

Invii un'applicazione all'istanza del servizio, l'applicazione viene avviata ma si verifica immediatamente un suo malfunzionamento e lo stato di integrità è `unhealthy`. Nel file di log compare il seguente errore: `/lib64/libc.so.6: version GLIBC_2.14 not found`.
{: tsSymptoms}

Non hai compilato l'applicazione utilizzando un sistema operativo RHEL 6.5 o una versione CentOS equivalente.
{: tsCauses}

Devi ricompilare la tua applicazione in un sistema operativo RHEL (Red Hat Enterprise Linux) 6.5 o una versione CentOS equivalente utilizzando processori Intel. Invia nuovamente la tua applicazione all'istanza del servizio.
{: tsResolve}
