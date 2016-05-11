---

copyright:
  years: 2015, 2016

---

# Creazione di un provider di identità personalizzato
{: #custom-create}
Per creare un provider di identità personalizzato, sviluppa un'applicazione web che espone un'API RESTful:

```
POST <url_di_base>/apps/<id_tenant>/<nome_area_di_autenticazione>/<tipo_di_richiesta>
```

* `url_di_base`: specifica l'URL di base dell'applicazione web del provider di identità personalizzato. L'URL di base è l'URL da registrare nel
dashboard {{site.data.keyword.amashort}}.
* `id_tenant` : specifica l'identificativo univoco del tenant. Quando {{site.data.keyword.amashort}} richiama questa API, fornisce
sempre il GUID dell'applicazione {{site.data.keyword.Bluemix}} (`applicationGUID`).
* `nome_area_di_autenticazione` : specifica il nome dell'area di autenticazione personalizzata definita nel dashboard {{site.data.keyword.amashort}}.
* `tipo_di_richiesta` : specifica uno dei seguenti:
	* `startAuthorization`: specifica un primo passo del processo di autenticazione. Il provider di identità personalizzato deve
rispondere con uno stato di "challenge", "success" o "failure".
	* `handleChallengeAnswer`: gestisce una risposta alla richiesta di verifica dell'autenticazione dal client mobile.

## API `startAuthorization`
{: #custom-startauthorization}

`POST <url_di_base>/apps/<id_tenant>/<nome_area_di_autenticazione>/startAuthorization`

l'API `startAuthorization` viene utilizzata come un primo passo del processo di autenticazione. Un provider di identità personalizzato deve
rispondere con uno stato di "challenge", "success" o "failure".

Per consentire una massima flessibilità del processo di autenticazione, un provider di identità personalizzato ha accesso a tutte le intestazioni HTTP inviate da un client mobile nel corpo della richiesta. Le intestazioni vengono fornite nel seguente formato:

```JavaScript
{
    "headers" : {
    	"header1": "value1",  
    	"header2" : "value2"
    }
}
```

Un provider di identità personalizzato può rispondere con una richiesta di verifica dell'autenticazione o con un esito positivo o un esito negativo immediati. Lo stato HTTP della risposta deve essere `HTTP 200` e il JSON della risposta deve contenere le seguenti proprietà:

* `status` : specifica l'esito positivo (`success`), la richiesta di verifica (`challenge`) o l'esito negativo (`failure`) della richiesta.
* `stateId` (facoltativo): specifica un identificativo stringa generato casualmente per identificare la sessione di autenticazione con il client mobile. Questo attributo può essere omesso se il provider di identità personalizzato non memorizza alcuno stato.
* `challenge` : specifica un oggetto JSON che rappresenta una richiesta di verifica dell'autenticazione da inviare nuovamente al client mobile. Questo attributo viene inviato al client solo se lo stato è impostato su `challenge`.
* `userIdentity` : specifica un oggetto JSON che rappresenta un'identità utente.  L'identità utente consiste in proprietà quali `userName`, `displayName` e gli attributi.  Per ulteriori informazioni, vedi [Oggetto di identità utente](#custom-user-identity). Questa proprietà viene inviata al client mobile solo se lo stato è impostato su `success`.

Ad esempio:

```
{
	"status":"challenge",
	"stateId":"some-random-guid"
	"challenge":{
		message:"Immetti nome utente e password",
		attemptsLeft: 3
	}
}
```

## `handleChallengeAnswer` API
{: #custom-handleChallengeAnswer}

`POST <url_di_base>/apps/<id_tenant>/<nome_area_di_autenticazione>/handleChallengeAnswer`

L'API `handleChallengeAnswer` gestisce una risposta alla richiesta di verifica dell'autenticazione dal client mobile. Analogamente all'API `startAuthorization`,
l'API `handleChallengeAnswer` risponde con lo stato `challenge`, `success` o `failure`.

Analogamente alla richiesta `startAuthorization`, il provider di identità personalizzato ha accesso a tutte le intestazioni HTTP inviate dal client mobile nel corpo della richiesta. Oltre alle intestazioni di richiesta del client mobile, il corpo della richiesta `handleChallengeAnswer` include anche le proprietà `stateId` e `challengeAnswer`.

### Esempio di corpo della richiesta `handleChallengeAnswer`
{: #custom-handleChallengeAnswer-example}

```JavaScript
{
    "headers" : {
    	"header1": "value1",  
    	"header2" : "value2"
	},
    "stateId" : "123123123",
    "challengeAnswer" : {
    	"pinCode":12345
 	}
}
```

La risposta da un'API `handleChallengeAnswer` deve avere la stessa struttura della risposta dell'API `startAuthorization`.

## Oggetto di identità utente
{: #custom-user-identity}

Una risposta a una richiesta di autenticazione con esito positivo deve includere un oggetto di identità utente, con i seguente attributi:
* `userName` : specifica un nome utente univoco.
* `displayName` : specifica il nome di visualizzazione dell'utente.
* `attributes` (facoltativo): specifica un oggetto JSON che contiene gli attributi utente personalizzati.

### Esempio di oggetto di identità utente
{: #custom-user-identity-example}
```JavaScript
{
    "userName" : "janesmith",
    "displayName" : "Jane Smith",
    "attributes" : {
        "Language" : "French",
        "Country" : "Canada"
    }
}
```

L'oggetto di identità utente viene utilizzato dal servizio {{site.data.keyword.amashort}} per generare un token ID inviato al client mobile come parte dell'intestazione di autorizzazione. Dopo un'autenticazione con esito positivo, il cliente mobile ha accesso completo all'oggetto di identità utente.

## Considerazioni sulla sicurezza
{: #custom-security}

Ciascuna richiesta dal servizio {{site.data.keyword.amashort}} a un provider di identità personalizzato contiene un'intestazione di autorizzazione in modo che il provider di identità personalizzato possa verificare che la richiesta sta provenendo da un'origine autorizzata. Anche se non è strettamente obbligatorio, valuta una convalida dell'intestazione di autorizzazione strumentando il tuo provider di identità personalizzato con un SDK server {{site.data.keyword.amashort}}. Per utilizzare questo SDK, nella tua applicazione di provider di identità personalizzato deve avere implementato il Node.js o Liberty for Java&trade;&trade; e deve essere in esecuzione su {{site.data.keyword.Bluemix_notm}}.

L'intestazione di autorizzazione contiene informazioni sul client mobile e sull'applicazione mobile che hanno attivato il processo di autenticazione. Puoi utilizzare il contesto di sicurezza per recuperare questi dati. per ulteriori informazioni, consulta [Protezione delle risorse](protecting-resources.html)

## Implementazione di esempio del provider di identità personalizzato
{: #custom-sample}
Puoi utilizzare una qualsiasi delle seguenti implementazioni di esempio Node.js di un provider di identità personalizzato come un riferimento quando sviluppi il tuo provider di identità personalizzato. Scarica il codice dell'applicazione integrale dai repository GitHub.

* [Esempio semplice](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
* [Esempio avanzato](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

<!---
 ### JSON structure (simple sample)
{: #custom-sample-json}
This implementation assumes that the supplied authentication challenge answer is a JSON object with the following structure:

```
{
 	username: "my.username",
 	password: "my.password"
 }
 ```

### Custom identity provider sample code (simple sample)
{: #custom-sample-code}
```JavaScript
var express = require('express');
var cfenv = require('cfenv');
var log4js = require('log4js');
var jsonParser = require('body-parser').json();

// Using hardcoded user repository
var userRepository = {
	"john.lennon":      { password: "12345", displayName:"John Lennon", dob:"October 9, 1940"},
	"paul.mccartney":   { password: "67890", displayName:"Paul McCartney", dob:"June 18, 1942"},
	"ringo.starr":      { password: "abcde", displayName:"Ringo Starr", dob: "July 7, 1940"},
	"george.harrison":  { password: "fghij", displayName: "George Harrison", dob:"Feburary 25, 1943"}
}

var app = express();
var logger = log4js.getLogger("CustomIdentityProviderApp");
logger.info("Starting up");

app.post('/apps/:tenantId/:realmName/startAuthorization', jsonParser, function(req, res){
	var tenantId = req.params.tenantId;
	var realmName = req.params.realmName;
	var headers = req.body.headers;

	logger.debug("startAuthorization", tenantId, realmName, headers);

	var responseJson = {
		status: "challenge",
		challenge: {
			text: "Enter username and password"
		}
	};

	res.status(200).json(responseJson);
});

app.post('/apps/:tenantId/:realmName/handleChallengeAnswer', jsonParser, function(req, res){
	var tenantId = req.params.tenantId;
	var realmName = req.params.realmName;
	var challengeAnswer = req.body.challengeAnswer;


	logger.debug("handleChallengeAnswer", tenantId, realmName, challengeAnswer);

	var username = req.body.challengeAnswer["username"];
	var password = req.body.challengeAnswer["password"];

	var userObject = userRepository[username];

	var responseJson = { status: "failure" };

	if (userObject && userObject.password == password ){
		logger.debug("Login success for userId ::", username);
		responseJson.status = "success";
		responseJson.userIdentity = {
			userName: username,
			displayName: userObject.displayName,
			attributes: {
				dob: userObject.dob
			}
		}
	} else {
		logger.debug("Login failure for userId ::", username);
	}

	res.status(200).json(responseJson);
});

app.use(function(req, res, next){
	res.status(404).send("Questo non è l'URL che stai cercando");
});

var server = app.listen(cfenv.getAppEnv().port, function () {
	var host = server.address().address;
	var port = server.address().port;
	logger.info('Server listening at %s:%s', host, port);
});
```
--->

## Fasi successive
{: #next-steps}
* [Configurazione di {{site.data.keyword.amashort}} per l'autenticazione personalizzata](custom-auth-config-mca.html)
* [Configurazione dell'autenticazione personalizzata per Android](custom-auth-android.html)
* [Configurazione dell'autenticazione personalizzata per iOS](custom-auth-ios.html)
* [Configurazione dell'autenticazione personalizzata per Cordova](custom-auth-cordova.html)
