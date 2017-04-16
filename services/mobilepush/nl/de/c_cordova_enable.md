---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Cordova-Anwendungen für den Empfang von Push-Benachrichtigungen aktivieren
{: #cordova_enable}
Letzte Aktualisierung: 18. Januar 2017
{: .last-updated}

Cordova ist eine Plattform zum Erstellen von Hybridanwendungen mit JavaScript, CSS und HTML. Der {{site.data.keyword.mobilepushshort}}-Service unterstützt die Entwicklung von iOS- und Android-Anwendungen, die auf Cordova basieren.

Sie können Cordova-Anwendungen für den Empfang von Push-Benachrichtigungen auf Ihren Geräten aktivieren.

## Cordova-Push-Plug-in installieren
{: #cordova_install}

Installieren und verwenden Sie das Client-Push-Plug-in für die weitere Entwicklung Ihrer Cordova-Anwendungen. Dabei wird auch das Cordova Core-Plug-in installiert, das Ihre Verbindung zu Bluemix initialisiert.

### Vorbemerkungen

1. Laden Sie die aktuelle Version für das Android Studio-SDK und Xcode herunter.
1. Richten Sie den Emulator ein. Verwenden Sie für Android Studio einen Emulator, der die Google Play-API unterstützt.
1. Installieren Sie das Git-Befehlszeilentool. Stellen Sie unter Windows sicher, dass Sie die Option zum Ausführen von Git über die Windows-Eingabeaufforderung auswählen. Informationen zum Herunterladen und Installieren dieses Tools finden Sie unter [Git ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://git-scm.com/downloads){: new_window}.
1. Installieren Sie Node.js und das NPM-Tool (NPM = Node Package Manager). Das NPM-Befehlszeilentool wird als Produktpaket mit Node.js bereitgestellt. Informationen zum Herunterladen und Installieren von Node.js finden Sie unter [Node.js ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://nodejs.org/en/download/){: new_window}.
1. Installieren Sie über die Befehlszeile die Cordova-Befehlszeilentools mithilfe des Befehls **npm install -g cordova**. Dies ist eine Voraussetzung für die Verwendung des Cordova-Push-Plug-ins. Informationen zum Installieren von Cordova und zum Einrichten Ihrer Cordova-App finden Sie unter [Cordova Apache ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cordova.apache.org/#getstarted){: new_window}. Weitere Informationen finden Sie in der [Readme-Datei ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window} für das Cordova-Push-Plug-in.
1. Wechseln Sie in den Ordner, in dem Sie Ihre Cordova-App erstellen möchten, und führen Sie den folgenden Befehl aus, um eine Cordova-Anwendung zu erstellen. Wenn Sie bereits über eine Cordova-App verfügen, fahren Sie mit Schritt 3 fort.
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

## Cordova-Plug-in
{: #cordova_initialize}

Bevor Sie das Cordova-Plug-in für den  {{site.data.keyword.mobilepushshort}}-Service verwenden können, müssen Sie es initialisieren, indem Sie die Anwendungsroute und die Anwendungs-GUID übergeben. Nach der Initialisierung des Plug-ins können Sie die Verbindung zu der Serveranwendung herstellen, die Sie im Bluemix-Dashboard erstellt haben. Das Cordova-Plug-in ist die Oberfläche für die Android- und iOS-Client-SDKs zum Aktivieren einer Cordova-Anwendung für die Kommunikation mit Bluemix-Services.

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


## Geräte registrieren
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

##Nächste Schritte

{: #cordova_register_next}

Erstellen Sie das Projekt und führen Sie es mit den folgenden Befehlen aus:

####Android
{: android-next-steps}

```
cordova build android
```
	{: codeblock}

```
cordova run android
```
	{: codeblock}

####iOS
{: ios-next-steps}

```
cordova build ios
```
	{: codeblock}

```
cordova run ios
```
	{: codeblock}

## Push-Benachrichtigungen in Geräten empfangen
{: #cordova_receive}

Kopieren Sie das folgende Code-Snippet, um Push-Benachrichtigungen auf Geräten zu empfangen.

###JavaScript

Fügen Sie das folgende JavaScript-Code-Snippet in die Webkomponente Ihrer Cordova-Anwendung ein.
```
var showNotification = function(notif) {
  alert(JSON.stringify(notif));
        };
        BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

###Eigenschaften für Android-Benachrichtigungen

Im folgenden Abschnitt sind die Eigenschaften für Android-Benachrichtigungen aufgelistet:

* **message** - Push-Benachrichtigung
* **payload** - JSON-Objekt mit den Nutzdaten einer Benachrichtigung


###Eigenschaften für iOS-Benachrichtigungen

Im folgenden Abschnitt sind die Eigenschaften für iOS-Benachrichtigungen aufgelistet:

* **message** - Push-Benachrichtigung
* **payload** - JSON-Objekt, das die Nutzdaten einer Benachrichtigung enthält
action-loc-key - Diese Zeichenfolge dient als Schlüssel zum Abrufen einer lokalisierten Zeichenfolge in der aktuellen Lokalisierung, die anstelle von `View` als Titel für die entsprechende Schaltfläche verwendet werden soll.
* **badge** - Die Nummer, die als Badge des App-Symbols angezeigt werden soll. Wenn diese Eigenschaft fehlt, wird das Badge nicht geändert. Um das Badge zu entfernen, legen Sie für diese Eigenschaft den Wert 0 fest.
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

## Einfache Push-Benachrichtigungen senden
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

## Nächste Schritte
{: #next_steps_tags}

Nachdem Sie einfache Benachrichtigungen erfolgreich eingerichtet haben, können Sie tagbasierte Benachrichtigungen und erweiterte Optionen konfigurieren.

Fügen Sie die Funktionen des {{site.data.keyword.mobilepushshort}}-Service Ihrer App hinzu.
Informationen zur Verwendung tagbasierter Benachrichtigungen finden Sie in [Tagbasierte Benachrichtigungen](c_tag_basednotifications.html).
Informationen zur Verwendung erweiterter Benachrichtigungsoptionen finden Sie in [Erweiterte Push-Benachrichtigungen aktivieren](t_advance_badge_sound_payload.html).
