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



