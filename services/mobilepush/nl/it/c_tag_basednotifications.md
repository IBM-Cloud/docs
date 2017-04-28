---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Abilitazione di notifiche basate sulle tag
{: #tag_based_notifications}
Ultimo aggiornamento: 12 aprile 2017
{: .last-updated}

I messaggi di notifica basata su tag sono destinati a tutti i dispositivi sottoscritti una specifica tag. 

Puoi definire le tag e quindi utilizzarle per
                        inviare e ricevere messaggi. Devi prima creare le tag per l'applicazione, impostare
                        le sottoscrizioni di tag e iniziare quindi le notifiche basate sulle
                        tag. Per inviare una notifica basata sulle tag utilizzando la [API REST](https://mobile.{DomainName}/imfpush/){: new_window}, assicurati che i "tagName" siano forniti durante l'inserimento nella risorsa messaggi.


## Gestione delle tag
{: #manage_tags}

Utilizza il dashboard {{site.data.keyword.mobilepushshort}} per creare ed eliminare tag per la tua applicazione e avviare quindi le notifiche basate sulle tag. La notifica basata sulle tag viene ricevuta dai dispositivi che hanno sottoscritto le tag.


### Creazione di tag
{: #create_tags}

Le notifiche basate sulle tag sono messaggi destinati a tutti i dispositivi sottoscritti a una particolare tag. Ciascun dispositivo può sottoscrivere qualsiasi numero di tag. Quando viene eliminata una tag, vengono eliminate anche le informazioni associate con tale tag, inclusi i relativi sottoscrittori e dispositivi. L'annullamento della sottoscrizione automatico non è obbligatorio, poiché la tag non esiste più. Non è richiesta alcuna ulteriore azione dal lato client.

1. Nel dashboard {{site.data.keyword.mobilepushshort}} **Tags**.
1. Fai clic sul pulsante + **Crea tag**.   
   1. Nel campo **Nome**, immetti il nome della tag. Ad esempio, "coupons".
   1. Nel campo **Descrizione**, immetti una descrizione della tag.
   1. Fai clic su **Save**.

1. Nell'area **Frammenti di codice**, seleziona la piattaforma per la tua applicazione mobile.
1. Modifica i frammenti di codice per gestire gli errori e copiali quindi per ogni tag nella tua applicazione mobile.

### Eliminazione di tag
{: #delete_tags}

1. Dalla scheda **Tag**, seleziona la tag che vuoi eliminare e fai clic sull'icona **Elimina**.
1. Fai clic su **OK**.

### Modifica della descrizione di una tag
{: #edit_tags}

1. Dalla scheda **Tag**, seleziona la tag che vuoi modificare.
1. Fai clic sull'icona **Modifica**.
1. Modifica la descrizione della tag e fai quindi clic sul pulsante **Salva**.

## Come ottenere le tag
{: #get_tags}

Le tag forniscono un modo per inviare notifiche mirate agli utenti sulla base dei loro interessi, a differenza dai broadcast generali che vengono inviati a tutte le applicazioni. Puoi creare e gestire le tag utilizzando la scheda Tag nel dashboard {{site.data.keyword.mobilepushshort}}oppure utilizzare le API REST. Puoi utilizzare i frammenti di codice per gestire e sottoporre a query le tue sottoscrizioni di tag per la tua
            applicazione mobile. Puoi utilizzare questi frammenti di codice per ottenere sottoscrizioni, sottoscrivere una tag, annullare la sottoscrizione a un tag o ottenere un elenco delle tag disponibili. Copia e incolla questi frammenti di codice nella tua applicazione mobile.

### Come ottenere le tag su Android
{: #android-get-tags}

La API **getTags** restituisce l'elenco di
            tag disponibili che il dispositivo può sottoscrivere. Una volta sottoscritto a una determinata tag, il dispositivo può ricevere {{site.data.keyword.mobilepushshort}} inviata per tale tag.

Copia i seguenti frammenti di codice nella tua applicazione mobile Android per ottenere un elenco di tag sottoscritte dal dispositivo e per ottenere un elenco delle tag disponibili.

Utilizza l'API **getTags** per ottenere un elenco delle tag disponibili a cui può sottoscriversi il dispositivo.

```
// Ottieni un elenco di tag disponibili a cui può sottoscriversi il dispositivo
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
	{: codeblock}

### Come ottenere le tag su Cordova
{: #cordova-get-tags}

Copia i seguenti frammenti di codice nella tua applicazione mobile per ottenere un elenco di tag sottoscritte dal dispositivo e per ottenere un elenco delle tag disponibili.

Richiama un array delle tag disponibili per la sottoscrizione.

```
//Ottieni un elenco di tag disponibili a cui può sottoscriversi il dispositivo
BMSPush.retrieveAvailableTags(function(tags) {
  alert(tags);
}, failure); 
```
	{: codeblock}

```
//Ottieni un elenco di tag disponibili sottoscritte dal dispositivo.
BMSPush.retrieveSubscriptions(function(tags) {
   alert(tags); 
}, failure); 
```
	{: codeblock}


### Come ottenere le tag su Swift
{: #swift-get-tags}

La API **retrieveAvailableTagsWithCompletionHandler** restituisce l'elenco di
            tag disponibili che il dispositivo può sottoscrivere. Una volta sottoscritto a una determinata tag, il dispositivo può ricevere {{site.data.keyword.mobilepushshort}} inviata per tale tag.

Richiama {{site.data.keyword.mobilepushshort}} per ottenere le sottoscrizioni per una tag.

Copia i seguenti frammenti di codice nella tua applicazione mobile Swift per ottenere un elenco delle tag disponibili sottoscritte dal dispositivo e per ottenere un elenco delle tag disponibili a cui può sottoscriversi il dispositivo.
```
//Ottieni un elenco di tag disponibili a cui può sottoscriversi il dispositivo
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
//Ottieni un elenco di tag disponibili sottoscritte dal dispositivo
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

### Come ottenere le tag su Google Chrome, Safari e Mozilla Firefox
{: #web-get-tags}

Per ottenere l'elenco di tag disponibili a cui possono sottoscriversi i clienti, utilizza il seguente codice.

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


### Come ottenere le tag sulle estensioni e applicazioni Google Chrome
{: #ext-get-tags}

Per ottenere l'elenco di tag disponibili a cui possono sottoscriversi i clienti, utilizza il seguente codice.

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

Copia il seguente frammento di codice nelle tue estensioni e applicazioni Google Chrome per ottenere un elenco di tag a cui hanno sottoscritto i clienti.

```
var bmsPush = new BMSPush();
  bmsPush.retrieveSubscriptions(function(response) 
	{
   alert(response.response)
 })
```
	{: codeblock}


## Sottoscrizione e annullamento di sottoscrizioni alle tag
{: #Subscribe_tags}

Utilizza i seguenti frammenti di codice per consentire ai tuoi dispositivi di ottenere sottoscrizioni, sottoscriversi a una tag e annullare la sottoscrizione a una tag.

### Sottoscrizione e annullamento di sottoscrizioni alle tag su Android
{: #android-subscribe-tags}

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

### Sottoscrizione e annullamento di sottoscrizioni alle tag su Cordova
{: #cordova-subscribe-tags}

Copia e incolla questo frammento di codice nella tua applicazione mobile Cordova.

```
var tag = "YourTag";
BMSPush.subscribe(tag, success, failure);
BMSPush.unsubscribe(tag, success, failure);
```
	{: codeblock}


### Sottoscrizione e annullamento di sottoscrizioni alle tag su Swift
{: #swift-subscribe-tags}

Copia e incolla questo frammento di codice nella tua applicazione mobile Swift.

Utilizza la API **subscribeToTags** per sottoscrivere a una
                tag.

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

Utilizza la API **unsubscribeFromTags** per annullare la sottoscrizione a una
                tag.

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

### Sottoscrizione e annullamento di sottoscrizioni alle tag su Google Chrome e Mozilla Firefox
{: #web-subscribe-tags}

Per sottoscriverti alle tag dalle applicazioni web, utilizza il seguente frammento di codice:

```
var tagsArray = ["tag1", "Tag2"]
bmsPush.subscribe(tagsArray,function(response) {
  alert(response.response)
})
```
	{: codeblock}

Per annullare la sottoscrizione alle tag utilizza il metodo **unSubscribe**.

```
var tagsArray = ["tag1", "Tag2"]
 bmsPush.unSubscribe(tagsArray,function(response) {
 alert(response.response)
})
```
	{: codeblock}

## Utilizzo delle notifiche basate sulle tag
{: #using_tags}

Le notifiche basate sulle tag sono messaggi destinati a tutti i dispositivi sottoscritti a una particolare tag. Ciascun dispositivo può essere sottoscritto a un qualsiasi numero di tag. Questo argomento descrive come inviare notifiche basate sulle tag. Le sottoscrizioni vengono gestite dall'istanza Bluemix del servizio {{site.data.keyword.mobilepushshort}}. Quando viene eliminata una tag, vengono eliminate anche tutte le informazioni associate con tale tag, inclusi i relativi sottoscrittori e dispositivi. Non è necessario un annullamento della sottoscrizione automatico per questa tag poiché non esiste più e non sono richieste ulteriori azioni dal lato client.

Crea le tag utilizzando l'opzione **Manage Tags**. 

1. Dal dashboard **Push Notification**, fai clic su **Send Notifications**.
1. Seleziona l'opzione **Device by Tag** nell'elenco a discesa **Send To**.
1. Cerca le tag che vuoi utilizzare e selezionale.
![Schermata notifiche](images/tag_notification.jpg)
1. Nel campo **Message Text**, immetti il testo che deve essere inviato come notifica ai destinatari sottoscritti.
1. Fai clic su **Send**.
