---

copyright:
  year: 2016

---

# Google-Authentifizierung für Webanwendungen aktivieren
{: #google-auth-web}

*Letzte Aktualisierung: 18. Juli 2016*
{: .last-updated}

Sie können Benutzer über die Google-Anmeldung für Ihre Webanwendung authentifizieren.


## Vorbereitungen
{: #before-you-begin}

Voraussetzungen:
* Web-App.
* Instanz einer {{site.data.keyword.Bluemix_notm}}-Anwendung, die durch den {{site.data.keyword.amashort}}-Service geschützt ist. Weitere Informationen zur Erstellung einer {{site.data.keyword.Bluemix_notm}}-Back-End-Anwendung finden Sie in der [Einführung](index.html).
* URI für die letzte Weiterleitung (nach Beendigung des Berechtigungsprozesses).



## Google-Anwendung für die Website konfigurieren
Erstellen Sie zur Verwendung von Google als Identitätsprovider ein Projekt in der [Google Developer Console](https://console.developers.google.com). Zum Erstellen eines Projekts gehört das Anfordern einer **Google-Client-ID** und eines **geheimen Schlüssels**. Die Google-Client-ID und der geheime Schlüssel sind die eindeutigen Kennungen für Ihre Anwendung, die von der Google-Authentifizierung verwendet werden und zum Einrichten des {{site.data.keyword.amashort}}-Dashboards erforderlich sind.


1. Öffnen Sie Ihre Google-Anwendung in der Google Developer Console. 
3. Fügen Sie die Google+-API hinzu. 
3. Erstellen Sie Berechtigungsnachweise unter Verwendung von 'OAuth'. Wählen Sie Webanwendungen als Anwendungstyp aus. Geben Sie den {{site.data.keyword.amashort}}-Weiterleitungs-URI in das Feld 'Authorized redirect URIs' ein. Der autorisierte {{site.data.keyword.amashort}}-Weiterleitungs-URI kann über die Google-Konfigurationsanzeige des {{site.data.keyword.amashort}}-Dashboards angefordert werden (siehe nachfolgende Schritte). 
6. Speichern Sie die Änderungen. Notieren Sie die Google-Client-ID und den geheimen Anwendungsschlüssel. 


## {{site.data.keyword.amashort}} für die Google-Authentifizierung konfigurieren
Wenn Sie eine Google-Anwendungs-ID und einen geheimen Schlüssel besitzen, können Sie die Google-Authentifizierung im {{site.data.keyword.amashort}}-Dashboard aktivieren.

1. Öffnen Sie Ihre App im {{site.data.keyword.Bluemix_notm}}-Dashboard.
1. Klicken Sie auf die Kachel für {{site.data.keyword.amashort}}. Das {{site.data.keyword.amashort}}-Dashboard wird geladen.
1. Klicken Sie auf die Schaltfläche in der Google-Anzeige. 
1. Gehen Sie im Abschnitt **Für Web konfigurieren** wie folgt vor:   
    * Notieren Sie den Wert im Textfeld **Mobile Client Access-Weiterleitungs-URI für Google Developer Console**. Dies ist der Wert, den Sie in das Feld **Authorized redirect URIs** unter **Restrictions in the Client ID for Web application** des **Google Developers-Portals** in Schritt 3 oben eingeben müssen.
    * Geben Sie die **Google-Client-ID** und den **geheimen Schlüssel des Clients** ein.
    * Geben Sie den Weiterleitungs-URI in das Feld **Weiterleitungs-URIs Ihrer Webanwendung** ein. Dies ist der Wert für den Weiterleitungs-URI, auf den nach Beendigung des Berechtigungsprozesses zugegriffen wird. Er wird vom Entwickler festgelegt. 
1. Klicken Sie auf **Speichern**.


## {{site.data.keyword.amashort}}-Berechtigungsablauf mit Google als Identitätsprovider implementieren

Die Umgebungsvariable `VCAP_SERVICES` wird automatisch für jede {{site.data.keyword.amashort}}-Serviceinstanz erstellt und enthält Eigenschaften, die für den Berechtigungsprozess erforderlich sind. Sie besteht aus einem JSON-Objekt und kann durch Klicken auf **Umgebungsvariablen** im Navigator auf der linken Seite Ihrer Anwendung angezeigt werden. 

Gehen Sie wie folgt vor, um den Berechtigungsprozess zu starten: 

1. Rufen Sie den Berechtigungsendpunkt (`authorizationEndpoint`) und die Client-ID (`clientId`) von den Serviceberechtigungsnachweisen ab, die in der Umgebungsvariablen `VCAP_SERVICES` gespeichert sind.  

    **Hinweis:** Wenn Sie den {{site.data.keyword.amashort}}-Service erstellt haben, bevor die Webunterstützung hinzugefügt wurde, sind möglicherweise keine Berechtigungsendpunkte in den Serviceberechtigungsnachweisen vorhanden. Verwenden Sie in diesem Fall die folgenden Berechtigungsendpunkte abhängig von Ihrer Bluemix-Region:


 	USA (Süden): 
 	```
 	https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization
 	```
 	London: 
 	```
 	https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization
  	```
  	Sydney: 
  	```
  	https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization
  	```
1. Erstellen Sie den Berechtigungsserver-URI mit `response_type("code")`, `client_id` und `redirect_uri` als Abfrageparameter. 
1. Leiten Sie von Ihrer Web-App zum generierten URI weiter.
  
Im nachfolgenden Beispiel werden die Parameter von der Variablen `VCAP_SERVICES` abgerufen, außerdem wird die URL erstellt und die Weiterleitungsanforderung wird gesendet. 
  
```Java
 var cfEnv = require("cfenv"); 
 app.get("/protected", checkAuthentication, function(req, res, next){ 
 	res.send("Hello from protected endpoint"); 
 }); 

 app.get("/protected", checkAuthentication, function(req, res, next){ 
 	res.send("Hello from protected endpoint"); 
 	function checkAuthentication(req, res, next){ 

	// Prüfen, ob Benutzer authentifiziert ist
 	if (req.session.userIdentity){
		next() 
	} else { 
		// Falls nicht - Weiterleitung an Berechtigungsserver
		var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
		var authorizationEndpoint = mcaCredentials.authorizationEndpoint;
		var clientId = mcaCredentials.clientId;
		var redirectUri = "http://some-server/oauth/callback"; // Weiterleitungs-URI Ihrer Webanwendung
		var redirectUrl = authorizationEndpoint + "?response_type=code";
		redirectUrl += "&client_id=" + clientId;
		redirectUrl += "&redirect_uri=" + redirectUri;
		res.redirect(redirectUrl);
	}
} 

  ```

Der Parameter `redirect_uri` gibt den Weiterleitungs-URI Ihrer Webanwendung an und muss mit dem im {{site.data.keyword.amashort}}-Dashboard definierten URI übereinstimmen.
Nach der Weiterleitung zum Berechtigungsendpunkt wird ein Anmeldeformular von Google angezeigt. Nachdem der Benutzer die Berechtigungen für die Anmeldung über seine Google-Identität erteilt hat, ruft der {{site.data.keyword.amashort}}-Service den Weiterleitungs-URI Ihrer Webanwendung auf und gibt den Autorisierungscode als Abfrageparameter an. 

## Tokens abrufen
Im nächsten Schritt werden Zugriffstoken und Identitätstokens mithilfe des zuvor empfangenen Autorisierungscodes abgerufen. Gehen Sie dazu wie folgt vor:  

1. Rufen Sie das Token (`tokenEndpoint`), die Client-ID (`clientId`) und den geheimen Schlüssel (`secret`) von den Serviceberechtigungsnachweisen ab, die in der Umgebungsvariablen `VCAP_SERVICES` gespeichert sind.  
  
    **Hinweis:** Wenn Sie den {{site.data.keyword.amashort}}-Service erstellt haben, bevor die Webunterstützung hinzugefügt wurde, sind möglicherweise keine Berechtigungsendpunkte in den Serviceberechtigungsnachweisen vorhanden. Verwenden Sie in diesem Fall die folgenden Berechtigungsendpunkte abhängig von Ihrer Bluemix-Region:
 
 	USA (Süden): 
 	```
 	https:// mobileclientaccess.ng.bluemix.net/oauth/v2/token 
  	```
 	London: 
  	```
  	https:// mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token  
   	```
   	Sydney: 
  	```
   	https:// mobileclientaccess.au-syd.bluemix.net/oauth/v2/token 
  	```

2. Senden Sie eine Post-Anforderung an den Token-Server-URI mit Bewilligungstyp ("authorization_code"), client_id, redirect_uri und code als Formularparameter. Senden Sie `clientId` und `clientSecret` als HTTP-Basisauthentifizierungsnachweise. 
 
Der folgende Code ruft die erforderlichen Werte ab und sendet sie mit einer Post-Anforderung. 
    
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
		redirect_uri: "http://some-server/oauth/callback",// Weiterleitungs-URI Ihrer Webanwendung
		code: req.query.code
	}

	request.post({
		url: tokenEndpoint, 
		formData: formData 
		}, function (err, response, body){ 
			var parsedBody = JSON.parse(body); 
			req.session.accessToken = parsedBody.access_token; 
			req.session.idToken = parsedBody.id_token; 
			var idTokenComponents = parsedBody.id_token.split("."); // [Header, Nutzdaten, Signatur]
			var decodedIdentity= base64url(idTokenComponents[1]);
			req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"];
			res.redirect("/");
			}
	).auth(mcaCredentials.clientId, mcaCredentials.secret); 
  }
); 
  ```

  Der Parameter `redirect_uri` entspricht dem URI für die Weiterleitung nach erfolgreicher oder fehlgeschlagener Authentifizierung bei Google+ und muss mit `redirect_uri` aus Schritt 1 übereinstimmen.  
   
Sie müssen diese POST-Anforderung innerhalb von 10 Minuten senden, da der Autorisierungscode danach abgelaufen ist. Nach 10 Minuten ist ein neuer Code erforderlich. 

Der POST-Antwortteil enthält das `Zugriffstoken` und das `ID-Token` in Base64-Codierung. 

Nachdem Sie das Zugriffstoken und das Identitätstoken empfangen haben, können Sie die Websitzung als authentifiziert markieren und optional diese Tokens speichern.   


##Abgerufenes Zugriffs- und Identitätstoken verwenden 

Das Identitätstoken enthält Informationen zu der Benutzeridentität. Bei der Google-Authentifizierung enthält das Token alle Informationen, bei denen der Benutzer eingewilligt hat, dass sie geteilt werden, wie zum Beispiel den vollständigen Namen, die URL des Profilfotos usw.   

Das Zugriffstoken ermöglicht die Kommunikation mit Ressourcen, die von den {{site.data.keyword.amashort}}-Berechtigungsfiltern geschützt werden; weitere Informationen hierzu finden Sie unter [Ressourcen schützen](protecting-resources.html).


Um Anforderungen an geschützte Ressourcen zu stellen, fügen Sie einen Berechtigungsheader mit folgender Struktur zu den Anforderungen hinzu:  

`Authorization=Bearer <accessToken> <idToken>`

**Hinweis:** 

* `accessToken` und `idToken` müssen durch ein Leerzeichen getrennt werden. 

* `idToken` ist optional. Wenn kein Identitätstoken angegeben wird, besteht zwar Zugriff auf die geschützte Ressource, es können jedoch keine Informationen zu dem berechtigten Benutzer abgerufen werden.  



