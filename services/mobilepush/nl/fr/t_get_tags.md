# Obtention des balises
{: #get_tags}

Les balises permettent d'envoyer des notifications ciblées aux utilisateurs en fonction de leurs intérêts, à la différence des diffusions
générales qui sont envoyées à toutes les applications. Vous pouvez créer et gérer des balises à l'aide de l'onglet Balise du tableau de bord Push ou utiliser l'API REST. Vous pouvez utiliser des fragments de code dans les sections suivantes pour gérer et interroger vos abonnements aux balises pour votre application mobile. Ils permettent d'obtenir des abonnements, de s'abonner à une balise, de se désabonner d'une balise et d'obtenir la liste des balises disponibles. Vous copiez et collez ces fragments de code dans votre application mobile.

## Android

L'API **getTags** renvoie la liste des balises disponibles auxquelles le périphérique peut s'abonner. Lorsqu'un
périphérique est abonné à une balise en particulier, il peut recevoir toutes les notifications push envoyées pour cette balise.

Copiez les fragments de code ci-après dans votre application mobile Android afin d'obtenir la liste des balises auxquelles le périphérique est
abonné ainsi que la liste des balises disponibles.

Utilisez l'API **getTags** pour obtenir la liste des balises disponibles auxquelles le périphérique peut s'abonner.

```
// Obtenez la liste des balises disponibles auxquelles le périphérique peut s'abonner
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

Utilisez l'API **getSubscriptions** pour obtenir la liste des balises auxquelles le périphérique est abonné.

```
// Obtenez la liste des balises auxquelles le périphérique est abonné.
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

Copiez les fragments de code ci-après dans votre application mobile afin d'obtenir la liste des balises auxquelles le périphérique est abonné ainsi que la liste des balises disponibles auxquelles le périphérique peut s'abonner.

Renvoyez un tableau des balises auxquelles le périphérique peut s'abonner.

```
//Obtenez la liste des balises disponibles auxquelles le périphérique peut s'abonner
MFPPush.retrieveAvailableTags(function(tags) {
    alert(tags);
}, null);

```

```
//Obtenez la liste des balises disponibles auxquelles le périphérique est abonné.
MFPPush.getSubscriptionStatus(function(tags) {
    alert(tags);
}, null);
```

## Objective-C

Copiez les fragments de code ci-après dans votre application iOS développée à l'aide de la méthode Objective-C afin d'obtenir la liste des balises auxquelles le périphérique est abonné ainsi que la liste des balises disponibles auxquelles le périphérique peut s'abonner.

Utilisez l'API **retrieveAvailableTags** ci-après pour obtenir la liste des balises disponibles auxquelles le périphérique peut s'abonner.

```
//Obtenez la liste des balises disponibles auxquelles le périphérique peut s'abonner
[push retrieveAvailableTagsWithCompletionHandler:
^(IMFResponse *response, NSError *error){
 if(error) {    
   [self updateMessage:error.description];  
 } else {
   [self updateMessage:@"Successfully retrieved available tags."];
 NSDictionary *availableTags = [[NSDictionary alloc]init];
 availableTags = [response tags];
[self.appDelegateVC updateMessage:availableTags.description];
}
}];
```
       
Utilisez l'API **retrieveSubscriptions** pour obtenir la liste des balises auxquelles le périphérique est abonné.


```
// Obtenez la liste des balises auxquelles le périphérique est abonné.
[push retrieveSubscriptionsWithCompletionHandler:
^(IMFResponse *response, NSError *error) {
  if(error) {
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

L'API **retrieveAvailableTagsWithCompletionHandler** renvoie la liste des balises disponibles auxquelles le périphérique peut s'abonner. Lorsqu'un
périphérique est abonné à une balise en particulier, il peut recevoir toutes les notifications push envoyées pour cette balise.

Appelez le service Push pour obtenir les abonnements à une balise.

Copiez les fragments de code ci-après dans votre application mobile Swift afin d'obtenir la liste des balises auxquelles le périphérique est abonné ainsi que la liste des balises disponibles auxquelles le périphérique peut s'abonner.


```
//Obtenez la liste des balises disponibles auxquelles le périphérique peut s'abonner
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
//Obtenez la liste des balises disponibles auxquelles le périphérique est abonné
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



