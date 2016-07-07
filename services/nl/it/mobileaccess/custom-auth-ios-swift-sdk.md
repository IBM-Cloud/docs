---

copyright:
  years: 2016

---

# Configurazione dell'SDK client {{site.data.keyword.amashort}} per iOS (SDK Swift)
{: #custom-ios}

Configura la tua applicazione iOS che sta utilizzando l'autenticazione personalizzata per utilizzare l'SDK client {{site.data.keyword.amashort}} e connetti la tua applicazione a {{site.data.keyword.Bluemix}}.  La nuova SDK Swift rilasciata {{site.data.keyword.amashort}} aggiunge e migliora le funzionalità fornite dalla SDK Objective-C Mobile Client Access esistente.

**Nota:** mentre la SDK Objective-C SDK rimane completamente supportata ed è ancora considerata la SDK primaria per i servizi mobili {{site.data.keyword.Bluemix_notm}}, è pianificato di abbandonarla più avanti questo anno in favore di questa nuova SDK Swift.

## Prima di cominciare
{: #before-you-begin}

Devi disporre di una risorsa che sia protetta da un'istanza del servizio {{site.data.keyword.amashort}} configurato per utilizzare un provider di identità personalizzato.  La tua applicazione mobile deve anche essere strumentata con l'SDK client {{site.data.keyword.amashort}}.  Per ulteriori informazioni, consulta:
 * [Introduzione a {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/index.html)
 * [Configurazione dell'SDK Swift iOS](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)
 * [Utilizzo di un provider di identità personalizzato](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Creazione di un provider di identità personalizzato](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configurazione di {{site.data.keyword.amashort}} per l'autenticazione personalizzata](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## Configurazione di {{site.data.keyword.amashort}} per l'autenticazione personalizzata
 {: #custom-auth-ios-configmca}

 1. Apri la tua applicazione nel dashboard {{site.data.keyword.Bluemix_notm}}.

 1. Fai clic su **Opzioni mobili** e annota **Rotta** (*applicationRoute*) e **GUID applicazione** (*applicationGUID*). Questi valori ti servono quando inizializzi l'SDK.

 1. Fai clic sul tile {{site.data.keyword.amashort}}. Il dashboard {{site.data.keyword.amashort}} viene caricato.

 1. Fai clic sul tile **Custom**.

 1. In **Realm name**, specifica la tua area di autenticazione personalizzata.

 1. In **URL**, specifica la tua applicationRoute.

 1. Fai clic su **Save**.




### Inizializzazione dell'SDK client
{: #custom-ios-sdk-initialize}

Inizializza l'SDK passando i parametri `applicationRoute` e `applicationGUID`. Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `application:didFinishLaunchingWithOptions` del tuo delegato dell'applicazione

1. Ottieni i valori di parametro della tua applicazione. Apri la tua applicazione nel dashboard {{site.data.keyword.Bluemix_notm}}. Fai clic su **Opzioni mobili**. I valori `applicationRoute` e `applicationGUID` sono visualizzati nei campi **Rotta** e **GUID applicazione**.

1. Importa i framework richiesti nella classe dove vuoi utilizzare l'SDK client {{site.data.keyword.amashort}}.

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
```

1. Inizializza l'SDK client {{site.data.keyword.amashort}}, modifica il gestore autorizzazione in modo che sia MCAAuthorizationManager e definisci un delegato di autenticazione e registralo. Sostituisci `<applicationRoute>` e `<applicationGUID>` con
i valori per **Rotta** e **GUID applicazione** che hai ottenuto da **Opzioni mobili** nel dashboard {{site.data.keyword.Bluemix_notm}}. 

  Sostituisci `<applicationBluemixRegion>` con la regione in cui è ospitata la tua applicazione {{site.data.keyword.Bluemix_notm}}. Per visualizzare la tua regione {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona viso (![Viso](/face.png "Viso")) nell'angolo in alto a sinistra del dashboard.

  Per `<yourProtectedRealm>`, utilizza il **Realm name** che hai definito nel tile **Custom** del dashboard {{site.data.keyword.amashort}}.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"
 let customRealm = "<yourProtectedRealm>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<applicationBluemixRegion>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

  //Delegato di autenticazione per gestire la richiesta di verifica personalizzata
 class MyAuthDelegate : AuthenticationDelegate {
      func onAuthenticationChallengeReceived(authContext: AuthenticationContext, challenge: AnyObject){
          print("onAuthenticationChallengeReceived")
              let answer = <An answer to the challenge sent by the backend (Should be of type [String:AnyObject])>
              authContext.submitAuthenticationChallengeAnswer(answer)
      }

      func onAuthenticationSuccess(info: AnyObject?) {
           print("onAuthenticationSuccess info = \(info)")
           print("onAuthenticationSuccess")
      }

      func onAuthenticationFailure(info: AnyObject?){
        print("onAuthenticationFailure info = \(info)")
        print("onAuthenticationFailure")
      }
  }

  let delegate = MyAuthDelegate()
  let mcaAuthManager = MCAAuthorizationManager.sharedInstance

 do {
      try mcaAuthManager.registerAuthenticationDelegate(delegate, realm: customRealm)
  } catch {
      print("error with register: \(error)")
  }
 return true
 }   
 ```

## Verifica dell'autenticazione
{: #custom-ios-testing}

Dopo che hai inizializzato l'SDK client e registrato un delegato di autenticazione personalizzato, puoi iniziare a effettuare richieste al tuo backend mobile.

### Prima di cominciare
{: #custom-ios-testing-before}

 Devi disporre di un'applicazione creata con il contenitore tipo {{site.data.keyword.mobilefirstbp}} e di una risorsa protetta da {{site.data.keyword.amashort}} all'endpoint `/protected`.

1. Invia una richiesta all'endpoint protetto del tuo backend mobile nel tuo browser aprendo `{applicationRoute}/protected`, ad esempio `http://my-mobile-backend.mybluemix.net/protected`.
  L'endpoint `/protected` di un backend mobile creato con il contenitore tipo {{site.data.keyword.mobilefirstbp}} è protetto con {{site.data.keyword.amashort}}. All'endpoint possono accedere solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}. Di conseguenza, nel tuo browser viene visualizzato un messaggio `Unauthorized`.

1. Utilizza la tua applicazione iOS per effettuare una richiesta allo stesso endpoint. Aggiungi il seguente codice dopo che hai inizializzato `BMSClient` e registrato il tuo delegato di autenticazione personalizzato:

 ```Swift
 let customResourceURL = "<il percorso della tua risorsa protetta>"
 let request = Request(url: customResourceURL, method: HttpMethod.GET)
 let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in
  if error == nil {
      print ("response:\(response?.responseText), no error")
  } else {
      print ("error: \(error)")
  }
 }

 request.sendWithCompletionHandler(callBack)
 ```

1. 	Quando la tua richiesta ha esito positivo, nella console Xcode vedi il seguente output:

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

1. Puoi anche aggiungere la funzionalità di disconnessione aggiungendo il seguente codice:

 ```
 MCAAuthorizationManager.sharedInstance.logout(callBack)
 ```  

 Se richiami questo codice dopo che un utente ha eseguito l'accesso, l'utente viene disconnesso. Quando l'utente prova ad eseguire nuovamente l'accesso, deve rispondere nuovamente alla richiesta di verifica proveniente dal server.

 Passare `callBack` alla funzione di disconnessione è facoltativo. Puoi anche passare `nil`.
