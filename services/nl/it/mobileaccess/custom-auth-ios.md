---

copyright:
  years: 2015, 2016

---

# Configurazione dell'SDK client {{site.data.keyword.amashort}} per iOS
{: #custom-ios}

Configura la tua applicazione iOS che sta utilizzando l'autenticazione personalizzata per utilizzare l'SDK client {{site.data.keyword.amashort}} e connetti la tua applicazione a {{site.data.keyword.Bluemix}}.

**Suggerimento:** se stai sviluppando la tua applicazione iOS in Swift, valuta l'utilizzo dell'SDK Swift client {{site.data.keyword.amashort}}. Le istruzioni in questa pagina si applicano all'SDK Objective-C client {{site.data.keyword.amashort}}. Per istruzioni sull'utilizzo dell'SDK Swift, vedi [Configurazione dell'SDK client {{site.data.keyword.amashort}} per iOS (SDK Swift)](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-ios-swift-sdk.html)

## Prima di cominciare
{: #before-you-begin}
Devi disporre di una risorsa che sia protetta da un'istanza del servizio {{site.data.keyword.amashort}} configurato per utilizzare un provider di identità personalizzato.  La tua applicazione mobile deve anche essere strumentata con l'SDK client {{site.data.keyword.amashort}}.  Per ulteriori informazioni, consulta:
 * [Introduzione a {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Configurazione dell'SDK Objective-C iOS](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html)
 * [Utilizzo di un provider di identità personalizzato](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Creazione di un provider di identità personalizzato](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configurazione di {{site.data.keyword.amashort}} per l'autenticazione personalizzata](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)



## Installazione dell'SDK client con CocoaPods
{: #custom-ios-sdk-cocoapods}
Utilizza il gestore dipendenze CocoaPods per installare l'SDK client {{site.data.keyword.amashort}}.

1. Apri il terminale e passa alla directory root del tuo progetto iOS.

1. Modifica il `Podfile` e aggiungi la seguente riga.

	```
	pod 'IMFCore'
	```

1. Dalla riga di comando, esegui `pod install`.
CocoaPods installa le dipendenze aggiunte. Vengono visualizzati lo stato di avanzamento e quali componenti sono stati aggiunti.

**Importante**: devi ora aprire il tuo progetto utilizzando un file xcworkspace che è stato generato da CocoaPods. Di norma, il
nome è `{il-tuo-nome-progetto}.xcworkspace`.

1. Esegui `open {il-tuo-nome-progetto}.xcworkspace` dalla riga di comando per aprire il tuo spazio di lavoro del progetto iOS.



### Inizializzazione dell'SDK client
{: #custom-ios-sdk-initialize}

Inizializza l'SDK passando i parametri di rotta (`applicationRoute`) e GUID (`applicationGUID`) dell'applicazione. Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `application:didFinishLaunchingWithOptions` del tuo delegato dell'applicazione

1. Ottieni i valori di parametro della tua applicazione. Apri la tua applicazione nel dashboard {{site.data.keyword.Bluemix_notm}}. Fai clic su **Opzioni mobili** per visualizzare i valori per **Rotta** (`applicationRoute`) e **GUID applicazione** (`applicationGUID`).

1. Importa il framework `IMFCore` nella classe che desideri utilizzi l'SDK client.

	Objective-C:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	```

	Swift:

	L'SDK client {{site.data.keyword.amashort}} viene implementato con Objective-C. Potesti dover aggiungere un'intestazione di collegamento al tuo progetto Swift per utilizzare l'SDK.

	* Fai clic con il pulsante destro del mouse sul tuo progetto in Xcode e seleziona **New File...**
	* Nella categoria **iOS Source**, scegli **Header file**. Denomina il file `BridgingHeader.h`.
	* Aggiungi `#import <IMFCore/IMFCore.h>` alla tua intestazione di collegamento.
	* Fai clic sul tuo progetto in Xcode e seleziona la scheda **Build Settings**.
	* Cerca `Objective-C Bridging Header`.
	* Imposta il valore sull'ubicazione del tuo file `BridgingHeader.h`, ad esempio: `$(SRCROOT)/MyApp/BridgingHeader.h`
	* Verifica che la tua intestazione di collegamento venga rilevata da Xcode compilando il tuo progetto.

1. Inizializza l'SDK client. Sostituisci applicationRoute e applicationGUID con i valori per **Rotta** (`applicationRoute`) e **GUID applicazione** (`applicationGUID`) che hai ottenuto da **Opzioni mobili**.

	Objective-C:

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	Swift:

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```


## Delegato IMFAuthenticationHandler
{: #custom-ios-sdk-authhandler}


L'SDK client {{site.data.keyword.amashort}} fornisce l'interfaccia `IMFAuthenticationHandler` per implementare un flusso di autenticazione personalizzato. L'`IMFAuthenticationHandler` espone tre metodi richiamati in fasi differenti del processo di autenticazione.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
 						didReceiveAuthenticationChallenge:(NSDictionary*)challenge;
```

Questo metodo viene richiamato quando viene ricevuta una richiesta di verifica dell'autenticazione personalizzata dal servizio {{site.data.keyword.amashort}}. Gli argomenti includono

* Il protocollo `IMFAuthenticationContext` viene fornito dall'SDK client {{site.data.keyword.amashort}} in modo che lo sviluppatore possa
a sua volta segnalare le risposte alle richieste di verifica dell'autenticazione oppure gli errori durante la raccolta di credenziali (ad es. l'utente ha annullato l'operazione)
* `NSDictionary` contenente una richiesta di verifica dell'autenticazione personalizzata come restituita da un provider di identità personalizzato

Richiamando il metodo `authenticationContext:didReceiveAuthenticationChallenge`, l'SDK client {{site.data.keyword.amashort}} sta
delegando il controllo allo sviluppatore e si sta mettendo in modalità di attesa di credenziali. È responsabilità dello sviluppatore raccogliere le credenziali e notificarle a sua volta all'SDK client {{site.data.keyword.amashort}} utilizzando uno dei metodi di protocollo `IMFAuthenticationContext` come sarà descritto qui di seguito.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationSuccess:(NSDictionary *)userInfo;
```

Questo metodo viene richiamato dopo un'autenticazione con esito positivo. Gli argomenti includono IMFauthenticationContext e un NSDictionary facoltativo che contiene informazioni estese sull'esito positivo dell'autenticazione.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationFailure:(NSDictionary*)userInfo;
```

Questo metodo viene richiamato dopo un errore di autenticazione. Gli argomenti includono IMFauthenticationContext e un NSDictionary facoltativo che contiene informazioni estese sull'esito negativo dell'autenticazione.

## Protocollo IMFAuthenticationContext
{: #custom-ios-sdk-authcontext}


`IMFAuthenticationContext` viene fornito come un argomento al metodo `authenticationContext:didReceiveAuthenticationChallenge` di un `IMFAuthenticationHandler` personalizzato. È responsabilità dello sviluppatore raccogliere credenziali e utilizzare
i metodi `IMFAuthenticationContext` per restituire credenziali all'SDK client {{site.data.keyword.amashort}} o notificare un errore. Utilizza uno dei seguenti metodi

```
-(void) submitAuthenticationChallengeAnswer:(NSDictionary*) answer;

-(void) submitAuthenticationFailure:(NSDictionary*) userInfo;
```

## Implementazione di esempio di un IMFAuthenticationDelegate personalizzato
{: #custom-ios-sdk-sample}


L'esempio IMFAuthenticationDelegate è progettato per funzionare con l'esempio di provider di identità personalizzato. Puoi scaricare
l'esempio dal [repository Github](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample).

Objective-C:

``` Objective-C
CustomAuthenticationDelegate.h
-----------------------------------
#import <Foundation/Foundation.h>

@import IMFCore;
@interface CustomAuthenticationDelegate : NSObject <IMFAuthenticationDelegate>
@end


CustomAuthenticationDelegate.m
-----------------------------------
#import "CustomAuthenticationDelegate.h"

@implementation CustomAuthenticationDelegate

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationChallenge:(NSDictionary *)challenge{

	NSLog(@"didReceiveAuthenticationChallenge :: %@", challenge);

	// In questo esempio, l'IMFAuthenticationDelegate restituisce immediatamente una
		// serie di credenziali codificata (hardcoded). In uno scenario realistico, questo è il punto
		// in cui lo sviluppatore mostra uno schermo di accesso, raccoglie le credenziali e richiama
	// l'API [context submitAuthenticationChallengeAnswer:]

	NSDictionary *challengeAnswer = [NSDictionary dictionaryWithObjectsAndKeys:
									 @"john.lennon", @"username",
									 @"12345", @"password", nil];

	[context submitAuthenticationChallengeAnswer:challengeAnswer];

	// Se si è verificato un errore di raccolta delle credenziali, devi
		// segnalarlo all'IMFAuthenticationContext. In caso contrario, l'SDK Client Mobile Client
		// Access resterà in uno stato di attesa delle credenziali
		// per sempre
}

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationSuccess:(NSDictionary *)userInfo{
	NSLog(@"didReceiveAuthenticationSuccess");


}

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationFailure:(NSDictionary *)userInfo{
	NSLog(@"didReceiveAuthenticationFailure");

}

@end
```

Implementazione Swift:

```Swift
import Foundation

class CustomAuthenticationDelegate : NSObject, IMFAuthenticationDelegate{

	func authenticationContext(context: IMFAuthenticationContext!,
					didReceiveAuthenticationChallenge challenge: [NSObject : AnyObject]!) {

		NSLog("didReceiveAuthenticationChallenge :: %@", challenge)

		// In questo esempio, l'IMFAuthenticationDelegate restituisce immediatamente una
		// serie di credenziali codificata (hardcoded). In uno scenario realistico, questo è il punto
		// in cui lo sviluppatore mostra uno schermo di accesso, raccoglie le credenziali e richiama
		// l'API context.submitAuthenticationChallengeAnswer()

		let challengeAnswer: [String:String] = [
			"username":"john.lennon",
			"password":"12345"
		]

		context.submitAuthenticationChallengeAnswer(challengeAnswer)

		// Se si è verificato un errore di raccolta delle credenziali, devi
		// segnalarlo all'IMFAuthenticationContext. In caso contrario, l'SDK Client Mobile Client
		// Access resterà in uno stato di attesa delle credenziali
		// per sempre
}


	func authenticationContext(context: IMFAuthenticationContext!,
					didReceiveAuthenticationSuccess userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationSuccess")
	}

	func authenticationContext(context: IMFAuthenticationContext!,
					didReceiveAuthenticationFailure userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationFailure")
	}
}
```

## Registrazione di un IMFAuthenticationDelegate personalizzato

Dopo che hai creato un IMFAuthenticationDelegate personalizzato, registralo presso `IMFClient`. Richiama il seguente codice nella tua applicazione prima di inviare richieste alle tue risorse protette. Utilizza il nome di area di autenticazione (realmName) che hai specificato nel dashboard {{site.data.keyword.amashort}}.

Applicazioni Objective-C:

```Objective-C
[[IMFClient sharedInstance]
				registerAuthenticationDelegate:[CustomAuthenticationDelegate new]
										forRealm:realmName];
```

Applicazioni Swift:
```Swift
IMFClient.sharedInstance().registerAuthenticationDelegate(CustomAuthenticationDelegate(),
									forRealm: realmName)
```




## Verifica dell'autenticazione
{: #custom-ios-testing}
Dopo che hai inizializzato l'SDK client e registrato un `IMFAuthenticationDelegate` personalizzato, puoi iniziare a effettuare richieste al tuo backend mobile.

### Prima di cominciare
{: #custom-ios-testing-before}
 Devi disporre di un'applicazione creata con il contenitore tipo {{site.data.keyword.mobilefirstbp}} e di una risorsa protetta da {{site.data.keyword.amashort}} all'endpoint `/protected`.

1. Invia una richiesta all'endpoint protetto del tuo backend mobile nel tuo browser aprendo `{applicationRoute}/protected`, ad esempio `http://my-mobile-backend.mybluemix.net/protected`.
  L'endpoint `/protected` di un backend mobile creato con il contenitore tipo {{site.data.keyword.mobilefirstbp}} è protetto con {{site.data.keyword.amashort}}. All'endpoint possono accedere solo le applicazioni mobili strumentate con
l'SDK client {{site.data.keyword.amashort}}. Di conseguenza, nel tuo browser viene visualizzato un messaggio `Unauthorized`.
1. Utilizza la tua applicazione iOS per effettuare una richiesta allo stesso endpoint. Aggiungi il seguente codice dopo aver inizializzato `BMSClient` e registrato il tuo `IMFAuthenticationDelegate` personalizzato:

	Objective-C:

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
			NSLog(@"%@", [[IMFAuthorizationManager sharedInstance] userIdentity]);
		}
	}];
	```

	Swift:

	```Swift
	let requestPath = IMFClient.sharedInstance().backendRoute + "/protected"

	let request = IMFResourceRequest(path: requestPath, method: "GET");
	request.sendWithCompletionHandler { (response, error) -> Void in
		if (nil != error){
			NSLog("Error :: %@", error.description)
		} else {
			NSLog("Response :: %@", response.responseText)
			NSLog("%@", IMFAuthorizationManager.sharedInstance().userIdentity)
		}
	};

	```
1. 	Quando la tua richiesta ha esito positivo, nella console Xcode vedi il seguente output:

	![immagine](images/ios-custom-login-success.png)
	
	
	
	Puoi anche aggiungere la funzionalità di disconnessione aggiungendo il seguente codice:

	Objective C: 

	```Objective-C
	[[IMFAuthorizationManager sharedInstance] logout : callBack]
	```
	Swift: 

	```Swift
	IMFAuthorizationManager.sharedInstance().logout(callBack)
	```

Se richiami questo codice dopo che un utente ha eseguito l'accesso, l'utente viene disconnesso. Quando l'utente prova ad eseguire nuovamente l'accesso, deve rispondere nuovamente alla richiesta di verifica proveniente dal server.
Passare `callBack` alla funzione di disconnessione è facoltativo. Puoi anche passare `nil`.

