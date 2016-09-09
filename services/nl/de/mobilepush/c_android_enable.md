    ---

copyright:
 years: 2015 2016

---


# Android-Anwendungen für den Empfang von Push-Benachrichtigungen aktivieren
{: #tag_based_notifications}
Letzte Aktualisierung: 16. August 2016
{: .last-updated}

Aktivieren Sie Android-Anwendungen für den Empfang von Push-Benachrichtigungen und für das Senden von Push-Benachrichtigungen an Ihre Geräte. 

## Client-Push-SDK mit Gradle installieren
{: #android_install}

In diesem Abschnitt wird die Vorgehensweise zum Installieren und Verwenden des Client-Push-SDK für die weitere Entwicklung Ihrer Android-Anwendungen beschrieben.

Das Push-SDK für mobile Bluemix®-Services kann mithilfe von Gradle hinzugefügt werden. Gradle lädt automatisch Artefakte aus Repositorys herunter und stellt Sie in Ihrer Android-Anwendung zur Verfügung. Stellen Sie sicher, dass Sie Android Studio und das Android Studio-SDK ordnungsgemäß einrichten. Weitere Informationen zum Einrichten Ihres Systems finden Sie unter [Android Studio Overview](https://developer.android.com/tools/studio/index.html). Informationen zu Gradle finden Sie in [Configuring Gradle Builds](http://developer.android.com/tools/building/configuring-gradle.html).

1. Öffnen Sie in Android Studio nach dem Erstellen und Öffnen der mobilen Anwendung die Anwendungsdatei **build.gradle**. 
2. Fügen Sie die folgenden Abhängigkeiten zu Ihrer mobilen Anwendung hinzu. Die folgenden Importanweisungen sind für Code-Snippets erforderlich: 

	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```


2. Fügen Sie die folgenden Abhängigkeiten zu Ihrer mobilen Anwendung hinzu. Mit den folgenden Zeilen wird das Push-Client-SDK der Bluemix™ Mobile-Services und das Google Play Services-SDK zu Ihren Abhängigkeiten für den Kompilierungsbereich hinzugefügt. 

	```
	dependencies {
	  compile group: 'com.ibm.mobilefirstplatform.clientsdk.android', 
		name: 'push', 
		version: '2.+',
		ext: 'aar', 
		transitive: true
	}  
	```
3. Fügen Sie die folgenden Berechtigungen in der Datei **AndroidManifest.xml** hinzu. Ein Beispielmanifest
finden Sie in [Android helloPush Sample Application](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml). Eine Gradle-Beispieldatei finden Sie unter [Sample Build Gradle file](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle).

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
   Weitere Informationen zu [Android-Berechtigungen](http://developer.android.com/guide/topics/security/permissions.html) finden Sie hier.
4. Fügen Sie die Einstellungen für die Benachrichtigungsabsicht für die Aktivität hinzu. Mit dieser Einstellung wird die Anwendung gestartet, wenn der Benutzer im Benachrichtigungsbereich auf die empfangene Benachrichtigung klickt.

	```
	<intent-filter>
		<action android:name="<ihr_android-paketname.IBMPushNotification"/>
		<category  android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
	```
	**Hinweis**: Ersetzen Sie in der obigen Aktion *ihr_android-paketname* durch den Namen des Anwendungspakets, der in Ihrer Anwendung verwendet wird.
5. Fügen Sie den Absichtsservice und Absichtsfilter von Google Cloud Messaging (GCM) für die Ereignisbenachrichtigungen des Typs RECEIVE hinzu.

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


## Push-SDK für Android-Apps initialisieren
{: #android_initialize}

Die Methode 'onCreate' der Hauptaktivität in Ihrer Android-Anwendung ist eine übliche Position für den Initialisierungscode.

Um Ihre App-Route und App-GUID zu beziehen, wählen Sie im Navigationsbereich für Ihre initialisierten Push-Services die Option 'Konfiguration' aus und klicken Sie auf **Mobile Systemerweiterungen**. Verwenden Sie diese Werte für Ihre Route und App-GUID. Ändern Sie das Code-Snippet so, dass die Parameter 'appRoute' und 'appGUID' der Bluemix-App verwendet werden.


###Core-SDK initialisieren

```
// Initialize the SDK for Java (Android) with IBM Bluemix AppGUID and route
BMSClient.getInstance().initialize(getApplicationContext(), appRoute , appGuid, bluemixRegionSuffix);

```


####appRoute
{: approute}

Gibt die Route an, die der Serveranwendung zugewiesen ist, die Sie in Bluemix erstellt haben.

####AppGUID
{: appguid}

Gibt den eindeutigen Schlüssel an, der der Instanz des Service für {{site.data.keyword.mobilepushshort}} auf Bluemix zugewiesen ist. Bei diesem Wert muss die Groß-/Kleinschreibung beachtet werden. Diesen Wert können Sie im Push-Dashboard über 'Mobile Systemerweiterungen' abrufen. 

####bluemixRegionSuffix
{: bluemixRegionSuffix}

Gibt den Standort an, an dem die App gehostet ist. Sie können einen der folgenden drei Werte verwendet: 

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

###Client-Push-SDK initialisieren

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext(), "AppGUID");
```
####AppGUID
{: AppGUID}

Dies ist der 'AppGUID'-Schlüssel des {{site.data.keyword.mobilepushshort}}-Service. 

## Android-Geräte registrieren
{: #android_register}

Verwenden Sie die API `MFPPush.register()`, um das Gerät beim {{site.data.keyword.mobilepushshort}}-Service zu registrieren. Für die Registrierung bei Android-Geräten müssen Sie zunächst die GCM-Angaben (Google Cloud Messaging) im Bluemix-Dashboard für die Konfiguration des {{site.data.keyword.mobilepushshort}}-Service hinzufügen. Weitere Informationen finden Sie im Abschnitt zur [Konfiguration von Berechtigungsnachweisen für Google Cloud Messaging](t_push_provider_android.html).

Kopieren Sie die folgenden Code-Snippets und fügen Sie sie in Ihre mobile Android-Anwendung ein.

```
	//Register Android devices
	push.registerDevice(new MFPPushResponseListener<String>() {
	    @Override
	    public void onSuccess(String deviceId) {
	           //handle success here
	    }
	    @Override
	    public void onFailure(MFPPushException ex) {
	    //handle failure here
	    }
	});
```

```
	//Handles the notification when it arrives
	MFPPushNotificationListener notificationListener = new MFPPushNotificationListener() {
	    @Override
	    public void onReceive (final MFPSimplePushNotification message){
	      // Handle Push Notification
	    }
	};
```


## Push-Benachrichtigungen in Android-Geräten empfangen
{: #android_receive}

Rufen Sie die Methode **MFPPush.listen()** auf, um das Objekt 'notificationListener' für den Push-Service zu registrieren. Diese Methode wird in der Regel über die Methode **onResume()** der Aktivität aufgerufen, die Push-Benachrichtigungen verarbeitet.

1. Rufen Sie die Methode **listen()** auf, um das Objekt 'notificationListener' für den Push-Service zu registrieren. Diese Methode wird in der Regel über die Methode **onResume()** der Aktivität aufgerufen, die Push-Benachrichtigungen verarbeitet.

	```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
	       push.listen(notificationListener);
	   }
	}
  ```
2. Erstellen Sie einen Build für das Projekt und führen Sie ihn in dem Gerät oder im Emulator aus. Wenn die Methode onSuccess() für den Antwortlistener in der Methode register() aufgerufen wird, wird bestätigt, dass das Gerät erfolgreich für den {{site.data.keyword.mobilepushshort}}-Service registriert wurde. An diesem Punkt können Sie gemäß der in 'Einfache Push-Benachrichtigungen senden' beschriebenen Anleitung eine Nachricht senden.
3. Überprüfen Sie, ob die Geräte Ihre Benachrichtigung empfangen haben. Wenn die Anwendung im Vordergrund ausgeführt wird, wird die Benachrichtigung von **MFPPushNotificationListener** verarbeitet. Wenn die Anwendung im Hintergrund ausgeführt wird, wird eine Nachricht in der Benachrichtigungsleiste angezeigt.


## Einfache Push-Benachrichtigungen senden 
{: #send}

Nach dem Entwickeln Ihrer Anwendungen können Sie einfache Push-Benachrichtigungen (ohne Tags, Badges, zusätzliche Nutzdaten oder Audiodateien) senden.

1. Wählen Sie unter **Zielgruppe auswählen** eine der folgenden Zielgruppen aus:
**Alle Geräte** oder die Plattform **Nur iOS-Geräte** oder
**Nur Android-Geräte**. 

	**Hinweis**: Wenn Sie die Option **Alle Geräte** auswählen, erhalten alle Geräte, die Push-Benachrichtigungen subskribiert haben, Benachrichtigungen. 

![Anzeige 'Benachrichtigungen'](images/tag_notification.jpg)

2. Geben Sie in **Eigene Benachrichtigung erstellen** die gewünschte Nachricht ein und klicken Sie auf **Senden**.
3. Überprüfen Sie, ob die Geräte Ihre Benachrichtigung empfangen haben. Der folgende Screenshot zeigt ein Alertfeld bei der Verarbeitung einer Push-Benachrichtigung
im Vordergrund auf einem Android-Gerät.

![Push-Benachrichtigung im Vordergrund auf einem Android-Gerät](images/Android_Screenshot.jpg)

Der folgende Screenshot zeigt eine Push-Benachrichtigung im Hintergrund auf einem Android-Gerät.

![Push-Benachrichtigung im Hintergrund auf einem Android-Gerät](images/background.jpg)



## Nächste Schritte
{: #next_steps_tags}

Nachdem Sie einfache Benachrichtigungen erfolgreich eingerichtet haben, können Sie tagbasierte
Benachrichtigungen und erweiterte Optionen konfigurieren.

Fügen Sie die folgenden Funktionen des Push-Benachrichtigungsservice zu Ihrer App hinzu.
Informationen zur Verwendung tagbasierter Benachrichtigungen finden Sie in [Tagbasierte Benachrichtigungen](c_tag_basednotifications.html).
Informationen zur Verwendung erweiterter Benachrichtigungen finden Sie in [Erweiterte Push-Benachrichtigungen](t_advance_notifications.html).
