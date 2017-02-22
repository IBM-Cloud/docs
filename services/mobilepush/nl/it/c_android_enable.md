---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Abilitazione delle applicazioni Android alla ricezione di {{site.data.keyword.mobilepushshort}}
{: #tag_based_notifications}
Ultimo aggiornamento: 16 gennaio 2017
{: .last-updated}

Puoi abilitare le applicazioni Android a ricevere le notifiche di push ai tuoi dispositivi. Android Studio è un prerequisito ed è il metodo raccomandato per creare progetti Android. Una conoscenza di base di Android Studio è essenziale.

## Installazione del Push SDK client con Gradle
{: #android_install}

Questa sezione descrive come installare e utilizzare il Push SDK client per sviluppare
    ulteriormente le tue applicazioni Android.

Il Push SDK dei servizi mobili Bluemix® può essere aggiunto utilizzando Gradle. Gradle
          scarica automaticamente le risorse dai repository e le rende disponibili alla tua applicazione Android. Assicurati di impostare correttamente Android Studio e Android Studio SDK. Per ulteriori informazioni su come impostare il tuo sistema, consulta la [Panoramica di Android Studio ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.android.com/tools/studio/index.html "Icona link esterno"){: new_window}. Per informazioni su Gradle, vedi [Configuring Gradle Builds ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://developer.android.com/tools/building/configuring-gradle.html "Icona link esterno"){: new_window}.

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
    classpath 'com.android.tools.build:gradle:3.0.0'
    classpath 'com.google.gms:google-services:3.0.0'
}
``` 
    {: codeblock}
5. Nel file **AndroidManifest.xml**, aggiungi le seguenti autorizzazioni. Per visualizzare un manifest di esempio, vedi [Applicazione di esempio helloPush Android ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml "Icona link esterno"){: new_window}. Per visualizzare un file Gradle di esempio, vedi [File Build Gradle di esempio ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle "Icona link esterno"){: new_window}.
```
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.GET_ACCOUNTS" />
<uses-permission android:name="android.permission.USE_CREDENTIALS" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
```
	{: codeblock}
 Leggi ulteriori informazioni sulle [Autorizzazioni Android ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://developer.android.com/guide/topics/security/permissions.html "Icona link esterno"){: new_window} qui.

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

Per configurare il progetto FCM e ottenere le tue credenziali, consulta [Come ottenere il tuo ID mittente e la chiave API](t_push_provider_android.html). Completa la seguente procedura utilizzando la console FCM (Firebase Cloud Messaging).

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

## Inizializzazione di Push SDK per applicazioni Android
{: #android_initialize}

Un posto comune dove inserire il codice di inizializzazione è nel metodo onCreate dell'attività principale nella tua applicazione Android. Esistono due componenti per la SDK che deve essere inizializzata. Uno è la SDK core e l'altro è la SDK push creata all'inizio della SDK core.

###Inizializza il Core SDK

```
// Inizializza l'SDK per Android
    BMSClient.getInstance().initialize(this, BMSClient.REGION_US_SOUTH);
```
    {: codeblock}

####bluemixRegionSuffix
{: bluemixRegionSuffix}

Specifica l'ubicazione in cui è ospitata l'applicazione. Puoi utilizzare uno dei seguenti tre valori:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

###Inizializza il Push SDK client

```
//Inizializza il Push SDK for Java client
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext(), "appGUID", "clientSecret");
```
	{: codeblock}

####AppGUID
{: appguid_initialize_client_push_sdk}

Questa è la chiave AppGUID del servizio {{site.data.keyword.mobilepushshort}}. Questo valore è
                sensibile al maiuscolo/minuscolo. Apri il dashboard Push Notification e seleziona la scheda di configurazione. Puoi ottenere questo valore dalle opzioni mobili nella scheda di configurazione del dashboard del servizio Push Notification. 

## Registrazione di dispositivi Android
{: #android_register}

Utilizza l'API `MFPPush.register()` per registrare il dispositivo con il servizio {{site.data.keyword.mobilepushshort}}. Per registrare le periferiche Android, devi aggiungere le informazioni FCM (Firebase Cloud Messaging) o GCM (Google Cloud Messaging) nel dashboard di configurazione del servizio {{site.data.keyword.mobilepushshort}}. Per ulteriori informazioni, consulta [Configurazione delle credenziali per GCM (Google Cloud Messaging)](t_push_provider_android.html).

Copia i seguenti frammenti di codice nella tua applicazione mobile Android.

```
//Registra dispositivi Android
	push.registerDevice(new MFPPushResponseListener<String>() {
    @Override
	    public void onSuccess(String deviceId) {
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

## Ricezione di notifiche di push su dispositivi Android
{: #android_receive}

Per registrare l'oggetto  notificationListener con push, richiama il metodo **MFPPush.listen()**. Questo metodo viene di norma
                            richiamato dal metodo ** onResume() **dell'attività che
                            sta gestendo le notifiche di push.

1. Per registrare l'oggetto  notificationListener con push, richiama il metodo **listen()**. Questo metodo viene di norma richiamato dai metodi **onResume()** e **onPause** dell'attività che sta gestendo le notifiche di push.


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

2. Crea il progetto ed eseguilo sul dispositivo o sull'emulatore. Quando viene richiamato il metodo onSuccess() per il listener di risposte nel metodo register(), ricevi una conferma che il dispositivo ha eseguito correttamente la registrazione con il servizio {{site.data.keyword.mobilepushshort}}. In questo momento puoi inviare un messaggio come descritto in Invio di notifiche di push di base.
3. Verifica che i tuoi dispositivi abbiano ricevuto la tua notifica. Se l'applicazione è in
            primo piano, la notifica viene gestita da **MFPPushNotificationListener**. Se l'applicazione è in background, viene visualizzato un messaggio nella barra di notifica.

## Monitoraggio di notifiche di push su dispositivi Android
{: #android_monitor}

Per monitorare lo stato corrente della notifica all'interno dell'applicazione, puoi implementare l'interfaccia `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener` e definire il metodo onStatusChange(String messageId, MFPPushNotificationStatus status). 

Il **messageId** è l'identificativo del messaggio inviato dal server.  **MFPPushNotificationStatus** definisce lo stato delle notifiche come valori:

- **RECEIVED** - L'applicazione ha ricevuto la notifica. 
- **QUEUED** - L'applicazione mette in coda la notifica per richiamare il listener delle notifiche. 
- **OPENED** - L'utente apre la notifica selezionandola dalla barra o avviandola dall'icona dell'applicazione oppure quando l'applicazione è in primo piano. 
- **DISMISSED** - L'utente cancella/ignora la notifica nella barra.

Devi registrare la classe **com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener** con MFPPush.

```
push.setNotificationStatusListener(new MFPPushNotificationStatusListener() {
@Override
public void onStatusChange(String messageId, MFPPushNotificationStatus status) {
// Handle status change
}
});
```
    {: codeblock}


### In ascolto dello stato DISMISSED

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

Devi estendere il ricevitore di trasmissione  **com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler** e sovrascrivere il metodo **onReceive()**, dove **MFPPushNotificationStatusListener** deve essere registrato prima di richiamare il metodo  **onReceive()** della classe di base.

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

## Invio di {{site.data.keyword.mobilepushshort}} di base
{: #send}

Dopo che hai sviluppato le tue applicazioni, puoi inviare delle notifiche di push di base.

Per inviare notifiche push di base, completa la seguente procedura:

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

Puoi anche personalizzare le impostazioni di {{site.data.keyword.mobilepushshort}} per inviare le notifiche ai dispositivi Android. Sono supportate le seguenti opzioni di personalizzazione facoltative.
![Impostazioni personalizzate Android](images/android_custom_settings.jpg)

- **Chiave di compressione**:  le chiavi di compressione solo allegate alle notifiche. Se più notifiche arrivano in sequenza con la stessa chiave di compressione quando il dispositivo è offline, esse vengono compresse. Quando un dispositivo va online, riceve le notifiche dal server FCM/GCM e visualizza solo l'ultima notifica rilevando la stessa chiave di compressione. Se la chiave di compressione non viene inviata, sia il nuovo che il vecchio messaggio vengono archiviati per una consegna successiva.
- **Audio**: indica un file audio da riprodurre al ricevimento di un notifica. Supporta il valore predefinito o il nome della risorsa audio integrata nell'applicazione.
- **Icona**: specifica il nome dell'icona da visualizzare per la notifica. Assicurati di aver fornito l'icona nella cartella res/drawable, con l'applicazione client.
- **Priorità**: specifica le opzioni per l'assegnazione della priorità di consegna dei messaggi. Una priorità `high` o `max` creerà una notifica di avviso, mentre i messaggi di priorità `low` o `default` non apriranno le connessioni di rete in un dispositivo silenzioso. Per i messaggi con l'opzione impostata su `min`, sarà inviata una notifica silenziosa.
- **Visibilità**: puoi scegliere di impostare l'opzione di visibilità della notifica su `public` o `private`. L'opzione `private` limita la visualizzazione pubblica e puoi scegliere di abilitarla se il tuo dispositivo è protetto da un pattern o un pin e le impostazioni di notifica vengono impostate su "Hide sensitive notification content". Quando la visibilità è impostata su `private`, deve essere menzionato un campo "redact". Solo il contenuto specificato nel campo redact sarà mostrato nella schermata di blocco sul dispositivo. Scegliendo `public` sarà possibile leggere le notifiche liberamente.
- **TTL (Time to live)**: questo valore è impostato in secondi. Se questo parametro non viene specificato, il server FCM/GCM archivia il messaggio per quattro settimane e tenterà di consegnarlo. La validità scade dopo quattro settimane. L'intervallo di valori possibile è compreso tra 0 e 2,419,200 secondi.
- **Ritarda quando inattivo**: impostando questo valore su `true` si danno istruzioni al server FCM/GCM di non consegnare la notifica se il dispositivo è inattivo. Imposta questo valore su `false`, per assicurati di consegnare la notifica anche se il dispositivo è inattivo.
- **Sincronizzazione**: impostando questo valore su `true`, le notifiche vengono sincronizzate in tutti i tuoi dispositivi registrati. Se l'utente con un nome utente dispone di più dispositivi con la stessa applicazione installata, la lettura della notifica su un dispositivo assicura l'eliminazione delle notifiche negli altri dispositivi. Devi assicurarti di essere registrato con il servizio {{site.data.keyword.mobilepushshort}} con l'ID utente per questa opzione perché funzioni.
- **Payload addizionale**: specifica i valori di payload personalizzati per le tue notifiche.


## Fasi successive
{: #next_steps_tags}

Dopo che hai correttamente configurato le notifiche di base, puoi configurare le notifiche
        basate sulle tag e le opzioni avanzate.

Aggiungi queste funzioni del servizio push notifications alla tua applicazione.
Per utilizzare le notifiche basate sulle tag, vedi [Notifiche basate sulle tag](c_tag_basednotifications.html).
Per utilizzare le opzioni di notifica avanzate, vedi [Abilitazione delle notifiche di push avanzate](t_advance_badge_sound_payload.html).
