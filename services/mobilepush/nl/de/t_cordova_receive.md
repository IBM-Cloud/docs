---

copyright:
 years: 2015, 2016

---

# Push-Benachrichtigungen in Geräten empfangen
{: #cordova_receive}

Kopieren Sie die folgenden Code-Snippets und fügen Sie sie ein, um Push-Benachrichtigungen
auf Geräten zu empfangen.

##JavaScript

Fügen Sie das folgende JavaScript-Code-Snippet in die Webkomponente Ihrer Cordova-Anwendung ein.


```
var notification = function(notification){
    // notification is a JSON object.
    alert(notification.message);
};
MFPPush.registerNotificationsCallback(notification);
```

##Eigenschaften für Android-Benachrichtigungen

Im folgenden Abschnitt sind die Eigenschaften für Android-Benachrichtigungen aufgelistet:

* message - Push-Benachrichtigung.
* payload - JSON-Objekt mit den Nutzdaten einer Benachrichtigung.


##Eigenschaften für iOS-Benachrichtigungen

Im folgenden Abschnitt sind die Eigenschaften für iOS-Benachrichtigungen aufgelistet:

* message - Push-Benachrichtigung.
* payload - JSON-Objekt mit den Nutzdaten einer Benachrichtigung.
action-loc-key - Diese Zeichenfolge dient als Schlüssel zum Abrufen einer lokalisierten Zeichenfolge in der aktuellen Lokalisierung, die anstelle von 'View' als Titel für die rechte Schaltfläche verwendet werden soll.
* badge - Die Nummer, die als Badge des App-Symbols angezeigt werden soll. Wenn diese Eigenschaft fehlt, wird das Badge nicht geändert. Um das Badge zu entfernen,
legen Sie für diese Eigenschaft den Wert 0 fest.
* sound - Der Name einer Audiodatei im App-Bundle oder im Ordner 'Library/Sounds'
des Datencontainers der App.

##Objective-C

Fügen Sie die folgenden Objective-C-Code-Snippets zur Klasse 'delegate' Ihrer Anwendung hinzu.

```
// Handle receiving a remote notification
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler {

 [[CDVMFPPush sharedInstance] didReceiveRemoteNotification:userInfo];
}
```

```
// Handle receiving a remote notification on launch
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

    [[CDVMFPPush sharedInstance] didReceiveRemoteNotificationOnLaunch:launchOptions];
}
```

##Swift

Fügen Sie die folgenden Swift-Code-Snippets zur Klasse 'delegate' Ihrer Anwendung hinzu.

```
// Handle receiving a remote notification
funcapplication(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: ){

    CDVMFPPush.sharedInstance().didReceiveRemoteNotification(userInfo)
}
```

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

    CDVMFPPush.sharedInstance().didReceiveRemoteNotificationOnLaunch(launchOptions)
}

```
Nächster Schritt: [Einfache Push-Benachrichtigungen senden](t_send_push_notifications.html).
