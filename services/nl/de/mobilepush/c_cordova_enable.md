---

copyright:
 years: 2015, 2016

---

# Cordova-Anwendungen für den Empfang von Push-Benachrichtigungen aktivieren
{: #cordova_enable}

Cordova ist eine Plattform zum Erstellen von Hypridanwendungen mit JavaScript, CSS und HTML. {{site.data.keyword.mobilepushshort}} unterstützt die Entwicklung von iOS- und Android-Anwendungen, die auf Cordova basieren.

Aktivieren Sie Cordova-Anwendungen für den Empfang von Push-Benachrichtigungen und für das Senden von Push-Benachrichtigungen an Ihre Geräte.




## Cordova Push-Plug-in installieren
{: #cordova_install}

Installieren und verwenden Sie das Client-Push-Plug-in für die weitere Entwicklung Ihrer Cordova-Anwendungen. Dieser Befehl installiert auch das Cordova Core-Plug-in, das Ihre Verbindung zu Bluemix initialisiert.

### Vorbemerkungen

1. Laden Sie die aktuellen Version für das Android Studio-SDK und Xcode herunter.
1. Richten Sie den Emulator ein. Verwenden Sie für Android Studio einen Emulator, der die Google Play-API unterstützt.
1. Installieren Sie das Git-Befehlszeilentool. Stellen Sie unter Windows sicher, dass Sie die Option zum Ausführen von Git über die Windows-Eingabeaufforderung auswählen. Informationen zum Herunterladen und Installieren dieses Tools finden Sie unter [Git](https://git-scm.com/downloads).

1. Installieren Sie Node.js und das NPM-Tool (NPM = Node Package Manager). Das NPM-Befehlszeilentool wird als Produktpaket mit Node.js bereitgestellt. Informationen zum Herunterladen und Installieren von Node.js finden Sie unter [Node.js](https://nodejs.org/en/download/).
1. Installieren Sie über die Befehlszeile die Cordova-Befehlszeilentools mithilfe des Befehls **npm install -g cordova**. Dies ist eine Voraussetzung für die Verwendung des Cordova-Plug-ins. Informationen zum Installieren von Cordova und zum Einrichten Ihrer Cordova-App finden Sie unter [Cordova Apache](https://cordova.apache.org/#getstarted).

 **Hinweis**: Die Readme-Datei für das Cordova Push-Plug-in finden Sie unter [https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push).

1. Wechseln Sie in den Ordner, in dem Sie Ihre Cordova-App erstellen möchten, und führen Sie den folgenden Befehl aus, um eine Cordova-Anwendung zu erstellen. Wenn Sie bereits über eine Cordova-App verfügen, fahren Sie mit Schritt 3 fort.

 ```
cordova create your_app_name
	cd your_app_name
```
1. Optional: Bearbeiten Sie die Datei **config.xml** und ersetzen Sie im Element <name> den Standardnamen 'HelloCordova' durch einen eigenen Namen.

	**Hinweis**: Stellen Sie sicher, dass Sie die richtige Bundle-ID angeben. Falls Sie dies nicht tun, werden in Xcode die folgenden Fehlernachrichten angezeigt.
	* The executable was signed with invalid entitlements (Die ausführbare Funktion ist mit ungültigen Berechtigungen signiert).
	* The entitlements specified in your application’s Code Signing Entitlements file do not match those specified in your provisioning profile (Die in der Berechtigungsdatei für die Codeunterzeichnung Ihrer Anwendung angegebenen Berechtigungen stimmen nicht mit den angegebenen Berechtigungen in Ihrem Bereitstellungsprofil überein).

	Um dieses Problem zu beheben, geben Sie korrekte Bundle-ID in Xcode oder in der Datei **config.xml** Ihrer Cordova-App an.

1. Fügen Sie die Mindestversion der unterstützten API oder die Bereitstellungszieldeklaration zur Datei 'config.xml' Ihrer Cordova-Anwendung hinzu: Der Wert für 'minSdkVersion' muss größer als 15 sein. Der Wert für 'targetSdkVersion' muss immer das neueste Android-SDK angeben, das bei Google verfügbar ist.
	* **Android**:  Öffnen Sie die Datei 'config.xml' in einem Texteditor und aktualisieren Sie das
   Element `<platform name="android">` mit der SDK-Mindestversion und der SDK-Zielversion:

	```
	<!-- add deployment target declaration -->
	<platform name="android">  
			  <preference name="android-minSdkVersion" value="15" />
			  <preference name="android-targetSdkVersion" value="23" />
			</platform>
	```
   * **iOS**: Aktualisieren Sie das Element <platform name="ios"> mit einer Bereitstellungszieldeklaration:

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- other properties -->
	</ platform>
	```

1. Fügen Sie über die Cordova-Befehlszeilenschnittstelle (CLI) Ihre Plattform (iOS und/oder Android) mit den folgenden Befehlen hinzu.

	```
	cordova platform add ios@3.9.0
	cordova platform add android
	```
1. Geben Sie im Stammverzeichnis Ihrer Cordova-Anwendung den folgenden Befehl ein, um das Cordova Push-Plug-in **cordova plugin add ibm-mfp-push** zu installieren.

	Je nachdem, welche Plattformen Sie hinzugefügt haben, sehen Sie eine Anzeige
ähnlich der folgenden:

	```
	Installing "ibm-mfp-push" for android
	Installing "ibm-mfp-push" for ios
	```
1. Überprüfen Sie in *eigenes_anwendungsstammverzeichnis* mit dem Befehl **cordova plugin list**, dass die Plug-ins Cordova Core und Cordova Push erfolgreich installiert wurden.

	Je nachdem, welche Plattformen Sie hinzugefügt haben, sehen Sie eine Anzeige ähnlich der folgenden:

	```
	ibm-mfp-core 1.0.0 "MFPCore"
	ibm-mfp-push 1.0.0 “MFPPush"
	```
1. (nur iOS): Konfigurieren Sie Ihre iOS-Entwicklungsumgebung.
	a. Öffnen Sie die Datei 'ihr_app-name.xcodeproj' im Verzeichnis *ihr_app-name***/platforms/ios** mit Xcode.

	b. Fügen Sie den Bridging-Header hinzu. Rufen Sie **Build settings > Swift Compiler - Code Generation > Objective-C Bridging Header** auf und fügen Sie den folgenden Pfad hinzu: *ihr_projektname***/Plugins/ibm-mfp-core/Bridging-Header.h**.

	c. Fügen Sie die Frameworks-Parameter hinzu. Rufen Sie **Build Settings > Linking > Runpath Search Paths** auf und fügen Sie die folgenden Parameter hinzu:
	```
	@executable_path/Frameworks
	```
	d. Entfernen Sie die Kommentarzeichen aus den folgenden Push-Importanweisungen im Bridging-Header. Wechseln Sie in das Verzeichnis *ihr_projektname***/Plugins/ibm-mfp-core/Bridging-Header.h**.

	```
	//#import <IMFPush/IMFPush.h>
	//#import <IMFPush/IMFPushClient.h>
	//#import <IMFPush/IMFResponse+IMFPushCategory.h>
	```
	e. Erstellen Sie die Anwendung und führen Sie sie mit Xcode aus.
1. (Nur Android): Erstellen Sie Ihr Android-Projekt mit dem folgenden Befehl:
**cordova build android**.

	**Hinweis**: Bevor Sie das Projekt in Android Studio öffnen, müssen Sie zuerst die Cordova-Anwendung über die Cordova-Befehlszeilenschnittstellen erstellen. Andernfalls kann es zu Buildfehlern kommen.


## Cordova-Plug-in
{: #cordova_initialize}

Bevor Sie das Cordova-Plug-in für Push Notifications Service verwenden können, müssen Sie es initialisieren, indem Sie die Anwendungsroute und die Anwendungs-GUID übergeben. Nach der Initialisierung des Plug-ins können Sie die Verbindung zu der Serveranwendung herstellen, die Sie im Bluemix-Dashboard erstellt haben. Das Cordova-Plug-in ist die Oberfläche für die Android- und iOS-Client-SDKs zum Aktivieren einer Cordova-Anwendung für die Kommunikation mit Bluemix-Services.

1. Initialisieren Sie 'BMSClient', indem Sie das folgende Code-Snippet kopieren und in Ihre Haupt-JavaScript-Datei (die für gewöhnlich im Verzeichnis **www/js** gespeichert ist) einfügen.

	```
	BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	```
1. Ändern Sie das Code-Snippet so, dass die Parameter für die Routen und Anwendungs-GUID von Bluemix verwendet werden. Klicken Sie auf den Link **Mobile Optionen** in Ihrem Bluemix-Anwendungsdashboard, um die Anwendungsroute und die App-GUID abzurufen. Verwenden Sie die Werte für die Route und die App-GUID als Parameter in Ihrem Code-Snippet für `BMSClient.initialize`.

	**Hinweis**: Wenn Sie beispielsweise mit der Cordova-CLI eine Cordova-App erstellt haben, erstellt Cordova den Befehl 'app-name', speichert diesen Javascript-Code in der Datei **index.js** hinter der Funktion `app.receivedEvent` in der Funktion `onDeviceReady: function()` zum Initialisieren des BMS-Clients.

```
onDeviceReady: function() {
    app.receivedEvent('deviceready');
	    BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	    },
```

## Geräte registrieren
{: #cordova_register}

Rufen Sie die Registrierungsfunktion auf, um ein Gerät für Push Notifications Service zu registrieren.

Kopieren Sie das folgende Code-Snippet und fügen Sie es in Ihre Cordova-Anwendung ein, um ein Gerät zu registrieren.

```
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	MFPPush.registerDevice({}, success, failure);
```

### Android
{: #cordova_register_android}
Android verwendet den Einstellungsparameter nicht. Wenn Sie nur eine Android-App erstellen, übergeben Sie ein leeres Objekt. Beispiel:

```
	MFPPush.registerDevice({}, success, failure);
	MFPPush.unregisterDevice(success, failure);
```

### iOS
{: #cordova_register_ios}
Wenn Sie die Eigenschaften für Alert, Badge und Audio anpassen möchten, fügen Sie das folgende JavaScript-Code-Snippet zur Webkomponente Ihrer Cordova-Anwendung hinzu.

```
	var settings = {
	   ios: {
	       alert: true,
	       badge: true,
	       sound: true
	   }
	}
	MFPPush.registerDevice(settings, success, failure);
```



### JavaScript
{: #cordova_register_js}

```
MFPPush.registerDevice({}, success, failure);
```

Sie können mit JSON.parse auf den Inhalt des Antwortparameters mit der Funktion 'success' in Javascript using JSON.parse:
**var token = JSON.parse(response).token**


Es sind folgende Schlüssel verfügbar: `token`, `userId` und `deviceId`.

Das folgende JavaScript-Code-Snippet zeigt, wie Sie das Bluemix Mobile Services-Client-SDK initialisieren, ein Gerät für den Push Notifications Service registrieren und Push-Benachrichtigungen überwachen können. Sie fügen diesen Code in Ihre Javascript-Datei ein.



```
//Register device token with Bluemix Push Notification Service
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
  CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
```

```
//Handle error when failed to register device token with APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```

in **onDeviceReady: function()**.

```
onDeviceReady: function() {
     app.receivedEvent('deviceready');
     BMSClient.initialize("https://http://myroute_mybluemix.net","my_appGuid");
     var success = function(message) { console.log("Success: " + message); };
     var failure = function(message) { console.log("Error: " + message); };
     var settings = {
         ios: {
             alert: true,
             badge: true,
             sound: true
         }   
     };
     MFPPush.registerDevice(settings, success, failure);
     var notification = function(notif){
         alert (notif.message);
     };
     MFPPush.registerNotificationsCallback(notification);

 }
```

### Objective-C
{: #cordova_register_objective}
Fügen Sie das folgende Objective-C-Code-Snippet zur Klasse 'delegate' Ihrer Anwendung hinzu.

```
	// Register the device token with Bluemix Push Notification Service
	- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
	  [[CDVMFPPush sharedInstance] didRegisterForRemoteNotifications:deviceToken];
	}
	// Handle error when failed to register device token with APNs
	- (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error {
	   [[CDVMFPPush sharedInstance] didFailToRegisterForRemoteNotificationsWithError:error];
	}
```

###Swift
{: #cordova_register_swift}
Fügen Sie das folgende Swift-Code-Snippet zur Klasse 'delegate' Ihrer Anwendung hinzu.

```     
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
// Handle error when failed to register device token with APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
   CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```

##Nächste Schritte

{: #cordova_register_next}

Erstellen Sie das Projekt und führen Sie es mit den folgenden Befehlen aus:

	* Android: **cordova build android** und anschließend **cordova run android**

	* iOS: **cordova build ios** und anschließend **cordova run ios**



## Push-Benachrichtigungen in Geräten empfangen
{: #cordova_receive}

Kopieren Sie die folgenden Code-Snippets und fügen Sie sie ein, um Push-Benachrichtigungen
auf Geräten zu empfangen.

###JavaScript

Fügen Sie das folgende JavaScript-Code-Snippet in die Webkomponente Ihrer Cordova-Anwendung ein.


```
var notification = function(notification){
    // notification is a JSON object.
    alert(notification.message);
};
MFPPush.registerNotificationsCallback(notification);
```

###Eigenschaften für Android-Benachrichtigungen

Im folgenden Abschnitt sind die Eigenschaften für Android-Benachrichtigungen aufgelistet:

* message - Push-Benachrichtigung.
* payload - JSON-Objekt mit den Nutzdaten einer Benachrichtigung


###Eigenschaften für iOS-Benachrichtigungen

Im folgenden Abschnitt sind die Eigenschaften für iOS-Benachrichtigungen aufgelistet:

* message - Push-Benachrichtigung.
* payload - JSON-Objekt mit den Nutzdaten einer Benachrichtigung.
action-loc-key - Diese Zeichenfolge dient als Schlüssel zum Abrufen einer lokalisierten Zeichenfolge in der aktuellen Lokalisierung, die anstelle von 'View' als Titel für die rechte Schaltfläche verwendet werden soll.
* badge - Die Nummer, die als Badge des App-Symbols angezeigt werden soll. Wenn diese Eigenschaft fehlt, wird das Badge nicht geändert. Um das Badge zu entfernen, legen Sie für diese Eigenschaft den Wert 0 fest.
* sound - Der Name einer Audiodatei im App-Bundle oder im Ordner 'Library/Sounds' des Datencontainers der App.

###Objective-C

Fügen Sie die folgenden Objective-C-Code-Snippets zur Klasse 'delegate' Ihrer Anwendung hinzu.

```
// Handle receiving a remote notification
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler {

 [[CDVMFPPush sharedInstance] didReceiveRemoteNotification:userInfo];
}
```

```
// Handle receiving a remote notification on launch
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

    [[CDVMFPPush sharedInstance] didReceiveRemoteNotificationOnLaunch:launchOptions];
}
```

###Swift

Fügen Sie die folgenden Swift-Code-Snippets zur Klasse 'delegate' Ihrer Anwendung hinzu.

```
// Handle receiving a remote notification
funcapplication(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: ){

    CDVMFPPush.sharedInstance().didReceiveRemoteNotification(userInfo)
}
```

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

    CDVMFPPush.sharedInstance().didReceiveRemoteNotificationOnLaunch(launchOptions)
}

```


{: #push-send-notifications}
## Einfache Push-Benachrichtigungen senden


Nach dem Entwickeln Ihrer Anwendungen können Sie einfache Push-Benachrichtigungen (ohne Tags, Badges, zusätzliche Nutzdaten oder Audiodateien) senden.


Senden Sie einfache Push-Benachrichtigungen.

1. Wählen Sie unter **Zielgruppe auswählen** eine der folgenden Zielgruppen aus: **Alle Geräte** oder die Plattform **Nur iOS-Geräte** oder **Nur Android-Geräte**. 

	**Hinweis**: Wenn Sie die Option **Alle Geräte** auswählen, erhalten alle Geräte, die Push-Benachrichtigungen subskribiert haben, Ihre Benachrichtigung.

	![Anzeige 'Benachrichtigungen'](images/tag_notification.jpg)

2. Geben Sie in **Eigene Benachrichtigung erstellen** die gewünschte Nachricht ein und klicken Sie auf **Senden**.
3. Überprüfen Sie, ob die Geräte Ihre Benachrichtigung empfangen haben.

	Der folgende Screenshot zeigt ein Alertfeld bei der Verarbeitung einer Push-Benachrichtigung im Vordergrund eines Android- und iOS-Geräts.

	![Push-Benachrichtigung im Vordergrund auf einem Android-Gerät](images/Android_Screenshot.jpg)

	![Push-Benachrichtigung im Vordergrund auf einem iOS-Gerät](images/iOS_Screenshot.jpg)

	Der folgende Screenshot zeigt eine Push-Benachrichtigung im Hintergrund auf einem Android-Gerät.
	![Push-Benachrichtigung im Hintergrund auf einem Android-Gerät](images/background.jpg)



## Nächste Schritte
{: #next_steps_tags}

Nachdem Sie einfache Benachrichtigungen erfolgreich eingerichtet haben, können Sie tagbasierte Benachrichtigungen und erweiterte Optionen konfigurieren.

Fügen Sie die folgenden Funktionen von Push Notifications Service zu Ihrer App hinzu.
Informationen zur Verwendung tagbasierter Benachrichtigungen finden Sie in [Tagbasierte Benachrichtigungen](c_tag_basednotifications.html).
Informationen zur Verwendung erweiterter Benachrichtigungen finden Sie in [Erweiterte Push-Benachrichtigungen](t_advance_notifications.html).
