---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# Novità nel dashboard Mobile
{: #what_is_new}

### Novità a partire da dicembre 2016
{: #dec-2016}

L'aggiornamento di dicembre 2016 del dashboard {{site.data.keyword.Bluemix}} Mobile introduce le seguenti modifiche:

   * Puoi rimuovere un servizio connesso da un progetto in modo da poter essere eliminato o riutilizzato con un altro progetto. 
   * Puoi aggiungere un servizio esistente a un progetto.
   * Puoi creare o connettere un servizio CloudantNoSQL esistente come origine dati quando utilizzi uno starter codice.
   * Laddove supportato, puoi creare o connettere un servizio Object Storage esistente come origine dati per il tuo progetto.
   * Puoi personalizzare il progetto di navigazione dell'applicazione che crei con uno starter IU. 
   

### Novità a partire da novembre 2016
{: #nov-2016}

L'aggiornamento di novembre 2016 del dashboard {{site.data.keyword.Bluemix}} Mobile introduce le seguenti modifiche:

   * Puoi ora generare le risorse SDK per i tuoi progetti dalla pagina **Codice**.
   * Cordova è ora supportato per lo starter codice di base.
   * Puoi ora [segnalare gli eventi di rete ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobileanalytics/sdk.html#network-requests "Icona link esterno"){: new_window} e [monitorare le richieste di rete ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobileanalytics/app-monitoring.html#monitor-network-requests "Icona link esterno"){: new_window} nella pagina **Richieste di rete** della console {{site.data.keyword.mobileanalytics_short}}.
   * Puoi ora [esportare i dati in dashDB ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobileanalytics/app-monitoring.html#dashdb "Icona link esterno"){: new_window} nella console {{site.data.keyword.mobileanalytics_short}}.


### Novità a partire da ottobre 2016
{: #oct-2016}

L'aggiornamento di ottobre 2016 del dashboard {{site.data.keyword.Bluemix_notm}} Mobile introduce le seguenti modifiche:

   * Puoi ora aggiungere le funzionalità {{site.data.keyword.mobilepushshort}} e Analytics al tuo progetto direttamente dal dashboard.
   * Gli [Starter codice](starters.html#Code_Starter) sono ora disponibili.
   * Puoi aggiungere Authentication ai tuoi progetti creati da uno starter codice.
   * Swift è ora supportato.


#### Analisi
{: #analytics}

   * La modalità demo è abilitata per impostazione predefinita quando aggiungi la funzionalità Analytics. Puoi disattivare la modalità demo per visualizzare le analisi dopo l'esecuzione della tua applicazione.


#### Builder IU
{: #ui_builder}

   * È ora possibile accedere alla funzionalità **{{site.data.keyword.mobilepushshort}}** dal progetto.
   * La scheda **Impostazioni progetto** è stata ridenominata in **Impostazioni**.
   * La scheda **Autenticazione** è stata ridenominata in **Accesso utente**.


#### Codice
{: #code}

   * Il codice Objective-C e Swift generato per iOS utilizza ora CocoaPods per gestire le dipendenze. Questo significa che devi installare CocoaPods. Per installarlo, esegui `sudo gem install cocoapods`. Dopo aver installato CocoaPods, esegui `pod setup` per configurarlo se non è già configurato). Infine, esegui `pod install` per scaricare e installare le dipendenze del progetto necessarie prima di aprire il tuo file `.xcworkspace` in Xcode. Ulteriori dettagli sono disponibili nel file `README.md` nell'archivio del codice scaricato. Per ulteriori informazioni, vedi [Strumenti per sviluppatori prerequisiti](get_code.html#prereq-dev-tools).

Controlla frequentemente di essere al passo con i nuovi aggiornamenti.
