---

copyright:
  years: 2016, 2017
lastupdated: "2016-12-15"

---
{:new_window: target="_blank"}

# Esercitazione - Starter IU catalogo negozio
{: #tutorial_store_catalog}

Il starter IU catalogo negozio {{site.data.keyword.Bluemix}} fornisce una struttura dell'applicazione di vendite di base che puoi personalizzare e ti fornisce i punti di integrazione per ogni servizio {{site.data.keyword.Bluemix_notm}} Mobile.


## Requisiti
{: #tutorial_requirements}

* Un account [Bluemix ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](http://bluemix.net "Icona link esterno")


## Introduzione
{: #tutorial_gs}

Per essere velocemente operativo con lo starter IU catalogo negozio, segui la seguente procedura:

1. rea un progetto dashboard Mobile in {{site.data.keyword.Bluemix_notm}}.

   1. Dalla pagina **Introduzione** nel dashboard Mobile, fai clic su **Crea progetto**.

      In alternativa puoi fare clic su **Crea progetto** nella pagina **Progetti**.

   2. Seleziona **Starter IU**, se non è già selezionato.

   3. Seleziona **Catalogo negozio** e fai clic su **Crea progetto**.

   4. Immetti il nome del tuo progetto e fai clic su **Crea**.

2. Facoltativo: aggiungi la funzionalità {{site.data.keyword.mobilepushshort}}.

   1. Fai clic su **Aggiungi** per **{{site.data.keyword.mobilepushshort}}** nella pagina **Panoramica progetto**.

      In alternativa puoi fare clic su **Crea** nella pagina **{{site.data.keyword.mobilepushshort}}**.

   2. Immetti il nome del tuo servizio e fai clic su **Crea**.

   3. Per iOS, [configura il servizio Apple Push Notification![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobilepush/t_push_provider_ios.html "Icona link esterno"){: new_window}.

   4. Per Android, [configura Google Cloud Messaging ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobilepush/t_push_provider_android.html "Icona link esterno"){: new_window}.

3. Facoltativo: aggiungi altre funzionalità.

   1. Fai clic su **Aggiungi** per la funzionalità nella pagina **Panoramica progetto**.

   2. Immetti il nome del tuo servizio e fai clic su **Crea**.

   3. Segui le istruzioni fornite con il servizio per configurarlo.

4. Progetta la tua applicazione.

   1. Seleziona **Builder IU** nel menu di navigazione per personalizzare la progettazione della tua applicazione.
   
		**Suggerimento:** per visualizzare una veloce panoramica del builder IU, seleziona **Mostrami come funziona** nella navigazione dopo aver selezionato il builder IU.

   2. Seleziona la scheda **Progettazione** nella navigazione.

      È presente uno spazio di lavoro per la progettazione e una vista simulata dell'aspetto della tua applicazione.

   3. Facoltativamente aggiungi nuove schermate selezionando **Crea schermata**. Denomina una nuova schermata per rendere più facile il riferimento alla tua applicazione. Le nuove schermate vengono create allo stesso livello della schermata principale, indipendentemente da ciò che è selezionato nell'albero. Puoi anche selezionarla dai seguenti tipi di schermata:
      * Menu
      * Elenco
      * Associazione
      * Personalizzata
      * Grafico	   

   4. Puoi modificare il titolo del menu della tua applicazione selezionando la casella di testo *Menu* nella sezione **Layout** della tua interfaccia e sostituendo il contenuto nel campo **Dati da visualizzare**. Visualizza i tuoi aggiornamenti nella sezione del dispositivo simulato.

      Aggiorna gli elementi di progettazione selezionando ognuno di essi e aggiornando le informazioni, se necessario. Questi elementi vengono visualizzati in un formato ad albero. Puoi modificare l'ordine o l'ubicazione degli elementi del menu trascinando un elemento in una nuova ubicazione. Tutti gli elementi secondari di un elemento vengono invece spostati con l'elemento principale. Le informazioni testuali nei tre elementi visualizzate nei campi **Dati da visualizzare** fanno riferimento al contenuto nel foglio di calcolo dell'origine dati. *Non modificare questi elementi nella vista **Progettazione** perché vengono sovrascritti dal contenuto nelle origini dati identificate nella vista **Dati**.*

		Un elemento che viene identificato nell'albero come un *Modulo* è indipendente e può essere modificato inline. Non dispone di informazioni di riferimento da un'origine dati.

   5. Seleziona **Dati** nella navigazione per visualizzare i dati che vengono utilizzati dall'applicazione. Nel template sono disponibili informazioni predefinite; tuttavia, puoi modificare l'origine dei dati selezionando **Crea nuovo**. Puoi fare riferimento a più di una origine dati, in modo da fornire un nome per ogni origine che vuoi utilizzare. Puoi anche selezionarla dalla seguenti opzioni di origine dati
      * Cloud
      * Locale
      * Cloudant
      * Google Sheet
      * Excel Online
      * Google Drive

      Puoi anche importare, esportare o modificare il contenuto presente nella tabella, se in locale, utilizzando i pulsanti e selezionando il contenuto nella tabella.

	  Nota: se importi dati che non corrispondono alla struttura dei dati predefiniti, attiva lo slider *Sostituisci schema*. Un esempio di questo è un file .csv con meno colonne rispetto ai dati forniti con il tuo starter.
	  
   6. Seleziona **Navigazione** per personalizzare le azioni di navigazione nella tua applicazione. Questa opzione è facoltativa perché per molte schermate le azioni di navigazione vengono create automaticamente in base alle relazioni delle schermate. Puoi modificare la schermata di destinazione selezionando la schermata o il campo *da* cui vuoi navigare nell'elenco delle voci di menu. Seleziona quindi la schermata *verso* cui vuoi navigare nel campo della schermata di destinazione.  

   7. Seleziona **Accesso utente** nella navigazione per modificare i requisiti di accesso al tuo progetto. Puoi attivare/disattivare l'accesso utente con lo switch. Quando l'accesso utente è attivo, puoi impostare il timeout utente di inattività e le credenziali degli utenti che possono accedere all'applicazione.

   8. Seleziona **Impostazioni** nel menu di navigazione per modificare le informazioni generali e i colori per il tuo progetto. Questa schermata è dove immetti la chiave API Google, se necessaria per i servizi che hai aggiunto al tuo progetto. Questa schermata è inoltre dove aggiungi il tuo identificativo bundle univoco registrato con l'Apple Store o il Google Play Store.

      Se desideri aggiungere l'SDK IBM MobileFirst Foundation al tuo progetto, attiva lo switch.

   9. Se hai attivato lo switch per aggiungere IBM MobileFirst Platform Foundation al tuo progetto nella schermata *Impostazioni*, viene visualizzata una selezione **Foundation** nella navigazione. Seleziona **Foundation** e completa le informazioni necessarie specifiche per IBM MobileFirst Platform Foundation.

   10. Seleziona **Pubblica** nel menu di navigazione per immettere le informazioni finali necessarie per creare la tua applicazione mobile. Puoi immettere il tuo identificativo Bundle per iOS e l'identificativo Applicazione per Android.

       Se stai creando un'applicazione iOS, devi ottenere il tuo identificativo bundle, il tuo certificato di distribuzione come ad esempio un file *.p12* e il tuo profilo di provisioning come un file *.mobileprovision* dal portale di provisioning di Apple. Possono essere creati contemporaneamente e con lo stesso computer che utilizzerai quando invierai la tua applicazione all'Apple store. Il certificato di distribuzione e il profilo di provisioning devono basarsi sull'identificativo bundle. 	

5. Scarica il tuo progetto.

   1. Fai clic su **Codice** e seleziona il tuo linguaggio di programmazione o la tua piattaforma preferiti.

   2. Per Android, puoi scegliere tra le seguenti opzioni dopo aver generato il codice:

      * Scarica il codice

      * Scarica APK

      * Scarica con codice QR

   3. Per iOS, puoi scegliere la seguente opzione dopo aver generato il codice:

      * Scarica il codice

6. Esegui la tua applicazione sul tuo dispositivo o simulatore.


## Operazioni successive
{: #tutorial_next}

[Provatela! ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](http://console.{DomainName}/mobile/create-project?starter=fb5e31a9-1186-4d46-939e-2f620f35b83b "Icona link esterno"){: new_window}


### Esercitazioni starter IU
{: #tutorials_UI}

* [Esercitazione - Catalogo negozio](tutorial_store_catalog.html)


### Esercitazioni starter codice
{: #tutorials_Code}

* [Esercitazione - Di base](tutorial.html)
* [Esercitazione - Cloudant Sync](tutorial_cloudant_synd.html)
* [Esercitazione - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Esercitazione - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Esercitazione - Linguaggio Watson](tutorial_watson_language.html)
* [Esercitazione - Weather ](tutorial_weather.html)

