---

Copyright :
  Années : 2015, 2016

---

# Abonnement à des balises et désabonnement
{: #Subscribe_tags}

Utilisez les fragments de code ci-après pour permettre à vos périphériques de s'abonner à une balise et de s'en désabonner.

## Android

Copiez et collez le fragment de code suivant dans votre application mobile Android :

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

Copiez et collez le fragment de code suivant dans votre application mobile Cordova :

```
var tag = "YourTag";
MFPPush.subscribe(tag, success, failure);
MFPPush.unsubscribe(tag, success, failure);
```

## Objective-C

Copiez et collez le fragment de code suivant dans votre application mobile Objective-C :

Utilisez l'API **subscribeToTags** pour vous abonner à une balise.

```
[push subscribeToTags:tags completionHandler:
^(IMFResponse *response, NSError *error) {
  if(error) {
     [self updateMessage:error.description];
  }else{
      NSDictionary* subStatus = [[NSDictionary alloc]init];
      subStatus = [response subscribeStatus];
      [self updateMessage:@"Parsed subscribe status is:"];
      [self updateMessage:subStatus.description];
  }
}];
```

Utilisez l'API **unsubscribeFromTags** pour vous désabonner d'une balise.

```
[push unsubscribeFromTags:tags completionHandler:
^(IMFResponse *response, NSError *error) {
   if(error) {
       [self updateMessage:error.description];
 } else {
       NSDictionary* subStatus = [[NSDictionary alloc]init];
       subStatus = [response unsubscribeStatus];
       [self updateMessage:subStatus.description];
  }
}];
```

## Swift

Copiez et collez le fragment de code suivant dans votre application mobile Swift :

**Abonnement à des balises disponibles**

Utilisez l'API **subscribeToTags** pour vous abonner à une balise.

```
push.subscribeToTags(tagsArray: tags) { (response: IMFResponse!, error: NSError!) -> Void in
	if (error != nil) { 
		//erreur lors de l'abonnement à des balises
	} else {
		//l'abonnement aux balises var a abouti (subStatus = response.subscribeStatus();)
	}
} 
```

**Désabonnement de balises**

Utilisez l'API **unsubscribeFromTags** pour vous désabonner d'une balise.

```
push.unsubscribeFromTags(response, completionHandler: { (response, statusCode, error) -> Void in

    if error.isEmpty {
        print( "Response during unsubscribed tags : \(response.description)")
        print( "status code during unsubscribed tags : \(statusCode)")
    }
    else {
        print( "Error during unsubscribed tags \(error) ")
        print( "Error during unsubscribed tags \n  - status code: \(statusCode) \n Error :\(error) \n")
    }
}
```
