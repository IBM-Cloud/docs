---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Abilitazione dell'autenticazione Facebook per le applicazioni iOS (SDK Swift)
{: #facebook-auth-ios}

Per utilizzare Facebook come un provider di identità nelle tue applicazioni iOS {{site.data.keyword.amafull}}, aggiungi e configura la piattaforma iOS per la tua applicazione Facebook.
{: shortdesc}

## Prima di cominciare
{: #before-you-begin}

È necessario disporre di

* Un'istanza di un servizio {{site.data.keyword.amafull}} e di un'applicazione {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni su come creare un'applicazione di back-end {{site.data.keyword.Bluemix_notm}}, vedi [Introduzione](index.html).
* L'URL della tua applicazione di back-end (**Rotta applicazione**). Avrai bisogno di questo valore per inviare le richieste agli endpoint protetti della tua applicazione di back-end.
* Il tuo valore **TenantID**. Apri il tuo servizio nel dashboard {{site.data.keyword.amashort}}. Fai clic sul pulsante **Opzioni per dispositivi mobili**. Il valore `tenantId` (noto anche come `appGUID`)  viene visualizzato nel campo **GUID applicazione / TenantId**. Avrai bisogno di questo valore per inizializzare il gestore autorizzazione.
* La tua **Regione** {{site.data.keyword.Bluemix_notm}}. Puoi trovare la tua regione {{site.data.keyword.Bluemix_notm}} corrente nell'intestazione, accanto all'icona **Avatar** ![Icona Avatar](images/face.jpg "Icona Avatar"). Il valore della regione visualizzato deve essere uno dei seguenti: `Stati Uniti Sud`, `Regno Unito` o `Sydney` e corrisponde ai valori SDK richiesti per la SDK Swift: `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` o `BMSClient.Region.sydney`. Avrai bisogno di questo valore per inizializzare il client {{site.data.keyword.amashort}}.
* Un progetto iOS configurato per lavorare con CocoaPods.  Per ulteriori informazioni, vedi **Installa CocoaPods** in  [Configurazione dell'SDK Swift iOS](getting-started-ios-swift-sdk.html).  
   **Nota:** non è necessario installare l'SDK {{site.data.keyword.amashort}} core prima di procedere.
* Un'applicazione Facebook sul sito Web [Facebook for Developers ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developers.facebook.com "Icona link esterno"){: new_window}.

**Importante:** non devi necessariamente installare separatamente l'SDK Facebook (`com.facebook.FacebookSdk`). L'SDK Facebook viene installato automaticamente con il seguente pod {{site.data.keyword.amashort}} `BMSFacebookAuthentication`. Puoi saltare il passo **Aggiungi l'SDK Facebook al tuo progetto Xcode** quando aggiungi o configuri la tua applicazione sul sito web Facebook for Developers.

## Configurazione della tua applicazione Facebook per la piattaforma iOS
{: #facebook-auth-ios-config}

Sul sito Facebook for Developers:

1. Accedi al tuo account in [Facebook for Developers ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developers.facebook.com "Icona link esterno"){: new_window}.

1. Assicurati che la piattaforma iOS sia stata aggiunta alla tua applicazione. Quando aggiungi o configuri la piattaforma iOS devi fornire il **bundleId** della tua applicazione iOS. Per trovare il **bundleId** della tua applicazione iOS, cerca il **Bundle Identifier**
nel file `info.plist` o nella scheda **General** del progetto Xcode.

  **Suggerimento:**: valuta l'abilitazione del suffisso di schema URL o di SSO (Single Sign On) se intendi utilizzare tali funzioni.

1. Fai clic su **Save Settings**.

## Configurazione di {{site.data.keyword.amashort}} per l'autenticazione Facebook
{: #facebook-auth-ios-configmca}

Dopo che hai configurato l'ID applicazione Facebook e la tua applicazione Facebook perché serva client iOS, puoi abilitare l'autenticazione Facebook nel tuo servizio {{site.data.keyword.amashort}}.

1. Apri il tuo servizio nel dashboard {{site.data.keyword.amashort}}.
1. Dalla scheda **Manage**, attiva **Authorization**.
1. Espandi la sezione **Facebook**.
1. Aggiungi l'**ID applicazione Facebook** e fai clic su **Salva**.

## Configurazione dell'SDK client {{site.data.keyword.amashort}} per iOS
{: #facebook-auth-ios-sdk}

### Installazione di CocoaPods
{: #install-cocoapods}

1. Apri il terminale ed esegui il comando **pod --version**. Se CocoaPods è installato, viene visualizzato il numero della versione. Puoi passare direttamente alla sezione successiva per l'installare l'SDK.

1. Se non hai CocoaPods installato, esegui:

   ```
   sudo gem install cocoapods
   ```
   {: codeblock}

Per ulteriori informazioni, visita il [sito Web CocoaPods![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cocoapods.org/ "Icona link esterno"){: new_window}.

### Installazione dell'SDK Swift client {{site.data.keyword.amashort}} con CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. Se non disponi di un `Podfile` nel tuo progetto iOS, esegui `pod init` per creare il file.

1. Modifica `Podfile` e aggiungi le seguenti righe:

   ```
   use_frameworks!
   pod 'BMSFacebookAuthentication'
   ```
   {: codeblock}

   **Nota:** se hai questa riga nel tuo file Pod: `pod 'BMSSecurity'`, la devi rimuovere. Il pod `BMSFacebookAuthentication` installa tutti i frameork necessari.

   **Suggerimento:** puoi aggiungere `use_frameworks!` alla tua destinazione Xcode invece di averlo nel Podfile.

1. Salva il `Podfile` ed esegui il comando `pod install` dalla riga di comando. CocoaPods installa le dipendenze. Vengono visualizzati lo stato di avanzamento e quali componenti sono stati aggiunti.

   **Importante**: devi ora aprire il tuo progetto utilizzando il file `xcworkspace` che viene generato da CocoaPods. Di norma, il
nome è `{il-tuo-nome-progetto}.xcworkspace`.  

1. Esegui `open {il-tuo-nome-progetto}.xcworkspace` dalla riga di comando per aprire il tuo spazio di lavoro del progetto iOS.

### Abilitare Keychain Sharing per iOS
{: #enable_keychain}

Abilita `Keychain Sharing`. Vai alla scheda `Funzionalità` e passa `Keychain Sharing` su `Attivo` nel tuo progetto Xcode.

### Configurazione del tuo progetto iOS per l'autenticazione Facebook
{: #facebook-auth-ios-configproject}

1. Trova il file `info.plist`, che di solito si trova nella cartella `Supporting files` nel tuo progetto Xcode.

1. Configura l'integrazione Facebook aggiungendo le seguenti proprietà al tuo file `info.plist`:

   ![immagine](images/ios-facebook-infoplist-settings.png)

   Aggiorna le proprietà schema URL e FacebookAppID con il tuo ID applicazione Facebook.

   Puoi anche aggiornare il file `info.plist` facendo clic con il pulsante destro del mouse su di esso, selezionando **Open as > Source Code** e aggiungendo il seguente XML:

   ```XML
   <key>CFBundleURLTypes</key>
   <array>
      <dict>
         <key>CFBundleURLSchemes</key>
         <array>
            <string>fb{your-facebook-application-id}</string>
         </array>
      </dict>
   </array>
   <key>FacebookAppID</key>
   <string>{your-facebook-application-id}</string>
   <key>FacebookDisplayName</key>
   <string>{your-faceebook-application-name}</string>
   <key>LSApplicationQueriesSchemes</key>
   <array>
      <string>fbauth</string>
      <string>fbauth2</string>
   </array>
   <key>NSAppTransportSecurity</key>
   <dict>
      <key>NSExceptionDomains</key>
      <dict>
         <key>facebook.com</key>
         <dict>
            <key>NSIncludesSubdomains</key>
            <true/>                
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
         </dict>
         <key>fbcdn.net</key>
         <dict>
            <key>NSIncludesSubdomains</key>
            <true/>
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
         </dict>
         <key>akamaihd.net</key>
         <dict>
            <key>NSIncludesSubdomains</key>
            <true/>
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
         </dict>
      </dict>
   </dict>
   ```
   {: codeblock}

   Aggiorna le proprietà `CFBundleURLSchemes` e `FacebookappID` con il tuo ID applicazione Facebook. Aggiorna `FacebookDisplayName` con il nome della tua applicazione Facebook.

   **Importante**: assicurati di non sovrascrivere alcuna proprietà esistente nel file `info.plist`. Se hai delle proprietà che si sovrappongono, devi unirle manualmente. Per ulteriori informazioni, vedi [Configure Xcode Project ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developers.facebook.com/docs/ios/getting-started/ "Icona link esterno"){: new_window} e [Preparing Your Apps for iOS9 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developers.facebook.com/docs/ios/ios9 "Icona link esterno"){: new_window}.

## Inizializzazione dell'SDK Swift client {{site.data.keyword.amashort}}
{: #facebook-auth-ios-initalize-swift}

Inizializza l'SDK client passando il parametro `tenantId`.

Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `application:didFinishLaunchingWithOptions` del tuo delegato dell'applicazione.

1. Importa il framework richiesto nella classe che desideri utilizzi l'SDK client {{site.data.keyword.amashort}} aggiungendo le seguenti intestazioni:

   ```swift
 import UIKit
 import BMSCore
 import BMSSecurity
   ```
   {: codeblock}

1. Inizializza l'SDK client.

   ```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

   func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: 
		[UIApplicationLaunchOptionsKey: Any]?) -> Bool {
      let mcaAuthManager = MCAAuthorizationManager.sharedInstance
      mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
      //the regionName should be one of the following: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney
      BMSClient.sharedInstance.authorizationManager = mcaAuthManager
      FacebookAuthenticationManager.sharedInstance.register()
   }
   ```
   {: codeblock}

   Nel codice:

   * Sostituisci `<applicationBluemixRegion>` con la regione in cui è ospitata la tua applicazione {{site.data.keyword.Bluemix_notm}}.
   * Sostituisci `tenantId` con il valore **TenantId/GUID applicazione**.

   Per ulteriori informazioni su questi valori, vedi [Prima di cominciare](#before-you-begin).

1. Segnala all'SDK Facebook l'attivazione dell'applicazione e registra il gestore autenticazione Facebook aggiungendo il seguente codice al
metodo `application:didFinishLaunchingWithOptions` nel tuo delegato dell'applicazione. Aggiungi questo codice dopo aver inizializzato l'istanza BMSClient e registrato Facebook come gestore autenticazione.

   ```Swift
  return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
   ```
   {: codeblock}

1. Copia il file `FacebookAuthenticationManager.swift` dai file di origine pod `BMSFacebookAuthentication` alla directory del tuo progetto.

1. Aggiungi il seguente codice al tuo delegato dell'applicazione.

   ```Swift
   func application(_ app: UIApplication,
      open url: URL,
      options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool{
         return FacebookAuthenticationManager.sharedInstance.onOpenURL(app, open: url, options: options)
      }
   ```
   {: codeblock}

## Verifica dell'autenticazione
{: #facebook-auth-ios-testing}

Dopo che l'SDK client è stato inizializzato e il gestore autenticazione Facebook è stato registrato, puoi iniziare a effettuare richieste alla tua applicazione di back-end mobile.

### Prima di cominciare
{: #facebook-auth-ios-testing-before}

Devi utilizzare il contenitore tipo {{site.data.keyword.mobilefirstbp}} e disporre già di una risorsa protetta da {{site.data.keyword.amashort}} all'endpoint `/protected`. Se devi configurare un endpoint `/protected`, consulta [Protezione delle risorse](protecting-resources.html).

1. Prova a inviare una richiesta all'endpoint protetto del backend mobile appena creato nel tuo browser. Apri il seguente URL: `{applicationRoute}/protected`, sostituendo `{applicationRoute}` con il valore richiamato dalle **Opzioni mobili** (consulta [Configurazione di Mobile Client Access per l'autenticazione Facebook](#facebook-auth-ios-configmca)).
Ad esempio: `http://my-mobile-backend.mybluemix.net/protected`
<br/>L'endpoint `/protected` di un'applicazione di back-end mobile creato con il contenitore tipo MobileFirst Services Starter è protetto con {{site.data.keyword.amashort}}. Nel tuo browser viene restituito un messaggio `Unauthorized`. Questo messaggio viene restituito perché a questo endpoint possono accedere solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}.

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

1. Esegui la tua applicazione. Viene visualizzata una schermata di accesso Facebook.

   ![immagine](images/ios-facebook-login.png)

   Questa schermata può avere un aspetto lievemente differente se non sei attualmente collegato a Facebook.

1. Fai clic su **OK** per autorizzare {{site.data.keyword.amashort}} a usare la tua identità utente Facebook per scopi di autenticazione.

1. 	Quando la tua richiesta ha esito positivo, nella console Xcode è visualizzato il seguente output:

   ```
   response:Optional("Salve, questa è una risorsa protetta dell'applicazione backend mobile!"), no error
   ```
   {: screen}

1. Puoi anche aggiungere la funzionalità di disconnessione aggiungendo il seguente codice:

   ```
   FacebookAuthenticationManager.sharedInstance.logout(callBack)
   ```
   {: codeblock}

   Se richiami questo codice dopo che un utente ha eseguito l'accesso con Facebook e l'utente prova ad eseguire nuovamente l'accesso, gli viene richiesto di autorizzare {{site.data.keyword.amashort}} a utilizzare Facebook per scopi di autenticazione.

   Per passare da un utente all'altro, è necessario richiamare questo codice e l'utente deve eseguire la disconnessione da Facebook nel suo browser.

   Passare `callBack` alla funzione di disconnessione è facoltativo. Puoi anche passare `nil`.
