---

copyright:
 years: 2015, 2016

---

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
