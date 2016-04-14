---

copyright:
 years: 2015, 2016

---

# Installazione del Push SDK client con Gradle
{: #android_install}

Questa sezione descrive come installare e utilizzare il Push SDK client per sviluppare
    ulteriormente le tue applicazioni Android.

Il Push SDK dei servizi mobili Bluemix® può essere aggiunto utilizzando Gradle. Gradle
          scarica automaticamente le risorse dai repository e le rende disponibili alla tua applicazione Android. Assicurati di impostare correttamente
          Android Studio e Android Studio SDK. Per ulteriori informazioni su come impostare il tuo sistema, consulta la [panoramica di Android Studio](https://developer.android.com/tools/studio/index.html). Per informazioni su Gradle, consulta [Configuring Gradle Builds](http://developer.android.com/tools/building/configuring-gradle.html).

1. In Android Studio, dopo aver creato e aperto la tua applicazione mobile, apri il tuo file **build.gradle** dell'applicazione. Quindi aggiungi le seguenti dipendenze alla tua applicazione mobile. Queste istruzioni di importazione sono necessarie per i frammenti di codice elencati qui di seguito.

	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```


1. Aggiungi le seguenti dipendenze alla tua applicazione mobile. Le seguenti righe aggiungono l'SDK del client di push Bluemix™ Mobile Services e l'SDK dei servizi Google Play alle tue dipendenze dell'ambito di compilazione.

	```
	dependencies {
	  compile 'com.ibm.mobilefirstplatform.clientsdk.android:push:1.+'
	  compile 'com.google.android.gms:play-services:7.8.0'
	}  
	```
1. Nel file **AndroidManifest.xml**, aggiungi le seguenti autorizzazioni. Per visualizzare un manifest di esempio, consulta [Applicazione di esempio Android helloPush](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml). Per visualizzare un file Gradle di esempio, consulta [Sample Build Gradle file](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle).

	```
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="com.ibm.clientsdk.android.app.permission.C2D_MESSAGE" />
	<uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
	<uses-permission android:name="android.permission.WAKE_LOCK" />
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
	```

	Puoi leggere ulteriori informazioni sulle [autorizzazioni Android](http://developer.android.com/guide/topics/security/permissions.html) qui.

1. Aggiungi le impostazioni di intento di notifica per l'attività. Questa impostazione avvia l'applicazione
          quando l'utente fa clic sulla notifica ricevuta dall'area di notifica.

	```
	<intent-filter>  
		<action android:name="<Your_Android_Package_Name.IBMPushNotification"/>   
		<category  android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
	```
	**Nota**: sostituisci *Your_Android_Package_Name* nell'azione sopra indicata con il nome del pacchetto applicazione utilizzato nella tua applicazione.

1. Aggiungi il servizio di intento GCM (Google Cloud Messaging) e i filtri di intento per
          le notifiche di evento RECEIVE.

	```
	service android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushIntentService" />

	<receiver
	    android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.internal.MFPPushBroadcastReceiver"
	    android:permission="com.google.android.c2dm.permission.SEND">
	    <intent-filter>
	        <action android:name="com.google.android.c2dm.intent.RECEIVE" />

	        <category android:name="com.ibm.mobilefirstplatform.clientsdk.android.app" />
	    </intent-filter>
	    <intent-filter>
	        <action android:name="android.intent.action.BOOT_COMPLETED" />

	        <category android:name="com.ibm.mobilefirstplatform.clientsdk.android.app" />
	    </intent-filter>
	</receiver>
	```
