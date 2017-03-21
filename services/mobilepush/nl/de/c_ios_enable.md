---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#iOS-Anwendungen für das Senden von Push-Benachrichtigungen aktivieren
{: #enable-push-ios-notifications}
Letzte Aktualisierung: 14. Februar 2017
{: .last-updated}

Sie können iOS-Anwendungen für das Senden von Push-Benachrichtigungen an Ihre Geräte aktivieren.


##CocoaPods installieren
{: #enable-push-ios-notifications-install}

Für ein vorhandenes Xcode-Projekt können Sie das Bluemix Mobile Services-Client-SDK mithilfe des Abhängigkeitsmanagementtools CocoaPods einrichten. Als Alternative dazu können Sie das Software-Development-Kit (SDK) manuell installieren.

Informationen zu Swift Push finden Sie in der [Readme-Datei ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}.



1. Installieren Sie CocoaPods, indem Sie in Ihrem Mac-Terminal folgenden Befehl verwenden.
```$ sudo gem install cocoapods
```
	{: codeblock}
2. Geben Sie den Befehl `pod init` in das Terminal ein, um CocoaPods zu initialisieren. Führen Sie den Befehl unbedingt aus dem Verzeichnis aus, in dem sich Ihr Xcode-Projekt befindet. Mit dem Befehl `pod init` wird eine Datei 'Podfile' erstellt.  
3. Fügen Sie in der generierten Datei 'Podfile' die erforderlichen SDK-Abhängigkeiten hinzu. Kopieren Sie die folgende Datei 'Podfile'.
   
	```
		source 'https://github.com/CocoaPods/Specs.git'
	// Copy the following list as is and remove the dependencies you do not need.
		use_frameworks!
		target 'MyApp' do
	    platform :ios, '8.0'
		pod 'BMSCore'
	    pod 'BMSPush'
      pod 'BMSAnalyticsAPI'
	end
	```
		{: codeblock}

3. Wechseln Sie am Terminal in Ihren Projektordner und installieren Sie die Abhängigkeiten mithilfe des Befehls `pod update`.

Mit diesem Befehl werden Ihre Abhängigkeiten installiert und es wird ein neuer Xcode-Arbeitsbereich erstellt.  
**Hinweis**: Stellen Sie sicher, dass Sie immer den neuen Xcode-Arbeitsbereich öffnen und nicht die ursprüngliche Xcode-Projektdatei:
```
  $ open App.xcworkspace
```
	{: codeblock}

Der Arbeitsbereich enthält Ihr ursprüngliches Projekt und das Projekt 'Pods', das Ihre Abhängigkeiten enthält. Wenn Sie den Bluemix mobile Services-Quellenordner ändern möchten, finden Sie diesen in Ihrem Projekt 'Pods' unter `Pods/yourImportedSourceFolder`, zum Beispiel: `Pods/BMSPush`.

##Frameworks mit Carthage hinzufügen
{: #carthage}

Fügen Sie mithilfe von [Carthage ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window} Frameworks zu Ihrem Projekt hinzu. Beachten Sie, dass Carthage in Xcode8 nicht unterstützt wird.

1. Fügen Sie `BMSPush`-Frameworks zur Cartfile hinzu:
```
  github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
	{: codeblock}
2. Führen Sie den Befehl `carthage update` aus. Wenn der Build abgeschlossen ist, ziehen Sie `BMSPush.framework`, `BMSCore.framework` und `BMSAnalyticsAPI.framework` in das Xcode-Projekt.
3. Befolgen Sie die Anweisungen auf der [Carthage-Website ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}, um die Integration abzuschließen.

##iOS-SDK einrichten
{: ios-sdk}

Richten Sie das iOS-SDK ein. Fügen Sie den folgenden Code der Datei **AppDelegate.swift** in Ihrer Anwendung hinzu. Beachten Sie, dass dies auch bei APNs registriert wird.  
```
  func application(_ application: UIApplication,
didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {  
   BMSPushClient.sharedInstance.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE")
  }
```
    {: codeblock}

##Importierte Frameworks und Quellenordner verwenden
{: using-imported-frameworks}

Referenzieren Sie das SDK in Ihrem Code. Stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind.

- iOS 8.0 oder höher	
- Xcode 7

Schreiben Sie `#import`-Anweisungen für die entsprechenden Header, zum Beispiel:
```
//swift
import BMSCore
import BMSPush
```
		{: codeblock}

Die Push-Readme-Datei für Swift finden Sie in der [Readme-Datei ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}.

**Hinweis**: Durch Aktualisieren Ihres Projekts 'Pods' mithilfe der CocoaPods-Befehle `pod install` oder `pod update` werden die Bluemix Mobile Services-Quellenorder möglicherweise überschrieben. Wenn Sie Ihre angepassten Versionen der ursprünglichen Dateien aufbewahren möchten, müssen Sie sicherstellen, dass für sie ein Backup durchgeführt wird, bevor Sie einen dieser Befehle absetzen.


##Buildeinstellungen
{: build-settings}

Rufen Sie **Xcode > Build Settings > Build Options** auf und setzen Sie **Enable Bitcode** auf **No**.

**Achtung**: Ab iOS 9 können sich Änderungen an der Komponente 'App Transport Security' (ATS) auf die Verarbeitung des Authentifizierungsprozesses auswirken. Die folgenden Blogbeiträge enthalten weitere Informationen zu den Änderungen: [ATS and Bitcode in iOS 9 ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/){: new_window} und [Connect your iOS 9 app to Bluemix today ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/){: new_window}.

## Push-SDK für iOS-Apps initialisieren
{: #enable-push-ios-notifications-initialize}

Das Anwendungs-Delegat für die iOS-Anwendung ist eine übliche Position für den Initialisierungscode. Klicken Sie in Ihrem Push-Dashboard auf den Link **Mobile Systemerweiterungen**, um die Anwendungsroute und die GUID abzurufen.

###Core-SDK initialisieren
{: Initializing-the-core-sdk}


```
// Core-SDK für Swift mit IBM Bluemix-GUID, Route und Region initialisieren
let myBMSClient = BMSClient.sharedInstance
myBMSClient.initialize(bluemixRegion: "Location where your app is hosted.") 
```
	{: codeblock}

### Route, GUID und Bluemix-Region
{: route-guid-bluemix-region}

####appRoute
{: ios-approute}

Gibt die Route an, die der Serveranwendung zugewiesen ist, die Sie in Bluemix erstellt haben.

####GUID
{: ios-guid}

Gibt den eindeutigen Schlüssel an, der der Anwendung zugewiesen wird, die Sie in Bluemix erstellt haben. Bei diesem Wert muss die Groß-/Kleinschreibung beachtet werden.

####bluemixRegionSuffix
{: ios-bluemixRegionSuffix}

Gibt den Standort an, an dem die App gehostet ist. Der Parameter `bluemixRegion` gibt an, welche Bluemix-Bereitstellung verwendet wird. Sie können diesen Wert mit der statischen Eigenschaft `BMSClient.REGION` angeben und einen von drei Werten verwenden:

- BMSClient.Region.usSouth 
- BMSClient.Region.unitedKingdom
- BMSClient.Region.sydney

####AppGUID
{: ios-AppGUID}

Gibt den eindeutigen 'AppGUID'-Schlüssel an, der dem von Ihnen in Bluemix erstellten {{site.data.keyword.mobilepushshort}}-Service zugewiesen wird.

###Client-Push-SDK initialisieren
{: initializing-the-client-Push-SDK}

```
	//Initialize client Push SDK for Swift
let push = BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


## iOS-Anwendungen und -Geräte registrieren
{: #enable-push-ios-notifications-register}


Nach der Installation auf einem Gerät muss eine Anwendung bei APNs registriert werden, um ferne Benachrichtigungen empfangen zu können. Nachdem das von APNs generierte Gerätetoken von der App empfangen worden ist, muss es zurück an den {{site.data.keyword.mobilepushshort}}-Service geleitet werden.

Führen Sie zum Registrieren von iOS-Anwendungen und -Geräten die folgenden Schritte aus:

1. Erstellen Sie eine Back-End-Anwendung.
2. Übergeben Sie das Token an {{site.data.keyword.mobilepushshort}}.


###Back-End-Anwendung erstellen
{: create-a-backend-app}

Erstellen Sie im Bluemix®-Katalog im Abschnitt 'Boilerplates' eine Back-End-Anwendung, mit der der {{site.data.keyword.mobilepushshort}}-Service automatisch an diese Anwendung gebunden wird. Wenn Sie bereits eine Back-End-App erstellt haben, stellen Sie sicher, dass Sie diese App an den {{site.data.keyword.mobilepushshort}} Service binden.


###Tokens an {{site.data.keyword.mobilepushshort}} übergeben
{: pass-token-push-notifications}

Nachdem das Token von APNs empfangen worden ist, leiten Sie es als Teil der Methode `registerDevice:withDeviceToken` an {{site.data.keyword.mobilepushshort}} weiter.

Nachdem das Token von APNs empfangen worden ist, leiten Sie es als Teil der Methode `didRegisterForRemoteNotificationsWithDeviceToken` an Push Notifications weiter.

```
  func application (_application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data){
   let push =  BMSPushClient.sharedInstance
   push.registerWithDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
      if error.isEmpty {
           print( "Response during device registration : \(response)")
            print( "status code during device registration : \(statusCode)")
        }
       else{
            print( "Error during device registration \(error) ")
           print( "Error during device registration \n  - status code: \(statusCode) \n Error :\(error) \n")
        }
   }
  }
```
	{: codeblock}


## Push-Benachrichtigungen in iOS-Geräten empfangen
{: #enable-push-ios-notifications-receiving}


Um Push-Benachrichtigungen in iOS-Geräten zu empfangen, fügen Sie die folgende Swift-Methode zum Anwendungs-Delegat Ihrer Anwendung hinzu.

```
  // For Swift
func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) 
  { //UserInfo dictionary will contain data sent from the server }
```
	{: codeblock}

## Push-Benachrichtigungen in iOS-Geräten überwachen
{: ios-monitoring}

Um den aktuellen Status der Benachrichtigung zu überwachen, fügen Sie die folgende Swift-Methode zum Anwendungs-Delegat Ihrer Anwendung hinzu.

```
	// Send notification status when app is opened by clicking the notifications
func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any]) {
 	let push =  BMSPushClient.sharedInstance
 let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 let data = respJson.data(using: String.Encoding.utf8)
 	let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 let messageId:String = jsonResponse.value(forKey: "nid") as! String
    push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
      print("Send message status to the Push server")
     }
}
```
	{: codeblock}

```
	// Send notification status when the app is in background mode.
	func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
 	let payLoad = ((((userInfo as NSDictionary).value(forKey: "aps") as! NSDictionary).value(forKey: "alert") as! NSDictionary).value(forKey: "body") as! NSString)
 self.showAlert(title: "Recieved Push notifications", message: payLoad)
 let push =  BMSPushClient.sharedInstance
 let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 let data = respJson.data(using: String.Encoding.utf8)
 	let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 let messageId:String = jsonResponse.value(forKey: "nid") as! String
 push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
       completionHandler(UIBackgroundFetchResult.newData)
   }
}
```
	{: codeblock}


## Einfache Push-Benachrichtigungen senden
{: #send}

Nach dem Entwickeln Ihrer Anwendungen können Sie einfache Push-Benachrichtigungen senden.

Führen Sie die Schritte aus, um einfache Push-Benachrichtigungen zu senden:

1. Wählen Sie **Benachrichtigungen senden** aus und erstellen Sie eine Nachricht, indem Sie eine Option für **Senden an** auswählen. Die unterstützten Optionen sind **Gerät nach Tag**, **Geräte-ID**, **Benutzer-ID**, **Android-Geräte**, **iOS-Geräte**, **Webbenachrichtigungen** und **Alle Geräte**.  
**Hinweis**: Wenn Sie die Option **Alle Geräte** auswählen, erhalten alle Geräte, die Push-Benachrichtigungen subskribiert haben, Benachrichtigungen.
![Anzeige 'Benachrichtigungen'](images/tag_notification.jpg)

2. Erstellen Sie Ihre Nachricht im Feld **Nachricht**. Treffen Sie Ihre Auswahl, um die optionalen Einstellungen wie erforderlich zu konfigurieren.
3. Klicken Sie auf **Senden**.
3. Überprüfen Sie, ob die Geräte Ihre Benachrichtigung empfangen haben.

Die folgende Abbildung zeigt ein Alertfeld bei der Verarbeitung einer {{site.data.keyword.mobilepushshort}} eines iOS-Geräts.

![Push-Benachrichtigung im Vordergrund auf einem iOS-Gerät](images/iOS_Screenshot.jpg) 

### Optionale Einstellungen beim Senden von Benachrichtigungen
{: #send_ios_otpional_setting}

Sie können die {{site.data.keyword.mobilepushshort}}-Einstellungen zum Senden von Benachrichtigung an iOS-Geräte anpassen. Die folgenden optionalen Anpassungsoptionen werden unterstützt:

- **Badge** (Badge): Gibt die Zahl an, die auf dem Anwendungsbadge angezeigt wird. Der Standardwert lautet Null (0) und führt dazu, dass kein Badge angezeigt wird. 
- **Sound** (Audio): Gibt einen Soundclip an, der beim Empfang einer Benachrichtigung abgespielt wird. Unterstützt den Standard oder den Namen einer Soundressource, die in der App gebündelt ist.
- **Additional payload** (Zusätzliche Nutzdaten): Gibt die angepassten Werte für Nutzdaten für Ihre Benachrichtigungen an.

##Interaktive Benachrichtigungen aktivieren

Sie können jetzt Ihre iOS-Benachrichtigungen durch zusätzliche Details wie das Hinzufügen eines Bildes, einer Karte oder einer Antwortschaltfläche attraktiver gestalten, indem Sie interaktive Benachrichtigungen aktivieren. Dadurch wird den Kunden mehr Kontext geboten, verbunden mit der Möglichkeit sofortiger Maßnahmen ohne Verlassen des aktuellen Kontexts.  

Verwenden Sie den folgenden Code zum Aktivieren interaktiver Benachrichtigungen:

```
	// This defines the button action.
	let actionOne = BMSPushNotificationAction(identifierName: "ACCEPT", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
 let actionTwo = BMSPushNotificationAction(identifierName: "DECLINE", buttonTitle: "Decline", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
```
	{: codeblock}
```
	// This defines category for the buttons
let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
```
	{: codeblock}
```
	// This updates the registration to include the buttonsPass the defined category into iOS BMSPushClientOptions
let notificationOptions = BMSPushClientOptions(categoryName: [category])
let push = BMSPushClient.sharedInstance
push.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE", options: notificationOptions)
```
	{: codeblock}

Führen Sie die folgenden Schritte aus, um eine interaktive Benachrichtigung zu senden:

1. Wählen Sie im Abschnitt zum Erstellen für die Dropdown-Liste 'Senden an' **iOS-Geräte** aus.
2. Geben Sie die Benachrichtigungsnachricht ein, die Sie senden möchten.
3. Wählen Sie im Abschnitt mit den optionalen Einstellungen **Mobile** aus und klicken Sie auf **iOS**.
4. Wählen Sie in der Dropdown-Liste 'Typ' **Gemischt** aus.
5. Geben Sie im Feld 'Kategorie' den Benachrichtigungstyp an, den Sie in Ihrer App definiert haben. 

![Interaktive Benachrichtigung für iOS](images/push_ios_notification_interactive.jpg) 

## Nächste Schritte
{: #next_steps_tags}

Nachdem Sie einfache Benachrichtigungen erfolgreich eingerichtet haben, können Sie tagbasierte Benachrichtigungen und erweiterte Optionen konfigurieren.

Fügen Sie diese Funktionen des Push Notifications-Service Ihrer App hinzu.
Informationen zur Verwendung tagbasierter Benachrichtigungen finden Sie in [Tagbasierte Benachrichtigungen](c_tag_basednotifications.html).
Informationen zur Verwendung erweiterter Benachrichtigungsoptionen finden Sie in [Erweiterte Push-Benachrichtigungen aktivieren](t_advance_badge_sound_payload.html).
