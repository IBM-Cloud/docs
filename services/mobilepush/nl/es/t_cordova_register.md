---

copyright:
 years: 2015, 2016

---

# Registro de dispositivos

{: #cordova_register}

Para registrar un dispositivo con el Servicio de notificaciones Push, invoque el método de registro.

Copie y pegue el siguiente fragmento de código en la aplicación de Cordova para registrar un dispositivo.

```
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	MFPPush.registerDevice({}, success, failure);
```

## Android
{: #cordova_register_android}
Android no utiliza el parámetro settings. Si solo está creando una aplicación Android, pase un objeto vacío; por ejemplo:

```
	MFPPush.registerDevice({}, success, failure);
	MFPPush.unregisterDevice(success, failure);
```

##	iOS
{: #cordova_register_ios}
Si desea personalizar la alerta, el identificador y las propiedades de sonido, añada el siguiente fragmento de código de JavaScript a la parte web de la aplicación de Cordova.

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

Puede acceder al contenido del parámetro de respuesta de éxito en Javascript utilizando JSON.parse:
**var token = JSON.parse(response).token**


Las claves disponibles son las siguientes: `token`, `userId` y `deviceId`.

El siguiente fragmento de código JavaScript muestra cómo inicializar el SDK del cliente de Bluemix Mobile Services, cómo registrar un dispositivo con el servicio de notificaciones Push y cómo escuchar las notificaciones push. Coloque este código en el archivo Javascript.



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

dentro de la **onDeviceReady: function()**.

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
Añada el siguiente fragmento de código Objective-C a la clase de delegado de la aplicación

```
	// Registre la señal del dispositivo con Bluemix Push Notification Service
	- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
	  [[CDVMFPPush sharedInstance] didRegisterForRemoteNotifications:deviceToken];
	}
	// Manejar el error cuando no ha podido registrar la señal del dispositivo con APNs
	- (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error {
	   [[CDVMFPPush sharedInstance] didFailToRegisterForRemoteNotificationsWithError:error];
	}
```

##Swift
{: #cordova_register_swift}
Añada el siguiente fragmento de código de Swift a la clase de delegado de la aplicación.

```     
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
// Manejar el error cuando no se pueda registrar la señal del dispositivo con APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
   CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```

##Pasos siguientes
{: #cordova_register_next}

1. Cree el proyecto y, a continuación, ejecute el proyecto utilizando los mandatos siguientes:

	* Android: **cordova build android** y, a continuación, **cordova run android**

	* iOS: **cordova build ios** y, a continuación, **cordova run ios**
1. [Recepción de notificaciones push en dispositivos](t_cordova_receive.html).
