---

copyright:
 years: 2015, 2016

---

# Recepción de notificaciones push en dispositivos
{: #cordova_receive}

Copie y pegue los siguientes fragmentos de código para recibir notificaciones push en dispositivos.

##JavaScript

Añada el siguiente fragmento de código JavaScript a la parte web de la aplicación de Cordova.


```
var notification = function(notification){
    // notification is a JSON object.
    alert(notification.message);
};
MFPPush.registerNotificationsCallback(notification);
```

##Propiedades de notificación de Android

En la sección siguiente se listan las propiedades de notificación de Android:

* message - mensaje de notificación de Push
* payload - objeto JSON que contiene una carga útil de notificación


##Propiedades de notificación de iOS

En la sección siguiente se listan las propiedades de notificación de iOS:

* message - mensaje de notificación de Push
* payload - objeto de JSON que contiene una action-loc-key de carga útil de notificación - La serie se utiliza como una clave para obtener una serie localizada en la localización actual para que la utilice el título del botón derecho en lugar de “Vista".
* badge - El número que se mostrará como el identificador del icono de app. Si falta esta propiedad, el identificador no se modificará. Para eliminar el identificador, establezca el valor de esta propiedad en 0.
* sound - El nombre de un archivo de sonido del paquete de la app de la carpeta Biblioteca/Sonidos del contenedor de datos de la app.

##Objective-C

Añada los siguientes fragmentos de código de Objective-C en la clase de delegado de la aplicación.

```
// Maneje la recepción de una notificación remota
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

##Swift

Añada los siguientes fragmentos de código de Swift a la clase de delegado de la aplicación.

```
// Handle receiving a remote notification
funcapplication(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: ){

    CDVMFPPush.sharedInstance().didReceiveRemoteNotification(userInfo)
}
```

```
// Maneje la recepción de una notificación remota al iniciar
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

    CDVMFPPush.sharedInstance().didReceiveRemoteNotificationOnLaunch(launchOptions)
}

```
Siguiente paso. [Enviar notificaciones push básicas](t_send_push_notifications.html).
