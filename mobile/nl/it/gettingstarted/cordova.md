<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Introduzione all'esempio HelloWorld
{: #gettingstarted-cordova}
*Ultimo aggiornamento: 2 marzo 2016*

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

	Android:

	```Bash
	cordova platform add android
	```

	iOS:

	```Bash
	cordova platform add ios
	```

4. Aggiungi il plugin Cordova con il seguente comando:

	```Bash
	cordova plugin add ibm-mfp-core
	```

5. Configura la tua applicazione Cordova per Android, iOS o entrambi.

	* **Android**

		Prima di aprire il tuo progetto in Android Studio, genera ed esegui la tua applicazione Cordova tramite l'interfaccia riga di comando (CLI) per evitare errori durante la generazione.

		```Bash
		cordova build android
		```

		```Bash
		cordova run android
		```

	* **iOS**

		Per evitare errori durante la generazione, configura il tuo progetto Xcode nel seguente modo.

		- Utilizza la versione più recente di Xcode per aprire il tuo file `xcode.proj` nella directory *&lt;nome_applicazione&gt;*/platforms/ios.

			**Importante:** se ricevi un messaggio che ti invita ad eseguire la conversione alla sintassi Swift più recente ("Convert to Latest Swift Syntax"), fai clic su **Cancel**.

		- Vai a **Build Settings > Swift Compiler - Code Generation > Objective-C Bridging Header** e aggiungi il seguente percorso:

			```
			<il_nome_del_tuo_progetto>/Plugins/ibm-mfp-core/Bridging-Header.h
			```

		- Vai a **Build settings > Linking > Runpath Search Paths** e aggiungi il seguente parametro Frameworks:

			```
			@executable_path/Frameworks
			```

		- Genera ed esegui la tua applicazione con Xcode.		
6. Configura l'esempio HelloWorld.

	- Passa alla directory dove hai clonato il progetto.
	- Apri il file *&lt;directory_della_tua_applicazione&gt;*/www/js/index.js e sostituisci *&lt;ROTTA_APPLICAZIONE&gt;* e *&lt;ID_APPLICAZIONE&gt;* con i tuoi valori di ID applicazione e rotta Bluemix.

		**Nota:** assicurati che la tua rotta stia utilizzando la protezione del protocollo https.

		```Javascript
		// Bluemix credentials
		route: "<ROTTA_APPLICAZIONE>",
		GUID: "<GUID_APPLICAZIONE>",
		```

7. Esegui l'esempio sul tuo emulatore o sul tuo dispositivo mobile.

	Genera l'applicazione Cordova utilizzando i seguenti comandi:

	```Bash
	cordova build android
	```

	```Bash
	cordova build ios
	```

	Esegui l'applicazione di esempio utilizzando questi comandi:

	```Bash
	cordova run android
	```

	```Bash
	cordova run ios
	```

Viene presentata un'applicazione di visualizzazione singola con un pulsante **PING BLUEMIX** (Esegui ping di Bluemix). Quando tocchi il pulsante, l'applicazione verifica la connessione dal client all'applicazione {{site.data.keyword.Bluemix_notm}} di backend. La connessione viene verificata utilizzando la rotta di applicazione specificata nel file `index.js`.


![Applicazione Hello World connessa correttamente a Bluemix](images/yayconnected.jpg "Figura 1. Applicazione Hello World connessa correttamente a Bluemix")


Dopo che hai stabilito con esito positivo una connessione a {{site.data.keyword.Bluemix_notm}} dall'applicazione mobile, viene visualizzato un messaggio che indica che la connessione è stata stabilita ("Yay! You are connected").


<!--![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")-->

Se la connessione non riesce, viene visualizzato un messaggio di errore. Ulteriori informazioni sull'errore sono incluse nel messaggio. Per risolvere l'errore, puoi controllare i seguenti elementi:

- Verifica di aver incollato correttamente i valori di instradamento e GUID.
- Visualizza il log di debug di Xcode o Android.
- Controlla lo stato dell'applicazione in {{site.data.keyword.Bluemix_notm}}.

## Passi successivi:
{: #next}
Per informazioni su come ottenere l'SDK e integrarlo nella tua applicazione mobile, vedi:
* [Mobile Client Access: Configurazione del plugin Cordova](../services/mobileaccess/getting-started-cordova.html)
* [Push Notifications: Configurazione del plugin Cordova](../mobilepush/enablepush_cordova.html#setup_sdk_cordova)

# rellinks

## samples
   * [HelloWorld (Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld)

## sdk
   * [bms-clientsdk-cordova-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

<!--## api
   * [Core API](https://www.{DomainName}/docs/api/content/api/mobilefirst/cordova/core-api-doc/overview-summary.html)
-->
