---

copyright:
  years: 2015, 2016

---

# Configurazione dell'SDK Objective-C iOS
{: #getting-started-ios}

Strumenta la tua applicazione iOS con l'SDK {{site.data.keyword.amashort}}, inizializza l'SDK ed effettua richieste a risorse protette e non protette.

**Suggerimento:** se stai sviluppando la tua applicazione iOS in Swift, valuta l'utilizzo dell'SDK Swift client {{site.data.keyword.amashort}}. Per i dettagli, vedi [Configurazione dell'SDK Swift iOS](getting-started-ios-swift-sdk.html)

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
	pod 'IMFCore'
	```

1. Salva il file `Podfile` ed esegui `pod install` dalla riga di comando. <br/>Cocoapods installa le dipendenze aggiunte. Puoi vedere lo stato di avanzamento e quali componenti sono stati aggiunti.<br/>
**Importante**: CocoaPods genera un file `xcworkspace`.  In futuro, dovrai aprire questo file per lavorare sul tuo progetto.

1. Apri il tuo spazio di lavoro del progetto iOS. Apri il file `xcworkspace` che è stato generato da CocoaPods. Ad esempio: `{il-tuo-nome-progetto}.xcworkspace`. Esegui `open {il-tuo-nome-progetto}.xcworkspace`.

## Inizializzazione dell'SDK client {{site.data.keyword.amashort}}
{: #init-mca-sdk-ios}

Per utilizzare l'SDK client {{site.data.keyword.amashort}}, devi inizializzare l'SDK passando i parametri di **Rotta** (`applicationRoute`) e **GUID applicazione** (`applicationGUID`).


1. Dalla pagina principale del dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sulla tua applicazione. Fai clic su **Opzioni mobili**. Ti servono i valori **Rotta** e **GUID applicazione** per inizializzare l'SDK.

1. Importa il framework `IMFCore` nella classe che desideri utilizzi l'SDK client {{site.data.keyword.amashort}} aggiungendo la seguente intestazione:

	**Objective-C:**
	 ```Objective-C
	#import <IMFCore/IMFCore.h>
	```

	**Swift:**

	L'SDK client {{site.data.keyword.amashort}} viene implementato con Objective-C. Potresti dover aggiungere un'intestazione di collegamento al tuo progetto Swift:

	1. Fai clic con il pulsante destro del mouse sul tuo progetto in Xcode e seleziona **New File..**.
	1. Nella categoria **iOS Source**, fai clic su **Header file**. Denomina il file `BridgingHeader.h`.
	1. Aggiungi la seguente riga all'intestazione di collegamento: `#import <IMFCore/IMFCore.h>`
	1. Fai clic sul tuo progetto in Xcode e seleziona la scheda **Build Settings**.
	1. Cerca `Objective-C Bridging Header`.
	1. Imposta il valore sull'ubicazione del tuo file `BridgingHeader.h`, ad esempio `$(SRCROOT)/MyApp/BridgingHeader.h`.
	1. Assicurati che la tua intestazione di collegamento venga rilevata da Xcode compilando il tuo progetto. Non dovresti vedere alcun messaggio di errore.

1. Utilizza il seguente codice per inizializzare l'SDK client {{site.data.keyword.amashort}}.  Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `application:didFinishLaunchingWithOptions` del tuo delegato dell'applicazione. <br/>Sostituisci *applicationRoute* e *applicationGUID* con i valori da **Opzioni mobili** nel dashboard {{site.data.keyword.Bluemix_notm}}.

	**Objective-C:**

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	**Swift:**

	```Swift
IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",backendGUID: "applicationGUID")
	```

## Effettuazione di una richiesta al tuo backend mobile
{: #request}

Dopo che l'SDK client {{site.data.keyword.amashort}} è stato inizializzato, puoi iniziare a effettuare richieste al tuo backend mobile.

1. Prova a inviare una richiesta a un endpoint protetto sul tuo backend mobile nel tuo browser. Apri il seguente URL: `{applicationRoute}/protected`. Ad esempio: `http://my-mobile-backend.mybluemix.net/protected`
<br/>L'endpoint `/protected` di un backend mobile creato con il contenitore tipo MobileFirst Services Starter è protetto con {{site.data.keyword.amashort}}. Nel tuo browser viene restituito un messaggio `Unauthorized` perché a questo endpoint possono accedere solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}.

1. Utilizza la tua applicazione iOS per effettuare una richiesta allo stesso endpoint. Aggiungi il seguente codice dopo che hai inizializzato `IMFClient`:

	**Objective-C:**

	```Objective-C
	NSString *requestPath = [NSString stringWithFormat:@"%@/protected",
								[[IMFClient sharedInstance] backendRoute]];

	IMFResourceRequest *request =  [IMFResourceRequest requestWithPath:requestPath
																method:@"GET"];

	[request sendWithCompletionHandler:^(IMFResponse *response, NSError *error) {
		if (error){
			NSLog(@"Error :: %@", [error description]);
		} else {
			NSLog(@"Response :: %@", [response responseText]);
		}
	}];
	```

	**Swift:**

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
