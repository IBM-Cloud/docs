---

copyright:
 years: 2015, 2016

---


# Gerät mit Benutzer-ID registrieren
{: #register_device_with_userId}
Letzte Aktualisierung: 16. August 2016
{: .last-updated}

Führen Sie die folgenden Schritte aus, um eine Registrierung für die Benachrichtigung auf Benutzer-ID-Basis durchzuführen:

## Android
{: android-register}
 
Initialisieren Sie die Klasse 'MFPPush' mit dem Schlüssel `AppGUID` und dem Schlüssel `clientSecret` des {{site.data.keyword.mobilepushshort}}-Service. 

```
// Initialize the MFPPush
push = MFPPush.getInstance();
push.initialize(getApplicationContext(),"AppGUID", "clientSecret");
```

####AppGUID
{: push-app-guid}

Dies ist der 'AppGUID'-Schlüssel des {{site.data.keyword.mobilepushshort}}-Service. 

####clientSecret
{: android-client-secret}

Dies ist der geheime Clientschlüssel des {{site.data.keyword.mobilepushshort}}-Service. 

Verwenden Sie die API **registerDeviceWithUserId**, um das Gerät für Push-Benachrichtigungen zu registrieren.

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

Übergeben Sie den Wert der eindeutigen Benutzer-ID zur Registrierung für Push-Benachrichtigungen. 

**Anmerkung:** Um Push-Benachrichtigungen zu aktivieren, die auf einer Benutzer-ID basieren, müssen Sie sicherstellen, dass Sie das Gerät mit einer Benutzer-ID registrieren und außerdem den geheimen Clientschlüssel ('clientSecret') übergeben, der bei der Bereitstellung der {{site.data.keyword.mobilepushshort}}-Services zugeordnet wird. Wenn Sie keinen gültigen geheimen Clientschlüssel ('clientSecret') übergeben, schlägt die Geräteregistrierung fehl. 


## Cordova
{: cordova-register}

Kopieren Sie das folgende Code-Snippet in Ihre mobile Anwendung, um die Registrierung für Benachrichtigungen durchzuführen, die auf einer Benutzer-ID basieren. 

Initialisieren Sie `MFPPush` mit `clientsecret`. 

```
MFPPush.initialize("appGUID", "clientSecret");
```

###appGUID 
{: cordova-pushappguid}

Dies ist der 'AppGUID'-Schlüssel des {{site.data.keyword.mobilepushshort}}-Service.  

####clientSecret 
{: cordova-client-secret}

Dies ist der geheime Clientschlüssel des {{site.data.keyword.mobilepushshort}}-Service. 

```
//Register for {{site.data.keyword.mobilepushshort}} with userId
var userId = "userId";
MFPPush.registerDevice({},success,failure,userId); 
```
####userId
{: cordova-user-id}

Übergeben Sie den Wert der eindeutigen Benutzer-ID zur Registrierung beim {{site.data.keyword.mobilepushshort}}-Service. 


## Objective-C
{: objc-register}

Verwenden Sie die folgenden APIs für die Registrierung von Push-Benachrichtigungen auf Benutzer-ID-Basis. 

```
// Initialize the MFPPush
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID" clientSecret:@"clientSecret"]; 
```
###AppGUID 
{: objc-pushappguid}

Dies ist der 'AppGUID'-Schlüssel des {{site.data.keyword.mobilepushshort}}-Service. 

####clientSecret
{: objc-client-secret}

Dies ist der geheime Clientschlüssel des {{site.data.keyword.mobilepushshort}}-Service. 

Verwenden Sie die API **registerWithUserId**, um das Gerät für Push-Benachrichtigungen zu registrieren. 

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

Übergeben Sie den Wert der eindeutigen Benutzer-ID zur Registrierung für Push-Benachrichtigungen. 

## Swift
{: swift-register}

```
// Initialize the BMSPushClient
let push =  BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```

####AppGUID 
{: swift-pushappguid}
Dies ist der 'AppGUID'-Schlüssel des {{site.data.keyword.mobilepushshort}}-Service. 

####clientSecret
{: swift-client-secret} 

Dies ist der geheime Clientschlüssel des {{site.data.keyword.mobilepushshort}}-Service. 

Verwenden Sie die API **registerWithUserId**, um das Gerät für Push-Benachrichtigungen zu registrieren. 

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

Übergeben Sie den Wert der eindeutigen Benutzer-ID zur Registrierung für Push-Benachrichtigungen. 


# Benachrichtigungen auf Benutzer-ID-Basis verwenden
{: #using_userid}


Benutzer-ID-basierte Benachrichtigungen sind Benachrichtigungen, deren Ziel ein bestimmter Benutzer ist. Viele Geräte können mit einem einzigen Benutzer registriert werden. In den folgenden Schritten wird beschrieben, wie Benachrichtigungen auf Benutzer-ID-Basis gesendet werden. 

1. Klicken Sie im **Push Notification**-Dashboard auf die Registerkarte **Benachrichtigungen**.
1. Wählen Sie die Option **Benutzer-ID** aus, um Benachrichtigungen auf Benutzer-ID-Basis zu senden.
1. Suchen Sie mit dem Feld **Suche** für Benutzer-IDs diejenige Benutzer-ID, die Sie verwenden möchten, und klicken Sie anschließend auf die Schaltfläche **Hinzufügen**.![Anzeige 'Benachrichtigungen'](images/user_notification.jpg)
1. Geben Sie im Feld **Nachrichtentext** den Text ein, der in Ihrer Benachrichtigung gesendet werden soll.
1. Klicken Sie auf die Schaltfläche **Senden**.
