---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-08"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configurazione dell'autenticazione personalizzata per le applicazioni Web {{site.data.keyword.amashort}}
{: #custom-web}

Aggiungi l'autenticazione personalizzata e la funzionalità di sicurezza {{site.data.keyword.amafull}} alla tua applicazione Web.

## Prima di cominciare
{: #before-you-begin}

Prima di iniziare, devi disporre di:

* Un'applicazione Web.
* Una risorsa che sia protetta da un'istanza del servizio {{site.data.keyword.amashort}} configurata per utilizzare un provider di identità personalizzato (consulta [Configurazione dell'autenticazione personalizzata](custom-auth-config-mca.html)).  
* Il tuo valore **TenantID**. Apri il tuo servizio nel dashboard {{site.data.keyword.amashort}}. Fai clic sul pulsante **Opzioni per dispositivi mobili**. Il valore `tenantId` (noto anche come `appGUID`)  viene visualizzato nel campo **GUID applicazione / TenantId**. Avrai bisogno di questo valore per inizializzare il gestore autorizzazione.
* Il tuo nome **Realm**. Questo è il valore che hai specificato nel campo **Nome realm** della sezione **Personalizzato** nella scheda **Gestione** del dashboard {{site.data.keyword.amashort}}.
* L'URL della tua applicazione di back-end (**Rotta applicazione**). Avrai bisogno di questo valore per inviare le richieste agli endpoint protetti della tua applicazione di back-end.
* La tua **Regione** {{site.data.keyword.Bluemix_notm}}. Puoi trovare la tua regione {{site.data.keyword.Bluemix_notm}} corrente nell'intestazione, accanto all'icona **Avatar** ![Icona Avatar](images/face.jpg "Icona Avatar"). Il valore della regione visualizzato deve essere uno dei seguenti: `Stati Uniti Sud`, `Regno Unito` o `Sydney` e corrisponde ai valori delle SDK richiesti nel codice Javascript: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` o `BMSClient.REGION_UK`. Avrai bisogno di questo valore per inizializzare il client {{site.data.keyword.amashort}}.
* L'URI Per il reindirizzamento finale (dopo il completamento del processo di autorizzazione). Questo è il valore **I tuoi URI di reindirizzamento dell'applicazione web** che hai immesso nella sezione **Personalizzato** della scheda **Gestione**.

Per ulteriori informazioni

* [Introduzione a {{site.data.keyword.amashort}}](getting-started.html)
* [Utilizzo di un provider di identità personalizzato](custom-auth.html)
* [Creazione di un provider di identità personalizzato](custom-auth-identity-provider.html)
* [Configurazione di {{site.data.keyword.amashort}} per l'autenticazione personalizzata](custom-auth-config-mca.html)


## Configurazione di un provider di identità personalizzato
{: #custom-auth-config}

Quando crei un provider di identità personalizzato devi definire un metodo POST con una rotta nella seguente struttura:

`/apps/:tenantID/<your-realm-name>/handleChallengeAnswer`

`tenantID` è il parametro dell'URL e `<your-realm-name>` è il nome realm di tua scelta.

Il corpo della richiesta conterrà un oggetto `challengeAnswer` che contiene `username` e `password`.

Dopo la convalida dell'utente, questa rotta deve restituire un oggetto JSON della seguente struttura.

```json
{
	status: "success", 
            userIdentity: {
		userName: <user name>, 
                displayName: <display name> 
                attributes: <additional attributes json> 
            }
}
```
{: codeblock}

**Nota:** il campo `attributes` è facoltativo.

Il seguente codice mostra una richiesta POST.

```Java
var app = express();
var bodyParser = require('body-parser');
app.use(bodyParser.json());

var users = {
	"John": {
		password: "123",
      displayName: "John Doe"
	}
};

app.post('/apps/:tenantID/customAuthRealm_1/handleChallengeAnswer',
         function(req, res) {
	console.log ("tenantID " + req.params.tenantID);

	var challengeAnswer = req.body.challengeAnswer;
         console.log ("challengeAnswer " + JSON.stringify(challengeAnswer));

	if (challengeAnswer && users[challengeAnswer.username] && challengeAnswer.password === users[challengeAnswer.username].password) {
		res.json({
                  status: "success",
                  userIdentity: {
				userName: challengeAnswer.username,
                  displayName: users[challengeAnswer.username].displayName
                  }
		});
         } else {
		res.json({
                  status: "failure"
		});
	}

});
```
{: codeblock}


## Configurazione di {{site.data.keyword.amashort}} per l'autenticazione personalizzata
{: #custom-auth-config-mca}

Dopo che hai configurato il tuo provider di identità personalizzato, puoi abilitare l'autenticazione personalizzata nel dashboard {{site.data.keyword.amashort}}.

1. Apri il tuo servizio nel dashboard {{site.data.keyword.amashort}}.
1. Dalla scheda **Manage**, attiva **Authorization**.
1. Espandi la sezione **Personalizzato**.
1. Immetti **Nome realm**, **URL provider di identità personalizzato**.
1. Immetti il valore **I tuoi URI di reindirizzamento dell'applicazione web**. Questo è l'URI del reindirizzamento finale dopo una corretta autorizzazione.
1. Fai clic su **Save**.


## Implementazione del flusso dell'autorizzazione {{site.data.keyword.amashort}} utilizzando un provider dell'identità personalizzato
{: #custom-auth-flow}

La variabile di ambiente `VCAP_SERVICES` viene creata automaticamente per ogni istanza del servizio {{site.data.keyword.amashort}} e contiene le proprietà necessarie per il processo di autorizzazione. È formato da un oggetto JSON e puoi visualizzarlo nella scheda **Credenziali del servizio** nel dashboard {{site.data.keyword.amashort}}.

Per richiedere l'autenticazione utente, reindirizzare il browser all'endpoint del server di autorizzazione. A tal fine:

1. Richiama l'endpoint di autorizzazione (`authorizationEndpoint`) e l'ID client (`clientId`) dalle credenziali del servizio memorizzate nella variabile di ambiente `VCAP_SERVICES`.

	`var cfEnv = require("cfenv");`

	`var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;`

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

3. Vai dalla tua applicazione Web all'URI generato.

   Il seguente esempio richiama i parametri dalla variabile `VCAP_SERVICES`, crea l'URL e invia la richiesta di reindirizzamento.

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
			// Se non lo è - ritorna al server di autorizzazione
    var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
    var authorizationEndpoint = mcaCredentials.authorizationEndpoint;
    var clientId = mcaCredentials.clientId;
    var redirectUri = "http://some-server/oauth/callback"; // L'uri di reindirizzamento della tua applicazione web
    var redirectUrl = authorizationEndpoint + "?response_type=code";
    redirectUrl += "&client_id=" + clientId;
    redirectUrl += "&redirect_uri=" + redirectUri;
    res.redirect(redirectUrl);
  }
	}
	```
	{: codeblock}

	Tieni presente che il parametro `redirect_uri` rappresenta l'URI di reindirizzamento della tua applicazione Web e deve essere uguale al valore definito nel dashboard {{site.data.keyword.amashort}}.  

	Un parametro `state` può essere trasmesso con la richiesta. Questo parametro sarà propagato al metodo POST del provider di identità personalizzato e vi si può accedere dal corpo della richiesta (`req.body.stateId`).  

	Dopo il reindirizzamento dell'endpoint di autorizzazione l'utente visualizzerà un modulo di accesso. Dopo avere autenticato le credenziali dell'utente con il provider di identità personalizzato, il servizio {{site.data.keyword.amashort}} richiamerà il tuo URI di reindirizzamento dell'applicazione web fornendo il codice concesso come un parametro di query.  

	Dopo il reindirizzamento, l'utente riceve un modulo di accesso. Dopo avere autenticato le credenziali dell'utente con il provider di identità personalizzato, il servizio {{site.data.keyword.amashort}} richiamerà il tuo URI di reindirizzamento dell'applicazione Web fornendo il codice concesso come un parametro di query.

## Ottenimento dei token
{: custom-auth-tokens}

Il passo successivo è quello di ottenere il token di accesso e il token di identità utilizzando il codice concesso ricevuto precedentemente. A tal fine:

1. Richiama `authorizationEndpoint`, `clientId` e `secret` dalle credenziali del servizio archiviate nella variabile di ambiente `VCAP_SERVICES`.

	**Nota:** se hai aggiunto il servizio {{site.data.keyword.amashort}} prima dell'aggiunta del supporto Web potresti non avere l'endpoint token nelle credenziali del servizio. Invece, utilizza i seguenti URL, a seconda della tua regione {{site.data.keyword.Bluemix_notm}}:

	Stati Uniti Sud:

	`     https://mobileclientaccess.ng.bluemix.net/oauth/v2/token   
 `

	Londra:

	`     https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token
 `

	Sydney:

	`     https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token
 `

2. Invia una richiesta POST all'URI del server del token con `grant_type`, `client_id`, `redirect_uri` e `code` come parametri del modulo e `clientId` e `secret` come credenziali di autenticazione HTTP di base.

	Nel seguente esempio, il seguente codice richiama i valori necessari e li invia con una richiesta POST:

	```Java
var cfEnv = require("cfenv");
var base64url = require("base64url ");
app.get("/oauth/callback", function(req, res, next){
		var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials; 
    var tokenEndpoint = mcaCredentials.tokenEndpoint;

		var formData = {
			grant_type: "authorization_code",
			client_id: mcaCredentials.clientId,
			redirect_uri: "http://some-server/oauth/callback",   // Your Web application redirect uri
			code: req.query.code
		}

		request.post({
			url: tokenEndpoint,
			formData: formData
		}, function (err, response, body) {
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

	Tieni presente che il parametro `redirect_uri` deve corrispondere al `redirect_uri` utilizzato nella richiesta di autorizzazione precedente. Il parametro code deve essere il codice concesso ricevuto nella risposta al termine della richiesta di autorizzazione. Il codice concesso è valido solo per 10 minuti, dopo i quali avrai bisogno di ottenere un nuovo codice.

	Il corpo della risposta conterrà `access_token` e `id_token` in formato JWT; vedi il [sito Web JWT![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://jwt.io "Icona link esterno"){: new_window}.

	Come hai ricevuto l'accesso e i token di identità, puoi indicare la sessione Web come autenticata e facoltativamente conservare questi token.


## Utilizzo dell'accesso ottenuto e del token di identità
{: #custom-auth-using-token}

Il token di identità contiene informazioni sull'identità dell'utente. Nel caso di un'autenticazione personalizzata, il token conterrà tutte le informazioni restituite dal provider di identità personalizzato al momento dell'autenticazione. Nel campo `imf.user`, il campo `displayName` conterrà il `displayName` restituito dal provider di identità personalizzato e il campo `id` conterrà il `userName`.  Tutti gli altri valori restituiti dal provider di identità personalizzato vengono restituiti nel campo `attributes` in `imf.user`.  

Il token di accesso consente la comunicazione con le risorse protette dai filtri di autorizzazione {{site.data.keyword.amashort}} (consulta [Protezione delle risorse](protecting-resources.html)). Per effettuare richieste che proteggano le risorse aggiungi un'intestazione dell'autorizzazione alle richieste con la seguente struttura:

`Authorization=Bearer <accessToken> <idToken>`

#### Suggerimenti:
{: #tips_token}

* Il `<accessToken>` e il `<idToken>` devono essere separati da uno spazio vuoto.

* Il token di identità è facoltativo. Se hai fornito il token di identità, è possibile accedere alla risorsa protetta ma non si riceveranno le informazioni sull'utente autorizzato.
