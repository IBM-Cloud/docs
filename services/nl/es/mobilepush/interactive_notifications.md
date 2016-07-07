---

copyright:
 years: 2015, 2016

---

# Notificaciones interactivas
{: #interactive-notifications}

Las notificaciones interactivas permiten a los usuarios actuar cuando llega una notificación sin abrir la aplicación. Cuando llega una notificación interactiva, el dispositivo mostrará los botones de acción junto con el mensaje de notificación. Se admiten notificaciones interactivas en dispositivos iOS con versión 8 y posterior. Si se envía una notificación interactiva a dispositivos iOS con una versión anterior a la 8, no se mostrarán las acciones de notificación.


##Envío de notificaciones push interactivas


La notificación interactiva puede enviarse utilizando el panel de control de push o utilizando la API REST (consulte la documentación de la API REST). 

Desde la consola Push: 

En el separador de notificaciones del panel de control de Push, pulse Enviar notificación. Elija los destinatarios de la notificación y pulse Siguiente. En la página para componer notificación, se puede enviar un push interactivo estableciendo el tipo en valor predeterminado o mixto, y especificando el valor de categoría en el separador de opciones avanzadas. Para configurar el valor de categoría en el cliente, consulte la sección Manejo de notificación push interactiva en aplicación iOS nativa. 

## Manejo de notificaciones push interactivas en una aplicación iOS 

Debe seguir estos pasos para recibir notificaciones interactivas:

1. Habilite la funcionalidad de la aplicación para realizar tareas en segundo plano al recibir notificaciones remotas. Este paso es necesario si algunas de las acciones están habilitadas para segundo plano. 
1. En `AppDelegate (application: didRegisterForRemoteNotificationsWithDeviceTokenapplication:)`, establezca las categorías antes de establecer `deviceToken` en `WLPush Object`.

```
	if([application respondsToSelector:@selector(registerUserNotificationSettings:)]){
	 UIUserNotificationType userNotificationTypes = UIUserNotificationTypeNone | UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge;
	      
	 UIMutableUserNotificationAction *acceptAction = [[UIMutableUserNotificationAction alloc] init];
	 acceptAction.identifier = @"OK";
	 acceptAction.title = @"OK";
	      
	 UIMutableUserNotificationAction *rejetAction = [[UIMutableUserNotificationAction alloc] init];
	 rejetAction.identifier = @"NOK";
	 rejetAction.title = @"NOK";
	      
	 UIMutableUserNotificationCategory *cateogory = [[UIMutableUserNotificationCategory alloc] init];
	 cateogory.identifier = @"poll";
	 [cateogory setActions:@[acceptAction,rejetAction] forContext:UIUserNotificationActionContextDefault];
	 [cateogory setActions:@[acceptAction,rejetAction] forContext:UIUserNotificationActionContextMinimal];
	      
	 NSSet *catgories = [NSSet setWithObject:cateogory];
	 [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:userNotificationTypes categories:catgories]];
}
```

1. Implemente el nuevo método callback en AppDelegate:

```
	-(void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forRemoteNotification:(NSDictionary *)userInfo completionHandler:(void (ˆ)())completionHandler
``` 

5. Este nuevo método callback se invoca cuando el usuario pulsa el botón de acción. La implementación de este método puede realizar las tareas asociadas al identificador especificado y ejecutar el bloque en el parámetro `completionHandler`.
