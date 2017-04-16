---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Notificaciones interactivas
{: #interactive-notifications}
Última actualización: 23 de enero de 2017
{: .last-updated}

Las notificaciones interactivas permiten a los usuarios responder a notificaciones sin tener que abrir la aplicación. Cuando llega una notificación interactiva, el dispositivo mostrará los botones de acción junto con el mensaje de notificación. Se admiten notificaciones interactivas en dispositivos iOS con versión 8 o posteriores. Para notificaciones interactivas enviadas a dispositivos iOS anteriores a la versión 8, no se mostrarán las acciones de notificación.

## Envío de {{site.data.keyword.mobilepushshort}} interactivas


La notificación interactiva puede enviarse utilizando el panel de control de push o utilizando la [Documentación de la API REST](t_restapi.html).

Desde la consola de {{site.data.keyword.mobilepushshort}}: 

1. En el separador de notificaciones del panel de control de Push, pulse **Enviar notificación**. 
2. Elija los destinatarios de la notificación y pulse **Siguiente**. 
3. En la página para crear notificaciones se puede enviar un push interactivo estableciendo Tipo en Predeterminado o Mixto y especificando Valor de categoría en el separador Opciones avanzadas. Para configurar el valor de categoría en el cliente, consulte la sección **Manejo de {{site.data.keyword.mobilepushshort}} interactivas** en aplicaciones iOS nativas.

## Manejo de {{site.data.keyword.mobilepushshort}} interactivas en una aplicación iOS


### Swift

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

Para recibir una notificación accionable en una aplicación de iOS Cordova, siga estos pasos:

1. Añada el campo de categoría dentro del método `BMSPush.initialize`.
   ```
	var category =  {"Category_Name":[{"IdentifierName_1":"actionName_1"},{"IdentifierName_2":"actionName_2"}]}
       BMSPush.initialize(appGUID,clientSecret,category);
    ```
	{: codeblock} 
2. Implemente el nuevo método callback en AppDelegate.
3. Este nuevo método callback se invoca cuando el usuario pulsa el botón de acción. La implementación de este método debe realizar tareas asociadas con el identificador especificado y ejecutar el bloque en el parámetro completionHandler.
