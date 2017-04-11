---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:pre: .pre}


# Configurazione dell'SDK Swift iOS
{: #getting-started-ios}

Crea le tue applicazioni Swift con l'SDK client {{site.data.keyword.appid_short}}, inizializza l'SDK, autentica gli utenti ed effettua le richieste alle risorse protette e non protette.
{:shortdesc}


## Prima di cominciare
{: #before-you-begin}

Hai bisogno delle seguenti informazioni:
  * Un'istanza di {{site.data.keyword.appid_short_notm}}.
  * Il tuo ID tenant.
    * Nella scheda **Credenziali del servizio** del tuo dashboard del servizio, fai clic su **Visualizza credenziali**. Il tuo ID Tenant viene visualizzato nel campo **ID tenant**. Questo valore viene utilizzato per inizializzare la tua applicazione.
  * La tua regione {{site.data.keyword.Bluemix_notm}}.
  Puoi trovare la tua regione cercando nella IU. Il valore viene utilizzato per inizializzare la tua applicazione.
    <table> <caption> Tabella 1. Regioni {{site.data.keyword.Bluemix_notm}} e valori SDK corrispondenti </caption>
    <tr>
      <th> Regione Bluemix </th>
      <th> Valore SDK </th>
    </tr>
    <tr>
      <td> Stati Uniti Sud </td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> Sydney </td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> Regno Unito </td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * Un progetto Xcode (versione 8.1 o superiore).
  * CocoaPods (versione 1.1.0 o superiore).


## Installazione dell'SDK client {{site.data.keyword.appid_short_notm}}
{: #install-appid-sdk}

L'SDK client {{site.data.keyword.appid_short_notm}} è distribuito con CocoaPods, un gestore dipendenze per i progetti Swift e Objective-C Cocoa. CocoaPods scarica le risorse utente e le rende disponibili al tuo progetto.

1. Crea un progetto Xcode oppure apri un progetto esistente.
2. Apri o crea il Podfile nella directory del progetto.
3. Nella tua destinazione del progetto, aggiungi una dipendenza per il pod 'BluemixAppID'. Assicurati che anche il comando `use_frameworks!` sia nella tua destinazione.

  Ad esempio:

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {:pre}

4. Per scaricare la dipendenza `BluemixAppID`, esegui il seguente comando:

  ```swift
  pod install --repo-update
  ```
  {:pre}

6. Apri il tuo progetto Xcode e abilita Keychain Sharing. In **Project Settings**, fai clic su **Capabilities** > **Keychain Sharing**.
7. In **Project Settings** > **Info** > **URL Types** aggiungi un tipo di URL. Riempi le caselle di testo **Identifier** e **URL Scheme** con questo valore: $(PRODUCT_BUNDLE_IDENTIFIER)


## Inizializzazione dell'SDK client {{site.data.keyword.appid_short_notm}}
{: #initialize-client-sdk}

1. Aggiungi la seguente importazione al tuo file `AppDelegate.swift`:

  ```swift
  import BluemixAppID
  ```
  {:pre}

2. Inizializza l'SDK client passando i parametri ID tenant e regione al metodo di inizializzazione. Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo application:didFinishLaunchingWithOptions: di AppDelegate nella tua applicazione Swift.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.Region_UK)
  ```
  {:pre}

  * Sostituisci ״tenantId״ con l'ID tenant per il tuo servizio ID applicazione.
  * Sostituisci AppID.REGION_UK con la tua regione {{site.data.keyword.appid_short_notm}}. 

3. Aggiungi il seguente codice al tuo file AppDelegate.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {:pre}

## Autentica gli utenti utilizzando il widget di accesso
{: #authenticate-login}

Dopo che l'SDK client {{site.data.keyword.appid_short_notm}} è stato inizializzato, puoi autenticare i tuoi utenti eseguendo il widget di accesso. La configurazione predefinita del widget di accesso utilizza Facebook, Google o entrambi come opzioni di autenticazione. Se configuri solo uno dei due, il widget di accesso non si avvia e l'utente viene reindirizzato alla schermata di autenticazione IDP configurata.



1. Aggiungi la seguente importazione al file in cui desideri utilizzare l'SDK.

  ```swift
  import BluemixAppID
  ```
  {:pre}

2. Esegui il seguente comando per avviare il widget.

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //Utente autenticato
      }

      public func onAuthorizationCanceled() {
          //Autenticazione annullata dall'utente
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Si è verificata un'eccezione
      }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {:pre}

## Accesso agli attributi dell'utente
{: #accessing}

Quando ottieni un token di accesso, è possibile ottenere l'accesso all'endpoint degli attributi protetti dell'utente. Questo viene fatto utilizzando i seguenti metodi API:

  ```swift
  func setAttribute(key: String, value: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func setAttribute(key: String, value: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)

  func getAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)

  func getAttributes(completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)

  func deleteAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  ```
  {:pre}

Quando il token di accesso non viene esplicitamente trasmesso, {{site.data.keyword.appid_short_notm}} utilizza l'ultimo token ricevuto.

Ad esempio, puoi richiamare questo codice per impostare un nuovo attributo o sovrascriverne uno esistente:

  ```swift
  AppID.sharedInstance.userAttributeManager?.setAttribute("key", "value", completionHandler: { (error, result) in
      if error = nil {
          //Attributi ricevuti come un dizionario
      } else {
          // Si è verificato un errore
      }
  })
  ```
  {:pre}


### Accesso anonimo
{: #anonymous notoc}

Con {{site.data.keyword.appid_short_notm}} puoi accedere in modo anonimo, consulta [identità anonima](/docs/services/appid/user-profile.html#anonymous).

  ```swift
  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //Utente autenticato
      }

      public func onAuthorizationCanceled() {
          //Autenticazione annullata dall'utente
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Si è verificato un errore
      }
   }

  AppID.sharedInstance.loginAnonymously( authorizationDelegate: delegate())
  ```
  {:pre}

### Autenticazione progressiva
{: #progressive notoc}

Quando ospiti un token di accesso anonimo, l'utente può essere identificato trasmettendolo al metodo loginWidget.launch:

  ```swift
  func launch(accessTokenString: String? , delegate: AuthorizationDelegate)
  ```
  {:pre}

Dopo un accesso anonimo, si verifica l'autenticazione progressiva anche se il widget di accesso viene richiamato trasmettendo un token di accesso, perché il servizio ha utilizzato l'ultimo token ricevuto. Se desideri cancellare i tuoi token memorizzati, esegui il seguente comando:

  ```swift
  var appIDAuthorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)
  appIDAuthorizationManager.clearAuthorizationData()
  ```
  {:pre}



## Fasi successive
{: #next-steps}

{{site.data.keyword.appid_short_notm}} fornisce una configurazione predefinita quando configuri per la prima volta i tuoi provider di identità. Puoi utilizzare la configurazione predefinita solo nella modalità di sviluppo. Prima di pubblicare la tua applicazione, aggiorna la configurazione [Facebook](/docs/services/appid/identity-providers.html#facebook) e [Google](/docs/services/appid/identity-providers.html#google) predefinita con le tue proprie credenziali.
