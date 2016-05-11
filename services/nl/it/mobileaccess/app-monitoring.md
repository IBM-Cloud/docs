---

copyright:
  years: 2015, 2016
  
---

# Monitoraggio applicazioni
{: #app-monitoring}

Oltre alle funzioni di sicurezza, {{site.data.keyword.amafull}} fornisce anche il monitoraggio e l'analisi per le tue applicazioni mobili. Puoi registrare i log client e i dati di monitoraggio con l'SDK client {{site.data.keyword.amashort}}. Gli sviluppatori possono controllare quando inviare questi dati al servizio {{site.data.keyword.amashort}}. Tutti gli eventi di sicurezza, quali la riuscita o meno dell'autenticazione, che si verificano nel servizio {{site.data.keyword.amashort}} vengono registrati automaticamente.

Quando i dati vengono distribuiti a {{site.data.keyword.amashort}}, puoi utilizzare il dashboard di monitoraggio {{site.data.keyword.amashort}} per ottenere informazioni approfondite di analisi relative alle tue applicazioni mobili e ai tuoi dispositivi e log client. Le informazioni sulle richieste effettuate dalla tua applicazione alle risorse protette {{site.data.keyword.amashort}} sono registrate per impostazione predefinita.

I dati registrati automaticamente includono informazioni quali il numero di autenticazioni, nuovi dispositivi e nuovi utenti. Puoi inoltre configurare
l'SDK client {{site.data.keyword.amashort}} per notificare le seguenti informazioni:

### Statistiche di utilizzo delle tue applicazioni mobili
{: #usage-stats}

Puoi configurare le tue applicazioni mobili per registrare gli eventi del ciclo di vita dell'applicazione e inviare i dati registrati al servizio {{site.data.keyword.amashort}} con poche e semplici chiamate API. Puoi registrare il
                                numero di aperture di applicazioni, notifiche di push ricevute e così via.

### Acquisizione di log lato client
{: #client-side-logcapture}

Le applicazioni in uso di produzione di tanto in tanto riscontrano dei problemi la cui
                                correzione richiede l'attenzione di uno sviluppatore. È spesso difficile riprodurre
                                tali problemi. <!--in R&D.--> Gli sviluppatori che hanno lavorato sul codice potrebbero non disporre
                                dell'ambiente o dell'esatto dispositivo con cui eseguire la verifica. In tali situazioni,
                                è utile poter richiamare i log di debug dai dispositivi client poiché i problemi si verificano
                                nell'ambiente in cui succedono.

## Conservazione dei dati catturati
{: #preserve-captureddata}

Non c'è modo di garantire che tutti i dati catturati vengano conservati sul lato client. I tuoi utenti
                                potrebbero eseguire l'applicazione mobile non in linea e accumulare simultaneamente
                                dati di analisi e di log acquisiti. Poiché il client è non in linea con uno spazio
                                su file system limitato, gli eventi registrati meno recenti devono essere
                                eliminati al fine di conservare gli eventi registrati più di recente. Spetta allo sviluppatore decidere quando inviare i dati catturati
al servizio {{site.data.keyword.amashort}} utilizzando le API fornite.

## Utilizzo del dashboard di monitoraggio {{site.data.keyword.amashort}}
{: #monitoring-dashboard}

1. Apri il dashboard {{site.data.keyword.Bluemix}} e fai clic sull'applicazione {{site.data.keyword.Bluemix_notm}}

2. Quando il tuo dashboard dell'applicazione {{site.data.keyword.Bluemix_notm}} viene aperto, fai clic su un tile {{site.data.keyword.amashort}}

3. Nel dashboard {{site.data.keyword.amashort}}, fai clic sul link `Monitoraggio` nel menu di sinistra

## Fasi successive
{: #next-steps}
* [Abilitazione, configurazione e utilizzo del Logger](app-monitoring-logger.html)
* [Raccolta dell'analisi dell'utilizzo](app-monitoring-gathering-analytics.html)
