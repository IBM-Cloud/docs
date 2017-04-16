---

copyright:
 years: 2015, 2016

---

# Registrando Dispositivos

{: #cordova_register}

Para registrar um dispositivo no Serviço de notificação push, chame o método de
registro.

Copie e cole o fragmento de código a seguir em seu aplicativo
Cordova para registrar um dispositivo.

```
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	MFPPush.registerDevice({}, success, failure);
```

## Android
{: #cordova_register_android}
O Android não usa o parâmetro de definições. Se você estiver somente compilando um app
Android, passe um objeto vazio; por exemplo:

```
	MFPPush.registerDevice({}, success, failure);
	MFPPush.unregisterDevice(success, failure);
```

##	iOS
{: #cordova_register_ios}
Se deseja customizar o alerta, badge e propriedades de som,
inclua o seguinte fragmento de código JavaScript na
web part de seu aplicativo Cordova.

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



## JavaScript
{: #cordova_register_js}

```
MFPPush.registerDevice({}, success, failure);
```

É possível acessar o conteúdo do parâmetro de resposta de sucesso em Javascript usando JSON.parse:
**var token = JSON.parse(response).token**


As chaves disponíveis são como a seguir: `token`, `userId` e `deviceId`.

O fragmento de código JavaScript a seguir mostra como inicializar o SDK do cliente Bluemix
Mobile Services, registrar um dispositivo no Serviço de notificação push e atender a
notificações push. Coloque esse código em seu arquivo Javascript.



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

within the **onDeviceReady: function()**.

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
Inclua o fragmento de código Objective-C a seguir em sua classe de delegação de aplicativo.

```
	// Register the device token with Bluemix Push Notification Service
	- (void)application:(UIApplication *)application
didRegisterForRemoteNotificationsWithDeviceToken:(NSData
*)deviceToken {
	  [[CDVMFPPush sharedInstance] didRegisterForRemoteNotifications:deviceToken];
	}
	// Handle error when failed to register device token with APNs
	- (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error {
	   [[CDVMFPPush sharedInstance] didFailToRegisterForRemoteNotificationsWithError:error];
	}
```

## Swift
{: #cordova_register_swift}
Inclua o seguinte fragmento de código Swift em sua classe de
delegação de aplicativo.

```     
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
// Handle error when failed to register device token with APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
   CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```

## Próximas Etapas
{: #cordova_register_next}

1. Compile seu projeto e, em seguida, execute-o usando os comandos a seguir:

	* Android - **cordova build android** e depois **cordova run android**

	* iOS - **cordova build ios** e depois **cordova run ios**
1. [Recebendo
notificações push em dispositivos](t_cordova_receive.html).
