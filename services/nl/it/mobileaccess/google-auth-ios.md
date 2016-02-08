# Abilitazione dell'autenticazione Google nelle applicazioni iOS
{: #google-auth-ios}

## Prima di cominciare
{: #google-auth-ios-before}
* Devi disporre di una risorsa protetta da {{site.data.keyword.amashort}} e di un progetto iOS strumentato con l'SDK client {{site.data.keyword.amashort}}. Per ulteriori informazioni, vedi [Introduzione a {{site.data.keyword.amashort}}](getting-started.html) e [Configurazione
dell'SDK iOS](getting-started-ios.html).
* Proteggi manualmente la tua applicazione di backend con l'SDK server {{site.data.keyword.amashort}}. Per ulteriori informazioni, vedi [Protezione delle risorse](protecting-resources.html).


## Configurazione di un progetto Google per la piattaforma iOS
{: #google-auth-ios-project}
per iniziare a usare Google come provider di identità, crea un progetto nella Google Developer Console per ottenere un ID client Google. Questo ID client è un identificativo univoco per consentire a Google di riconoscere l'applicazione che sta tentando di connettersi. Se già hai un progetto Google, puoi tralasciare i passi che descrivono la creazione del progetto e iniziare con l'aggiunta delle credenziali.

1. Apri la [Google Developers Console](https://console.developers.google.com).

1. Crea un progetto. Fai clic su **Create project**.

1. Seleziona il tuo progetto e fai clic su **Use Google APIs**. Puoi anche fare clic su **Enable APIs and get credentials like keys**.

1. Nell'elenco delle API, scegli l'API Google+ e fai clic su **Enable API**.

1. Fai clic su **Credentials > Add credentials** e seleziona **OAuth 2.0 client ID**.

1. Ti potrebbe essere chiesto di impostare un nome prodotto sulla console di consenso. Procedi ad eseguire tale operazione.

1. A questo punto, ti verrà presentata una scelta del tipo di applicazione. Seleziona **iOS**.

1. Fornisci un nome significativo per il tuo client iOS. Specifica il bundleId della tua applicazione iOS. Per trovare il bundleId della tua applicazione iOS, cerca il **Bundle Identifier** nel file `info.plist` o nella scheda **General** del progetto Xcode.

1. Annota il tuo nuovo ID client iOS. Questo valore ti servirà quando configuri l'applicazione in {{site.data.keyword.Bluemix_notm}}.


## Configurazione di {{site.data.keyword.amashort}} per l'autenticazione Google
{: #google-auth-ios-config}

Ora che hai un ID client iOS, puoi abilitare l'autenticazione Google nel dashboard {{site.data.keyword.Bluemix_notm}}.

1. Apri il dashboard {{site.data.keyword.Bluemix}} e fai clic sulla tua applicazione {{site.data.keyword.Bluemix_notm}}

1. Fai clic su **Opzioni mobili** e annota i valori *applicationRoute* e *applicationGUID*. Questi valori ti servono per inizializzare l'SDK.

1. Fai clic su un tile {{site.data.keyword.amashort}}

1. Raggiungerai il dashboard {{site.data.keyword.amashort}}

1. Fai clic su **Set up authentication**

1. Fai clic su **Google**

1. Specifica l'ID client per l'iOS ottenuto nei passi precedenti e fai clic su **Save**

## Configurazione dell'SDK client {{site.data.keyword.amashort}} per iOS
{: #google-auth-ios-sdk}

### Installazione dell'SDK client {{site.data.keyword.amashort}} utilizzando Cocoapods
{: #google-auth-ios-sdk-cocoapods}

1. Passa al tuo progetto iOS

1. Modifica il `Podfile` e aggiungi la riga qui di seguito alla destinazione richiesta

	```
	pod 'IMFGoogleAuthentication'
	```

1. Salva il `Podfile` ed esegui `pod install` dalla riga di comando

1. Cocoapods installerà le dipendenze aggiunte. Vedrai lo stato di avanzamento e quali componenti sono stati aggiunti.

	> Da questo punto in poi, dovrai sempre aprire il tuo progetto utilizzando un file xcworkspace generato da Cocoapods. Di norma il nome è {il-tuo-nome-progetto}.xcworkspace.  

1. Esegui `open {il-tuo-nome-progetto}.xcworkspace` dalla riga di comando per aprire il tuo spazio di lavoro del progetto iOS

### Configurazione del progetto iOS per l'autenticazione Google
{: #google-auth-ios-googleauth}

1. Trova il file `info.plist`, che di solito si trova nella cartella `Supporting files` nel tuo progetto Xcode

1. Configura l'integrazione Google aggiungendo i due schemi URL indicati di seguito al tuo file `info.plist`

	![immagine](images/ios-google-infoplist-settings.png)

	> Il primo schema URL è l'ID client inverso che hai ottenuto dalla Google Developer Console. Ad esempio, Se il tuo ID client è `123123-abcabc.apps.googleusercontent.com`, il tuo schema URL dovrebbe essere `com.googleusercontent.apps.123123-abcabc`

	> Il secondo schema URL è un ID bundle della tua applicazione

1. In alternativa, puoi aggiornare il file `info.plist` facendo clic con il pulsante destro del mouse su di esso, selezionando `Open as` -> `Source code` e aggiungendo il seguente XML

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
	> Aggiornare entrambi gli schemi URL come descritto in precedenza

	> Accertati di non sovrascrivere proprietà esistenti in `info.plist`. Se hai delle proprietà che si sovrappongono, dovrai unirle manualmente. Per
ulteriori informazioni, consulta la sezioni [Try Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start) della documentazione di Google.

## Inizializzazione dell'SDK client {{site.data.keyword.amashort}}
{: #google-auth-ios-initialize}

Per poter utilizzare l'SDK client {{site.data.keyword.amashort}}, devi inizializzarlo passando i parametri applicationGUID e applicationRoute.

> Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `application:didFinishLaunchingWithOptions` del tuo delegato dell'applicazione

1. Apri la pagina principale del dashboard {{site.data.keyword.Bluemix_notm}} e fai clic sull'applicazione creata in precedenza. Questo aprirà il tuo dashboard dell'applicazione di backend mobile.

2. Fai clic su `Opzioni mobili` nella parte superiore destra del dashboard. Verranno visualizzati i valori di rotta applicazione e GUID applicazione.

1. Importa il framework richiesto nella classe che desideri utilizzi l'SDK client {{site.data.keyword.amashort}} aggiungendo le seguenti intestazioni

	Applicazioni Objective-C:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```

	Applicazioni Swift:

	L'SDK client {{site.data.keyword.amashort}} viene implementato utilizzando Objective-C; potresti pertanto dover aggiungere un'intestazione di collegamento al tuo progetto swift per poterlo utilizzare.

	* Fai clic con il pulsante destro del mouse sul tuo progetto in Xcode e seleziona `New File...`
	* Nella categoria `iOS Source`, seleziona `Header file`
	* Denominalo `BridgingHeader.h`
	* Aggiungi le seguenti importazioni alla tua intestazione di collegamento

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```
	* Fai clic sul tuo progetto in Xcode e seleziona la scheda `Build Settings`
	* Cerca `Objective-C Bridging Header`
	* Imposta il valore sull'ubicazione del tuo file `BridgingHeader.h`, ad esempio: `$(SRCROOT)/MyApp/BridgingHeader.h`
	* Assicurati che la tua intestazione di collegamento venga rilevata da Xcode compilando il tuo progetto; non dovresti vedere alcun messaggio di errore

3. Utilizza il seguente codice per inizializzare l'SDK client>

	Applicazioni Objective-C:

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	Applicazioni Swift:

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```

	> Sostituisci applicationRoute e applicationGUID con i valori ottenuti da Opzioni mobili

1. Registra il gestore autenticazione Google aggiungendo il seguente codice al metodo `application:didFinishLaunchingWithOptions` nel tuo delegato
dell'applicazione. Ti consigliamo di eseguire questa operazione subito dopo che hai inizializzato l'IMFClient

	Applicazioni Objective-C:

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```

	Applicazioni Swift:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```

1. Aggiungi il seguente codice al tuo delegato dell'applicazione

	Applicazioni Objective-C:

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

	Applicazioni Swift:

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
Devi utilizzare il contenitore tipo {{site.data.keyword.mobilefirstbp}} e disporre già di una risorsa protetta da {{site.data.keyword.amashort}} all'endpoint `/protected`. Se devi configurare un endpoint `/protected`, consulta [Protezione delle risorse](protecting-resources.html).


1. Prova a inviare una richiesta all'endpoint protetto del tuo backend mobile nel tuo browser desktop aprendo `http://{appRoute}/protected`, ad esempio `http://my-mobile-backend.mybluemix.net/protected`

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
			NSLog("%@", IMFAuthorizationManager.sharedInstance().userIdentity)
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
