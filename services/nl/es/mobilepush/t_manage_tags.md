---

copyright:
 years: 2015, 2016

---

# Gestión de etiquetas
{: #manage_tags}

Utilice el panel de control de Push para crear y suprimir etiquetas para la aplicación y, a continuación, iniciar
  las notificaciones basadas en etiquetas. La notificación basada en etiquetas se recibe en el dispositivo suscrito a la etiqueta.


## Creación de etiquetas
{: #create_tags}

Las notificaciones basadas en etiquetas son mensajes de notificación que están pensados para todos los dispositivos
   suscritos a una etiqueta determinada. Cada dispositivo se puede suscribir a cualquier número de etiquetas. Cuando una etiqueta se ha suprimido, toda la información asociada con dicha etiqueta, incluidos los suscriptores y los dispositivos, se suprimirán. No es necesaria ninguna anulación de la suscripción automática para esta etiqueta porque ya no existe y no es necesaria ninguna acción desde el lado del cliente.

1. En el panel de control Push, seleccione el separador **Etiquetas**.
1. Pulse el botón **Crear etiqueta** +.   

   a. En el campo **Nombre**, especifique el nombre de la etiqueta. Por ejemplo, "cupones".
   
   b. En el campo **Descripción**, especifique una descripción de las etiquetas.
   
   c. Pulse **Guardar**.
   
1. En el área **Fragmentos de código**, seleccione la plataforma para la aplicación
      para móviles.
1. Modifique los fragmentos de código para manejar errores y, a continuación, copiar los fragmentos de código para cada etiqueta
      en la aplicación para móviles.

## Supresión de etiquetas
{: #delete_tags}

1. Desde el separador **Etiqueta**, seleccione la etiqueta que desea suprimir y pulse
      el icono de supresión.
1. Pulse **Aceptar**.

## Edición de una descripción de etiquetas
{: #edit_tags}

1. Desde el separador **Etiqueta**, seleccione la etiqueta que desee editar.
1. Pulse el icono de edición.
1. Edite la descripción de etiquetas y, a continuación, pulse el botón **Guardar**.

# Obtención de etiquetas
{: #get_tags}

Las etiquetas proporcionan una forma para enviar notificaciones de destino a usuarios en función de sus intereses,
        a diferencia de las difusiones generales que se envían a todas las aplicaciones. Puede crear y gestionar etiquetas utilizando el separador Etiqueta en el panel de control Push o utilizando las API REST. Puede utilizar fragmentos de código en la secciones siguientes para gestionar y consultar las suscripciones de etiquetas para la aplicación móvil. Puede utilizar estos
  fragmentos de código para obtener suscripciones, suscritas a una etiqueta, no suscritas desde una etiqueta, obtener una lista de
  etiquetas disponibles. Copie y pegue estos fragmentos de código en su aplicación móvil.

## Android

La API **getTags**
            devuelve la lista de etiquetas disponibles a la que el dispositivo se puede suscribir. Después de suscribir el dispositivo a una determinada etiqueta, el dispositivo podrá recibir cualquier notificación push que se haya enviado para dicha etiqueta.

Copie los fragmentos de código siguientes en la aplicación para móviles de Android para obtener una lista de
      etiquetas a las que el dispositivo está suscrito y para obtener una lista de etiquetas disponibles.

Utilice la API **getTags** siguiente para obtener una lista de etiquetas disponibles a las que el dispositivo se puede suscribir.

```
// Get a list of available tags to which the device can subscribe
push.getTags(new MFPPushResponseListener<List<String>>(){  
   @Override
    public void onSuccess(List<String> tags) { 
   updateTextView("Retrieved available tags: " + tags);  
   System.out.println("Available tags are: "+tags);
   availableTags = tags;   
   subscribeToTag();   
  }    
  @Override    
  public void onFailure(MFPPushException ex) {
     updateTextView("Error getting available tags.. " + ex.getMessage());
  }
})  
```

Utilice la API **getSubscriptions** para obtener una lista de etiquetas a las que está
       suscrito el dispositivo.

```
// Get a list of tags that to which the device is subscribed.
push.getSubscriptions(new MFPPushResponseListener<List<String>>() {
    @Override
    public void onSuccess(List<String> tags) {
    updateTextView("Retrieved subscriptions : " + tags);
    System.out.println("Subscribed tags are: "+tags);
    subscribedTags = tags;
    subscribeToTag();
    }
    @Override
    public void onFailure(MFPPushException ex) {
         updateTextView("Error getting subscriptions.. " + ex.getMessage());
    }
})
```

## Cordova

Copie los siguientes fragmentos de código en la aplicación para móviles para obtener una lista de etiquetas a las que el dispositivo está suscrito y para obtener una lista de etiquetas disponibles a las que se puede suscribir el dispositivo.

Recupere una matriz de etiquetas disponibles a las que suscribirse.

```
//Get a list of available tags to which the device can subscribe
MFPPush.retrieveAvailableTags(function(tags) {
    alert(tags);
}, null);

```

```
//Get a list of available tags to which the device is subscribed.
MFPPush.getSubscriptionStatus(function(tags) {
    alert(tags);
}, null);
```

## Objective-C

Copie los siguientes fragmentos de código en la aplicación iOS desarrollada utilizando Objective-C para obtener una lista de etiquetas a las que el dispositivo está suscrito y para obtener una lista de etiquetas disponibles a las que se puede suscribir el dispositivo.

Utilice la API **retrieveAvailableTags** siguiente para obtener una lista de etiquetas disponibles a las que está suscrito el dispositivo.

```
//Get a list of available tags to which the device can subscribe 
[push retrieveAvailableTagsWithCompletionHandler:
^(IMFResponse *response, NSError *error){ 
 if(error){    
   [self updateMessage:error.description];  
 } else {
   [self updateMessage:@"Successfully retrieved available tags."];
 NSDictionary *availableTags = [[NSDictionary alloc]init];
 availableTags = [response tags];
[self.appDelegateVC updateMessage:availableTags.description];
}
}];
```
       
Utilice la API **retrieveSubscriptions** para obtener una lista de etiquetas a las que está suscrito
       el dispositivo.


```
// Get a list of tags that to which the device is subscribed.
[push retrieveSubscriptionsWithCompletionHandler:
^(IMFResponse *response, NSError *error) {
  if(error){
     [self updateMessage:error.description];
   } else {
     [self updateMessage:@"Successfully retrieved subscriptions."];
 NSDictionary *subscribedTags = [[NSDictionary alloc]init];
subscribedTags = [response subscriptions];
[self.appDelegateVC updateMessage:subscribedTags.description];
}
}];
```

## Swift

La API **retrieveAvailableTagsWithCompletionHandler** devuelve la lista de etiquetas disponibles a la que el dispositivo se puede suscribir. Después de suscribir el dispositivo a una determinada etiqueta, el dispositivo podrá recibir cualquier notificación push que se haya enviado para dicha etiqueta.

Invocar al servicio push para obtener suscripciones para una etiqueta.

Copie los siguientes fragmentos de código en la aplicación para móviles Swift para obtener una lista de etiquetas disponibles a las que el dispositivo está suscrito y para obtener una lista de etiquetas disponibles a las que se puede suscribir el dispositivo.


```
//Get a list of available tags to which the device can subscribe
push.retrieveAvailableTagsWithCompletionHandler({ (response, statusCode, error) -> Void in

    if error.isEmpty {

        print( "Response during retrieve tags : \(response)")
        print( "status code during retrieve tags : \(statusCode)")
    }
    else{
        print( "Error during retrieve tags \(error) ")
        Print( "Error during retrieve tags \n  - status code: \(statusCode) \n Error :\(error) \n")
    }
}
```

```
//Get a list of available tags to which the device is subscribed
push.retrieveSubscriptionsWithCompletionHandler { (response, statusCode, error) -> Void in
    if error.isEmpty {

        print( "Response during retrieving subscribed tags : \(response.description)")
        print( "status code during retrieving subscribed tags : \(statusCode)")
    }
    else {
        print( "Error during retrieving subscribed tags \(error) ")
        Print( "Error during retrieving subscribed tags \n  - status code: \(statusCode) \n Error :\(error) \n")
    }
}
```

# Suscripción y cancelación de la suscripción a las etiquetas
{: #Subscribe_tags}

Utilice los siguientes fragmentos de código para permitir que los dispositivos obtengan suscripciones, se suscriban a una etiqueta y cancelen la suscripción de una etiqueta.

## Android

Copie y pegue este fragmento de código en la aplicación para móviles de Android.

```
push.subscribe(allTags.get(0),
new MFPPushResponseListener<String>() {
  @Override
  public void onFailure(MFPPushException ex) {
    updateTextView("Error subscribing to Tag1.."
           + ex.getMessage());
  }
  @Override
  public void onSuccess(String arg0) {
   updateTextView("Succesfully Subscribed to: "+ arg0);
   unsubscribeFromTags(arg0);
   }
});
```

```
push.unsubscribe(tag, new MFPPushResponseListener<String>() {
 @Override
 public void onSuccess(String s) {
   updateTextView("Unsubscribing from tag");
   updateTextView("Successfully unsubscribed from tag . "+ tag);
 }
 @Override
 public void onFailure(MFPPushException e) {
 updateTextView("Error while unsubscribing from tags. "+ e.getMessage());
 }
});
```

## Cordova

Copie y pegue este fragmento de código en la aplicación para móviles de Cordova.

```
var tag = "YourTag";
MFPPush.subscribe(tag, success, failure);
MFPPush.unsubscribe(tag, success, failure);
```

## Objective-C

Copie y pegue este fragmento de código en la aplicación para móviles de Objective-C.

Utilice la API **subscribeToTags** para suscribirse a una etiqueta.

```
[push subscribeToTags:tags completionHandler:
^(IMFResponse *response, NSError *error) {
  if(error){
     [self updateMessage:error.description];
  }else{
      NSDictionary* subStatus = [[NSDictionary alloc]init];
      subStatus = [response subscribeStatus];
      [self updateMessage:@"Parsed subscribe status is:"];
      [self updateMessage:subStatus.description];
  }
}];
```

Utilice la API **unsubscribeFromTags** para anular la suscripción a una etiqueta.

```
[push unsubscribeFromTags:tags completionHandler:
^(IMFResponse *response, NSError *error) {
   if(error){
       [self updateMessage:error.description];
 } else {
       NSDictionary* subStatus = [[NSDictionary alloc]init];
       subStatus = [response unsubscribeStatus];
       [self updateMessage:subStatus.description];
  }
}];
```

## Swift

Copie y pegue este fragmento de código en la aplicación para móviles de Swift.

**Suscribirse a etiquetas disponibles**

Utilice la API **subscribeToTags** para suscribirse a una etiqueta.

```
push.subscribeToTags(tagsArray: tags) { (response: IMFResponse!, error: NSError!) -> Void in
	if (error != nil) { 
		//error while subscribing to tags
	} else {
		//successfully subscribed to tags var subStatus = response.subscribeStatus();
	}
} 
```

**Eliminar suscripción a etiquetas**

Utilice la API **unsubscribeFromTags** para anular la suscripción a una etiqueta.

```
push.unsubscribeFromTags(response, completionHandler: { (response, statusCode, error) -> Void in

    if error.isEmpty {
        print( "Response during unsubscribed tags : \(response.description)")
        print( "status code during unsubscribed tags : \(statusCode)")
    }
    else {
        print( "Error during  unsubscribed tags \(error) ")
        print( "Error during unsubscribed tags \n  - status code: \(statusCode) \n Error :\(error) \n")
    }
}
```


# Utilización de notificaciones basadas en etiquetas
{: #using_tags}


Las notificaciones basadas en etiquetas son mensajes de notificación que están pensados para todos los dispositivos
   suscritos a una etiqueta determinada. Cada dispositivo se puede suscribir a cualquier número de etiquetas. Esta sección describe cómo enviar notificaciones basadas en código. Las suscripciones las mantiene la instancia de Bluemix del servicio de notificaciones Push. Cuando una etiqueta se ha suprimido, toda la información asociada con dicha etiqueta, incluidos los suscriptores y los dispositivos, se suprimirán. No es necesaria ninguna anulación de la suscripción automática para esta etiqueta porque ya no existe y no es necesaria ninguna acción desde el lado del cliente.

**Antes de empezar**

Cree etiquetas en la pantalla **Etiquetas**. Para obtener más información sobre cómo crear etiquetas, consulte [Creación de etiquetas](t_manage_tags.html).

1. Desde el panel de control de **Notificación Push**, pulse el separador
      **Notificaciones**.
1. Seleccione la opción **Etiquetas** a enviar mediante las notificaciones basadas en etiquetas.
1. En el campo **Búsqueda** de etiquetas, busque las etiquetas que desee utilizar y, a continuación, el botón **+Añadir**.![Pantalla de notificaciones](images/tag_notification.jpg)
1. Vaya al área **Crear sus notificaciones** y, en el campo
      **Texto del mensaje**, especifique texto que desee enviar en la notificación.
1. Pulse el botón **Enviar**.
