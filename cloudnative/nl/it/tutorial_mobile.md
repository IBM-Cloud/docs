---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Esercitazione end-to-end dello starter di base mobile
{: #tutorial}

La seguente esercitazione end-to-end ti guida attraverso i passaggi per creare un progetto dallo starter di base mobile. Questa include l'installazione degli strumenti prerequisiti e la procedura per eseguire il progetto in Xcode e Android Studio.

Puoi creare un progetto utilizzando la [{{site.data.keyword.dev_console}}](#create-devex) basata su web o la [{{site.data.keyword.dev_cli_notm}}](#create-cli) controllata dai comandi.

## Installazione degli strumenti per sviluppatori
{: #dev_tools}

Assicurati di installare gli [strumenti per sviluppatori prerequisiti ![icona link esterno](../icons/launch-glyph.svg "External link icon")](get_code.html#prereq-dev-tools){: new_window}.


## Creazione di un progetto utilizzando la {{site.data.keyword.dev_console}}
{: #create-devex}

1. Crea un progetto {{site.data.keyword.dev_console}} in {{site.data.keyword.Bluemix}}.

   1. Dalla pagina [**Introduzione** ![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/developer/getting-started/) della {{site.data.keyword.dev_console}}, fai clic su **Crea progetto**.

      In alternativa puoi fare clic su **Crea progetto** dalla pagina **Progetti**.

   2. Seleziona **Applicazione mobile** e fai clic su **Avanti**.

   3. Seleziona **Di base** e fai clic su **Avanti**.

   4. Immetti il nome del tuo progetto. Per questa esercitazione, utilizza `MobileBasicProject`.

   5. Seleziona la tua piattaforma. Per questa esercitazione, utilizza `Swift`.
   
   6. Fai clic su **Crea**.

2. Facoltativo: aggiungi la funzionalità Authentication.

   1. Fai clic su **Aggiungi** per **Authentication** nella pagina **Panoramica progetto**.

      In alternativa, puoi fare selezionare **Crea** o **Aggiungi esistente** nella pagina **Funzionalità > Authentication**.

   2. Immetti il nome del tuo servizio e fai clic su **Crea**.
   
   3. Attiva **Authentication**.
   
   4. Seleziona il tuo provider di identità ed immetti le informazioni per configurarlo. Puoi abilitare solo un provider di identità.
   
   5. Consulta [Configurazione dei provider di identità} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/appid/identity-providers.html){: new_window} per ulteriori informazioni sulla configurazione di Authentication.

3. Facoltativo: aggiungi la funzionalità Analytics.

   1. Fai clic su **Aggiungi** per **Analytics** dalla pagina **Panoramica progetto**.

      In alternativa, puoi fare clic su **Crea** o **Aggiungi esistente** dalla pagina **Funzionalità > Analytics**.

   2. Immetti il nome del tuo servizio e fai clic su **Crea**.
   
   3. Disattiva la **Modalità demo** per visualizzare i tuoi dati di analisi dopo l'esecuzione della tua applicazione.
   
   4. Vedi [Introduzione a {{site.data.keyword.mobileanalytics_short}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobileanalytics/index.html){: new_window} per ulteriori informazioni sulla configurazione di Analytics.

4. Facoltativo: aggiungi la funzionalità {{site.data.keyword.mobilepushshort}}.

   1. Fai clic su **Aggiungi** per **{{site.data.keyword.mobilepushshort}}** nella pagina **Panoramica progetto**.

      In alternativa, puoi fare clic su **Crea** o **Aggiungi esistente** dalla pagina **Funzionalità > {{site.data.keyword.mobilepushshort}}**.

   2. Immetti il nome del tuo servizio e fai clic su **Crea**.

   3. Per iOS, [configura il servizio Apple Push Notification ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. Per Android, [configura Firebase Cloud Messaging ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobilepush/t_push_provider_android.html){: new_window}.

5. Facoltativo: aggiungi la funzionalità Data.

   1. Fai clic su **Visualizza** per **Data** nella pagina **Panoramica progetto**.

      In alternativa puoi selezionare **Crea** nella pagina **Data**.
      
   2. Scegli **{{site.data.keyword.cloudant_short_notm}}** o **{{site.data.keyword.objectstorageshort}}**.

   3. Immetti il nome del tuo servizio e fai clic su **Crea**.

   4. Vedi [Introduzione a {{site.data.keyword.cloudant_short_notm}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/Cloudant/index.html){: new_window} per ulteriori informazioni sulla configurazione di {{site.data.keyword.cloudant_short_notm}}.

   5. Vedi [Introduzione a {{site.data.keyword.objectstorageshort}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/ObjectStorage/index.html){: new_window} per ulteriori informazioni sulla configurazione di {{site.data.keyword.objectstorageshort}}.

6. Genera il tuo codice del progetto:

   1. Fai clic su **Richiama codice** nella pagina **Panoramica progetto** per selezionare il tuo linguaggio.
   
      In alternativa puoi fare clic sulla pagina **Codice**.
      
   2. Fai clic su **Genera Swift**.
   
   3. Quando il codice del progetto ha terminato la generazione, fai clic su **Scarica Swift** per scaricare il tuo archivio del progetto.

7. Inizia a lavorare con il tuo progetto scaricato:

	1. Espandi il file archiviato.
	
	2. Passa alla nuova directory del progetto.
	
	3. Utilizza la {{site.data.keyword.dev_cli_notm}} per continuare.

8. Facoltativo: [Aggiorna il tuo progetto](project_overview_page.html#update_language) per generare un nuovo linguaggio.


## Creazione di un progetto utilizzando la {{site.data.keyword.dev_cli_notm}}
{: #create-cli}

1. Assicurati di installare la [{{site.data.keyword.dev_cli_short}}](dev_cli.html).

2. Nella tua finestra del terminale, passa a una directory locale di tua scelta ed esegui il seguente comando.

	```
	bx dev create
	```
	{: codeblock}
	
3. Fornisci i seguenti valori quando richiesto:

	* Seleziona un modello: 2 (per mobile)
	* Seleziona uno starter: 1 (di base)
	* Seleziona una piattaforma: 3 (per iOS Swift)
	* Immetti un nome per il tuo progetto: `MobileBasicProjectCLI`

4. Se desideri aggiungere servizi al tuo progetto, immetti `y` quando ti viene domandato e rispondi alle rimanenti domande.

5. Dopo aver salvato `MobileBasicProjectCLI`, passa alla cartella `MobileBasicProjectCLI/MobileBasicProjectCLI-Swift`.


## Esecuzione del tuo progetto Swift in Xcode
{: #run_swift}

1. Estrai il file `MobileBasicProject-Swift.zip`.

2. Apri il file `README.md` in un visualizzatore Markdown per rivedere i passi di configurazione del progetto.

   1. Apri il tuo terminale e passa alla tua cartella del progetto.
   
      1. Esegui `pod setup` se hai bisogno di configurare il repository CocoaPods.
      
      2. Esegui `pod update` se hai bisogno di aggiornare i tuoi pod esistenti.
      
      3. Esegui `pod install` per installare i pod obbligatori per il tuo progetto.
      
   3. Apri il tuo spazio di lavoro `BasicProject.xcworkspace` Xcode.
      
3. Esegui la tua applicazione.


## Esecuzione del tuo progetto Cordova in Xcode
{: #run_cordova_xcode}

1. Estrai il file `MobileBasicProject-Cordova.zip`.

2. Apri il file `README.md` in un visualizzatore Markdown per configurare il tuo progetto.

   1. Apri il tuo progetto `platforms/ios` in Xcode.
      
3. Esegui la tua applicazione.


## Esecuzione del tuo progetto Cordova in Android Studio
{: #run_cordova_studio}

1. Estrai il file `BasicProject-Cordova.zip`.

2. Apri il file `README.md` in un visualizzatore Markdown per configurare il tuo progetto.

   1. Apri il tuo progetto `platforms/android` in Android Studio.
      
3. Esegui la tua applicazione.


## Esecuzione del tuo progetto Android in Android Studio
{: #run_android}

1. Estrai il file `MobileBasicProject-Android.zip`.

2. Apri il file `README.md` in un visualizzatore Markdown per configurare il tuo progetto.

   1. Apri il tuo progetto `BasicProject-Android` in Android Studio.
      
3. Esegui la tua applicazione.
