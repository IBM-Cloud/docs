---

copyright:
 years: 2015, 2016

---

#iOS-Anwendungen für den Empfang und das Senden von {{site.data.keyword.mobilepushshort}} aktivieren
{: #enable-push-ios-notifications}
Letzte Aktualisierung: 19. Oktober 2016
{: .last-updated}

Sie können iOS-Anwendungen zum Empfangen und Senden von {{site.data.keyword.mobilepushshort}} von bzw. an Ihre Geräte aktivieren.


##CocoaPods installieren
{: #enable-push-ios-notifications-install}

Für ein vorhandenes Xcode-Projekt können Sie das Bluemix Mobile Services-Client-SDK mithilfe des Abhängigkeitsmanagementtools CocoaPods einrichten. Als Alternative dazu können Sie das Software-Development-Kit (SDK) manuell installieren.

Die Push-Readme-Datei für Swift finden Sie in [Readme](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master).



1. Installieren Sie CocoaPods, indem Sie in Ihrem Mac-Terminal folgenden Befehl verwenden.
```
$ sudo gem install cocoapods
```
	{: codeblock}
2. Geben Sie den Befehl `pod init` in das Terminal ein, um CocoaPods zu initialisieren. Führen Sie den Befehl unbedingt aus dem Verzeichnis aus, in dem sich Ihr Xcode-Projekt befindet. Mit dem Befehl `pod init` wird eine Datei 'Podfile' erstellt.  
3. Fügen Sie in der generierten Datei 'Podfile' die erforderlichen SDK-Abhängigkeiten hinzu. Kopieren Sie eine der folgenden 'Podfile'-Dateien nach Bedarf.
 
**Objective-C**
   
```
source 'https://github.com/CocoaPods/Specs.git'
	# Copy the following list as is and remove the dependencies you do not need.
	pod 'IMFCore'
	pod 'IMFPush'
```
	{: codeblock}

**Swift**
   
```
source 'https://github.com/CocoaPods/Specs.git'
	# Copy the following list as is and remove the dependencies you do not need.
use_frameworks!
target 'MyApp' do
	    platform :ios, '9.0'
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

##Carthage
{: #carthage}

Fügen Sie mithilfe von [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) Frameworks zu Ihrem Projekt hinzu. Beachten Sie, dass Carthage in Xcode8 nicht unterstützt wird.

1. Fügen Sie `BMSPush`-Frameworks zur Cartfile hinzu:
```
github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
	{: codeblock}
2. Führen Sie den Befehl `carthage update` aus. Wenn der Build abgeschlossen ist, ziehen Sie `BMSPush.framework`, `BMSCore.framework` und `BMSAnalyticsAPI.framework` in das Xcode-Projekt.
3. Gehen Sie den Anweisungen auf der [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos)-Site entsprechend vor, um die Integration abzuschließen.


##Importierte Frameworks und Quellenordner verwenden
{: using-imported-frameworks}

Referenzieren Sie das SDK in Ihrem Code. Je nach Bedarf verwenden Sie eine der folgenden Methoden.

**Objective-C**

Schreiben Sie `#import`-Anweisungen für die entsprechenden Header, zum Beispiel:

```
	//Objective-C
#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```
	{: codeblock}

**Hinweis**: Durch Aktualisieren Ihres Projekts 'Pods' mithilfe der CocoaPods-Befehle `pod install` oder `pod update` werden die Bluemix Mobile Services-Quellenorder möglicherweise überschrieben. Wenn Sie Ihre angepassten Versionen der ursprünglichen Dateien aufbewahren möchten, müssen Sie sicherstellen, dass für sie ein Backup durchgeführt wird, bevor Sie einen dieser Befehle absetzen.

**Swift**

Stellen Sie sicher, dass folgende Voraussetzungen erfüllt sind:

- iOS 8.0 oder höher
- Xcode 7


Schreiben Sie `#import`-Anweisungen für die entsprechenden Header, zum Beispiel:
```
//swift
import BMSCore
import BMSPush
```
	{: codeblock}
Die Push-Readme-Datei für Swift finden Sie in [Readme](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master).##Buildeinstellungen
{: build-settings}

Rufen Sie **Xcode > Build Settings > Build Options** auf und setzen Sie **Enable Bitcode** auf **No**.

**Achtung**: Ab iOS 9 können sich Änderungen an der Komponente 'App Transport Security' (ATS) auf die Verarbeitung des Authentifizierungsprozesses auswirken. Die folgenden Blogeinträge liefern weitere Informationen zu den Änderungen: [ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) und [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/).

## Push-SDK für iOS-Apps initialisieren
{: #enable-push-ios-notifications-initialize}

Das Anwendungs-Delegat für die iOS-Anwendung ist eine übliche Position für den Initialisierungscode. Klicken Sie in Ihrem Push-Dashboard auf den Link **Mobile Systemerweiterungen**, um die Anwendungsroute und die GUID abzurufen.

###Core-SDK initialisieren
{: Initializing-the-core-sdk}

**Objective-C**

```
// SDK für Object-C mit IBM Bluemix-GUID initialisieren und weiterleiten
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```
	{: codeblock}

**Swift**

```
// Core-SDK für Swift mit IBM Bluemix-GUID, Route und Region initialisieren
let myBMSClient = BMSClient.sharedInstance
myBMSClient.initialize(bluemixRegion: "Location where your app is hosted.")
myBMSClient.defaultRequestTimeout = 10.0 // Zeitlimitüberschreitung in Sekunden
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

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

####AppGUID
{: ios-AppGUID}

Gibt den eindeutigen 'AppGUID'-Schlüssel an, der dem von Ihnen in Bluemix erstellten {{site.data.keyword.mobilepushshort}}-Service zugewiesen wird.

###Client-Push-SDK initialisieren
{: initializing-the-client-Push-SDK}

**Objective-C**

```
//Initialize client Push SDK for Objective-C
IMFPushClient *push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID" clientSecret:@"clientSecret"];
```
	{: codeblock}

**Swift**

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

Erstellen Sie im Bluemix®-Katalog im Abschnitt 'Boilerplates' eine Back-End-Anwendung, mit der der {{site.data.keyword.mobilepushshort}}-Service automatisch an diese Anwendung gebunden wird. Falls Sie bereits eine Back-End-App erstellt haben, stellen Sie sicher, dass Sie diese App an den {{site.data.keyword.mobilepushshort}}-Service binden.

**Objective-C**

```
//For Objective-C
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
if ([[[UIDevice currentDevice] systemVersion] floatValue] >= 8.0){
    [[UIApplication sharedApplication] registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge) categories:categories]];
	    [[UIApplication sharedApplication] registerForRemoteNotifications];
	    }
	    else{
	    [[UIApplication sharedApplication] registerForRemoteNotificationTypes:
	    (UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)];
	    }
	    return YES;
	}
```
	{: codeblock}

**Swift**

```
//For Swift
	func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
	let settings = UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound], categories: nil) UIApplication.sharedApplication().registerUserNotificationSettings(settings) UIApplication.sharedApplication().registerForRemoteNotifications()
	}
```
	{: codeblock}

###Tokens an {{site.data.keyword.mobilepushshort}} übergeben
{: pass-token-push-notifications}

Nachdem das Token von APNs empfangen worden ist, leiten Sie es als Teil der Methode `registerDevice:withDeviceToken` an {{site.data.keyword.mobilepushshort}} weiter.

**Objective-C**

```
//Für Objective-C
		-( void) application:( UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:( NSData *)deviceToken{
     IMFClient *client = [IMFClient sharedInstance];
	[client initializeWithBackendRoute: @"your-backend-route-here" backendGUID: @"Your-backend-GUID-here"];
	// Push-Instanz abrufen
	IMFPushClient* push = [IMFPushClient sharedInstance];
	[push initializeWithAppGUID:@"appGUID"];
	[push registerWithDeviceToken:deviceToken completionHandler:^(IMFResponse *response,  NSError *error) {
    if (error){
     NSLog(@"%@",error.description);
  }  s
else {
    NSLog(@"%@",response.responseJson.description);
}
	}];
 }
```
	{: codeblock}

**Swift**

Nachdem das Token von APNs empfangen worden ist, leiten Sie es als Teil der Methode `didRegisterForRemoteNotificationsWithDeviceToken` an Push Notifications weiter.

```
func application (application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   let push =  BMSPushClient.sharedInstance
   push.initializeWithAppGUID("appGUID")
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

Sie können Push-Benachrichtigungen auf iOS-Geräten mit einer der folgenden Methoden empfangen.

**Objective-C**

Um Push-Benachrichtigungen in iOS-Geräten zu empfangen, fügen Sie die folgende Objective-C-Methode zum Anwendungs-Delegat Ihrer Anwendung hinzu.

```
// Für Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
	}
```
	{: codeblock}

**Swift**

Um Push-Benachrichtigungen in iOS-Geräten zu empfangen, fügen Sie die folgende Swift-Methode zum Anwendungs-Delegat Ihrer Anwendung hinzu.
```
// Für Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
//UserInfo dictionary will contain data sent from the server
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


## Nächste Schritte
{: #next_steps_tags}

Nachdem Sie einfache Benachrichtigungen erfolgreich eingerichtet haben, können Sie tagbasierte Benachrichtigungen und erweiterte Optionen konfigurieren.

Fügen Sie die folgenden Funktionen von Push Notifications Service zu Ihrer App hinzu.
Informationen zur Verwendung tagbasierter Benachrichtigungen finden Sie in [Tagbasierte Benachrichtigungen](c_tag_basednotifications.html).
Informationen zur Verwendung erweiterter Benachrichtigungsoptionen finden Sie in [Erweiterte Push-Benachrichtigungen aktivieren](t_advance_badge_sound_payload.html).
