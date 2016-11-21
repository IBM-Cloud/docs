---

copyright:
 years: 2015, 2016

---


# Ein Gerät mit einer Benutzer-ID registrieren
{: #register_device_with_userId}
Letzte Aktualisierung: 17. Oktober 2016
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
	{: codeblock}

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
	{: codeblock}

####userId
{: android-user-id}

Übergeben Sie die eindeutige Benutzer-ID für die Registrierung bei {{site.data.keyword.mobilepushshort}}.

**Hinweis:** Um {{site.data.keyword.mobilepushshort}} zu aktivieren, die auf einer Benutzer-ID basieren, müssen Sie sicherstellen, dass Sie das Gerät mit einer Benutzer-ID registrieren und außerdem den geheimen Clientschlüssel ('clientSecret') übergeben, der bei der Bereitstellung der {{site.data.keyword.mobilepushshort}}-Services zugeordnet wird. Die Geräteregistrierung schlägt ohne einen gültigen geheimen Clientschlüssel fehl.


## Objective-C
{: objc-register}

Verwenden Sie die folgenden APIs für die Registrierung von Push-Benachrichtigungen auf Benutzer-ID-Basis.
```
// Initialize the MFPPush
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID" clientSecret:@"clientSecret"];
```
	{: codeblock}

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
	{: codeblock}

####userId
{: objc-user-id}

Übergeben Sie die eindeutige Benutzer-ID für die Registrierung bei {{site.data.keyword.mobilepushshort}}.

## Swift
{: swift-register}

```
// Initialize the BMSPushClient
let push =  BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}

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
	{: codeblock}

####userId
{: swift-user-id}

Übergeben Sie die eindeutige Benutzer-ID für die Registrierung bei {{site.data.keyword.mobilepushshort}}.

## Google Chrome und Mozilla Firefox
{: web-register}

Verwenden Sie die folgenden APIs, um die Registrierung für Benachrichtigungen durchzuführen, die auf einer Benutzer-ID basieren. Initialisieren Sie das SDK mit `app GUID`, `app Region` und `Client Secret`.

```
var bmsPush = new BMSPush();
var params = {
    "appGUID":"push app GUID",
    "appRegion":"App Region",
    "clientSecret":"Push Client Secret" 
    }
  bmsPush.initialize(params, function(response){
          alert(response.response)
    })
```
	{: codeblock}
  
Nach der erfolgreichen Registrierung registrieren Sie die Webanwendung bei der Benutzer-ID.

```
bmsPush.registerWithUserId("UserId", function(response) {
 alert(response.response)
  })
```
	{: codeblock}

## Google Chrome-Apps und Erweiterungen
{: web-register-new}

Verwenden Sie die folgenden APIs, um die Registrierung für Benachrichtigungen durchzuführen, die auf einer Benutzer-ID basieren. Initialisieren Sie das SDK mit `app GUID`, `app Region` und `Client Secret`.

```
var bmsPush = new BMSPush();
var params = {
    "appGUID":"push app GUID",
    "appRegion":"App Region",
    "clientSecret":"Push Client Secret"
    }
  bmsPush.initialize(params, function(response){
          alert(response.response)
    })
```
	{: codeblock}
  
Nach der erfolgreichen Registrierung registrieren Sie die Webanwendung bei der Benutzer-ID.

```
bmsPush.registerWithUserId("UserId", function(response) {
 alert(response.response)
  })
```
	{: codeblock}

# Benachrichtigungen, die auf einer Benutzer-ID basieren
{: #using_userid}


Die Benachrichtigungen, die auf einer Benutzer-ID basieren, sind Benachrichtigungsnachrichten, deren Ziel ein bestimmter Benutzer ist. Viele Geräte können mit einem einzigen Benutzer registriert werden. In den folgenden Schritten wird beschrieben, wie Benachrichtigungen auf Benutzer-ID-Basis gesendet werden.

1. Wählen Sie im Dashboard **Push-Benachrichtigungen** die Option **Benachrichtigung senden** aus.
1. Wählen Sie die **Benutzer-ID** in der Liste der Optionen **Senden an** aus.
1. Suchen Sie im Feld **Benutzer-ID** nach der Benutzer-ID, die Sie verwenden möchten, und klicken Sie anschließend auf **Hinzufügen**.![Notifications Screen](images/user_notification.jpg)
1. Geben Sie im Feld **Nachricht** den Text ein, den Sie in Ihrer Benachrichtigung senden möchten.
1. Klicken Sie auf **Senden**.
