---

copyright:
 years: 2015, 2016

---


# Registrazione del dispositivo con l'ID utente
{: #register_device_with_userId}
*Ultimo aggiornamento: 20 luglio 2016*
{: .last-updated}

Per registrare la notifica basate sull'ID utente, completa la seguente procedura:

## Android
 
Inizializza la classe IMFPush con il `pushTenantId` e la chiave `clientSecret` del Push Notification service.

```
// Inizializza MFPPush
push = MFPPush.getInstance();
push.initializeBluemixPushWithClientSecret(getApplicationContext(),"clientSecret");
```

**clientSecret** 

Questa è la chiave clientSecret del Push Notifications service.


Utilizza l'API **registerWithUserId** per registrare il dispositivo per le notifiche di push.

```
// Registra il dispositivo per il servizio push notifications.
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

Passa il valore ID utente univoco per la registrazione per le notifiche di push.

>**Nota:** per abilitare le notifiche di push indirizzate dall'ID utente, assicurati di aver registrato il dispositivo con un ID utente e inoltre di passare il 'clientSecret' assegnato quando viene eseguito il provisioning dei Push Notifications service. Se non passi un clientSecret valido, la registrazione del dispositivo avrà esito negativo.


## Cordova

Copia il seguente frammento di codice nella tua applicazione mobile per registrare le notifiche basate sull'ID.

Inizializza `MFPPush` con `clientsecret`. 

```
MFPPush.initializeBluemixPushWithClientSecret("clientSecret");
```

**clientSecret** 

Questa è la chiave clientSecret del Push Notifications service.

```
//Registra la notifica di push con l'ID utente
var userId = "userId";
MFPPush.registerWithUserId(userId,success,failure);
```
**userId** 

Passa il valore ID utente univoco per la registrazione per il Push Notification service.


## Objective-C


Utilizza le seguenti API per registrare le notifiche di push basate sull'ID utente.


```
// Inizializza MFPPush
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeBluemixPushWithClientSecret:@"clientSecret"];
```

**clientSecret** 

Questa è la chiave clientSecret del Push Notifications service.


Utilizza l'API **registerWithUserId** per registrare il dispositivo per le notifiche di push.


```
// Registra il dispositivo per il servizio push notifications.
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

Passa il valore ID utente univoco per la registrazione per le notifiche di push.

## Swift

```
// Inizializza BMSPushCliet
let push =  BMSPushClient.sharedInstance
push.initializeBluemixPushWithClientSecret("clientSecret")
```

**clientSecret** 

Questa è la chiave clientSecret del Push Notifications service.

Utilizza l'API **registerWithUserId** per registrare il dispositivo per le notifiche di push.

```
// Registra il dispositivo per il servizio Push Notifications.
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

Passa il valore ID utente univoco per la registrazione per le notifiche di push.


# Utilizzo delle notifiche basate sull'ID utente
{: #using_userid}


Le notifiche basate sull'ID utente sono messaggi di notifica destinati a uno specifico utente. Possono essere registrati con un utente molti dispositivi. I seguenti passi descrivono come inviare le notifiche basate sull'ID utente. 

1. Dal dashboard **Push Notification**, fai clic sulla scheda **Notifications**.
1. Seleziona l'opzione **UserId** per inviare notifiche basate sull'ID utente.
1. Nel campo **Search** UserId, cerca gli ID utente che vuoi utilizzare e fai quindi clic sul pulsante **+Add**.![Schermata notifiche](images/tag_notification.jpg)
1. Nel campo **Message Text**, immetti il testo che vuoi inviare nella tua notifica.
1. Fai clic sul pulsante **Send**.
