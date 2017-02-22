---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Gestión de etiquetas
{: #manage_tags}
Última actualización: 11 de enero de 2017
{: .last-updated}

Utilice el panel de control {{site.data.keyword.mobilepushshort}} para crear y suprimir etiquetas para la aplicación y, a continuación, iniciar las notificaciones basadas en etiquetas. La notificación basada en etiquetas se recibe en los dispositivos suscritos a las etiquetas.


## Creación de etiquetas
{: #create_tags}

Las notificaciones basadas en etiquetas son mensajes que están pensados para todos los dispositivos suscritos a una etiqueta determinada. Cada dispositivo se puede suscribir a cualquier número de etiquetas. Cuando se suprime una etiqueta, también se suprime toda la información asociada a dicha etiqueta, incluidos los suscriptores y los dispositivos. No es necesaria la anulación automática de la suscripción, porque la etiqueta ya no existe. No es necesario realizar más acciones en el lado del cliente.

1. En el panel de control {{site.data.keyword.mobilepushshort}}, seleccione el separador **Etiquetas**.
1. Pulse el botón **Crear etiqueta** +.   
   1. En el campo **Nombre**, especifique el nombre de la etiqueta. Por ejemplo, "cupones".
   1. En el campo **Descripción**, especifique una descripción de las etiquetas.
   1. Pulse **Guardar**.

1. En el área **Fragmentos de código**, seleccione la plataforma para la aplicación para móviles.
1. Modifique los fragmentos de código para manejar errores y, a continuación, copiar los fragmentos de código para cada etiqueta en la aplicación para móviles.

## Supresión de etiquetas
{: #delete_tags}

1. En el separador **Etiqueta**, seleccione la etiqueta que desea suprimir y pulse el icono **Suprimir**.
1. Pulse **Aceptar**.

## Edición de una descripción de etiquetas
{: #edit_tags}

1. Desde el separador **Etiqueta**, seleccione la etiqueta que desee editar.
1. Pulse el icono **Editar**.
1. Edite la descripción de etiquetas y, a continuación, pulse el botón **Guardar**.

# Obtención de etiquetas
{: #get_tags}

Las etiquetas proporcionan una forma para enviar notificaciones de destino a usuarios en función de sus intereses, a diferencia de las difusiones generales que se envían a todas las aplicaciones. Puede crear y gestionar etiquetas utilizando el separador Etiqueta en el panel de control {{site.data.keyword.mobilepushshort}} o utilizando las API REST. Puede utilizar fragmentos de código para gestionar y consultar las suscripciones de etiquetas para la aplicación móvil. Puede utilizar estos fragmentos de código para obtener suscripciones, suscribirse a una etiqueta, anular la suscripción de una etiqueta u obtener una lista de las etiquetas disponibles. Copie estos fragmentos de código en su aplicación móvil.

## Obtención de etiquetas en Android
{: android-get-tags}

La API **getTags** devuelve la lista de etiquetas disponibles a la que el dispositivo se puede suscribir. Después de suscribir el dispositivo a una determinada etiqueta, el dispositivo podrá recibir {{site.data.keyword.mobilepushshort}} que se hayan enviado para dicha etiqueta.

Copie los fragmentos de código siguientes en la aplicación para móviles de Android para obtener una lista de las etiquetas a las que el dispositivo está suscrito y para obtener una lista de las etiquetas disponibles.

Utilice la API **getTags** siguiente para obtener una lista de etiquetas disponibles a las que el dispositivo se puede suscribir.

```
// Obtenga una lista de etiquetas disponibles a las que se puede suscribir el dispositivo
push.getTags(new MFPPushResponseListener<List<String>>(){
   @Override
   public void onSuccess(List<String> tags){
   updateTextView("Retrieved available tags: " + tags);
   System.out.println("Available tags are: "+tags);
   availableTags = tags;
   subscribeToTag();
  }
  @Override
  public void onFailure(MFPPushException ex){
     updateTextView("Error getting available tags.. " + ex.getMessage());
  }
   })  
```
	{: codeblock}

Utilice la API **getSubscriptions** para obtener una lista de etiquetas a las que está suscrito el dispositivo.

```
// Obtenga una lista de las etiquetas disponibles a las que el dispositivo se suscribe.
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
	{: codeblock}

## Obtención de etiquetas en Cordova
{: cordova-get-tags}

Copie los siguientes fragmentos de código en la aplicación para móviles para obtener una lista de las etiquetas a las que el dispositivo está suscrito y para obtener una lista de las etiquetas disponibles.

Recupere una matriz de etiquetas disponibles a las que suscribirse.

```
//Obtenga una lista de etiquetas disponibles a las que el dispositivo se puede suscribir
BMSPush.retrieveAvailableTags(function(tags) {
  alert(tags);
}, failure); 
```
	{: codeblock}

```
//Obtenga una lista de las etiquetas disponibles a las que el dispositivo se suscribe.
BMSPush.retrieveSubscriptions(function(tags) {
   alert(tags); 
}, failure); 
```
	{: codeblock}


## Obtención de etiquetas en Swift
{: swift-get-tags}

La API **retrieveAvailableTagsWithCompletionHandler** devuelve la lista de etiquetas disponibles a la que el dispositivo se puede suscribir. Después de suscribir el dispositivo a una determinada etiqueta, el dispositivo podrá recibir {{site.data.keyword.mobilepushshort}} que se hayan enviado para dicha etiqueta.

Llame el servicio {{site.data.keyword.mobilepushshort}} para obtener suscripciones para una etiqueta.

Copie los siguientes fragmentos de código en la aplicación para móviles Swift para obtener una lista de etiquetas disponibles a las que el dispositivo está suscrito y para obtener una lista de etiquetas disponibles a las que se puede suscribir el dispositivo.
```
//Obtenga una lista de etiquetas disponibles a las que se puede suscribir el dispositivo
	push.retrieveAvailableTagsWithCompletionHandler({ (response, statusCode, error) -> Void in
    if error.isEmpty
		{
     print( "Response during retrieve tags : \(response)")
        print( "status code during retrieve tags : \(statusCode)")
    }
    else
	{
    print( "Error during retrieve tags \(error) ")
    Print( "Error during retrieve tags \n  - status code: \(statusCode) \n Error :\(error) \n")
    	}
	}
```
		{: codeblock}

```
//Obtenga una lista de etiquetas disponibles a las que está suscrito el dispositivo
push.retrieveSubscriptionsWithCompletionHandler { (response, statusCode, error) -> Void in
    if error.isEmpty {
    print( "Response during retrieving subscribed tags : \(response?.description)")
        print( "status code during retrieving subscribed tags : \(statusCode)")
    }
    else 
	{
    print( "Error during retrieving subscribed tags \(error) ")
    Print( "Error during retrieving subscribed tags \n  - status code: \(statusCode) \n Error :\(error) \n")
        }
	}
```
	{: codeblock}

## Google Chrome, Safari y Mozilla Firefox
{: web-get-tags}

Para obtener la lista de etiquetas disponibles, a las que se pueden suscribir los clientes, utilice el código siguiente.

```
var bmsPush = new BMSPush();
  bmsPush.retrieveAvailableTags(function(response) 
	{
  alert(response.response)
    var json = JSON.parse(response.response);
    var tagsA = []
  for (i in json.tags)
	{
    tagsA.push(json.tags[i].name)
    }
   alert(tagsA)
 })
```
	{: codeblock}


## Aplicaciones y extensiones de Google Chrome
{: web-get-tags}

Para obtener la lista de etiquetas disponibles, a las que se pueden suscribir los clientes, utilice el código siguiente.

```
var bmsPush = new BMSPush();
  bmsPush.retrieveAvailableTags(function(response) 
	{
  alert(response.response)
    var json = JSON.parse(response.response);
    var tagsA = []
  for (i in json.tags)
	{
    tagsA.push(json.tags[i].name)
    }
   alert(tagsA)
 })
```
	{: codeblock}

Copie los siguientes fragmentos de código en las aplicaciones y extensiones de Google Chrome para obtener una lista de etiquetas a las que están suscritos los clientes.

```
var bmsPush = new BMSPush();
  bmsPush.retrieveSubscriptions(function(response) 
	{
   alert(response.response)
 })
```
	{: codeblock}


# Suscripción y cancelación de la suscripción a las etiquetas
{: #Subscribe_tags}

Utilice los siguientes fragmentos de código para permitir que los dispositivos obtengan suscripciones, se suscriban a una etiqueta y cancelen la suscripción de una etiqueta.

## Suscripción y cancelación de la suscripción a las etiquetas en Android
{: android-subscribe-tags}

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
	{: codeblock}

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
	{: codeblock}

## Suscripción y cancelación de la suscripción a las etiquetas en Cordova
{: cordova-subscribe-tags}

Copie y pegue este fragmento de código en la aplicación para móviles de Cordova.

```
var tag = "YourTag";
BMSPush.subscribe(tag, success, failure);
BMSPush.unsubscribe(tag, success, failure);
```
	{: codeblock}


## Suscripción y cancelación de la suscripción a las etiquetas en Swift
{: swift-subscribe-tags}

Copie y pegue este fragmento de código en la aplicación para móviles de Swift.

Utilice la API **subscribeToTags** para suscribirse a una etiqueta.

```
push.subscribeToTags(tagsArray: ["MyTag"], completionHandler: { (response, statusCode, error) -> Void in
    if error.isEmpty {
        print("Response when subscribing to tags: \(response?.description)")
        print("Status code when subscribing to tags: \(statusCode)")
    } else {
        print("Error when subscribing to tags: \(error) ")
        print("Error status code when subscribing to tags: \(statusCode)")
    }
})
```
	{: codeblock}

Utilice la API **unsubscribeFromTags** para anular la suscripción a una etiqueta.

```
push.unsubscribeFromTags(response, completionHandler: { (response, statusCode, error) -> Void in
    if error.isEmpty {
     print( "Response during unsubscribed tags : \(response?.description)")
        print( "status code during unsubscribed tags : \(statusCode)")
    }
  else {
    print( "Error during  unsubscribed tags \(error) ")
    print( "Error during unsubscribed tags \n  - status code: \(statusCode) \n Error :\(error) \n")
  }
}
```
	{: codeblock}

## Google Chrome y Mozilla Firefox
{: web-subscribe-tags}

Para suscribirse a etiquetas de aplicaciones web, utilice el siguiente fragmento de código:

```
var tagsArray = ["tag1", "Tag2"]
bmsPush.subscribe(tagsArray,function(response) {
  alert(response.response)
})
```
	{: codeblock}

La anulación de la suscripción de etiquetas utiliza el método **unSubscribe**.

```
var tagsArray = ["tag1", "Tag2"]
 bmsPush.unSubscribe(tagsArray,function(response) {
 alert(response.response)
})
```
	{: codeblock}

# Utilización de notificaciones basadas en etiquetas
{: #using_tags}

Las notificaciones basadas en etiquetas son mensajes que están pensados para todos los dispositivos suscritos a una etiqueta determinada. Cada dispositivo se puede suscribir a cualquier número de etiquetas. En este tema se describe cómo enviar notificaciones basadas en etiquetas. Las suscripciones las mantiene la instancia de Bluemix del servicio {{site.data.keyword.mobilepushshort}}. Cuando se suprime una etiqueta, también se suprime toda la información asociada a dicha etiqueta, incluidos los suscriptores y los dispositivos. No es necesaria ninguna anulación de la suscripción automática para esta etiqueta porque ya no existe y no es necesaria ninguna acción desde el lado del cliente.

Cree etiquetas en la pantalla **Etiquetas**. Para obtener más información sobre cómo crear etiquetas, consulte [Creación de etiquetas](t_manage_tags.html).

1. Desde el panel de control **Notificación Push**, pulse **Enviar notificaciones**.
1. Seleccione la opción **Dispositivo por etiqueta** en la lista desplegable **Enviar a**.
1. Busque las etiquetas que desee utilizar y selecciónelas.
![pantalla Notificaciones](images/tag_notification.jpg)
1. En el campo **Texto del mensaje**, especifique texto que desee enviar como notificación a la audiencia suscrita.
1. Pulse **Enviar**.
