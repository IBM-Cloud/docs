---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**Importante: il servizio {{site.data.keyword.amafull}} è stato sostituito con il servizio {{site.data.keyword.appid_full}}.**

# Abilitazione dell'autenticazione Google per le applicazioni iOS (SDK Swift)
{: #google-auth-ios}

Utilizza l'accesso Google per autenticare gli utenti nella tua applicazione Swift iOS {{site.data.keyword.amafull}}.


## Prima di cominciare
{: #before-you-begin}

È necessario disporre di:

* Un'istanza di un servizio {{site.data.keyword.amafull}} e di un'applicazione {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni su come creare un'applicazione di back-end {{site.data.keyword.Bluemix_notm}}, vedi [Introduzione](index.html).
* L'URL della tua applicazione di back-end (**Rotta applicazione**). Avrai bisogno di questo valore per inviare le richieste agli endpoint protetti della tua applicazione di back-end.
* Il tuo valore **TenantID**. Apri il tuo servizio nel dashboard {{site.data.keyword.amashort}}. Fai clic sul pulsante **Opzioni per dispositivi mobili**. Il valore `tenantId` (noto anche come `appGUID`)  viene visualizzato nel campo **GUID applicazione / TenantId**. Avrai bisogno di questo valore per inizializzare il gestore autorizzazione.
* La tua **Regione** {{site.data.keyword.Bluemix_notm}}. Puoi trovare la tua regione {{site.data.keyword.Bluemix_notm}} corrente nell'intestazione, accanto all'icona **Avatar** ![Icona Avatar](images/face.jpg "Icona Avatar"). Il valore della regione visualizzato deve essere uno dei seguenti: **Stati Uniti Sud**, **Regno Unito** o **Sydney**, e corrisponde ai valori richiesti nel codice:  `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` o `BMSClient.Region.sydney`.
* Un progetto iOS in Xcode. Non deve essere instrumentato con l'SDK client {{site.data.keyword.amashort}}.  


## Preparazione della tua applicazione per l'accesso Google
{: #google-sign-in-ios}

Prepara la tua applicazione per l'accesso Google attenendoti alle istruzioni fornite da Google in [Google Sign-In for iOS ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developers.google.com/identity/sign-in/ios/start-integrating){: new_window}.

Questo processo:

* prepara un nuovo progetto sul sito Google Developers,
* crea il file `GoogleService-Info.plist` e il valore `REVERSE_CLIENT_ID` da aggiungere al tuo progetto Xcode e
* crea l'**ID client Google** da aggiungere alla tua applicazione di back-end {{site.data.keyword.Bluemix_notm}}.

La seguente procedura ti fornisce una breve sintesi delle attività che devi eseguire per preparare la tua applicazione.

**Nota:** non è necessario aggiungere il CocoaPod Google Sign-In. L'SDK necessario viene aggiunta dal CocoaPod `BMSGoogleAuthentication`.

1. Prendi nota del **Bundle Identifier** nel tuo progetto Xcode dalla sezione **Identity** della scheda **General** della destinazione principale. Ne hai bisogno per creare il tuo progetto di accesso Google.

1. Crea un progetto per l'accesso Google per iOS sul [sito Google Developer ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developers.google.com/mobile/add?platform=ios){: new_window}.

1. Aggiungi l'API Google Sign-In API al tuo progetto.

1. Richiama il `GoogleService-Info.plist`.

   **Importante:** quando ottieni il file `GoogleService-Info.plist`, aprilo e annota il valore di `CLIENT_ID`. Hai bisogno di questo valore per configurare l'applicazione di back-end {{site.data.keyword.amashort}}.

1. Aggiungi il file `GoogleService-Info.plist` al tuo progetto Xcode. Per ulteriori informazioni, vedi [Add the configuration file to your project ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config){: new_window}.

1. Aggiorna gli schemi URL nel tuo progetto Xcode con il tuo `REVERSE_CLIENT_ID` e l'ID bundle. Per ulteriori informazioni, vedi [Add URL schemes to your project ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developers.google.com/identity/sign-in/ios/start-integrating#add_a_url_scheme_to_your_project){: new_window}.

1. Aggiorna il file `project-Bridging-Header.h` della tua applicazione con il seguente codice:

	```
	#import <Google/SignIn.h>
	```
	{: codeblock}

	Per ulteriori informazioni sull'aggiornamento del file di intestazione di collegamento, vedi [Enable sign-in ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in){: new_window}.

## Configurazione di Mobile Client Access per l'autenticazione Google
{: #google-auth-ios-config}

Ora che hai un ID client iOS, puoi abilitare l'autenticazione Google nel servizio {{site.data.keyword.amashort}}.

1. Apri il tuo servizio nel dashboard {{site.data.keyword.amashort}}.
1. Dalla scheda **Manage**, attiva **Authorization**.
1. Espandi la sezione **Google**.
1. In **Application ID for iOS**, specifica il valore `CLIENT_ID` che hai ottenuto dal file `GoogleService-Info.plist`.
1. Fai clic su **Save**.

## Configurazione dell'SDK client per iOS
{: #google-auth-ios-sdk}

### Installazione di CocoaPods
{: #install-cocoapods}

1. Apri il terminale ed esegui il comando **pod --version**. Se già hai CocoaPods installato, viene visualizzato il numero versione. Puoi passare direttamente alla sezione successiva per l'installare l'SDK.

1. Se non hai CocoaPods installato, esegui:

	```
	sudo gem install cocoapods
	```
	{: codeblock}

Per ulteriori informazioni, visita il [sito Web CocoaPods ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cocoapods.org/){: new_window}.

### Installazione dell'SDK Swift client {{site.data.keyword.amashort}} con CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. Se non disponi di un `Podfile` nel tuo progetto iOS, esegui `pod init` per creare il file.

1. Modifica `Podfile` e aggiungi le seguenti righe alla destinazione pertinente:

	```
	use_frameworks!
	pod 'BMSGoogleAuthentication'
	```
	{: codeblock}

	**Nota:** se hai già installato l'SDK core {{site.data.keyword.amashort}}, puoi rimuovere questa riga: `pod 'BMSSecurity'`. Il pod `BMSGoogleAuthentication` installa tutti i frameork necessari.

	**Suggerimento:** puoi aggiungere `use_frameworks!` alla tua destinazione Xcode invece di averlo nel Podfile.

1. Salva il `Podfile` ed esegui `pod install` dalla riga di comando. CocoaPods installa le dipendenze. Vedrai lo stato di avanzamento e quali componenti sono stati aggiunti.

	**Importante**: devi ora aprire il tuo progetto utilizzando il file `xcworkspace` che viene generato da CocoaPods. Di norma, il
nome è `{il-tuo-nome-progetto}.xcworkspace`.  

1. Esegui `open {il-tuo-nome-progetto}.xcworkspace` dalla riga di comando per aprire il tuo spazio di lavoro del progetto iOS.

1. Copia il file `GoogleAuthenticationManager.swift` dai file di origine pod `BMSGoogleAuthentication` alla directory del tuo progetto.

### Abilitare Keychain Sharing per iOS
{: #enable_keychain}

Abilita `Keychain Sharing`. Vai alla scheda `Funzionalità` e passa `Keychain Sharing` su `Attivo` nel tuo progetto Xcode.


## Inizializzazione dell'SDK Swift client {{site.data.keyword.amashort}}
{: #google-auth-ios-initialize}

Per utilizzare l'SDK client {{site.data.keyword.amashort}}, inizializzala passando il parametro `tenantID`.

Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `application:didFinishLaunchingWithOptions` del tuo delegato dell'applicazione.

1. Importa i framework richiesti nella classe dove vuoi utilizzare l'SDK client {{site.data.keyword.amashort}}. Aggiungi le seguenti intestazioni:

	```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: 
		[UIApplicationLaunchOptionsKey: Any]?) -> Bool {

		let mcaAuthManager = MCAAuthorizationManager.sharedInstance
		mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
		//the regionName should be one of the following: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney   
		BMSClient.sharedInstance.authorizationManager = mcaAuthManager
		GoogleAuthenticationManager.sharedInstance.register()
		return true
	}

	// [START openurl]
	    func application(_ application: UIApplication,
			     open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
			return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, sourceApplication: sourceApplication, annotation: annotation)
      }

	@available(iOS 9.0, *)
	func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any]) -> Bool {
		return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, options: options)
  }

	```
	{: codeblock}

	Nel codice:

      * Sostituisci  `<serviceTenantID>` con il valore richiamato dalle **Opzioni mobili**.
      * Sostituisci `<applicationBluemixRegion>` con la tua **Regione** {{site.data.keyword.Bluemix_notm}}.

	Per ulteriori informazioni su come ottenere questi valori consulta [Prima di cominciare](#before-you-begin).


## Verifica dell'autenticazione
{: #google-auth-ios-testing}

Dopo che l'SDK client è stato inizializzato e il gestore autenticazione Google è stato registrato, puoi iniziare a effettuare richieste alla tua applicazione di back-end mobile.

### Prima di cominciare
{: #google-auth-ios-testing-before}

Devi utilizzare il contenitore tipo {{site.data.keyword.mobilefirstbp}} e disporre già di una risorsa protetta da {{site.data.keyword.amashort}} all'endpoint `/protected`. Se devi configurare un endpoint `/protected`, consulta [Protezione delle risorse](protecting-resources.html).

1. Prova a inviare una richiesta all'endpoint protetto della tua applicazione di back-end mobile nel tuo browser desktop aprendo `{applicationRoute}/protected`.  Ad esempio `http://my-mobile-backend.mybluemix.net/protected`.

1. L'endpoint `/protected` di un'applicazione di back-end mobile creato con il contenitore tipo MobileFirst Services è protetto con {{site.data.keyword.amashort}}; pertanto, possono accedere ad esso solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}. Di conseguenza, vedrai `Unauthorized` nel tuo browser del desktop.

1. Utilizza la tua applicazione iOS per effettuare una richiesta allo stesso endpoint.

	```Swift
	let protectedResourceURL = "<your protected resource absolute path>"
	let request = Request(url: protectedResourceURL, method: HttpMethod.GET)

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

1. Esegui la tua applicazione. Vedrai comparire una schermata di accesso Google

 ![immagine](images/ios-google-login.png)

1. Quando esegui l'accesso e fai clic su **OK**, stai autorizzando {{site.data.keyword.amashort}} a utilizzare la tua identità utente Google per scopi di autenticazione.

1. La tua richiesta dovrebbe avere esito positivo. Il seguente output viene visualizzato nel log.

	```
	response:Optional("Salve, questa è una risorsa protetta dell'applicazione backend mobile!"), no error
	```
	{: screen}

1. Puoi anche aggiungere la funzionalità di disconnessione aggiungendo il seguente codice:

	```
	GoogleAuthenticationManager.sharedInstance.logout(callBack)
	```
	{: codeblock}

	Se richiami questo codice dopo che un utente ha eseguito l'accesso con Google e l'utente prova ad eseguire nuovamente l'accesso, gli viene richiesto di autorizzare {{site.data.keyword.amashort}} a utilizzare Google per scopi di autenticazione. A tal punto, l'utente può fare clic sul nome utente <!--in the upper-right corner of the screen--> per selezionare, ed eseguire l'accesso con, un altro utente.

	Passare `callBack` alla funzione di disconnessione è facoltativo. Puoi anche passare `nil`.
