---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#Erweiterte Push-Benachrichtigungen aktivieren
Letzte Aktualisierung: 11. Januar 2017
{: .last-updated}

Konfigurieren Sie ein iOS Badge, zusätzliche JSON-Nutzdaten, umsetzbare Benachrichtigungen und Blockierungsnachrichten.

## Audio, Nutzdaten und iOS Badge konfigurieren
{: #badge-sound-payload}

Konfigurieren Sie ein iOS Badge, eine Audiodatei und zusätzliche JSON-Nutzdaten.

1. Navigieren Sie im Dashboard für Push-Benachrichtigungen zur Registerkarte **Benachrichtigungen**.
2. Konfigurieren Sie im Abschnitt **Optionale Felder** die folgenden Komponenten für Push-Benachrichtigungen. 
	- **Sound File** (Audiodatei) - Geben Sie eine Zeichenfolge ein, die auf die Audiodatei in Ihrer mobilen App verweist. Geben Sie den Zeichenfolgenamen der zu verwendenden Audiodatei in den Nutzdaten an.
	- **iOS Badge**: Für iOS-Geräte die Nummer, die als Badge für das App-Symbol angezeigt werden soll. Wenn diese Eigenschaft fehlt, wird das Badge nicht geändert. Um das Badge zu entfernen, legen Sie für diese Eigenschaft den Wert 0 fest.
	
###Android

Fügen Sie die Audiodatei zum Verzeichnis `res/raw` der Android-Anwendung hinzu. Fügen Sie beim Senden einer Benachrichtigung den Namen der Audiodatei zum entsprechenden Feld für {{site.data.keyword.mobilepushshort}} hinzu.

```
"settings": {
     "gcm" : {
     "sound":"tt.wav",
	  }
 }  
```
    {: codeblock}	
	
###iOS

```
"settings": {
     "apns" : {
      "badge": 10,
	      "sound": "tt.wav",
	  }
}
``` 
	{: codeblock}
		
**Zusätzliche Nutzdaten** - Diese Nutzdaten können ein beliebiges Schlüssel/Wert-Paar sein; es muss sich jedoch um ein JSON-Objekt handeln, das Sie mit der Push-Benachrichtigung senden möchten.

```
{"key":"value", "key2":"value2"}
```
	{: codeblock}

## Android-Benachrichtigungen blockieren 
{: #hold-notifications-android}

Wenn Ihre Anwendung in den Hintergrund wechselt, ist es möglicherweise wünschenswert, dass {{site.data.keyword.mobilepushshort}} solche Benachrichtigungen vorübergehend blockiert, die an Ihre Anwendung gesendet wurden. Rufen Sie zum Blockieren von Benachrichtigungen die Methode 'hold()' in der Methode 'onPause()' der Aktivität auf, die Push-Benachrichtigungen verarbeitet.

```
@Override
protected void onPause() {
    super.onPause();
    if (push != null) {
        push.hold();
    }
} 
```
	{: codeblock}
## Umsetzbare iOS-Benachrichtigungen aktivieren  
{: #enable-actionable-notifications-ios}

Im Gegensatz zu konventionellen Push-Benachrichtigungen werden Benutzer bei umsetzbaren Benachrichtigungen dazu aufgefordert, bei Erhalt des Benachrichtigungsalerts
eine Auswahl zu treffen, ohne die App zu öffnen. 

Führen Sie die entsprechenden Schritte aus, um umsetzbare Push-Benachrichtigungen in Ihrer Anwendung zu aktivieren.

1. Erstellen Sie eine Benutzeraktion.
```
//For Swift
	let acceptAction = UIMutableUserNotificationAction()
	acceptAction.identifier = "ACCEPT_ACTION"
	acceptAction.title = "Accept"
	acceptAction.destructive = false
	acceptAction.authenticationRequired = false
	acceptAction.activationMode = UIUserNotificationActivationMode.Foreground
```
	{: codeblock}
```
//For Swift
	let declineAction = UIMutableUserNotificationAction()
	declineAction.identifier = "DECLINE_ACTION"
	declineAction.title = "Decline"
	declineAction.destructive = true
	declineAction.authenticationRequired = false
	declineAction.activationMode = UIUserNotificationActivationMode.Background
```
	{: codeblock}

2. Erstellen Sie die Benachrichtigungskategorie und legen Sie eine Aktion fest. Gültige Kontexte sind **UIUserNotificationActionContextDefault** oder **UIUserNotificationActionContextMinimal**.
```
// For Swift
	let pushCategory = UIMutableUserNotificationCategory()
	pushCategory.identifier = "TODO_CATEGORY"
	pushCategory.setActions([acceptAction, declineAction], forContext: UIUserNotificationActionContext.Default)
```
	{: codeblock}

1. Erstellen Sie die Benachrichtigungseinstellung und weisen Sie die Kategorien aus dem vorherigen Schritt zu.
```
// For Swift
	let categories = NSSet(array:[pushCategory]);
```
	{: codeblock}

1. Erstellen Sie die lokale oder ferne Benachrichtigung und weisen Sie ihr die Identität der Kategorie zu.
```
//For Swift
	let settings = UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound], categories: categories as? Set<UIUserNotificationCategory>)
    UIApplication.sharedApplication().registerUserNotificationSettings(settings)
    UIApplication.sharedApplication().registerForRemoteNotifications() 
```
	{: codeblock}
	
## Umsetzbare iOS-Benachrichtigungen verarbeiten  
{: #actionable-notifications}

Wenn eine umsetzbare Benachrichtigung empfangen wird, wird die Steuerung basierend auf der ausgewählten Kennung an die folgende Methode weitergeleitet.

 
```
func application(application: UIApplication, handleActionWithIdentifier identifier: String?, forRemoteNotification userInfo: [NSObject : AnyObject], completionHandler: () -> Void) {
      //must call completion handler when finished
      completionHandler()
  }
```    
	{: codeblock}
    
