---

copyright:
  years: 2016

---

# Configurazione dell'SDK Swift iOS
{: #getting-started-ios}

Strumenta la tua applicazione iOS con l'SDK {{site.data.keyword.amashort}}, inizializza l'SDK ed effettua richieste a risorse protette e non protette.

## Prima di cominciare
{: #before-you-begin}
* Devi disporre di un'istanza di un backend mobile protetto dal servizio {{site.data.keyword.amashort}}. Per ulteriori informazioni su come creare un backend mobile, consulta [Introduzione](getting-started.html).
* Assicurati di aver configurato correttamente Xcode. Per ulteriori informazioni su come configurare il tuo ambiente di sviluppo iOS, consulta il [sito web per gli sviluppatori Apple](https://developer.apple.com/support/xcode/).


## Installazione dell'SDK client {{site.data.keyword.amashort}}
{: #install-mca-sdk-ios}
L'SDK {{site.data.keyword.amashort}} è distribuito con CocoaPods, un gestore dipendenze per i progetti iOS. CocoaPods scarica automaticamente le risorse utente dai repository e le rende disponibili alla tua applicazione iOS.


### Installa CocoaPods
{: #install-cocoapods}
1. Apri il terminale ed esegui il comando **pod --version**. Se già hai CocoaPods installato, viene visualizzato il numero versione. Puoi passare direttamente alla sezione successiva per l'installare l'SDK.

1. Se non hai CocoaPods installato, esegui:
```
sudo gem install cocoapods
```
Per ulteriori informazioni, visita il [sito web di CocoaPods](https://cocoapods.org/).

### Installa l'SDK client {{site.data.keyword.amashort}} con CocoaPods
{: #install-sdk-cocoapods}

1. Nel terminale, passa alla directory root del tuo progetto iOS.

1. Se non hai già inizializzato il tuo spazio di lavoro per CocoaPods, esegui il comando `pod init`.<br/>
 CocoaPods crea un file `Podfile` per te, che è dove definisci le dipendenze per il tuo progetto iOS.

1. Modifica il file `Podfile` e aggiungi la seguente riga alle destinazioni richieste:

	```
  use_frameworks!
	pod 'BMSSecurity'
	```
  **Suggerimento:** puoi aggiungere `use_frameworks!` alla tua destinazione Xcode invece di averlo nel Podfile.

1. Salva il file `Podfile` ed esegui `pod install` dalla riga di comando. <br/>Cocoapods installa le dipendenze aggiunte. Puoi vedere lo stato di avanzamento e quali componenti sono stati aggiunti.<br/>
**Importante**: CocoaPods genera un file `xcworkspace`.  In futuro, dovrai aprire questo file per lavorare sul tuo progetto.

1. Apri il tuo spazio di lavoro del progetto iOS. Apri il file `xcworkspace` che è stato generato da CocoaPods. Ad esempio: `{il-tuo-nome-progetto}.xcworkspace`. Esegui `open {il-tuo-nome-progetto}.xcworkspace`.

## Inizializzazione dell'SDK client {{site.data.keyword.amashort}}
{: #init-mca-sdk-ios}

 Inizializza l'SDK passando i parametri `applicationRoute` e `applicationGUID`. Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `application:didFinishLaunchingWithOptions` del tuo delegato dell'applicazione.

1. Ottieni i valori di parametro della tua applicazione. Apri la tua applicazione nel dashboard {{site.data.keyword.Bluemix_notm}}. Fai clic su **Opzioni mobili**. I valori `applicationRoute` e `applicationGUID` sono visualizzati nei campi **Rotta** e **GUID applicazione**.

1. Importa i framework richiesti nella classe dove vuoi utilizzare l'SDK client {{site.data.keyword.amashort}}.

 ```Swift
 import BMSCore
 import BMSSecurity
 ```  

1. Inizializza l'SDK client {{site.data.keyword.amashort}}. Sostituisci `<applicationRoute>` e `<applicationGUID>` con
i valori per **Rotta** e **GUID applicazione** che hai ottenuto da **Opzioni mobili** nel dashboard {{site.data.keyword.Bluemix_notm}}.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 // Inizializza l'SDK client.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<regione Bluemix applicazione>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 return true
 }
 ```

## Effettuazione di una richiesta al tuo backend mobile
{: #request}

Dopo che l'SDK client {{site.data.keyword.amashort}} è stato inizializzato, puoi iniziare a effettuare richieste al tuo backend mobile.

1. Prova a inviare una richiesta a un endpoint protetto sul tuo backend mobile nel tuo browser. Apri il seguente URL: `{applicationRoute}/protected`. Ad esempio: `http://my-mobile-backend.mybluemix.net/protected`
<br/>L'endpoint `/protected` di un backend mobile creato con il contenitore tipo MobileFirst Services Starter è protetto con {{site.data.keyword.amashort}}. Nel tuo browser viene restituito un messaggio `Unauthorized` perché a questo endpoint possono accedere solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}.

1. Utilizza la tua applicazione iOS per effettuare una richiesta allo stesso endpoint. Aggiungi il seguente codice dopo che hai inizializzato `BMSClient`:

 ```Swift
 let customResourceURL = "<il percorso della tua risorsa protetta>"
 let request = Request(url: customResourceURL, method: HttpMethod.GET)
 let callBack:MfpCompletionHandler = {(response: Response?, error: NSError?) in
     if error == nil {
         print ("response:\(response?.responseText), no error")
     } else {
         print ("error: \(error)")
     }
 }

 request.sendWithCompletionHandler(callBack)
 ```

1.  Quando la tua richiesta ha esito positivo, nella console Xcode vedrai il seguente output:

 ```
 response:Optional("Salve, questa è una risorsa protetta dell'applicazione backend mobile!"), no error
 ```

## Fasi successive
{: #next-steps}
Quando ti sei connesso all'endpoint protetto, non è stata richiesta alcuna credenziale. Per richiedere ai tuoi utenti di accedere alla tua applicazione, devi configurare l'autenticazione Facebook, Google o personalizzata.
  * [Facebook](facebook-auth-ios-swift-sdk.html)
  * [Google](google-auth-ios-swift-sdk.html)
  * [Personalizzata](custom-auth-ios-swift-sdk.html)
