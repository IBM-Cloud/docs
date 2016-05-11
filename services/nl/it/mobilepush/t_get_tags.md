# Come ottenere le tag
{: #get_tags}

Le tag forniscono un modo per inviare notifiche mirate agli utenti sulla base dei loro interessi,
        a differenza dai broadcast generali che vengono inviati a tutte le applicazioni. Puoi creare e gestire le tag utilizzando la scheda Tag nel dashboard Push oppure utilizzare le API REST. Puoi utilizzare i frammenti di codice nelle seguenti sezioni per gestire e sottoporre a query le tue sottoscrizioni di tag per la tua applicazione mobile. Puoi utilizzare questi frammenti di codice per ottenere sottoscrizioni, sottoscrivere
            una tag e ottenere un elenco delle tag disponibili. Copi e incolli questi frammenti di codice nella tua applicazione mobile.

## Android

La API **getTags** restituisce l'elenco di
            tag disponibili che il dispositivo può sottoscrivere. Una volta sottoscritto a una
            determinata tag, il dispositivo può ricevere una qualsiasi notifica di push inviata per tale
            tag.

Copia i seguenti frammenti di codice nella tua applicazione mobile Android per ottenere un elenco di
      tag sottoscritte dal dispositivo e per ottenere un elenco delle tag disponibili.

Utilizza l'API **getTags** per ottenere un elenco delle tag disponibili a cui può sottoscriversi il dispositivo.

```
// Ottieni un elenco di tag disponibili a cui può sottoscriversi il dispositivo
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

Utilizza la API **getSubscriptions** per ottenere un elenco delle tag sottoscritte dal dispositivo.

```
// Ottieni un elenco delle tag sottoscritte dal dispositivo.
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
         updateTextView("Errore di ottenimento delle sottoscrizioni.. " + ex.getMessage());
    }
})
```

## Cordova

Copia i seguenti frammenti di codice nella tua applicazione mobile per ottenere un elenco di tag sottoscritte dal dispositivo e per ottenere un elenco delle tag disponibili a cui può sottoscriversi il dispositivo.

Richiama un array delle tag disponibili per la sottoscrizione.

```
//Ottieni un elenco di tag disponibili a cui può sottoscriversi il dispositivo
MFPPush.retrieveAvailableTags(function(tags) {
    alert(tags);
}, null);

```

```
//Ottieni un elenco di tag disponibili sottoscritte dal dispositivo.
MFPPush.getSubscriptionStatus(function(tags) {
    alert(tags);
}, null);
```

## Objective-C

Copia i seguenti frammenti di codice nella tua applicazione iOS sviluppata con Objective-C per ottenere un elenco di tag sottoscritte dal dispositivo e per ottenere un elenco delle tag disponibili a cui può sottoscriversi il dispositivo.

Utilizza la seguente API **retrieveAvailableTags** per ottenere un elenco delle tag disponibili a cui può sottoscriversi il dispositivo.

```
//Ottieni un elenco di tag disponibili a cui può sottoscriversi il dispositivo
[push retrieveAvailableTagsWithCompletionHandler:
^(IMFResponse *response, NSError *error){
 if(error){    
   [self  updateMessage:error.description];  
 } else {
   [self updateMessage:@"Successfully retrieved available tags."];
 NSDictionary *availableTags = [[NSDictionary alloc]init];
 availableTags = [response tags];
[self.appDelegateVC updateMessage:availableTags.description];
}
}];
```
       
Utilizza la API **retrieveSubscriptions** per ottenere un elenco delle tag sottoscritte dal dispositivo.


```
// Ottieni un elenco delle tag sottoscritte dal dispositivo.
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

La API **retrieveAvailableTagsWithCompletionHandler** restituisce l'elenco di
            tag disponibili che il dispositivo può sottoscrivere. Una volta sottoscritto a una
            determinata tag, il dispositivo può ricevere una qualsiasi notifica di push inviata per tale
            tag.

Richiama il servizio push per ottenere le sottoscrizioni per una tag.

Copia i seguenti frammenti di codice nella tua applicazione mobile Swift per ottenere un elenco delle tag disponibili sottoscritte dal dispositivo e per ottenere un elenco delle tag disponibili a cui può sottoscriversi il dispositivo.


```
//Ottieni un elenco di tag disponibili a cui può sottoscriversi il dispositivo
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
//Ottieni un elenco di tag disponibili sottoscritte dal dispositivo
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



