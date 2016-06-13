---

copyright:
 years: 2015, 2016

---

# iOS-Anwendungen für den Empfang von Push-Benachrichtigungen aktivieren
{: #enable-push-ios-notifications}

Aktivieren Sie iOS-Anwendungen für den Empfang von Push-Benachrichtigungen und für das
Senden von Push-Benachrichtigungen an Ihre Geräte.


##CocoaPods installieren
{: #enable-push-ios-notifications-install}

Für ein vorhandenes Xcode-Projekt können Sie das Bluemix Mobile Services-Client-SDK mithilfe des Abhängigkeitsmanagementtools CocoaPods einrichten. Als Alternative dazu können Sie das Software-Development-Kit (SDK) manuell installieren.

**Hinweis**: Die Push-Readme-Datei für Swift finden Sie unter https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master.



1. Installieren Sie CocoaPods, indem Sie in Ihrem Mac-Terminal folgenden Befehl verwenden.
```
$ sudo gem install cocoapods
```
2. Geben Sie den folgenden Befehl in das Terminal ein, um CocoaPods zu initialisieren. Stellen Sie beim Absetzen des Befehls sicher, dass Sie ihn in dem Verzeichnis ausführen, in dem sich Ihr Xcode-Projekt befindet. Mit dem Befehl `pod init` wird eine Dateibezeichnung erstellt.  
```
$ pod init
```
3. Fügen Sie in der generierten Datei 'Podfile' die von Ihnen benötigten SDK-Abhängigkeiten hinzu. Kopieren Sie die folgende Datei 'Podfile'.

   Objective-C

    ```
    source 'https://github.com/CocoaPods/Specs.git'
	Copy the following list as is and remove the dependencies you do not need
	pod 'IMFCore'
	pod 'IMFPush'
	```

   Swift

	```
	source 'https://github.com/CocoaPods/Specs.git'
	// Copy the following list as is and remove the dependencies you do not need.
	use_frameworks!

	target 'MyApp' do
	    platform :ios, '8.0'
	    pod 'BMSCore'
	    pod 'BMSPush'
	end
	```
3. Wechseln Sie am Terminal in Ihren Projektordner und installieren Sie die
Abhängigkeiten mithilfe des folgenden Befehls:
```
$ pod update
```
Mit diesem Befehl werden Ihre Abhängigkeiten installiert und es wird ein neuer Xcode-Arbeitsbereich erstellt.  **Hinweis**: Stellen Sie sicher, dass Sie immer den neuen Xcode-Arbeitsbereich öffnen und nicht die ursprüngliche Xcode-Projektdatei:

	```
	$ open App.xcworkspace
	```
Der Arbeitsbereich enthält Ihr ursprüngliches Projekt und das Projekt 'Pods', das Ihre Abhängigkeiten enthält. Wenn Sie einen Bluemix Mobile Services-Quellenordner ändern möchten, finden Sie diesen in Ihrem Projekt 'Pods' unter `Pods/yourImportedSourceFolder`, zum Beispiel: `Pods/IMFGoogleAuthentication`.

##Importierte Frameworks und Quellenordner verwenden

Referenzieren Sie das SDK in Ihrem Code.


### Objective-C

Schreiben Sie #import-Anweisungen für die entsprechenden Header, zum Beispiel:

```
//Objective-C
#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**Hinweis**: Durch Aktualisieren Ihres Projekts 'Pods' mithilfe der CocoaPods-Befehle `pod install` oder `pod update` werden die Bluemix Mobile Services-Quellenorder möglicherweise überschrieben. Wenn Sie Ihre angepassten Versionen der ursprünglichen Dateien aufbewahren möchten, müssen Sie sicherstellen, dass für sie ein Backup durchgeführt wird, bevor Sie einen dieser Befehle absetzen.

###Swift

**Voraussetzungen**

- iOS 8.0 oder höher
- Xcode 7


Schreiben Sie #import-Anweisungen für die entsprechenden Header, zum Beispiel:

```
//swift
import BMSCore
import BMSPush
```


##Buildeinstellungen

Rufen Sie **Xcode > Build Settings > Build Options** auf und setzen Sie **Enable Bitcode** auf **No**.

**Achtung**: Ab iOS 9 können sich Änderungen an der Komponente 'App Transport Security' (ATS) auf die Verarbeitung des Authentifizierungsprozesses auswirken. Die folgenden Blogeinträge liefern weitere Informationen zu den Änderungen: [ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) und [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/).




## Push-SDK für iOS-Apps initialisieren
{: #enable-push-ios-notifications-initialize}

Das Anwendungs-Delegat für die iOS-Anwendung ist eine übliche Position für den Initialisierungscode. Klicken Sie auf den Link **Mobile Optionen** in Ihrem Bluemix-Anwendungsdashboard, um die Anwendungsroute und die GUID abzurufen.

###Core-SDK initialisieren

####Objective-C

```
// Initialize the SDK for Object-C with IBM Bluemix GUID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```

####Swift

```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance

myBMSClient.initializeWithBluemixAppRoute("BluemixAppRoute", bluemixAppGUID: "APPGUID", bluemixRegion:"Location where your app Hosted")
myBMSClient.defaultRequestTimeout = 10.0 // Timput in seconds
```


###Client-Push-SDK initialisieren

####Objective-C

```
//Initialize client Push SDK for Objective-C
IMFPushClient _pushService = [IMFPushClient sharedInstance];
```

####Swift

```
//Initialize client Push SDK for Swift
let push = BMSPushClient.sharedInstance
```

### Route, GUID und Bluemix-Region

**appRoute**

Gibt die Route an, die der Serveranwendung zugewiesen ist, die Sie in Bluemix erstellt haben.

**GUID**

Gibt den eindeutigen Schlüssel an, der der Anwendung zugewiesen wird, die Sie in Bluemix erstellt haben. Bei diesem Wert muss die Groß-/Kleinschreibung beachtet werden.

**bluemixRegionSuffix**

Gibt den Standort an, an dem die App gehostet ist. Der Parameter `bluemixRegion` gibt an, welche Bluemix-Bereitstellung Sie verwenden. Sie können diesen Wert mit der statischen Eigenschaft `BMSClient.REGION` angeben und einen von drei Werten verwenden:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY




## iOS-Anwendungen und -Geräte registrieren
{: #enable-push-ios-notifications-register}


Eine Anwendung (App) muss bei APNs registriert werden, um ferne Benachrichtigungen zu empfangen. Dieser Schritt erfolgt meistens nach der Installation der App auf einem Gerät. Nachdem das von APNs generierte Gerätetoken von der App empfangen wurde, muss es zurück an Push Notifications Service geleitet werden.

Führen Sie zum Registrieren von iOs-Anwendungen und -Geräten die folgenden Schritte aus:

1. Back-End-Anwendung erstellen
2. Token an Push Notifications übergeben


###Back-End-Anwendung erstellen

Erstellen Sie eine Back-End-Anwendung im Abschnitt 'Boilerplates' des Bluemix®-Katalogs, mit der der Push-Service automatisch an diese Anwendung gebunden wird. Wenn Sie bereits eine Back-End-App erstellt haben, stellen Sie sicher, dass Sie die App an Push Notifications Service binden.

####Objective-C

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

```
	//For Swift
	func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
		let notificationTypes: UIUserNotificationType = UIUserNotificationType.Badge | UIUserNotificationType.Alert | UIUserNotificationType.Sound
		let notificationSettings: UIUserNotificationSettings = UIUserNotificationSettings(forTypes: notificationTypes, categories: categories)
		application.registerUserNotificationSettings(notificationSettings)
		application.registerForRemoteNotifications()
	}
```

###Token an Push Notifications übergeben

Sobald das Token von APNs empfangen wird, leiten Sie es als Teil der Methode `registerDevice:withDeviceToken` an Push Notifiacations weiter.

####Objective-C

```
//For Objective-C
-( void) application:( UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:( NSData *)deviceToken{

   IMFClient *client = [IMFClient sharedInstance];

 [client initializeWithBackendRoute:@"your-backend-route-here" backendGUID:@"Your-backend-GUID-here"];


 // get Push instance
IMFPushClient* push = [IMFPushClient sharedInstance];
[push registerDeviceToken:deviceToken completionHandler:^(IMFResponse *response,  NSError *error) {
   if (error){
     [ self  updateMessage:error .description];
  }  else {
    [ self updateMessage:response .responseJson .description];
}
}];
```

####Swift

Sobald das Token von APNs empfangen wird, leiten Sie es als Teil der Methode `registerDevice:withDeviceToken` an Push Notifiacations weiter.

```
func application (application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   let push =  BMSPushClient.sharedInstance
   push.registerDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
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

###Objective-C
Um Push-Benachrichtigungen in iOS-Geräten zu empfangen, fügen Sie die folgende Objective-C-Methode zum Anwendungs-Delegat Ihrer Anwendung hinzu.

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
}
```

###Swift
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


Senden Sie einfache Push-Benachrichtigungen.

1. Wählen Sie unter **Zielgruppe auswählen** eine der folgenden Zielgruppen aus:
**Alle Geräte** oder die Plattform **Nur iOS-Geräte** oder
**Nur Android-Geräte**. 

	**Hinweis**: Wenn Sie die Option **Alle Geräte** auswählen, erhalten alle Geräte, die
Push-Benachrichtigungen subskribiert haben, Ihre Benachrichtigung.

	![Anzeige 'Benachrichtigungen'](images/tag_notification.jpg)

2. Geben Sie in **Eigene Benachrichtigung erstellen** die gewünschte Nachricht ein und klicken Sie auf **Senden**.
3. Überprüfen Sie, ob die Geräte Ihre Benachrichtigung empfangen haben.

	Der folgende Screenshot zeigt ein Alertfeld bei der Verarbeitung einer Push-Benachrichtigung im Vordergrund eines Android- und iOS-Geräts.

	![Push-Benachrichtigung im Vordergrund auf einem Android-Gerät](images/Android_Screenshot.jpg)

	![Push-Benachrichtigung im Vordergrund auf einem iOS-Gerät](images/iOS_Screenshot.jpg)

	Der folgende Screenshot zeigt eine Push-Benachrichtigung im Hintergrund auf einem Android-Gerät.
	![Push-Benachrichtigung im Hintergrund auf einem Android-Gerät](images/background.jpg)




## Nächste Schritte
{: #next_steps_tags}

Nachdem Sie einfache Benachrichtigungen erfolgreich eingerichtet haben, können Sie tagbasierte Benachrichtigungen und erweiterte Optionen konfigurieren.

Fügen Sie die folgenden Funktionen von Push Notifications Service zu Ihrer App hinzu.
Informationen zur Verwendung tagbasierter Benachrichtigungen finden Sie in [Tagbasierte Benachrichtigungen](c_tag_basednotifications.html).
Informationen zur Verwendung erweiterter Benachrichtigungen finden Sie in [Erweiterte Push-Benachrichtigungen](t_advance_notifications.html).
