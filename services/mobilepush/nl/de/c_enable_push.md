---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Benachrichtigungen für mobile Geräte aktivieren
{: #c_enable_push-notifications}
Letzte Aktualisierung: 12. April 2017
{: .last-updated}

Stellen Sie sicher, dass die im Abschnitt [Berechtigungsnachweise für einen Benachrichtigungsprovider konfigurieren](t__main_push_config_provider.html) angegebenen Schritte durchgeführt wurden.

In diesem Abschnitt wird beschrieben, wie Sie Ihre Clientanwendungen - mobile oder Web-Browser-Anwendungen und auch Chrome-Apps und Erweiterungen - für den Empfang von Push-Benachrichtigungen aktivieren, wie Sie grundlegende Benachrichtigungen erstellen, wie Sie das SDK oder Plug-in abrufen und initialisieren und wie Sie Ihr Gerät oder Ihren Browser für den Empfang von Push-Benachrichtigungen registrieren. Sie können auch die [REST-API](t_restapi.html) verwenden, um Ihre mobilen Anwendungen und Web-Browser-Anwendungen für den Empfang von Push-Benachrichtigungen zu aktivieren.

**Hinweis**: Für Registrierungen von Geräten, Browsern, Chrome-Apps und Erweiterungen pflegt der {{site.data.keyword.mobilepushshort}}-Service eine eindeutige Referenz auf Tokens, die von Benachrichtigungsprovidern ausgegeben werden
(APNs für Apple bzw. FCM für Google). Der Benachrichtigungsprovider des {{site.data.keyword.mobilepushshort}}-Service kann diese Tokens aus diversen Gründen inaktivieren. 

Ein Beispiel wäre die Inaktivierung bei der Deinstallation einer App auf dem Gerät. Bei einem Szenario, bei dem der Versuch unternommen wird, eine Benachrichtigung auf Grundlage der Providerantwort über die Inaktivierung des Geräts zuzustellen, entfernt der {{site.data.keyword.mobilepushshort}}-Service die Geräte- oder Web-Browserregistrierungen. Dadurch werden wiederum nachfolgende Versuche, die Benachrichtigung an diese inaktivierten Geräte zu senden, blockiert.


## Android-Anwendungen für den Empfang von Push-Benachrichtigungen aktivieren
{: #tag_based_notifications}


Sie können Android-Anwendungen für den Empfang von Push-Benachrichtigungen auf Ihren Geräten aktivieren. Android Studio ist dafür Voraussetzung und auch die empfohlene Methode für die Erstellung von Android-Projekten. Grundlegende Kenntnisse von Android Studio sind erforderlich.

### Client-Push-SDK mit Gradle installieren
{: #android_install}

In diesem Abschnitt wird die Vorgehensweise zum Installieren und Verwenden des Client-Push-SDK für die weitere Entwicklung Ihrer Android-Anwendungen beschrieben.

Das Push-SDK für {{site.data.keyword.Bluemix}} Mobile Services kann mithilfe von [Gradle ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://developer.android.com/tools/building/configuring-gradle.html){: new_window} hinzugefügt werden. Gradle lädt automatisch Artefakte aus Repositorys herunter und stellt sie in Ihrer Android-Anwendung zur Verfügung. Stellen Sie sicher, dass Sie [Android Studio ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.android.com/tools/studio/index.html) und das Android Studio-SDK korrekt einrichten. 

Führen Sie nach der Erstellung und Öffnung Ihrer mobilen Anwendung mithilfe von Android Studio die folgenden Schritte aus.

1. Fügen Sie Abhängigkeiten zu Ihrer Modulebenendatei **build.gradle** hinzu. 	

	- Fügen Sie die folgende Abhängigkeit hinzu, um das Push-Client-SDK von Bluemix™ Mobile Services und das Google Play Services-SDK zu Ihren Abhängigkeiten für den Kompilierungsbereich hinzuzufügen.
	```
	com.ibm.mobilefirstplatform.clientsdk.android:push:3.+
	```
    	{: codeblock}
	
	- Fügen Sie die folgenden Abhängigkeiten zu Importanweisungen hinzu, die für Codeausschnitte erforderlich sind.
	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```
    	{: codeblock}

	- Fügen Sie die folgende Abhängigkeit am Ende Ihrer Modulebenendatei **build.gradle** hinzu.
	```
		apply plugin: 'com.google.gms.google-services'
	```
		{: codeblock}
3. Fügen Sie die folgenden Abhängigkeiten zu Ihrer Projektebenendatei **build.gradle** hinzu.
```
dependencies {
    classpath 'com.android.tools.build:gradle:2.2.3'
    classpath 'com.google.gms:google-services:3.0.0'
}
``` 
    {: codeblock}
5. Fügen Sie die folgenden Berechtigungen in der Datei **AndroidManifest.xml** hinzu. Informationen zum Anzeigen eines Beispielmanifests finden Sie bei der [Android-Beispielanwendung 'helloPush' ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml){: new_window}. Eine Gradle-Beispieldatei finden Sie bei der [Beispieldatei für Gradle-Build ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle){: new_window}.
```
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
```
	{: codeblock}
 Weitere Informationen zu [Android-Berechtigungen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://developer.android.com/guide/topics/security/permissions.html){: new_window} finden Sie hier.

4. Fügen Sie die Einstellungen für die Benachrichtigungsabsicht für die Aktivität hinzu. Mit dieser Einstellung wird die Anwendung gestartet, wenn der Benutzer im Benachrichtigungsbereich auf die empfangene Benachrichtigung klickt.
```
	<intent-filter>
	<action android:name="Your_Android_Package_Name.IBMPushNotification"/>
	<category  android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
```
	{: codeblock}
**Hinweis**: Ersetzen Sie in der obigen Aktion *Your_Android_Package_Name* durch den Namen des Anwendungspakets, der in Ihrer Anwendung verwendet wird.

5. Fügen Sie den Absichtsservice und die Absichtsfilter von Firebase Cloud Messaging (FCM) bzw. Google Cloud Messaging (GCM) für Ereignisbenachrichtigungen des Typs RECEIVE und REGISTRATION hinzu.
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

6. Der {{site.data.keyword.mobilepushshort}}-Service unterstützt den Abruf von Einzelbenachrichtigungen aus dem Benachrichtigungsfach. Für Benachrichtigungen, auf die über das Benachrichtigungsfach zugegriffen wird, wird Ihnen ein Handle nur für die Benachrichtigung bereitgestellt, auf die geklickt wird. Wenn die Anwendung auf normale Weise geöffnet wird, werden alle Benachrichtigungen angezeigt. Aktualisieren Sie Ihre Datei **AndroidManifest.xml** mit dem folgenden Snippet, um diese Funktion zu nutzen:

```
	<activity android:name="
com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationHandler"
android:theme="@android:style/Theme.NoDisplay"/>
```
    {: codeblock}

Stellen Sie sicher, dass die im Abschnitt [Berechtigungsnachweise für einen Benachrichtigungsprovider konfigurieren](t__main_push_config_provider.html) angegebenen Schritte durchgeführt wurden, um das FCM-Projekt einzurichten und die Berechtigungsnachweise abzurufen. Führen Sie die folgenden Schritte mit der FCM-Konsole (Firebase Cloud Messaging) aus.

1. Klicken Sie in der Firebase-Konsole auf das Symbol für die **Projekteinstellungen**.
    ![Firebase-Projekteinstellungen](images/FCM_4.jpg)

3. Wählen Sie auf der Registerkarte 'Allgemein' im Fenster mit Ihren Apps die Option **ADD APP** oder **Add Firebase to your Android app** aus.
    ![Firebase zu Android hinzufügen](images/FCM_5.jpg)

4. Fügen Sie im Fenster 'Add Firebase to your Android app' **com.ibm.mobilefirstplatform.clientsdk.android.push** als Paketnamen hinzu. Das Feld 'App nickname' ist optional. Klicken Sie auf **ADD APP**. 
    ![Fenster 'Adding Firebase to your Android app'](images/FCM_1.jpg)

5. Geben Sie den Paketnamen Ihrer Anwendung an, indem Sie ihn im Fenster 'Add Firebase to your Android app' eingeben. Das Feld 'App nickname' ist optional. Klicken Sie auf **ADD APP**. 

	![Paketnamen Ihrer Anwendung hinzufügen](images/FCM_2.jpg)

6. Die Datei `google-services.json` wird generiert. Kopieren Sie die Datei `google-services.json` in das Stammverzeichnis Ihres Android-Anwendungsmoduls. Beachten Sie, dass die Datei `google-service.json` die hinzugefügten Paketnamen enthält.

    ![JSON-Datei zum Stammverzeichnis Ihrer Anwendung hinzufügen](images/FCM_7.jpg)

5. Klicken Sie im Fenster 'Add Firebase to your Android app' auf **Continue** und dann auf **Finish**. 

  

Bauen Sie Ihre Anwendung auf und führen Sie sie aus.

### Push-SDK für Android-Apps initialisieren
{: #android_initialize}

Die Methode 'onCreate' der Hauptaktivität in Ihrer Android-Anwendung ist eine übliche Position für den Initialisierungscode. Zwei Komponenten des SDK müssen initialisiert werden. Eine ist das Core-SDK, die andere ist das Push-SDK, das auf dem Core-SDK aufgebaut ist.

#### Core-SDK initialisieren
{: #initz_core_sdk}

```
// SDK für Android initialisieren
    BMSClient.getInstance().initialize(this, BMSClient.REGION_US_SOUTH);
```
    {: codeblock}

#### bluemixRegionSuffix
{: #bluemixRegionSuffix}

Gibt den Standort an, an dem die App gehostet ist. Sie können einen der folgenden drei Werte verwendet:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

#### Client-Push-SDK initialisieren
{: #initiz_client_pushSDK}

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext(), "appGUID", "clientSecret");
```
	{: codeblock}

#### AppGUID
{: #appguid_initialize_client_push_sdk}

Dies ist der 'AppGUID'-Schlüssel des {{site.data.keyword.mobilepushshort}}-Service. Bei diesem Wert muss die Groß-/Kleinschreibung beachtet werden. Öffnen Sie das Push Notification-Dashboard und wählen Sie die Registerkarte 'Konfigurieren' aus. Diesen Wert können Sie im Dashboard des Push Notifications-Service in der Registerkarte 'Konfigurieren' über 'Mobile Systemerweiterungen' abrufen. 

### Android-Geräte registrieren
{: #android_register}

Verwenden Sie die API `MFPPush.register()`, um das Gerät beim {{site.data.keyword.mobilepushshort}}-Service zu registrieren. Für die Registrierung bei Android-Geräten müssen Sie die FCM-Informationen (Firebase Cloud Messaging) im Bluemix-Dashboard für die Konfiguration des {{site.data.keyword.mobilepushshort}}-Service hinzufügen. Weitere Informationen finden Sie in [Berechtigungsnachweise für einen Benachrichtigungsprovider konfigurieren](t__main_push_config_provider.html). 

Kopieren Sie die folgenden Code-Snippets in Ihre mobile Android-Anwendung.

```
	//Register Android devices
	push.registerDevice(new MFPPushResponseListener<String>() {
    	@Override
    	public void onSuccess(String response) {
    		//handle success here
	    }
		@Override
    public void onFailure(MFPPushException ex) {
    		//handle failure here
	    }
		});
```
	{: codeblock}


```
	//Handles the notification when it arrives
	MFPPushNotificationListener notificationListener = new MFPPushNotificationListener() {
    @Override
	    public void onReceive (final MFPSimplePushNotification message){
	      // Push Notification ausführen
	    }
		};
```
	{: codeblock}

### Push-Benachrichtigungen in Android-Geräten empfangen
{: #android_receive}

1. Verwenden Sie die Methode `MFPPush.listen()`, um das Objekt 'notificationListener' für den Push Notifications-Service zu registrieren. Diese Methode wird in der Regel über die Methoden `onResume()` und `onPause` der Aktivität aufgerufen, die Push-Benachrichtigungen verarbeitet.
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

2. Erstellen Sie einen Build für das Projekt und führen Sie ihn in dem Gerät oder im Emulator aus. Wenn die Methode onSuccess() für den Antwortlistener in der Methode register() aufgerufen wird, wird bestätigt, dass das Gerät erfolgreich für den {{site.data.keyword.mobilepushshort}}-Service registriert wurde, und Sie können nun eine Push-Benachrichtigung senden. 
3. Überprüfen Sie, ob die Geräte Ihre Benachrichtigung empfangen haben. Wenn die Anwendung im Vordergrund ausgeführt wird, wird die Benachrichtigung von `MFPPushNotificationListener` verarbeitet. Wenn die Anwendung im Hintergrund ausgeführt wird, wird eine Nachricht in der Benachrichtigungsleiste angezeigt.

### Push-Benachrichtigungen in Android-Geräten überwachen
{: #android_monitor}

Wenn Sie den aktuellen Status der Benachrichtigung innerhalb der Anwendung überwachen möchten, können Sie die Schnittstelle `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener` implementieren und die Methode onStatusChange(String messageId, MFPPushNotificationStatus status) definieren. 

Die `messageId` ist die Kennung der vom Server gesendeten Nachricht.  `MFPPushNotificationStatus` definiert den Status der Benachrichtigungen als Werte:

- RECEIVED - Die App hat die Benachrichtigung empfangen. 
- QUEUED - Die App hat die Benachrichtigung in die Warteschlange gestellt, um den Listener für Benachrichtigungen aufzurufen. 
- OPENED - Der Benutzer öffnet die Benachrichtigung, indem er im Fach auf die Benachrichtigung klickt oder indem er sie über das App-Symbol startet oder wenn sich die App im Vordergrund befindet. 
- DISMISSED - Der Benutzer löscht/verwirft die Benachrichtigung im Fach.

Sie müssen die Klasse `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener` für MFPPush registrieren.

```
	push.setNotificationStatusListener(new MFPPushNotificationStatusListener() {
	@Override
public void onStatusChange(String messageId, MFPPushNotificationStatus status) {
		// Handle status change
}
	});
```
    {: codeblock}


#### Empfangsbereitschaft für Status DISMISSED
{: #android_monitor_listen}

Sie können für den Status DISMISSED unter jeder der folgenden Bedingungen empfangsbereit sein:

- Wenn die App aktiv ist (im Vordergrund oder Hintergrund ausgeführt wird)

  Fügen Sie das Snippet Ihrer Datei `AndroidManifest.xml` hinzu:

```
	<receiver android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler">
<intent-filter>
<action android:name="Your_Android_Package_Name.Cancel_IBMPushNotification"/>
	</intent-filter>
	</receiver>
```
	{: codeblock}

- Wenn die App aktiv ist (im Vordergrund oder Hintergrund ausgeführt wird) und wenn sie nicht ausgeführt wird (geschlossen ist)

Erweitern Sie den Broadcastempfänger `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler` und überschreiben Sie die Methode `onReceive()`. Dabei muss `MFPPushNotificationStatusListener` vor dem Aufrufen der Methode `onReceive()` der Basisklasse registriert werden. 

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


Fügen Sie das folgende Snippet Ihrer Datei `AndroidManifest.xml` hinzu:

```
	<receiver android:name="Your_Android_Package_Name.Your_Handler">
<intent-filter>
<action android:name="Your_Android_Package_Name.Cancel_IBMPushNotification"/>
	</intent-filter>
	</receiver>
```
    {: codeblock}

### Einfache Push-Benachrichtigungen senden
{: #send-basic-notification}

Nach dem Entwickeln Ihrer Anwendungen können Sie einfache Push-Benachrichtigungen senden.

Führen Sie die folgenden Schritte aus, um einfache Push-Benachrichtigungen zu senden:

1. Wählen Sie **Benachrichtigungen senden** aus und erstellen Sie eine Nachricht, indem Sie eine Option für **Senden an** auswählen. Die unterstützten Optionen sind **Gerät nach Tag**, **Geräte-ID**, **Benutzer-ID**, **Android-Geräte**, **iOS-Geräte**, **Webbenachrichtigungen** und **Alle Geräte**.
**Hinweis**: Wenn Sie die Option **Alle Geräte** auswählen, erhalten alle Geräte, die Push-Benachrichtigungen subskribiert haben, Benachrichtigungen.
![Anzeige 'Benachrichtigungen'](images/tag_notification.jpg)

2. Erstellen Sie Ihre Nachricht im Feld **Nachricht**. Treffen Sie Ihre Auswahl, um die optionalen Einstellungen wie erforderlich zu konfigurieren.
3. Klicken Sie auf **Senden**.
3. Überprüfen Sie, ob die Geräte Ihre Benachrichtigung empfangen haben.

Der folgende Screenshot zeigt ein Alertfeld bei der Verarbeitung einer Push-Benachrichtigung
im Vordergrund auf einem Android-Gerät.

![Push-Benachrichtigung im Vordergrund auf einem Android-Gerät](images/Android_Screenshot.jpg)

Der folgende Screenshot zeigt eine Push-Benachrichtigung im Hintergrund auf einem Android-Gerät.

![Push-Benachrichtigung im Hintergrund auf einem Android-Gerät](images/background.jpg)

### Optionale Android-Einstellungen beim Senden von Benachrichtigungen
{: #send_otpional_setting}

Sie können die {{site.data.keyword.mobilepushshort}}-Einstellungen zum Senden von Benachrichtigung an Android-Geräte anpassen. Die folgenden optionalen Anpassungsoptionen werden unterstützt:
![Benutzerdefinierte Android-Einstellungen](images/android_custom_settings.jpg)

- Collapse Key (Schlüssel ausblenden): Ausgeblendete Schlüssel sind den Benachrichtigungen angehängt. Wenn mehrere Benachrichtigungen nacheinander mit demselben ausgeblendeten Schlüssel eintreffen, während das Gerät offline ist, werden die Benachrichtigungen ausgeblendet. Wenn ein Gerät wieder online ist, empfängt es Benachrichtigungen vom FCM/GCM-Server und zeigt nur die aktuellste Benachrichtigung an, die denselben ausgeblendeten Schlüssel aufweist. Falls der ausgeblendete Schlüssel nicht definiert ist, werden sowohl die neuen als auch die alten Nachrichten für die künftige Bereitstellung gespeichert.
- Sound (Audio): Gibt einen Soundclip an, der beim Empfang einer Benachrichtigung abgespielt wird. Unterstützt den Standard oder den Namen einer Soundressource, die in der App gebündelt ist.
- Icon (Symbol): Gibt den Namen des Symbols an, das für die Benachrichtigung angezeigt werden soll. Stellen Sie sicher, dass das Symbol zusammen mit der Clientanwendung im Ordner `res/drawable` gepackt ist.
- Priority (Priorität): Gibt die Optionen für die Zuordnung der Zustellpriorität zu Nachrichten an. Die Priorität `high` oder `max` bewirkt Heads-up-Benachrichtigungen, während die Nachrichten mit der Priorität `low` oder `default` keine Netzverbindungen auf Geräten, die sich im Ruhemodus befinden, öffnen. Nachrichten mit der Option `min` sind Benachrichtigungen im Hintergrund.
- Visibility (Sichtbarkeit): Sie können durch Ihre Auswahl der Option `public` oder `private` die Sichtbarkeit von Benachrichtigungen festlegen. Die Option `private` beschränkt die öffentliche Anzeige und Sie können die Aktivierung auswählen, wenn Ihr Gerät mit einer Pin oder einem Muster geschützt ist und für die Benachrichtigungseinstellung **Sensiblen Inhalt von Benachrichtigungen ausblenden** festgelegt wurde. Wenn für die Sichtbarkeit `private` festgelegt wurde, muss das Feld `redact` erwähnt werden. Es wird nur der Inhalt, der im Feld `redact` angegeben ist, auf einer sicheren, gesperrten Anzeige dargestellt. Durch die Auswahl von `public` werden die Benachrichtigungen wiedergegeben, die offen gelesen werden können.
- Time to live (Lebensdauer): Dieser Wert wird in Sekunden angegeben. Falls dieser Parameter nicht angegeben ist, speichert der FCM/GCM-Server die Nachricht für vier Wochen und versucht, diese zu übermitteln. Die Gültigkeit läuft nach vier Wochen ab. Der mögliche Wertebereich liegt zwischen 0 und 2.419.200 Sekunden.
- Delay when idle (Verzögerung bei Inaktivität): Durch das Festlegen dieses Werts auf `true` wird der FCM/GCM-Server angewiesen, die Benachrichtigung nicht auszuliefern, wenn das Gerät inaktiv ist. Legen Sie für diesen Wert `false` fest, um die Übermittlung der Benachrichtigung sicherzustellen, auch wenn das Gerät inaktiv ist.
- Sync (Synchronisation): Durch das Festlegen von `true` für diese Option werden Benachrichtigungen über alle registrierten Geräte hinweg synchronisiert. Falls der Benutzer mit einem Benutzernamen über mehrere Geräte mit denselben installierten Anwendungen verfügt, wird die Benachrichtigung durch das Lesen auf einem Gerät auf den anderen Geräten gelöscht. Sie müssen sicherstellen, dass Sie beim {{site.data.keyword.mobilepushshort}}-Service mit der Benutzer-ID registriert sind, damit diese Option funktioniert.
- Additional payload (Zusätzliche Nutzdaten): Gibt die angepassten Werte für Nutzdaten für Ihre Benachrichtigungen an.


### Nächste Schritte
{: #next_steps_tag_based_notifications}

Nachdem Sie einfache Benachrichtigungen erfolgreich eingerichtet haben, können Sie tagbasierte Benachrichtigungen und erweiterte Optionen konfigurieren.

Fügen Sie diese Push Notifications-Service-Features zur App hinzu.
Informationen zur Verwendung tagbasierter Benachrichtigungen finden Sie in [Tagbasierte Benachrichtigungen](c_tag_basednotifications.html).
Informationen zur Verwendung erweiterter Benachrichtigungsoptionen finden Sie in [Erweiterte Push-Benachrichtigungen aktivieren](t_advance_badge_sound_payload.html).


## Cordova-Anwendungen für den Empfang von Push-Benachrichtigungen aktivieren
{: #cordova_enable}


Cordova ist eine Plattform zum Erstellen von Hybridanwendungen mit JavaScript, CSS und HTML. Der {{site.data.keyword.mobilepushshort}}-Service unterstützt die Entwicklung von iOS- und Android-Anwendungen, die auf Cordova basieren.

Sie können Cordova-Anwendungen für den Empfang von Push-Benachrichtigungen auf Ihren Geräten aktivieren.

### Cordova-Push-Plug-in installieren
{: #cordova_install}

Installieren und verwenden Sie das Client-Push-Plug-in für die weitere Entwicklung Ihrer Cordova-Anwendungen. Dabei wird auch das Cordova Core-Plug-in installiert, das Ihre Verbindung zu Bluemix initialisiert.

1. Laden Sie die aktuelle Version für das Android Studio-SDK und Xcode herunter.
1. Richten Sie den Emulator ein. Verwenden Sie für Android Studio einen Emulator, der die Google Play-API unterstützt.
1. Installieren Sie das Git-Befehlszeilentool. Stellen Sie unter Windows sicher, dass Sie die Option zum Ausführen von Git über die Windows-Eingabeaufforderung auswählen. Informationen zum Herunterladen und Installieren dieses Tools finden Sie unter [Git ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://git-scm.com/downloads){: new_window}.
1. Installieren Sie Node.js und das NPM-Tool (NPM = Node Package Manager). Das NPM-Befehlszeilentool wird als Produktpaket mit Node.js bereitgestellt. Informationen zum Herunterladen und Installieren von Node.js finden Sie unter [Node.js ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://nodejs.org/en/download/){: new_window}.
1. Installieren Sie über die Befehlszeile die Cordova-Befehlszeilentools mithilfe des Befehls **npm install -g cordova**. Dies ist eine Voraussetzung für die Verwendung des Cordova-Push-Plug-ins. Informationen zum Installieren von Cordova und zum Einrichten Ihrer Cordova-App finden Sie unter [Cordova Apache ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cordova.apache.org/#getstarted){: new_window}. Weitere Informationen finden Sie in der [Readme-Datei ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window} für das Cordova-Push-Plug-in.
1. Wechseln Sie in den Ordner, in dem Sie Ihre Cordova-App erstellen möchten, und führen
Sie den folgenden Befehl aus, um eine Cordova-Anwendung zu erstellen. Wenn Sie bereits über eine
Cordova-App verfügen, fahren Sie mit Schritt 3 fort.
```cordova create your_app_name
	cd your_app_name
```
	{: codeblock}
- Optional: Sie können die Datei **config.xml** bearbeiten und den Anwendungsnamen im Element <name> in einen von Ihnen gewählten Namen statt des Standardnamens 'HelloCordova' ändern.

Stellen Sie sicher, dass Sie die richtige Bundle-ID angegeben haben. Folgende Fehlernachrichten können zu einem Ergebnis in Xcode führen, wenn die falsche Bundle-ID angegeben wird.

* The executable was signed with invalid entitlements (Die ausführbare Funktion ist mit ungültigen Berechtigungen signiert).
* The entitlements specified in your application’s Code Signing Entitlements file do not match those specified in your provisioning profile (Die in der Berechtigungsdatei für die Codeunterzeichnung Ihrer Anwendung angegebenen Berechtigungen stimmen nicht mit den angegebenen Berechtigungen in Ihrem Bereitstellungsprofil überein). Um dieses Problem zu beheben, geben Sie korrekte Bundle-ID in Xcode oder in der Datei **config.xml** Ihrer Cordova-App an.

1. Fügen Sie die Mindestversion der unterstützten API oder die Bereitstellungszieldeklaration zur Datei 'config.xml' Ihrer Cordova-Anwendung hinzu: Der Wert für 'minSdkVersion' muss größer als 15 sein. Der Wert für 'targetSdkVersion' muss immer das neueste Android-SDK angeben, das bei Google verfügbar ist.
	
	* Android - Öffnen Sie die Datei **config.xml** mit dem Editor und aktualisieren
das Element `<platform name="android">` mit der SDK-Mindestversion und -Zielversion:

	```
	<platform name="android">
    	<preference name="android-minSdkVersion" value="15" />
    	<preference name="android-targetSdkVersion" value="23" />
    	<!-- add minimum and target Android API level declaration -->
	</platform> 
	```
    	{: codeblock}

   * iOS - Aktualisieren Sie das Element <platform name="ios"> mit einer Bereitstellungszieldeklaration:

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- add deployment target declaration -->
	</platform>
	```
		{: codeblock}

1. Fügen Sie über die Cordova-Befehlszeilenschnittstelle (CLI) mit einem oder beiden der folgenden Befehle Ihre Plattform (iOS und/oder Android) hinzu:
```
cordova platform add ios
	cordova platform add android
```
	{: codeblock}

1. Geben Sie im Stammverzeichnis Ihrer Cordova-Anwendung den folgenden Befehl ein, um das Cordova-Push-Plug-in zu installieren: **cordova plugin add bms-push**. Je nachdem, welche Plattformen Sie hinzugefügt haben, wird Folgendes angezeigt:
```
Installing "bms-push" for android
Installing "bms-push" for ios
```
	{: codeblock}

1. Überprüfen Sie in Ihrem App-Stammverzeichnis mit dem Befehl **cordova plugin list**, dass das Cordova Core- und das Cordova Push-Plug-in erfolgreich installiert wurden. Je nachdem, welche Plattformen Sie hinzugefügt haben, wird Folgendes angezeigt:
```
bms-core <version> "BMSCore"
bms-push <version> "BMSPush" 
```
	{: codeblock}

1. Konfigurieren Sie Ihre iOS-Entwicklungsumgebung.
2. Erstellen Sie die Anwendung und führen Sie sie aus mit Xcode.
1. Laden Sie Ihre Firebase-Datei `google-services.json` für Android herunter und speichern Sie sie im Stammordner Ihres Cordova-Projekts in `[name-ihrer-anwendung]/platforms/android.
	1. Wechseln Sie in das Verzeichnis `[name-ihrer-anwendung]/platforms/android`.
	2. Öffnen Sie die Datei `build.gradle` (Pfad: plattform > android > build.gradle).
	3. Suchen Sie die Zeichenfolge `buildscript` in der Datei `build.gradle`.
	4. Fügen Sie nach der Zeile für den Klassenpfad (classpath) die folgende Zeile hinzu: classpath 'com.google.gms:google-services:3.0.0'
	5. Suchen Sie nach "dependencies" (Abhängigkeiten). Wählen Sie Abhängigkeiten aus, die den Text `compile` enthalten, und fügen Sie unmittelbar nach dem Ende dieser Abhängigkeiten die folgende Zeile hinzu: :apply plugin: 'com.google.gms.google-services'.
	6. Bereiten Sie Ihr Cordova-Android-Projekt vor und erstellen Sie es.
		```
		cordova prepare android
		cordova build android
		```
			{: codeblock}
	**Hinweis**: Erstellen Sie zuerst die Cordova-Anwendung über die Cordova-Befehlszeilenschnittstelle, bevor Sie das Projekt in Android Studio öffnen. Dies hilft bei der Vermeidung von Buildfehlern.

### Cordova-Plug-in
{: #cordova_initialize}

Bevor Sie das Cordova-Plug-in für den  {{site.data.keyword.mobilepushshort}}-Service verwenden können, müssen Sie es initialisieren, indem Sie die Anwendungsroute und die Anwendungs-GUID übergeben. Nach der Initialisierung des
Plug-ins können Sie die Verbindung zu der Serveranwendung herstellen, die Sie im Bluemix-Dashboard
erstellt haben. Das Cordova-Plug-in ist die Oberfläche für die Android- und iOS-Client-SDKs zum Aktivieren einer Cordova-Anwendung für die Kommunikation mit Bluemix-Services.

1. Initialisieren Sie 'BMSClient', indem Sie das folgende Code-Snippet kopieren und in Ihre Haupt-JavaScript-Datei (die für gewöhnlich im Verzeichnis **www/js** gespeichert ist) einfügen.

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

Fügen Sie für 'YOUR APP REGION' die Region für Ihre Anwendung ein. Die folgenden Konstanten stehen zur Verfügung:

```
REGION_US_SOUTH // ".ng.bluemix.net";
REGION_UK //".eu-gb.bluemix.net";
REGION_SYDNEY // ".au-syd.bluemix.net";
```

Beispiel:

```
BMSClient.initialize(BMSClient.REGION_US_SOUTH);
```

**Anmerkung**: Wenn Sie unter Verwendung der Cordova-Befehlszeilenschnittstelle eine Cordova-App erstellt haben, beispielsweise mit dem Befehl Cordova create app-name, übernehmen Sie diesen JavaScript-Code in die Datei index.js hinter der Funktion app.receivedEvent innerhalb der Funktion onDeviceReady: function(), um `BMSClient` zu initialisieren. 


### Geräte registrieren
{: #cordova_register}


Rufen Sie die Registrierungsfunktion auf, um ein Gerät für den {{site.data.keyword.mobilepushshort}}-Service zu registrieren. Kopieren Sie das folgende Code-Snippet in Ihre Cordova-Anwendung, um ein Gerät zu registrieren.

```
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure);
```
	{: codeblock}

Das folgende JavaScript-Code-Snippet zeigt, wie Sie das Bluemix Mobile Services-Client-SDK initialisieren, ein Gerät für den {{site.data.keyword.mobilepushshort}}-Service registrieren und Push-Benachrichtigungen überwachen. Schließen Sie diesen Code in Ihre Javascript-Datei ein.

Innerhalb der Funktion **onDeviceReady: function()**.

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

Fügen Sie das folgende Swift-Code-Snippet zur Klasse 'delegate' Ihrer Anwendung hinzu.

```
// Register the device token with Bluemix Push Notification Service
func application(application: UIApplication,
  didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData) {
   CDVBMSPush.sharedInstance().didRegisterForRemoteNotificationsWithDeviceToken(deviceToken)
} 
// Handle error when failed to register device token with APNs
func application(application: UIApplication,
    didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer) {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(error)
} 
```
	{: codeblock}

### Nächste Schritte
{: #cordova_register_next}

Erstellen Sie das Projekt und führen Sie es mit den folgenden Befehlen aus:

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

### Push-Benachrichtigungen in Geräten empfangen
{: #cordova_receive}

Kopieren Sie das folgende Code-Snippet, um Push-Benachrichtigungen auf Geräten zu empfangen.

#### JavaScript
{: #jvscrpt}

Fügen Sie das folgende JavaScript-Code-Snippet in die Webkomponente Ihrer Cordova-Anwendung ein.
```
var showNotification = function(notif) {
  alert(JSON.stringify(notif));
        };
        BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

#### Eigenschaften für Android-Benachrichtigungen
{: #And_notif}

Im folgenden Abschnitt sind die Eigenschaften für Android-Benachrichtigungen aufgelistet:

* **message** - Push-Benachrichtigung
* **payload** - JSON-Objekt mit den Nutzdaten einer Benachrichtigung


#### Eigenschaften für iOS-Benachrichtigungen
{: #ios_notif}

Im folgenden Abschnitt sind die Eigenschaften für iOS-Benachrichtigungen aufgelistet:

* **message** - Push-Benachrichtigung
* **payload** - JSON-Objekt, das die Nutzdaten einer Benachrichtigung enthält
action-loc-key - Diese Zeichenfolge dient als Schlüssel zum Abrufen einer lokalisierten Zeichenfolge in der aktuellen Lokalisierung, die anstelle von `View` als Titel für die entsprechende Schaltfläche verwendet werden soll.
* **badge** - Die Nummer, die als Badge des App-Symbols angezeigt werden soll. Wenn diese Eigenschaft fehlt, wird das Badge nicht geändert. Um das Badge zu entfernen,
legen Sie für diese Eigenschaft den Wert 0 fest.
* **sound** - Der Name einer Audiodatei im App-Bundle oder im Ordner 'Library/Sounds' des Datencontainers der App.


Fügen Sie die folgenden Swift-Code-Snippets zur Klasse 'delegate' Ihrer Anwendung hinzu.
```
// Handle receiving a remote notification
func application(application: UIApplication,
   didReceiveRemoteNotification userInfo: [NSObject : AnyObject],  fetchCompletionHandler completionHandler: ) {
   CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(userInfo)
}
```
	{: codeblock}

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
  let remoteNotif = launchOptions?[UIApplicationLaunchOptionsKey.remoteNotification] as? NSDictionary
  if remoteNotif != nil {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationOnLaunchWithLaunchOptions(launchOptions)
  }
} 
```
	{: codeblock}

### Einfache Push-Benachrichtigungen senden
{: #push-send-notifications}

Nach dem Entwickeln Ihrer Anwendungen können Sie einfache Push-Benachrichtigungen senden.

Führen Sie die Schritte aus, um einfache Push-Benachrichtigungen zu senden:

1. Wählen Sie **Benachrichtigungen senden** aus und erstellen Sie eine Nachricht, indem Sie eine Option für **Senden an** auswählen. Die unterstützten Optionen sind **Gerät nach Tag**, **Geräte-ID**, **Benutzer-ID**, **Android-Geräte**, **iOS-Geräte**, **Webbenachrichtigungen** und **Alle Geräte**.
**Hinweis**: Wenn Sie die Option **Alle Geräte** auswählen, erhalten alle Geräte, die Push-Benachrichtigungen subskribiert haben, Benachrichtigungen.
![Anzeige 'Benachrichtigungen'](images/tag_notification.jpg)

2. Erstellen Sie Ihre Nachricht im Feld **Nachricht**. Treffen Sie Ihre Auswahl, um die optionalen Einstellungen wie erforderlich zu konfigurieren.
3. Klicken Sie auf **Senden**.
3. Überprüfen Sie, ob die Geräte Ihre Benachrichtigung empfangen haben.

Der folgende Screenshot zeigt ein Alertfeld bei der Verarbeitung einer Push-Benachrichtigung im Vordergrund eines Android- bzw. iOS-Geräts.

![Push-Benachrichtigung im Vordergrund auf einem Android-Gerät](images/Android_Screenshot.jpg)

![Push-Benachrichtigung im Vordergrund auf einem iOS-Gerät](images/iOS_Screenshot.jpg)

   Die folgende Abbildung zeigt eine Push-Benachrichtigung im Hintergrund auf einem Android-Gerät.
![Push-Benachrichtigung im Hintergrund auf einem Android-Gerät](images/background.jpg)

#### Nächste Schritte
{: #next_steps_basic_notifications}

Nachdem Sie einfache Benachrichtigungen erfolgreich eingerichtet haben, können Sie tagbasierte Benachrichtigungen und erweiterte Optionen konfigurieren.

Fügen Sie die {{site.data.keyword.mobilepushshort}}-Service-Features zur App hinzu.
Informationen zur Verwendung tagbasierter Benachrichtigungen finden Sie in [Tagbasierte Benachrichtigungen](c_tag_basednotifications.html).
Informationen zur Verwendung erweiterter Benachrichtigungsoptionen finden Sie in [Erweiterte Push-Benachrichtigungen aktivieren](t_advance_badge_sound_payload.html).


## iOS-Anwendungen für das Senden von Push-Benachrichtigungen aktivieren
{: #enable-push-ios-notifications}

Sie können iOS-Anwendungen für das Senden von Push-Benachrichtigungen an Ihre Geräte aktivieren.


### CocoaPods installieren
{: #enable-push-ios-notifications-install}

Für ein vorhandenes Xcode-Projekt können Sie das Bluemix Mobile Services-Client-SDK mithilfe des Abhängigkeitsmanagementtools CocoaPods einrichten. Als Alternative dazu können Sie das Software-Development-Kit (SDK) manuell installieren.

Informationen zu Swift Push finden Sie in der [Readme-Datei ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}.



1. Installieren Sie CocoaPods, indem Sie in Ihrem Mac-Terminal folgenden Befehl verwenden.
	```
		$ sudo gem install cocoapods
	```
	{: codeblock}
2. Geben Sie den Befehl `pod init` in das Terminal ein, um CocoaPods zu initialisieren. Führen Sie den Befehl unbedingt aus dem Verzeichnis aus, in dem sich Ihr Xcode-Projekt befindet. Mit dem Befehl `pod init` wird eine Datei 'Podfile' erstellt.  
3. Fügen Sie in der generierten Datei 'Podfile' die erforderlichen SDK-Abhängigkeiten hinzu. Kopieren Sie die folgende Datei 'Podfile'.
   
	```
		source 'https://github.com/CocoaPods/Specs.git'
	// Copy the following list as is and remove the dependencies you do not need.
		use_frameworks!
		target 'MyApp' do
	    platform :ios, '8.0'
		pod 'BMSCore'
	    pod 'BMSPush'
      pod 'BMSAnalyticsAPI'
	end
	```
		{: codeblock}

3. Wechseln Sie am Terminal in Ihren Projektordner und installieren Sie die Abhängigkeiten mithilfe des Befehls `pod update`.

Mit diesem Befehl werden Ihre Abhängigkeiten installiert und es wird ein neuer Xcode-Arbeitsbereich erstellt.  
**Hinweis**: Stellen Sie sicher, dass Sie immer den neuen Xcode-Arbeitsbereich öffnen und nicht die ursprüngliche Xcode-Projektdatei:
```
  $ open App.xcworkspace
```
	{: codeblock}

Der Arbeitsbereich enthält Ihr ursprüngliches Projekt und das Projekt 'Pods', das Ihre Abhängigkeiten enthält. Wenn Sie den Bluemix mobile Services-Quellenordner ändern möchten, finden Sie diesen in Ihrem Projekt 'Pods' unter `Pods/yourImportedSourceFolder`, zum Beispiel: `Pods/BMSPush`.

### Frameworks mit Carthage hinzufügen
{: #carthage}

Fügen Sie mithilfe von [Carthage ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window} Frameworks zu Ihrem Projekt hinzu. Beachten Sie, dass Carthage in Xcode8 nicht unterstützt wird.

1. Fügen Sie `BMSPush`-Frameworks zur Cartfile hinzu:
	```
	github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
	```
	{: codeblock}
2. Führen Sie den Befehl `carthage update` aus. Wenn der Build abgeschlossen ist, ziehen Sie `BMSPush.framework`, `BMSCore.framework` und `BMSAnalyticsAPI.framework` in das Xcode-Projekt.
3. Befolgen Sie die Anweisungen auf der [Carthage-Website ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}, um die Integration abzuschließen.

### iOS-SDK einrichten
{: #ios-sdk}

Richten Sie das iOS-SDK ein. Fügen Sie den folgenden Code der Datei **AppDelegate.swift** in Ihrer Anwendung hinzu. Beachten Sie, dass dies auch bei APNs registriert wird.  
```
  func application(_ application: UIApplication,
didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {  
   BMSPushClient.sharedInstance.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE")
  }
```
    {: codeblock}

### Importierte Frameworks und Quellenordner verwenden
{: #using-imported-frameworks}

Referenzieren Sie das SDK in Ihrem Code. Stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind.

- iOS 8.0 oder höher	
- Xcode 7

Schreiben Sie `#import`-Anweisungen für die entsprechenden Header, zum Beispiel:
```
	 //swift
import BMSCore
import BMSPush
```
		{: codeblock}

Die Push-Readme-Datei für Swift finden Sie in der [Readme-Datei ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}.

**Hinweis**: Durch Aktualisieren Ihres Projekts 'Pods' mithilfe der CocoaPods-Befehle `pod install` oder `pod update` werden die Bluemix Mobile Services-Quellenorder möglicherweise überschrieben. Wenn Sie Ihre angepassten Versionen der ursprünglichen Dateien aufbewahren möchten, müssen Sie sicherstellen, dass für sie ein Backup durchgeführt wird, bevor Sie einen dieser Befehle absetzen.


### Buildeinstellungen
{: #build-settings}

Rufen Sie **Xcode > Build Settings > Build Options** auf und setzen Sie **Enable Bitcode** auf **No**.

**Achtung**: Ab iOS 9 können sich Änderungen an der Komponente 'App Transport Security' (ATS) auf
die Verarbeitung des Authentifizierungsprozesses auswirken. Die folgenden Blogbeiträge enthalten weitere Informationen zu den Änderungen: [ATS and Bitcode in iOS 9 ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/){: new_window} und [Connect your iOS 9 app to Bluemix today ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/){: new_window}.

### Push-SDK für iOS-Apps initialisieren
{: #enable-push-ios-notifications-initialize}

Das Anwendungs-Delegat für die iOS-Anwendung ist eine übliche Position für den Initialisierungscode. Klicken Sie in Ihrem Push-Dashboard auf den Link **Mobile Systemerweiterungen**, um die Anwendungsroute und die GUID abzurufen.

#### Core-SDK initialisieren
{: #Initializing-the-core-sdk}

Verwenden Sie das folgende Code-Snippet, um das Core-SDK für Swift mit IBM Bluemix-GUID, Route und Region zu initialisieren: 
```
	let myBMSClient = BMSClient.sharedInstance
	myBMSClient.initialize(bluemixRegion: "Location where your app is hosted.") 
```
	{: codeblock}

#### Route, GUID und Bluemix-Region
{: #route-guid-bluemix-region}


- **appRoute**: Gibt die Route an, die der Serveranwendung zugewiesen ist, die Sie in Bluemix erstellt haben.


- **GUID**: Gibt den eindeutigen Schlüssel an, der der Anwendung zugewiesen wird, die Sie in Bluemix erstellt haben. Bei diesem Wert muss die Groß-/Kleinschreibung beachtet werden.


- **bluemixRegionSuffix**: Gibt den Standort an, an dem die App gehostet ist. Der Parameter `bluemixRegion` gibt an, welche Bluemix-Bereitstellung verwendet wird. Sie können diesen Wert mit der statischen Eigenschaft `BMSClient.REGION` angeben und einen von drei Werten verwenden:

	- BMSClient.Region.usSouth 
	- BMSClient.Region.unitedKingdom
	- BMSClient.Region.sydney


- **AppGUID**: Gibt den eindeutigen 'AppGUID'-Schlüssel an, der dem von Ihnen in Bluemix erstellten {{site.data.keyword.mobilepushshort}}-Service zugewiesen wird.

#### Client-Push-SDK initialisieren
{: #initializing-the-client-Push-SDK}

```
	let push = BMSPushClient.sharedInstance
	push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


### iOS-Anwendungen und -Geräte registrieren
{: #enable-push-ios-notifications-register}

Nach der Installation auf einem Gerät muss eine Anwendung bei APNs registriert werden, um ferne Benachrichtigungen empfangen zu können. Nachdem das von APNs generierte Gerätetoken von der App empfangen worden ist, muss es zurück an den {{site.data.keyword.mobilepushshort}}-Service geleitet werden.

Führen Sie zum Registrieren von iOS-Anwendungen und -Geräten die folgenden Schritte aus:

1. Erstellen Sie eine Back-End-Anwendung.
2. Übergeben Sie das Token an {{site.data.keyword.mobilepushshort}}.


#### Back-End-Anwendung erstellen
{: #create-a-backend-app}

Erstellen Sie im Bluemix®-Katalog im Abschnitt 'Boilerplates' eine Back-End-Anwendung, mit der der {{site.data.keyword.mobilepushshort}}-Service automatisch an diese Anwendung gebunden wird. Wenn Sie bereits eine Back-End-App erstellt haben, stellen Sie sicher, dass Sie diese App an den {{site.data.keyword.mobilepushshort}} Service binden.


#### Tokens an Push Notifications übergeben
{: #pass-token-push-notifications}

Nachdem das Token von APNs empfangen worden ist, leiten Sie es als Teil der Methode `registerDevice:withDeviceToken` an {{site.data.keyword.mobilepushshort}} weiter.

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


### Push-Benachrichtigungen in iOS-Geräten empfangen
{: #enable-push-ios-notifications-receiving}

Um Push-Benachrichtigungen in iOS-Geräten zu empfangen, fügen Sie die folgende Swift-Methode zum Anwendungs-Delegat Ihrer Anwendung hinzu.

```
   func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) 
  { //UserInfo dictionary will contain data sent from the server }
```
	{: codeblock}

### Push-Benachrichtigungen in iOS-Geräten überwachen
{: #ios-monitoring}


Sie können die Anzahl und den aktuellen Status der gesendeten Push-Benachrichtigungen überwachen. Zum Aktivieren der Überwachung fügen Sie abhängig vom jeweiligen Ereignis eine der folgenden Swift-Methoden zur Klasse 'delegate' Ihrer Anwendung hinzu. 



- Benachrichtigungsstatus senden, wenn die App durch Klicken auf die Benachrichtigung geöffnet wird.
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



- Benachrichtigungsstatus senden, wenn sich die App im Hintergrundmodus befindet.
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


### Einfache Push-Benachrichtigungen senden
{: #send}

Nach dem Entwickeln Ihrer Anwendungen können Sie einfache Push-Benachrichtigungen senden.

Führen Sie die Schritte aus, um einfache Push-Benachrichtigungen zu senden:

1. Wählen Sie **Benachrichtigungen senden** aus und erstellen Sie eine Nachricht, indem Sie eine Option für **Senden an** auswählen. Die unterstützten Optionen sind **Gerät nach Tag**, **Geräte-ID**, **Benutzer-ID**, **Android-Geräte**, **iOS-Geräte**, **Webbenachrichtigungen** und **Alle Geräte**.  
**Hinweis**: Wenn Sie die Option **Alle Geräte** auswählen, erhalten alle Geräte, die Push-Benachrichtigungen subskribiert haben, Benachrichtigungen.
![Anzeige 'Benachrichtigungen'](images/tag_notification.jpg)

2. Erstellen Sie Ihre Nachricht im Feld **Nachricht**. Treffen Sie Ihre Auswahl, um die optionalen Einstellungen wie erforderlich zu konfigurieren.
3. Klicken Sie auf **Senden**.
3. Überprüfen Sie, ob die Geräte Ihre Benachrichtigung empfangen haben.

Die folgende Abbildung zeigt ein Alertfeld bei der Verarbeitung einer {{site.data.keyword.mobilepushshort}} eines iOS-Geräts.

![Push-Benachrichtigung im Vordergrund auf einem iOS-Gerät](images/iOS_Screenshot.jpg) 

#### Optionale Einstellungen beim Senden von Benachrichtigungen
{: #send_ios_otpional_setting}

Sie können die {{site.data.keyword.mobilepushshort}}-Einstellungen zum Senden von Benachrichtigung an iOS-Geräte anpassen. Die folgenden optionalen Anpassungsoptionen werden unterstützt:

- **Badge** (Badge): Gibt die Zahl an, die auf dem Anwendungsbadge angezeigt wird. Der Standardwert lautet Null (0) und führt dazu, dass kein Badge angezeigt wird. 
- **Sound** (Audio): Gibt einen Soundclip an, der beim Empfang einer Benachrichtigung abgespielt wird. Unterstützt den Standard oder den Namen einer Soundressource, die in der App gebündelt ist.
- **Additional payload** (Zusätzliche Nutzdaten): Gibt die angepassten Werte für Nutzdaten für Ihre Benachrichtigungen an.

### Interaktive Benachrichtigungen aktivieren
{: #enb_snd_ios_otpional}

Sie können jetzt Ihre iOS-Benachrichtigungen durch zusätzliche Details wie das Hinzufügen eines Bildes, einer Karte oder einer Antwortschaltfläche attraktiver gestalten, indem Sie interaktive Benachrichtigungen aktivieren. Dadurch wird den Kunden mehr Kontext geboten, verbunden mit der Möglichkeit sofortiger Maßnahmen ohne Verlassen des aktuellen Kontexts.  

Verwenden Sie den folgenden Code zum Aktivieren interaktiver Benachrichtigungen:



- Schaltflächenaktion definieren
	```
		let actionOne = BMSPushNotificationAction(identifierName: "ACCEPT", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
 let actionTwo = BMSPushNotificationAction(identifierName: "DECLINE", buttonTitle: "Decline", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
	```
		{: codeblock}


- Kategorie für die Schaltflächen definieren
	```
		let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
	```
		{: codeblock}


- Registrierung aktualisieren, um Schaltflächen einzubeziehen
	```
		Pass the defined category into iOS BMSPushClientOptions
		let notificationOptions = BMSPushClientOptions(categoryName: [category])
		let push = BMSPushClient.sharedInstance
		push.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE", options: notificationOptions)
	```
		{: codeblock}

Führen Sie die folgenden Schritte aus, um eine interaktive Benachrichtigung zu senden:

1. Wählen Sie im Abschnitt zum Erstellen für die Dropdown-Liste 'Senden an' **iOS-Geräte** aus.
2. Geben Sie die Benachrichtigungsnachricht ein, die Sie senden möchten.
3. Wählen Sie im Abschnitt mit den optionalen Einstellungen **Mobile** aus und klicken Sie auf **iOS**.
4. Wählen Sie in der Dropdown-Liste 'Typ' **Gemischt** aus.
5. Geben Sie im Feld 'Kategorie' den Benachrichtigungstyp an, den Sie in Ihrer App definiert haben. 

![Interaktive Benachrichtigung für iOS](images/push_ios_notification_interactive.jpg) 

#### Nächste Schritte
{: #next_steps_02}

Nachdem Sie einfache Benachrichtigungen erfolgreich eingerichtet haben, können Sie tagbasierte Benachrichtigungen und erweiterte Optionen konfigurieren.

Fügen Sie die folgenden Funktionen von Push Notifications Service zu Ihrer App hinzu.
Informationen zur Verwendung tagbasierter Benachrichtigungen finden Sie in [Tagbasierte Benachrichtigungen](c_tag_basednotifications.html).
Informationen zur Verwendung erweiterter Benachrichtigungsoptionen finden Sie in [Erweiterte Push-Benachrichtigungen aktivieren](t_advance_badge_sound_payload.html).
