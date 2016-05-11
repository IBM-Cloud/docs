---

copyright:
  years: 2016

---

# Abilitazione dell'autenticazione Facebook nelle applicazioni iOS (SDK Swift)
{: #facebook-auth-ios}

Per utilizzare Facebook come un provider di identità nelle tue applicazioni iOS, aggiungi e configura la piattaforma iOS per la tua applicazione Facebook.

## Prima di cominciare
{: #facebook-auth-ios-before}

* Devi disporre di una risorsa protetta da {{site.data.keyword.amashort}} e di un progetto iOS strumentato con l'SDK client {{site.data.keyword.amashort}}.  Per ulteriori informazioni, vedi [Introduzione a {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) e [Configurazione dell'SDK Swift iOS](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html).  
* Proteggi manualmente la tua applicazione di backend con l'SDK server {{site.data.keyword.amashort}}. Per ulteriori informazioni, vedi [Protezione delle risorse](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).
* Crea un ID applicazione Facebook. Per ulteriori informazioni, vedi [Ottenimento di un ID applicazione Facebook dal portale sviluppatori Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).

## Configurazione della tua applicazione Facebook per la piattaforma iOS
{: #facebook-auth-ios-config}

1. Accedi al [dashboard della tua applicazione Facebook](https://developers.facebook.com/apps/).

1. Annota l'**ID applicazione** per la tua applicazione. Questo valore ti servirà quando configuri il tuo progetto iOS per l'autenticazione Facebook.

1. Fai clic su **Settings > Add Platform > iOS**.

1. Specifica il *bundleId* della tua applicazione iOS. Per trovare il *bundleId* della tua applicazione iOS, cerca il **Bundle Identifier**
nel file `info.plist` o nella scheda **General** del progetto Xcode.
**Suggerimento:**: valuta l'abilitazione del suffisso di schema URL o di SSO (Single Sign On) se intendi utilizzare tali funzioni.

1. Fai clic su **Save Settings**.

## Configurazione di {{site.data.keyword.amashort}} per l'autenticazione Facebook
{: #facebook-auth-ios-configmca}

Dopo che hai configurato l'ID applicazione Facebook e la tua applicazione Facebook perché serva client iOS, puoi abilitare l'autenticazione Facebook in {{site.data.keyword.amashort}}.

1. Apri la tua applicazione nel dashboard {{site.data.keyword.Bluemix}}.

1. Fai clic su **Opzioni mobili** e annota **Rotta** (*applicationRoute*) e **GUID applicazione** (*applicationGUID*). Questi valori ti servono quando inizializzi l'SDK.

1. Fai clic sul tile {{site.data.keyword.amashort}}. Il dashboard {{site.data.keyword.amashort}} viene caricato.

1. Fai clic sul tile **Facebook**.

1. Specifica l'ID applicazione Facebook e fai clic su **Save**.

## Configurazione dell'SDK client {{site.data.keyword.amashort}} per iOS
{: #facebook-auth-ios-sdk}

### Installazione di CocoaPods
{: #facebook-auth-cocoapods}

L'SDK client {{site.data.keyword.amashort}} viene distribuito con CocoaPods, un gestore dipendenze per i progetti iOS. CocoaPods scarica automaticamente le risorse utente dai repository e le rende disponibili alla tua applicazione iOS.

1. Apri il terminale ed esegui il comando `pod --version`. Se già hai CocoaPods installato, viene visualizzato il numero versione. Puoi passare direttamente alla sezione successiva di questa esercitazione.

1. Installa CocoaPods eseguendo `sudo gem install cocoapods`. Fai riferimento al [sito web CocoaPods](https://cocoapods.org/) nel caso ti occorrano ulteriori indicazioni.

1. Chiudi XCode.

1. Apri il terminale e vai (con `cd`) alla directory del tuo progetto.

1.  Esegui `pod init`.

### Installazione dell'SDK Swift client {{site.data.keyword.amashort}} con CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. Nel tuo progetto iOS, modifica il `Podfile` e aggiungi le seguenti righe:

 ```
use_frameworks!
pod 'BMSFacebookAuthentication'
	```
 **Suggerimento:** puoi aggiungere `use_frameworks!` alla tua destinazione Xcode invece di averlo nel Podfile.

1. Salva il `Podfile` ed esegui il comando `pod install` dalla riga di comando. CocoaPods installa le dipendenze. Vengono visualizzati lo stato di avanzamento e quali componenti sono stati aggiunti.

 **Importante**: devi ora aprire il tuo progetto utilizzando il file `xcworkspace` che viene generato da CocoaPods. Di norma, il
nome è `{il-tuo-nome-progetto}.xcworkspace`.  

1. Esegui `open {il-tuo-nome-progetto}.xcworkspace` dalla riga di comando per aprire il tuo spazio di lavoro del progetto iOS.

### Configurazione del tuo progetto iOS per l'autenticazione Facebook
{: #facebook-auth-ios-configproject}

1. Trova il file `info.plist`, che di solito si trova nella cartella `Supporting files` nel tuo progetto Xcode.

1. Configura l'integrazione Facebook aggiungendo le seguenti proprietà al tuo file `info.plist`:

   ![immagine](images/ios-facebook-infoplist-settings.png)

   Aggiorna le proprietà schema URL e FacebookappID con il tuo ID applicazione Facebook.

   Puoi anche aggiornare il file `info.plist` facendo clic con il pulsante destro del mouse su di esso, selezionando **Open as > Source Code** e aggiungendo il seguente XML:

   ```XML
	<key>CFBundleURLTypes</key>
	<array>
		<dict>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>fb{il-tuo-id-applicazione-facebook}</string>
			</array>
		</dict>
	</array>
	<key>FacebookAppID</key>
	<string>{il-tuo-id-applicazione-facebook}</string>
	<key>FacebookDisplayName</key>
	<string>{your-faceebook-application-name}</string>
	<key>LSApplicationQueriesSchemes</key>
	<array>
		<string>fbauth</string>
		<string>fbauth2</string>
	</array>
	<key>NSAppTransportSecurity</key>
	<dict>
	    <key>NSExceptionDomains</key>
	    <dict>
	        <key>facebook.com</key>
	        <dict>
	            <key>NSIncludesSubdomains</key>
	            <true/>                
	            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
	            <false/>
	        </dict>
	        <key>fbcdn.net</key>
	        <dict>
	            <key>NSIncludesSubdomains</key>
	            <true/>
	            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
	            <false/>
	        </dict>
	        <key>akamaihd.net</key>
	        <dict>
	            <key>NSIncludesSubdomains</key>
	            <true/>
	            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
	            <false/>
	        </dict>
	    </dict>
	</dict>
```
   Aggiorna le proprietà schema URL e FacebookappID con il tuo ID applicazione Facebook. Aggiorna il FacebookDisplayName con il nome della tua applicazione Facebook.

    **Importante**: assicurati di non sovrascrivere alcuna proprietà esistente nel file `info.plist`. Se hai delle proprietà che si sovrappongono, devi unirle manualmente. Per ulteriori informazioni, vedi [Configure Xcode Project](https://developers.facebook.com/docs/ios/getting-started/) e [Preparing Your Apps for iOS9](https://developers.facebook.com/docs/ios/ios9).

## Inizializzazione dell'SDK Swift client {{site.data.keyword.amashort}}
{: #facebook-auth-ios-initalize-swift}

Inizializza l'SDK client passando i parametri `applicationGUID` e `applicationRoute`.

Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `application:didFinishLaunchingWithOptions` del tuo delegato dell'applicazione

1. Ottieni i valori di parametro della tua applicazione. Apri la tua applicazione nel dashboard {{site.data.keyword.Bluemix_notm}}. Fai clic su **Opzioni mobili**. I valori `applicationRoute` e `applicationGUID` sono visualizzati nei campi **Rotta** e **GUID applicazione**.

1. Importa il framework richiesto nella classe che desideri utilizzi l'SDK client {{site.data.keyword.amashort}} aggiungendo le seguenti intestazioni:

 ```swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```
2. Inizializza l'SDK client.	Sostituisci `<applicationRoute>` e `<applicationGUID>` con
i valori per **Rotta** e **GUID applicazione** che hai ottenuto da **Opzioni mobili** nel dashboard {{site.data.keyword.Bluemix_notm}}.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<regione Bluemix applicazione>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 FacebookAuthenticationManager.sharedInstance.register()
 ```

1. Segnala all'SDK Facebook l'attivazione dell'applicazione e registra il gestore autenticazione Facebook aggiungendo il seguente codice al
metodo `application:didFinishLaunchingWithOptions` nel tuo delegato dell'applicazione. Aggiungi questo codice subito dopo aver inizializzato l'istanza BMSClient e registrato Facebook come gestore autenticazione.

 ```Swift
  return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
 ```

1. Copia il file `FacebookAuthenticationManager.swift` dai file di origine pod `BMSFacebookAuthentication` alla directory del tuo progetto.

1. Aggiungi il seguente codice al tuo delegato dell'applicazione.

 ```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		return FacebookAuthenticationManager.sharedInstance.onOpenURL(application, url: url, sourceApplication: sourceApplication, annotation: annotation)

	}
 ```

## Verifica dell'autenticazione
{: #facebook-auth-ios-testing}

Dopo che l'SDK client è stato inizializzato e il gestore autenticazione Facebook è stato registrato, puoi iniziare a effettuare richieste al tuo backend mobile.

### Prima di cominciare
{: #facebook-auth-ios-testing-before}

Devi utilizzare il contenitore tipo {{site.data.keyword.mobilefirstbp}} e disporre già di una risorsa protetta da {{site.data.keyword.amashort}} all'endpoint `/protected`. Se devi configurare un endpoint `/protected`, consulta [Protezione delle risorse](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Prova a inviare una richiesta all'endpoint protected del backend mobile appena creato nel tuo browser. Apri il seguente URL: `{applicationRoute}/protected`.
Ad esempio: `http://my-mobile-backend.mybluemix.net/protected`
<br/>L'endpoint `/protected` di un backend mobile creato con il contenitore tipo MobileFirst Services Starter è protetto con {{site.data.keyword.amashort}}. Nel tuo browser viene restituito un messaggio `Unauthorized`. Questo messaggio viene restituito perché a questo endpoint possono accedere solo le applicazioni mobili strumentate con l'SDK client{{site.data.keyword.amashort}}.

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

1. Esegui la tua applicazione. Viene visualizzata una schermata di accesso Facebook.

   ![immagine](images/ios-facebook-login.png)

   Questa schermata può avere un aspetto lievemente differente se non sei attualmente collegato a Facebook.

1. Fai clic su **OK** per autorizzare {{site.data.keyword.amashort}} a usare la tua identità utente Facebook per scopi di autenticazione.

1. 	Quando la tua richiesta ha esito positivo, nella console Xcode è visualizzato il seguente output:

 ```
 "onAuthenticationSuccess info = Optional({
     attributes =     {
     };
     deviceId = 218227041863639;
     displayName = "Don+Lon";
     isUserAuthenticated = 1;
     userId = 218227041863639;
 })
 response:Optional("Salve, questa è una risorsa protetta dell'applicazione backend mobile!"), no error
 ```

1. Puoi anche aggiungere la funzionalità di disconnessione aggiungendo il seguente codice:

 ```
FacebookAuthenticationManager.sharedInstance.logout(callBack)
```

 Se richiami questo codice dopo che un utente ha eseguito l'accesso con Facebook e l'utente prova ad eseguire nuovamente l'accesso, gli viene richiesto di autorizzare {{site.data.keyword.amashort}} a utilizzare Facebook per scopi di autenticazione. 

 Per passare da un utente all'altro, è necessario richiamare questo codice e l'utente deve eseguire la disconnessione da Facebook nel suo browser.

 Il passaggio di ```callBack``` alla funzione di disconnessione è facoltativo. Puoi anche passare `nil`.
