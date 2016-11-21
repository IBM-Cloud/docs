---

copyright:
 years: 2015, 2016

---

# Notificaciones interactivas
{: #interactive-notifications}
Última actualización: 17 de octubre de 2016
{: .last-updated}

Las notificaciones interactivas permiten a los usuarios actuar cuando llega una notificación sin abrir la aplicación. Cuando llega una notificación interactiva, el dispositivo mostrará los botones de acción junto con el mensaje de notificación. Se admiten notificaciones interactivas en dispositivos iOS con versión 8 y posterior. Si se envía una notificación interactiva a dispositivos iOS con una versión anterior a la 8, no se mostrarán las acciones de notificación.

##Envío de {{site.data.keyword.mobilepushshort}} interactivas


La notificación interactiva puede enviarse utilizando el panel de control de push o utilizando la [Documentación de la API REST](t_restapi.html).

Desde la consola Push: 

1. En el separador de notificaciones del panel de control de Push, pulse **Enviar notificación**. 
2. Elija los destinatarios de la notificación y pulse **Siguiente**. 
3. En la página para crear notificaciones se puede enviar un push interactivo estableciendo Tipo en Predeterminado o Mixto y especificando Valor de categoría en el separador Opciones avanzadas. Para configurar el valor de categoría en el cliente, consulte la sección **Manejo de {{site.data.keyword.mobilepushshort}} interactivas** en aplicaciones iOS nativas.

## Manejo de {{site.data.keyword.mobilepushshort}} interactivas en una aplicación iOS

Siga estos pasos para recibir notificaciones interactivas:

1. Habilite la funcionalidad de la aplicación para realizar tareas en segundo plano al recibir notificaciones remotas. Este paso es necesario si algunas de las acciones están habilitadas para segundo plano.
1. En AppDelegate (application: didRegisterForRemoteNotificationsWithDeviceTokenapplication:), establezca las categorías antes de establecer `deviceToken` en `WLPush Object`.
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
	{: codeblock}

1. Implemente el nuevo método callback en AppDelegate:
	```
	 -(void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forRemoteNotification:(NSDictionary *)userInfo completionHandler:(void (ˆ)())completionHandler
	```
	{: codeblock} 
5. Este nuevo método callback se invoca cuando el usuario pulsa el botón de acción. La implementación de este método debe realizar tareas asociadas con el identificador especificado y ejecutar el bloque en el parámetro `completionHandler`.
