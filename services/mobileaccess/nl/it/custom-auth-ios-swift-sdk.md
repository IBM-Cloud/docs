---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-16"

---

{:codeblock:.codeblock}


# Configurazione dell'autenticazione personalizzata per la tua applicazione iOS (Swift SDK) {{site.data.keyword.amashort}}
{: #custom-ios}

Configura la tua applicazione iOS che sta utilizzando l'autenticazione personalizzata per utilizzare l'SDK client {{site.data.keyword.amafull}} e connetti la tua applicazione a {{site.data.keyword.Bluemix}}.  


## Prima di cominciare
{: #before-you-begin}

Prima di iniziare devi disporre di:

* Una risorsa che sia protetta da un'istanza del servizio {{site.data.keyword.amashort}} configurata per utilizzare un provider di identità personalizzato (consulta [Configurazione dell'autenticazione personalizzata](custom-auth-config-mca.html)).  
* Il tuo valore **TenantID**. Apri il tuo servizio nel dashboard {{site.data.keyword.amashort}}. Fai clic sul pulsante **Opzioni per dispositivi mobili**. Il valore `tenantId` (noto anche come `appGUID`)  viene visualizzato nel campo **GUID applicazione / TenantId**. Avrai bisogno di questo valore per inizializzare il gestore autorizzazione.
* Il tuo nome **Realm**. Questo è il valore che hai specificato nel campo **Nome realm** della sezione **Personalizzato** nella scheda **Gestione** del dashboard {{site.data.keyword.amashort}}.
* L'URL della tua applicazione di back-end (**Rotta applicazione**). Avrai bisogno di questo valore per inviare le richieste agli endpoint protetti della tua applicazione di back-end.
* La tua **Regione** {{site.data.keyword.Bluemix_notm}}. Puoi trovare la tua regione {{site.data.keyword.Bluemix_notm}} corrente nell'intestazione, accanto all'icona **Avatar** ![Icona Avatar](images/face.jpg "Icona Avatar"). Il valore della regione visualizzato deve essere uno dei seguenti: **Stati Uniti Sud**, **Regno Unito** o **Sydney**, e corrisponde alla costante richiesta nel codice:  `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` o `BMSClient.Region.sydney`.

Per ulteriori informazioni, consulta:
 * [Introduzione a {{site.data.keyword.amashort}}](index.html)
 * [Configurazione dell'SDK Swift iOS](getting-started-ios-swift-sdk.html)
 * [Utilizzo di un provider di identità personalizzato](custom-auth.html)
 * [Creazione di un provider di identità personalizzato](custom-auth-identity-provider.html)
 * [Configurazione di {{site.data.keyword.amashort}} per l'autenticazione personalizzata](custom-auth-config-mca.html)

### Abilitare Keychain Sharing per iOS
{: #enable_keychain}

Abilita `Keychain Sharing`. Vai alla scheda `Funzionalità` e passa `Keychain Sharing` su `Attivo` nel tuo progetto Xcode.


### Inizializzazione dell'SDK client
{: #custom-ios-sdk-initialize}

Inizializza l'SDK passando il parametro `applicationGUID` (**TenantId**). Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `application:didFinishLaunchingWithOptions` del tuo delegato dell'applicazione.

1. Importa i framework richiesti nella classe dove vuoi utilizzare l'SDK client {{site.data.keyword.amashort}}.

	```Swift
	import UIKit
	import BMSCore
	import BMSSecurity
	```
	{: codeblock}

1. Inizializza l'SDK client {{site.data.keyword.amashort}}, modifica il gestore autorizzazione in modo che sia  `MCAAuthorizationManager` e definisci un delegato di autenticazione e registralo.

```Swift

	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>
	let customRealm = "<yourProtectedRealm>"

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: 
		[UIApplicationLaunchOptionsKey: Any]?) -> Bool {

		let mcaAuthManager = MCAAuthorizationManager.sharedInstance
	    		mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
	 //regionName deve essere una della seguenti costanti BMSClient.Region: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom o BMSClient.Region.sydney
		BMSClient.sharedInstance.authorizationManager = mcaAuthManager

	//Delegato di autenticazione per gestire la richiesta di verifica personalizzata
 class MyAuthDelegate : AuthenticationDelegate {
		func onAuthenticationChallengeReceived(_ authContext: AuthenticationContext, challenge: AnyObject){
		    print("onAuthenticationChallengeReceived")
		    let answer = try? Utils.parseJsonStringtoDictionary( "{\"userName\":\"" + "test" + "\",\"password\":\"" + "test" + "\"}")
			authContext.submitAuthenticationChallengeAnswer(answer)
		}

		func onAuthenticationSuccess(_ info: AnyObject?) {
		    print("onAuthenticationSuccess info = \(info)")
           print("onAuthenticationSuccess")
      }

		func onAuthenticationFailure(_ info: AnyObject?){
		     print("onAuthenticationFailure info = \(info)")
        print("onAuthenticationFailure")
      }
	     }

	     let delegate = MyAuthDelegate()
	     mcaAuthManager.registerAuthenticationDelegate(delegate, realm: customRealm)

	     return true
 }


```
{: codeblock}

Nel codice:
* Sostituisci `MCAServiceTenantId` con il valore **TenantId** e `<applicationBluemixRegion>` con la tua **Regione** {{site.data.keyword.amashort}} (consulta [Prima di cominciare](##before-you-begin)).
* Utilizza il `realmName` che hai specifico nel dashboard {{site.data.keyword.amashort}} (consulta [Configurazione dell'autenticazione personalizzata](custom-auth-config-mca.html)).
* Sostituisci `<applicationBluemixRegion>` con la regione in cui è ospitata la tua applicazione {{site.data.keyword.Bluemix_notm}}. Per visualizzare la tua regione {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona Avatar ![icona Avatar](images/face.jpg "icona Avatar")  nella barra del menu per aprire il widget **Account e supporto**.  Il valore della regione visualizzato deve essere uno dei seguenti: **Stati Uniti Sud**, **Regno Unito** o **Sydney**, e corrisponde alla costante richiesta nel codice:  `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` o `BMSClient.Region.sydney`.


## Verifica dell'autenticazione
{: #custom-ios-testing}

Dopo che hai inizializzato l'SDK client e registrato un delegato di autenticazione personalizzato, puoi iniziare a effettuare richieste al tuo back-end mobile.

### Prima di cominciare
{: #custom-ios-testing-before}

 Devi disporre di un'applicazione creata con il contenitore tipo {{site.data.keyword.mobilefirstbp}} e di una risorsa protetta da {{site.data.keyword.amashort}} all'endpoint `/protected`.

1. Invia una richiesta all'endpoint protetto della tua applicazione di back-end mobile nel tuo browser aprendo `{applicationRoute}/protected`. Sostituisci   `{applicationRoute}` con il valore richiamato dalle **Opzioni mobili** (consulta [Configurazione di Mobile Client Access per l'autenticazione personalizzata](#custom-auth-ios-configmca)). Ad esempio `http://my-mobile-backend.mybluemix.net/protected`.

 L'endpoint `/protected` di un'applicazione di back-end mobile creato con il contenitore tipo {{site.data.keyword.mobilefirstbp}} è protetto con {{site.data.keyword.amashort}}. All'endpoint possono accedere solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}. Di conseguenza, nel tuo browser viene visualizzato un messaggio `Unauthorized`.

1. Utilizza la tua applicazione iOS per effettuare una richiesta allo stesso endpoint. Aggiungi il seguente codice dopo che hai inizializzato `BMSClient` e registrato il tuo delegato di autenticazione personalizzato:

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

1. Quando la tua richiesta ha esito positivo, nella console Xcode vedi il seguente output:

	 ```
	 onAuthenticationSuccess info = Optional({
     attributes =     {
	     };
     deviceId = don;
     displayName = "Don+Lon";
     isUserAuthenticated = 1;
     userId = don;
 })
	 response:Optional("Salve Don Lon"), no error
	 ```
	 {: codeblock}

1. Puoi anche aggiungere la funzionalità di disconnessione aggiungendo il seguente codice:

	 ```
	 MCAAuthorizationManager.sharedInstance.logout(callBack)
	 ```
	 {: codeblock}

 Se richiami questo codice dopo che un utente ha eseguito l'accesso, l'utente viene disconnesso. Quando l'utente prova ad eseguire nuovamente l'accesso, deve rispondere nuovamente alla richiesta di verifica proveniente dal server.

 Passare `callBack` alla funzione di disconnessione è facoltativo. Puoi anche passare `nil`.
