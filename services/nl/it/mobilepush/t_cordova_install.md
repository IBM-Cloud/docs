---

copyright:
 years: 2015, 2016

---

# Installazione del plugin Cordova
{: #cordova_install}

Installa e utilizza il plugin di Push client per sviluppare ulteriormente le tue applicazioni Cordova. Questo installa anche il plugin Cordova Core, che inizializza la tua connessione a Bluemix.

### Prima di cominciare

1. Scarica le ultime versioni dell'SDK Android Studio e Xcode.
1. Configura il tuo emulatore. Per Android Studio, utilizza un emulatore che supporti l'API Google Play.
1. Installa lo strumento della riga di comando Git. Per Windows, assicurati di selezionare l'opzione **Esegui Git dal prompt dei comandi della finestra**. Per informazioni su come scaricare e installare questo strumento, consulta [Git](https://git-scm.com/downloads).

1. Installa lo strumento Node.js e il gestore pacchetti di nodi (NPM). Lo strumento della riga comandi NPM è integrato con Node.js. Per informazioni su come scaricare e installare Node.js, consulta [Node.js](https://nodejs.org/en/download/).
1. Dalla riga comandi, installa gli strumenti della riga di comando Cordova utilizzando il comando **npm install -g cordova**. È necessario per utilizzare il plugin Push Cordova. Per informazioni su come installare Cordova e configurare la tua applicazione Cordova, consulta [Cordova Apache](https://cordova.apache.org/#getstarted).

	**Nota**: per visualizzare il file readme del plugin Push Cordova, vai a [https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push)


## Installazione del plugin Cordova
1. Passa alla cartella in cui vuoi creare la tua applicazione Cordova ed esegui il seguente comando per
           creare un'applicazione Cordova. Se hai un'applicazione Cordova esistente, vai al passo 3.


	cordova create your_app_name
	cd your_app_name
	```
1. Facoltativo: (Facoltativo) modifica il file **config.xml** e modifica il nome dell'applicazione nell'elemento <name> in uno a tua scelta, invece del nome predefinito HelloCordova.

	**Nota**: assicurati di specificare l'ID bundle corretto. In caso contrario, i seguenti messaggi di errore vengono visualizzati in Xcode.
	* L'eseguibile è stato firmato con diritti non validi.
	* I diritti specificati nel tuo file Diritti di firma del codice non corrispondo a quelli specificati nel tuo profilo di provisioning.

	Per risolvere questo problema, specifica l'ID bundle corretto in Xcode o nel tuo file **config.xml** dell'applicazione Cordova.

1. Aggiungi la API supportata minima o la dichiarazione di destinazione della distribuzione al file config.xml per la tua applicazione Cordova. Il valore minSdkVersion deve essere maggiore di 15. Il valore targetSdkVersion deve sempre riflettere l'SDK Android più recente disponibile da Google.
	* **Android** - Con il tuo editor, apri il file config.xml e aggiorna l'elemento
```<platform name="android">``` con le versioni SDK minima e di destinazione:

	```
	<!-- add deployment target declaration -->
	<platform name="android">  
			  <preference name="android-minSdkVersion" value="15" />
			  <preference name="android-targetSdkVersion" value="23" />
			</platform>
	```
   * **iOS** - Aggiorna l'elemento <platform name="ios"> con una dichiarazione di destinazione della distribuzione:

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- other properties -->
	</ platform>
	```

1. Dalla CLI (command-line interface) Cordova, aggiungi le tue piattaforme: iOS, Android o entrambe utilizzando i seguenti comandi.

	```
	cordova platform add ios
	cordova platform add android
	```
1. Dalla directory root della tua applicazione Cordova, immetti il seguente comando per installare il plugin Cordova Push: **cordova plugin add ibm-mfp-push**.

	A seconda delle piattaforme da te aggiunte, vedrai qualcosa di simile a questo:

	```
	Installing "ibm-mfp-push" for android
	Installing "ibm-mfp-push" for ios
	```
1. Da *your-app-root-folder*, verifica che i plugin Cordova Core e Push siano stati installati correttamente utilizzando questo comando: **cordova plugin list**.

	A seconda delle piattaforme da te aggiunte, vedrai qualcosa di simile a questo:

	```
	ibm-mfp-core 1.0.0 "MFPCore"
	ibm-mfp-push 1.0.0 “MFPPush"
	```
1. (solo iOS) - Configura il tuo ambiente di sviluppo iOS.
	a. Apri il tuo file your-app-name.xcodeproj nella directory *your-app-name***/platforms/ios** con Xcode.

	b. Aggiungi l'intestazione di collegamento. Vai a **Build settings > Swift Compiler - Code Generation > Objective-C Bridging Header** e aggiungi il seguente percorso: *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	c. Aggiungi il parametro Frameworks. Vai a **Build Settings > Linking > Runpath Search Paths** e aggiungi il seguente parametro:
	```
	@executable_path/Frameworks
	```
	d. Rimuovi il commento per le seguenti istruzioni di importazione push nella tua intestazione di collegamento. Vai a *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	```
	//#import <IMFPush/IMFPush.h>
	//#import <IMFPush/IMFPushClient.h>
	//#import <IMFPush/IMFResponse+IMFPushCategory.h>
	```
	e. Crea ed esegui la tua applicazione con Xcode.
1. (solo Android)- Crea il tuo progetto Android utilizzando il seguente comando:
**cordova build android**.

	**Nota**: prima di aprire il tuo progetto in Android Studio, devi prima creare la tua applicazione Cordova con la CLI di Cordova. Altrimenti, riscontrerai degli errori di generazione.

1. Fase successiva. [Inizializzazione del plugin Cordova](t_cordova_initalize.html).
