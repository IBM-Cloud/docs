<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Introduzione all'esempio HelloWorld
{: #gettingstarted-cordova}

Se desideri iniziare a lavorare con una nuova applicazione Cordova, puoi utilizzare l'applicazione HelloWorld. Questa applicazione illustra come stabilire una connessione al tuo backend Bluemix da un'applicazione mobile senza autenticazione. Nell'applicazione è già installato l'SDK. Quando sei pronto, puoi ottenere le specifiche librerie che desideri utilizzare nella tua applicazione.

1. Crea il tuo backend mobile in Bluemix.
<ol>
	<li>Nella sezione Contenitori tipo del catalogo Bluemix, fai clic su MobileFirst Services Starter.</li>
    	<li>Immetti un nome e un host per la tua applicazione e fai clic su **Crea**.</li>
    	<li>Fai clic su **Fine**. </li>
</ol>
2. Ottieni il progetto da GitHub. Per ottenere il progetto puoi, facoltativamente, utilizzare il comando git clone. Dal tuo computer, apri il terminale e immetti quindi il seguente comando:
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld
```

3. Esegui i seguenti comandi dalla directory del tuo progetto per aggiungere gli ambienti di piattaforma Android e iOS:

Android:
```
cordova platform add android
```

iOS:
```
cordova platform add ios
```

4. Aggiungi il plug-in Cordova con il seguente comando:
```
cordova plugin add ibm-mfp-core
```

5. Configura la tua applicazione Cordova per Android, iOS o entrambi.

 * Android

	 Prima di aprire il tuo progetto in Android Studio, crea ed esegui la tua applicazione Cordova tramite la tua interfaccia riga di comando (CLI) per evitare errori di build.

	 ```
	 cordova build android
	 ```

	 ```
	 cordova run android
	 ```

 * iOS

	 Configura il tuo progetto Xcode nel seguente modo per evitare errori di build.

	    1. Utilizza la versione più recente di Xcode per aprire il tuo file xcode.proj nella directory &lt;nome_applicazione&gt;/platforms/ios.

			**Importante:** se ricevi un messaggio che indica di eseguire la conversione alla sintassi Swift più recente ("Convert to Latest Swift Syntax"), fai clic su Cancel.

		2. Vai a **Build Settings > Swift Compiler - Code Generation > Objective-C Bridging Header** e aggiungi il seguente percorso:

		```
		<il_nome_del_tuo_progetto>/Plugins/ibm-mfp-core/Bridging-Header.h
		```
		3. Vai a **Build settings > Linking > Runpath Search Paths** e aggiungi il seguente parametro Frameworks:

		```
		@executable_path/Frameworks
		```
		4. Crea ed esegui la tua applicazione con Xcode.

6. Configura l'esempio HelloWorld
<ol>
	<li>Passa alla directory dove hai clonato il progetto</li>
	<li>Apri il file &lt;tua_directory_applicazione&gt;/www/js/index.js e sostituisci &lt;ROTTA_APPLICAZIONE&gt; e &lt;ID_APPLICAZIONE&gt; con i tuoi valori di ID applicazione e rotta Bluemix.</li>
</ol>

Nota: accertati che la tua &lt;ROTTA_APPLICAZIONE&gt; stia utilizzando in modo sicuro il protocollo https.

```
// Credenziali Bluemix
route: "<ROTTA_APPLICAZIONE>",
GUID: "<GUID_APPLICAZIONE>",
```

7. Esegui l'esempio sul tuo dispositivo o sul tuo emulatore mobile.

   Crea l'applicazione Cordova utilizzando i seguenti comandi:
	 ```
	 cordova build ios
	 ```
	 ```
	 cordova build android
	 ```

   Esegui l'applicazione di esempio utilizzando i seguenti comandi:
	 ```
	 cordova run ios
	 ```
   ```
	 cordova run android
	 ```


Viene visualizzata un'applicazione con una singola vista con un pulsante **ESEGUI PING BLUEMIX**. Quando selezioni il pulsante, l'applicazione verifica la connessione dal client all'applicazione Bluemix di backend. La connessione viene verificata utilizzando la rotta applicazione da te specificata nel file index.js.


![Applicazione Hello World connessa correttamente a Bluemix](images/yayconnected.jpg "Figura 1. Applicazione Hello World connessa correttamente a Bluemix")

Quando stabilisci correttamente una connessione a Bluemix dall'applicazione mobile, viene visualizzato un messaggio che indica che la connessione è stata stabilita con esito positivo (Yay! You are connected).
8. Risolvi gli eventuali problemi.

<!--![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")-->

Se la connessione non riesce, viene visualizzato un messaggio che indica che qualcosa è andato storto (Bummer Something went wrong). Sono incluse delle ulteriori informazioni sull'errore.
Controllare i seguenti elementi:
 * Verifica di avere incollato correttamente i valori di rotta e GUID.
 * Visualizza il log di debug Xcode o Android.
 * Controlla lo stato della tua applicazione in Bluemix.

## Passi successivi:
{: #next}
Per informazioni su come ottenere SDK e integrarlo nella tua applicazione mobile, vedi Impostazione dell'SDK client Cordova.

# rellinks

## samples
   * [HelloWorld (Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld)

## sdk
   * [bms-clientsdk-cordova-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

<!--## api
   * [Core API](https://www.{DomainName}/docs/api/content/api/mobilefirst/cordova/core-api-doc/overview-summary.html)
-->
