---

copyright:
  years: 2015, 2016

---

# Angepassten Identitätsprovider erstellen
{: #custom-create}
Zur Erstellung eines angepassten Identitätsproviders entwickeln Sie eine Webanwendung, die eine REST-konforme API bereitstellt:

```
POST <base_url>/apps/<tenant_id>/<realm_name>/<request_type>
```

* `base_url`: Gibt die Basis-URL der Webanwendung des angepassten Identitätsproviders an. Die Basis-URL ist die URL, die im {{site.data.keyword.amashort}}-Dashboard registriert werden muss.
* `tenant_id`: Gibt die eindeutige Kennung des Tenants an. Wenn {{site.data.keyword.amashort}} diese API aufruft, wird immer die GUID der App für {{site.data.keyword.Bluemix}} (`applicationGUID`) übergeben.
* `realm_name`: Gibt den angepassten Realmnamen an, der im {{site.data.keyword.amashort}}-Dashboard definiert ist.
* `request_type`: Gibt einen der folgenden Werte an:
	* `startAuthorization`: Gibt einen ersten Schritt des Authentifizierungsprozesses an. Der angepasste Identitätsprovider muss mit dem Status "challenge", "success" oder "failure" antworten.
	* `handleChallengeAnswer`: Verarbeitet eine Antwort auf eine Authentifizierungsanforderung aus dem mobilen Client.

## API `startAuthorization`
{: #custom-startauthorization}

`POST <base_url>/apps/<tenant_id>/<realm_name>/startAuthorization`

Die API `startAuthorization` wird als erster Schritt des Authentifizierungsprozesses verwendet. Ein angepasster Identitätsprovider muss mit dem Status "challenge", "success" oder "failure" antworten.

Eine hohe Flexibilität erhält der Authentifizierungsprozess dadurch, dass ein angepasster Identitätsprovider im Anforderungshauptteil Zugriff auf alle HTTP-Header hat, die von einem mobilen Client gesendet werden. Die Header werden im folgenden Format bereitgestellt:

```JavaScript
{
    "headers" : {
    	"header1": "value1",  
    	"header2" : "value2"
    }
}
```

Ein angepasster Identitätsprovider kann mit Authentifizierungsanforderung ('challenge'), mit sofortigem Erfolg ('success') oder Fehler ('failure') antworten. Der Antwort-HTTP-Status muss `HTTP 200` sein und die das Antwort-JSON-Objekt muss die folgenden Eigenschaften enthalten:

* `status`: Gibt `success`, `challenge` oder `failure` für die Anforderung an.
* `stateId` (optional): Gibt eine zufällig generierte Zeichenfolgekennung an, die die Authentifizierungssitzung mit dem mobilen Client identifiziert. Dieses Attribut kann weggelassen werden, wenn der angepasste Identitätsprovider keinen Status speichert.
* `challenge`: Gibt ein JSON-Objekt an, dass eine Authentifizierungsanforderung darstellt, die zurück an den mobilen Client gesendet wird. Dieses Attribut wird nur dann an den Client gesendet, wenn der Status auf den Wert `challenge` gesetzt wird.
* `userIdentity`: Gibt ein JSON-Objekt an, das eine Benutzeridentität darstellt.  Die Benutzeridentität besteht aus Eigenschaften wie `userName` (Benutzername), `displayName` (Anzeigename) und Attributen.  Weitere Informationen finden Sie in [Benutzeridentitätsobjekt](#custom-user-identity). Diese Eigenschaft wird nur dann an den mobilen Client gesendet, wenn der Status auf `success` gesetzt wird.

Beispiel:

```
{
	"status":"challenge",
	"stateId":"some-random-guid"
	"challenge":{
		message:"Enter username and password",
		attemptsLeft: 3
	}
}
```

## API `handleChallengeAnswer`
{: #custom-handleChallengeAnswer}

`POST <base_url>/apps/<tenant_id>/<realm_name>/handleChallengeAnswer`

Die API `handleChallengeAnswer` verarbeitet eine Antwort auf eine Authentifizierungsanforderung aus dem mobilen Client. Ebenso wie die API `startAuthorization` antwortet die API `handleChallengeAnswer` mit dem Status `challenge` (Anforderung), `success` (Erfolg) oder `failure` (Fehler).

Ähnlich wie bei einer Anforderung `startAuthorization` hat der angepasste Identitätsprovider im Anforderungshauptteil Zugriff auf alle HTTP-Header, die von dem mobilen Client gesendet werden. Neben den Anforderungsheadern des mobilen Clients enthält der Hauptteil der Anforderung `handleChallengeAnswer` auch die Eigenschaften `stateId` und `challengeAnswer`.

### Beispiel für den Hauptteil einer Anforderung `handleChallengeAnswer`
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

Die Antwort aus einer API `handleChallengeAnswer` muss dieselbe Struktur wie die Antwort der API `startAuthorization` aufweisen.

## Benutzeridentitätsobjekt
{: #custom-user-identity}

Eine Antwort auf eine erfolgreiche Authentifizierungsanforderung muss ein Benutzeridentitätsobjekt mit den folgenden Attributen enthalten:
* `userName`: Gibt einen eindeutigen Benutzernamen an.
* `displayName`: Gibt den Anzeigenamen des Benutzers an.
* `attributes` (optional): Gibt ein JSON-Objekt an, das angepasste Benutzerattribute enthält.

### Beispiel für ein Benutzeridentitätsobjekt
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

Das Benutzeridentitätsobjekt wird vom {{site.data.keyword.amashort}}-Service zum Generieren eines ID-Tokens verwendet, das an den mobilen Client als Teil des Berechtigungsheaders gesendet wird. Nach einer erfolgreichen Authentifizierung hat der mobile Client uneingeschränkten Zugriff auf das Benutzeridentitätsobjekt.

## Sicherheitsaspekte
{: #custom-security}

Jede Anforderung aus dem {{site.data.keyword.amashort}}-Service an einen angepassten Identitätsprovider enthält einen Berechtigungsheader, sodass der der angepasste Identitätsprovider überprüfen kann, ob die Anforderung von einer autorisierten Quelle kommt. Obwohl dies nicht streng obligatorisch ist, sollten Sie in Betracht ziehen, den Berechtigungsheader zu validieren, indem Sie Ihren angepassten Identitätsprovider mit einem {{site.data.keyword.amashort}}-Server-SDK instrumentieren. Zur Verwendung dieses SDK muss Ihre angepasste Identitätsprovideranwendung mit Node.js oder Liberty for Java&trade;&trade; implementiert sein und in {{site.data.keyword.Bluemix_notm}} ausgeführt werden.

Der Berechtigungsheader enthält Informationen zum mobilen Client und zur mobilen App, die den Authentifizierungsprozess ausgelöst haben. Sie können den Sicherheitskontext zum Abrufen dieser Daten verwenden. Weitere Informationen finden Sie in [Ressourcen schützen](protecting-resources.html).

## Beispielimplementierung eines angepassten Identitätsproviders
{: #custom-sample}
Sie können beliebige der folgenden Beispiele für Node.js-Implementierungen eines angepassten Identitätsproviders als Referenz verwenden, wenn Sie Ihren angepassten Identitätsprovider entwickeln. Laden Sie den vollständigen Anwendungscode aus den GitHub-Repositorys herunter.

* [Einfaches Beispiel](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
* [Erweitertes Beispiel](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

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
	res.status(404).send("This is not the URL you're looking for");
});

var server = app.listen(cfenv.getAppEnv().port, function () {
	var host = server.address().address;
	var port = server.address().port;
	logger.info('Server listening at %s:%s', host, port);
});
```
--->

## Nächste Schritte
{: #next-steps}
* [{{site.data.keyword.amashort}} für die angepasste Authentifizierung konfigurieren](custom-auth-config-mca.html)
* [Angepasste Authentifizierung für Android konfigurieren](custom-auth-android.html)
* [Angepasste Authentifizierung für iOS konfigurieren](custom-auth-ios.html)
* [Angepasste Authentifizierung für Cordova konfigurieren](custom-auth-cordova.html)
