---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Interaktive Benachrichtigungen und Hintergrundbenachrichtigungen  
{: #interactive-notifications}
Letzte Aktualisierung: 03. März 2017
{: .last-updated}

Interaktive Benachrichtigungen ermöglichen den Benutzern das Beantworten einer Benachrichtigung, ohne die Anwendung zu öffnen. Wenn eine interaktive Benachrichtigung eingeht, zeigt das Gerät die Aktionsschaltflächen zusammen mit der Benachrichtigung an. Interaktive Benachrichtigungen werden für iOS-Geräte mit Version 8 oder einer neueren Version unterstützt. Wenn interaktive Benachrichtigungen an iOS-Geräte gesendet werden, die mit einer älteren Version als Version 8 ausgeführt werden, werden die Benachrichtigungsaktionen nicht angezeigt.

## Interaktive Benachrichtigungen senden
{: #send_interactive_notifications}

Interaktive Benachrichtigungen können über das Push-Dashboard oder mithilfe der REST-API (siehe [REST-API-Dokumentation](t_restapi.html)) gesendet werden.

Gehen Sie in der {{site.data.keyword.mobilepushshort}}-Konsole wie folgt vor: 

1. Klicken Sie auf der Registerkarte 'Benachrichtigungen' im Push-Dashboard auf **Benachrichtigung senden**. 
2. Wählen Sie die Benachrichtigungsempfänger aus und klicken Sie auf **Weiter**. 
3. Auf der Seite für die Benachrichtigungserstellung können Sie beim Senden von interaktiven Push-Benachrichtigungen den Typ 'Standard' oder 'Gemischt' festlegen und auf der Registerkarte mit den erweiterten Optionen den Kategoriewert angeben. Informationen zum Konfigurieren des Kategoriewerts auf dem Client finden Sie im Abschnitt zur Verarbeitung interaktiver Push-Benachrichtigungen in nativen iOS-Anwendungen.

## Interaktive Push-Benachrichtigungen in einer iOS-Anwendung verarbeiten
{: #send_interactive_notifications_ios}

### Swift
{: #send_interactive_notifications_ios_swift}

Führen Sie die folgenden Schritte aus, um interaktive Benachrichtigungen zu erhalten:

1. Aktivieren Sie die Anwendungsfunktion zum Durchführen von Hintergrundtasks beim Empfang der fernen Benachrichtigungen. 
1. Initialisieren Sie das `BMSPush`-SDK mit Ihrer Aktionskategorie.
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

1. Implementieren Sie die neue Callback-Methode in AppDelegate:
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
5. Diese neue Callback-Methode wird aufgerufen, wenn der Benutzer auf die Aktionsschaltfläche klickt. Die Implementierung dieser Methode muss die Aufgaben durchführen, die der angegebenen ID zugeordnet sind, und den Block im Parameter `completionHandler` ausführen.


### Cordova
{: #send_interactive_notifications_ios_cordova}

Führen Sie die folgenden Schritte aus, um umsetzbare Benachrichtigungen in einer Cordova-iOS-Anwendung zu empfangen:

1. Fügen Sie das Kategoriefeld in der Methode `BMSPush.initialize` hinzu.
   ```
	var category =  {"Category_Name":[{"IdentifierName_1":"actionName_1"},{"IdentifierName_2":"actionName_2"}]}
       BMSPush.initialize(appGUID,clientSecret,category);
    ```
	{: codeblock} 
2. Implementieren Sie die neue Callback-Methode in AppDelegate.
3. Diese neue Callback-Methode wird aufgerufen, wenn der Benutzer auf die Aktionsschaltfläche klickt. Die Implementierung dieser Methode muss die Aufgaben durchführen, die der angegebenen ID zugeordnet sind, und den Block im Parameter 'completionHandler' ausführen.

## Hintergrundbenachrichtigungen für iOS verarbeiten
{: #send_silent_notifications_for_ios}

Hintergrundbenachrichtigungen werden nicht auf dem Gerät angezeigt. Diese Benachrichtigungen werden von der Anwendung im Hintergrund empfangen; dadurch wird die Anwendung für maximal 30 Sekunden aktiviert, um die angegebene Hintergrundtask auszuführen. Der Eingang der Benachrichtigung wird vom Benutzer möglicherweise nicht bemerkt. Verwenden Sie zum Senden von Hintergrundbenachrichtigungen für iOS die [REST-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://mobile.{DomainName}/imfpush/){: new_window}.   

1. Wenn Sie Push-Hintergrundbenachrichtigungen senden möchten, implementieren Sie die folgende Methode in der Datei `appDelegate.m` in Ihrem Projekt. In Swift ist der Wert für `contentAvailable` , der vom Server für Hintergrundbenachrichtigungen gesendet wird, gleich 1.
```
// For Swift
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
    //Default notification 
           completionHandler(UIBackgroundFetchResult.NoData)
       }
    }
```
	{: codeblock}

