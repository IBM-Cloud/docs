---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

Der {{site.data.keyword.amafull}}-Service wird durch den {{site.data.keyword.appid_full}}-Service ersetzt.

#Angepasste Authentifizierung für {{site.data.keyword.amashort}}-Webanwendungen konfigurieren
{: #custom-web}

Sie können Ihrer Web-App eine angepasste Authentifizierung und die Sicherheitsfunktionalität von {{site.data.keyword.amafull}} hinzufügen.

## Vorbereitungen
{: #before-you-begin}

Voraussetzungen:

* Eine Web-App.
* Eine Ressource, die durch eine Instanz des {{site.data.keyword.amashort}}-Service geschützt wird, die zur Verwendung eines angepassten Identitätsproviders konfiguriert ist (siehe die Veröffentlichung zur [Konfiguration der angepassten Authentifizierung](custom-auth-config-mca.html)).  
* Der Wert für die Tenant-ID. Öffnen Sie den Service im {{site.data.keyword.amashort}}-Dashboard. Klicken Sie auf die Schaltfläche **Mobile Systemerweiterungen**. Im Feld **App-GUID/TenantId** wird der Wert `tenantId` (auch als `appGUID` bezeichnet) angezeigt. Sie benötigen diesen Wert für die Initialisierung von Authorization Manager.
* Der Realname. Dies ist der Wert, den Sie im Feld **Realmname** des Abschnitts **Angepasst** auf der Registerkarte **Management** des {{site.data.keyword.amashort}}-Dashboards angegeben haben.
* Die URL der Back-End-Anwendung (**App-Route**). Sie benötigen diese Werte zum Senden von Anforderungen an die geschützten Endpunkte der Back-End-Anwendung.
* Die {{site.data.keyword.Bluemix_notm}}-**Region**. Ihre aktuelle {{site.data.keyword.Bluemix_notm}}-Region finden Sie im Header neben dem Symbol **Avatar** ![Avatarsymbol](images/face.jpg "Avatarsymbol"). Der Regionswert, der angezeigt wird, sollte einer der folgenden sein: `USA (Süden)`, `Vereinigtes Königreich` oder `Sydney`. Außerdem sollte er den im JavaScript-Code erforderlichen SDK-Werten entsprechen: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` oder `BMSClient.REGION_UK`. Sie benötigen diesen Wert für die Initialisierung des {{site.data.keyword.amashort}}-Clients.
* URI für die letzte Weiterleitung (nach Beendigung des Berechtigungsprozesses). Dies ist der Wert für **Weiterleitungs-URIs Ihrer Webanwendung**, den Sie im Abschnitt **Angepasst** auf der Registerkarte **Management** eingegeben haben.

Weitere Informationen finden Sie über die folgenden Links:

* [Einführung in {{site.data.keyword.amashort}}](getting-started.html)
* [Angepassten Identitätsprovider verwenden](custom-auth.html)
* [Angepassten Identitätsprovider erstellen](custom-auth-identity-provider.html)
* [{{site.data.keyword.amashort}} für die angepasste Authentifizierung konfigurieren](custom-auth-config-mca.html)


##Angepassten Identitätsprovider konfigurieren
{: #custom-auth-config}

Beim Erstellen eines angepassten Identitätsproviders müssen Sie eine POST-Methode mit einer Route mit folgender Struktur definieren:

`/apps/:tenantID/<your-realm-name>/handleChallengeAnswer`

`tenantID` ist ein URL-Parameter und `<your-realm-name>` ist ein beliebiger, von Ihnen ausgewählter Realmname.

Der Anforderungshauptteil enthält ein Objekt `challengeAnswer`, das `Benutzername` und `Kennwort` enthält.

Nach der Validierung des Benutzers muss diese Route ein JSON-Objekt mit der folgenden Struktur zurückgeben.

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

**Hinweis:** Das Feld `attributes` ist optional.

Der folgende Code veranschaulicht eine solche POST-Anforderung

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


##{{site.data.keyword.amashort}} für eine angepasste Authentifizierung konfigurieren
{: #custom-auth-config-mca}

Nach der Konfiguration des angepassten Identitätsproviders können Sie die angepasste Authentifizierung im {{site.data.keyword.amashort}}-Dashboard aktivieren.

1. Öffnen Sie den Service im {{site.data.keyword.amashort}}-Dashboard.
1. Aktivieren Sie auf der Registerkarte **Verwalten** die Option **Berechtigung**.
1. Erweitern Sie den Abschnitt **Angepasst**.
1. Geben Sie den **Realname** und die **angepasste Identitätsprovider-URL**.
1. Geben Sie den Wert für **Weiterleitungs-URIs Ihrer Webanwendung** ein. Dies ist der URI für die letzte Weiterleitung nach der erfolgreichen Autorisierung.
1. Klicken Sie auf **Speichern**.


##{{site.data.keyword.amashort}}-Berechtigungsablauf mit einem angepassten Identitätsprovider implementieren
{: #custom-auth-flow}

Die Umgebungsvariable `VCAP_SERVICES` wird automatisch für jede {{site.data.keyword.amashort}}-Serviceinstanz erstellt und enthält Eigenschaften, die für den Berechtigungsprozess erforderlich sind. Sie besteht aus einem JSON-Objekt und kann auf die Registerkarte mit den Serviceberechtigungsnachweisen im {{site.data.keyword.amashort}}-Dashboard angezeigt werden.

Wenn Sie eine Benutzerberechtigung anfordern wollen, leiten Sie den Browser an den Endpunkt des Berechtigungsservers weiter. Gehen Sie dazu wie folgt vor:

1. Rufen Sie den Berechtigungsendpunkt (`authorizationEndpoint`) und die Client-ID (`clientId`) von den Serviceberechtigungsnachweisen ab, die in der Umgebungsvariablen `VCAP_SERVICES` gespeichert sind.

	`var cfEnv = require("cfenv");`

	`var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;`

	**Hinweis:** Wenn Sie den {{site.data.keyword.amashort}}-Service vor der Webunterstützung zur Ihrer Anwendung hinzugefügt haben, ist möglicherweise kein Tokenendpunkt in den Serviceberechtigungsnachweisen enthalten. Verwenden Sie stattdessen die folgenden URLs, abhängig von Ihrer {{site.data.keyword.Bluemix_notm}}-Region:

	USA (Süden):

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization`

	London:

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization`

	Sydney:

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization`

2. Erstellen Sie den Berechtigungsserver-URI mit `response_type("code")`, `client_id` und `redirect_uri` als Abfrageparameter.  

3. Leiten Sie von Ihrer Web-App zum generierten URI weiter.

   Im nachfolgenden Beispiel werden die Parameter von der Variablen `VCAP_SERVICES` abgerufen, außerdem wird die URL erstellt und die Weiterleitungsanforderung wird gesendet.

	```Java
var cfEnv = require("cfenv"); 
app.get("/protected", checkAuthentication, function(req, res, next){
		res.send("Hello from protected endpoint"); 
  }
	);

	function checkAuthentication(req, res, next){
		// Check if user is authenticated
		if (req.session.userIdentity) {
			next()
		} else {
			// If not - redirect to authorization server
			var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
			var authorizationEndpoint = mcaCredentials.authorizationEndpoint;
			var clientId = mcaCredentials.clientId;
			var redirectUri = "http://some-server/oauth/callback"; // Your web application redirect uri
			var redirectUrl = authorizationEndpoint + "?response_type=code";
			redirectUrl += "&client_id=" + clientId;
			redirectUrl += "&redirect_uri=" + redirectUri;
			res.redirect(redirectUrl);
		}
	}
	```
	{: codeblock}

	Der Parameter `redirect_uri` gibt den Weiterleitungs-URI Ihrer Webanwendung an und muss mit dem im {{site.data.keyword.amashort}}-Dashboard definierten URI übereinstimmen.  

	Ein Parameter `state` kann zusammen mit der Anforderung übergeben werden. Dieser Parameter wird an die POST-Methode des angepassten Identitätsproviders weitergegeben und kann über den Anforderungshauptteil (`req.body.stateId`) abgerufen werden.  

	Nach der Weiterleitung zum Berechtigungsendpunkt wird ein Anmeldeformular angezeigt. Nachdem die Berechtigungsnachweise des Benutzers vom angepassten Identitätsprovider authentifiziert wurden, ruft der {{site.data.keyword.amashort}}-Service den Weiterleitungs-URI Ihrer Webanwendung auf und gibt den Autorisierungscode als Abfrageparameter an.  

	Nach der Weiterleitung wird ein Anmeldeformular angezeigt. Nachdem die Berechtigungsnachweise des Benutzers vom angepassten Identitätsprovider authentifiziert wurden, ruft der {{site.data.keyword.amashort}}-Service den Weiterleitungs-URI der Webanwendung auf und gibt den Autorisierungscode als Abfrageparameter an.

##Tokens abrufen
{: custom-auth-tokens}

Im nächsten Schritt werden das Zugriffstoken und das Identitätstoken mithilfe des zuvor empfangenen Autorisierungscodes abgerufen. Gehen Sie dazu wie folgt vor:

1. Rufen Sie `authorizationEndpoint`, `clientId` und `secret` von den Serviceberechtigungsnachweisen ab, die in der Umgebungsvariablen `VCAP_SERVICES` gespeichert sind.

	**Hinweis:** Wenn Sie den {{site.data.keyword.amashort}}-Service vor der Webunterstützung zur Ihrer Anwendung hinzugefügt haben, ist möglicherweise kein Tokenendpunkt in den Serviceberechtigungsnachweisen enthalten. Verwenden Sie stattdessen die folgenden URLs, abhängig von Ihrer {{site.data.keyword.Bluemix_notm}}-Region:

	USA (Süden):

	`     https://mobileclientaccess.ng.bluemix.net/oauth/v2/token   
 `

	London:

	`     https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token
 `

	Sydney:

	`     https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token 
 `

2. Senden Sie eine POST-Anforderung an die Token-Server-URI mit `grant_type`, `client_id`, `redirect_uri` und `code` als Formularparameter sowie `clientId` und `secret` als HTTP-Basisauthentifizierungsnachweise.

	Der Code im folgenden Beispiel ruft die erforderlichen Werte ab und sendet sie mit einer POST-Anforderung.

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

	Beachten Sie, dass der Parameter `redirect_uri` mit dem Parameter `redirect_uri` aus der vorhergehenden Berechtigungsanforderung übereinstimmen muss. Als Wert für den Parameter 'code' muss der Autorisierungscode angegeben werden, der in der Antwort am Ende der Autorisierungsanforderung empfangen wurde. Der Autorisierungscode ist nur 10 Minuten gültig, danach muss ein neuer Code abgerufen werden.

	Der Antworthauptteil enthält die Parameter `access_token` und `id_token` im JWT-Format (siehe die [JWT-Website ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://jwt.io){: new_window}).

	Nachdem Sie das Zugriffstoken und das Identitätstoken empfangen haben, können Sie die Websitzung als authentifiziert markieren und optional diese Tokens speichern.


##Abgerufenes Zugriffs- und Identitätstoken verwenden
{: #custom-auth-using-token}

Das Identitätstoken enthält Informationen zu der Benutzeridentität. Bei einer angepassten Authentifizierung enthält das Token alle Informationen, die vom angepassten Identitätsprovider bei der Authentifizierung zurückgegeben werden. Das Feld `displayName` unter `imf.user` enthält den `Anzeigenamen`, der vom angepassten Identitätsprovider zurückgegeben wurde, und das Feld `id` enthält den `Benutzernamen`.  Alle anderen vom angepassten Identitätsprovider zurückgegebenen Werte werden im Feld `attributes` unter `imf.user` zurückgegeben.  

Das Zugriffstoken ermöglicht die Kommunikation mit Ressourcen, die von den {{site.data.keyword.amashort}}-Berechtigungsfiltern geschützt werden (siehe [Ressourcen schützen](protecting-resources.html)). Um Anforderungen an geschützte Ressourcen zu stellen, fügen Sie einen Berechtigungsheader mit folgender Struktur zu den Anforderungen hinzu:

`Authorization=Bearer <accessToken> <idToken>`

####Tipps:
{: #tips_token}

* `<accessToken>` und `<idToken>` müssen durch ein Leerzeichen getrennt werden.

* Das Identitätstoken ist optional. Wenn kein Identitätstoken angegeben wird, besteht zwar Zugriff auf die geschützte Ressource, es können jedoch keine Informationen zu dem berechtigten Benutzer abgerufen werden.
