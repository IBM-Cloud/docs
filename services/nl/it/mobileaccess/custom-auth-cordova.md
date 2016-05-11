---

copyright:
  years: 2015, 2016

---

# Configurazione dell'SDK client {{site.data.keyword.amashort}} per Cordova
{: #custom-cordova}
Configura la tua applicazione Cordova che sta utilizzando l'autenticazione personalizzata per utilizzare l'SDK client {{site.data.keyword.amashort}} e connettere la tua applicazione a {{site.data.keyword.Bluemix}}.


## Prima di cominciare
{: #before-you-begin}
Devi disporre di una risorsa che sia protetta da un'istanza del servizio {{site.data.keyword.amashort}} configurato per utilizzare un provider di identità personalizzato.  La tua applicazione mobile deve anche essere strumentata con l'SDK client {{site.data.keyword.amashort}}.  Per ulteriori informazioni, consulta:
 * [Introduzione a {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Configurazione dell'SDK Cordova](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)
 * [Utilizzo di un provider di identità personalizzato](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Creazione di un provider di identità personalizzato](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configurazione di {{site.data.keyword.amashort}} per l'autenticazione personalizzata](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)

## Inizializzazione dell'SDK client {{site.data.keyword.amashort}}
{: #custom-cordova-sdk}
Inizializza l'SDK passando i parametri applicationGUID e applicationRoute.

1. Ottieni i valori di parametro della tua applicazione. Apri la tua applicazione nel dashboard {{site.data.keyword.Bluemix_notm}}. Fai clic su **Opzioni mobili**. Vengono visualizzati i valori di **Rotta** (`applicationRoute`) e **GUID applicazione** (`applicationGUID`).
1. Inizializza l'SDK client.

	```JavaScript
	BMSClient.initialize(applicationRoute, applicationGUID);

	```
 Sostituisci *applicationRoute* e *applicationGUID* con i valori di **Rotta** e **GUID applicazione** dal
pannello **Opzioni mobili** della tua applicazione sul dashboard {{site.data.keyword.Bluemix_notm}}.

## Interfaccia listener di autenticazione
{: #custom-cordva-auth}

L'SDK client {{site.data.keyword.amashort}} fornisce un'interfaccia listener di autenticazione per implementare un flusso di autenticazione personalizzato. Devi aggiungere i seguenti metodi che vengono richiamati in fasi diverse di un processo di autenticazione.

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...},
	onAuthenticationSuccess: function(info){...},
	onAuthenticationFailure: function(info){...}
}
```

Ciascun metodo gestisce una fase differente di un processo di autenticazione.

### Metodo onAuthenticationChallengeReceived
{: #onAuthenticationChallengeReceived}
Questo metodo viene richiamato quando viene ricevuta una richiesta di verifica dell'autenticazione personalizzata dal servizio {{site.data.keyword.amashort}}.
```JavaScript
onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...}
```

#### Argomenti
{: #onAuthenticationChallengeReceived-args}
* `authenticationContext`: fornito dall'SDK client {{site.data.keyword.amashort}} per consentire allo sviluppatore di notificare a sua volta le risposte alle richieste di verifica dell'autenticazione oppure un errore durante la raccolta di credenziali, come ad esempio l'utente che annulla la richiesta di autenticazione.
* `challenge`: un oggetto JSON che contiene una richiesta di verifica dell'autenticazione personalizzata, come restituita da un provider di identità personalizzato.

Richiamando il metodo `onAuthenticationChallengeReceived`, l'SDK client {{site.data.keyword.amashort}} delega il controllo allo sviluppatore. {{site.data.keyword.amashort}} attende le credenziali. Lo sviluppatore deve raccogliere le credenziali e notificarle a sua volta all'SDK client {{site.data.keyword.amashort}} utilizzando uno dei seguenti metodi di interfaccia `authContext`.

```JavaScript
onAuthenticationSuccess: function(info){...}
```

Questo metodo viene richiamato dopo un'autenticazione con esito positivo. Gli argomenti includono un JSONObject facoltativo che contiene informazioni estese sull'esito positivo dell'autenticazione.

```JavaScript
onAuthenticationFailure: function(info){...}
```

Questo metodo viene richiamato dopo un esito negativo dell'autenticazione. Gli argomenti includono un JSONObject facoltativo che contiene informazioni estese sull'esito negativo dell'autenticazione.

## authenticationContext
{: #custom-cordova-authcontext}

Il valore `authenticationContext` viene fornito come un argomento al metodo `onAuthenticationChallengeReceived` di
un listener di autenticazione personalizzato. Lo sviluppatore deve raccogliere le credenziali e utilizzare i metodi `authenticationContext` per restituire le credenziali all'SDK client {{site.data.keyword.amashort}} o notificare un errore. Utilizza uno dei seguenti metodi:

```JavaScript
authenticationContext.submitAuthenticationChallengeAnswer(challengeAnswer);

authenticationContext.submitAuthenticationFailure(info);
```

## Implementazione di esempio di un listener di autenticazione personalizzato
{: #custom-cordova-authlisten-sample}

Questo esempio di listener di autenticazione è progettato per funzionare con un provider di identità personalizzato. Puoi scaricare il provider di
identità personalizzato da [questo repository Github](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample).

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
		// segnalarlo all'authenticationContext. In caso contrario, l'SDK Client Mobile Client
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

## Registrazione di un listener di autenticazione personalizzato
{: #custom-cordova-authreg}

Dopo che hai creato un listener di autenticazione personalizzato, eseguine la registrazione presso `BMSClient` prima di poter iniziare a utilizzarlo. Aggiungi il seguente codice alla tua applicazione.  Richiama questo codice prima di
inviare richieste alle tue risorse protette.

```Java
BMSClient.registerAuthenticationListener(realmName, customAuthenticationListener);
```
 Utilizza il *realmName* che hai specifico nel dashboard {{site.data.keyword.amashort}}.


## Verifica dell'autenticazione
{: #custom-cordova-test}
Dopo che l'SDK client è stato inizializzato e che un AuthenticationListener personalizzato è stato registrato, puoi iniziare a effettuare richieste al tuo backend mobile.

### Prima di cominciare
{: #custom-cordova-testing-before}
Devi disporre di un'applicazione creata con il contenitore tipo {{site.data.keyword.mobilefirstbp}} e di una risorsa protetta da {{site.data.keyword.amashort}} all'endpoint `/protected`.


1. Invia una richiesta all'endpoint protetto del tuo backend mobile nel tuo browser aprendo `{applicationRoute}/protected`, ad esempio `http://my-mobile-backend.mybluemix.net/protected`.
 L'endpoint `/protected` di un backend mobile creato con il contenitore tipo {{site.data.keyword.mobilefirstbp}} è protetto con {{site.data.keyword.amashort}}. All'endpoint possono accedere solo le applicazioni mobili strumentate con
l'SDK client {{site.data.keyword.amashort}}. Di conseguenza, nel tuo browser viene visualizzato un messaggio `Unauthorized`.

1. Utilizza la tua applicazione Cordova per effettuare una richiesta allo stesso endpoint. Aggiungi il seguente codice dopo che hai inizializzato `BMSClient` e registrato il tuo AuthenticationListener personalizzato.

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
	request.send(success, failure);
	```

1. 	Quando la tua richiesta ha esito positivo, nella console LogCat o Xcode è presente il seguente output:

	![immagine](images/android-custom-login-success.png)

	![immagine](images/ios-custom-login-success.png)
