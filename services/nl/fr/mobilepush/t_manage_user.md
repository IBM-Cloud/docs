---

copyright:
 years: 2015, 2016

---


# Enregistrement du périphérique avec l'ID utilisateur
{: #register_device_with_userId}
*Dernière mise à jour : 20 juillet 2016*
{: .last-updated}

Pour procéder à un enregistrement pour une notification à base d'ID utilisateur, procédez comme suit :

## Android
 
Initialisez la classe IMFPush avec les clés `pushTenantId` et `clientSecret` du service Notifications Push.

```
// Initialize the MFPPush
push = MFPPush.getInstance();
push.initializeBluemixPushWithClientSecret(getApplicationContext(),"clientSecret");
```

**clientSecret** 

Il s'agit de la clé clientSecret du service Notifications push.


Utilisez l'API **registerWithUserId** pour enregistrer le périphérique pour les notifications push.

```
// Register the device to push notifications service.
push.registerWithUserId("userId",new MFPPushResponseListener<String>() {
    @Override
	    public void onSuccess(String deviceId) {
        updateTextView("Device is registered with Push Service.");
        displayTags();
    }

    @Override
    public void onFailure(MFPPushException ex) {
        updateTextView("Error registering with Push Service...\n"
        + "Push notifications will not be received.");
    }
});
```

**userId** 

Passe la valeur ID utilisateur unique pour l'enregistrement des notifications push.

>**Remarque :** pour activer les notifications push ciblées par ID utilisateur, prenez soin d'enregistrer le périphérique avec un ID utilisateur et passez aussi la clé clientSecret qui est allouée quand les services Notifications Push sont provisionnés. Si vous ne transférez pas une clé clientSecret valide, l'enregistrement du périphérique échoue.
## Cordova

Copiez le fragment de code suivant dans votre application mobile pour effectuer un enregistrement pour des notifications à base d'ID utilisateur.

Initialisez `MFPPush` avec `clientsecret`. 

```
MFPPush.initializeBluemixPushWithClientSecret("clientSecret");
```

**clientSecret** 

Il s'agit de la clé clientSecret du service Notifications push.

```
//Register for Push notification with userId
var userId = "userId";
MFPPush.registerWithUserId(userId,success,failure);
```
**userId** 

Passe la valeur ID utilisateur unique pour l'enregistrement du service Notifications Push.


## Objective-C


Utilisez les API suivantes pour l'enregistrement des notifications push à base d'ID utilisateur.


```
// Initialize the MFPPush
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeBluemixPushWithClientSecret:@"clientSecret"];
```

**clientSecret** 

Il s'agit de la clé clientSecret du service Notifications push.


Utilisez l'API **registerWithUserId** pour enregistrer le périphérique pour les notifications push.


```
// Register the device to push notifications service.
[push registerDeviceToken:deviceToken WithUserId:@"userId" completionHandler:^(IMFResponse *response, NSError *error) {
    NSString *message=@"";
    
	if (error){
        message = [NSString stringWithFormat:@"Error registering for push notifications: %@", error.description];
        NSLog(@"%@",message);
    } else {
        message=@"Successfully registered for push notifications";
        NSLog(@"%@",message);
    }
}];
```


**userId** 

Passe la valeur ID utilisateur unique pour l'enregistrement des notifications push.

## Swift

```
// Initialize the BMSPushCliet
let push =  BMSPushClient.sharedInstance
push.initializeBluemixPushWithClientSecret("clientSecret")
```

**clientSecret** 

Il s'agit de la clé clientSecret du service Notifications push.

Utilisez l'API **registerWithUserId** pour enregistrer le périphérique pour les notifications push.

```
// Register the device to Push Notifications service.
push.registerDeviceToken("deviceToken", WithUserId: "userId")  { (response, statusCode, error) -> Void in
if error.isEmpty {

    print( "Response during device registration : \(response)")

        print( "status code during device registration : \(statusCode)")

    } else {

        print( "Error during device registration \(error) ")
    }
}
```

**userId** 

Passe la valeur ID utilisateur unique pour l'enregistrement des notifications push.


# Utilisation des notifications à base d'ID utilisateur
{: #using_userid}


Les notifications à base d'ID utilisateur sont des messages de notification qui sont ciblés vers un utilisateur spécifique. Plusieurs périphériques différents peuvent être enregistrés avec un seul et même utilisateur. La procédure suivante décrit comment envoyer des notifications à base d'ID utilisateur. 

1. Dans le tableau de bord **Notifications Push**, cliquez sur l'onglet **Notifications**.
1. Sélectionnez l'option relative à l'ID utilisateur pour envoyer des notifications à base d'ID utilisateur.
1. Dans la zone de recherche des ID utilisateur, recherchez l'ID utilisateur que vous voulez utiliser puis cliquez sur le bouton d'ajout.![Ecran des notifications](images/tag_notification.jpg)
1. Dans la zone relative au texte du message, entrez le texte que vous voulez envoyer dans votre notification.
1. Cliquez sur le bouton **Send**.
