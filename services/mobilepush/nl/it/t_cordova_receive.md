---

copyright:
 years: 2015, 2016

---

# Ricezione di notifiche di push sui dispositivi
{: #cordova_receive}

Copia e incolla i seguenti dispositivi di codice per ricevere notifiche di push sui dispositivi.

##JavaScript

Aggiungi il seguente frammento di codice JavaScript alla parte web della tua applicazione Cordova.


```
var notification = function(notification){
    // la notifica è un oggetto JSON.
    alert(notification.message);
};
MFPPush.registerNotificationsCallback(notification);
```

##Proprietà di notifica Android

La seguente selezione elenca le proprietà di notifica Android:

* message - messaggio di notifica di push
* payload - oggetto JSON che contiene un payload di notifica


##Proprietà di notifica iOS

La seguente sezione elenca le proprietà di notifica iOS:

* message - messaggio di notifica di push
* payload - oggetto JSON che contiene un payload di notifica
action-loc-key - la stringa viene utilizzata come una chiave per ottenere una stringa localizzata nella localizzazione corrente da utilizzare per il titolo del pulsante destro invece di “View".
* badge - il numero da visualizzare come badge dell'icona applicazione. Se questa proprietà
                            non è presente, il badge non viene modificato. Per rimuovere il badge, imposta
                            il valore di questa proprietà su 0.
* sound - il nome di un file audio nel bundle dell'applicazione o nella cartella
                            Library/Sounds dei contenitore di dati dell'applicazione.

##Objective-C

Aggiungi i seguenti frammenti di codice Objective-C alla classe delegato della tua applicazione.

```
// Gestisci la ricezione di una notifica remota
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler {

 [[CDVMFPPush sharedInstance] didReceiveRemoteNotification:userInfo];
}
```

```
// Gestisci la ricezione di una notifica all'avvio
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

    [[CDVMFPPush sharedInstance] didReceiveRemoteNotificationOnLaunch:launchOptions];
}
```

##Swift

Aggiungi i seguenti frammenti di codice Swift alla classe delegato della tua applicazione.

```
// Gestisci la ricezione di una notifica remota
funcapplication(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: ){

    CDVMFPPush.sharedInstance().didReceiveRemoteNotification(userInfo)
}
```

```
// Gestisci la ricezione di una notifica remota all'avvio
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

    CDVMFPPush.sharedInstance().didReceiveRemoteNotificationOnLaunch(launchOptions)
}

```
Fase successiva. [Invia notifiche di push di base](t_send_push_notifications.html).
