---

copyright:
 years: 2015, 2016

---


# Enregistrement du périphérique avec l'ID utilisateur
{: #register_device_with_userId}
Dernière mise à jour : 16 août 2016
{: .last-updated}

Pour procéder à un enregistrement pour une notification à base d'ID utilisateur, procédez comme suit :

## Android
{: android-register}
 
Initialisez la classe MFPPush avec l'identificateur `AppGUID` et la clé `clientSecret` du service {{site.data.keyword.mobilepushshort}}.

```
// Initialize the MFPPush
push = MFPPush.getInstance();
push.initialize(getApplicationContext(),"AppGUID", "clientSecret");
```

####AppGUID
{: push-app-guid}

Il s'agit de la clé AppGUID du service {{site.data.keyword.mobilepushshort}}.

####clientSecret
{: android-client-secret}

Il s'agit de la clé clientSecret du service {{site.data.keyword.mobilepushshort}}.

Utilisez l'API **registerDeviceWithUserId** pour enregistrer le périphérique pour {{site.data.keyword.mobilepushshort}}.

```
// Register the device to {{site.data.keyword.mobilepushshort}}.
push.registerDeviceWithUserId("userId",new MFPPushResponseListener<String>() {
    @Override
	    public void onSuccess(String deviceId) {
        Log.d("Device is registered with Push Service.");
    }

    @Override
    public void onFailure(MFPPushException ex) {
        Log.d("Error registering with Push Service...\n"
        + "Push notifications will not be received.");
    }
});
```

####userId
{: android-user-id}

Passe la valeur ID utilisateur unique pour l'enregistrement de {{site.data.keyword.mobilepushshort}}.

**Remarque :** pour activer les notifications de type {{site.data.keyword.mobilepushshort}} ciblées par ID utilisateur, prenez soin d'enregistrer le périphérique avec un ID utilisateur et passez aussi la valeur confidentielle clientSecret qui est allouée quand les services {{site.data.keyword.mobilepushshort}} sont provisionnés. Si vous ne transférez pas une clé clientSecret valide, l'enregistrement du périphérique échoue.


## Cordova
{: cordova-register}

Copiez le fragment de code ci-après sur votre application mobile pour enregistrer un ID utilisateur basé sur des notifications.

Initialisez `MFPPush` avec `clientsecret`. 

```
MFPPush.initialize("appGUID", "clientSecret");
```

###appGUID 
{: cordova-pushappguid}

Il s'agit de la clé AppGUID du service {{site.data.keyword.mobilepushshort}}. 

####clientSecret 
{: cordova-client-secret}

Il s'agit de la clé clientSecret du service {{site.data.keyword.mobilepushshort}}.

```
//Register for {{site.data.keyword.mobilepushshort}} with userId
var userId = "userId";
MFPPush.registerDevice({},success,failure,userId); 
```
####userId
{: cordova-user-id}

Passe la valeur ID utilisateur unique pour l'enregistrement du service {{site.data.keyword.mobilepushshort}}.


## Objective-C
{: objc-register}

Utilisez les API suivantes pour l'enregistrement des notifications de type {{site.data.keyword.mobilepushshort}} à base d'ID utilisateur.

```
// Initialize the MFPPush
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID" clientSecret:@"clientSecret"]; 
```
###AppGUID 
{: objc-pushappguid}

Il s'agit de la clé AppGUID du service {{site.data.keyword.mobilepushshort}}.

####clientSecret
{: objc-client-secret}

Il s'agit de la clé clientSecret du service {{site.data.keyword.mobilepushshort}}.

Utilisez l'API **registerWithUserId** pour enregistrer le périphérique pour {{site.data.keyword.mobilepushshort}}.

```
// Register the device to push notifications service.
[push registerWithDeviceToken:deviceToken WithUserId:@"userId" completionHandler:^(IMFResponse *response, NSError *error) {
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


####userId 
{: objc-user-id}

Passe la valeur ID utilisateur unique pour l'enregistrement de {{site.data.keyword.mobilepushshort}}.

## Swift
{: swift-register}

```
// Initialize the BMSPushClient
let push =  BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```

####AppGUID 
{: swift-pushappguid}
Il s'agit de la clé AppGUID du service {{site.data.keyword.mobilepushshort}}.

####clientSecret
{: swift-client-secret} 

Il s'agit de la clé clientSecret du service {{site.data.keyword.mobilepushshort}}.

Utilisez l'API **registerWithUserId** pour enregistrer le périphérique pour {{site.data.keyword.mobilepushshort}}.

```
// Register the device to Push Notifications service.
push.registerWithDeviceToken("deviceToken", WithUserId: "userId")  { (response, statusCode, error) -> Void in
if error.isEmpty {

    print( "Response during device registration : \(response)")

        print( "status code during device registration : \(statusCode)")

    } else {

        print( "Error during device registration \(error) ")
    }
}
```

####userId 
{: swift-user-id}

Passe la valeur ID utilisateur unique pour l'enregistrement de {{site.data.keyword.mobilepushshort}}.


# Utilisation des notifications à base d'ID utilisateur
{: #using_userid}


Les notifications à base d'ID utilisateur sont des messages de notification qui sont ciblés vers un utilisateur spécifique. Plusieurs périphériques différents peuvent être enregistrés avec un seul et même utilisateur. La procédure suivante décrit comment envoyer des notifications à base d'ID utilisateur. 

1. Dans le tableau de bord **Notifications Push**, cliquez sur l'onglet **Notifications**.
1. Sélectionnez l'option relative à l'ID utilisateur pour envoyer des notifications à base d'ID utilisateur.
1. Dans la zone de recherche des ID utilisateur, recherchez l'ID utilisateur que vous voulez utiliser puis cliquez sur le bouton d'ajout.![Ecran des notifications](images/user_notification.jpg)
1. Dans la zone relative au texte du message, entrez le texte que vous voulez envoyer dans votre notification.
1. Cliquez sur le bouton **Send**.
