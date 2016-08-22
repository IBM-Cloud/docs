---

copyright:
  years: 2016

---

#Angepasste Authentifizierung für {{site.data.keyword.amashort}}-Webanwendungen konfigurieren
{: #custom-web}

*Letzte Aktualisierung: 18. Juli 2016*
{: .last-updated}

Sie können Ihrer {{site.data.keyword.amashort}}-Web-App eine angepasste Authentifizierung hinzufügen. 

## Vorbereitungen
{: #before-you-begin}
Voraussetzungen:

*	Web-App. 
*	Instanz einer {{site.data.keyword.Bluemix_notm}}-Anwendung, die durch den {{site.data.keyword.amashort}}-Service geschützt ist. Weitere Informationen zur Erstellung einer {{site.data.keyword.Bluemix_notm}}-Back-End-Anwendung finden Sie in der [Einführung in {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html). 
*	URI für die letzte Weiterleitung (nach Beendigung des Berechtigungsprozesses).


Weitere Informationen finden Sie über die folgenden Links:
 * [Einführung in {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Angepassten Identitätsprovider verwenden](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Angepassten Identitätsprovider erstellen](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [{{site.data.keyword.amashort}} für die angepasste Authentifizierung konfigurieren](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


##Angepassten Identitätsprovider konfigurieren 

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

**Hinweis:** Das Feld `attributes` ist optional. 

Der folgende Code veranschaulicht eine solche Post-Anforderung. 

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


##{{site.data.keyword.amashort}} für eine angepasste Authentifizierung konfigurieren 

Nach der Konfiguration des angepassten Identitätsproviders können Sie die angepasste Authentifizierung im {{site.data.keyword.amashort}}-Dashboard aktivieren.  

1. Öffnen Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard. 
2. Klicken Sie auf die entsprechende Kachel für die {{site.data.keyword.amashort}}-Anwendung. Das App-Dashboard wird geladen.  
3. Klicken Sie auf die Schaltfläche **Konfigurieren** der Kachel 'Angepasst'. 
4. Geben Sie im Textfeld **Realmname** den Realmnamen ein, der im Handlerendpunkt Ihres angepassten Identitätsproviders konfiguriert ist. 
5. Geben Sie die URL des angepassten Identitätsproviders ein.  
6. Geben Sie den Weiterleitungs-URI der Webanwendung ein, der vom {{site.data.keyword.amashort}}-Dashboard nach der erfolgreichen Authentifizierung verwendet werden soll.  
7. Klicken Sie auf 'Speichern'. 


##{{site.data.keyword.amashort}}-Berechtigungsablauf mit einem angepassten Identitätsprovider implementieren 

Die Umgebungsvariable `VCAP_SERVICES` wird automatisch für jede {{site.data.keyword.amashort}}-Serviceinstanz erstellt und enthält Eigenschaften, die für den Berechtigungsprozess erforderlich sind. Sie besteht aus einem JSON-Objekt und kann durch Klicken auf **Umgebungsvariablen** im Navigator auf der linken Seite Ihrer Anwendung angezeigt werden. 

Wenn Sie eine Benutzerberechtigung anfordern wollen, leiten Sie den Browser an den Endpunkt des Berechtigungsservers weiter. Gehen Sie dazu wie folgt vor:  

1. Rufen Sie den Berechtigungsendpunkt (`authorizationEndpoint`) und die Client-ID (`clientId`) von den Serviceberechtigungsnachweisen ab, die in der Umgebungsvariablen `VCAP_SERVICES` gespeichert sind.  

  **Hinweis:** Wenn Sie den Mobile Client Access-Service vor der Webunterstützung zur Ihrer Anwendung hinzugefügt haben, ist möglicherweise kein Tokenendpunkt in den Serviceberechtigungsnachweisen enthalten. Verwenden Sie stattdessen die nachfolgenden URLs abhängig von Ihrer {{site.data.keyword.Bluemix_notm}}-Region:  
 
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
2. Erstellen Sie den Berechtigungsserver-URI mit `response_type("code")`, `client_id` und `redirect_uri` als Abfrageparameter.   
1. Leiten Sie von Ihrer Web-App zum generierten URI weiter. 

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
    // Falls nicht - an Berechtigungsserver weiterleiten
    var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
    var authorizationEndpoint = mcaCredentials.authorizationEndpoint;
    var clientId = mcaCredentials.clientId;
    var redirectUri = "http://some-server/oauth/callback"; // Ihr Weiterleitungs-URI für die Webanwendung
    var redirectUrl = authorizationEndpoint + "?response_type=code";
    redirectUrl += "&client_id=" + clientId;
    redirectUrl += "&redirect_uri=" + redirectUri;
    res.redirect(redirectUrl);
  }

} 

 ```
 
Der Parameter `redirect_uri` gibt den Weiterleitungs-URI Ihrer Webanwendung an und muss mit dem im {{site.data.keyword.amashort}}-Dashboard definierten URI übereinstimmen.
  

Ein Parameter `state` kann zusammen mit der Anforderung übergeben werden. Dieser Parameter wird an die POST-Methode des angepassten Identitätsproviders weitergegeben und kann über den Anforderungshauptteil (`req.body.stateId`) abgerufen werden.  

Nach der Weiterleitung zum Berechtigungsendpunkt wird ein Anmeldeformular angezeigt. Nachdem die Berechtigungsnachweise des Benutzers vom angepassten Identitätsprovider authentifiziert wurden, ruft der {{site.data.keyword.amashort}}-Service den Weiterleitungs-URI Ihrer Webanwendung auf und gibt den Autorisierungscode als Abfrageparameter an.   

Nach der Weiterleitung wird ein Anmeldeformular angezeigt. Nachdem die Berechtigungsnachweise des Benutzers vom angepassten Identitätsprovider authentifiziert wurden, ruft der {{site.data.keyword.amashort}}-Service den Weiterleitungs-URI der Webanwendung auf und gibt den Autorisierungscode als Abfrageparameter an.  

##Tokens abrufen

Im nächsten Schritt werden das Zugriffstoken und das Identitätstoken mithilfe des zuvor empfangenen Autorisierungscodes abgerufen. Gehen Sie dazu wie folgt vor:  

1. Rufen Sie `authorizationEndpoint`, `clientId` und `secret` von den Serviceberechtigungsnachweisen ab, die in der Umgebungsvariablen `VCAP_SERVICES` gespeichert sind.  

   **Hinweis:** Wenn Sie den Mobile Client Access-Service vor der Webunterstützung zu Ihrer Anwendung hinzugefügt haben, ist möglicherweise kein Tokenendpunkt in den Serviceberechtigungsnachweisen enthalten. Verwenden Sie in diesem Fall die nachfolgenden URLs abhängig von Ihrer Bluemix-Region:  

 USA (Süden): 
 ```
     https://mobileclientaccess.ng.bluemix.net/oauth/v2/token   
 ```
 London: 
 ```
     https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token
 ``` 
 Sydney: 
 ``` 
     https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token 
 ```
1. Senden Sie eine Post-Anforderung an den Token-Server-URI mit `grant_type`, `client_id`, `redirect_uri` und `code` als Formularparameter sowie `clientId` und `secret` als HTTP-Basisauthentifizierungsnachweise. 


Der Code im folgenden Beispiel ruft die erforderlichen Werte ab und sendet sie mit einer Post-Anforderung. 


 ```Java
var cfEnv = require("cfenv");
var base64url = require("base64url ");
app.get("/oauth/callback", function(req, res, next){ 
    var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials; 
    var tokenEndpoint = mcaCredentials.tokenEndpoint; 

    var formData = { 
      grant_type: "authorization_code",
      client_id: mcaCredentials.clientId,
      redirect_uri: "http://some-server/oauth/callback",   // Weiterleitungs-URI Ihrer Webanwendung
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
Beachten Sie, dass der Parameter `redirect_uri` mit dem Parameter `redirect_uri` aus der vorhergehenden Berechtigungsanforderung übereinstimmen muss. Als Wert für den Parameter 'code' muss der Autorisierungscode angegeben werden, der in der Antwort am Ende der Autorisierungsanforderung empfangen wurde. Der Autorisierungscode ist nur 10 Minuten gültig, danach muss ein neuer Code abgerufen werden.

Der Antworthauptteil enthält die Parameter `access_token` und `id_token` in JWT-Format (https://jwt.io/).

Nachdem Sie das Zugriffstoken und das Identitätstoken empfangen haben, können Sie die Websitzung als authentifiziert markieren und optional diese Tokens speichern. 

##Abgerufenes Zugriffs- und Identitätstoken verwenden 

Das Identitätstoken enthält Informationen zu der Benutzeridentität. Bei einer angepassten Authentifizierung enthält das Token alle Informationen, die vom angepassten Identitätsprovider bei der Authentifizierung zurückgegeben werden. Das Feld `displayName` unter `imf.user` enthält den `Anzeigenamen`, der vom angepassten Identitätsprovider zurückgegeben wurde, und das Feld `id` enthält den `Benutzernamen`. Alle anderen vom angepassten Identitätsprovider zurückgegebenen Werte werden im Feld `attributes` unter `imf.user` zurückgegeben.  

Das Zugriffstoken ermöglicht die Kommunikation mit Ressourcen, die von den Mobile Client Access-Berechtigungsfiltern geschützt werden (siehe [Ressourcen schützen](protecting-resources.html)). Um Anforderungen an geschützte Ressourcen zu stellen, fügen Sie einen Berechtigungsheader mit folgender Struktur zu den Anforderungen hinzu:  

`Authorization=Bearer <accessToken> <idToken>` 

**Hinweis:** 

* `<accessToken>` und `<idToken>` müssen durch ein Leerzeichen getrennt werden. 

* Das Identitätstoken ist optional. Wenn kein Identitätstoken angegeben wird, besteht zwar Zugriff auf die geschützte Ressource, es können jedoch keine Informationen zu dem berechtigten Benutzer abgerufen werden.  



