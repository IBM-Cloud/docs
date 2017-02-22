---

copyright:
  year: 2016, 2017
lastupdated: "2017-01-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Facebook-Authentifizierung für Webanwendungen aktivieren
{: #facebook-auth-web}

Sie können Benutzer über Facebook für Ihre {{site.data.keyword.amafull}}-Webanwendung authentifizieren. Fügen Sie die Sicherheitsfunktionalität von {{site.data.keyword.amashort}} hinzu.

## Vorbereitungen
{: #facebook-auth-android-before}
Voraussetzungen:

* Eine Web-App.
* Ein {{site.data.keyword.amashort}}-Service. Weitere Informationen finden Sie in der [Einführung](index.html).
* URI für die letzte Weiterleitung (nach Beendigung des Berechtigungsprozesses).


## Anwendung auf der Site 'Facebook for Developers' konfigurieren
{: #facebook-auth-config}

Zur Verwendung von Facebook als Identitätsprovider auf Ihrer Website müssen Sie die Website-Plattform Ihrer Facebook-Anwendung hinzufügen und sie konfigurieren.

1. Melden Sie sich auf der Site [Facebook for Developers](https://developers.facebook.com) bei Ihrem Konto an.
	Informationen zum Erstellen einer neuen App finden Sie unter [Anwendung auf der Site 'Facebook for Developers' erstellen](facebook-auth-overview.html#facebook-appID).
1. Notieren Sie die **App-ID** und den **geheimen Schlüssel der App**. Sie benötigen diese Werte beim Konfigurieren Ihres Webprojekts für die Facebook-Authentifizierung im Mobile Client Access-Dashboard.
1. Wählen Sie unter **Products List** die Option **Facebook Login** aus.
4. Fügen Sie die **Web**-Plattform hinzu, falls sie nicht vorhanden ist.
6. Geben Sie den Callback-Endpunkt-URI des Berechtigungsservers im Feld **Valid OAuth redirect URIs** ein. Sie können diesen Wert nach der Konfiguration des {{site.data.keyword.amashort}}-Service anhand der nachfolgenden Schritte konfigurieren.
7. Speichern Sie die Änderungen.


## {{site.data.keyword.amashort}} für die Facebook-Authentifizierung konfigurieren
{: #facebook-auth-config-ama}

Nachdem Sie Ihre Facebook-App-ID und den geheimen Schlüssel der App erhalten haben und Ihre Facebook for Developers-Anwendung zur Bedienung von Web-Clients konfiguriert wurde, können Sie die Facebook-Authentifizierung im {{site.data.keyword.amashort}}-Dashboard aktivieren.

1. Öffnen Sie das {{site.data.keyword.amashort}}-Service-Dashboard.
1. Aktivieren Sie auf der Registerkarte **Verwalten** die Option **Berechtigung**.
1. Erweitern Sie den Abschnitt **Facebook**.
1. Wählen Sie die Option zum Hinzufügen von Facebook zu einer Web-App aus.
5. Notieren Sie den Wert im Textfeld **Mobile Client Access-Weiterleitungs-URI für Facebook for Developers**. Sie müssen diesen Wert in das Feld **Valid OAuth redirect URIs** bei der **Facebook-Anmeldung** des Facebook-Entwicklerportals eingeben.
6. Geben Sie die Werte für **Anwendungs-ID** und **Geheimer Schlüssel der App** für Facebook ein, die Sie von der Site 'Facebook for Developers' abgerufen haben.
7. Geben Sie den Weiterleitungs-URI in das Feld **Weiterleitungs-URIs Ihrer Webanwendung** ein. Dies ist der Wert für den Weiterleitungs-URI, auf den nach Beendigung des Berechtigungsprozesses zugegriffen wird. Er wird vom Entwickler festgelegt.
8. Klicken Sie auf **Speichern**.


## {{site.data.keyword.amashort}}-Berechtigungsablauf mit Facebook als Identitätsprovider implementieren
{: #facebook-auth-flow}

Die Umgebungsvariable `VCAP_SERVICES` wird automatisch für jede {{site.data.keyword.amashort}}-Serviceinstanz erstellt und enthält Eigenschaften, die für den Berechtigungsprozess erforderlich sind. Sie besteht aus einem JSON-Objekt und kann auf die Registerkarte mit den Serviceberechtigungsnachweisen im {{site.data.keyword.amashort}}-Service-Dashboard angezeigt werden.

Gehen Sie wie folgt vor, um den Berechtigungsprozess zu starten:

1. Rufen Sie den Berechtigungsendpunkt (`authorizationEndpoint`) und die Client-ID (`clientId`) von den Serviceberechtigungsnachweisen ab, die in der Umgebungsvariablen `VCAP_SERVICES` gespeichert sind.

	`var cfEnv = require("cfenv");`

	**Hinweis:** Wenn Sie den {{site.data.keyword.amashort}}-Service vor der Webunterstützung zur Ihrer Anwendung hinzugefügt haben, ist möglicherweise kein Tokenendpunkt in den **Serviceberechtigungsnachweisen** enthalten. Verwenden Sie stattdessen die folgenden URLs, abhängig von Ihrer {{site.data.keyword.Bluemix_notm}}-Region:

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
		// Prüfen, ob Benutzer authentifiziert ist

		if (req.session.userIdentity){   
			next()  
     } else {   
			// If not - redirect to authorization server   
			var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;   
			var authorizationEndpoint = mcaCredentials.authorizationEndpoint;   
			var clientId = mcaCredentials.clientId;   
			var redirectUri = "http://some-server/oauth/callback"; 
			// Your Web application redirect URI   

			var redirectUrl = authorizationEndpoint + "?response_type=code";
        redirectUrl += "&client_id=" + clientId;   
        redirectUrl += "&redirect_uri=" + redirectUri;   

			res.redirect(redirectUrl);  
  
      }
	}
	```
	{: codeblock}

	Der Parameter `redirect_uri` entspricht dem URI für die Weiterleitung nach erfolgreicher oder nicht erfolgreicher Authentifizierung bei Facebook.   

	Nach der Weiterleitung zum Berechtigungsendpunkt wird ein Anmeldeformular von Facebook angezeigt. Nachdem Facebook die Benutzeridentität berechtigt hat, ruft der {{site.data.keyword.amashort}}-Service den Weiterleitungs-URI der Webanwendung auf und gibt den Autorisierungscode als Abfrageparameter an.  


## Tokens abrufen
{: #facebook-auth-tokens}

Im nächsten Schritt werden das Zugriffs- und das Identitätstoken mithilfe des zuvor empfangenen Autorisierungscodes abgerufen:

1.  Rufen Sie das Token (`tokenEndpoint`), die Client-ID (`clientId`) und den geheimen Schlüssel (`secret`) von den Serviceberechtigungsnachweisen ab, die in der Umgebungsvariablen `VCAP_SERVICES` gespeichert sind.

	**Hinweis:** Wenn Sie {{site.data.keyword.amashort}} verwendet haben, bevor die Webunterstützung hinzugefügt wurde, ist möglicherweise kein Tokenendpunkt in den Serviceberechtigungsnachweisen enthalten. Verwenden Sie stattdessen die folgenden URLs, abhängig von Ihrer Bluemix-Region:

	USA (Süden):

	`     https://mobileclientaccess.ng.bluemix.net/oauth/v2/token   
 `

	London:

	`     https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token
 `

	Sydney:

	`     https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token 
 `

2. Senden Sie eine POST-Anforderung an die Token-Server-URI mit Bewilligungstyp ("authorization_code"), `clientId` und Ihrer Weiterleitungs-URI als Formularparameter. Senden Sie `clientId` und `secret` als HTTP-Basisauthentifizierungsnachweise.

	Der folgende Code ruft die erforderlichen Werte ab und sendet sie mit einer POST-Anforderung.

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
			redirect_uri: "http://some-server/oauth/callback",
			// Weiterleitungs-URIs Ihrer Webanwendung
			code: req.query.code
		}

		request.post( {
			url: tokenEndpoint, 
    formData: formData 
    }, function (err, response, body){
			var parsedBody = JSON.parse(body); 
			req.session.accessToken = parsedBody.access_token; 
			req.session.idToken = parsedBody.id_token; 
			var idTokenComponents = parsedBody.id_token.split("."); 
			// [header, payload, signature] 
			var decodedIdentity= base64url.decode(idTokenComponents[1]);
			req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"]; 
			res.redirect("/");
		}
		).auth(mcaCredentials.clientId, mcaCredentials.secret); 

   }
	);
	```
	{: codeblock}

	Beachten Sie, dass der Parameter `redirect_uri` mit dem Parameter `redirect_uri` aus der vorhergehenden Berechtigungsanforderung übereinstimmen muss. Als Wert für den Parameter `code` muss der Autorisierungscode angegeben werden, der in der Antwort von der Berechtigungsanforderung empfangen wurde. Der Autorisierungscode ist 10 Minuten gültig, danach muss ein neuer Code abgerufen werden.

	Der Antworthauptteil enthält den Zugriffscode und die Token-ID im JWT-Format (siehe die [JWT-Website ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://jwt.io/ "Symbol für externen Link"){: new_window}.

	Nachdem Sie das Zugriffstoken und das Identitätstoken empfangen haben, können Sie die Websitzung als authentifiziert markieren und optional diese Tokens speichern.  

##Abgerufenes Zugriffs- und Identitätstoken verwenden
{: #facebook-auth-using-token}

Das Identitätstoken enthält Informationen zu der Benutzeridentität. Bei der Facebook-Authentifizierung enthält das Token alle Informationen, bei denen der Benutzer eingewilligt hat, dass sie geteilt werden, wie zum Beispiel den vollständigen Namen, die Altersgruppe, die URL des Profilfotos usw.  

Das Zugriffstoken ermöglicht die Kommunikation mit Ressourcen, die von den {{site.data.keyword.amashort}}-Berechtigungsfiltern geschützt werden; weitere Informationen hierzu finden Sie unter [Ressourcen schützen](protecting-resources.html).

Um Anforderungen an geschützte Ressourcen zu stellen, fügen Sie einen Berechtigungsheader mit folgender Struktur zu den Anforderungen hinzu:

`Authorization=Bearer <accessToken> <idToken>`

#### Tipps:
{: #tips}

* `accessToken` und `idToken` müssen durch ein Leerzeichen getrennt werden.

* `idToken` ist optional. Wenn kein Identitätstoken angegeben wird, besteht zwar Zugriff auf die geschützte Ressource, es können jedoch keine Informationen zu dem berechtigten Benutzer abgerufen werden.
