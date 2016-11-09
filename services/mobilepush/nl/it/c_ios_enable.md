---

copyright:
 years: 2015, 2016

---

#Abilitazione delle applicazioni iOS a ricevere e inviare {{site.data.keyword.mobilepushshort}}
{: #enable-push-ios-notifications}
Ultimo aggiornamento: 19 ottobre 2016
{: .last-updated}

Puoi abilitare le applicazioni iOS a ricevere e inviare {{site.data.keyword.mobilepushshort}} ai tuoi dispositivi.


##Installazione di CocoaPods
{: #enable-push-ios-notifications-install}

Per un progetto Xcode esistente, puoi impostare il Bluemix Mobile services client SDK utilizzando lo strumento di gestione delle dipendenze CocoaPods. Un alternativa consiste nell'installare l'SDK in modo manuale.

Per visualizzare il file readme Swift Push, vai a [Readme](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master).



1. Installa CocoaPods utilizzando il seguente comando nel tuo terminale Mac.
```
$ sudo gem install cocoapods
```
	{: codeblock}
2. Immetti il comando `pod init` nel terminale per inizializzare CocoaPods. Assicurati di eseguire il comando dalla directory in cui si trova il progetto Xcode. Il comando `pod init` crea un Podfile.  
3. Nel Podfile generato, aggiungi le dipendenze SDK richieste. Copia i seguenti Podfile, in base alla tua preferenza.
 
**Objective-C**
   
```
source 'https://github.com/CocoaPods/Specs.git'
	# Copia il seguente elenco come è e rimuovi le dipendenze di cui non hai bisogno.
	pod 'IMFCore'
	pod 'IMFPush'
```
	{: codeblock}

**   Swift

	**
   
```
source 'https://github.com/CocoaPods/Specs.git'
	# Copia il seguente elenco come è e rimuovi le dipendenze di cui non hai bisogno.
use_frameworks!
target 'MyApp' do
	    platform :ios, '9.0'
pod 'BMSCore'
	    pod 'BMSPush'
      pod 'BMSAnalyticsAPI'
	end
```
	{: codeblock}

3. Dal terminale, vai alla cartella del progetto e installa le dipendenze con il comando `pod update`.

Il comando installa le tue dipendenze e crea un nuovo spazio di lavoro Xcode.   
**Nota**: assicurati di aprire sempre il nuovo spazio di lavoro Xcode invece del file di progetto Xcode originale:
```
$ open App.xcworkspace
```
	{: codeblock}

Lo spazio di lavoro contiene il tuo progetto originale e il progetto Pods che contiene le tue dipendenze. Per modificare una cartella di origine Bluemix mobile services, puoi trovarla nel tuo progetto Pods, in `Pods/yourImportedSourceFolder`, ad esempio: `Pods/BMSPush`.

##Carthage
{: #carthage}

Aggiungi framework al tuo progetto utilizzando [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos). Nota che Carthage in Xcode8 non è supportato.

1. Aggiunti i framework `BMSPush` al tuo Cartfile:
```
github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
	{: codeblock}
2. Esegui il comando `carthage update`. Quando la build è stata completata, trascina `BMSPush.framework`, `BMSCore.framework` e `BMSAnalyticsAPI.framework` nel tuo progetto Xcode.
3. Segui le istruzioni sul sito [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) per completare l'integrazione.


##Utilizzo dei framework importati e delle cartelle di origine
{: using-imported-frameworks}

Fai riferimento all'SDK nel tuo codice. Utilizza uno dei seguenti metodi, in base alla tua preferenza. 

**Objective-C**

Scrivi le direttive `#import` per le intestazioni
pertinenti, ad esempio:

```
	//Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFPush/IMFPush.h>
```
	{: codeblock}

**Nota**: aggiornare il tuo progetto Pods utilizzando i comandi CocoaPods `pod install` o `pod update` potrebbe sovrascrivere le cartelle di origine Bluemix Mobile services. Se vuoi conservare le tue versioni personalizzate dei file originali, assicurati che ne sia stato eseguito il backup prime di immettere uno di questi comandi.

**   Swift

	**

Assicurati che siano implementati i seguenti prerequisiti: 

- iOS 8.0 o successiva
- Xcode 7


Scrivi le direttive `#import` per le intestazioni
pertinenti, ad esempio:
```
//swift
import BMSCore
import BMSPush
```
	{: codeblock}
Per visualizzare il file readme Swift Push, vai a [Readme](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master).

##Impostazioni di creazione
{: build-settings}

Vai a **Xcode > Build Settings > Build Options e imposta Enable Bitcode** su **No**.

**Attenzione**: a partire da iOS 9, le modifiche alla funzione ATS (App Transport Security) potrebbero influenzare il modo in cui gestisci il processo di autenticazione. I seguenti post del blog descrivono in maggiore dettaglio le modifiche:[ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) e [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/).

## Inizializzazione di Push SDK per applicazioni iOS
{: #enable-push-ios-notifications-initialize}

Un posto comune dove inserire il codice di inizializzazione è nel delegato dell'applicazione per l'applicazione iOS. Fai clic sul link **Opzioni mobili** nel tuo dashboard Push per ottenere il GUID e la rotta dell'applicazione.

###Inizializzazione dell'SDK Core
{: Initializing-the-core-sdk}

**Objective-C**

```
// Inizializza l'SDK for Object-C con la rotta e la GUID IBM Bluemix
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```
	{: codeblock}

**   Swift

	**

```
// Inizializza l'SDK Core for Swift con l'area, la rotta e la GUID IBM Bluemix
let myBMSClient = BMSClient.sharedInstance
myBMSClient.initialize(bluemixRegion: "Location where your app is hosted.")
myBMSClient.defaultRequestTimeout = 10.0 // Timeout in secondi
```
	{: codeblock}

### Rotta, GUID e area Bluemix
{: route-guid-bluemix-region}

####appRoute
{: ios-approute}

Specifica la rotta assegnato all'applicazione server creata in Bluemix.

####GUID
{: ios-guid}

Specifica la chiave univoca assegnata all'applicazione creata in Bluemix. Questo valore è
                sensibile al maiuscolo/minuscolo.

####bluemixRegionSuffix
{: ios-bluemixRegionSuffix}

Specifica l'ubicazione in cui è ospitata l'applicazione. Il parametro `bluemixRegion` specifica quale distribuzione di Bluemix stati utilizzando. Puoi impostare questo valore con una proprietà statica `BMSClient.REGION` e utilizzare uno dei seguenti tre valori:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

####AppGUID
{: ios-AppGUID}

Specifica la chiave AppGUID univoca assegnata al servizio {{site.data.keyword.mobilepushshort}} creata in Bluemix.

###Inizializzazione del Push SDK client
{: initializing-the-client-Push-SDK}

**Objective-C**

```
//Inizializza il Push SDK for Objective-C client
IMFPushClient *push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID" clientSecret:@"clientSecret"];
```
	{: codeblock}

**   Swift

	**

```
//Inizializza il Push SDK for Swift client
let push = BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


## Registrazione di dispositivi ed applicazioni iOS
{: #enable-push-ios-notifications-register}


Un'applicazione deve essere registrata con il servizio APNS per ricevere le notifiche remote, dopo l'installazione su un dispositivo. Una volta che il token del dispositivo generato da APNS viene ricevuto dall'applicazione, questo deve essere trasmesso nuovamente al servizio {{site.data.keyword.mobilepushshort}}.

Per registrare le applicazioni e dispositivi iOS, devi: 

1. Creare un'applicazione di backend. 
2. Inviare il token a {{site.data.keyword.mobilepushshort}}.


###Crea un'applicazione di backend
{: create-a-backend-app}

Crea un'applicazione di backend nella sezione Contenitori tipo del catalogo Bluemix®, che esegue automaticamente il bind del servizio {{site.data.keyword.mobilepushshort}} a questa applicazione. Se già hai creato un'applicazione di backend, assicurati di eseguirne il bind al servizio {{site.data.keyword.mobilepushshort}}.

**Objective-C**

```
//Per Objective-C
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

**   Swift

	**

```
//Per Swift
	func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
	let settings = UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound], categories: nil) UIApplication.sharedApplication().registerUserNotificationSettings(settings) UIApplication.sharedApplication().registerForRemoteNotifications()
	}
```
	{: codeblock}

###Trasmissione dei token a {{site.data.keyword.mobilepushshort}}
{: pass-token-push-notifications}

Dopo che il token viene ricevuto da APNs, passa il token a {{site.data.keyword.mobilepushshort}} come parte del metodo `registerWithDeviceToken`.

**Objective-C**

```
//Per Objective-C
		-( void) application:( UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:( NSData *)deviceToken{
     IMFClient *client = [IMFClient sharedInstance];
	[client initializeWithBackendRoute: @"your-backend-route-here" backendGUID: @"Your-backend-GUID-here"];
	// ottieni l'istanza Push
	IMFPushClient* push = [IMFPushClient sharedInstance];
	[push initializeWithAppGUID:@"appGUID"];
	[push registerWithDeviceToken:deviceToken completionHandler:^(IMFResponse *response,  NSError *error) {
    if (error){
     NSLog(@"%@",error.description);
  }  else {
    NSLog(@"%@",response.responseJson.description);
}
	}];
 }
```
	{: codeblock}

**   Swift

	**

Dopo che il token viene ricevuto da APNs, passa il token a Push Notifications come parte del metodo `didRegisterForRemoteNotificationsWithDeviceToken`.

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


## Ricezione di notifiche di push su dispositivi iOS
{: #enable-push-ios-notifications-receiving}

Puoi ricevere le notifiche di push sui dispositivi iOS utilizzando uno dei seguenti metodi.

**Objective-C**

Per ricevere notifiche di push sui dispositivi ioS, aggiungi il seguente metodo Objective-C al delegato applicazione della tua applicazione.

```
// Per Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//il dizionario userInfo conterrà i dati inviati dal server.
	}
```
	{: codeblock}

**   Swift

	**

Per ricevere notifiche di push sui dispositivi ioS, aggiungi il seguente metodo Swift al delegato applicazione della tua applicazione.
```
// Per Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
//Il dizionario UserInfo conterrà i dati inviati dal server
   }
```
	{: codeblock}

## Invio di notifiche di push di base
{: #send}

Dopo che hai sviluppato le tue applicazioni, puoi inviare delle notifiche di push di base.

Per inviare notifiche push di base, completa la seguente procedura:

1. Seleziona **Send Notifications** e componi un messaggio scegliendo l'opzione **Send to**. Le opzioni supportate sono **Device by Tag**, **Device Id**, **User Id**, **Android devices**, **iOS devices**, **Web Notifications** e **All Devices**.  
**Nota**: quando selezioni l'opzione **All Devices**, tutti i dispositivi sottoscritti a {{site.data.keyword.mobilepushshort}} riceveranno le notifiche.
![Schermata notifiche](images/tag_notification.jpg)

2. Nel campo **Message**, componi il messaggio. Scegli di configurare le impostazioni facoltative come richiesto.
3. Fai clic su **Send**.
3. Verifica che i tuoi dispositivi abbiano ricevuto la tua notifica.

La seguente immagine mostra una casella di avviso che gestisce {{site.data.keyword.mobilepushshort}} su un dispositivo iOS.

![Notifica push in primo piano su iOS](images/iOS_Screenshot.jpg) 

### Impostazioni facoltative per l'invio delle notifiche
{: #send_ios_otpional_setting}

Puoi anche personalizzare le impostazioni di {{site.data.keyword.mobilepushshort}} per inviare le notifiche ai dispositivi iOS. Sono supportate le seguenti opzioni di personalizzazione facoltative.

- **Badge**:  indica il numero che viene visualizzato nel badge dell'applicazione. Il valore predefinito è zero (0) e ciò significa che non sarà visualizzato un badge. 
- **Audio**: indica un file audio da riprodurre al ricevimento di un notifica. Supporta il valore predefinito o il nome della risorsa audio integrata nell'applicazione.
- **Payload addizionale**: specifica i valori di payload personalizzati per le tue notifiche.


## Fasi successive
{: #next_steps_tags}

Dopo che hai correttamente configurato le notifiche di base, puoi configurare le notifiche
        basate sulle tag e le opzioni avanzate.

Aggiungi queste funzioni del Servizio Push Notifications alla tua applicazione.
Per utilizzare le notifiche basate sulle tag, vedi [Notifiche basate sulle tag](c_tag_basednotifications.html).
Per utilizzare le opzioni di notifica avanzate, vedi [Abilitazione delle notifiche di push avanzate](t_advance_badge_sound_payload.html).
