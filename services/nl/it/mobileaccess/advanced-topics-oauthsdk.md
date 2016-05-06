---

copyright:
  years: 2015, 2016
  
---

# Comunicazioni backend-backend
{: #backend-comm}

In alcuni scenari avanzati, potresti dover inviare richieste dalla tua applicazione di backend in esecuzione su {{site.data.keyword.Bluemix}} a un altro servizio di backend protetto dal servizio {{site.data.keyword.amashort}}, ad esempio il servizio {{site.data.keyword.cloudant}}). In questi casi, devi aggiungere un token OAuth alla richiesta.

Utilizza il modulo npmjs `bms-mca-oauth-sdk` per ottenere e inserire i token OAuth nelle richieste.

## Installazione del modulo bms-mca-oauth-sdk
{: #sdk}

Su una riga di comando, apri la directory dell'applicazione Node.js ed esegui questo comando:

```Bash
npm install -save bms-mca-oauth-sdk
```

## Utilizzo del modulo bms-mca-oauth-sdk
{: #using-sdk}

Il seguente codice illustra come utilizzare il modulo `bms-mca-oauth-sdk`.


``` JavaScript
var oauthSDK = require('bms-mca-oauth-sdk');

var options = {

	// Puoi memorizzare in cache i token per evitare roundtrip supplementari su ogni richiesta
	// Questa proprietà definisce il numero di token da memorizzare in cache

	cacheSize: 100,

	// Tutte le proprietà di seguito indicate vengono recuperate automaticamente quando il tuo Node.js
	// viene eseguito su {{site.data.keyword.Bluemix_notm}} e associato mediante bind a un'istanza del servizio {{site.data.keyword.amashort}}.
	// In alternativa, puoi ottenere i valori di queste proprietà facendo clic su Visualizza credenziali
	// sul tile del servizio {{site.data.keyword.amashort}} nel tuo dashboard dell'applicazione {{site.data.keyword.Bluemix_notm}}

	appId: "appId",				// applicationGUID Bleumix, noto anche come tenantId
	clientId: "clientId",			
	secret: "secret",
	serverUrl: "serverUrl"
};

oauthSDK.getAuthorizationHeader(options).then(function(authHeader){

	// Nella richiesta che vuoi inviare alla risorsa protetta,
	// aggiungi il valore authHeader.

	request.headers.Authorization = authHeader;

	// Inviare la richiesta

});

```
