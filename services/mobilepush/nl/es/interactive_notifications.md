---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Notificaciones interactivas y silenciosas  
{: #interactive-notifications}
Última actualización: 3 de marzo de 2017
{: .last-updated}

Las notificaciones interactivas permiten a los usuarios responder a notificaciones sin tener que abrir la aplicación. Cuando llega una notificación interactiva, el dispositivo mostrará los botones de acción junto con el mensaje de notificación. Se admiten notificaciones interactivas en dispositivos iOS con versión 8 o posteriores. Para notificaciones interactivas enviadas a dispositivos iOS anteriores a la versión 8, no se mostrarán las acciones de notificación.

## Envío de notificaciones interactivas
{: #send_interactive_notifications}

La notificación interactiva puede enviarse utilizando el panel de control de push o utilizando la [Documentación de la API REST](t_restapi.html).

Desde la consola de {{site.data.keyword.mobilepushshort}}: 

1. En el separador de notificaciones del panel de control de Push, pulse **Enviar notificación**. 
2. Elija los destinatarios de la notificación y pulse **Siguiente**. 
3. En la página para crear notificaciones se puede enviar un push interactivo estableciendo Tipo en Predeterminado o Mixto y especificando Valor de categoría en el separador Opciones avanzadas. Para configurar el valor de categoría en el cliente, consulte la sección **Manejo de {{site.data.keyword.mobilepushshort}} interactivas** en aplicaciones iOS nativas.

## Manejo de notificaciones interactivas en una aplicación iOS
{: #send_interactive_notifications_ios}

### Swift
{: #send_interactive_notifications_ios_swift}

Siga estos pasos para recibir notificaciones interactivas:

1. Habilite la funcionalidad de la aplicación para realizar tareas en segundo plano al recibir notificaciones remotas. 
1. Inicialice el SDK `BMSPush` con su categoría de acción.
	```
	let myBMSClient = BMSClient.sharedInstance
	myBMSClient.initialize(bluemixRegion: BMSClient.Region.usSouth)
	let push =  BMSPushClient.sharedInstance
    let actionOne = BMSPushNotificationAction(identifierName: "FIRST", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
   	let actionTwo = BMSPushNotificationAction(identifierName: "SECOND", buttonTitle: "Reject", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
   	let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
   	let notifOptions = BMSPushClientOptions(categoryName: [category])
	push.initializeWithAppGUID(appGUID: "YOUR_APP_GUID", clientSecret:"YOUR_APP_CLIENT_SECRET", options: notifOptions)
	```
		{: codeblock}

1. Implemente el nuevo método callback en AppDelegate:
	```
	 func userNotificationCenter(_ center: UNUserNotificationCenter,
       didReceive response: UNNotificationResponse,
       withCompletionHandler completionHandler: @escaping () -> Void) {
            switch response.actionIdentifier {
		    case "FIRST":
		      print("FIRST")
		    case "SECOND":
		      print("SECOND")  
		    default:
		      print("Unknown action")
		    }
		completionHandler
	}
	```
	{: codeblock} 
5. Este nuevo método callback se invoca cuando el usuario pulsa el botón de acción. La implementación de este método debe realizar tareas asociadas con el identificador especificado y ejecutar el bloque en el parámetro `completionHandler`.


### Cordova
{: #send_interactive_notifications_ios_cordova}

Para recibir una notificación accionable en una aplicación de iOS Cordova, siga estos pasos:

1. Añada el campo de categoría dentro del método `BMSPush.initialize`.
   ```
	var category =  {"Category_Name":[{"IdentifierName_1":"actionName_1"},{"IdentifierName_2":"actionName_2"}]}
       BMSPush.initialize(appGUID,clientSecret,category);
    ```
	{: codeblock} 
2. Implemente el nuevo método callback en AppDelegate.
3. Este nuevo método callback se invoca cuando el usuario pulsa el botón de acción. La implementación de este método debe realizar tareas asociadas con el identificador especificado y ejecutar el bloque en el parámetro completionHandler.

## Manejo de notificaciones silenciosas para iOS
{: #send_silent_notifications_for_ios}

Las notificaciones silenciosas no aparecen en la pantalla del dispositivo. Estas notificaciones se reciben mediante la aplicación en segundo plano, que activa la aplicación durante 30 segundos para realizar la tarea en segundo plano. Puede que el usuario no tenga en cuenta la llegada de la notificación. Para enviar notificaciones silenciosas para iOS, utilice la [API REST ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://mobile.{DomainName}/imfpush/){: new_window}.   

1. Para enviar notificaciones push silenciosas, implemente el siguiente método en el archivo `appDelegate.m` del proyecto. En Swift, el valor `contentAvailable` que envía el servidor para las instalaciones silenciosas es igual a 1.
```
// Para Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       let contentAPS = userInfo["aps"] as [NSObject : AnyObject]
       if let contentAvailable = contentAPS["content-available"] as? Int {
           //silent or mixed push
           if contentAvailable == 1 {
               completionHandler(UIBackgroundFetchResult.NewData)
           } else {
               completionHandler(UIBackgroundFetchResult.NoData)
           }
       } else {
    //Default notification 
           completionHandler(UIBackgroundFetchResult.NoData)
       }
    }
```
	{: codeblock}

