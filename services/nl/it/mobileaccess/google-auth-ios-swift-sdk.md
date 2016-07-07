 ---

copyright:
  years: 2016

---
{:screen:  .screen}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}

# Abilitazione dell'autenticazione Google per le applicazioni iOS (SDK Swift)
{: #google-auth-ios}
Utilizza l'accesso Google per autenticare gli utenti nella tua applicazione Swift iOS {{site.data.keyword.amashort}}. La nuova SDK Swift rilasciata {{site.data.keyword.amashort}} aggiunge e migliora le funzionalità fornite dalla SDK Objective-C Mobile Client Access esistente.

**Nota:** mentre la SDK Objective-C SDK rimane completamente supportata ed è ancora considerata la SDK primaria per i servizi mobili {{site.data.keyword.Bluemix_notm}}, è pianificato di abbandonarla più avanti questo anno in favore di questa nuova SDK Swift.



## Prima di cominciare
{: #google-auth-ios-before}
È necessario disporre di:

* Un progetto iOS in Xcode. Non deve essere instrumentato con l'SDK client {{site.data.keyword.amashort}}.  
* Un'istanza di un'applicazione  {{site.data.keyword.Bluemix_notm}} che è protetta da un servizio {{site.data.keyword.amashort}}. Per ulteriori informazioni su come creare un back-end {{site.data.keyword.Bluemix_notm}}, consulta [Introduzione](index.html).


## Preparazione della tua applicazione per l'accesso Google
{: #google-sign-in-ios}

Prepara la tua applicazione per l'accesso Google attenendoti alle istruzioni fornite da Google in [Google Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start-integrating). 

Questo processo: 
* prepara un nuovo progetto sul sito Google Developers, 
*  crea il file `GoogleService-Info.plist` e il valore `REVERSE_CLIENT_ID` da aggiungere al tuo progetto Xcode e
* crea l'**ID client Google** da aggiungere alla tua applicazione di back-end {{site.data.keyword.Bluemix_notm}}.

La seguente procedura ti fornisce una breve sintesi delle attività che devi eseguire per preparare la tua applicazione. 

**Nota:** non è necessario aggiungere il CocoaPod `Google/SignIn`. L'SDK necessario viene aggiunta dal seguente CocoaPod `BMSGoogleAuthentication`.

1. Prendi nota del **Bundle Identifier** nel tuo progetto Xcode dalla sezione **Identity** della scheda **General** della destinazione principale. Ne hai bisogno per creare il tuo progetto di accesso Google.

1. Crea un progetto su Google Developer per Google Sign-In for iOS all'indirizzo https://developers.google.com/mobile/add?platform=ios. 

2. Aggiungi il servizio Google Sign-In al tuo progetto.

3. Richiama il `GoogleService-Info.plist`.

  **Importante:** quando ottieni il file `GoogleService-Info.plist`, aprilo e annota il valore di `CLIENT_ID`. Hai bisogno di questo valore per configurare l'applicazione di back-end {{site.data.keyword.amashort}}.

1. Aggiungi il file `GoogleService-Info.plist` al tuo progetto Xcode. Per ulteriori informazioni, vedi [Add the configuration file to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config).

1. Aggiorna gli schemi URL nel tuo progetto Xcode con il tuo `REVERSE_CLIENT_ID` e l'ID bundle. Per ulteriori informazioni,
vedi [Add URL schemes to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add_a_url_scheme_to_your_project).


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
{: #install-cocoapods}

1. Apri il terminale ed esegui il comando **pod --version**. Se già hai CocoaPods installato, viene visualizzato il numero versione. Puoi passare direttamente alla sezione successiva per l'installare l'SDK.

1. Se non hai CocoaPods installato, esegui:
```
sudo gem install cocoapods
```
Per ulteriori informazioni, visita il [sito web di CocoaPods](https://cocoapods.org/).

### Installazione dell'SDK Swift client {{site.data.keyword.amashort}} con CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. Se non disponi di un `Podfile` nel tuo progetto iOS, esegui `pod init` per creare il file.

1. Modifica `Podfile` e aggiungi le seguenti righe alla destinazione pertinente:

 ```
 use_frameworks!
 pod 'BMSGoogleAuthentication'
 ```
 
 **Nota:** se hai già installato l'SDK core {{site.data.keyword.amashort}}, puoi rimuovere questa riga: `pod 'BMSSecurity'`. Il pod `BMSGoogleAuthentication` installa tutti i frameork necessari.
	
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

1. Utilizza il seguente codice per inizializzare l'SDK client. Sostituisci `<applicationRoute>` e `<applicationGUID>` con i valori per **Rotta** e **GUID applicazione** che hai ottenuto da **Opzioni mobili** nel dashboard {{site.data.keyword.Bluemix_notm}}. Sostituisci `<applicationBluemixRegion>` con la regione in cui è ospitata la tua applicazione {{site.data.keyword.Bluemix_notm}}. Per visualizzare la tua regione {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona viso (![Viso](/face.png "Viso")) nell'angolo in alto a sinistra del dashboard. 

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 // Inizializza l'SDK client.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUId, bluemixRegion: BMSClient.<applicationBluemixRegion>)

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
{: screen}

1. Puoi anche aggiungere la funzionalità di disconnessione aggiungendo il seguente codice:

 ```
 GoogleAuthenticationManager.sharedInstance.logout(callBack)
 ```

  Se richiami questo codice dopo che un utente ha eseguito l'accesso con Google e l'utente prova ad eseguire nuovamente l'accesso, gli viene richiesto di autorizzare {{site.data.keyword.amashort}} a utilizzare Google per scopi di autenticazione. A tal punto, l'utente può fare clic sul nome utente nell'angolo superiore destro dello schermo per selezionare, ed eseguire l'accesso con, un altro utente.

   Passare `callBack` alla funzione di disconnessione è facoltativo. Puoi anche passare `nil`.
