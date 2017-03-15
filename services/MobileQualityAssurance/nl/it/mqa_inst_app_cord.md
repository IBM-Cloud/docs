---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Strumentazione di MQA con un'applicazione Cordova (Obsoleto)
{: #instrumentcord}

Per utilizzare {{site.data.keyword.mqafull}} con la tua applicazione Cordova, devi scaricare l'SDK e strumentarla effettuando alcune modifiche utilizzando l'interfaccia riga di comando (CLI).
{: shortdesc}

Prima di poter strumentare un'applicazione con {{site.data.keyword.mqa}}, devi avere un account {{site.data.keyword.Bluemix}} e aver correttamente installato la versione dell'ambiente di sviluppo per le piattaforme dell'applicazione che stai strumentando. 

Per strumentare {{site.data.keyword.mqa}} in modo che utilizzi la tua applicazione Cordova, completa la seguente procedura:

1. Aggiungi le autorizzazioni necessarie e la SDK scaricata al tuo progetto Cordova.

	1. Apri un finestra dei comandi e passa alla directory che contiene i tuoi file del progetto.

	2. Aggiungi il plugin {{site.data.keyword.mqa}} al tuo progetto Cordova completando la seguente procedura, in base al tuo ambiente:

		**Importante**: se stai utilizzando Xcode 7.x su iOS 9, devi configurare l'impostazione Enable Bitcode su No in Xcode Build Settings. Puoi modificare questa impostazione aprendo Xcode utilizzando il file del progetto Cordova .xcodeproj, ubicato nella cartella platform\iPhone.

		* IBM MobileFirst™ Platform Foundation versione 7.1:

			1. Immetti il seguente comando per installare il plugin {{site.data.keyword.mqa}}:

				```
				mfp cordova plugin add plugin_location
				```
				{: codeblock}

			Dove *plugin_location* è il percorso della directory del plugin {{site.data.keyword.mqa}} estratto che hai scaricato.

			2. Se la tua applicazione è in esecuzione su Android, ridenomina il file `project_name/app_name/platforms/android/custom_rules.xml` in `custom_rules.xml.bak`.

		* Apache Cordova precedente alla versione 4.0:
			1. Immetti il seguente comando per installare il plugin {{site.data.keyword.mqa}}:

				```
				cordova plugin add plugin_location
				```
				{: codeblock}

			Dove *plugin_location* è il percorso della directory del plugin {{site.data.keyword.mqa}} estratto che hai scaricato.

			2. Immetti il seguente comando per aggiungere un ulteriore plugin obbligatorio:

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

			3. Se la tua applicazione è in esecuzione su Android, ridenomina il file `project_name/app_name/platforms/android/custom_rules.xml` in `custom_rules_bak.xml`.

		* Apache Cordova versione 4.0 o successiva:

			1. Inserire il seguente comando:

				```
				cordova plugin add plugin_location
				```
				{: codeblock}

			Dove *plugin_location* è il percorso della directory del plugin {{site.data.keyword.mqa}} estratto che hai scaricato.

			2. Immetti il seguente comando per aggiungere un ulteriore plugin obbligatorio:

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

2. Avvia una nuova sessione di {{site.data.keyword.mqa}} per ogni accesso.

	1. Apri il file `index.js` ubicato nella seguente directory: `your_project_name\www\js`.

	2. Aggiungi i seguenti parametri e la funzione nella funzione `onDeviceReady()` nel file `index.js`. Posiziona la funzione prima della parentesi di chiusura della funzione.

	Restrizione: per un'applicazione già strumentata per Mobile Quality Assurance utilizzando una vecchia versione del plugin in modo che Cordova utilizzi le funzioni incluse nel plugin Mobile Quality Assurance per Cordova versione 3.0.18 e successive, devi ricreare e sostituire la tua chiave dell'applicazione. Per ulteriori informazioni su come ricreare la tua chiave dell'applicazione, consulta le impostazioni di gestione dell'applicazione. Le chiavi dell'applicazione generate prima di febbraio 2016 continuano a funzionare con il vecchio plugin, ma non non funzioneranno più dopo l'aggiornamento del tuo plugin alla versione 3.0.08 o successiva.

		```
		MQA.startNewSession(
			{
				mode: "QA",
				// o modalità: "MARKET" per la modalità di produzione.
			android: {
				appKey: "your_MQA_Android_appKey" ,
				notificationsEnabled: true},
			ios: {
				appKey: "your_MQA_iOS_appKey" ,
				screenShotsFromGallery: true,}
			},
			{
			success: function () {console.log("Session
			   Started successfully");},
			error: function (string) { console.log("Session
			   error" + string);}
			}
			);
		```
		{: codeblock}

	3. Continua con la procedura in [Introduzione a {{site.data.keyword.mqa}}](index.html).



# Link correlati
{: #rellinks notoc}

## Link correlati
{: #general notoc}
* [Introduzione a {{site.data.keyword.mqa}}](index.html){:new_window}
