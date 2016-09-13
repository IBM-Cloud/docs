---

copyright:
 years: 2015, 2016

---

# iOS-Anwendungen für den Empfang von Push-Benachrichtigungen aktivieren
{: #enable-push-ios-notifications}
Letzte Aktualisierung: 16. August 2016
{: .last-updated}

Sie können iOS-Anwendungen zum Empfangen von Push-Benachrichtigungen von Ihren Geräten und zum Senden von Push-Benachrichtigungen an Ihre Geräte aktivieren. 


##CocoaPods installieren
{: #enable-push-ios-notifications-install}

Für ein vorhandenes Xcode-Projekt können Sie das Bluemix Mobile Services-Client-SDK mithilfe des Abhängigkeitsmanagementtools CocoaPods einrichten. Als Alternative dazu können Sie das Software-Development-Kit (SDK) manuell installieren.

**Hinweis**: Die Push-Readme-Datei für Swift finden Sie unter der Webadresse 'https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master'. 



1. Installieren Sie CocoaPods, indem Sie in Ihrem Mac-Terminal folgenden Befehl verwenden.
```
$ sudo gem install cocoapods
```
2. Geben Sie den folgenden Befehl in das Terminal ein, um CocoaPods zu initialisieren. Führen Sie den Befehl unbedingt aus dem Verzeichnis aus, in dem sich Ihr Xcode-Projekt befindet. Mit dem Befehl `pod init` wird eine Dateibezeichnung erstellt.  
```
$ pod init
```
3. Fügen Sie in der generierten Datei 'Podfile' die erforderlichen SDK-Abhängigkeiten hinzu. Kopieren Sie eine der folgenden 'Podfile'-Dateien nach Bedarf. 

###Objective-C
   {: objc-sdkdependencies}

    ```
    source 'https://github.com/CocoaPods/Specs.git'
	# Copy the following list as is and remove the dependencies you do not need
	pod 'IMFCore'
	pod 'IMFPush'
	```

####Swift
   {: swift-sdkdependencies}

	```
	source 'https://github.com/CocoaPods/Specs.git'
	# Copy the following list as is and remove the dependencies you do not need.
	use_frameworks!

	target 'MyApp' do
	    platform :ios, '8.0'
	    pod 'BMSCore'
	    pod 'BMSPush'
      pod 'BMSAnalyticsAPI'
	end
	```
3. Wechseln Sie am Terminal in Ihren Projektordner und installieren Sie die Abhängigkeiten mithilfe des folgenden Befehls:

```
$ pod update
```
Mit diesem Befehl werden Ihre Abhängigkeiten installiert und es wird ein neuer Xcode-Arbeitsbereich erstellt.  **Hinweis**: Stellen Sie sicher, dass Sie immer den neuen Xcode-Arbeitsbereich öffnen und nicht die ursprüngliche Xcode-Projektdatei:

	```
	$ open App.xcworkspace
	```
Der Arbeitsbereich enthält Ihr ursprüngliches Projekt und das Projekt 'Pods', das Ihre Abhängigkeiten enthält. Wenn Sie einen Bluemix Mobile Services-Quellenordner ändern möchten, finden Sie diesen in Ihrem Projekt 'Pods' unter `Pods/yourImportedSourceFolder`, zum Beispiel: `Pods/BMSPush`.

##Carthage
{: #carthage}

Fügen Sie mithilfe von [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) Frameworks zu Ihrem Projekt hinzu. (https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos%29.)

1. Fügen Sie `BMSPush`-Frameworks zur Cartfile hinzu:
```
github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
2. Führen Sie den Befehl `carthage update` aus. Wenn der Build abgeschlossen ist, ziehen Sie `BMSPush.framework`, `BMSCore.framework` und `BMSAnalyticsAPI.framework` in das Xcode-Projekt.
3. Gehen Sie den Anweisungen auf der [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos)-Site entsprechend vor, um die Integration abzuschließen.

##Importierte Frameworks und Quellenordner verwenden
{: using-imported-frameworks}

Referenzieren Sie das SDK in Ihrem Code.


####Objective-C
{: objc-import-directives}

Schreiben Sie #import-Anweisungen für die entsprechenden Header, zum Beispiel:

```
 //Objective-C
#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**Hinweis**: Durch Aktualisieren Ihres Projekts 'Pods' mithilfe der CocoaPods-Befehle `pod install` oder `pod update` werden die Bluemix Mobile Services-Quellenorder möglicherweise überschrieben. Wenn Sie Ihre angepassten Versionen der ursprünglichen Dateien aufbewahren möchten, müssen Sie sicherstellen, dass für sie ein Backup durchgeführt wird, bevor Sie einen dieser Befehle absetzen.

####Swift
{: swift-import-directives}

####Voraussetzungen
{: prerequisites}

- iOS 8.0 oder höher
- Xcode 7


Schreiben Sie #import-Anweisungen für die entsprechenden Header, zum Beispiel:

```
//swift
import BMSCore
import BMSPush
```
**Achtung**: Die Push-Readme-Datei für Swift finden Sie in [Readme](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master).

##Buildeinstellungen
{: build-settings}

Rufen Sie **Xcode > Build Settings > Build Options** auf und setzen Sie **Enable Bitcode** auf **No**.

**Achtung**: Ab iOS 9 können sich Änderungen an der Komponente 'App Transport Security' (ATS) auf die Verarbeitung des Authentifizierungsprozesses auswirken. Die folgenden Blogeinträge liefern weitere Informationen zu den Änderungen: [ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) und [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/).




## Push-SDK für iOS-Apps initialisieren
{: #enable-push-ios-notifications-initialize}

Das Anwendungs-Delegat für die iOS-Anwendung ist eine übliche Position für den Initialisierungscode. Klicken Sie in Ihrem Push-Dashboard auf den Link **Mobile Systemerweiterungen**, um die Anwendungsroute und die GUID abzurufen. 

###Core-SDK initialisieren
{: Initializing-the-core-sdk}

####Objective-C
{: objc-initialize-core-sdk}

```
// Initialize the SDK for Object-C with IBM Bluemix GUID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```

####Swift
{: swift-initialize-core-sdk}

```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance
myBMSClient.initializeWithBluemixAppRoute("BluemixAppRoute", bluemixAppGUID: "APPGUID", bluemixRegion:"Location where your app Hosted")
myBMSClient.defaultRequestTimeout = 10.0 // Timeout in seconds
```

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

Gibt den eindeutigen 'AppGUID'-Schlüssel an, der dem von Ihnen in Bluemix erstellten Service für Push-Benachrichtigungen zugewiesen wird. 

###Client-Push-SDK initialisieren
{: initializing-the-client-Push-SDK}

####Objective-C
{: objc-initialize-push-sdk}

```
//Initialize client Push SDK for Objective-C
IMFPushClient *push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID"];

```

####Swift
{: swift-initialize-push-sdk}

```
//Initialize client Push SDK for Swift
let push = BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID")

```



## iOS-Anwendungen und -Geräte registrieren
{: #enable-push-ios-notifications-register}


Nach der Installation einer Anwendung (App) auf einem Gerät muss die Anwendung (App) muss bei APNs registriert werden, um ferne Benachrichtigungen zu empfangen. Nachdem das von APNs generierte Gerätetoken von der App empfangen worden ist, muss es zurück an den {{site.data.keyword.mobilepushshort}}-Service geleitet werden. 

Führen Sie zum Registrieren von iOS-Anwendungen und -Geräten die folgenden Schritte aus:

1. Back-End-Anwendung erstellen
2. Token an {{site.data.keyword.mobilepushshort}} übergeben


###Back-End-Anwendung erstellen
{: create-a-backend-app}

Erstellen Sie im Bluemix®-Katalog im Abschnitt 'Boilerplates' eine Back-End-Anwendung, mit der der {{site.data.keyword.mobilepushshort}}-Service automatisch an diese Anwendung gebunden wird. Falls Sie bereits eine Back-End-App erstellt haben, stellen Sie sicher, dass Sie diese App an den {{site.data.keyword.mobilepushshort}}-Service binden. 

####Objective-C
{: objc-backendapp-code}

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

####Swift
{: swift-backendapp-code}

```
	//For Swift
	func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
		let settings = UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound], categories: nil) UIApplication.sharedApplication().registerUserNotificationSettings(settings) UIApplication.sharedApplication().registerForRemoteNotifications()
	}
```

###Tokens an {{site.data.keyword.mobilepushshort}} übergeben
{: pass-token-push-notifications}

Nachdem das Token von APNs empfangen worden ist, leiten Sie es als Teil der Methode `registerDevice:withDeviceToken` an {{site.data.keyword.mobilepushshort}} weiter. 

####Objective-C
{: objc-token}

```
//For Objective-C
-( void) application:( UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:( NSData *)deviceToken{

   IMFClient *client = [IMFClient sharedInstance];

 [client initializeWithBackendRoute:@"your-backend-route-here" backendGUID:@"Your-backend-GUID-here"];


 // get Push instance
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
```

####Swift
{: swift-token}

Nachdem das Token von APNS empfangen worden ist, leiten Sie es als Teil der Methode `didRegisterForRemoteNotificationsWithDeviceToken` an Push

Notifications weiter. 

```

func application (application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   let push =  BMSPushClient.sharedInstance
  push.initializeWithAppGUID("appGUID")
  push.registerWithDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
  push.initializeWithPushAppGUID("pushAppGUID")
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



## Push-Benachrichtigungen in iOS-Geräten empfangen
{: #enable-push-ios-notifications-receiving}

Empfangen Sie Push-Benachrichtigungen in iOS-Geräten.

####Objective-C
{: objc-receive-push-notifications}

Um Push-Benachrichtigungen in iOS-Geräten zu empfangen, fügen Sie die folgende Objective-C-Methode zum Anwendungs-Delegat Ihrer Anwendung hinzu.

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
}
```

####Swift
{: swift-receive-push-notifications}
Um Push-Benachrichtigungen in iOS-Geräten zu empfangen, fügen Sie die folgende Swift-Methode zum Anwendungs-Delegat Ihrer Anwendung hinzu.

```
 // For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //UserInfo dictionary will contain data sent from the server
   }

```



## Einfache Push-Benachrichtigungen senden
{: #send}

Nach dem Entwickeln Ihrer Anwendungen können Sie einfache Push-Benachrichtigungen (ohne Tags, Badges, zusätzliche Nutzdaten oder Audiodateien) senden.


1. Wählen Sie unter **Zielgruppe auswählen** eine der folgenden Zielgruppen aus:
**Alle Geräte** oder die Plattform **Nur iOS-Geräte** oder
**Nur Android-Geräte**. 

	**Hinweis**: Wenn Sie die Option **Alle Geräte** auswählen, erhalten alle Geräte, die
Push-Benachrichtigungen subskribiert haben, Ihre Benachrichtigung.

![Anzeige 'Benachrichtigungen'](images/tag_notification.jpg)

2. Geben Sie in **Eigene Benachrichtigung erstellen** die gewünschte Nachricht ein und klicken Sie auf **Senden**.
3. Überprüfen Sie, ob die Geräte die Benachrichtigung empfangen haben. Die folgende Abbildung zeigt ein Alertfeld bei der Verarbeitung einer Push-Benachrichtigung im Vordergrund und Hintergrund eines iOS-Geräts. 

	![Push-Benachrichtigung im Vordergrund auf einem Android-Gerät](images/iOS_Foreground.jpg)

![Push-Benachrichtigung im Vordergrund auf einem iOS-Gerät](images/iOS_Screenshot.jpg)




## Nächste Schritte
{: #next_steps_tags}

Nachdem Sie einfache Benachrichtigungen erfolgreich eingerichtet haben, können Sie tagbasierte Benachrichtigungen und erweiterte Optionen konfigurieren.

Fügen Sie die folgenden Funktionen von Push Notifications Service zu Ihrer App hinzu.
Informationen zur Verwendung tagbasierter Benachrichtigungen finden Sie in [Tagbasierte Benachrichtigungen](c_tag_basednotifications.html).
Informationen zur Verwendung erweiterter Benachrichtigungen finden Sie in [Erweiterte Push-Benachrichtigungen](t_advance_notifications.html).
