---

copyright:
  years: 2015, 2016

---

# Utilizzo {{site.data.keyword.amashort}} con un ambiente di sviluppo locale
{: #protecting-local}

Puoi configurare il tuo ambiente di sviluppo locale per utilizzare il servizio {{site.data.keyword.amashort}} che è in esecuzione su {{site.data.keyword.Bluemix}}. Specificamente, puoi utilizzare l'SDK server {{site.data.keyword.amashort}} quando stai sviluppando codice lato server con un server di sviluppo locale, come ad esempio Node.js.

L'SDK server {{site.data.keyword.amashort}} richiede che siano impostate due variabili di ambiente. Quando stai sviluppando codice lato server su {{site.data.keyword.Bluemix_notm}}, queste variabili vengono fornite dall'infrastruttura {{site.data.keyword.Bluemix_notm}}.

* `VCAP_SERVICES`: contiene informazioni sui servizi associati mediante bind all'applicazione di backend mobile.
* `VCAP_APPLICATION`: contiene informazioni sull'applicazione di backend mobile.

Per utilizzare {{site.data.keyword.amashort}} con un ambiente di sviluppo locale, devi aggiungere manualmente queste variabili di ambiente.

1. Apri il dashboard {{site.data.keyword.Bluemix_notm}} del tuo backend mobile che è protetto con il servizio {{site.data.keyword.amashort}}.

1. Fai clic su **Opzioni mobili** e copia il valore **AppGUID**.

1. Nel tuo ambiente di sviluppo locale, imposta la variabile di ambiente *VCAP_APPLICATION*. La variabile deve contenere un oggetto JSON convertito in stringa con una singola proprietà.
```JavaScript
{
    application_id:"appGUID"
}
```
Sostituisci la variabile *appGUID* con il valore dal campo **Opzioni mobili**.

1. Fai clic su **Visualizza credenziali** sul tile del servizio {{site.data.keyword.amashort}} nella tua applicazione di backend mobile
sul dashboard {{site.data.keyword.Bluemix_notm}}. Viene visualizzato un oggetto JSON con le credenziali di accesso fornite da {{site.data.keyword.amashort}} alla tua applicazione di backend mobile.

1. Nel tuo ambiente di sviluppo locale, imposta la variabile di ambiente `VCAP_SERVICES`. Il valore della variabile deve essere un oggetto JSON convertito in stringa che contiene le credenziali {{site.data.keyword.amashort}}.  Per ulteriori informazioni, vedi il seguente esempio.

## Codice di esempio
{: #local-dev-sample}

Per utilizzare il servizio {{site.data.keyword.amashort}} in un ambiente di sviluppo Node.js locale, aggiungi il seguente codice prima di richiedere il modulo `bms-mca-token-validation-strategy`.

```JavaScript
var vcapApplication = {
	application_id:"appGUID"
};

var vcapServices = {
	"AdvancedMobileAccess": [
		{
			"credentials": {
				"admin_url": "https://mobile.ng.bluemix.net/imfmobileplatformdashboard/?appGuid=appGUID",
				"clientId": "appGUID",
				"secret": "secret",
				"serverUrl": "https://imf-authserver.ng.bluemix.net/imf-authserver",
				"tenantId": "appGUID"
			}
		}
	]
};

process.env["VCAP_APPLICATION"] = JSON.stringify(vcapApplication);
process.env["VCAP_SERVICES"] = JSON.stringify(vcapServices);

var MCABackendStrategy =
	require('bms-mca-token-validation-strategy').MCABackendStrategy;

// Il resto del tuo codice
```
Sostituisci le ricorrenze del valore *appGUID* nel codice con il valore *appGUID* di backend mobile.


## Configurazione delle applicazioni mobili per lavorare con un server di sviluppo locale
{: #configuring-local}

Inizializza gli SDK client {{site.data.keyword.amashort}} con l'URL reale della tua applicazione {{site.data.keyword.Bluemix_notm}} e utilizza l'host locale (o l'indirizzo IP) in ciascuna delle tue richieste. Consulta i seguenti esempi.

Nei seguenti esempi, potresti dover modificare `localhost` in un indirizzo IP effettivo del tuo server di sviluppo.

### Android

```Java
String baseRequestUrl = "http://localhost:3000";
String bluemixAppRoute = "http://myapp.mybluemix.net";
String bluemixAppGUID = "il-tuo-guid-applicazione-bluemix";

BMSClient.getInstance().initialize(bluemixAppRoute, bluemixAppGUID);

Request request =
			new Request(baseRequestUrl + "/resource/path", Request.GET);

request.send(this, new ResponseListener() {
	@Override
	public void onSuccess (Response response) {
		Log.d("Myapp", "onSuccess :: " + response.getResponseText());
	}
	@Override
	public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
		if (null != t) {
			Log.d("Myapp", "onFailure :: " + t.getMessage());
		} else if (null != extendedInfo) {
			Log.d("Myapp", "onFailure :: " + extendedInfo.toString());
		} else {
			Log.d("Myapp", "onFailure :: " + response.getResponseText());
		}
	}
});
```
### Cordova

```JavaScript
var baseRequestUrl = "http://localhost:3000";
var bluemixAppRoute = "http://myapp.mybluemix.net";
var bluemixAppGUID = "il-tuo-guid-applicazione-bluemix";

BMSClient.initialize(bluemixAppRoute, bluemixAppGUID);

var success = function(data){
   	console.log("success", data);
}

var failure = function(error){
	console.log("failure", error);
}

var request = new MFPRequest(baseRequestUrl +
							"/resource/path", MFPRequest.GET);

request.send(success, failure);
```

### iOS - Objective C

```Objective-C
NSString *baseRequestUrl = @"http://localhost:3000";
NSString *bluemixAppRoute = @"http://myapp.mybluemix.net";
NSString *bluemixAppGUID = @"il-tuo-guid-applicazione-bluemix";

[[IMFClient sharedInstance]
			initializeWithBackendRoute:bluemixAppRoute
			backendGUID:bluemixAppGUID];

NSString *requestPath = [NSString stringWithFormat:@"%@/resource/path",
								baseRequestUrl];

IMFResourceRequest *request =  [IMFResourceRequest
				requestWithPath:requestPath
				method:@"GET"];

[request sendWithCompletionHandler:^(IMFResponse *response, NSError *error) {
	if (error){
		NSLog(@"Error :: %@", [error description]);
	} else {
		NSLog(@"Response :: %@", [response responseText]);
	}
}];
```

### iOS - Swift

```Swift
let baseRequestUrl = "http://localhost:3000";
let bluemixAppRoute = "http://myapp.mybluemix.net";
let bluemixAppGUID = "il-tuo-guid-applicazione-bluemix";

IMFClient.sharedInstance().initializeWithBackendRoute(bluemixAppRoute,
	 							backendGUID: bluemixAppGuid)

let requestPath = baseRequestUrl + "/resource/path"

let request = IMFResourceRequest(path: requestPath, method: "GET");

request.sendWithCompletionHandler { (response, error) -> Void in
	if (nil != error){
		NSLog("Error :: %@", error.description)
	} else {
		NSLog("Response :: %@", response.responseText)
	}
};

```
