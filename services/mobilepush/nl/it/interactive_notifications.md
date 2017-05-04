---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Notifiche interattive e automatiche  
{: #interactive-notifications}
Ultimo aggiornamento: 03 marzo 2017
{: .last-updated}

Le notifiche interattive consentono agli utenti di rispondere a una notifica senza aprire l'applicazione. Quando viene ricevuta una notifica, il dispositivo visualizza i pulsanti di azione insieme al messaggio di notifica. Le notifiche interattive sono supportare sui dispositivi iOS con versione 8 o successiva. Per le notifiche interattive inviate a dispositivi iOS precedenti alla versione 8, le azioni di notifica non vengono visualizzate.

## Invio di notifiche interattive
{: #send_interactive_notifications}

La notifica interattiva può essere inviata utilizzando il dashboard Push o utilizzando la [Documentazione API REST](t_restapi.html).

Dalla console {{site.data.keyword.mobilepushshort}}: 

1. Nella scheda delle notifiche del dashboard Push, fai clic su **Invia notifica**. 
2. Scegli i tuoi destinatari per la notifica e fai clic su **Avanti**. 
3. Nella pagina di composizione della notifica, può essere inviato un push interattivo impostando il tipo su predefinito o misto e specificando il valore della categoria nella scheda del delle opzioni avanzate. Per configurare il valore della categoria sul client, controlla **Gestione {{site.data.keyword.mobilepushshort}}** interattiva nella sezione dell'applicazione iOS nativa.

## Gestione di notifiche interattive su un'applicazione iOS
{: #send_interactive_notifications_ios}

### Swift
{: #send_interactive_notifications_ios_swift}

Completa la seguente procedura per ricevere le notifiche interattive:

1. Abilita la funzionalità dell'applicazione ad eseguire attività in background per la ricezione di notifiche remote. 
1. Inizializza l'SDK `BMSPush` con la tua categoria di azione.
	```
	let myBMSClient = BMSClient.sharedInstance
	myBMSClient.initialize(bluemixRegion: BMSClient.Region.usSouth)
	let push =  BMSPushClient.sharedInstance
    let actionOne = BMSPushNotificationAction(identifierName: "FIRST", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
   	let actionTwo = BMSPushNotificationAction(identifierName: "SECOND", buttonTitle: "Reject", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
   	let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
   	let notifOptions = BMSPushClientOptions(categoryName: [category])
	push.initializeWithAppGUID(appGUID: "YOUR_APP_GUID", clientSecret:"YOUR_APP_CLIENT_SECRET", options: notifOptions)
	```
		{: codeblock}

1. Implementa il nuovo metodo di callback su AppDelegate:
	```
	 func userNotificationCenter(_ center: UNUserNotificationCenter,
       didReceive response: UNNotificationResponse,
       withCompletionHandler completionHandler: @escaping () -> Void) {
            switch response.actionIdentifier {
		    case "FIRST":
		      print("FIRST")
		    case "SECOND":
		      print("SECOND")  
		    default:
		      print("Unknown action")
		    }
		completionHandler
	}
	```
	{: codeblock} 
5. Questo nuovo metodo di callback viene richiamato quando l'utente fa clic sul pulsante azione. L'implementazione di questo metodo deve eseguire le azioni associate con l'identificativo specificato ed eseguire il blocco nel parametro `completionHandler`.


### Cordova
{: #send_interactive_notifications_ios_cordova}

Per ottenere una notifica operativa in un'applicazione iOS Cordova, completa la procedura:

1. Aggiungi il campo di categoria all'interno del metodo `BMSPush.initialize`.
   ```
	var category =  {"Category_Name":[{"IdentifierName_1":"actionName_1"},{"IdentifierName_2":"actionName_2"}]}
       BMSPush.initialize(appGUID,clientSecret,category);
    ```
	{: codeblock} 
2. Implementa il nuovo metodo di callback su AppDelegate.
3. Questo nuovo metodo di callback viene richiamato quando l'utente fa clic sul pulsante azione. L'implementazione di questo metodo deve eseguire le attività associate con l'identificativo specificato ed eseguire il blocco nel parametro completionHandler.

## Gestione di notifiche automatiche per iOS
{: #send_silent_notifications_for_ios}

Le notifiche automatiche non vengono visualizzate sulla schermata del dispositivo. Queste notifiche vengono ricevute dall'applicazione in background, che la attivano per 30 secondi in modo che esegua l'attività in background specificata. Un utente non viene avvisato dell'arrivo della notifica. Per inviare notifiche automatiche per iOS, utilizza l'[API REST![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://mobile.{DomainName}/imfpush/){: new_window}.   

1. Per inviare notifiche automatiche, implementa il seguente metodo nel file `appDelegate.m` nel tuo progetto. In Swift, il valore `contentAvailable` inviato dal server per le notifiche automatiche è uguale a 1.
```
// Per Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       let contentAPS = userInfo["aps"] as [NSObject : AnyObject]
       if let contentAvailable = contentAPS["content-available"] as? Int {
           //silent or mixed push
           if contentAvailable == 1 {
               completionHandler(UIBackgroundFetchResult.NewData)
           } else {
               completionHandler(UIBackgroundFetchResult.NoData)
           }
       } else {
    //Notifica predefinita
           completionHandler(UIBackgroundFetchResult.NoData)
       }
    }
```
	{: codeblock}

