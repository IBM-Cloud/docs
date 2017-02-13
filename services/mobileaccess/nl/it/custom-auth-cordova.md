---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configurazione dell'autenticazione personalizzata per la tua applicazione Cordova {{site.data.keyword.amashort}}
{: #custom-cordova}

Strumentazione della tua applicazione Cordova per utilizzare l'autenticazione personalizzata e l'SDK client {{site.data.keyword.amafull}} per accedere alla tua applicazione protetta.

## Prima di cominciare
{: #before-you-begin}
* Una risorsa che sia protetta da un'istanza del servizio {{site.data.keyword.amashort}} configurata per utilizzare un provider di identità personalizzato (consulta [Configurazione dell'autenticazione personalizzata](custom-auth-config-mca.html)).  
* Il tuo valore **TenantID**. Apri il tuo servizio nel dashboard {{site.data.keyword.amashort}}. Fai clic sul pulsante **Opzioni per dispositivi mobili**. Il valore `tenantId` (noto anche come `appGUID`)  viene visualizzato nel campo **GUID applicazione / TenantId**. Avrai bisogno di questo valore per inizializzare il gestore autorizzazione.
* Il tuo nome **Realm**. Questo è il valore che hai specificato nel campo **Nome realm** della sezione **Personalizzato** nella scheda **Gestione** del dashboard {{site.data.keyword.amashort}}.
* La tua **Regione** {{site.data.keyword.Bluemix_notm}}. Puoi trovare la tua regione {{site.data.keyword.Bluemix_notm}} corrente nell'intestazione, accanto all'icona **Avatar** ![Icona Avatar](images/face.jpg "Icona Avatar"). Il valore che viene visualizzato della regione deve essere uno dei seguenti: `US South`, `United Kingdom` o `Sydney`. La sintassi esatta delle costanti SDK corrispondenti viene fornita negli esempi di codice.

Per ulteriori informazioni, consulta:

 * [Configurazione di {{site.data.keyword.amashort}} per l'autenticazione personalizzata](custom-auth-config-mca.html). Viene illustrato come configurare il servizio {{site.data.keyword.amashort}} per l'autenticazione personalizzata. Qui definisci il valore **Realm**.
 * [Configurazione dell'SDK Cordova](getting-started-cordova.html). Informazioni sulla configurazione dell'applicazione client Cordova.
 * [Utilizzo di un provider di identità personalizzato](custom-auth.html). Come autenticare gli utenti a un provider di identità personalizzato.
 * [Creazione di un provider di identità personalizzato](custom-auth-identity-provider.html). Alcuni esempi di come funziona un provider di identità personalizzato.

## Configura il tuo codice Cordova WebView
### Inizializzazione dell'SDK client {{site.data.keyword.amashort}} in Cordova WebView
{: #custom-cordova-sdk}
Inizializza l'SDK passando il parametro `<applicationBluemixRegion>` nel file `index.js`.

```JavaScript
BMSClient.initialize("<applicationBluemixRegion>");
```
{: codeblock}

Sostituisci `<applicationBluemixRegion>` con la tua regione (consulta [Prima di cominciare](#before-you-begin)).


### Interfaccia listener di autenticazione
{: #custom-cordva-auth}

L'SDK client {{site.data.keyword.amashort}} fornisce un'interfaccia listener di autenticazione per implementare un flusso di autenticazione personalizzato. Devi aggiungere i seguenti metodi che vengono richiamati in fasi diverse di un processo di autenticazione.

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...},
	onAuthenticationSuccess: function(info){...},
	onAuthenticationFailure: function(info){...}
}
```
{: codeblock}

Ciascun metodo gestisce una fase differente di un processo di autenticazione.

### Metodo onAuthenticationChallengeReceived
{: #onAuthenticationChallengeReceived}
Questo metodo viene richiamato quando viene ricevuta una richiesta di verifica dell'autenticazione personalizzata dal servizio {{site.data.keyword.amashort}}.
```JavaScript
onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...}
```
{: codeblock}

* `authenticationContext`: fornito dall'SDK client {{site.data.keyword.amashort}} per consentire allo sviluppatore di notificare a sua volta le risposte alle richieste di verifica dell'autenticazione oppure un errore durante la raccolta di credenziali, come ad esempio l'utente che annulla la richiesta di autenticazione.
* `challenge`: un oggetto JSON che contiene una richiesta di verifica dell'autenticazione personalizzata, come restituita da un provider di identità personalizzato.

Richiamando il metodo `onAuthenticationChallengeReceived`, l'SDK client {{site.data.keyword.amashort}} delega il controllo allo sviluppatore. {{site.data.keyword.amashort}} attende le credenziali. Lo sviluppatore deve raccogliere le credenziali e notificarle a sua volta all'SDK client {{site.data.keyword.amashort}} utilizzando uno dei seguenti metodi di interfaccia `authContext`.

```JavaScript
onAuthenticationSuccess: function(info){...}
```
{: codeblock}

Questo metodo viene richiamato dopo un'autenticazione con esito positivo. Gli argomenti includono un oggetto JSON facoltativo che contiene informazioni estese sull'esito positivo dell'autenticazione.

```JavaScript
onAuthenticationFailure: function(info){...}
```
{: codeblock}

Questo metodo viene richiamato dopo un esito negativo dell'autenticazione. Gli argomenti includono un oggetto JSON facoltativo che contiene informazioni estese sull'esito negativo dell'autenticazione.

### authenticationContext
{: #custom-cordova-authcontext}

Il valore `authenticationContext` viene fornito come un argomento al metodo `onAuthenticationChallengeReceived` di
un listener di autenticazione personalizzato. Lo sviluppatore deve raccogliere le credenziali e utilizzare i metodi `authenticationContext` per restituire le credenziali all'SDK client {{site.data.keyword.amashort}} o notificare un errore. Utilizza uno dei seguenti metodi:

```JavaScript
authenticationContext.submitAuthenticationChallengeAnswer(challengeAnswer);
```
{: codeblock}

```JavaScript
authenticationContext.submitAuthenticationFailure(info);
```
{: codeblock}

Il seguente codice illustra come un listener di autenticazione del cliente può raccogliere le credenziali, gestire le difficoltà e fornire le risposte di autenticazione.

## Implementazione di esempio di un flusso di lavoro del listener di autorizzazione personalizzato.
{: #custom-cordova-authlisten-sample}

Questo esempio di listener di autenticazione è progettato per funzionare con un provider di identità personalizzato. Puoi scaricare il provider di identità personalizzato da [questo repository Github![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "Icona link esterno"){: new_window}.

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {
		console.log("onAuthenticationChallengeReceived :: ", challenge);

		// In questo esempio, il listener di autenticazione restituisce immediatamente una
		// serie di credenziali codificata (hardcoded). In uno scenario realistico, questo è il punto
		// in cui lo sviluppatore mostra uno schermo di accesso, raccoglie le credenziali e richiama
		// l'API authenticationContext.submitAuthenticationChallengeAnswer()

		var challengeResponse = {
			username: "john.lennon",
			password: "12345"
		}

		authenticationContext.submitAuthenticationChallengeAnswer(challengeResponse);

		// Se si è verificato un errore di raccolta delle credenziali, devi
		// segnalarlo all'authenticationContext. In caso contrario, l'SDK client Mobile Client
		// Access resterà in uno stato di attesa delle credenziali
		// per sempre

	},

	onAuthenticationSuccess: function(info){
		console.log("onAuthenticationSuccess :: ", info);
	},

	onAuthenticationFailure: function(info){
		console.log("onAuthenticationFailure :: ", info);
	}
}
```
{: codeblock}

## Registrazione di un listener di autenticazione personalizzato in Cordova WebView
{: #custom-cordova-authreg}

Dopo che hai creato un listener di autenticazione personalizzato, devi eseguirne la registrazione presso `BMSClient` prima di poter iniziare a utilizzarlo. Aggiungi il seguente codice alla tua applicazione.  Richiama questo codice prima di
inviare richieste alle tue risorse protette.

```Java
BMSClient.registerAuthenticationListener(<realmName>, customAuthenticationListener);
```
{: codeblock}
 Utilizza il `realmName` che hai specifico nel dashboard {{site.data.keyword.amashort}}.

## Configura il gestore autorizzazione nel codice nativo

Il gestore autorizzazione {{site.data.keyword.amashort}} deve essere registrato nel tuo codice della piattaforma nativo.

**Android** (aggiungi a `onCreate` nell'attività principale)

```
String tenantId = "<tenantId>";
MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
```
{: codeblock}

**iOS Objective-C** (aggiungi a `AppDelegate.m`)

Registra il tuo gestore autorizzazione in base alla tua versione di Xcode.

```
#import "<your_module_name>-Swift.h"

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions

{  

    //[CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];
 }
```
{: codeblock}

Nota: per il nome del file di intestazione Swift corretto, sostituisci `your_module_name` con il nome modulo del tuo progetto, ad esempio, se il tuo nome modulo è `Cordova`, dovrebbe essere `#import "Cordova-Swift.h"`. Per trovare il nome modulo vai a **Build Settings > Packagin` > Product Module Name**.

**Nota:** sostituisci il tuo `tenantId` con l'ID tenant trovato nel pulsante **Opzioni mobili** nel dashboard del servizio {{site.data.keyword.amashort}}.


## Abilitare Keychain Sharing per iOS

Abilita `Keychain Sharing` andando alla scheda `Funzionalità` e passa `Keychain Sharing` su `Attivo` nel tuo progetto Xcode.


## Verifica dell'autenticazione
{: #custom-cordova-test}
Dopo che l'SDK client è stato inizializzato e che un `AuthenticationListener` personalizzato è stato registrato, puoi iniziare a effettuare richieste alla tua applicazione di back-end mobile.

### Prima di cominciare
{: #custom-cordova-testing-before}
Devi disporre di un'applicazione creata con il contenitore tipo {{site.data.keyword.mobilefirstbp}} e di una risorsa protetta da {{site.data.keyword.amashort}} all'endpoint `/protected`.


1. Invia una richiesta all'endpoint protetto della tua applicazione di back-end mobile nel tuo browser aprendo `{applicationRoute}/protected`, ad esempio `http://my-mobile-backend.mybluemix.net/protected`.
 L'endpoint `/protected` di un'applicazione di back-end mobile creato con il contenitore tipo {{site.data.keyword.mobilefirstbp}} è protetto con {{site.data.keyword.amashort}}. All'endpoint possono accedere solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}. Di conseguenza, nel tuo browser viene visualizzato un messaggio `Unauthorized`.

1. Utilizza la tua applicazione Cordova per effettuare una richiesta allo stesso endpoint. Aggiungi il seguente codice dopo che hai inizializzato `BMSClient` e registrato il tuo AuthenticationListener personalizzato.

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new BMSRequest("<your-application-route>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

	Sostituisci `<your-application-route>` con il tuo URL dell'applicazione di back-end (consulta [Prima di cominciare](#before-you-begin)).

1. 	Quando la tua richiesta ha esito positivo, nella console `LogCat` o Xcode è presente il seguente output:

	![immagine](images/android-custom-login-success.png)

	![immagine](images/ios-custom-login-success.png)
