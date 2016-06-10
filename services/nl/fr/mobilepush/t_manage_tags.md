---

copyright:
 years: 2015, 2016

---

# Gestion des balises
{: #manage_tags}

Utilisez le tableau de bord Push afin de créer et de supprimer des balises pour votre application, puis d'initier des notifications en
fonction d'une balise. Une notification basée sur les balises est reçue sur le périphérique abonné à la balise.


## Création de balises
{: #create_tags}

Les notifications en fonction d'une balise sont des messages de notification qui sont envoyés à tous les périphériques abonnés à une balise particulière. Chaque périphérique peut s'abonner à un nombre illimité de balises. Lorsqu'une balise est supprimée, toutes les informations qui lui sont associées, y compris ses abonnés et périphériques, sont supprimées. Aucun désabonnement automatique n'est requis pour cette balise car elle n'existe plus et aucune action supplémentaire n'est requise depuis le côté client.

1. Dans le tableau de bord Push, sélectionnez l'onglet **Balises**.
1. Cliquez sur le bouton + **Créer une balise**.   

   a. Dans la zone **Nom**, entrez le nom de la balise. Exemple : "coupons".
   
   b. Dans la zone **Description**, entrez une description de balise.
   
   c. Cliquez sur **Sauvegarder**.
   
1. Dans la zone **Fragments de code**, sélectionnez la plateforme pour votre application mobile.
1. Modifiez les fragments de code pour traiter les erreurs, puis copiez-les pour chaque balise dans votre application mobile.

## Suppression de balises
{: #delete_tags}

1. Dans l'onglet **Balise**, sélectionnez la balise à supprimer et cliquez sur l'icône de suppression.
1. Cliquez sur **OK**.

## Edition d'une description de balise
{: #edit_tags}

1. Dans l'onglet **Balise**, sélectionnez la balise à éditer.
1. Cliquez sur l'icône d'édition.
1. Editez la description de la balise, puis cliquez sur le bouton **Sauvegarder**.

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


# Utilisation de notifications basées sur les balises
{: #using_tags}


Les notifications en fonction d'une balise sont des messages de notification qui sont envoyés à tous les périphériques abonnés à une balise particulière. Chaque périphérique peut s'abonner à un nombre illimité de balises. Cette section explique comment envoyer des notifications basées sur les balises. Les abonnements sont gérés par l'instance de service Bluemix Push Notifications. Lorsqu'une balise est supprimée, toutes les informations qui lui sont associées, y compris ses abonnés et périphériques, sont supprimées. Aucun désabonnement automatique n'est requis pour cette balise car elle n'existe plus et aucune action supplémentaire n'est requise depuis le côté client.

**Avant de commencer**

Créez des balises sur l'écran **Tag**. Pour plus d'informations sur la création de balises,
voir [Création de balises](t_manage_tags.html).

1. Dans le tableau de bord **Push Notifications**, cliquez sur l'onglet **Notifications**.
1. Sélectionnez l'option **Tags** pour envoyer des notifications basées sur les balises.
1. Dans la zone **Search** pour le balises, recherchez les balises que vous voulez utiliser, puis cliquez sur le bouton **+Add**.![Ecran Notifications](images/tag_notification.jpg)
1. Accédez à la zone **Create Your Notifications** et dans la zone **Message Text**, entrez le texte à
envoyer dans votre notification.
1. Cliquez sur le bouton **Send**.
