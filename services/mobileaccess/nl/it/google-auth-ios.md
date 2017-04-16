---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-01"

---

{:screen: .screen}
{:shortdesc: .shortdesc}


# Abilitazione dell'autenticazione Google per le applicazioni Objective C iOS
{: #google-auth-ios}


Utilizza l'accesso Google per autenticare gli utenti nella tua applicazione iOS {{site.data.keyword.amafull}}.

**Nota:** mentre la SDK Objective-C SDK rimane completamente supportata ed è ancora considerata la SDK primaria per i servizi mobili {{site.data.keyword.Bluemix_notm}}, è pianificato di abbandonarla più avanti questo anno in favore della nuova SDK Swift. Per le nuove applicazioni consigliamo caldamente di utilizzare l'SDK Swift. Le istruzioni in questa pagina si applicano all'SDK Objective-C client {{site.data.keyword.amashort}}. Per istruzioni sull'utilizzo dell'SDK Swift, vedi [Abilitazione dell'autenticazione Google nelle applicazioni iOS (SDK Swift)](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html).

## Prima di cominciare
{: #before-you-begin}
È necessario disporre di:
* Un'istanza di un servizio {{site.data.keyword.amafull}} e di un'applicazione {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni su come creare un'applicazione di back-end {{site.data.keyword.Bluemix_notm}}, vedi [Introduzione](index.html).
* L'URL della tua applicazione di back-end (**Rotta applicazione**). Avrai bisogno di questo valore per inviare le richieste agli endpoint protetti della tua applicazione di back-end.
* Il tuo valore **TenantID**. Apri il tuo servizio nel dashboard {{site.data.keyword.amashort}}. Fai clic sul pulsante **Opzioni per dispositivi mobili**. Il valore `tenantId` (noto anche come `appGUID`)  viene visualizzato nel campo **GUID applicazione / TenantId**. Avrai bisogno di questo valore per inizializzare il gestore autorizzazione.

## Configurazione di un progetto Google per la piattaforma iOS
{: #google-auth-ios-project}
per iniziare a usare Google come provider di identità, crea un progetto nella Google Developer Console per ottenere un ID client Google.  Questo ID client è un identificativo univoco per consentire a Google di riconoscere l'applicazione che sta tentando di connettersi.   

1. Se non hai creato un progetto iOS Google, segui i passi nel sito [Google Developer Console](https://console.developers.google.com).

1. Dall'elenco **Social APIs**, scegli **Google+ API** e fai clic su **Enable**.

1. Dall'elenco **Credentials** fai clic sul pulsante **Create credentials** e scegli **OAuth client ID**.

1. A questo punto, ti verrà presentata una scelta del tipo di applicazione. Seleziona **iOS**.

1. Fornisci un nome significativo per il tuo client iOS. Specifica l'ID bundle della tua applicazione iOS. Per trovare l'ID bundle della tua applicazione iOS, cerca il **Bundle Identifier** nel file `info.plist` o nella scheda **General** del progetto Xcode.

1. Annota il tuo nuovo ID client iOS Google iOS. Questo valore ti servirà quando configuri l'applicazione in {{site.data.keyword.Bluemix}}.




## Configurazione di {{site.data.keyword.amashort}} per l'autenticazione Google
{: #google-auth-ios-config}

Ora che hai un ID client iOS, puoi abilitare l'autenticazione Google nel dashboard {{site.data.keyword.Bluemix_notm}}.

1. Apri il tuo servizio nel dashboard {{site.data.keyword.amashort}}.
1. Dalla scheda **Manage**, attiva **Authorization**.
1. Espandi la sezione **Google**.
1. In **Application ID for iOS**, specifica il tuo ID client Google per iOS.
1. Fai clic su **Save**.


## Configurazione dell'SDK client Google {{site.data.keyword.amashort}} per iOS
{: #google-auth-ios-sdk}

### Installazione dell'SDK client {{site.data.keyword.amashort}} utilizzando CocoaPods
{: #google-auth-ios-sdk-cocoapods}

1. Passa al tuo progetto iOS.

1. Modifica il `Podfile` per aggiungere la seguente riga:

	```
	pod 'IMFGoogleAuthentication'
	```
{: codeblock}

1. Salva il `Podfile` ed esegui `pod install` dalla riga di comando. CocoaPods installa le dipendenze. Vedrai lo stato di avanzamento e quali componenti sono stati aggiunti.

  **Importante**: devi ora aprire il tuo progetto utilizzando il file `xcworkspace` che viene generato da CocoaPods. Di norma, il
nome è `{il-tuo-nome-progetto}.xcworkspace`.  

1. Esegui `open {il-tuo-nome-progetto}.xcworkspace` dalla riga di comando per aprire il tuo spazio di lavoro del progetto iOS.

### Configurazione del progetto iOS per l'autenticazione Google
{: #google-auth-ios-googleauth}
Configura l'integrazione Google aggiornando il file `info.plist`. Il file `info.plist` si trova di norma nella cartella `Supporting files` nel tuo progetto Xcode. Puoi modificare il file nell'editor di elenchi di proprietà o con un editor di testo.

* Configura l'integrazione Google aggiungendo i seguenti schemi URL indicati di seguito al tuo file `info.plist`.
	![File info.plist](images/ios-google-infoplist-settings.png)

	Il primo schema URL è una versione invertita dell'ID client dalla Google Developer Console.  Ad esempio, se il tuo ID client è `123123-abcabc.apps.googleusercontent.com`, il tuo schema URL è: `com.googleusercontent.apps.123123-abcabc`.

	Il secondo schema URL è l'ID bundle della tua applicazione.

* Utilizza un editor di testo. Fai clic con il tasto destro del mouse su `info.plist` e seleziona **Open as > Source code**. Aggiungi il seguente XML al file:

	```XML
	<key>CFBundleURLTypes</key>
	<array>
		<dict>
			<key>CFBundleTypeRole</key>
			<string>Editor</string>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>com.googleusercontent.apps.123123-abcabc</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeRole</key>
			<string>Editor</string>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>com.ibm.HelloWorld</string>
			</array>
		</dict>
	</array>

	```
{: codeblock}

	Aggiorna entrambi gli schemi URL.

	**Importante**: non sovrascrivere alcuna proprietà esistente nel file `info.plist`. Se hai delle proprietà che si sovrappongono, dovrai unirle manualmente. Per ulteriori informazioni, vedi [Try Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start).

## Inizializzazione dell'SDK client {{site.data.keyword.amashort}}
{: #google-auth-ios-initialize}

Per utilizzare l'SDK client {{site.data.keyword.amashort}}, inizializzalo passando i parametri TenantID e App Route.

Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `application:didFinishLaunchingWithOptions` del tuo delegato dell'applicazione.

1. Importa i framework richiesti nella classe dove vuoi utilizzare l'SDK client {{site.data.keyword.amashort}}. Aggiungi le seguenti intestazioni:

	#### Objective-C:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```
{: codeblock}

	#### Swift:

	L'SDK client {{site.data.keyword.amashort}} viene implementato con Objective-C. Potesti dover aggiungere un'intestazione di collegamento al tuo progetto Swift per utilizzare l'SDK.

	1. Fai clic con il pulsante destro del mouse sul tuo progetto in Xcode e seleziona **New File...**.

	2. Nella categoria **iOS Source**, scegli **Header file**.

	3. Denominalo `BridgingHeader.h`.

	4. Aggiungi le seguenti importazioni alla tua intestazione di collegamento:
		
	   `#import <IMFCore/IMFCore.h>`
		
	   `#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>`
	
	5. Fai clic sul tuo progetto in Xcode e seleziona la scheda **Build Settings**.

	6. Cerca `Objective-C Bridging Header`.

	7. Imposta il valore sull'ubicazione del tuo file `BridgingHeader.h`, ad esempio `$(SRCROOT)/MyApp/BridgingHeader.h`.

	8. Assicurati che la tua intestazione di collegamento venga rilevata da Xcode compilando il tuo progetto.

3. Utilizza il seguente codice per inizializzare l'SDK client.  Sostituisci `<applicationRoute>` e `<TenantID>` con i tuoi **Route** e **TenantID**.

	#### Objective-C:

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"<applicationRoute>"
			backendGUID:@"<TenantID>"];
	```
{: codeblock}

	#### Swift:

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("<applicationRoute>",
	 							backendGUID: "<TenantID>")
	```
{: codeblock}

1. Inizializza `AuthorizationManager` trasmettendo al servizio  {{site.data.keyword.amashort}} il parametro `tenantId`. 
  ####Objective-C
	
  ```Objective-C
     [[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"tenantId"];
  ```
 {: codeblock}

  ####Swift

  ```Swift
  IMFAuthorizationManager.sharedInstance().initializeWithTenantId("tenantId")
  ```
 {: codeblock}

1. Registra il gestore autenticazione Google aggiungendo il seguente codice al metodo `application:didFinishLaunchingWithOptions` nel tuo delegato
dell'applicazione. Aggiungi questo codice subito dopo che hai inizializzato IMFClient.

	#### Objective-C:

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```
{: codeblock}

	#### Swift:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```
{: codeblock}

1. Aggiungi il seguente codice al tuo delegato dell'applicazione.

	#### Objective-C:

	```Objective-C
	- (void)applicationDidBecomeActive:(UIApplication *)application {
		[[IMFGoogleAuthenticationHandler sharedInstance] handleDidBecomeActive];
	}

	- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {

		BOOL shouldHandleGoogleURL = [GPPURLHandler handleURL:url sourceApplication:sourceApplication annotation:annotation];

		[[IMFGoogleAuthenticationHandler sharedInstance] handleOpenURL:shouldHandleGoogleURL];
		return  shouldHandleGoogleURL;
	}
	```
{: codeblock}

	#### Swift:

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		let shouldHandleGoogleURL = GPPURLHandler.handleURL(url,
				sourceApplication: sourceApplication, annotation: annotation)

		IMFGoogleAuthenticationHandler.sharedInstance().handleOpenURL(shouldHandleGoogleURL)

		return shouldHandleGoogleURL;
	}
```
{: codeblock}

## Verifica dell'autenticazione
{: #google-auth-ios-testing}
Dopo che l'SDK client è stato inizializzato, puoi iniziare a effettuare richieste al tuo backend mobile.

### Prima di cominciare
{: #google-auth-ios-testing-before}
Devi utilizzare il contenitore tipo {{site.data.keyword.mobilefirstbp}} e disporre già di una risorsa protetta da {{site.data.keyword.amashort}} all'endpoint `/protected`. Se devi configurare un endpoint `/protected`, consulta [Protezione delle risorse](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Prova a inviare una richiesta all'endpoint protetto del tuo backend mobile nel tuo browser desktop aprendo `{applicationRoute}/protected`, ad esempio `http://my-mobile-backend.mybluemix.net/protected`

1. L'endpoint `/protected` di un backend mobile creato con il contenitore tipo MobileFirst Services è protetto con {{site.data.keyword.amashort}}; pertanto, possono accedere ad esso solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}. Di conseguenza, vedrai `Unauthorized` nel tuo browser del desktop.

1. Utilizza la tua applicazione iOS per effettuare una richiesta allo stesso endpoint.

	#### Objective-C:

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
			NSLog(@"%@", [[IMFAuthorizationManager sharedInstance] userIdentity]);
		}
	}];
	```
{: codeblock}

	#### Swift:

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
{: codeblock}

1. Esegui la tua applicazione. Vedrai comparire una schermata di accesso Google

	![immagine](images/ios-google-login.png)

	Questa schermata può avere un aspetto lievemente differente se sul tuo dispositivo non è installata l'applicazione Facebook o se non sei attualmente collegato a Facebook.

1. Facendo clic su **OK**, stai autorizzando {{site.data.keyword.amashort}} a utilizzare la tua identità utente Google per scopi di autenticazione.

1. 	La tua richiesta dovrebbe avere esito positivo. Dovresti vedere il seguente output nel LogCat

	![immagine](images/ios-google-login-success.png)
		
	Puoi anche aggiungere la funzionalità di disconnessione aggiungendo il seguente codice:

	#### Objective C:

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] logout : callBack]
	```
{: codeblock}

	#### Swift:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().logout(callBack)
	```
{: codeblock}

	Se richiami questo codice dopo che un utente ha eseguito l'accesso con Google e l'utente prova ad eseguire nuovamente l'accesso, gli viene richiesto di autorizzare {{site.data.keyword.amashort}} a utilizzare Google per scopi di autenticazione. A tal punto, l'utente può fare clic sul nome utente <!--in the upper-right corner of the screen--> per selezionare, ed eseguire l'accesso con, un altro utente.

	Passare `callBack` alla funzione di disconnessione è facoltativo. Puoi anche passare `nil`.
