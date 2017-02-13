---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# Esercitazione end-to-end dello starter codice {{site.data.keyword.visualrecognitionshort}}
{: #tutorial_vr}

La seguente esercitazione end-to-end spiega i passi per creare un progetto da uno starter codice {{site.data.keyword.visualrecognitionshort}}, inclusi gli strumenti che devi avere installati e di conseguenza, i passi per eseguire lo starter in Xcode e Android Studio.


### Installazione degli strumenti per sviluppatori
{: #dev_tools}

Assicurati di aver installato gli [strumenti per sviluppatori prerequisiti ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](get_code.html#prereq-dev-tools "Icona link esterno"){: new_window}.


### Creazione di un progetto da uno starter codice {{site.data.keyword.visualrecognitionshort}}
{: #create_project}

1. rea un progetto dashboard Mobile in {{site.data.keyword.Bluemix}}.

   1. Dalla pagina **Introduzione** nel dashboard Mobile, fai clic su **Crea progetto**.

      In alternativa puoi fare clic su **Crea progetto** dalla pagina **Progetti**.

   2. Fai clic su **Starter codice**.

   3. Seleziona **Visual Recognition** e fai clic su **Crea progetto**.

   4. Immetti il nome del tuo progetto. Per questa esercitazione, utilizza `VisualRecognitionProject`.
   
   5. Fai clic su **Crea**.

2. Facoltativo: aggiungi la funzionalità {{site.data.keyword.mobilepushshort}}.

   1. Fai clic su **Aggiungi** per **{{site.data.keyword.mobilepushshort}}** nella pagina **Panoramica progetto**.

      In alternativa puoi fare clic su **Crea** dalla pagina **{{site.data.keyword.mobilepushshort}}**.

   2. Immetti il nome del tuo servizio e fai clic su **Crea**.

   3. Per iOS, [configura il servizio Apple Push Notification![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobilepush/t_push_provider_ios.html "Icona link esterno"){: new_window}.

   4. Per Android, [configura Firebase Cloud Messaging ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobilepush/t_push_provider_android.html "Icona link esterno"){: new_window}.
   
3. Facoltativo: aggiungi la funzionalità Analytics.

   1. Fai clic su **Aggiungi** per **Analytics** dalla pagina **Panoramica progetto**.

      In alternativa puoi fare clic su **Crea** dalla pagina **Analytics**.

   2. Immetti il nome del tuo servizio e fai clic su **Crea**.
   
   3. Disattiva la **Modalità demo** per visualizzare i tuoi dati di analisi dopo l'esecuzione della tua applicazione.
   
   4. Vedi [Introduzione a {{site.data.keyword.mobileanalytics_short}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobileanalytics/index.html "Icona link esterno"){: new_window} per ulteriori informazioni sulla configurazione di Analytics.
  
4. Facoltativo: aggiungi la funzionalità Authentication.

   1. Fai clic su **Aggiungi** per **Authentication** nella pagina **Panoramica progetto**.

      In alternativa puoi selezionare **Crea** nella pagina **Authentication Notifications**.

   2. Immetti il nome del tuo servizio e fai clic su **Crea**.
   
   3. Attiva **Authentication**.
   
   4. Seleziona il tuo provider di identità ed immetti le informazioni richieste per configurarlo. Puoi abilitare solo un provider di identità.

   5. Vedi [Introduzione a {{site.data.keyword.amashort}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobileaccess/index.html "Icona link esterno"){: new_window} per ulteriori informazioni sulla configurazione di Authentication.

5. Genera il tuo codice del progetto.

   1. Fai clic su **Richiama codice** nella pagina **Panoramica progetto** per selezionare la piattaforma e la lingua.
   
      In alternativa puoi fare clic sulla pagina **Codice**.
      
   2. Per iOS, fai clic su **iOS Swift**.
   
   3. Per Android, fai clic su **Android**.
   
   4. Quando il codice del progetto ha terminato la generazione, fai clic su **Scarica codice** per scaricare il tuo archivio del progetto.


### Esecuzione del tuo progetto in Xcode
{: #run_xcode}

1. Estrai il file `VisualRecognitionProject-Swift.zip`.

2. Apri il file `README.md` in un visualizzatore Markdown per rivedere i passi di configurazione del progetto.

   1. Crea la tua istanza del servizio [{{site.data.keyword.visualrecognitionshort}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://console.{DomainName}/catalog/services/visual-recognition/ "Icona link esterno"){: new_window}.
   
   2. Apri il tuo terminale e passa alla tua cartella del progetto.
   
      1. Esegui `pod setup` se hai bisogno di configurare il repository CocoaPods.
      
      2. Esegui `pod update` se hai bisogno di aggiornare i tuoi pod esistenti.
      
      3. Esegui `pod install` per installare i pod obbligatori per il tuo progetto.
      
      4. Esegui `carthage update --platform iOS` per creare le dipendenze e i framework da utilizzare con l'SDK {{site.data.keyword.ibmwatson}} Developer Cloud iOS.
      
   3. Apri il tuo spazio di lavoro `VisualRecognitionProject.xcworkspace` Xcode.
   
   4. Aggiungi le tue credenziali del servizio {{site.data.keyword.visualrecognitionshort}}.
   
      1. Copia la tua `api_key` dalle tue credenziali del servizio {{site.data.keyword.visualrecognition}}.
      
      2. Incolla la tua `api_key` nella chiave `VisualRecognitionAPIKey` nel file `WatsonCredentials.plist`.
      
3. Esegui la tua applicazione.


### Esecuzione del tuo progetto in Android Studio
{: #run_studio}

1. Estrai il file `VisualRecognitionProject-Android.zip`.

2. Apri il file `README.md` in un visualizzatore Markdown per configurare il tuo progetto.

   1. Crea la tua istanza del servizio [{{site.data.keyword.visualrecognitionshort}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://console.{DomainName}/catalog/services/visual-recognition/ "Icona link esterno"){: new_window}.
   
      Salta questo passo se hai già un'istanza del servizio {{site.data.keyword.visualrecognitionshort}}.
   
   2. Apri il tuo progetto `VisualRecognitionProject-Android` in Android Studio.
   
   4. Aggiungi le tue credenziali del servizio {{site.data.keyword.visualrecognitionshort}}.
   
      1. Copia la tua `api_key` dalle tue credenziali del servizio {{site.data.keyword.visualrecognitionshort}}.
      
      2. Incolla la tua `api_key` nella chiave `watson_visual_recognition_api_key` nel file `res/values/watson_credentials.xml`.
      
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
* [Esercitazione - Cloudant Sync](tutorial_cloudant_synd.html)
* [Esercitazione - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Esercitazione - Linguaggio Watson](tutorial_watson_language.html)
* [Esercitazione - Weather ](tutorial_weather.html)

