---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}


#Habilitación de notificaciones push avanzadas

Configure un identificador de iOS, un sonido, una carga útil de JSON adicional, notificaciones accionables y notificaciones retenidas.

## Configure un sonido y carga útil e identificador iOS
{: #badge-sound-payload}

Configure un identificador de iOS, un sonido y la carga útil adicional de JSON.

1. En el panel de control Notificaciones Push, vaya al
                        separador **Notificaciones**.
2. Vaya a la sección **Campos opcionales** para configurar las
                    siguientes características de notificaciones push. 
	- **Archivo de sonido**: Escriba una serie que apunte al archivo de sonido
                            de la app móvil. En la carga útil, especifique el nombre de serie del
                            archivo de sonido a utilizar.
	- **Identificador iOS**: Para dispositivos iOS, el número
                            que se mostrará como el identificador del icono de app. Si falta esta propiedad, el
                            identificador no se modificará. Para eliminar el identificador, establezca el valor de esta
                            propiedad en 0.
	
	


###Android

```
"settings": {
     "gcm" : {
     "sound":"tt.wav",
	  }
 }  
```
	
	
###iOS

```
"settings": {
     "apns" : {
      "badge": 10,
	      "sound": "tt.wav",
	  }
}
``` 		
**Carga útil adicional**: Esta carga útil puede ser cualquier
                            par de valores de claves y debe ser un objeto JSON que desee enviar con la
                            notificación push.

```
{"key":"value", "key2":"value2"}
```


## Retención de notificaciones de Android 
{: #hold-notifications-android}

Cuando su aplicación entre en segundo plano, probablemente querrá enviar por push para
                            contener notificaciones de volver que se envían a la aplicación. Para retener notificaciones, invoque el método hold() en el método onPause() de la actividad que maneja las notificaciones push.

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```

## Habilitación de notificaciones de iOS accionables  
{: #enable-actionable-notifications-ios}

A diferencia de las notificaciones push tradicionales, estas solicitan a los usuarios que realicen una selección al recibir la alerta de notificación sin abrir la app. Utilice las instrucciones siguientes para habilitar notificaciones push en la aplicación.

1. Cree una acción de respuesta del usuario.

   Objective-C

	```
	// For Objective-C
	UIMutableUserNotificationAction *acceptAction = [[UIMutableUserNotificationAction alloc] init];
	    acceptAction.identifier = @"ACCEPT_ACTION";
	    acceptAction.title = @"Accept";
	     /* Optional properties
	     acceptAction.destructive = NO;
	  acceptAction.authenticationRequired = NO; */
	  
	 ```
   Swift

	```
	//For Swift
	let acceptAction = UIMutableUserNotificationAction()
	acceptAction.identifier = "ACCEPT_ACTION"
	acceptAction.title = "Accept"
	acceptAction.destructive = false
	acceptAction.authenticationRequired = false
	acceptAction.activationMode = UIUserNotificationActivationMode.Foreground*/
	```
	
	```
	//For Swift
	let declineAction = UIMutableUserNotificationAction()
	declineAction.identifier = "DECLINE_ACTION"
	declineAction.title = "Decline"
	declineAction.destructive = true
	declineAction.authenticationRequired = false
	declineAction.activationMode = UIUserNotificationActivationMode.Background
	```

2. Cree la categoría de notificaciones y configure una acción. **UIUserNotificationActionContextDefault** o
                **UIUserNotificationActionContextMinimal** son contextos válidos.

	Objective-C

	```
	// For Objective-C
	UIMutableUserNotificationCategory *callCat = [[UIMutableUserNotificationCategory alloc] init];
	    callCat.identifier = @"POLL_CATEGORY";
	    [callCat setActions:@[acceptAction, declineAction] forContext:UIUserNotificationActionContextDefault];
	```    

	Swift

	```
	// For Swift
	let pushCategory = UIMutableUserNotificationCategory()
	pushCategory.identifier = "TODO_CATEGORY"
	pushCategory.setActions([acceptAction, declineAction], forContext: UIUserNotificationActionContext.Default)
	```

1. Cree el valor de notificación y asigne las categorías desde el paso anterior.

	Objective-C

	```
	// For Objective-C
	NSSet *categories = [NSSet setWithObjects:callCat, nil];
	```

	Swift

	```
	// For Swift
	let categories = NSSet(array:[pushCategory]);
	```

1. Cree una notificación remota o local y asígnele la identidad de la categoría.

	Objective-C

	```
	//For Objective-C

	[[UIApplication sharedApplication] registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge) categories:categories]];

	[[UIApplication sharedApplication] registerForRemoteNotifications];
	```

	Swift

	```
	//For Swift
	let notificationTypes: UIUserNotificationType = UIUserNotificationType.Badge | UIUserNotificationType.Alert | UIUserNotificationType.Sound
	let notificationSettings: UIUserNotificationSettings = UIUserNotificationSettings(forTypes: notificationTypes, categories: categories)

	application.registerUserNotificationSettings(notificationSettings)
	application.registerForRemoteNotifications()
	```
	
## Gestión de notificaciones de iOS accionables  
{: #actionable-notifications}

Al recibir una notificación que necesita reacciones, el control se pasa al siguiente método según el identificador seleccionado.

###Objective-C

```
(void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forRemoteNotification:
(UILocalNotification *)notification completionHandler:(void (^)())completionHandler
{
  NSLog(@"actionable notification received.");
  //must call completion handler when finished
  completionHandler();
}
```

###Swift
 
```
func application(application: UIApplication, handleActionWithIdentifier identifier: String?, forRemoteNotification userInfo: [NSObject : AnyObject], completionHandler: () -> Void) {
      //must call completion handler when finished
      completionHandler()
  }
```    
    
