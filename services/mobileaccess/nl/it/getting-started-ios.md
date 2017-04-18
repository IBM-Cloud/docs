---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"

---
{:shortdesc: .shortdesc}

# Configurazione dell'SDK Objective-C iOS
{: #getting-started-ios}

Strumenta la tua applicazione iOS con l'SDK {{site.data.keyword.amafull}}, inizializza l'SDK ed effettua richieste a risorse protette e non protette.

{:shortdesc}

**Importante:** mentre la SDK Objective-C SDK rimane completamente supportata ed è ancora considerata la SDK primaria per i servizi mobili  {{site.data.keyword.Bluemix_notm}}, è pianificato di abbandonarla più avanti questo anno in favore della nuova SDK Swift. Per le nuove applicazioni consigliamo caldamente di utilizzare l'SDK Swift (consulta [Configurazione dell'SDK Swift iOS](getting-started-ios-swift-sdk.html)).

## Prima di cominciare
{: #before-you-begin}
È necessario disporre di:
* Un'istanza di un'applicazione  {{site.data.keyword.Bluemix_notm}} che è protetta da un servizio {{site.data.keyword.amashort}}. Per ulteriori informazioni su come creare un'applicazione di back-end {{site.data.keyword.Bluemix_notm}}, vedi [Introduzione](index.html).
* Il tuo **TenantID**. Apri il tuo servizio nel dashboard {{site.data.keyword.amashort}}. Fai clic su **Opzioni mobili**. I valori `tenantId` (noti anche come `appGUID`)  vengono visualizzati nel campo **GUID applicazione / TenantId**. Avrai bisogno di questo valore per inizializzare il gestore autorizzazione {{site.data.keyword.amashort}}.
* La tua **Rotta applicazione**. Questa è l'URL della tua applicazione di back-end. Hai bisogno di questo valore per inviare le richieste agli endpoint protetti correlati.
* Un progetto Xcode.  


## Installazione dell'SDK client {{site.data.keyword.amashort}}
{: #install-mca-sdk-ios}
L'SDK {{site.data.keyword.amashort}} è distribuito con CocoaPods, un gestore dipendenze per i progetti iOS. CocoaPods scarica automaticamente le risorse utente dai repository e le rende disponibili alla tua applicazione iOS.


### Installa CocoaPods
{: #install-cocoapods}

1. Apri il terminale ed esegui il comando **pod --version**. Se già hai CocoaPods installato, viene visualizzato il numero versione. Passa direttamente alla sezione successiva per l'installare l'SDK.

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


	`pod 'IMFCore'`

1. Salva il file `Podfile` ed esegui `pod install` dalla riga di comando. <br/>Cocoapods installa le dipendenze aggiunte e visualizza i componenti aggiunti.<br/>

	**Importante**: CocoaPods genera un file `xcworkspace`.  In futuro, dovrai aprire questo file per lavorare sul tuo progetto.

1. Apri il tuo spazio di lavoro del progetto iOS. Apri il file `xcworkspace` che è stato generato da CocoaPods. Ad esempio: `{il-tuo-nome-progetto}.xcworkspace`. Esegui `open {il-tuo-nome-progetto}.xcworkspace`.

## Inizializzazione dell'SDK client {{site.data.keyword.amashort}}
{: #init-mca-sdk-ios}

1. Importa il framework `IMFCore` nella classe che desideri utilizzi l'SDK client {{site.data.keyword.amashort}} aggiungendo la seguente intestazione:

	####Objective-C
	{: #imfcore-objc}

	```Objective-C
	#import <IMFCore/IMFCore.h>
	```

	####Swift
	{: #sdk-swift}

	L'SDK client {{site.data.keyword.amashort}} viene implementato con Objective-C. Potresti dover aggiungere un'intestazione di collegamento al tuo progetto Swift:
	1. Fai clic con il pulsante destro del mouse sul tuo progetto in Xcode e seleziona **New File**.
	1. Nella categoria **iOS Source**, fai clic su **Header file**. Denomina il file `BridgingHeader.h`.
	1. Aggiungi la seguente riga all'intestazione di collegamento: `#import <IMFCore/IMFCore.h>`.
	1. Fai clic sul tuo progetto in Xcode e seleziona la scheda **Build Settings**.
	1. Cerca `Objective-C Bridging Header`.
	1. Imposta il valore sull'ubicazione del tuo file `BridgingHeader.h`, ad esempio `$(SRCROOT)/MyApp/BridgingHeader.h`.
	1. Assicurati che la tua intestazione di collegamento venga rilevata da Xcode compilando il tuo progetto. Non dovresti vedere alcun messaggio di errore.

1. Utilizza il seguente codice per inizializzare l'SDK client {{site.data.keyword.amashort}}.  Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `application:didFinishLaunchingWithOptions` del tuo delegato dell'applicazione. <br/>
Per informazioni su come ottenere `applicationRoute` e `applicationGUID`  consulta [Prima di cominciare](#before-you-begin). 

	####Objective-C
	{: #sharedinstance-objc}

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	####Swift
	{: #sharedinstance-swift}
	```Swift
 		MFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",backendGUID: "applicationGUID")
	```

## Inizializzazione di AuthorizationManager
Inizializza `AuthorizationManager` trasmettendo al servizio  {{site.data.keyword.amashort}} il parametro `tenantId`. Per informazioni su come ottenere questi valori, consulta [Prima di cominciare](#before-you-begin). 

#### Objective-C

```Objective-C
[[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"<tenantId>"];
```

#### Swift

```Swift
IMFAuthorizationManager.sharedInstance().initializeWithTenantId("<tenantId>")
```

	
## Effettuare una richiesta alla tua applicazione di back-end mobile
{: #request}

Dopo che l'SDK client {{site.data.keyword.amashort}} è stato inizializzato, puoi iniziare a effettuare richieste alla tua applicazione di back-end mobile.

1. Prova a inviare una richiesta a un endpoint protetto sula tua applicazione di back-end mobile nel tuo browser. Apri il seguente URL: `{applicationRoute}/protected`. Ad esempio: `http://my-mobile-backend.mybluemix.net/protected`
<br/>L'endpoint `/protected` di un'applicazione di back-end mobile creato con il contenitore tipo MobileFirst Services Starter è protetto con {{site.data.keyword.amashort}}. Nel tuo browser viene restituito un messaggio `Unauthorized` perché a questo endpoint possono accedere solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}.

1. Utilizza la tua applicazione iOS per effettuare una richiesta allo stesso endpoint. Aggiungi il seguente codice dopo che hai inizializzato `IMFClient`:

	####Objective-C
	{: #nsstring-objc}

	```Objective-C
	NSString *requestPath = [NSString stringWithFormat:@"%@/protected",
								[[IMFClient sharedInstance] backendRoute]];

	IMFResourceRequest *request =  [IMFResourceRequest
				requestWithPath:requestPath
				method:@"GET"];

	[request sendWithCompletionHandler:^(IMFResponse *response, NSError *error) {
		if (error){
			NSLog(@"Error :: %@", [error description]);
		} else {
			NSLog(@"Response :: %@", [response responseText]);
		}
	}];
	```

	####Swift
	{: #imfclientrequestpath-swift}

	```Swift
	let requestPath = IMFClient.sharedInstance().backendRoute + "/protected"

	let request = IMFResourceRequest(path: requestPath, method: "GET");
	request.sendWithCompletionHandler { (response, error) -> Void in
		if (nil != error){
			NSLog("Error :: %@", error.description)
		} else {
			NSLog("Response :: %@", response.responseText)
		}
	};

	```

1.  Quando la tua richiesta ha esito positivo, nella console Xcode vedrai il seguente output:

	![immagine](images/getting-started-ios-success.png)

## Fasi successive
{: #next-steps}
Quando ti sei connesso all'endpoint protetto, non è stata richiesta alcuna credenziale. Per richiedere ai tuoi utenti di accedere alla tua applicazione, devi configurare l'autenticazione Facebook, Google o personalizzata.
  * [Facebook](facebook-auth-ios.html)
  * [Google](google-auth-ios.html)
  * [Personalizzata](custom-auth-ios.html)
