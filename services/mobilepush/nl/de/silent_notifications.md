------

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Hintergrundbenachrichtigungen für iOS verarbeiten
{: #silent-notifications}
Letzte Aktualisierung: 16. Januar 2017
{: .last-updated}

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

