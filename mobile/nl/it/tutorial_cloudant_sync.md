---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Esercitazione end-to-end dello starter codice Cloudant Sync
{: #tutorial}

La seguente esercitazione end-to-end spiega i passi per creare un progetto da uno starter codice Cloudant Sync, inclusi gli strumenti che devi avere installato e, successivamente, i passi per eseguire lo starter in Android Studio.


### Installazione degli strumenti per sviluppatori
{: #dev_tools}

Assicurati di aver installato gli [strumenti per sviluppatori prerequisiti ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](get_code.html#prereq-dev-tools "Icona link esterno"){: new_window}.


### Creazione di un progetto dallo starter codice Cloudant Sync
{: #create_project}

1. rea un progetto dashboard Mobile in {{site.data.keyword.Bluemix}}.

   1. Dalla pagina **Introduzione** nel dashboard Mobile, fai clic su **Crea progetto**.

      In alternativa puoi fare clic su **Crea progetto** dalla pagina **Progetti**.

   2. Fai clic su **Starter codice**.

   3. Seleziona **Cloudant Sync** e fai clic su **Crea progetto**.

   4. Immetti il nome del tuo progetto. Per questa esercitazione, utilizza `CloudantSyncProject`.
   
   5. Fai clic su **Crea**.

2. Aggiungi la funzionalità Data. Puoi creare una nuova istanza del servizio {{site.data.keyword.cloudant}} o aggiungerne una esistente.

   1. Fai clic su **Visualizza** sul tile **Data** nella pagina **Panoramica progetto**.

      In alternativa, puoi fare clic su **Crea** o **Aggiungi esistente** e quindi su **Cloudant NoSQL DB** nella pagina **Data**.
      
   2. Facoltativo: se hai scelto di creare una nuova istanza, immetti il nome del servizio e fai clic su **Crea**.

   3. Facoltativo: se hai scelto di aggiungere un'istanza del servizio esistente, seleziona la tua istanza dall'elenco e fai clic su **Aggiungi esistente**.

   4. Fai clic sull'icona **Menu** nel tile del servizio e seleziona **Avvia...** per avviare la tua istanza del servizio.

      1. Fai clic su **AVVIA** per avviare la tua console {{site.data.keyword.cloudant}}.

      2. Fai clic su **Crea database**, immetti il nome del database e fai clic su **Crea**.

      3. Fai clic sull'icona **+** accanto a **Tutti i documenti** per aggiungere i documenti.

3. Facoltativo: aggiungi la funzionalità {{site.data.keyword.mobilepushshort}}.

   1. Fai clic su **Aggiungi** per **{{site.data.keyword.mobilepushshort}}** nella pagina **Panoramica progetto**.

      In alternativa puoi fare clic su **Crea** dalla pagina **{{site.data.keyword.mobilepushshort}}**.

   2. Immetti il nome del tuo servizio e fai clic su **Crea**.

   3. Per Android, [configura Firebase Cloud Messaging ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobilepush/t_push_provider_android.html "Icona link esterno"){: new_window}.
   
4. Facoltativo: aggiungi la funzionalità Analytics.

   1. Fai clic su **Aggiungi** per **Analytics** dalla pagina **Panoramica progetto**.

      In alternativa puoi fare clic su **Crea** dalla pagina **Analytics**.

   2. Immetti il nome del tuo servizio e fai clic su **Crea**.
   
   3. Disattiva la **Modalità demo** per visualizzare i tuoi dati di analisi dopo l'esecuzione della tua applicazione.
   
   4. Vedi [Introduzione a {{site.data.keyword.mobileanalytics_short}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobileanalytics/index.html "Icona link esterno"){: new_window} per ulteriori informazioni sulla configurazione di Analytics.
  
5. Facoltativo: aggiungi la funzionalità Authentication.

   1. Fai clic su **Aggiungi** per **Authentication** nella pagina **Panoramica progetto**.

      In alternativa puoi selezionare **Crea** nella pagina **Authentication Notifications**.

   2. Immetti il nome del tuo servizio e fai clic su **Crea**.
   
   3. Attiva **Authentication**.
   
   4. Seleziona il tuo provider di identità ed immetti le informazioni richieste per configurarlo. Puoi abilitare solo un provider di identità.

   5. Vedi [Introduzione a {{site.data.keyword.amashort}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobileaccess/index.html "Icona link esterno"){: new_window} per ulteriori informazioni sulla configurazione di Authentication.

6. Genera il tuo codice del progetto.

   1. Fai clic su **Richiama codice** nella pagina **Panoramica progetto** per selezionare la piattaforma e la lingua.
   
      In alternativa puoi fare clic sulla pagina **Codice**.
      
   2. Per Android, fai clic su **Android**.
   
   3. Quando il codice del progetto ha terminato la generazione, fai clic su **Scarica codice** per scaricare il tuo archivio del progetto.


### Esecuzione del tuo progetto Android in Android Studio
{: #run_android}

1. Estrai il file `CloudantSyncProject-Android.zip`.

2. Apri il file `README.md` in un visualizzatore Markdown per configurare il tuo progetto.

   1. Apri il tuo progetto `CloudantSyncProject-Android` in Android Studio.

   2. Aggiungi le tue credenziali Cloudant.

      1. Dalla pagina **Data**, fai clic sull'icona **Menu** nel tile del servizio e seleziona **Avvia...** per avviare la tua istanza del servizio.

         1. Fai clic su **AVVIA** per avviare la tua console {{site.data.keyword.cloudant}}.

         2. Fai clic sul nome del tuo database e seleziona **Autorizzazioni**.

         3. Immetti il nome del tuo database nella stringa `cloudant_dbname` all'interno del file `res/values/cloudant_credentials.xml`.

         4. Fai clic su **Genera chiave API**.

             1. Copia il valore della **Chiave** e incollalo nella stringa `cloudant_api_key` nel file `res/values/cloudant_credentials.xml`.

             2. Copia il valore della **Password** e incollalo nella stringa `cloudant_api_password` nel file `res/values/cloudant_credentials.xml`.

             3. Seleziona l'autorizzazione **_admin**.
      
3. Esegui la tua applicazione.


## Operazioni successive
{: #what_next}

Visualizza altre esercitazioni.


### Esercitazioni starter IU
{: #tutorials_UI}

* [Esercitazione - Catalogo negozio](tutorial_store_catalog.html)


### Esercitazioni starter codice
{: #tutorials_Code}

* [Esercitazione - Di base](tutorial.html)
* [Esercitazione - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Esercitazione - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Esercitazione - Linguaggio Watson](tutorial_watson_language.html)
* [Esercitazione - Weather ](tutorial_weather.html)
