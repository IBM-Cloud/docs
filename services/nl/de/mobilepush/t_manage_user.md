---

copyright:
 years: 2015, 2016

---


# Gerät mit Benutzer-ID registrieren
{: #register_device_with_userId}
*Letzte Aktualisierung: 20. Juli 2016*
{: .last-updated}

Führen Sie die folgenden Schritte aus, um eine Registrierung für die Benachrichtigung auf Benutzer-ID-Basis durchzuführen:

## Android
 
Initialisieren Sie die Klasse 'IMFPush' mit den Schlüsseln `pushTenantId` und `clientSecret` des Push Notification-Service.

```
// Initialize the MFPPush
push = MFPPush.getInstance();
push.initializeBluemixPushWithClientSecret(getApplicationContext(),"clientSecret");
```

**clientSecret** 

Dies ist der geheime Clientschlüssel des Push Notifications-Service.


Verwenden Sie die API **registerWithUserId**, um das Gerät für Push-Benachrichtigungen zu registrieren.

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

Übergeben Sie den Wert für die eindeutige Benutzer-ID für die Registrierung von Push-Benachrichtigungen.

>**Anmerkung:** Um Push-Benachrichtigungen zu aktivieren, die auf einer Benutzer-ID basieren, müssen Sie sicherstellen, dass Sie das Gerät mit einer Benutzer-ID registrieren und außerdem den Schlüssel 'clientSecret' übergeben, der bei der Bereitstellung der Push Notifications-Services zugeordnet wird. Wenn Sie keinen gültigen clientSecret übergeben, schlägt die Geräteregistrierung fehl.


## Cordova

Kopieren Sie das folgende Code-Snippet in Ihre mobile Anwendung, um die Registrierung für Benachrichtigungen auf Benutzer-ID-Basis durchzuführen.

Initialisieren Sie `MFPPush` mit `clientsecret`. 

```
MFPPush.initializeBluemixPushWithClientSecret("clientSecret");
```

**clientSecret** 

Dies ist der geheime Clientschlüssel des Push Notifications-Service.

```
//Register for Push notification with userId
var userId = "userId";
MFPPush.registerWithUserId(userId,success,failure);
```
**userId** 

Übergeben Sie den Wert für die eindeutige Benutzer-ID für die Registrierung beim Push Notification-Service.


## Objective-C


Verwenden Sie die folgenden APIs für eine Registrierung für Push-Benachrichtigungen auf Benutzer-ID-Basis.


```
// Initialize the MFPPush
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeBluemixPushWithClientSecret:@"clientSecret"];
```

**clientSecret** 

Dies ist der geheime Clientschlüssel des Push Notifications-Service.


Verwenden Sie die API **registerWithUserId**, um das Gerät für Push-Benachrichtigungen zu registrieren.


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

Übergeben Sie den Wert für die eindeutige Benutzer-ID für die Registrierung von Push-Benachrichtigungen.

## Swift

```
// Initialize the BMSPushCliet
let push =  BMSPushClient.sharedInstance
push.initializeBluemixPushWithClientSecret("clientSecret")
```

**clientSecret** 

Dies ist der geheime Clientschlüssel des Push Notifications-Service.

Verwenden Sie die API **registerWithUserId**, um das Gerät für Push-Benachrichtigungen zu registrieren.

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

Übergeben Sie den Wert für die eindeutige Benutzer-ID für die Registrierung von Push-Benachrichtigungen.


# Benachrichtigungen auf Benutzer-ID-Basis verwenden
{: #using_userid}


Benutzer-ID-basierte Benachrichtigungen sind Benachrichtigungen, deren Ziel ein bestimmter Benutzer ist. Viele Geräte können mit einem einzigen Benutzer registriert werden. In den folgenden Schritten wird beschrieben, wie Benachrichtigungen auf Benutzer-ID-Basis gesendet werden. 

1. Klicken Sie im **Push Notification**-Dashboard auf die Registerkarte **Benachrichtigungen**.
1. Wählen Sie die Option **Benutzer-ID** aus, um Benachrichtigungen auf Benutzer-ID-Basis zu senden.
1. Suchen Sie mithilfe des Felds zum Suchen nach der Benutzer-ID nach der Benutzer-ID, die Sie verwenden möchten, und klicken Sie anschließend auf die Schaltfläche **Hinzufügen**.![Anzeige 'Benachrichtigungen](images/tag_notification.jpg)
1. Geben Sie im Feld **Nachrichtentext** den Text ein, der in Ihrer Benachrichtigung gesendet werden soll.
1. Klicken Sie auf die Schaltfläche **Senden**.
