---

copyright:
  years: 2015, 2016

---
<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Introduzione all'esempio HelloWorld
{: #gettingstarted-cordova}
*Ultimo aggiornamento: 17 marzo 2016*

Se desideri iniziare a lavorare con una nuova applicazione Cordova, puoi utilizzare l'applicazione HelloWorld. Questa applicazione illustra come connettere il tuo backend mobile su {{site.data.keyword.Bluemix}} da un'applicazione mobile senza autenticazione. Nell'applicazione è già installato l'SDK. Quando sei pronto, puoi ottenere le specifiche librerie
    che desideri utilizzare nella tua applicazione.

1. Crea il tuo backend mobile in {{site.data.keyword.Bluemix_notm}}.

	1. Nella sezione Contenitori tipo del catalogo {{site.data.keyword.Bluemix_notm}}, fai clic su MobileFirst Services Starter.
	1. Immetti un nome e un host per la tua applicazione e fai clic su **Crea**.
	1. Fai clic su **Fine**.

2. Ottieni il progetto da GitHub. Puoi utilizzare il comando git clone per ottenere il progetto. Dal tuo computer, apri il terminale e immetti quindi il seguente comando:

	```Bash
	git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld
	```

3. Esegui i seguenti comandi dalla directory del tuo progetto per aggiungere gli ambienti di piattaforma Android e iOS:

	### Android

	```Bash
	cordova platform add android
	```

	### iOS

	```Bash
	cordova platform add ios
	```

4. Aggiungi il plugin Cordova con il seguente comando:

	```Bash
	cordova plugin add ibm-mfp-core
	```

5. Configura l'esempio HelloWorld.

	* Passa alla directory dove hai clonato il progetto.
	* Apri il file *&lt;directory_della_tua_applicazione&gt;*/www/js/index.js e sostituisci *&lt;ROTTA_APPLICAZIONE&gt;* e *&lt;ID_APPLICAZIONE&gt;* con i tuoi valori di ID applicazione e rotta Bluemix.

		**Nota:** assicurati che la tua rotta stia utilizzando la protezione del protocollo https.

		```Javascript
		// Bluemix credentials
		route: "<ROTTA_APPLICAZIONE>",
		GUID: "<GUID_APPLICAZIONE>",
		```

6. Configura la tua applicazione Cordova per iOS. La piattaforma Android non richiede ulteriori configurazioni.

	### iOS
  Per evitare errori durante la generazione, configura il tuo progetto Xcode nel seguente modo.

	1. Utilizza la versione più recente di Xcode per aprire il tuo file `xcode.proj` nella directory *&lt;nome_applicazione&gt;*/platforms/ios.

		**Importante:** se ricevi un messaggio che ti invita ad eseguire la conversione alla sintassi Swift più recente ("Convert to Latest Swift Syntax"), fai clic su **Cancel**.

	2. Vai a **Build Settings > Swift Compiler - Code Generation > Objective-C Bridging Header** e aggiungi il seguente percorso:

		```
		<il_nome_del_tuo_progetto>/Plugins/ibm-mfp-core/Bridging-Header.h
		```

	3. Vai a **Build settings > Linking > Runpath Search Paths** e aggiungi il seguente parametro Frameworks:

		```
		@executable_path/Frameworks
		```

7. Genera ed esegui l'esempio sul tuo emulatore o sul tuo dispositivo mobile.

  ### Android
	1. Genera l'applicazione Cordova utilizzando il seguente comando:

    **Importante:** Prima di aprire il tuo progetto in Android Studio, devi prima generare la tua applicazione Cordova tramite l'interfaccia riga di comando (CLI) Cordova. Altrimenti, riscontrerai degli errori di generazione.

	```Bash
	cordova build android
	```

	2. Esegui l'applicazione di esempio in Android Studio.

  ### iOS
  1. Genera l'applicazione Cordova in Xcode.

    **Suggerimento:** la generazione in Xcode offre più opzioni, come il debug e la configurazione del progetto.

  2. Esegui l'applicazione di esempio in Xcode.

Viene presentata un'applicazione di visualizzazione singola con un pulsante **PING BLUEMIX** (Esegui ping di Bluemix). Quando tocchi il pulsante, l'applicazione verifica la connessione dal client all'applicazione {{site.data.keyword.Bluemix_notm}} di backend. La connessione viene verificata utilizzando la rotta di applicazione specificata nel file `index.js`.


![Applicazione Hello World connessa correttamente a Bluemix](images/yayconnected.jpg "Figura 1. Applicazione Hello World connessa correttamente a Bluemix")


Dopo che hai stabilito con esito positivo una connessione a {{site.data.keyword.Bluemix_notm}} dall'applicazione mobile, viene visualizzato un messaggio che indica che la connessione è stata stabilita ("Yay! la connessione è stata stabilita").


<!--![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")-->

Se la connessione non riesce, viene visualizzato un messaggio di errore. Ulteriori informazioni sull'errore sono incluse nel messaggio. Per risolvere l'errore, puoi controllare i seguenti elementi:

- Verifica di aver incollato correttamente i valori di instradamento e GUID.
- Visualizza il log di debug di Xcode o Android.
- Controlla lo stato dell'applicazione in {{site.data.keyword.Bluemix_notm}}.

## Passi successivi:
{: #next}
Per informazioni su come ottenere l'SDK e integrarlo nella tua applicazione mobile, vedi:
* [Mobile Client Access: Configurazione del plugin Cordova](../../services/mobileaccess/getting-started-cordova.html)
* [Push Notifications: Configurazione del plugin Cordova](../../services/mobilepush/enablepush_cordova.html#setup_sdk_cordova)

# rellinks

## samples
   * [HelloWorld (Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld)

## sdk
   * [bms-clientsdk-cordova-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

<!--## api
   * [Core API](https://classicdocs.{DomainName}/docs/api/content/api/mobilefirst/cordova/core-api-doc/overview-summary.html)
-->
