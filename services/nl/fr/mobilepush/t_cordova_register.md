---

Copyright :
  Années : 2015, 2016

---

# Enregistrement des périphériques

{: #cordova_register}

Pour enregistrer un périphérique auprès du service Notification push, appelez la méthode d'enregistrement.

Copiez et collez le fragment de code suivant dans votre application Cordova pour enregistrer un périphérique :

```
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	MFPPush.registerDevice({}, success, failure);
```

## Android
{: #cordova_register_android}
Android n'utilise pas le paramètre settings. Si vous générez uniquement un appli Android, indiquez un objet vide. Par exemple :

```
	MFPPush.registerDevice({}, success, failure);
	MFPPush.unregisterDevice(success, failure);
```

##	iOS
{: #cordova_register_ios}
Pour personnaliser les propriétés d'alerte, de badge et de son, ajoutez le fragment de code JavaScript suivant
à la partie Web de votre application Cordova.

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

Vous pouvez accéder au contenu du paramètre de réponse success dans Javascript à l'aide de JSON.parse : **var token = JSON.parse(response).token**


Les clés disponibles sont les suivantes : ```token```, ```userId`` et ```deviceId``.

Le fragment de code JavaScript ci-après montre comment initialiser votre logiciel SDK du client Bluemix Mobile Services, enregistrer un périphérique à l'aide du service Notification push et passer en mode écoute sur les notifications push. Placez ce code dans votre fichier Javascript.



```
//Enregistrez le jeton de périphérique auprès du service Notification push de Bluemix
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
  CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
```

```
//Traitez l'erreur en cas d'échec de l'enregistrement du jeton de périphérique auprès de APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```

Dans **onDeviceReady: function()**.

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
Ajoutez le fragment de code Objective-C suivant à la classe de votre délégué d'application :

```
	// Enregistrez le jeton de périphérique auprès du service Notification push de Bluemix
	- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
	  [[CDVMFPPush sharedInstance] didRegisterForRemoteNotifications:deviceToken];
	}
	// Traitez l'erreur en cas d'échec de l'enregistrement du jeton de périphérique auprès de APNs
	- (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error {
	   [[CDVMFPPush sharedInstance] didFailToRegisterForRemoteNotificationsWithError:error];
	}
```

##Swift
{: #cordova_register_swift}
Ajoutez le fragment de code Swift suivant à la classe de votre délégué d'application :

```     
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
//Traitez l'erreur en cas d'échec de l'enregistrement du jeton de périphérique auprès de APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```

##Etapes suivantes
{: #cordova_register_next}

1. Générez votre projet, puis exécutez-le à l'aide des commandes suivantes :

	* Android - **cordova build android**, puis **cordova run android**

	* iOS - **cordova build ios**, puis **cordova run ios**
1. [Réception de notifications push sur les périphériques](t_cordova_receive.html).
