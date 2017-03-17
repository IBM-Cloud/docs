---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#Abilitazione delle applicazioni iOS a inviare {{site.data.keyword.mobilepushshort}}
{: #enable-push-ios-notifications}
Ultimo aggiornamento: 14 febbraio 2017
{: .last-updated}

Puoi abilitare le applicazioni iOS a inviare {{site.data.keyword.mobilepushshort}} ai tuoi dispositivi.


##Installazione di CocoaPods
{: #enable-push-ios-notifications-install}

Per un progetto Xcode esistente, puoi impostare il Bluemix Mobile services client SDK utilizzando lo strumento di gestione delle dipendenze CocoaPods. Un'alternativa consiste nell'installare l'SDK in modo manuale.

Per visualizzare il file readme Swift Push, vai a [Readme ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}.



1. Installa CocoaPods utilizzando il seguente comando nel tuo terminale Mac.
```$ sudo gem install cocoapods
```
	{: codeblock}
2. Immetti il comando `pod init` nel terminale per inizializzare CocoaPods. Assicurati di eseguire il comando dalla directory in cui si trova il progetto Xcode. Il comando `pod init` crea un Podfile.  
3. Nel Podfile generato, aggiungi le dipendenze SDK richieste. Copia il seguente Podfile.
   
	```
		source 'https://github.com/CocoaPods/Specs.git'
	// Copia il seguente elenco come è e rimuovi le dipendenze di cui non hai bisogno.
		use_frameworks!
		target 'MyApp' do
	    platform :ios, '8.0'
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

##Aggiunta di framework utilizzando Carthage
{: #carthage}

Aggiungi i framework al tuo progetto utilizzando [Carthage ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}. Nota che Carthage in Xcode8 non è supportato.

1. Aggiungi i framework `BMSPush` al tuo Cartfile:
```
  github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
	{: codeblock}
2. Esegui il comando `carthage update`. Quando la build è stata completata, trascina `BMSPush.framework`, `BMSCore.framework` e `BMSAnalyticsAPI.framework` nel tuo progetto Xcode.
3. Segui le istruzioni sul sito di [Carthage ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window} per completare l'integrazione.

##Configurazione dell'SDK iOS
{: ios-sdk}

Per configurare l'SDK iOS, aggiungi il seguente codice nel file **AppDelegate.swift** della tua applicazione. Nota che questo registra anche gli APNs.  
```
  func application(_ application: UIApplication,
didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {  
   BMSPushClient.sharedInstance.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE")
  }
```
    {: codeblock}

##Utilizzo dei framework importati e delle cartelle di origine
{: using-imported-frameworks}

Fai riferimento all'SDK nel tuo codice. Assicurati che siano implementati i seguenti prerequisiti.

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

Per leggere il file readme Swift Push, vedi [Readme ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}.

**Nota**: aggiornare il tuo progetto Pods utilizzando i comandi CocoaPods `pod install` o `pod update` potrebbe sovrascrivere le cartelle di origine Bluemix Mobile services. Se vuoi conservare le tue versioni personalizzate dei file originali, assicurati che ne sia stato eseguito il backup prime di immettere uno di questi comandi.


##Impostazioni di creazione
{: build-settings}

Vai a **Xcode > Build Settings > Build Options e imposta Enable Bitcode** su **No**.

**Attenzione**: a partire da iOS 9, le modifiche alla funzione ATS (App Transport Security) potrebbero influenzare il modo in cui gestisci il processo di autenticazione. I seguenti post del blog descrivono in maggiore dettaglio le modifiche: [ATS and Bitcode in iOS 9 ![Icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/){: new_window} e [Connect your iOS 9 app to Bluemix today ![Icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/){: new_window}.

## Inizializzazione di Push SDK per applicazioni iOS
{: #enable-push-ios-notifications-initialize}

Un posto comune dove inserire il codice di inizializzazione è nel delegato dell'applicazione per l'applicazione iOS. Fai clic sul link **Opzioni mobili** nel tuo dashboard Push per ottenere il GUID e la rotta dell'applicazione.

###Inizializzazione dell'SDK Core
{: Initializing-the-core-sdk}


```
// Inizializza l'SDK Core for Swift con l'area, la rotta e la GUID IBM Bluemix
let myBMSClient = BMSClient.sharedInstance
myBMSClient.initialize(bluemixRegion: "Location where your app is hosted.") 
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

- BMSClient.Region.usSouth 
- BMSClient.Region.unitedKingdom
- BMSClient.Region.sydney

####AppGUID
{: ios-AppGUID}

Specifica la chiave AppGUID univoca assegnata al servizio {{site.data.keyword.mobilepushshort}} creata in Bluemix.

###Inizializzazione del Push SDK client
{: initializing-the-client-Push-SDK}

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


###Creazione di un'applicazione di backend
{: create-a-backend-app}

Crea un'applicazione di backend nella sezione Contenitori tipo del catalogo Bluemix®, che esegue automaticamente il bind del servizio {{site.data.keyword.mobilepushshort}} a questa applicazione. Se già hai creato un'applicazione di backend, assicurati di eseguirne il bind al servizio {{site.data.keyword.mobilepushshort}}.


###Trasmissione dei token a {{site.data.keyword.mobilepushshort}}
{: pass-token-push-notifications}

Dopo che il token viene ricevuto da APNs, passa il token a {{site.data.keyword.mobilepushshort}} come parte del metodo `registerWithDeviceToken`.

Dopo che il token viene ricevuto da APNs, passa il token a Push Notifications come parte del metodo `didRegisterForRemoteNotificationsWithDeviceToken`.

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


## Ricezione di notifiche di push su dispositivi iOS
{: #enable-push-ios-notifications-receiving}


Per ricevere notifiche di push sui dispositivi ioS, aggiungi il seguente metodo Swift al delegato applicazione della tua applicazione.

```
  // For Swift
func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) 
  { //UserInfo dictionary will contain data sent from the server }
```
	{: codeblock}

## Monitoraggio di notifiche di push su dispositivi iOS
{: ios-monitoring}

Per monitorare lo stato corrente della notifica, aggiungi il seguente metodo Swift al delegato applicazione della tua applicazione.

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

##Abilitazione di notifiche interattive

Puoi ora arricchire le tue notifiche iOS con maggiori dettagli, come l'aggiunta di un'immagine, una mappa o un pulsante di risposta, attraverso l'abilitazione di notifiche interattive. Ciò fornisce un maggiore contesto per i clienti, insieme alla capacità di agire immediatamente senza uscire dal contesto corrente.  

Per abilitare le notifiche interattive, utilizza il seguente codice:

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

Per inviare una notifica interattiva, completa la procedura:

1. Nella sezione Compose, dall'elenco a discesa Send To, seleziona **iOS Devices**.
2. Immetti il messaggio di notifica che vuoi inviare.
3. Nella sezione Optional Settings, seleziona **Mobile** e fai clic su **iOS**.
4. Nell'elenco a discesa Type, seleziona **Mixed**.
5. Nel campo Category, specifica il tipo di notifica che hai definito nella tua applicazione. 

![Notifica interattiva per iOS](images/push_ios_notification_interactive.jpg) 

## Fasi successive
{: #next_steps_tags}

Dopo che hai correttamente configurato le notifiche di base, puoi configurare le notifiche
        basate sulle tag e le opzioni avanzate.

Aggiungi queste funzioni del servizio Push Notifications alla tua applicazione.
Per utilizzare le notifiche basate sulle tag, vedi [Notifiche basate sulle tag](c_tag_basednotifications.html).
Per utilizzare le opzioni di notifica avanzate, vedi [Abilitazione delle notifiche di push avanzate](t_advance_badge_sound_payload.html).
