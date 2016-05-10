---

copyright:
 years: 2015, 2016

---

# Registrazione di dispositivi

{: #cordova_register}

Per registrare un dispositivo con il Push Notification Service, richiama il metodo.

Copia e incolla il seguente frammento di codice nella tua applicazione Cordova per registrare
                    un dispositivo.

```
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	MFPPush.registerDevice({}, success, failure);
```

## Android
{: #cordova_register_android}
Android non utilizza il parametro delle impostazioni. Se stai soltanto creando un'applicazione Android, invia un oggetto vuoto; ad esempio:

```
	MFPPush.registerDevice({}, success, failure);
	MFPPush.unregisterDevice(success, failure);
```

##	iOS
{: #cordova_register_ios}
Se vuoi personalizzare le proprietà di avviso, badge e audio,
                    aggiungi il seguente frammento di codice JavaScript alla parte web della tua applicazione
                    Cordova.

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

Puoi accedere ai contenuti del parametro di risposta con esito positivo in Javascript utilizzando JSON.parse:
**var token = JSON.parse(response).token**


Le chiavi disponibili sono le seguenti: ```token```, ```userId`` e ```deviceId``.

Il seguente frammento di codice JavaScript mostra come inizializzare il tuo Bluemix Mobile Services client SDK, registra un dispositivo ed è in ascolto per le notifiche push. Inserisci questo codice nel tuo file Javascript.



```
//Registra il token di dispositivo presso il Bluemix Push Notification Service
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
  CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
```

```
//Gestisci l'errore in caso di registrazione del token di dispositivo presso APNS non riuscita
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
Aggiungi il seguente frammento di codice Objective-C alla classe delegato della tua applicazione

```
	// Registra il token di dispositivo presso il Bluemix Push Notification Service
	- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
	  [[CDVMFPPush sharedInstance] didRegisterForRemoteNotifications:deviceToken];
	}
	// Gestisci l'errore in caso di registrazione del token di dispositivo presso APNS non riuscita
	- (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error {
	   [[CDVMFPPush sharedInstance] didFailToRegisterForRemoteNotificationsWithError:error];
	}
```

##Swift
{: #cordova_register_swift}
Aggiungi il seguente frammento di codice Swift alla classe delegato della tua applicazione.

```     
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
//Gestisci l'errore in caso di registrazione del token di dispositivo presso APNS non riuscita
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```

##Passi successivi
{: #cordova_register_next}

1. Crea il tuo progetto e quindi eseguilo utilizzando i seguenti comandi:

	* Android - **cordova build android**  e quindi **cordova run android**

	* iOS - **cordova build ios** e quindi **cordova run ios**
1. [Ricezione di notifiche di push sui dispositivi](t_cordova_receive.html).
