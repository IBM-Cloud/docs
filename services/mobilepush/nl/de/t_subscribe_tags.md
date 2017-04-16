---

copyright:
 years: 2015, 2016

---

# Tags subskribieren und die Subskription aufheben
{: #Subscribe_tags}

Verwenden Sie die folgenden Code-Snippets, um Ihren Geräten das Abrufen von Subskriptionen und das Subskribieren und das Aufheben der Subskription von Tags zu ermöglichen.

## Android

Kopieren Sie das folgende Code-Snippet und fügen Sie es in Ihre mobile Android-Anwendung ein.

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

Kopieren Sie das folgende Code-Snippet und fügen Sie es in Ihre mobile Cordova-Anwendung ein.

```
var tag = "YourTag";
MFPPush.subscribe(tag, success, failure);
MFPPush.unsubscribe(tag, success, failure);
```

## Objective-C

Kopieren Sie das folgende Code-Snippet und fügen Sie es in Ihre mobile Objective-C-Anwendung ein.

Verwenden Sie die API **subscribeToTags** zum Subskribieren eines Tags.

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

Verwenden Sie die API **unsubscribeFromTags** zum Aufheben der Subskription eines Tags.

```
[push unsubscribeFromTags:tags completionHandler:
^(IMFResponse *response, NSError *error) {
   if (error){
       [self updateMessage:error.description];
 } else {
       NSDictionary* subStatus = [[NSDictionary alloc]init];
       subStatus = [response unsubscribeStatus];
       [self updateMessage:subStatus.description];
  }
}];
```

## Swift

Kopieren Sie das folgende Code-Snippet und fügen Sie es in Ihre mobile Swift-Anwendung ein.

**Verfügbare Tags subskribieren**

Verwenden Sie die API **subscribeToTags** zum Subskribieren eines Tags.

```
push.subscribeToTags(tagsArray: tags) { (response: IMFResponse!, error: NSError!) -> Void in
	if (error != nil) { 
		//error while subscribing to tags
	} else {
		//successfully subscribed to tags var subStatus = response.subscribeStatus();
	}
} 
```

**Subskription von Tags aufheben**

Verwenden Sie die API **unsubscribeFromTags** zum Aufheben der Subskription eines Tags.

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
