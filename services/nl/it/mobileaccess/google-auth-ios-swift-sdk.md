---

copyright:
  years: 2016

---

# Abilitazione dell'autenticazione Google nelle applicazioni iOS (SDK Swift)
{: #google-auth-ios}

## Prima di cominciare
{: #google-auth-ios-before}

* Devi disporre di una risorsa protetta da {{site.data.keyword.amashort}} e di un progetto iOS strumentato con l'SDK client {{site.data.keyword.amashort}}.  Per ulteriori informazioni, vedi [Introduzione a {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) e [Configurazione dell'SDK Swift iOS](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html).  
* Proteggi manualmente la tua applicazione di backend con l'SDK server {{site.data.keyword.amashort}}. Per ulteriori informazioni, vedi [Protezione delle risorse](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

## Preparazione della tua applicazione per l'accesso Google
{: #google-sign-in-ios}

Prepara la tua applicazione per l'accesso Google attenendoti alle istruzioni fornite da Google nel documento '[Google Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start-integrating). La seguente procedura ti fornisce una breve sintesi delle attività che devi eseguire per preparare la tua applicazione.

1. Abilita l'accesso Google per iOS per la tua applicazione. Per ulteriori informazioni, vedi [Try Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start?ver=swift).

1. Ottieni un file di configurazione (`GoogleService-Info.plist`) per il tuo progetto. Per ottenere il file, vedi [Enable Google services for your app](https://developers.google.com/mobile/add?platform=ios).

 **Importante:** quando ottieni il file `GoogleService-Info.plist`, aprilo e annota il valore di `CLIENT_ID`. Questo valore ti servirà successivamente per configurare {{site.data.keyword.amashort}}.

1. Aggiungi il file `GoogleService-Info.plist` al tuo progetto Xcode. Per ulteriori informazioni,
vedi [Add the configuration file to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config)

1. Aggiorna gli schemi URL nel tuo progetto Xcode con il tuo `REVERSE_CLIENT_ID` e l'ID bundle. Per ulteriori informazioni,
vedi [Add URL schemes to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add_url_schemes_to_your_project).

1. Aggiorna il file project-Bridging-Header.h della tua applicazione con il seguente codice:

 ```
 #import <Google/SignIn.h>
 ```

 Per ulteriori informazioni sull'aggiornamento del file di intestazione di collegamento, vedi il passo 1 in [Enable sign-in](https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in).

## Configurazione di {{site.data.keyword.amashort}} per l'autenticazione Google
{: #google-auth-ios-config}

Ora che hai un ID client iOS, puoi abilitare l'autenticazione Google nel dashboard {{site.data.keyword.Bluemix}}.

1. Apri la tua applicazione nel dashboard {{site.data.keyword.Bluemix_notm}}.

1. Fai clic su **Opzioni mobili** e annota **Rotta** (*applicationRoute*) e **GUID applicazione** (*applicationGUID*). Questi valori ti servono quando inizializzi l'SDK.

1. Fai clic sul tile {{site.data.keyword.amashort}}. Il dashboard {{site.data.keyword.amashort}} viene caricato.

1. Fai clic sul tile **Google**.

1. In **Application ID for iOS**, specifica il valore `CLIENT_ID` dal file `GoogleService-Info.plist` che hai ottenuto precedentemente e fai clic su **Save**.

## Configurazione dell'SDK client {{site.data.keyword.amashort}} per iOS
{: #google-auth-ios-sdk}

### Installazione di CocoaPods
{: #google-auth-cocoapods}

L'SDK client {{site.data.keyword.amashort}} viene distribuito con CocoaPods, un gestore dipendenze per i progetti iOS. CocoaPods scarica automaticamente le risorse utente dai repository e le rende disponibili alla tua applicazione iOS.

1. Apri il terminale ed esegui il comando `pod --version`. Se già hai CocoaPods installato, viene visualizzato il numero versione. Puoi passare direttamente alla sezione successiva di questa esercitazione.

1. Installa CocoaPods eseguendo `sudo gem install cocoapods`. Fai riferimento al [sito web CocoaPods](https://cocoapods.org/) nel caso ti occorrano ulteriori indicazioni.

1. Chiudi XCode.

1. Apri il terminale e vai (con `cd`) alla directory del tuo progetto.

1.  Esegui `pod init`.

### Installazione dell'SDK Swift client {{site.data.keyword.amashort}} utilizzando CocoaPods
{: #google-auth-ios-sdk-cocoapods}

1. Passa al tuo progetto iOS.

1. Modifica `Podfile` per aggiungere le seguenti righe:

 ```
 use_frameworks!
 pod 'BMSGoogleAuthentication'
 ```
 **Suggerimento:** puoi aggiungere `use_frameworks!` alla tua destinazione Xcode invece di averlo nel Podfile.

1. Salva il `Podfile` ed esegui `pod install` dalla riga di comando. CocoaPods installa le dipendenze. Vedrai lo stato di avanzamento e quali componenti sono stati aggiunti.

 **Importante**: devi ora aprire il tuo progetto utilizzando il file `xcworkspace` che viene generato da CocoaPods. Di norma, il
nome è `{il-tuo-nome-progetto}.xcworkspace`.  

1. Esegui `open {il-tuo-nome-progetto}.xcworkspace` dalla riga di comando per aprire il tuo spazio di lavoro del progetto iOS.

1. Copia il file `GoogleAuthenticationManager.swift` dai file di origine pod `BMSGoogleAuthentication` alla directory del tuo progetto.

## Inizializzazione dell'SDK Swift client {{site.data.keyword.amashort}}
{: #google-auth-ios-initialize}

Per utilizzare l'SDK client {{site.data.keyword.amashort}}, inizializzalo passando i parametri `applicationGUID` e `applicationRoute`.

Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `application:didFinishLaunchingWithOptions` del tuo delegato dell'applicazione.

1. Ottieni i valori di parametro della tua applicazione. Apri la tua applicazione nel dashboard {{site.data.keyword.Bluemix_notm}}. Fai clic su **Opzioni mobili**. I valori `applicationRoute` e `applicationGUID` sono visualizzati nei campi **Rotta** e **GUID applicazione**.

1. Importa i framework richiesti nella classe dove vuoi utilizzare l'SDK client {{site.data.keyword.amashort}}. Aggiungi le seguenti intestazioni:

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```

1. Utilizza il seguente codice per inizializzare l'SDK client. Sostituisci `<applicationRoute>` e `<applicationGUID>` con
i valori per **Rotta** e **GUID applicazione** che hai ottenuto da **Opzioni mobili** nel dashboard {{site.data.keyword.Bluemix_notm}}.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 // Inizializza l'SDK client.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUId, bluemixRegion: BMSClient.<regione Bluemix applicazione>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 GoogleAuthenticationManager.sharedInstance.register()
      return true
      }

 // [START openurl]
      func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {
             return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, sourceApplication: sourceApplication, annotation: annotation)
      }

 @available(iOS 9.0, *)
 func application(app: UIApplication, openURL url: NSURL, options: [String : AnyObject]) -> Bool {
 return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, options: options)
  }
 ```

## Verifica dell'autenticazione
{: #google-auth-ios-testing}

Dopo che l'SDK client è stato inizializzato e il gestore autenticazione Google è stato registrato, puoi iniziare a effettuare richieste al tuo backend mobile.

### Prima di cominciare
{: #google-auth-ios-testing-before}

Devi utilizzare il contenitore tipo {{site.data.keyword.mobilefirstbp}} e disporre già di una risorsa protetta da {{site.data.keyword.amashort}} all'endpoint `/protected`. Se devi configurare un endpoint `/protected`, consulta [Protezione delle risorse](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Prova a inviare una richiesta all'endpoint protetto del tuo backend mobile nel tuo browser desktop aprendo `{applicationRoute}/protected`, ad esempio `http://my-mobile-backend.mybluemix.net/protected`

1. L'endpoint `/protected` di un backend mobile creato con il contenitore tipo MobileFirst Services è protetto con {{site.data.keyword.amashort}}; pertanto, possono accedere ad esso solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}. Di conseguenza, vedrai `Unauthorized` nel tuo browser del desktop.

1. Utilizza la tua applicazione iOS per effettuare una richiesta allo stesso endpoint.

 ```Swift
 let protectedResourceURL = "<URL della tua risorsa protetta>" // qualsiasi risorsa protetta
 let request = Request(url: protectedResourceURL , method: HttpMethod.GET)
 let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in
 if error == nil {
    print ("response:\(response?.responseText), no error")
 } else {
    print ("error: \(error)")
 }
 }

 request.sendWithCompletionHandler(callBack)
	```

1. Esegui la tua applicazione. Vedrai comparire una schermata di accesso Google

 ![immagine](images/ios-google-login.png)

1. Quando esegui l'accesso e fai clic su **OK**, stai autorizzando {{site.data.keyword.amashort}} a utilizzare la tua identità utente Google per scopi di autenticazione.

1. 	La tua richiesta dovrebbe avere esito positivo. Nel log dovresti vedere il seguente output.

 ```
 onAuthenticationSuccess info = Optional({attributes = {};
     deviceId = 105747725068605084657;
     displayName = "donlonqwerty@gmail.com";
     isUserAuthenticated = 1;
     userId = 105747725068605084657;
 })
 response:Optional("Salve, questa è una risorsa protetta!"), no error
 ```

1. Puoi anche aggiungere la funzionalità di disconnessione aggiungendo il seguente codice:

 ```
 GoogleAuthenticationManager.sharedInstance.logout(callBack)
 ```

  Se richiami questo codice dopo che un utente ha eseguito l'accesso con Google e l'utente prova ad eseguire nuovamente l'accesso, gli viene richiesto di autorizzare {{site.data.keyword.amashort}} a utilizzare Google per scopi di autenticazione. A tal punto, l'utente può fare clic sul nome utente nell'angolo superiore destro dello schermo per selezionare, ed eseguire l'accesso con, un altro utente.

   Passare `callBack` alla funzione di disconnessione è facoltativo. Puoi anche passare `nil`.
