---

copyright:
 years: 2015, 2016

---

# Gestione delle tag
{: #manage_tags}

Utilizza il dashboard Push per creare ed eliminare tag per la tua applicazione e avviare quindi le notifiche basate sulle tag. La notifica basata sulle tag viene ricevuta dal dispositivo che ha sottoscritto la tag.


## Creazione di tag
{: #create_tags}

Le notifiche basate sulle tag sono messaggi di notifica destinati a tutti i dispositivi che hanno sottoscritto una specifica tag. Ciascun dispositivo può sottoscrivere qualsiasi numero di tag. Quando viene eliminata una tag, vengono eliminate anche tutte le informazioni associate con tale tag, inclusi i relativi sottoscrittori e dispositivi. Non è necessario un annullamento della sottoscrizione automatico per questa tag poiché non esiste più e non sono richieste ulteriori azioni dal lato client.

1. Nel dashboard Push, seleziona la scheda **Tag**.
1. Fai clic sul pulsante + **Crea tag**.   

   a. Nel campo **Nome**, immetti il nome della tag. Ad esempio, "coupons".
   
   b. Nel campo **Descrizione**, immetti una descrizione della tag.
   
   c. Fai clic su **Salva**.
   
1. Nell'area **Frammenti di codice**, seleziona la piattaforma per la tua applicazione mobile.
1. Modifica i frammenti di codice per gestire gli errori e copiali quindi per ogni tag nella tua applicazione mobile.

## Eliminazione di tag
{: #delete_tags}

1. Dalla scheda **Tag**, seleziona la tag che vuoi eliminare e fai clic sull'icona di eliminazione.
1. Fai clic su **OK**.

## Modifica della descrizione di una tag
{: #edit_tags}

1. Dalla scheda **Tag**, seleziona la tag che vuoi modificare.
1. Fai clic sull'icona modifica.
1. Modifica la descrizione della tag e fai quindi clic sul pulsante **Salva**.

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

# Sottoscrizione e annullamento di sottoscrizioni di tag
{: #Subscribe_tags}

Utilizza i seguenti frammenti di codice per consentire ai tuoi dispositivi di ottenere sottoscrizioni, sottoscriversi a una tag e annullare la sottoscrizione a una tag.

## Android

Copia e incolla questo frammento di codice nella tua applicazione mobile Android.

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

Copia e incolla questo frammento di codice nella tua applicazione mobile Cordova.

```
var tag = "YourTag";
MFPPush.subscribe(tag, success, failure);
MFPPush.unsubscribe(tag, success, failure);
```

## Objective-C

Copia e incolla questo frammento di codice nella tua applicazione mobile Objective-C.

Utilizza la API **subscribeToTags** per sottoscrivere a una
                tag.

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

Utilizza la API **unsubscribeFromTags** per annullare la sottoscrizione a una
                tag.

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

Copia e incolla questo frammento di codice nella tua applicazione mobile Swift.

**Sottoscrizione alle tag disponibili**

Utilizza la API **subscribeToTags** per sottoscrivere a una
                tag.

```
push.subscribeToTags(tagsArray: tags) { (response: IMFResponse!, error: NSError!) -> Void in
	if (error != nil) { 
		//error while subscribing to tags
	} else {
		//successfully subscribed to tags var subStatus = response.subscribeStatus();
	}
} 
```

**Annullare la sottoscrizione alle tag**

Utilizza la API **unsubscribeFromTags** per annullare la sottoscrizione a una
                tag.

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


# Utilizzo delle notifiche basate sulle tag
{: #using_tags}


Le notifiche basate sulle tag sono messaggi di notifica destinati a tutti i dispositivi che hanno sottoscritto una specifica tag. Ciascun dispositivo può essere sottoscritto a un qualsiasi numero di tag. Questa sezione descrive come inviare notifiche basate sulle tag. Le sottoscrizioni vengono gestite dall'istanza Bluemix Push Notifications service. Quando viene eliminata una tag, vengono eliminate anche tutte le informazioni associate con tale tag, inclusi i relativi sottoscrittori e dispositivi. Non è necessario un annullamento della sottoscrizione automatico per questa tag poiché non esiste più e non sono richieste ulteriori azioni dal lato client.

**Prima di iniziare**

Crea le tag sulla schermata **Tag**. Per informazioni su come creare le tag, vedi [Creazione di tag](t_manage_tags.html).

1. Dal dashboard **Push Notification**, fai clic sulla scheda **Notifications**.
1. Seleziona l'opzione **Tags** per inviare notifiche basate sulle tag.
1. Nel campo **Search**, cerca le tag che vuoi utilizzare e fai quindi clic sul pulsante **+Add**.![Schermata notifiche](images/tag_notification.jpg)
1. Vai all'area **Create Your Notifications** e, nel campo **Message Text**, immetti il testo che vuoi inviare nella tua notifica.
1. Fai clic sul pulsante **Send**.
