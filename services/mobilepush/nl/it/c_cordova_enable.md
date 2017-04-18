---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Abilitazione delle applicazioni Cordova alla ricezione di notifiche di push
{: #cordova_enable}
Ultimo aggiornamento: 18 gennaio 2017
{: .last-updated}

Cordova è una piattaforma per creare applicazioni ibride con JavaScript, CSS e HTML. Il servizio {{site.data.keyword.mobilepushshort}} supporta lo sviluppo di applicazioni Android e iOS basate su Cordova.

Puoi abilitare le applicazioni Cordova a ricevere le notifiche di push ai tuoi dispositivi.

## Installazione del plugin push Cordova
{: #cordova_install}

Installa e utilizza il plugin di Push client per sviluppare ulteriormente le tue applicazioni Cordova. Questo installa anche il plugin Cordova core, che inizializza la tua connessione a Bluemix.

### Prima di cominciare

1. Scarica le ultime versioni dell'SDK Android Studio e Xcode.
1. Configura il tuo emulatore. Per Android Studio, utilizza un emulatore che supporti l'API Google Play.
1. Installa lo strumento della riga di comando Git. Per Windows, assicurati di selezionare l'opzione **Esegui Git dal prompt dei comandi della finestra**. Per informazioni su come scaricare e installare questo strumento, consulta [Git ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://git-scm.com/downloads "Icona link esterno"){: new_window}.
1. Installa lo strumento Node.js e il gestore pacchetti di nodi (NPM). Lo strumento della riga comandi NPM è integrato con Node.js. Per informazioni su come scaricare e installare Node.js, consulta [Node.js ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://nodejs.org/en/download/ "Icona link esterno"){: new_window}.
1. Dalla riga comandi, installa gli strumenti della riga di comando Cordova utilizzando il comando **npm install -g cordova**. È necessario per utilizzare il plugin Push Cordova. Per informazioni su come installare Cordova e configurare la tua applicazione Cordova, consulta [Cordova Apache ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cordova.apache.org/#getstarted "Icona link esterno"){: new_window}. Per ulteriori informazioni, vedi il [file readme ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push "Icona link esterno"){: new_window} del plug-in Cordova push.
1. Passa alla cartella in cui vuoi creare la tua applicazione Cordova ed esegui il seguente comando per
           creare un'applicazione Cordova. Se hai un'applicazione Cordova esistente, vai al passo 3.
```cordova create your_app_name
	cd your_app_name
```
	{: codeblock}
- Facoltativo: puoi modificare il file **config.xml** e modificare il nome dell'applicazione nell'elemento <name> in uno a tua scelta, invece del nome predefinito HelloCordova.

Assicurati di specificare l'ID bundle corretto. Il seguente messaggio di errore potrebbe essere in Xcode, se viene specificato un ID bundle non corretto.

* L'eseguibile è stato firmato con diritti non validi.
* I diritti specificati nel tuo file Diritti di firma del codice non corrispondo a quelli specificati nel tuo profilo di provisioning. Per risolvere questo problema, specifica l'ID bundle corretto in Xcode o nel tuo file **config.xml** dell'applicazione Cordova.

1. Aggiungi la API supportata minima o la dichiarazione di destinazione della distribuzione al file config.xml per la tua applicazione Cordova. Il valore minSdkVersion deve essere maggiore di 15. Il valore targetSdkVersion deve sempre riflettere l'SDK Android più recente disponibile da Google.
	
	* Android - Con il tuo editor, apri il file **config.xml** e aggiorna l'elemento
`<platform name="android">` con le versioni SDK minima e di destinazione: 

	```
	<platform name="android">
    	<preference name="android-minSdkVersion" value="15" />
    	<preference name="android-targetSdkVersion" value="23" />
    	<!-- add minimum and target Android API level declaration -->
	</platform> 
	```
    	{: codeblock}

   * iOS - Aggiorna l'elemento <platform name="ios"> con una dichiarazione di destinazione della distribuzione:

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- add deployment target declaration -->
	</platform>
	```
		{: codeblock}

1. Dalla CLI (command-line interface) Cordova, aggiungi le tue piattaforme: iOS, Android o entrambe utilizzando il comando:
```
cordova platform add ios
	cordova platform add android
```
	{: codeblock}

1. Dalla directory root della tua applicazione Cordova, immetti il seguente comando per installare il plugin Cordova push: **cordova plugin add bms-push**. A seconda delle piattaforme da te aggiunte, potresti visualizzare:
```
Installing "bms-push" for android
Installing "bms-push" for ios
```
	{: codeblock}

1. Dalla cartella root della tua applicazione, verifica che i plug-in Cordova core e push siano stati installati correttamente utilizzando questo comando: **cordova plugin list**. A seconda delle piattaforme da te aggiunte, potresti visualizzare:
```
bms-core <version> "BMSCore"
bms-push <version> "BMSPush" 
```
	{: codeblock}

1. Configura il tuo ambiente di sviluppo iOS.
2. Crea ed esegui la tua applicazione con Xcode.
1. Scarica il tuo Firebase `google-services.json` per Android e inseriscilo nella cartella root del tuo progetto Cordova, in `[your-app-name]/platforms/android.
	1. Vai a `[your-app-name]/platforms/android`.
	2. Apri il file `build.gradle` (Percorso : platform > android > build.gradle).
	3. Trova il testo `buildscript` nel file `build.gradle`.
	4. Dopo la riga del classpath, aggiungi la riga classpath 'com.google.gms:google-services:3.0.0'
	5. Trova quindi "dependencies". Seleziona le dipendenze in cui è presente il testo `compile` e subito dopo il punto in cui terminano queste dipendenze aggiungi la riga :apply plugin: 'com.google.gms.google-services'.
	6. Prepara e crea il tuo progetto Android Cordova.
		```
		cordova prepare android
		cordova build android
		```
			{: codeblock}
	**Nota**: prima di aprire il tuo progetto in Android Studio, devi creare la tua applicazione Cordova con la CLI di Cordova. Questo aiuterà nel prevenire errori di generazione.

## Inizializzazione del plugin Cordova
{: #cordova_initialize}

Prima di poter utilizzare il plugin Cordova del servizio {{site.data.keyword.mobilepushshort}}, devi inizializzarlo passando la rotta e il GUID dell'applicazione. Dopo che hai inizializzato il plugin, puoi stabilire una connessione all'applicazione server che hai creato nel dashboard Bluemix. Il plugin Cordova è il contenitore per gli SDK client Android e iOS per abilitare un'applicazione Cordova a comunicare con i servizi Bluemix.

1. Inizializza il BMSClient copiando e incollando il seguente frammento di codice nel tuo file JavaScript principale (normalmente ubicato nella directory **www/js**).

```
onDeviceReady: function() {
	app.receivedEvent('deviceready');
	BMSClient.initialize("YOUR APP REGION");
	var category =  {};
	BMSPush.initialize(appGUID,clientSecret,category);
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	BMSPush.registerDevice({}, success, failure);
	var showNotification = function(notif)
	{
	alert(JSON.stringify(notif));
	};
	BMSPush.registerNotificationsCallback(showNotification);
    } 
```
	{: codeblock}

Passa la regione per la tua applicazione. Sono fornite le seguenti costanti:

```
REGION_US_SOUTH // ".ng.bluemix.net";
REGION_UK //".eu-gb.bluemix.net";
REGION_SYDNEY // ".au-syd.bluemix.net";
```

Ad esempio:

```
BMSClient.initialize(BMSClient.REGION_US_SOUTH);
```

**Nota**: se hai creato un'applicazione Cordova utilizzando la CLI di Cordova, ad esempio, con il comando Cordova create app-name, inserisci questo codice Javascript nel file index.js, dopo la funzione app.receivedEvent all'interno della funzione onDeviceReady: function() per inizializzare `BMSClient`. 


## Registrazione di dispositivi
{: #cordova_register}


Per registrare un dispositivo con il servizio {{site.data.keyword.mobilepushshort}}, richiama il metodo di registro. Copia il seguente frammento di codice nella tua applicazione Cordova per registrare un dispositivo.

```
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure);
```
	{: codeblock}

Il seguente frammento di codice JavaScript mostra come inizializzare il tuo Bluemix Mobile Services client SDK, registra un dispositivo con il servizio {{site.data.keyword.mobilepushshort}} e ascolta le notifiche push. Inserisci questo codice nel tuo file Javascript.

All'interno di **onDeviceReady: function()**.

```
onDeviceReady: function() {
app.receivedEvent('deviceready');
BMSClient.initialize("YOUR APP REGION");
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure); 
 var showNotification = function(notif)
 {
 alert(JSON.stringify(notif));
 };
BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

Aggiungi il seguente frammento di codice Swift alla classe delegato della tua applicazione.

```
// Registra il token dispositivo con Bluemix Push Notification Service
func application(application: UIApplication,
  didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData) {
   CDVBMSPush.sharedInstance().didRegisterForRemoteNotificationsWithDeviceToken(deviceToken)
} 
// Gestisci l'errore in caso di registrazione del token di dispositivo presso APNS non riuscita
func application(application: UIApplication,
    didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer) {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(error)
} 
```
	{: codeblock}

## Fasi successive

{: #cordova_register_next}

Crea il tuo progetto e quindi eseguilo utilizzando i seguenti comandi:

#### Android
{: android-next-steps}

```
cordova build android
```
	{: codeblock}

```
cordova run android
```
	{: codeblock}

#### iOS
{: ios-next-steps}

```
cordova build ios
```
	{: codeblock}

```
cordova run ios
```
	{: codeblock}

## Ricezione di notifiche di push sui dispositivi
{: #cordova_receive}

Copia i seguenti frammenti di codice per ricevere notifiche di push sui dispositivi.

### JavaScript

Aggiungi il seguente frammento di codice JavaScript alla parte web della tua applicazione Cordova.
```
var showNotification = function(notif) {
  alert(JSON.stringify(notif));
        };
        BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

### Proprietà di notifica Android

La seguente selezione elenca le proprietà di notifica Android:

* **message** - messaggio di notifica di push
* **payload** - oggetto JSON che contiene un payload di notifica


### Proprietà di notifica iOS

La seguente sezione elenca le proprietà di notifica iOS:

* **message** - messaggio di notifica di push
* **payload** - oggetto JSON che contiene un payload di notifica
action-loc-key - la stringa viene utilizzata come una chiave per ottenere una stringa localizzata nella localizzazione corrente da utilizzare per il titolo del pulsante appropriato, invece di `View`.
* **badge** - il numero da visualizzare come badge dell'icona applicazione. Se questa proprietà
                            non è presente, il badge non viene modificato. Per rimuovere il badge, imposta
                            il valore di questa proprietà su 0.
* **sound** - il nome di un file audio nel bundle del'applicazione o nella cartella Library/Sounds del contenitore di dati dell'applicazione.


Aggiungi i seguenti frammenti di codice Swift alla classe delegato della tua applicazione.
```
// Gestisci la ricezione di una notifica remota
func application(application: UIApplication,
   didReceiveRemoteNotification userInfo: [NSObject : AnyObject],  fetchCompletionHandler completionHandler: ) {
   CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(userInfo)
}
```
	{: codeblock}

```
// Gestisci la ricezione di una notifica remota all'avvio
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
  let remoteNotif = launchOptions?[UIApplicationLaunchOptionsKey.remoteNotification] as? NSDictionary
  if remoteNotif != nil {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationOnLaunchWithLaunchOptions(launchOptions)
  }
} 
```
	{: codeblock}

## Invio di notifiche di push di base
{: #push-send-notifications}

Dopo che hai sviluppato le tue applicazioni, puoi inviare delle notifiche di push di base.

Per inviare notifiche push di base, completa la seguente procedura:

1. Seleziona **Send Notifications** e componi un messaggio scegliendo l'opzione **Send to**. Le opzioni supportate sono **Device by Tag**, **Device Id**, **User Id**, **Android devices**, **iOS devices**, **Web Notifications** e **All Devices**.
**Nota**: quando selezioni l'opzione **All Devices**, tutti i dispositivi sottoscritti a {{site.data.keyword.mobilepushshort}} riceveranno le notifiche.
![Schermata notifiche](images/tag_notification.jpg)

2. Nel campo **Message**, componi il messaggio. Scegli di configurare le impostazioni facoltative come richiesto.
3. Fai clic su **Send**.
3. Verifica che i tuoi dispositivi abbiano ricevuto la tua notifica.

Il seguente screenshot mostra una casella di avviso che gestisce una {{site.data.keyword.mobilepushshort}} in primo piano su un dispositivo Android e iOS.

![Notifica push in primo piano su Android](images/Android_Screenshot.jpg)

![Notifica push in primo piano su iOS](images/iOS_Screenshot.jpg)

   La seguente immagine mostra {{site.data.keyword.mobilepushshort}} in background per Android.
![Notifica push in background su Android](images/background.jpg)

## Fasi successive
{: #next_steps_tags}

Dopo che hai correttamente configurato le notifiche di base, puoi configurare le notifiche
        basate sulle tag e le opzioni avanzate.

Aggiungi le funzioni del servizio {{site.data.keyword.mobilepushshort}} alla tua applicazione.
Per utilizzare le notifiche basate sulle tag, vedi [Notifiche basate sulle tag](c_tag_basednotifications.html).
Per utilizzare le opzioni di notifica avanzate, vedi [Abilitazione delle notifiche di push avanzate](t_advance_badge_sound_payload.html).
