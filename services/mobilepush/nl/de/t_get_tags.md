# Tags abrufen
{: #get_tags}

Mit Tags können im Gegensatz zu allgemeinen Rundsendungen, die an alle Anwendungen gesendet werden, Benachrichtigungen auf der Grundlage eines Interessenbereichs zielgruppenspezifisch an Benutzer gesendet werden. Sie können Tags erstellen und verwalten, indem Sie die Registerkarte 'Tag' im Push-Dashboard oder REST-APIs verwenden. Sie können die Code-Snippets in den folgenden Abschnitten verwenden, um Ihre Tag-Subskriptionen für Ihre mobile Anwendung zu verwalten und abzufragen. Sie können diese Code-Snippets verwenden, um Subskriptionen abzurufen, eine Subskription für einen Tag einzurichten,
eine Subskription für einen Tag aufzuheben und eine Liste der verfügbaren Tags abzurufen. Sie kopieren diese Code-Snippets und fügen Sie in Ihre mobile Anwendung ein.

## Android

Die API **getTags** gibt die Liste mit den verfügbaren Tags zurück, die das Gerät subskribieren kann. Nachdem
das Gerät einen bestimmten Tag subskribiert hat, kann es alle Push-Benachrichtigungen empfangen, die für
diesen Tag gesendet werden.

Kopieren Sie die folgenden Code-Snippets in Ihre mobile Android-Anwendung, um eine Liste
der Tags abzurufen, die das Gerät subskribiert hat, und eine Liste der verfügbaren Tags.

Verwenden Sie die API **getTags**, um eine Liste der verfügbaren Tags abzurufen, die das Gerät subskribieren kann.

```
// Get a list of available tags to which the device can subscribe
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

Verwenden Sie die API **getSubscriptions**, um eine Liste der Tags abzurufen, die das
Gerät subskribiert hat.

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

Kopieren Sie die folgenden Code-Snippets in Ihre mobile Anwendung, um eine Liste der Tags abzurufen, die das Gerät subskribiert hat, und eine Liste der verfügbaren Tags, die das Gerät subskribieren kann.

Rufen Sie einen Array der Tags ab, die zum Subskribieren verfügbar sind.

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

Kopieren Sie die folgenden Code-Snippets in Ihre mit Objective-C entwickelte iOS-Anwendung, um eine Liste der Tags abzurufen, die das Gerät subskribiert hat, und eine Liste der verfügbaren Tags, die das Gerät subskribieren kann.

Verwenden Sie die API **retrieveAvailableTags**, um eine Liste der verfügbaren Tags abzurufen, die das Gerät subskribieren kann.

```
//Get a list of available tags to which the device can subscribe 
[push retrieveAvailableTagsWithCompletionHandler:
^(IMFResponse *response, NSError *error){ 
 if (error){[ self updateMessage:error.description];} else {
   [self updateMessage:@"Successfully retrieved available tags."];
 NSDictionary *availableTags = [[NSDictionary alloc]init];
 availableTags = [response tags];
[self.appDelegateVC updateMessage:availableTags.description];
}
}];
```
       
Verwenden Sie die API **retrieveSubscriptions**, um eine Liste der Tags abzurufen, die das Gerät subskribiert hat.


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

Die API **retrieveAvailableTagsWithCompletionHandler** gibt die Liste mit den verfügbaren Tags zurück, die das Gerät subskribieren kann. Nachdem
das Gerät einen bestimmten Tag subskribiert hat, kann es alle Push-Benachrichtigungen empfangen, die für
diesen Tag gesendet werden.

Rufen Sie den Push-Service auf, um die Subskriptionen für einen Tag abzurufen.

Kopieren Sie die folgenden Code-Snippets in Ihre mobile Swift-Anwendung, um eine Liste der Tags abzurufen, die das Gerät subskribiert hat, und eine Liste der verfügbaren Tags, die das Gerät subskribieren kann.


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
    if error.isEmpty
		{

        print( "Response during retrieving subscribed tags : \(response.description)")
        print( "status code during retrieving subscribed tags : \(statusCode)")
    }
    else {
        print( "Error during retrieving subscribed tags \(error) ")
        Print( "Error during retrieving subscribed tags \n  - status code: \(statusCode) \n Error :\(error) \n")
    }
}
```



