---

copyright:
 years: 2015 2016

---


# Android-Anwendungen für den Empfang von Push-Benachrichtigungen aktivieren
{: #tag_based_notifications}
Letzte Aktualisierung: 19. Oktober 2016
{: .last-updated}

Sie können Android-Anwendungen für den Empfang von {{site.data.keyword.mobilepushshort}} auf Ihren Geräten aktivieren. Android Studio ist dafür Voraussetzung und auch die empfohlene Methode für die Erstellung von Android-Projekten. Grundlegende Kenntnisse von Android Studio sind erforderlich.

## Client-Push-SDK mit Gradle installieren
{: #android_install}

In diesem Abschnitt wird die Vorgehensweise zum Installieren und Verwenden des Client-Push-SDK für die weitere Entwicklung Ihrer Android-Anwendungen beschrieben.

Das Push-SDK für Bluemix® Mobile Services kann mithilfe von Gradle hinzugefügt werden. Gradle lädt automatisch Artefakte aus Repositorys herunter und stellt Sie in Ihrer Android-Anwendung zur Verfügung. Stellen Sie sicher, dass Sie Android Studio und das Android Studio-SDK ordnungsgemäß einrichten. Weitere Informationen zum Einrichten Ihres Systems finden Sie unter [Android Studio Overview](https://developer.android.com/tools/studio/index.html). Informationen zu Gradle finden Sie in [Configuring Gradle Builds](http://developer.android.com/tools/building/configuring-gradle.html).

1. Öffnen Sie in Android Studio nach dem Erstellen und Öffnen der mobilen Anwendung die Anwendungsdatei **build.gradle**.
2. Fügen Sie die folgenden Abhängigkeiten zu Ihrer mobilen Anwendung hinzu. Mit den folgenden Zeilen wird das Push-Client-SDK der Bluemix™ Mobile-Services und das Google Play Services-SDK zu Ihren Abhängigkeiten für den Kompilierungsbereich hinzugefügt.
```
com.ibm.mobilefirstplatform.clientsdk.android:push:2.+
```
    {: codeblock}
2. Erstellen Sie das Projekt, um sicherzustellen, dass die Abhängigkeiten aufgelöst werden.
3. Fügen Sie die folgenden Abhängigkeiten zu Ihrer mobilen Anwendung hinzu. Die folgenden Importanweisungen sind für Code-Snippets erforderlich:
```
import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
```
    {: codeblock}

2. Fügen Sie die folgenden Berechtigungen in der Datei **AndroidManifest.xml** hinzu. Ein Beispielmanifest
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
	{: codeblock}
 Weitere Informationen zu [Android-Berechtigungen](http://developer.android.com/guide/topics/security/permissions.html) finden Sie hier.

4. Fügen Sie die Einstellungen für die Benachrichtigungsabsicht für die Aktivität hinzu. Mit dieser Einstellung wird die Anwendung gestartet, wenn der Benutzer im Benachrichtigungsbereich auf die empfangene Benachrichtigung klickt.
```
<intent-filter>
	<action android:name="Your_Android_Package_Name.IBMPushNotification"/>
	<category  android:name="android.intent.category.DEFAULT"/>
</intent-filter>
```
	{: codeblock}
**Hinweis**: Ersetzen Sie in der obigen Aktion *ihr_android-paketname* durch den Namen des Anwendungspakets, der in Ihrer Anwendung verwendet wird.

5. Fügen Sie den Absichtsservice und die Absichtsfilter von Firebase Cloud Messaging (FCM) bzw. Google Cloud Messaging (GCM) für Ereignisbenachrichtigungen des Typs RECEIVE hinzu.
```
<service android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushIntentService" />
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
    {: codeblock}

6. Der {{site.data.keyword.mobilepushshort}}-Service unterstützt den Abruf von Einzelbenachrichtigungen aus dem Benachrichtigungsfach. Für Benachrichtigungen, auf die über das Benachrichtigungsfach zugegriffen wird, wird Ihnen ein Handle nur für die Benachrichtigung bereitgestellt, auf die geklickt wird. Wenn die Anwendung auf normale Weise geöffnet wird, werden alle Benachrichtigungen angezeigt. Aktualisieren Sie Ihre Datei **AndroidManifest.xml** mit dem folgenden Snippet, um diese Funktion zu nutzen:

```
<activity android:name="
com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationHandler"
android:theme="@android:style/Theme.NoDisplay"/>
```

## Push-SDK für Android-Apps initialisieren
{: #android_initialize}

Die Methode 'onCreate' der Hauptaktivität in Ihrer Android-Anwendung ist eine übliche Position für den Initialisierungscode. Zwei Komponenten des SDK müssen initialisiert werden. Eine ist das Core-SDK, die andere ist das Push-SDK, das auf dem Core-SDK aufgebaut ist.

###Core-SDK initialisieren

```
// SDK für Android initialisieren
    BMSClient.getInstance().initialize(this, BMSClient.REGION_US_SOUTH);
```
    {: codeblock}

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
	{: codeblock}

####AppGUID
{: appguid_initialize_client_push_sdk}

Dies ist der 'AppGUID'-Schlüssel des {{site.data.keyword.mobilepushshort}}-Service. Bei diesem Wert muss die Groß-/Kleinschreibung beachtet werden. Öffnen Sie das Push Notification-Dashboard und wählen Sie die Registerkarte 'Konfigurieren' aus. Diesen Wert können Sie im Dashboard des Push Notification-Service in der Registerkarte 'Konfigurieren' über 'Mobile Systemerweiterungen' abrufen. 

## Android-Geräte registrieren
{: #android_register}

Verwenden Sie die API `MFPPush.register()`, um das Gerät beim {{site.data.keyword.mobilepushshort}}-Service zu registrieren. Bei der Registrierung für Android-Geräte fügen Sie dem Bluemix-Dashboard für die Konfiguration des {{site.data.keyword.mobilepushshort}}-Service die Angaben zu Firebase Cloud Messaging (FCM) bzw. Google Cloud Messaging (GCM) hinzu. Weitere Informationen finden Sie im Abschnitt zur [Konfiguration von Berechtigungsnachweisen für Google Cloud Messaging](t_push_provider_android.html).

Kopieren Sie die folgenden Code-Snippets in Ihre mobile Android-Anwendung.

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
	{: codeblock}

2. Erstellen Sie einen Build für das Projekt und führen Sie ihn in dem Gerät oder im Emulator aus. Wenn die Methode onSuccess() für den Antwortlistener in der Methode register() aufgerufen wird, wird bestätigt, dass das Gerät erfolgreich für den {{site.data.keyword.mobilepushshort}}-Service registriert wurde. An diesem Punkt können Sie gemäß der in 'Einfache Push-Benachrichtigungen senden' beschriebenen Anleitung eine Nachricht senden.
3. Überprüfen Sie, ob die Geräte Ihre Benachrichtigung empfangen haben. Wenn die Anwendung im Vordergrund ausgeführt wird, wird die Benachrichtigung von **MFPPushNotificationListener** verarbeitet. Wenn die Anwendung im Hintergrund ausgeführt wird, wird eine Nachricht in der Benachrichtigungsleiste angezeigt.


## Einfache Push-Benachrichtigungen senden
{: #send}

Nach dem Entwickeln Ihrer Anwendungen können Sie einfache Push-Benachrichtigungen senden.

Führen Sie die Schritte aus, um einfache Push-Benachrichtigungen zu senden:

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

### Optionale Einstellungen beim Senden von Benachrichtigungen
{: #send_otpional_setting}

Sie können die {{site.data.keyword.mobilepushshort}}-Einstellungen zum Senden von Benachrichtigung an Android-Geräte anpassen. Die folgenden optionalen Anpassungsoptionen werden unterstützt:
![Angepasste Android-Einstellungen](images/android_custom_settings.jpg)

- **Collapse Key** (Schlüssel ausblenden): Ausgeblendete Schlüssel sind den Benachrichtigungen angehängt. Wenn mehrere Benachrichtigungen nacheinander mit demselben ausgeblendeten Schlüssel eintreffen, während das Gerät offline ist, werden die Benachrichtigungen ausgeblendet. Wenn ein Gerät wieder online ist, empfängt es Benachrichtigungen vom FCM/GCM-Server und zeigt nur die aktuellste Benachrichtigung an, die denselben ausgeblendeten Schlüssel aufweist. Falls der ausgeblendete Schlüssel nicht definiert ist, werden sowohl die neuen als auch die alten Nachrichten für die künftige Bereitstellung gespeichert.
- **Sound** (Audio): Gibt einen Soundclip an, der beim Empfang einer Benachrichtigung abgespielt wird. Unterstützt den Standard oder den Namen einer Soundressource, die in der App gebündelt ist.
- **Icon** (Symbol): Gibt den Namen des Symbols an, das für die Benachrichtigung angezeigt werden soll. Stellen Sie sicher, dass Sie das Symbol zusammen mit der Clientanwendung im Ordner 'res/drawable' paketiert haben.
- **Priority** (Priorität): Gibt die Optionen für die Zuordnung der Zustellpriorität zu Nachrichten an. Die Priorität `high` oder `max` bewirkt Heads-up-Benachrichtigungen, während die Nachrichten mit der Priorität `low` oder `default` keine Netzverbindungen auf Geräten, die sich im Ruhemodus befinden, öffnen. Nachrichten mit der Option `min` sind Benachrichtigungen im Hintergrund.
- **Visibility** (Sichtbarkeit): Sie können durch Ihre Auswahl der Option `public` oder `private` die Sichtbarkeit von Benachrichtigungen festlegen. Die Option `private` beschränkt die öffentliche Anzeige und Sie können die Aktivierung auswählen, wenn Ihr Gerät mit einer Pin oder einem Muster geschützt ist und für die Benachrichtigungseinstellung "Sensiblen Inhalt von Benachrichtigungen ausblenden" festgelegt wurde. Wenn für die Sichtbarkeit `private` festgelegt wurde, muss das Feld "redact" erwähnt werden. Es wird nur der Inhalt, der im Feld 'redact' angegeben ist, auf einer sicheren, gesperrten Anzeige dargestellt. Durch die Auswahl von `public` werden die Benachrichtigungen wiedergegeben, die offen gelesen werden können.
- **Time to live** (Lebensdauer): Dieser Wert wird in Sekunden angegeben. Wenn dieser Parameter nicht angegeben ist, speichert der FCM/GCM-Server die Nachricht für vier Wochen und versucht diese zu übermitteln. Die Gültigkeit läuft nach vier Wochen ab. Der mögliche Wertebereich liegt zwischen 0 und 2.419.200 Sekunden.
- **Delay when idle**: (Verzögerung bei Inaktivität): Durch das Festlegen dieses Werts auf `true` wird der FCM/GCM-Server angewiesen, die Benachrichtigung nicht auszuliefern, wenn das Gerät inaktiv ist. Legen Sie für diesen Wert `false` fest, um die Übermittlung der Benachrichtigung sicherzustellen, auch wenn das Gerät inaktiv ist.
- **Sync** (Synchronisation): Durch das Festlegen von `true` für diese Option werden Benachrichtigungen über alle registrierten Geräte hinweg synchronisiert. Falls der Benutzer mit einem Benutzernamen über mehrere Geräte mit denselben installierten Anwendungen verfügt, wird die Benachrichtigung durch das Lesen auf einem Gerät auf den anderen Geräten gelöscht. Sie müssen sicherstellen, dass Sie beim {{site.data.keyword.mobilepushshort}}-Service mit der Benutzer-ID registriert sind, damit diese Option funktioniert.
- **Additional payload** (Zusätzliche Nutzdaten): Gibt die angepassten Werte für Nutzdaten für Ihre Benachrichtigungen an.


## Nächste Schritte
{: #next_steps_tags}

Nachdem Sie einfache Benachrichtigungen erfolgreich eingerichtet haben, können Sie tagbasierte
Benachrichtigungen und erweiterte Optionen konfigurieren.

Fügen Sie die folgenden Funktionen des Push Notifications Service zu Ihrer App hinzu.
Informationen zur Verwendung tagbasierter Benachrichtigungen finden Sie in [Tagbasierte Benachrichtigungen](c_tag_basednotifications.html).
Informationen zur Verwendung erweiterter Benachrichtigungsoptionen finden Sie in [Erweiterte Push-Benachrichtigungen aktivieren](t_advance_badge_sound_payload.html).
