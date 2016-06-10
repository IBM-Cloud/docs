---

copyright:
 years: 2015, 2016

---

# Tags verwalten
{: #manage_tags}

Mit dem Push-Dashboard können Sie Tags für Ihre Anwendungen erstellen oder löschen und anschließend tagbasierte Benachrichtigungen initialisieren. Die tagbasierte Benachrichtigung wird auf dem Gerät empfangen, von dem das Tag subskribiert wurde.


## Tags erstellen
{: #create_tags}

Tagbasierte Benachrichtigungen sind Benachrichtigungen, die als Ziel alle Geräte haben, die einen bestimmten Tag subskribiert haben. Jedes Gerät kann beliebig viele Tags subskribieren. Wenn ein Tag gelöscht wird, werden alle Informationen, die dem Tag zugeordnet sind (einschließlich Subskribente und Geräte) gelöscht. Für diesen Tag ist keine automatische Aufhebung der Subskription erforderlich, da er nicht mehr vorhanden ist und daher clientseitig keine weiteren Aktionen nötig sind.

1. Wählen Sie im Push-Dashboard die Registerkarte **Tags** aus.
1. Klicken Sie auf die Schaltfläche **Tag erstellen**.   

   a. Geben Sie in das Feld **Name** den Namen für den Tag ein. Beispiel: "Coupons".
   
   b. Geben Sie in das Feld **Beschreibung** eine Beschreibung für den Tag ein.
   
   c. Klicken Sie auf  **Speichern**.
   
1. Wählen Sie im Bereich **Code-Snippets** die Plattform für Ihre mobile Anwendung aus.
1. Ändern Sie die Code-Snippets so, dass Fehler verarbeitet werden, und kopieren Sie anschließend die Code-Snippets für jeden Tag in Ihre mobile Anwendung.

## Tags löschen
{: #delete_tags}

1. Wählen Sie in der Registerkarte **Tag** den Tag aus, den Sie löschen möchten, und klicken Sie auf das Löschsymbol.
1. Klicken Sie auf **OK**.

## Tagbeschreibung bearbeiten
{: #edit_tags}

1. Wählen Sie in der Registerkarte **Tag** den Tag aus, den Sie bearbeiten möchten.
1. Klicken Sie auf das Symbol für die Bearbeitung.
1. Bearbeiten Sie die Tagbeschreibung und klicken Sie anschließend auf die Schaltfläche **Speichern**.

# Tags abrufen
{: #get_tags}

Mit Tags können im Gegensatz zu allgemeinen Rundsendungen, die an alle Anwendungen gesendet werden, Benachrichtigungen auf der Grundlage eines Interessenbereichs zielgruppenspezifisch an Benutzer gesendet werden. Sie können Tags erstellen und verwalten, indem Sie die Registerkarte 'Tag' im Push-Dashboard oder REST-APIs verwenden. Sie können die Code-Snippets in den folgenden Abschnitten verwenden, um Ihre Tag-Subskriptionen für Ihre mobile Anwendung zu verwalten und abzufragen. Sie können diese Code-Snippets verwenden, um Subskriptionen abzurufen, eine Subskription für einen Tag einzurichten, eine Subskription für einen Tag aufzuheben und eine Liste der verfügbaren Tags abzurufen. Sie kopieren diese Code-Snippets und fügen Sie in Ihre mobile Anwendung ein.

## Android

Die API **getTags** gibt die Liste mit den verfügbaren Tags zurück, die das Gerät subskribieren kann. Nachdem das Gerät einen bestimmten Tag subskribiert hat, kann es alle Push-Benachrichtigungen empfangen, die für diesen Tag gesendet werden.

Kopieren Sie die folgenden Code-Snippets in Ihre mobile Android-Anwendung, um eine Liste der Tags abzurufen, die das Gerät subskribiert hat, und eine Liste der verfügbaren Tags.

Verwenden Sie die API **getTags**, um eine Liste der verfügbaren Tags abzurufen, die das Gerät subskribieren kann.

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

Verwenden Sie die API **getSubscriptions**, um eine Liste der Tags abzurufen, die das Gerät subskribiert hat.

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

Die API **retrieveAvailableTagsWithCompletionHandler** gibt die Liste mit den verfügbaren Tags zurück, die das Gerät subskribieren kann. Nachdem das Gerät einen bestimmten Tag subskribiert hat, kann es alle Push-Benachrichtigungen empfangen, die für diesen Tag gesendet werden.

Push-Service zum Abrufen von Subskriptionen für einen Tag aufrufen

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

# Tags subskribieren und die Subskribierung aufheben
{: #Subscribe_tags}

Verwenden Sie die folgenden Code-Snippets, um Ihren Geräten das Abrufen von Subskriptionen und das Subskribieren und das Aufheben der Subskribierung von Tags zu ermöglichen.

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

Verwenden Sie die API **unsubscribeFromTags** zum Aufheben der Subskribierung eines Tags.

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

**Subskribierung von Tags aufheben**

Verwenden Sie die API **unsubscribeFromTags** zum Aufheben der Subskribierung eines Tags.

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


# Tagbasierte Benachrichtigungen verwenden
{: #using_tags}


Tagbasierte Benachrichtigungen sind Benachrichtigungen, die als Ziel alle Geräte haben, die einen bestimmten Tag subskribiert haben. Jedes Gerät kann beliebig viele Tags subskribieren. In diesem Abschnitt wird beschrieben, wie tagbasierte Benachrichtigungen gesendet werden. Subskriptionen werden von der Bluemix-Instanz von Push Notifications Service verwaltet. Wenn ein Tag gelöscht wird, werden alle Informationen, die dem Tag zugeordnet sind (einschließlich Subskribente und Geräte) gelöscht. Für diesen Tag ist keine automatische Aufhebung der Subskription erforderlich, da er nicht mehr vorhanden ist und daher clientseitig keine weiteren Aktionen nötig sind.

**Vorbemerkungen**

Erstellen Sie Tags in der Anzeige **Tag**. Informationen zum Erstellen von Tags finden Sie in [Tags erstellen](t_manage_tags.html).

1. Klicken Sie im Push Notifications-Dashboard auf die Registerkarte **Benachrichtigungen**.
1. Wählen Sie die Option **Tags** aus, um tagbasierte Benachrichtigungen zu senden.
1. Suchen Sie mithilfe des Felds **Tags suchen** nach den Tags, die Sie verwenden möchten, und klicken Sie anschließend auf die Schaltfläche **Hinzufügen**.![Anzeige 'Benachrichtigungen](images/tag_notification.jpg)
1. Navigieren Sie zum Bereich **Eigene Benachrichtigungen erstellen**  und geben Sie in das Feld **Nachrichtentext** den Text ein, den Sie in Ihrer Benachrichtigung senden möchten.
1. Klicken Sie auf die Schaltfläche **Senden**.
