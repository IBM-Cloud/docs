---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Abilitazione delle notifiche per i dispositivi mobili
{: #c_enable_push-notifications}
Ultimo aggiornamento: 12 aprile 2017
{: .last-updated}

Assicurati di aver consultato [Configurazione delle credenziali per un provider di notifica](t__main_push_config_provider.html).

Questa sezione descrive come abilitare le tue applicazioni client - mobili, browser web e anche le estensioni e le applicazioni Chrome per ricevere notifiche di push e in che modo dettagliato come creare notifiche di base, ottenere e inizializzare l'SDK o il plugin e come registrare il tuo dispositivo o browser per ricevere notifiche di push. Puoi anche abilitare le tue applicazioni mobili o browser web a ricevere notifiche di push utilizzando la [API REST](t_restapi.html).

**Nota**: per le registrazioni del dispositivo, del browser, delle estensioni e delle applicazioni Chrome, il servizio {{site.data.keyword.mobilepushshort}} conserva un riferimento univoco ai token emessi dai provider di notifica -
APNs per Apple o FCM per Google. I token possono essere annullati dal provider di notifica del servizio {{site.data.keyword.mobilepushshort}} per molti motivi. 

Ad esempio, durante la disinstallazione di un'applicazione sul dispositivo. In questo scenario, quando viene tentato l'invio di una notifica in base ai provider, la risposta del dispositivo viene annullata, il servizio {{site.data.keyword.mobilepushshort}} rimuoverà le registrazioni del dispositivo o del browser web. Ciò impedirà i seguenti tentativi di invio della notifica ai dispositivi annullati.


## Abilitazione delle applicazioni Android alla ricezione di notifiche di push
{: #tag_based_notifications}


Puoi abilitare le applicazioni Android a ricevere le notifiche di push ai tuoi dispositivi. Android Studio è un prerequisito ed è il metodo raccomandato per creare progetti Android. La conoscenza di base di Android Studio è fondamentale.

### Installazione del Push SDK client con Gradle
{: #android_install}

Questa sezione descrive come installare e utilizzare il Push SDK client per sviluppare
    ulteriormente le tue applicazioni Android.

Puoi aggiungere il Push SDK di {{site.data.keyword.Bluemix}} Mobile Services utilizzando [Gradle ![icona link esterno](../../icons/launch-glyph.svg "External link icon")](http://developer.android.com/tools/building/configuring-gradle.html){: new_window}, che scarica automaticamente le risorse dai repository e le rende disponibili alla tua applicazione Android. Assicurati di impostare correttamente [Android Studio ![icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://developer.android.com/tools/studio/index.html) e l'SDK Android Studio. 

Dopo aver creato e aperto la tua applicazione mobile, completa la seguente procedura utilizzando Android Studio.

1. Aggiungi le dipendenze al tuo file **build.gradle** di livello del modulo. 	

	- Aggiungi la seguente dipendenza per includere il client di push dei servizi Bluemix™ Mobile e l'SDK dei servizi Google Play alle tue dipendenze dell'ambito di compilazione.
	```
	com.ibm.mobilefirstplatform.clientsdk.android:push:3.+
	```
    	{: codeblock}
	
	- Aggiungi le seguenti dipendenze per importare le istruzioni obbligatorie per i frammenti di codice.
	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```
    	{: codeblock}

	- Aggiungi le seguenti dipendenze alla fine del tuo file **build.gradle** di livello del modulo.
	```
		apply plugin: 'com.google.gms.google-services'
	```
		{: codeblock}
3. Aggiungi le seguenti dipendenze al tuo file **build.gradle** di livello del progetto.
```
dependencies {
    classpath 'com.android.tools.build:gradle:2.2.3'
    classpath 'com.google.gms:google-services:3.0.0'
}
``` 
    {: codeblock}
5. Nel file **AndroidManifest.xml**, aggiungi le seguenti autorizzazioni. Per visualizzare un manifest di esempio, vedi [Applicazione di esempio helloPush Android ![Icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml){: new_window}. Per visualizzare un file Gradle di esempio, vedi [Sample Build Gradle file ![Icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle){: new_window}.
```
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
```
	{: codeblock}
 Consulta le informazioni sulle [Autorizzazioni Android ![icona link esterno](../../icons/launch-glyph.svg "External link icon")](http://developer.android.com/guide/topics/security/permissions.html){: new_window} qui.

4. Aggiungi le impostazioni di intento di notifica per l'attività. Questa impostazione avvia l'applicazione
          quando l'utente fa clic sulla notifica ricevuta dall'area di notifica.
```
	<intent-filter>
	<action android:name="Your_Android_Package_Name.IBMPushNotification"/>
	<category  android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
```
	{: codeblock}
**Nota**: sostituisci *Your_Android_Package_Name* nell'azione sopra indicata con il nome del pacchetto applicazione utilizzato nella tua applicazione.

5. Aggiungi il servizio di intento FCM (Firebase Cloud Messaging) o GCM (Google Cloud Messaging) e i filtri di intento per le notifiche di evento RECEIVE e REGISTRATION.
```
	<service android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushIntentService"
    android:exported="true" >
    	<intent-filter>
        <action android:name="com.google.firebase.MESSAGING_EVENT" />
    </intent-filter>
	</service>
<service
    android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush"
    android:exported="true" >
    <intent-filter>
        <action android:name="com.google.firebase.INSTANCE_ID_EVENT" />
    </intent-filter>
	</service>
```
    {: codeblock}

6. Il servizio {{site.data.keyword.mobilepushshort}} supporta il richiamo di notifiche individuali dalla barra di notifica. Per le notifiche a cui accede la barra di notifica, ti viene fornito un gestore solo per la notifica su cui stai facendo clic. Vengono visualizzate tutte le notifiche quando l'applicazione viene aperta manualmente. Aggiorna il tuo file **AndroidManifest.xml** con il seguente frammento per utilizzare questa funzionalità:

```
	<activity android:name="
com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationHandler"
android:theme="@android:style/Theme.NoDisplay"/>
```
    {: codeblock}

Assicurati di aver consultato [Configurazione delle credenziali per un provider di notifica](t__main_push_config_provider.html) per configurare il progetto FCM e ottenere le tue credenziali. Completa la seguente procedura utilizzando la console FCM (Firebase Cloud Messaging).

1. Nella console Firebase, fai clic sull'icona **Impostazioni progetto**.
    ![Impostazioni progetto Firebase](images/FCM_4.jpg)

3. Seleziona **AGGIUNGI APPLICAZIONE** o l'**icona Aggiungi Firebase alla tua applicazione Android** dalla scheda Generale nel pannello Tue applicazioni.
    ![Aggiunta di Firebase a Android](images/FCM_5.jpg)

4. Nella finestra Aggiungi Firebase alla tua applicazione Android, aggiungi **com.ibm.mobilefirstplatform.clientsdk.android.push** come nome pacchetto. Il campo Nome alternativo applicazione è facoltativo. Fai clic su **AGGIUNGI APPLICAZIONE**. 
    ![Finestra Aggiunta di Firebase al tuo Android](images/FCM_1.jpg)

5. Includi il nome pacchetto della tua applicazione immettendolo nella finestra Aggiungi Firebase alla tua applicazione Android. Il campo Nome alternativo applicazione è facoltativo. Fai clic su **AGGIUNGI APPLICAZIONE**. 

	![Aggiunta del nome pacchetto della tua applicazione](images/FCM_2.jpg)

6. Viene generato il file `google-services.json`. Copia il file `google-services.json` nella directory root del modulo della tua applicazione Android. Nota che il file `google-service.json` include i nomi dei pacchetti aggiunti.

    ![Aggiunta del file json alla directory root della tua applicazione](images/FCM_7.jpg)

5. Nella finestra Aggiungi Firebase alla tua applicazione Android, fai clic su **Continua** e quindi su **Fine**. 

  

Crea ed esegui la tua applicazione.

### Inizializzazione di Push SDK per applicazioni Android
{: #android_initialize}

Un posto comune dove inserire il codice di inizializzazione è nel metodo onCreate dell'attività principale nella tua applicazione Android. Esistono due componenti per la SDK che deve essere inizializzata. Uno è la SDK core e l'altro è la SDK push che si basa sulla SDK core.

#### Inizializzazione dell'SDK Core
{: #initz_core_sdk}

```
// Inizializza l'SDK per Android
    BMSClient.getInstance().initialize(this, BMSClient.REGION_US_SOUTH);
```
    {: codeblock}

#### bluemixRegionSuffix
{: #bluemixRegionSuffix}

Specifica l'ubicazione in cui è ospitata l'applicazione. Puoi utilizzare uno dei seguenti tre valori:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

#### Inizializza il Push SDK client
{: #initiz_client_pushSDK}

```
//Inizializza il Push SDK for Java client
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext(), "appGUID", "clientSecret");
```
	{: codeblock}

#### AppGUID
{: #appguid_initialize_client_push_sdk}

Questa è la chiave AppGUID del servizio {{site.data.keyword.mobilepushshort}}. Questo valore è
                sensibile al maiuscolo/minuscolo. Apri il dashboard Push Notification e seleziona la scheda di configurazione. Puoi ottenere questo valore dalle opzioni mobili nella scheda di configurazione del dashboard del servizio Push Notification. 

### Registrazione di dispositivi Android
{: #android_register}

Utilizza l'API `MFPPush.register()` per registrare il dispositivo con il servizio {{site.data.keyword.mobilepushshort}}. Per registrare i dispositivi Android, aggiungi le informazioni FCM (Firebase Cloud Messaging) nel dashboard di configurazione del servizio Bluemix {{site.data.keyword.mobilepushshort}}. Per ulteriori informazioni, vedi [Configurazione delle credenziali per un provider di notifica](t__main_push_config_provider.html).

Copia i seguenti frammenti di codice nella tua applicazione mobile Android.

```
	//Registra dispositivi Android
	push.registerDevice(new MFPPushResponseListener<String>() {
    	@Override
    	public void onSuccess(String response) {
    		//gestisce esiti positivi qui
	    }
		@Override
    public void onFailure(MFPPushException ex) {
    		//gestisce esiti negativi qui
	    }
		});
```
	{: codeblock}


```
	//Gestisci la notifica quando arriva
	MFPPushNotificationListener notificationListener = new MFPPushNotificationListener() {
    @Override
	    public void onReceive (final MFPSimplePushNotification message){
	      // Gestisci Push Notification
	    }
		};
```
	{: codeblock}

### Ricezione di notifiche di push su dispositivi Android
{: #android_receive}

1. Per registrare l'oggetto notificationListener con il servizio Push Notifications, utilizza il metodo `MFPPush.listen()`. Questo metodo viene di norma richiamato dai metodi `onResume()` e `onPause` dell'attività che sta gestendo le notifiche di push.
```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
       push.listen(notificationListener);
	   }
	}
```
	{: codeblock}
```
	@Override
protected void onPause() {
    super.onPause();
    if (push != null) {
        push.hold();
    }
	}
```
	{: codeblock}

2. Crea il progetto ed eseguilo sul dispositivo o sull'emulatore. Quando il metodo onSuccess() viene richiamato per il listener di risposte nel metodo register(), si conferma che il dispositivo è stato registrato correttamente con il servizio {{site.data.keyword.mobilepushshort}} e puoi quindi inviare una notifica di push.
3. Verifica che i tuoi dispositivi abbiano ricevuto la tua notifica. Se l'applicazione è in
            primo piano, la notifica viene gestita da `MFPPushNotificationListener`. Se l'applicazione è in background, viene visualizzato un messaggio nella barra di notifica.

### Monitoraggio di notifiche di push su dispositivi Android
{: #android_monitor}

Per monitorare lo stato corrente della notifica all'interno dell'applicazione, puoi implementare l'interfaccia `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener` e definire il metodo onStatusChange(String messageId, MFPPushNotificationStatus status). 

Il `messageId` è l'identificativo del messaggio inviato dal server.  `MFPPushNotificationStatus` definisce lo stato delle notifiche come valori:

- RECEIVED - L'applicazione ha ricevuto la notifica. 
- QUEUED - L'applicazione mette in coda la notifica per richiamare il listener delle notifiche. 
- OPENED - L'utente apre la notifica selezionandola dalla barra o avviandola dall'icona dell'applicazione oppure quando l'applicazione è in primo piano. 
- DISMISSED - L'utente cancella/ignora la notifica nella barra.

Devi registrare la classe `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener` con MFPPush.

```
	push.setNotificationStatusListener(new MFPPushNotificationStatusListener() {
	@Override
public void onStatusChange(String messageId, MFPPushNotificationStatus status) {
		// Handle status change
}
	});
```
    {: codeblock}


#### In ascolto dello stato DISMISSED
{: #android_monitor_listen}

Puoi scegliere di ascoltare lo stato DISMISSED in una delle seguenti condizioni:

- Quando l'applicazione è attiva (in esecuzione in primo piano o in background)

  Aggiungi il frammento al tuo file `AndroidManifest.xml`:

```
	<receiver android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler">
<intent-filter>
<action android:name="Your_Android_Package_Name.Cancel_IBMPushNotification"/>
	</intent-filter>
	</receiver>
```
	{: codeblock}

- Quando l'applicazione è attiva (in esecuzione in primo piano o in background) e non in esecuzione (chiusa)

Estendi il ricevitore broadcast `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler` e sovrascrivi il metodo `onReceive()`, dove `MFPPushNotificationStatusListener` deve essere registrato prima di richiamare il metodo `onReceive()` della classe di base.

```
	public class MyDismissHandler extends MFPPushNotificationDismissHandler {
	@Override
public void onReceive(Context context, Intent intent) {
	MFPPush.getInstance().setNotificationStatusListener(new MFPPushNotificationStatusListener() {
	@Override
public void onStatusChange(String messageId, MFPPushNotificationStatus status) {
	// Handle status change
}
	});
super.onReceive(context, intent);
}
	}
```
    {: codeblock}


Aggiungi il seguente frammento al tuo file `AndroidManifest.xml`:

```
	<receiver android:name="Your_Android_Package_Name.Your_Handler">
<intent-filter>
<action android:name="Your_Android_Package_Name.Cancel_IBMPushNotification"/>
	</intent-filter>
	</receiver>
```
    {: codeblock}

### Invio delle notifiche di push di base
{: #send-basic-notification}

Dopo che hai sviluppato le tue applicazioni, puoi inviare delle notifiche di push di base.

Per inviare notifiche di push di base, completa la seguente procedura:

1. Seleziona **Send Notifications** e componi un messaggio scegliendo l'opzione **Send to**. Le opzioni supportate sono **Device by Tag**, **Device Id**, **User Id**, **Android devices**, **iOS devices**, **Web Notifications** e **All Devices**.
**Nota**: quando selezioni l'opzione **All Devices**, tutti i dispositivi sottoscritti a {{site.data.keyword.mobilepushshort}} riceveranno le notifiche.
![Schermata notifiche](images/tag_notification.jpg)

2. Nel campo **Message**, componi il messaggio. Scegli di configurare le impostazioni facoltative come richiesto.
3. Fai clic su **Send**.
3. Verifica che i tuoi dispositivi abbiano ricevuto la tua notifica.

Il seguente screenshot mostra una casella di avviso che gestisce una notifica push
in primo piano su un dispositivo Android.

![Notifica push in primo piano su Android](images/Android_Screenshot.jpg)

Il seguente screenshot mostra una notifica push in background per Android.

![Notifica push in background su Android](images/background.jpg)

### Impostazioni Android facoltative per l'invio delle notifiche
{: #send_otpional_setting}

Puoi anche personalizzare le impostazioni di {{site.data.keyword.mobilepushshort}} per inviare le notifiche ai dispositivi Android. Sono supportate le seguenti opzioni di personalizzazione facoltative:
![Impostazioni personalizzate Android](images/android_custom_settings.jpg)

- Chiave di compressione:  le chiavi di compressione solo allegate alle notifiche. Se più notifiche arrivano in sequenza con la stessa chiave di compressione quando il dispositivo è offline, esse vengono compresse. Quando un dispositivo va online, riceve le notifiche dal server FCM/GCM e visualizza solo l'ultima notifica rilevando la stessa chiave di compressione. Se la chiave di compressione non viene inviata, sia il nuovo che il vecchio messaggio vengono archiviati per una consegna successiva.
- Audio: indica un file audio da riprodurre alla ricezione di una notifica. Supporta il valore predefinito o il nome di una risorsa audio integrata nell'applicazione.
- Icona: specifica il nome dell'icona da visualizzare per la notifica. Assicurati di aver fornito l'icona nella cartella `res/drawable`, insieme all'applicazione client.
- Priorità: specifica le opzioni per l'assegnazione della priorità di consegna dei messaggi. Una priorità `high` o `max` creerà una notifica di avviso, mentre i messaggi di priorità `low` o `default` non apriranno le connessioni di rete in un dispositivo silenzioso. Per i messaggi con l'opzione impostata su `min`, sarà inviata una notifica silenziosa.
- Visibilità: puoi scegliere di impostare l'opzione di visibilità della notifica su `public` o `private`. L'opzione `private` limita la visualizzazione pubblica e puoi scegliere di abilitarla se il tuo dispositivo è protetto da un pattern o un pin e l'impostazione di notifica è impostata su **Hide sensitive notification content**. Quando la visibilità è impostata su `private`, è necessario menzionare un campo `redact`. Solo il contenuto specificato nel campo `redact` sarà visualizzato nella schermata di blocco sicura nel dispositivo. Scegliendo `public` sarà possibile leggere le notifiche liberamente.
- TTL (Time to live): questo valore è impostato in secondi. Se questo parametro non viene specificato, il server FCM/GCM archivia il messaggio per quattro settimane e tenterà di consegnarlo. La validità scade dopo quattro settimane. L'intervallo di valori possibile è compreso tra 0 e 2,419,200 secondi.
- Ritarda quando inattivo: l'impostazione di questo valore su `true` indica al server FCM/GCM di non consegnare la notifica se il dispositivo è inattivo. Imposta questo valore su `false`, per assicurati di consegnare la notifica anche se il dispositivo è inattivo.
- Sincronizzazione: impostando questa opzione su `true`, le notifiche vengono sincronizzate in tutti i tuoi dispositivi registrati. Se l'utente con un nome utente dispone di più dispositivi con la stessa applicazione installata, la lettura della notifica su un dispositivo assicura l'eliminazione delle notifiche negli altri dispositivi. Devi assicurarti di essere registrato con il servizio {{site.data.keyword.mobilepushshort}} con l'ID utente per questa opzione perché funzioni.
- Payload addizionale: specifica i valori di payload personalizzati per le tue notifiche.


### Fasi successive
{: #next_steps_tag_based_notifications}

Dopo che hai correttamente configurato le notifiche di base, puoi configurare le notifiche
        basate sulle tag e le opzioni avanzate.

Aggiungi queste funzioni del Servizio push notifications alla tua applicazione.
Per utilizzare le notifiche basate sulle tag, vedi [Notifiche basate sulle tag](c_tag_basednotifications.html).
Per utilizzare le opzioni di notifica avanzate, vedi [Abilitazione delle notifiche di push avanzate](t_advance_badge_sound_payload.html).


## Abilitazione delle applicazioni Cordova alla ricezione di notifiche di push
{: #cordova_enable}


Cordova è una piattaforma per creare applicazioni ibride con JavaScript, CSS e HTML. Il servizio {{site.data.keyword.mobilepushshort}} supporta lo sviluppo di applicazioni Android e iOS basate su Cordova.

Puoi abilitare le applicazioni Cordova a ricevere le notifiche di push ai tuoi dispositivi.

### Installazione del plugin push Cordova
{: #cordova_install}

Installa e utilizza il plugin di Push client per sviluppare ulteriormente le tue applicazioni Cordova. Questo installa anche il plugin Cordova core, che inizializza la tua connessione a Bluemix.

1. Scarica le ultime versioni dell'SDK Android Studio e Xcode.
1. Configura il tuo emulatore. Per Android Studio, utilizza un emulatore che supporti l'API Google Play.
1. Installa lo strumento della riga di comando Git. Per Windows, assicurati di selezionare l'opzione **Esegui Git dal prompt dei comandi della finestra**. Per informazioni su come scaricare e installare questo strumento, vedi [Git ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://git-scm.com/downloads){: new_window}.
1. Installa lo strumento Node.js e il gestore pacchetti di nodi (NPM). Lo strumento della riga comandi NPM è integrato con Node.js. Per informazioni su come scaricare e installare Node.js, vedi [Node.js ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://nodejs.org/en/download/){: new_window}.
1. Dalla riga comandi, installa gli strumenti della riga di comando Cordova utilizzando il comando **npm install -g cordova**. È necessario per utilizzare il plugin Push Cordova. Per informazioni su come installare Cordova e configurare la tua applicazione Cordova, vedi [Cordova Apache ![Icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://cordova.apache.org/#getstarted){: new_window}. Per ulteriori informazioni, vedi il [file Readme ![Icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window} del plug-in push Cordova.
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

### Inizializzazione del plugin Cordova
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


### Registrazione di dispositivi
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

### Fasi successive
{: #cordova_register_next}

Crea il tuo progetto e quindi eseguilo utilizzando i seguenti comandi:

#### Android
{: #android-next-steps}

```
cordova build android
```
	{: codeblock}

```
cordova run android
```
	{: codeblock}

#### iOS
{: #ios-next-steps}

```
cordova build ios
```
	{: codeblock}

```
cordova run ios
```
	{: codeblock}

### Ricezione di notifiche di push sui dispositivi
{: #cordova_receive}

Copia i seguenti frammenti di codice per ricevere notifiche di push sui dispositivi.

#### JavaScript
{: #jvscrpt}

Aggiungi il seguente frammento di codice JavaScript alla parte web della tua applicazione Cordova.
```
var showNotification = function(notif) {
  alert(JSON.stringify(notif));
        };
        BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

#### Proprietà di notifica Android
{: #And_notif}

La seguente selezione elenca le proprietà di notifica Android:

* **message** - messaggio di notifica di push
* **payload** - oggetto JSON che contiene un payload di notifica


#### Proprietà di notifica iOS
{: #ios_notif}

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

### Invio di notifiche di push di base
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

#### Fasi successive
{: #next_steps_basic_notifications}

Dopo che hai correttamente configurato le notifiche di base, puoi configurare le notifiche
        basate sulle tag e le opzioni avanzate.

Aggiungi le funzioni del servizio {{site.data.keyword.mobilepushshort}} alla tua applicazione.
Per utilizzare le notifiche basate sulle tag, vedi [Notifiche basate sulle tag](c_tag_basednotifications.html).
Per utilizzare le opzioni di notifica avanzate, vedi [Abilitazione delle notifiche di push avanzate](t_advance_badge_sound_payload.html).


## Abilitazione delle applicazioni iOS all'invio di notifiche di push
{: #enable-push-ios-notifications}

Puoi abilitare le applicazioni iOS a inviare {{site.data.keyword.mobilepushshort}} ai tuoi dispositivi.


### Installazione di CocoaPods
{: #enable-push-ios-notifications-install}

Per un progetto Xcode esistente, puoi impostare il Bluemix Mobile services client SDK utilizzando lo strumento di gestione delle dipendenze CocoaPods. Un'alternativa consiste nell'installare l'SDK in modo manuale.

Per visualizzare il file readme Swift Push, vai a [Readme ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}.



1. Installa CocoaPods utilizzando il seguente comando nel tuo terminale Mac.
	```
		$ sudo gem install cocoapods
	```
	{: codeblock}
2. Immetti il comando `pod init` nel terminale per inizializzare CocoaPods. Assicurati di eseguire il comando dalla directory in cui si trova il progetto Xcode. Il comando `pod init` crea un Podfile.  
3. Nel Podfile generato, aggiungi le dipendenze SDK richieste. Copia il seguente Podfile.
   
	```
		source 'https://github.com/CocoaPods/Specs.git'
	// Copia il seguente elenco come è e rimuovi le dipendenze di cui non hai bisogno.
		use_frameworks!
		target 'MyApp' do
	    platform :ios, '8.0'
		pod 'BMSCore'
	    pod 'BMSPush'
      pod 'BMSAnalyticsAPI'
	end
	```
		{: codeblock}

3. Dal terminale, vai alla cartella del progetto e installa le dipendenze con il comando `pod update`.

Il comando installa le tue dipendenze e crea un nuovo spazio di lavoro Xcode.  
**Nota**: assicurati di aprire sempre il nuovo spazio di lavoro Xcode invece del file di progetto Xcode originale:
```
  $ open App.xcworkspace
```
	{: codeblock}

Lo spazio di lavoro contiene il tuo progetto originale e il progetto Pods che contiene le tue dipendenze. Per modificare una cartella di origine Bluemix mobile services, puoi trovarla nel tuo progetto Pods, in `Pods/yourImportedSourceFolder`, ad esempio: `Pods/BMSPush`.

### Aggiunta di framework utilizzando Carthage
{: #carthage}

Aggiungi i framework al tuo progetto utilizzando [Carthage ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}. Nota che Carthage in Xcode8 non è supportato.

1. Aggiungi i framework `BMSPush` al tuo Cartfile:
	```
	github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
	```
	{: codeblock}
2. Esegui il comando `carthage update`. Quando la build è stata completata, trascina `BMSPush.framework`, `BMSCore.framework` e `BMSAnalyticsAPI.framework` nel tuo progetto Xcode.
3. Segui le istruzioni sul sito di [Carthage ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window} per completare l'integrazione.

### Configurazione dell'SDK iOS
{: #ios-sdk}

Per configurare l'SDK iOS, aggiungi il seguente codice nel file **AppDelegate.swift** della tua applicazione. Nota che questo registra anche gli APNs.  
```
  func application(_ application: UIApplication,
didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {  
   BMSPushClient.sharedInstance.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE")
  }
```
    {: codeblock}

### Utilizzo dei framework importati e delle cartelle di origine
{: #using-imported-frameworks}

Fai riferimento all'SDK nel tuo codice. Assicurati che siano implementati i seguenti prerequisiti.

- iOS 8.0 o successiva	
- Xcode 7

Scrivi le direttive `#import` per le intestazioni
pertinenti, ad esempio:
```
	 //swift
import BMSCore
import BMSPush
```
		{: codeblock}

Per leggere il file readme Swift Push, vedi [Readme ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}.

**Nota**: aggiornare il tuo progetto Pods utilizzando i comandi CocoaPods `pod install` o `pod update` potrebbe sovrascrivere le cartelle di origine Bluemix Mobile services. Se vuoi conservare le tue versioni personalizzate dei file originali, assicurati che ne sia stato eseguito il backup prime di immettere uno di questi comandi.


### Impostazioni di creazione
{: #build-settings}

Vai a **Xcode > Build Settings > Build Options e imposta Enable Bitcode** su **No**.

**Attenzione**: a partire da iOS 9, le modifiche alla funzione ATS (App Transport Security) potrebbero influenzare il modo in cui gestisci il processo di autenticazione. I seguenti post del blog descrivono in maggiore dettaglio le modifiche: [ATS and Bitcode in iOS 9 ![Icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/){: new_window} e [Connect your iOS 9 app to Bluemix today ![Icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/){: new_window}.

### Inizializzazione di Push SDK per applicazioni iOS
{: #enable-push-ios-notifications-initialize}

Un posto comune dove inserire il codice di inizializzazione è nel delegato dell'applicazione per l'applicazione iOS. Fai clic sul link **Opzioni mobili** nel tuo dashboard Push per ottenere il GUID e la rotta dell'applicazione.

#### Inizializzazione dell'SDK Core
{: #Initializing-the-core-sdk}

Per inizializzare l'SDK Core per Swift con l'area, la rotta e la GUID IBM Bluemix, utilizza il seguente frammento di codice.
```
	let myBMSClient = BMSClient.sharedInstance
	myBMSClient.initialize(bluemixRegion: "Location where your app is hosted.") 
```
	{: codeblock}

#### Rotta, GUID e area Bluemix
{: #route-guid-bluemix-region}


- **appRoute**: specifica la rotta assegnata all'applicazione server creata in Bluemix.


- **GUID**: specifica la chiave univoca assegnata all'applicazione creata in Bluemix. Questo valore è
                sensibile al maiuscolo/minuscolo.


- **bluemixRegionSuffix**: specifica l'ubicazione in cui è ospitata l'applicazione. Il parametro `bluemixRegion` specifica quale distribuzione di Bluemix stati utilizzando. Puoi impostare questo valore con una proprietà statica `BMSClient.REGION` e utilizzare uno dei seguenti tre valori:

	- BMSClient.Region.usSouth 
	- BMSClient.Region.unitedKingdom
	- BMSClient.Region.sydney


- **AppGUID**: specifica la chiave AppGUID univoca assegnata al servizio {{site.data.keyword.mobilepushshort}} creato in Bluemix.

#### Inizializzazione del Push SDK client
{: #initializing-the-client-Push-SDK}

```
	let push = BMSPushClient.sharedInstance
	push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


### Registrazione di dispositivi ed applicazioni iOS
{: #enable-push-ios-notifications-register}

Un'applicazione deve essere registrata con il servizio APNS per ricevere le notifiche remote, dopo l'installazione su un dispositivo. Una volta che il token del dispositivo generato da APNS viene ricevuto dall'applicazione, questo deve essere trasmesso nuovamente al servizio {{site.data.keyword.mobilepushshort}}.

Per registrare le applicazioni e dispositivi iOS, devi:

1. Creare un'applicazione di backend.
2. Inviare il token a {{site.data.keyword.mobilepushshort}}.


#### Creazione di un'applicazione di backend
{: #create-a-backend-app}

Crea un'applicazione di backend nella sezione Contenitori tipo del catalogo Bluemix®, che esegue automaticamente il bind del servizio {{site.data.keyword.mobilepushshort}} a questa applicazione. Se già hai creato un'applicazione di backend, assicurati di eseguirne il bind al servizio {{site.data.keyword.mobilepushshort}}.


#### Trasmissione dei token a Push Notifications
{: #pass-token-push-notifications}

Dopo che il token viene ricevuto da APNs, passa il token a {{site.data.keyword.mobilepushshort}} come parte del metodo `registerWithDeviceToken`.

```
  func application (_application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data){
   let push =  BMSPushClient.sharedInstance
   push.registerWithDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
      if error.isEmpty {
           print( "Response during device registration : \(response)")
            print( "status code during device registration : \(statusCode)")
        }
       else{
            print( "Error during device registration \(error) ")
           print( "Error during device registration \n  - status code: \(statusCode) \n Error :\(error) \n")
        }
   }
  }
```
	{: codeblock}


### Ricezione di notifiche di push su dispositivi iOS
{: #enable-push-ios-notifications-receiving}

Per ricevere notifiche di push sui dispositivi ioS, aggiungi il seguente metodo Swift al delegato applicazione della tua applicazione.

```
   func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) 
  { //UserInfo dictionary will contain data sent from the server }
```
	{: codeblock}

### Monitoraggio di notifiche di push su dispositivi iOS
{: #ios-monitoring}


Puoi monitorare il numero e lo stato corrente delle notifiche di push che sono state inviate. Per abilitare il monitoraggio, aggiungi uno dei seguenti metodi Swift al delegato applicazione della tua applicazione in base all'evento.



- Invia lo stato della notifica quando l'applicazione viene aperta facendo clic sulla notifica.
	```
		func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any]) { 					let push =  BMSPushClient.sharedInstance
				let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 let data = respJson.data(using: String.Encoding.utf8)
				let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 let messageId:String = jsonResponse.value(forKey: "nid") as! String
		    	push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
    		  print("Send message status to the Push server")
    	 }
		}
	```
			{: codeblock}



- Invia lo stato della notifica quando l'applicazione è in modalità background.
	```
		func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
	 	let payLoad = ((((userInfo as NSDictionary).value(forKey: "aps") as! NSDictionary).value(forKey: "alert") as! NSDictionary).value(forKey: "body") as! NSString)
	 	 	let push =  BMSPushClient.sharedInstance
			let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 let data = respJson.data(using: String.Encoding.utf8)
	 	let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 let messageId:String = jsonResponse.value(forKey: "nid") as! String
		push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
       completionHandler(UIBackgroundFetchResult.newData)
	}
	}
	```
			{: codeblock}


### Invio di notifiche di push di base
{: #send}

Dopo che hai sviluppato le tue applicazioni, puoi inviare delle notifiche di push di base.

Per inviare notifiche push di base, completa la seguente procedura:

1. Seleziona **Send Notifications** e componi un messaggio scegliendo l'opzione **Send to**. Le opzioni supportate sono **Device by Tag**, **Device Id**, **User Id**, **Android devices**, **iOS devices**, **Web Notifications** e **All Devices**.  
**Nota**: quando selezioni l'opzione **All Devices**, tutti i dispositivi sottoscritti a {{site.data.keyword.mobilepushshort}} riceveranno le notifiche.
![Schermata notifiche](images/tag_notification.jpg)

2. Nel campo **Message**, componi il messaggio. Scegli di configurare le impostazioni facoltative come richiesto.
3. Fai clic su **Send**.
3. Verifica che i tuoi dispositivi abbiano ricevuto la tua notifica.

La seguente immagine mostra una casella di avviso che gestisce {{site.data.keyword.mobilepushshort}} su un dispositivo iOS.

![Notifica push in primo piano su iOS](images/iOS_Screenshot.jpg) 

#### Impostazioni facoltative per l'invio delle notifiche
{: #send_ios_otpional_setting}

Puoi anche personalizzare le impostazioni di {{site.data.keyword.mobilepushshort}} per inviare le notifiche ai dispositivi iOS. Sono supportate le seguenti opzioni di personalizzazione facoltative.

- **Badge**:  indica il numero che viene visualizzato nel badge dell'applicazione. Il valore predefinito è zero (0) e ciò significa che non sarà visualizzato un badge. 
- **Audio**: indica un file audio da riprodurre al ricevimento di un notifica. Supporta il valore predefinito o il nome della risorsa audio integrata nell'applicazione.
- **Payload addizionale**: specifica i valori di payload personalizzati per le tue notifiche.

### Abilitazione di notifiche interattive
{: #enb_snd_ios_otpional}

Puoi ora arricchire le tue notifiche iOS con maggiori dettagli, come l'aggiunta di un'immagine, una mappa o un pulsante di risposta, attraverso l'abilitazione di notifiche interattive. Ciò fornisce un maggiore contesto per i clienti, insieme alla capacità di agire immediatamente senza uscire dal contesto corrente.  

Per abilitare le notifiche interattive, utilizza il codice:



- Per definire l'azione del pulsante
	```
		let actionOne = BMSPushNotificationAction(identifierName: "ACCEPT", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
 let actionTwo = BMSPushNotificationAction(identifierName: "DECLINE", buttonTitle: "Decline", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
	```
		{: codeblock}


- Per definire la categoria per i pulsanti
	```
		let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
	```
		{: codeblock}


- Per aggiornare la registrazione per includere i pulsanti
	```
		Pass the defined category into iOS BMSPushClientOptions
		let notificationOptions = BMSPushClientOptions(categoryName: [category])
		let push = BMSPushClient.sharedInstance
		push.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE", options: notificationOptions)
	```
		{: codeblock}

Per inviare una notifica interattiva, completa la procedura:

1. Nella sezione Compose, dall'elenco a discesa Send To, seleziona **iOS Devices**.
2. Immetti il messaggio di notifica che vuoi inviare.
3. Nella sezione Optional Settings, seleziona **Mobile** e fai clic su **iOS**.
4. Nell'elenco a discesa Type, seleziona **Mixed**.
5. Nel campo Category, specifica il tipo di notifica che hai definito nella tua applicazione. 

![Notifica interattiva per iOS](images/push_ios_notification_interactive.jpg) 

#### Fasi successive
{: #next_steps_02}

Dopo che hai correttamente configurato le notifiche di base, puoi configurare le notifiche
        basate sulle tag e le opzioni avanzate.

Aggiungi queste funzioni del Servizio Push Notifications alla tua applicazione.
Per utilizzare le notifiche basate sulle tag, vedi [Notifiche basate sulle tag](c_tag_basednotifications.html).
Per utilizzare le opzioni di notifica avanzate, vedi [Abilitazione delle notifiche di push avanzate](t_advance_badge_sound_payload.html).
