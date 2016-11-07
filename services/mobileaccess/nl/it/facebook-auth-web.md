---

copyright:
  year: 2016
lastupdated: "2016-10-03"

---
{:screen: .screen}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}


# Abilitazione dell'autenticazione Facebook per le applicazioni web
{: #facebook-auth-web}

Utilizza Facebook per autenticare gli utenti alla tua applicazione web {{site.data.keyword.amafull}}. Aggiungi la funzionalità di sicurezza {{site.data.keyword.amashort}}. 

## Prima di cominciare
{: #facebook-auth-android-before}
È necessario disporre di:

* Un'applicazione web. 
* Un'istanza di un'applicazione  {{site.data.keyword.Bluemix_notm}} che è protetta da un servizio {{site.data.keyword.amashort}}. Per ulteriori informazioni su come creare un'applicazione di back-end {{site.data.keyword.Bluemix_notm}}, vedi [Introduzione](index.html).
* L'URI Per il reindirizzamento finale (dopo il completamento del processo di autorizzazione).


## Configurazione di un'applicazione Facebook per il tuo sito web
{: #facebook-auth-config}

Per utilizzare Facebook come provider di identità per il tuo sito web, devi aggiungere e impostare la piattaforma del sito web sull'applicazione Facebook.

1. Accedi al sito web [Facebook for Developers](https://developers.facebook.com).
2. Apri o crea la tua applicazione.
3. Prendi nota di **App ID** e **App Secret**. Avrai bisogno di questi valori quando configuri il tuo progetto web per l'autenticazione Facebook nel dashboard {{site.data.keyword.amashort}}.
4. Aggiungi la piattaforma del **Website**, se non esiste.
5. Aggiungi o apri **Facebook Login** dall'elenco **Products**.
6. Immetti l'endpoint di callback del server di autorizzazione nella casella **Valid OAuth redirect URIs**. Trova questo URI di reindirizzamento dell'autorizzazione nei seguenti passi di configurazione del dashboard {{site.data.keyword.amashort}}.
7. Salva le modifiche.


## Configurazione di {{site.data.keyword.amashort}} per l'autenticazione Facebook
{: #facebook-auth-config-ama}

Una volta che disponi del tuo ID applicazione Facebook e del segreto applicazione e la tua applicazione Facebook è stata configurata perché serva i client web, puoi abilitare l'autenticazione Facebook nel dashboard  {{site.data.keyword.Bluemix_notm}}. 

1. Apri il dashboard {{site.data.keyword.Bluemix_notm}}.
2. Fai clic sul tile dell'applicazione pertinente per caricarla.
3. Fai clic sul tile per il servizio {{site.data.keyword.amashort}}.
4. Fai clic sul pulsante **Configura** nel pannello **Facebook**.
5. Prendi nota del valore nella casella di testo **Mobile Client Access Redirect URI for Facebook Developer Console**. Hai bisogno di questo valore da aggiungere alla casella **Valid OAuth redirect URIs** in **Facebook Login** del portale Facebook Developers nel passo sei della configurazione di un'applicazione Facebook per il tuo sito web.
6. Immetti **Application ID** e **App Secret** di Facebook.
7. Immetti l'URI di reindirizzamento in **Your Web Application Redirect URIs**. Questo valore è per l'URI di reindirizzamento a cui accedere dopo che viene completato il processo di autorizzazione e viene determinato dallo sviluppatore.
8. Fai clic su **Save**.


## Implementazione del flusso dell'autorizzazione {{site.data.keyword.amashort}} utilizzando Facebook come provider di identità
{: #facebook-auth-flow}

La variabile di ambiente `VCAP_SERVICES` viene creata automaticamente per ogni istanza del servizio {{site.data.keyword.amashort}} e contiene le proprietà necessarie per il processo di autorizzazione. È formata da un oggetto JSON e può essere visualizzata facendo clic su  **Environment Variables**  nella tua applicazione.

Per avviare il processo di autorizzazione:

1. Richiama l'endpoint di autorizzazione (`authorizationEndpoint`) e l'ID client (`clientId`) dalle credenziali del servizio archiviate nella variabile di ambiente `VCAP_SERVICES`. 

	**Nota:** se hai aggiunto il servizio {{site.data.keyword.amashort}} prima dell'aggiunta del supporto web potresti non avere l'endpoint token nelle credenziali del servizio. Invece, utilizza i seguenti URL, a seconda della tua regione {{site.data.keyword.Bluemix_notm}}: 
 
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

3. Vai dalla tua applicazione web all'URI generato.

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
 
2. Invia una richiesta POST all'URI del server del token con il tipo di concessione ("authorization_code"), `clientId` e il tuo URI di reindirizzamento come parametri del modulo. Invia `clientId` e `secret` come credenziali di autenticazion HTTP di base.
 
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

	Il corpo della risposta conterrà l'ID del token e il codice di accesso nel formato JWT (https://jwt.io/).

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
 



