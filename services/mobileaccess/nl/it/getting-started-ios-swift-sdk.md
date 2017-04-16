---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Configurazione dell'SDK Swift iOS
{: #getting-started-ios}

Strumenta la tua applicazione Swift iOS con l'SDK {{site.data.keyword.amashort}}, inizializza l'SDK ed effettua richieste a risorse protette e non protette.

{:shortdesc}


## Prima di cominciare
{: #before-you-begin}
È necessario disporre di:

* Un'istanza di un'applicazione  {{site.data.keyword.Bluemix_notm}}.
* Un'istanza di un servizio {{site.data.keyword.amafull}}.
* Il tuo **TenantID**. Apri il tuo servizio nel dashboard {{site.data.keyword.amashort}}. Fai clic su **Opzioni mobili**. I valori `tenantId` (noti anche come `appGUID`)  vengono visualizzati nel campo **GUID applicazione / TenantId**. Avrai bisogno di questo valore per inizializzare il gestore autorizzazione {{site.data.keyword.amashort}}.
* La tua **Rotta applicazione**. Questa è l'URL della tua applicazione di back-end. Hai bisogno di questo valore per inviare le richieste agli endpoint protetti correlati.
* La tua **Regione** {{site.data.keyword.Bluemix_notm}}.  Puoi trovare la tua regione {{site.data.keyword.Bluemix_notm}} corrente nell'intestazione, accanto all'icona **Avatar** ![Icona Avatar](images/face.jpg "Icona Avatar"). Il valore della regione visualizzato deve essere uno dei seguenti: `Stati Uniti Sud`,  `Sydney` o  `Regno Unito` e corrisponde ai valori delle SDK richiesti nel codice: `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` o `BMSClient.Region.sydney`.  Avrai bisogno di questo valore per inizializzare l'SDK {{site.data.keyword.amashort}}.
* Un progetto Xcode. Per ulteriori informazioni su come configurare il tuo ambiente di sviluppo iOS, consulta il [sito Web Apple Developer![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.apple.com/support/xcode/ "Icona link esterno"){: new_window}.


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
{: codeblock}

Per ulteriori informazioni, visita il [sito Web CocoaPods![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cocoapods.org/ "Icona link esterno"){: new_window}.

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
	{: codeblock}

  **Suggerimento:** puoi aggiungere `use_frameworks!` alla tua destinazione Xcode invece di averlo nel Podfile.

1. Salva il file `Podfile` ed esegui `pod install` dalla riga di comando. Cocoapods installa le dipendenze rilevanti e visualizza i pod e le dipendenze aggiunte.<br/>

   **Importante**: CocoaPods genera un file `xcworkspace`.  In futuro, dovrai aprire questo file per lavorare sul tuo progetto.

1. Apri il tuo spazio di lavoro del progetto iOS. Apri il file `xcworkspace` che è stato generato da CocoaPods. Ad esempio, per `{your-project-name}.xcworkspace`, esegui

	`open {your-project-name}.xcworkspace`

### Abilitare Keychain Sharing per iOS
{: #enable_keychain}

Abilita `Keychain Sharing`. Vai alla scheda `Funzionalità` e passa `Keychain Sharing` su `Attivo` nel tuo progetto Xcode.

## Inizializzazione dell'SDK client {{site.data.keyword.amashort}}
{: #init-mca-sdk-ios}

 Inizializza l'SDK passando il parametro `tenantId`. Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `application:didFinishLaunchingWithOptions` del tuo delegato dell'applicazione.

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
  {: codeblock}

* Sostituisci `tenantId` con il valore ottenuto dalle **Opzioni mobili**.
* Sostituisci `<applicationBluemixRegion>` con la regione in cui è ospitata la tua applicazione {{site.data.keyword.Bluemix_notm}}.

Per informazioni su questi valori, consulta [Prima di cominciare](#before-you-begin).


## Effettuare una richiesta alla tua applicazione di back-end mobile
{: #request}

Dopo che l'SDK client {{site.data.keyword.amashort}} è stato inizializzato, puoi iniziare a effettuare richieste alla tua applicazione di back-end mobile.

1. Prova a inviare una richiesta a un endpoint protetto sula tua applicazione di back-end mobile nel tuo browser. Apri il seguente URL: `{applicationRoute}/protected`, sostituendo `{applicationRoute}` con il valore **applicationRoute** richiamato dalle **Opzioni mobili** (consulta [Inizializzazione della SDK client Mobile Client Access](#init-mca-sdk-ios)). Ad esempio:

	`http://my-mobile-backend.mybluemix.net/protected
	`

	Nel tuo browser viene restituito un messaggio `Unauthorized` perché a questo endpoint possono accedere solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}.

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
