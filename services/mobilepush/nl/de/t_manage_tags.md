---

copyright:
 years: 2015, 2016

---

# Tags verwalten
{: #manage_tags}
Letzte Aktualisierung: 17. Oktober 2016
{: .last-updated}

Verwenden Sie das {{site.data.keyword.mobilepushshort}}-Dashboard, um Tags für Ihre Anwendung zu erstellen und zu löschen und anschließend tagbasierte Benachrichtigungen zu initiieren. Die tagbasierte Benachrichtigung wird auf Geräten empfangen, von denen Tags subskribiert wurden.


## Tags erstellen
{: #create_tags}

Tagbasierte Benachrichtigungen sind Benachrichtigungen, die all diejenigen Geräte als Ziel haben, die einen
bestimmten Tag subskribiert haben. Jedes Gerät kann beliebig viele Tags subskribieren. Wenn ein Tag gelöscht wird, werden die Informationen diesem Tag zugeordneten Informationen (einschließlich Subskribenten und Geräte) gelöscht. Es ist erforderlich, die automatische Subskription aufzuheben, wenn der Tag nicht mehr vorhanden ist. Es ist keine weitere Aktion von der Clientseite erforderlich.

1. Wählen Sie im {{site.data.keyword.mobilepushshort}}-Dashboard die Registerkarte **Tags** aus.
1. Klicken Sie auf die Schaltfläche **Tag erstellen**.   
   1. Geben Sie in das Feld **Name** den Namen für den Tag ein. Beispiel: "Coupons".
   1. Geben Sie in das Feld **Beschreibung** eine Beschreibung für den Tag ein.
   1. Klicken Sie auf **Speichern**.

1. Wählen Sie im Bereich **Code-Snippets** die Plattform für Ihre mobile Anwendung aus.
1. Ändern Sie die Code-Snippets so, dass Fehler verarbeitet werden, und kopieren Sie anschließend die Code-Snippets für jeden Tag in Ihre mobile Anwendung.

## Tags löschen
{: #delete_tags}

1. Wählen Sie auf der Registerkarte **Tag** den Tag aus, den Sie löschen möchten, und klicken Sie auf das Symbol **Löschen**.
1. Klicken Sie auf **OK**.

## Tagbeschreibung bearbeiten
{: #edit_tags}

1. Wählen Sie in der Registerkarte **Tag** den Tag aus, den Sie bearbeiten möchten.
1. Klicken Sie auf das Symbol **Bearbeiten**.
1. Bearbeiten Sie die Tagbeschreibung und klicken Sie anschließend auf die Schaltfläche **Speichern**.

# Tags abrufen
{: #get_tags}

Mit Tags können im Gegensatz zu allgemeinen Rundsendungen, die an alle Anwendungen gesendet werden, Benachrichtigungen auf der Grundlage eines Interessenbereichs zielgruppenspezifisch an Benutzer gesendet werden. Sie können Tags erstellen und verwalten, indem Sie die Registerkarte 'Tag' im {{site.data.keyword.mobilepushshort}}-Dashboard oder REST-APIs verwenden. Sie können Code-Snippets verwenden, um Ihre Tag-Subskriptionen für Ihre mobile Anwendung zu verwalten und abzufragen. Sie können diese Code-Snippets verwenden, um Subskriptionen abzurufen, eine Subskription für einen Tag einzurichten, eine Subskription für einen Tag aufzuheben oder eine Liste der verfügbaren Tags abzurufen. Kopieren Sie diese Code-Snippets in Ihre mobile Anwendung.

## Android
{: android-get-tags}

Die API **getTags** gibt die Liste mit den verfügbaren Tags zurück, die das Gerät subskribieren kann. Nachdem das Gerät einen bestimmten Tag subskribiert hat, kann es die Push-Benachrichtigungen empfangen, die für diesen Tag gesendet werden.

Kopieren Sie die folgenden Code-Snippets in Ihre mobile Android-Anwendung, um eine Liste der Tags abzurufen, die das Gerät subskribiert hat, und eine Liste der verfügbaren Tags.

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
	{: codeblock}

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
	{: codeblock}

## Cordova
{: cordova-get-tags}

Kopieren Sie die folgenden Code-Snippets in Ihre mobile Anwendung, um eine Liste der Tags abzurufen, die das Gerät subskribiert hat, und eine Liste der verfügbaren Tags, die das Gerät subskribieren kann.

Rufen Sie einen Array der Tags ab, die zum Subskribieren verfügbar sind.

```
//Get a list of available tags to which the device can subscribe
MFPPush.retrieveAvailableTags(function(tags) {
  alert(tags);
}, null);
```
	{: codeblock}

```
//Get a list of available tags to which the device is subscribed.
MFPPush.getSubscriptionStatus(function(tags) {
  alert(tags);
}, null);
```
	{: codeblock}

## Objective-C
{: objc-get-tags}

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
	{: codeblock}

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
	{: codeblock}

## Swift
{: swift-get-tags}

Die API **retrieveAvailableTagsWithCompletionHandler** gibt die Liste mit den verfügbaren Tags zurück, die das Gerät subskribieren kann. Nachdem das Gerät einen bestimmten Tag subskribiert hat, kann es Push-Benachrichtigungen empfangen, die für diesen Tag gesendet werden.

Rufen Sie die Push-Benachrichtigungen auf, um die Subskriptionen für einen Tag abzurufen.

Kopieren Sie die folgenden Code-Snippets in Ihre mobile Swift-Anwendung, um eine Liste der Tags abzurufen, die das Gerät subskribiert hat, und eine Liste der verfügbaren Tags, die das Gerät subskribieren kann.
```
//Get a list of available tags to which the device can subscribe
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
//Get a list of available tags to which the device is subscribed
	push.retrieveSubscriptionsWithCompletionHandler { (response, statusCode, error) -> Void in
    if error.isEmpty
		{
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

## Google Chrome und Mozilla Firefox
{: web-get-tags}

Zum Abrufen der Liste verfügbarer Tags, die von Kunden subskribiert werden können, verwenden Sie folgenden Code.

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

Kopieren Sie die folgenden Code-Snippets in Ihre Google Chrome-Apps und Erweiterungen, um eine Liste von Tags abzurufen, die von Kunden subskribiert wurden.

```
var bmsPush = new BMSPush();
  bmsPush.retrieveSubscriptions(function(response) 
	{
   alert(response.response)
 })
```
	{: codeblock}

## Google Chrome-Apps und Erweiterungen
{: web-get-tags}

Zum Abrufen der Liste verfügbarer Tags, die von Kunden subskribiert werden können, verwenden Sie folgenden Code.

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

Kopieren Sie die folgenden Code-Snippets in Ihre Google Chrome-Apps und Erweiterungen, um eine Liste von Tags abzurufen, die von Kunden subskribiert wurden.

```
var bmsPush = new BMSPush();
  bmsPush.retrieveSubscriptions(function(response) 
	{
   alert(response.response)
 })
```
	{: codeblock}


# Tags subskribieren und die Subskription aufheben
{: #Subscribe_tags}

Verwenden Sie die folgenden Code-Snippets, um Ihren Geräten das Abrufen von Subskriptionen und das Subskribieren und das Aufheben der Subskription von Tags zu ermöglichen.

## Android
{: android-subscribe-tags}

Kopieren Sie dieses Code-Snippet und fügen Sie es in Ihre mobile Android-Anwendung ein.

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

## Cordova
{: cordova-subscribe-tags}

Kopieren Sie dieses Code-Snippet und fügen Sie es in Ihre mobile Cordova-Anwendung ein.

```
var tag = "YourTag";
MFPPush.subscribe(tag, success, failure);
MFPPush.unsubscribe(tag, success, failure);
```
	{: codeblock}

## Objective-C
{: objc-subscribe-tags}

Kopieren Sie dieses Code-Snippet und fügen Sie es in Ihre mobile Objective-C-Anwendung ein.

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
	{: codeblock}

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
	{: codeblock}

## Swift
{: swift-subscribe-tags}

Kopieren Sie dieses Code-Snippet und fügen Sie es in Ihre mobile Swift-Anwendung ein.

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
	{: codeblock}

**Subskription von Tags aufheben**

Verwenden Sie die API **unsubscribeFromTags** zum Aufheben der Subskription eines Tags.

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

## Google Chrome und Mozilla Firefox
{: web-subscribe-tags}

Um Tags von Webanwendungen zu subskribieren, verwenden Sie das folgende Code-Snippet:

```
var tagsArray = ["tag1", "Tag2"]
bmsPush.subscribe(tagsArray,function(response) {
  alert(response.response)
})
```
	{: codeblock}

Um die Subskription von Tags aufzuheben, verwenden Sie die Methode `unSubscribe`.

```
var tagsArray = ["tag1", "Tag2"]
 bmsPush.unSubscribe(tagsArray,function(response) {
 alert(response.response)
})
```
	{: codeblock}

# Tagbasierte Benachrichtigungen verwenden
{: #using_tags}

Tagbasierte Benachrichtigungen sind Benachrichtigungen, die alle diejenigen Geräte zum Ziel haben, die einen bestimmten Tag subskribiert haben. Jedes Gerät kann beliebig viele Tags subskribieren. Dieses Thema beschreibt, wie tagbasierte Benachrichtigungen gesendet werden. Subskriptionen werden von der Bluemix-Instanz des {{site.data.keyword.mobilepushshort}}-Service verwaltet. Wenn ein Tag gelöscht wird, werden alle diesem Tag zugeordneten Informationen (einschließlich Subskribenten und Geräte) gelöscht. Für diesen Tag ist keine automatische Aufhebung der Subskription erforderlich, da er nicht mehr vorhanden ist und daher clientseitig keine weiteren Aktionen nötig sind.

###Vorbemerkungen
{: before-you-begin}

Erstellen Sie Tags in der Anzeige **Tag**. Informationen zum Erstellen von Tags finden Sie in [Tags erstellen](t_manage_tags.html).

1. Klicken Sie im **Push Notification**-Dashboard auf **Benachrichtigungen senden**.
1. Wählen Sie in der Dropdown-Liste **Senden an** die Option **Gerät nach Tag** aus.
1. Suchen Sie nach den Tags, die Sie verwenden möchten, und wählen Sie sie aus.
![Anzeige 'Benachrichtigungen'](images/tag_notification.jpg)
1. Geben Sie im Feld **Nachrichtentext** den Text ein, der als Benachrichtigung an die subskribierte Benutzergruppe gesendet werden soll.
1. Klicken Sie auf **Senden**.
