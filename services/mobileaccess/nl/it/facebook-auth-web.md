---

copyright:
  year: 2016, 2017
lastupdated: "2017-03-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

Il servizio {{site.data.keyword.amafull}} è stato sostituito con il servizio {{site.data.keyword.appid_full}}.

# Abilitazione dell'autenticazione Facebook per le applicazioni Web
{: #facebook-auth-web}

Utilizza Facebook per autenticare gli utenti alla tua applicazione Web {{site.data.keyword.amafull}}. Aggiungi la funzionalità di sicurezza {{site.data.keyword.amashort}}.

## Prima di cominciare
{: #facebook-auth-android-before}
È necessario disporre di:

* Un'applicazione Web.
* Un servizio {{site.data.keyword.amashort}}. Per ulteriori informazioni, vedi [Introduzione](index.html).
* L'URI Per il reindirizzamento finale (dopo il completamento del processo di autorizzazione).


## Configurazione di un'applicazione sul sito Facebook  for Developers
{: #facebook-auth-config}

Per utilizzare Facebook come provider di identità per il tuo sito web, devi aggiungere e impostare la piattaforma del sito web sull'applicazione Facebook.

1. Accedi al tuo account nel sito [Facebook for Developers](https://developers.facebook.com).
	Per informazioni sulla creazione di una nuova applicazione, consulta [Creazione di un'applicazione nel sito web Facebook for Developers](facebook-auth-overview.html#facebook-appID).
1. Prendi nota di **App ID** e **App Secret**. Avrai bisogno di questi valori quando configuri il tuo progetto Web per l'autenticazione Facebook nel dashboard Mobile Client Access.
1. Da **Products List**, scegli **Facebook Login**.
4. Aggiungi la piattaforma del **Web**, se non esiste.
6. Immetti l'endpoint di callback del server di autorizzazione nella casella **Valid OAuth redirect URIs**. Puoi aggiungere questo valore dopo aver configurato il tuo servizio {{site.data.keyword.amashort}} nelle seguenti istruzioni.
7. Salva le modifiche.


## Configurazione di {{site.data.keyword.amashort}} per l'autenticazione Facebook
{: #facebook-auth-config-ama}

Una volta che disponi del tuo ID applicazione Facebook e del segreto applicazione e la tua applicazione Facebook for Developers è stata configurata perché serva i client Web, puoi abilitare l'autenticazione Facebook nel dashboard {{site.data.keyword.amashort}}.

1. Apri il dashboard del servizio {{site.data.keyword.amashort}}.
1. Dalla scheda **Manage**, attiva **Authorization**.
1. Espandi la sezione **Facebook**.
1. Seleziona **Add Facebook to a Web App**.
5. Prendi nota del valore nella casella di testo **Mobile Client Access Redirect URI for Facebook for Developers**. Hai bisogno di questo valore da aggiungere alla casella **Valid OAuth redirect URIs** in **Facebook Login** del portale Facebook Developers.
6. Immetti il **App ID** e **App Secret** ottenuti dal sito web Facebook for Developers.
7. Immetti l'URI di reindirizzamento in **Your Web Application Redirect URIs**. Questo valore è per l'URI di reindirizzamento a cui accedere dopo che viene completato il processo di autorizzazione e viene determinato dallo sviluppatore.
8. Fai clic su **Save**.


## Implementazione del flusso dell'autorizzazione {{site.data.keyword.amashort}} utilizzando Facebook come provider di identità
{: #facebook-auth-flow}

La variabile di ambiente `VCAP_SERVICES` viene creata automaticamente per ogni istanza del servizio {{site.data.keyword.amashort}} e contiene le proprietà necessarie per il processo di autorizzazione. È formata da un oggetto JSON e può essere visualizzata nella scheda  **Service Credentials** nel dashboard del servizio {{site.data.keyword.amashort}}.

Per avviare il processo di autorizzazione:

1. Richiama l'endpoint di autorizzazione (`authorizationEndpoint`) e l'ID client (`clientId`) dalle credenziali del servizio archiviate nella variabile di ambiente `VCAP_SERVICES`.

	`var cfEnv = require("cfenv");`

	**Nota:** se hai aggiunto il servizio {{site.data.keyword.amashort}} prima dell'aggiunta del supporto Web potresti non avere l'endpoint token nelle **Service Credentials**. Invece, utilizza i seguenti URL, a seconda della tua regione {{site.data.keyword.Bluemix_notm}}:

	Stati Uniti Sud:

	`  https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization 
  `

	Londra:

	`  https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization 
  `

	Sydney:

	`  https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization 
  `

2. Crea l'URI del server dell'autorizzazione utilizzando `response_type("code")`, `client_id` e `redirect_uri` come parametri di query.

3. Vai dalla tua applicazione Web all'URI generato.

	Il seguente esempio richiama i parametri dalla variabile `VCAP_SERVICES`, creando l'URL e inviando la richiesta di reindirizzamento.

	```Java
  var cfEnv = require("cfenv");

	app.get("/protected", checkAuthentication, function(req, res, next){  
		res.send("Hello from protected endpoint"); 
  }
	);

	function checkAuthentication(req, res, next){
		// Controlla se l'utente è autenticato

		if (req.session.userIdentity){   
			next()  
     } else {
			// Se non lo è - reindirizza il server di autenticazione
			var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
			var authorizationEndpoint = mcaCredentials.authorizationEndpoint;
			var clientId = mcaCredentials.clientId;
			var redirectUri = "http://some-server/oauth/callback";
			// Il tuo URI di reindirizzamento dell'applicazione web   

			var redirectUrl = authorizationEndpoint + "?response_type=code";
        redirectUrl += "&client_id=" + clientId;   
        redirectUrl += "&redirect_uri=" + redirectUri;   

			res.redirect(redirectUrl);  
  
      }
	}
	```
	{: codeblock}

	Il parametro `redirect_uri` è l'URI per il reindirizzamento dopo l'esito positivo o negativo dell'autenticazione con Facebook.   

	Dopo il reindirizzamento dell'endpoint di autorizzazione l'utente visualizzerà un modulo
di accesso da Facebook. Dopo che Facebook autorizza l'identità dell'utente, il servizio {{site.data.keyword.amashort}} richiamerà il tuo URI di reindirizzamento dell'applicazione web fornendo il codice concesso come un parametro di query.  


## Ottenimento dei token
{: #facebook-auth-tokens}

Il passo successivo è quello di ottenere i token di accesso e di identità utilizzando il codice concesso ricevuto precedentemente:

1.  Richiama token `tokenEndpoint`, `clientId` e `secret` dalle credenziali del servizio archiviate nella variabile di ambiente `VCAP_SERVICES`.

	**Nota:** se utilizzi {{site.data.keyword.amashort}} prima dell'aggiunta del supporto web potresti non avere un endpoint token nelle credenziali del servizio. Invece, utilizza i seguenti URL, a seconda della tua regione Bluemix:

	Stati Uniti Sud:

	`     https://mobileclientaccess.ng.bluemix.net/oauth/v2/token   
 `

	Londra:

	`     https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token
 `

	Sydney:

	`     https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token
 `

2. Invia una richiesta POST all'URI del server del token con il tipo di concessione ("authorization_code"), `clientId` e il tuo URI di reindirizzamento come parametri del modulo. Invia `clientId` e `secret` come credenziali di autenticazione HTTP di base.

	Il seguente codice richiama i valori necessari e li invia con una richiesta POST:

	```Java
  var cfEnv = require("cfenv");
  var base64url = require("base64url ");
  var request = require('request');

	app.get("/oauth/callback", function(req, res, next){
		var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials; 
    var tokenEndpoint = mcaCredentials.tokenEndpoint; 
    var formData = {
			grant_type: "authorization_code",
      client_id: mcaCredentials.clientId,
      redirect_uri: "http://some-server/oauth/callback",   // Il tuo uri di reindirizzamento dell'applicazione web
      code: req.query.code
    }

  request.post({
			url: tokenEndpoint, 
    formData: formData 
    }, function (err, response, body){
			var parsedBody = JSON.parse(body); 
        req.session.accessToken = parsedBody.access_token; 
        req.session.idToken = parsedBody.id_token; 
        var idTokenComponents = parsedBody.id_token.split("."); // [header, payload, signature] 
			var decodedIdentity= base64url.decode(idTokenComponents[1]);
			req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"]; 
			res.redirect("/"); 
		}
		).auth(mcaCredentials.clientId, mcaCredentials.secret); 
  }
	);
	```
	{: codeblock}

	Tieni presente che il parametro `redirect_uri` deve corrispondere al `redirect_uri` utilizzato per la richiesta di autorizzazione precedente. Il parametro `code`  deve essere il codice concesso ricevuto nella risposta dalla richiesta di autorizzazione. Il codice è valido solo per 10 minuti, dopo i quali deve essere richiamato un nuovo codice..

	Il corpo della risposta conterrà l'ID del token e il codice di accesso in formato JWT (visita il [sito Web JWT ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://jwt.io/){: new_window}).

	Come hai ricevuto l'accesso e i token di identità, puoi indicare la sessione web come autenticata e facoltativamente conservare questi token.  

##Utilizzo dell'accesso ottenuto e del token di identità
{: #facebook-auth-using-token}

Il token di identità contiene informazioni sull'identità dell'utente. Nel caso dell'autenticazione Facebook, il token conterrà tutte le informazioni che l'utente ha deciso di condividere, come il nome completo, la fascia di età, l'url della foto del profilo, ecc.  

Il token di accesso abilita le comunicazioni con le risorse protette dai filtri di autorizzazione {{site.data.keyword.amashort}}, consulta [Protezione delle risorse](protecting-resources.html).

Per effettuare richieste che proteggano le risorse aggiungi un'intestazione dell'autorizzazione alle richieste con la seguente struttura:

`Authorization=Bearer <accessToken> <idToken>`

#### Suggerimenti
{: #tips}

* Il `accessToken` e il `idToken` devono essere separati da uno spazio vuoto.

* Il `idToken` è facoltativo. Se hai fornito il token di identità, è possibile accedere alla risorsa protetta ma non si riceveranno le informazioni sull'utente autorizzato.
