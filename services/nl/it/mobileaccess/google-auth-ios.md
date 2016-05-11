---

copyright:
  years: 2015, 2016

---

# Abilitazione dell'autenticazione Google nelle applicazioni iOS
{: #google-auth-ios}

**Suggerimento:** se stai sviluppando la tua applicazione iOS in Swift, valuta l'utilizzo dell'SDK Swift client {{site.data.keyword.amashort}}. Le istruzioni in questa pagina si applicano all'SDK Objective-C client {{site.data.keyword.amashort}}. Per istruzioni sull'utilizzo dell'SDK Swift, vedi [Abilitazione dell'autenticazione Google nelle applicazioni iOS (SDK Swift)](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)

## Prima di cominciare
{: #google-auth-ios-before}
* Devi disporre di una risorsa protetta da {{site.data.keyword.amashort}} e di un progetto iOS strumentato con l'SDK client {{site.data.keyword.amashort}}.  Per ulteriori informazioni, vedi [Introduzione a {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) e [Configurazione dell'SDK Objective-C iOS](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html).  
* Proteggi manualmente la tua applicazione di backend con l'SDK server {{site.data.keyword.amashort}}. Per ulteriori informazioni, vedi [Protezione delle risorse](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


## Configurazione di un progetto Google per la piattaforma iOS
{: #google-auth-ios-project}
per iniziare a usare Google come provider di identità, crea un progetto nella Google Developer Console per ottenere un ID client Google.  Questo ID client è un identificativo univoco per consentire a Google di riconoscere l'applicazione che sta tentando di connettersi.   Se già hai un progetto Google, puoi tralasciare i passi che descrivono la creazione del progetto e iniziare con l'aggiunta delle credenziali.



1. Crea un progetto nella [Google Developers Console](https://console.developers.google.com).
Se già hai un progetto, puoi tralasciare i passi che descrivono la creazione del progetto e iniziare con l'aggiunta delle credenziali.
   1.    Apri il menu di nuovo progetto. 
         
         ![immagine](images/FindProject.jpg)

   2.    Fai clic su **Create a project**.
   
         ![immagine](images/CreateAProject.jpg)


1. Dall'elenco **Social APIs**, scegli **Google+ API**.

     ![immagine](images/chooseGooglePlus.jpg)

1. Fai clic su **Enable** nella schermata successiva.

1. Seleziona la scheda **Consent Screen** e fornisci il nome prodotto visualizzato agli utenti. Altri valori sono facoltativi. Fai clic su **Save**.

    ![immagine](images/consentScreen.png)
    
1. Dall'elenco **Credentials**, scegli l'ID client OAuth.

     ![immagine](images/chooseCredentials.png)
     


1. A questo punto, ti verrà presentata una scelta del tipo di applicazione. Seleziona **iOS**.

1. Fornisci un nome significativo per il tuo client iOS. Specifica l'ID bundle della tua applicazione iOS. Per trovare l'ID bundle della tua applicazione iOS, cerca il **Bundle Identifier** nel file `info.plist` o nella scheda **General** del progetto Xcode.

1. Annota il tuo nuovo ID client iOS. Questo valore ti servirà quando configuri l'applicazione in {{site.data.keyword.Bluemix}}.


## Configurazione di {{site.data.keyword.amashort}} per l'autenticazione Google
{: #google-auth-ios-config}

Ora che hai un ID client iOS, puoi abilitare l'autenticazione Google nel dashboard {{site.data.keyword.Bluemix_notm}}.

1. Apri la tua applicazione nel dashboard {{site.data.keyword.Bluemix_notm}}.

1. Fai clic su **Opzioni mobili** e annota la tua **Rotta** (`applicationRoute`) e il tuo **GUID applicazione** (`applicationGUID`). Questi valori ti servono quando inizializzi l'SDK.

1. Fai clic sul tile {{site.data.keyword.amashort}}. Il dashboard {{site.data.keyword.amashort}} viene caricato.

1. Fai clic sul tile **Google**.

1. In **Application ID for iOS**, specifica il tuo ID client per Android e fai clic su **Save**.

	Nota: oltre all'ID client Google, è necessario anche il valore invertito per la tua configurazione client (vedi di seguito). Per accedere a entrambi i valori, scarica il plist di esempio utilizzando l'icona di matita:
		![scarica file info.plist](images/download_plist.png)

## Configurazione dell'SDK client {{site.data.keyword.amashort}} per iOS
{: #google-auth-ios-sdk}

### Installazione dell'SDK client {{site.data.keyword.amashort}} utilizzando CocoaPods
{: #google-auth-ios-sdk-cocoapods}

1. Passa al tuo progetto iOS.

1. Modifica il `Podfile` per aggiungere la seguente riga:

	```
	pod 'IMFGoogleAuthentication'
	```

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

* Utilizza un editor di testo. Fai clic con il pulsante destro del mouse su `info.plist` e seleziona **Open as > Source code**. Aggiungi il seguente XML al file:

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
	Aggiorna entrambi gli schemi URL.

	**Importante**: non sovrascrivere alcuna proprietà esistente nel file `info.plist`. Se hai delle proprietà che si sovrappongono, dovrai unirle manualmente. Per ulteriori informazioni, vedi [Try Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start).

## Inizializzazione dell'SDK client {{site.data.keyword.amashort}}
{: #google-auth-ios-initialize}

Per utilizzare l'SDK client {{site.data.keyword.amashort}}, inizializzalo passando i parametri applicationGUID e applicationRoute.

Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `application:didFinishLaunchingWithOptions` del tuo delegato dell'applicazione.

1. Ottieni i valori applicationGUID e applicationRoute. Nel dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sulla tua applicazione. Fai clic su **Opzioni mobili**. Vengono visualizzati i valori di rotta applicazione e GUID applicazione.

1. Importa i framework richiesti nella classe dove vuoi utilizzare l'SDK client {{site.data.keyword.amashort}}. Aggiungi le seguenti intestazioni:

	Objective-C:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```

	Swift:

	L'SDK client {{site.data.keyword.amashort}} viene implementato con Objective-C. Potesti dover aggiungere un'intestazione di collegamento al tuo progetto Swift per utilizzare l'SDK.

	1. Fai clic con il pulsante destro del mouse sul tuo progetto in Xcode e seleziona **New File...**
	2. Nella categoria **iOS Source**, scegli **Header file**.
	3. Denominalo `BridgingHeader.h`
	4. Aggiungi le seguenti importazioni alla tua intestazione di collegamento:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```
	5. Fai clic sul tuo progetto in Xcode e seleziona la scheda **Build Settings**.
	6. Cerca `Objective-C Bridging Header`.
	7. Imposta il valore sull'ubicazione del tuo file `BridgingHeader.h`, ad esempio `$(SRCROOT)/MyApp/BridgingHeader.h`.
	8. Assicurati che la tua intestazione di collegamento venga rilevata da Xcode compilando il tuo progetto.

3. Utilizza il seguente codice per inizializzare l'SDK client.  Sostituisci i valori *applicationRoute* e *applicationGUID* con
i valori **Rotta** e **GUID applicazione** che hai ottenuto da **Opzioni mobili**.

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



1. Registra il gestore autenticazione Google aggiungendo il seguente codice al metodo `application:didFinishLaunchingWithOptions` nel tuo delegato
dell'applicazione. Aggiungi questo codice subito dopo che hai inizializzato IMFClient.

	Objective-C:

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```

	Swift:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```

1. Aggiungi il seguente codice al tuo delegato dell'applicazione.

	Objective-C:

	```Objective-C
	- (void)applicationDidBecomeActive:(UIApplication *)application {
		[[IMFGoogleAuthenticationHandler sharedInstance] handleDidBecomeActive];
	}

	- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url
					sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {

		BOOL shouldHandleGoogleURL = [GPPURLHandler handleURL:url sourceApplication:sourceApplication annotation:annotation];

		[[IMFGoogleAuthenticationHandler sharedInstance] handleOpenURL:shouldHandleGoogleURL];
		return  shouldHandleGoogleURL;
	}
	```

	Swift:

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		let shouldHandleGoogleURL = GPPURLHandler.handleURL(url,
				sourceApplication: sourceApplication, annotation: annotation)

		IMFGoogleAuthenticationHandler.sharedInstance().handleOpenURL(shouldHandleGoogleURL)

		return shouldHandleGoogleURL;
	}
```

## Verifica dell'autenticazione
{: #google-auth-ios-testing}
Dopo che l'SDK client è stato inizializzato, puoi iniziare a effettuare richieste al tuo backend mobile.

### Prima di cominciare
{: #google-auth-ios-testing-before}
Devi utilizzare il contenitore tipo {{site.data.keyword.mobilefirstbp}} e disporre già di una risorsa protetta da {{site.data.keyword.amashort}} all'endpoint `/protected`. Se devi configurare un endpoint `/protected`, consulta [Protezione delle risorse](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Prova a inviare una richiesta all'endpoint protetto del tuo backend mobile nel tuo browser desktop aprendo `{applicationRoute}/protected`, ad esempio `http://my-mobile-backend.mybluemix.net/protected`

1. L'endpoint `/protected` di un backend mobile creato con il contenitore tipo MobileFirst Services è protetto con {{site.data.keyword.amashort}}; pertanto, possono accedere ad esso solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}. Di conseguenza, vedrai `Unauthorized` nel tuo browser del desktop.

1. Utilizza la tua applicazione iOS per effettuare una richiesta allo stesso endpoint.

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

1. Esegui la tua applicazione. Vedrai comparire una schermata di accesso Google

	![immagine](images/ios-google-login.png)

	Questa schermata può avere un aspetto lievemente differente se sul tuo dispositivo non è installata l'applicazione Facebook o se non sei attualmente collegato a Facebook.

1. Facendo clic su **OK**, stai autorizzando {{site.data.keyword.amashort}} a utilizzare la tua identità utente Google per scopi di autenticazione.

1. 	La tua richiesta dovrebbe avere esito positivo. Dovresti vedere il seguente output nel LogCat

	![immagine](images/ios-google-login-success.png)
	
	
	Puoi anche aggiungere la funzionalità di disconnessione aggiungendo il seguente codice:
	
	Objective C:
	
	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] logout : callBack]
	```

	Swift:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().logout(callBack)
	```


	Se richiami questo codice dopo che un utente ha eseguito l'accesso con Google e l'utente prova ad eseguire nuovamente l'accesso, gli viene richiesto di autorizzare Mobile Client Access a utilizzare Google per scopi di autenticazione. A tal punto, l'utente può fare clic sul nome utente nell'angolo superiore destro dello schermo per selezionare, ed eseguire l'accesso con, un altro utente.

	Passare `callBack` alla funzione di disconnessione è facoltativo. Puoi anche passare `nil`.
