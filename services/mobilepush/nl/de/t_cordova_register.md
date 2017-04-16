---

copyright:
 years: 2015, 2016

---

# Geräte registrieren

{: #cordova_register}

Rufen Sie die Registrierungsfunktion auf, um ein Gerät für Push Notifications Service zu registrieren.

Kopieren Sie das folgende Code-Snippet und fügen Sie es in Ihre Cordova-Anwendung
ein, um ein Gerät zu registrieren.

```
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	MFPPush.registerDevice({}, success, failure);
```

## Android
{: #cordova_register_android}
Android verwendet den Einstellungsparameter nicht. Wenn Sie nur eine Android-App erstellen, übergeben Sie ein leeres Objekt. Beispiel:

```
	MFPPush.registerDevice({}, success, failure);
	MFPPush.unregisterDevice(success, failure);
```

##	iOS
{: #cordova_register_ios}
Wenn Sie die Eigenschaften für Alert, Badge und Audio anpassen möchten, fügen Sie
das folgende JavaScript-Code-Snippet zur Webkomponente Ihrer Cordova-Anwendung hinzu.

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



##JavaScript
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

## Objective-C
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

##Swift
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

1. Erstellen Sie das Projekt und führen Sie es mit den folgenden Befehlen aus:

	* Android: **cordova build android** und anschließend **cordova run android**

	* iOS: **cordova build ios** und anschließend **cordova run ios**
1. [Push-Benachrichtigungen
in Geräten empfangen](t_cordova_receive.html)
