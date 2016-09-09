---

copyright:
 years: 2015, 2016

---


# Registrazione del dispositivo con l'ID utente
{: #register_device_with_userId}
Ultimo aggiornamento: 16 agosto 2016
{: .last-updated}

Per registrare la notifica basate sull'ID utente, completa la seguente procedura:

## Android
{: android-register}
 
Inizializza la classe MFPPush con le chiavi `AppGUID` e `clientSecret` del servizio {{site.data.keyword.mobilepushshort}}.

```
// Inizializza MFPPush
push = MFPPush.getInstance();
push.initialize(getApplicationContext(),"AppGUID", "clientSecret");
```

####AppGUID
{: push-app-guid}

Questa è la chiave AppGUID del servizio {{site.data.keyword.mobilepushshort}}.

####clientSecret
{: android-client-secret}

Questa è la chiave clientSecret del servizio {{site.data.keyword.mobilepushshort}}.

Utilizza l'API **registerDeviceWithUserId** per registrare il dispositivo per {{site.data.keyword.mobilepushshort}}.

```
// Registra il dispositivo per {{site.data.keyword.mobilepushshort}}.
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

Passa il valore ID utente univoco per la registrazione per {{site.data.keyword.mobilepushshort}}.

**Nota:** per abilitare le {{site.data.keyword.mobilepushshort}} indirizzate dall'ID utente, assicurati di aver registrato il dispositivo con un ID utente e inoltre di passare il 'clientSecret' assegnato quando viene eseguito il provisioning dei servizi {{site.data.keyword.mobilepushshort}}. Se non passi un clientSecret valido, la registrazione del dispositivo avrà esito negativo.


## Cordova
{: cordova-register}

Copia il seguente frammento di codice nella tua applicazione mobile per registrare le notifiche basate sull'ID utente. 

Inizializza `MFPPush` con `clientsecret`. 

```
MFPPush.initialize("appGUID", "clientSecret");
```

###appGUID 
{: cordova-pushappguid}

Questa è la chiave AppGUID del servizio {{site.data.keyword.mobilepushshort}}. 

####clientSecret 
{: cordova-client-secret}

Questa è la chiave clientSecret del servizio {{site.data.keyword.mobilepushshort}}.

```
//Registra {{site.data.keyword.mobilepushshort}} con l'ID utente
var userId = "userId";
MFPPush.registerDevice({},success,failure,userId);
```
####userId
{: cordova-user-id}

Passa il valore ID utente univoco per la registrazione per il servizio {{site.data.keyword.mobilepushshort}}.


## Objective-C
{: objc-register}

Utilizza le seguenti API per registrare le {{site.data.keyword.mobilepushshort}} basate sull'ID utente.

```
// Inizializza MFPPush
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID" clientSecret:@"clientSecret"];
```
###AppGUID 
{: objc-pushappguid}

Questa è la chiave AppGUID del servizio {{site.data.keyword.mobilepushshort}}.

####clientSecret
{: objc-client-secret}

Questa è la chiave clientSecret del servizio {{site.data.keyword.mobilepushshort}}.

Utilizza l'API **registerWithUserId** per registrare il dispositivo per {{site.data.keyword.mobilepushshort}}.

```
// Registra il dispositivo per il servizio push notifications.
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

Passa il valore ID utente univoco per la registrazione per {{site.data.keyword.mobilepushshort}}.

## Swift
{: swift-register}

```
// Inizializza BMSPushClient
let push =  BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```

####AppGUID 
{: swift-pushappguid}
Questa è la chiave AppGUID del servizio {{site.data.keyword.mobilepushshort}}.

####clientSecret
{: swift-client-secret} 

Questa è la chiave clientSecret del servizio {{site.data.keyword.mobilepushshort}}.

Utilizza l'API **registerWithUserId** per registrare il dispositivo per {{site.data.keyword.mobilepushshort}}.

```
// Registra il dispositivo per il servizio Push Notifications.
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

Passa il valore ID utente univoco per la registrazione per {{site.data.keyword.mobilepushshort}}.


# Utilizzo delle notifiche basate sull'ID utente
{: #using_userid}


Le notifiche basate sull'ID utente sono messaggi di notifica destinati a uno specifico utente. Possono essere registrati con un utente molti dispositivi. I seguenti passi descrivono come inviare le notifiche basate sull'ID utente. 

1. Dal dashboard **Push Notification**, fai clic sulla scheda **Notifications**.
1. Seleziona l'opzione **UserId** per inviare notifiche basate sull'ID utente.
1. Nel campo **Search** UserId, cerca gli ID utente che vuoi utilizzare e fai quindi clic sul pulsante **+Add**.![Schermata notifiche](images/user_notification.jpg)
1. Nel campo **Message Text**, immetti il testo che vuoi inviare nella tua notifica.
1. Fai clic sul pulsante **Send**.
