---

copyright:
  years: 2016
lastupdated: "2016-10-10"
---
{:shortdesc: .shortdesc}
{:screen: .screen}


# Configurazione dell'SDK Swift iOS
{: #getting-started-ios}

{{site.data.keyword.amafull}} ha rilasciato una nuova SDK Swift che aggiunge e migliora le funzionalità fornite dall'SDK Objective-C {{site.data.keyword.amashort}} esistente, rendendo più semplice l'autenticazione alla tua applicazione e fornendo una migliore protezione per le tue risorse di back-end. Strumenta la tua applicazione Swift iOS con l'SDK {{site.data.keyword.amashort}}, inizializza l'SDK ed effettua richieste a risorse protette e non protette.

{:shortdesc}

**Nota:** La SDK Objective-C riporta i dati di monitoraggio alla console di monitoraggio del servizio {{site.data.keyword.amashort}}. Nel caso fai affidamento sulla funzionalità di monitoraggio del servizio {{site.data.keyword.amashort}} devi continuare ad utilizzare l'SDK Objective-C.

Mentre la SDK Objective-C SDK rimane completamente supportata ed è ancora considerata la SDK primaria per i servizi mobili {{site.data.keyword.Bluemix_notm}}, è pianificato di abbandonarla più avanti questo anno in favore di questa nuova SDK Swift. 


## Prima di cominciare
{: #before-you-begin}
È necessario disporre di:
* Un'istanza di un'applicazione  {{site.data.keyword.Bluemix_notm}} che è protetta da un servizio {{site.data.keyword.amashort}}. Per ulteriori informazioni su come creare un'applicazione di back-end {{site.data.keyword.Bluemix_notm}}, vedi [Introduzione](index.html).
* Un progetto Xcode. Per ulteriori informazioni su come configurare il tuo ambiente di sviluppo iOS, consulta il [sito web per gli sviluppatori Apple](https://developer.apple.com/support/xcode/).


## Installazione dell'SDK client {{site.data.keyword.amashort}}
{: #install-mca-sdk-ios}
L'SDK {{site.data.keyword.amashort}} è distribuito con CocoaPods, un gestore dipendenze per i progetti iOS. CocoaPods scarica automaticamente le risorse utente dai repository e le rende disponibili alla tua applicazione iOS.


### Installa CocoaPods
{: #install-cocoapods}

1. In una finestra terminale, esegui il comando **pod --version**. Se già hai CocoaPods installato, viene visualizzato il numero versione e puoi passare direttamente alla sezione successiva per l'installare l'SDK.

1. Se non hai CocoaPods installato, esegui:

```
sudo gem install cocoapods
```

Per ulteriori informazioni, visita il [sito web di CocoaPods](https://cocoapods.org/).

### Installa l'SDK client {{site.data.keyword.amashort}} con CocoaPods
{: #install-sdk-cocoapods}

1. In una finestra terminale, passa alla directory root del tuo progetto iOS.

1. Se non hai già inizializzato il tuo spazio di lavoro per CocoaPods, esegui il comando `pod init`.<br/>
 CocoaPods crea un file `Podfile` per te, che è dove definisci le dipendenze per il tuo progetto iOS.

1. Modifica il file `Podfile` e aggiungi la seguente riga alle destinazioni richieste:

	```
  use_frameworks!
  pod 'BMSSecurity'
	```

  **Suggerimento:** puoi aggiungere `use_frameworks!` alla tua destinazione Xcode invece di averlo nel Podfile.

1. Salva il file `Podfile` ed esegui `pod install` dalla riga di comando. Cocoapods installa le dipendenze rilevanti e visualizza i pod e le dipendenze aggiunte.<br/>

   **Importante**: CocoaPods genera un file `xcworkspace`.  In futuro, dovrai aprire questo file per lavorare sul tuo progetto.

1. Apri il tuo spazio di lavoro del progetto iOS. Apri il file `xcworkspace` che è stato generato da CocoaPods. Ad esempio, per `{your-project-name}.xcworkspace`, esegui

	`open {your-project-name}.xcworkspace`

## Inizializzazione dell'SDK client {{site.data.keyword.amashort}}
{: #init-mca-sdk-ios}

 Inizializza l'SDK passando il parametro `applicationGUID`. Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `application:didFinishLaunchingWithOptions` del tuo delegato dell'applicazione.
 

1. Ottieni i valori del parametro del tuo servizio. Apri il tuo servizio nel dashboard {{site.data.keyword.Bluemix_notm}}. Fai clic su **Opzioni mobili**. I valori `applicationRoute` e `tenantId` (conosciuti anche come `appGUID`)  sono visualizzati nei campi **Rotta** and **GUID applicazione / TenantId**. Avrai bisogno di questi valori per inizializzare l'SDK e per inviare le richieste all'applicazione di backend. 

1. Importa i framework richiesti nella classe dove vuoi utilizzare l'SDK client {{site.data.keyword.amashort}}.

 ```Swift
 import BMSCore
 import BMSSecurity
 ```

1. Inizializza l'SDK client {{site.data.keyword.amashort}}.

```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: 
		[UIApplicationLaunchOptionsKey: Any]?) -> Bool {

	let mcaAuthManager = MCAAuthorizationManager.sharedInstance
    mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
      // valori possibili per regionName: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, BMSClient.Region.sydney
	BMSClient.sharedInstance.authorizationManager = mcaAuthManager	
	return true
	}
 ```

* Sostituisci `tenantId` con il valore ottenuto dalle **Opzioni mobili**. Consulta il **passo 1**.
* Sostituisci `<applicationBluemixRegion>` con la regione in cui è ospitata la tua applicazione {{site.data.keyword.Bluemix_notm}}. Per visualizzare la tua regione {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona **Avatar** ![icona Avatar](images/face.jpg "icona Avatar")  nella barra del menu per aprire il widget **Account e supporto**. Il valore della regione visualizzato deve essere uno dei seguenti: **Stati Uniti Sud**, **Regno Unito** o **Sydney**, e corrisponde ai valori costanti richiesti nel codice:  `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` o `BMSClient.Region.sydney`.

   
## Effettuare una richiesta alla tua applicazione di back-end mobile
{: #request}

Dopo che l'SDK client {{site.data.keyword.amashort}} è stato inizializzato, puoi iniziare a effettuare richieste alla tua applicazione di back-end mobile.

1. Prova a inviare una richiesta a un endpoint protetto sula tua applicazione di back-end mobile nel tuo browser. Apri il seguente URL: `{applicationRoute}/protected`, sostituendo `{applicationRoute}` con il valore **applicationRoute** richiamato dalle **Opzioni mobili** (consulta [Inizializzazione della SDK client Mobile Client Access](#init-mca-sdk-ios)). Ad esempio: 

	`http://my-mobile-backend.mybluemix.net/protected
	`

	L'endpoint `/protected` di un'applicazione di backend mobile creato con il contenitore tipo MobileFirst Services Starter è protetto con {{site.data.keyword.amashort}}. Nel tuo browser viene restituito un messaggio `Unauthorized` perché a questo endpoint possono accedere solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}.

1. Utilizza la tua applicazione iOS per effettuare una richiesta allo stesso endpoint. Aggiungi il seguente codice dopo che hai inizializzato `BMSClient`:

 ```Swift
	let customResourceURL = "<your protected resource absolute path>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
  if error == nil {
       	    print ("response:\(response?.responseText), no error")
 } else {
       	    print ("error: \(error)")
     }
	}

	request.send(completionHandler: callBack)
 ```
 {: codeblock}

1.  Quando la tua richiesta ha esito positivo, nella console Xcode è visualizzato il seguente output:

 ```
 response:Optional("Salve, questa è una risorsa protetta dell'applicazione backend mobile!"), no error
 ```
{: screen}
 
## Fasi successive
{: #next-steps}
Quando ti sei connesso all'endpoint protetto, non è stata richiesta alcuna credenziale. Per richiedere ai tuoi utenti di accedere alla tua applicazione, devi configurare l'autenticazione Facebook, Google o personalizzata.
  * [Facebook](facebook-auth-ios-swift-sdk.html)
  * [Google](google-auth-ios-swift-sdk.html)
  * [Personalizzata](custom-auth-ios-swift-sdk.html)
