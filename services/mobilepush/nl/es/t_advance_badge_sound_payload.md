---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#Habilitación de notificaciones push avanzadas
Última actualización: 11 de enero de 2017
{: .last-updated}

Configure un identificador de iOS, un sonido, una carga útil de JSON adicional, notificaciones accionables y notificaciones retenidas.

## Configure un sonido y carga útil e identificador iOS
{: #badge-sound-payload}

Configure un identificador y un sonido de iOS, y carga útil adicional de JSON.

1. En el panel de control {{site.data.keyword.mobilepushshort}}, vaya al separador **Notificaciones**.
2. Vaya a la sección **Campos opcionales** para configurar las características de {{site.data.keyword.mobilepushshort}}. 
	- **Archivo de sonido**: Escriba una serie que apunte al archivo de sonido de la app móvil. En la carga útil, especifique el nombre de serie del archivo de sonido a utilizar.
	- **Identificador iOS**: Para dispositivos iOS, el número que se mostrará como el identificador del icono de app. Si falta esta propiedad, el identificador no se modificará. Para eliminar el identificador, establezca el valor de esta propiedad en 0.
	
###Android

Añada el archivo de sonido en el directorio `res/raw` de la aplicación android. Al enviar la notificación, añada el nombre del archivo de sonido en el campo de sonido de {{site.data.keyword.mobilepushshort}}.

```
"settings": {
     "gcm" : {
     "sound":"tt.wav",
	  }
 }  
```
    {: codeblock}	
	
###iOS

```
"settings": {
     "apns" : {
      "badge": 10,
	      "sound": "tt.wav",
	  }
}
``` 
	{: codeblock}
		
**Carga útil adicional**: Esta carga útil puede ser cualquier par de clave-valor y debe ser un objeto JSON que desee enviar con la {{site.data.keyword.mobilepushshort}}.

```
{"key":"value", "key2":"value2"}
```
	{: codeblock}

## Retención de notificaciones de Android 
{: #hold-notifications-android}

Cuando su aplicación entre en segundo plano, probablemente querrá que la {{site.data.keyword.mobilepushshort}} retenga las notificaciones enviadas a la aplicación. Para retener las notificaciones, llame el método hold() en el método onPause() de la actividad que maneja las {{site.data.keyword.mobilepushshort}}.

```
@Override
protected void onPause() {
    super.onPause();
    if (push != null) {
        push.hold();
    }
} 
```
	{: codeblock}
## Habilitación de notificaciones de iOS accionables  
{: #enable-actionable-notifications-ios}

A diferencia de las {{site.data.keyword.mobilepushshort}} convencionales, estas solicitan a los usuarios que realicen una selección al recibir la alerta de notificación sin abrir la app. 

Siga estos pasos para habilitar las {{site.data.keyword.mobilepushshort}} accionables en la aplicación.

1. Cree una acción de respuesta del usuario.
```
//For Swift
	let acceptAction = UIMutableUserNotificationAction()
	acceptAction.identifier = "ACCEPT_ACTION"
	acceptAction.title = "Accept"
	acceptAction.destructive = false
	acceptAction.authenticationRequired = false
	acceptAction.activationMode = UIUserNotificationActivationMode.Foreground
```
	{: codeblock}
```
//For Swift
	let declineAction = UIMutableUserNotificationAction()
	declineAction.identifier = "DECLINE_ACTION"
	declineAction.title = "Decline"
	declineAction.destructive = true
	declineAction.authenticationRequired = false
	declineAction.activationMode = UIUserNotificationActivationMode.Background
```
	{: codeblock}

2. Cree la categoría de notificaciones y configure una acción. **UIUserNotificationActionContextDefault** o **UIUserNotificationActionContextMinimal** son contextos válidos.
```
// For Swift
	let pushCategory = UIMutableUserNotificationCategory()
	pushCategory.identifier = "TODO_CATEGORY"
	pushCategory.setActions([acceptAction, declineAction], forContext: UIUserNotificationActionContext.Default)
```
	{: codeblock}

1. Cree el valor de notificación y asigne las categorías del paso anterior.
```
// For Swift
	let categories = NSSet(array:[pushCategory]);
```
	{: codeblock}

1. Cree una notificación remota o local y asígnele la identidad de la categoría.
```
//For Swift
	let settings = UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound], categories: categories as? Set<UIUserNotificationCategory>)
    UIApplication.sharedApplication().registerUserNotificationSettings(settings)
    UIApplication.sharedApplication().registerForRemoteNotifications() 
```
	{: codeblock}
	
## Gestión de notificaciones de iOS accionables  
{: #actionable-notifications}

Al recibir una notificación que necesita reacciones, el control se pasa al siguiente método según el identificador seleccionado.

 
```
func application(application: UIApplication, handleActionWithIdentifier identifier: String?, forRemoteNotification userInfo: [NSObject : AnyObject], completionHandler: () -> Void) {
      //must call completion handler when finished
      completionHandler()
  }
```    
	{: codeblock}
    
