---

copyright:
  years: 2015, 2016
  
---

# Kommunikation zwischen Back-Ends
{: #backend-comm}

In einigen erweiterten Szenarios müssen Sie möglicherweise Anforderungen aus Ihrer Back-End-Anwendung, die in {{site.data.keyword.Bluemix}} ausgeführt wird, an einen anderen Back-End-Service senden, der durch den {{site.data.keyword.amashort}}-Service geschützt wird (z. B. an den {{site.data.keyword.cloudant}}-Service). In diesen Fällen müssen Sie der Anforderung das OAuth-Token hinzufügen.

Verwenden Sie das NPMJS-Modul `bms-mca-oauth-sdk`, um OAuth-Tokens abzurufen und in Anforderungen einzufügen.

## Modul 'bms-mca-oauth-sdk' installieren
{: #sdk}

Öffnen Sie in einer Befehlszeile das Verzeichnis der Node.js-Anwendung und führen Sie den folgenden Befehl aus:

```Bash
npm install -save bms-mca-oauth-sdk
```

## Modul 'bms-mca-oauth-sdk' verwenden
{: #using-sdk}

Der folgende Code demonstriert, wie das Modul `bms-mca-oauth-sdk` verwendet wird.


``` JavaScript
var oauthSDK = require('bms-mca-oauth-sdk');

var options = {

	// Tokens können im Cache gespeichert werden, um zusätzliche Umläufe
 // bei jeder Anforderung zu vermeiden.
	// Diese Eigenschaft definiert die Anzahl Token, die im Cache gespeichert werden.

	cacheSize: 100,

	// Alle folgenden Eigenschaften werden automatisch abgerufen, wenn Ihre Node.js
	// in {{site.data.keyword.Bluemix_notm}} aktiv ist und an eine Instanz des
 // {{site.data.keyword.amashort}}-Service gebunden ist.
	// Alternativ können Sie diese Eigenschaftswerte ermitteln, indem Sie auf
	// 'Berechtigungsnachweise anzeigen' auf der Kachel für den {{site.data.keyword.amashort}}-Service
 // in Ihrem {{site.data.keyword.Bluemix_notm}}-Anwendungsdashboard klicken.

	appId: "appId",				// Bluemix applicationGUID, auch: tenantId
	clientId: "clientId",			
	secret: "secret",
	serverUrl: "serverUrl"
};

oauthSDK.getAuthorizationHeader(options).then(function(authHeader){

	// In der Anforderung, die an die geschützte Ressource gesendet werden soll,
// den Wert 'authHeader' hinzufügen.

	request.headers.Authorization = authHeader;

	// Anforderung senden

});

```
