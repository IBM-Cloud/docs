---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Novità in {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}}
{: #what-is-new}


## Novità a partire da marzo 2017 
{: #mar-2017}

L'aggiornamento di marzo 2017 della {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} introduce le seguenti modifiche:

   * Il dashboard mobile {{site.data.keyword.Bluemix_notm}} è ora la {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}}.
   * La creazione del progetto è stata riprogettata per includere i tipi di modello del server Applicazione web, BFF e Microservizio con il supporto per Node.js, Java e Swift.
   * L'integrazione con il nuovo e migliorato servizio {{site.data.keyword.appid_full}} fornisce l'autenticazione per i progetti mobili e web.
   * Puoi ora anche generare SDK per i tuoi progetti utilizzando il [Plugin SDK Generator](sdk_cli.html). SDK generation nella {{site.data.keyword.dev_console}} è disponibile solo per i progetti mobili.
   * Puoi ora anche creare i progetti utilizzando la [{{site.data.keyword.dev_cli_short}}](dev_cli.html).


## Novità a partire da gennaio 2017
{: #jan-2017}

L'aggiornamento di gennaio 2017 del dashboard {{site.data.keyword.Bluemix_notm}} Mobile introduce le seguenti modifiche:

   * A partire dal 31 gennaio, gli Starter IU sono obsoleti. I progetti esistenti creati da uno Starter IU possono essere utilizzati fino al 30 aprile 2017. Per ulteriori informazioni sulla procedura di migrazione e sulle date di rimozione, vedi il [post del blog relativo agli annunci di deprecazione ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/blogs/bluemix/2017/01/bluemix-mobile-dashboard-update/).
{: deprecated}
   * Puoi ora aggiornare il tipo di starter del progetto invece di eliminare il progetto e crearne uno nuovo.
   * Puoi ora creare il tuo progetto con uno starter codice [Watson Conversation](tutorial_conversation.html).
   * Laddove supportato, puoi ora generare un SDK per il tuo progetto.
   * Puoi ora aggiungere le tue istanze [Calcolo](sdk_compute.html) esistenti e generare SDK client da aggiungere al tuo progetto.


## Novità a partire da dicembre 2016
{: #dec-2016}

L'aggiornamento di dicembre 2016 del dashboard {{site.data.keyword.Bluemix_notm}} Mobile introduce le seguenti modifiche:

   * Puoi ora rimuovere un servizio connesso da un progetto in modo da poterlo eliminare o riutilizzare con un altro progetto. 
   * Puoi ora aggiungere un servizio esistente a un progetto.
   * Puoi ora creare o connettere un servizio CloudantNoSQL esistente come origine dati quando utilizzi uno Starter codice.
   * Laddove supportato, puoi ora creare o connettere un servizio Object Storage esistente come origine dati per il tuo progetto.
   * Puoi ora personalizzare il progetto di navigazione dell'applicazione che crei con uno Starter IU. 
   

## Novità a partire da novembre 2016
{: #nov-2016}

L'aggiornamento di novembre 2016 del dashboard {{site.data.keyword.Bluemix_notm}} Mobile introduce le seguenti modifiche:

   * Puoi ora generare le risorse SDK per i tuoi progetti dalla pagina **Codice**.
   * Cordova è ora supportato per lo starter codice di base.
   * Puoi ora [segnalare gli eventi di rete ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobileanalytics/sdk.html#network-requests){: new_window} e [monitorare le richieste di rete ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobileanalytics/app-monitoring.html#monitor-network-requests){: new_window} nella pagina **Richieste di rete** della console {{site.data.keyword.mobileanalytics_short}}.
   * Puoi ora [esportare i dati in dashDB ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobileanalytics/app-monitoring.html#dashdb){: new_window} nella console {{site.data.keyword.mobileanalytics_short}}.


## Novità a partire da ottobre 2016
{: #oct-2016}

L'aggiornamento di ottobre 2016 del dashboard {{site.data.keyword.Bluemix_notm}} Mobile introduce le seguenti modifiche:

   * Puoi ora aggiungere le funzionalità {{site.data.keyword.mobilepushshort}} e Analytics al tuo progetto direttamente dal dashboard.
   * Gli [Starter codice](starters.html#Code_Starter) sono ora disponibili.
   * Puoi aggiungere Authentication ai tuoi progetti creati da uno starter codice.
   * Swift è ora supportato.


### Analisi
{: #analytics notoc}

   * La modalità demo è abilitata per impostazione predefinita quando aggiungi la funzionalità Analytics. Puoi disattivare la modalità demo per visualizzare le analisi dopo l'esecuzione della tua applicazione.


### Builder IU
{: #ui_builder notoc}

   * È ora possibile accedere alla funzionalità **{{site.data.keyword.mobilepushshort}}** dal progetto.
   * La scheda **Impostazioni progetto** è stata ridenominata in **Impostazioni**.
   * La scheda **Autenticazione** è stata ridenominata in **Accesso utente**.


### Codice
{: #code notoc}

   * Il codice Objective-C e Swift generato per iOS utilizza ora CocoaPods per gestire le dipendenze. Questo significa che devi installare CocoaPods. Per installarlo, esegui `sudo gem install cocoapods`. Dopo aver installato CocoaPods, esegui `pod setup` per configurarlo se non è già configurato). Infine, esegui `pod install` per scaricare e installare le dipendenze del progetto necessarie prima di aprire il tuo file `.xcworkspace` in Xcode. Ulteriori dettagli sono disponibili nel file `README.md` nell'archivio del codice scaricato. Per ulteriori informazioni, vedi [Strumenti per sviluppatori prerequisiti](get_code.html#prereq-dev-tools).

Controlla frequentemente di essere al passo con i nuovi aggiornamenti.
