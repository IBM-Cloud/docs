---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-07"

---
{:shortdesc: .shortdesc}

# Utilizzo {{site.data.keyword.amashort}} con un ambiente di sviluppo locale
{: #protecting-local}

Puoi configurare il tuo sviluppo locale per utilizzare il servizio {{site.data.keyword.amafull}} che è in esecuzione su {{site.data.keyword.Bluemix}}. Nello specifico, puoi sviluppare il codice localmente utilizzando l'SDK server {{site.data.keyword.amashort}} e inviare le richieste {{site.data.keyword.amashort}} al server di sviluppo. Queste richieste saranno protette dal servizio {{site.data.keyword.amashort}} in esecuzione in {{site.data.keyword.Bluemix}}.

## Prima di cominciare
{: #before-you-begin}

È necessario disporre di:
* Un'istanza di un'applicazione  {{site.data.keyword.Bluemix_notm}} che è protetta da un servizio {{site.data.keyword.amashort}}. Per ulteriori informazioni su come creare un'applicazione di back-end {{site.data.keyword.Bluemix_notm}}, vedi [Introduzione](index.html).
* I valori del parametro del servizio. Apri il tuo servizio nel dashboard {{site.data.keyword.amashort}}. Fai clic su **Opzioni mobili**. I valori `applicationRoute` e `appGUID` (conosciuti anche come `tenantId`)  sono visualizzati nei campi **Rotta** and **GUID applicazione / TenantId**. Avrai bisogno di questi valori per inizializzare l'SDK e per inviare le richieste all'applicazione di backend.
*  Trova la regione in cui è ospitata la tua applicazione {{site.data.keyword.Bluemix_notm}}. Per visualizzare la tua regione {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona **Avatar** ![icona Avatar](images/face.jpg "icona Avatar")  nella barra del menu per aprire il widget **Account e supporto**. Il valore della regione deve essere uno dei seguenti: **Stati Uniti Sud**, **Sydney** o **UK**. I valori costanti della SDK esatti che corrispondono a tali nomi sono indicati negli esempi di codice.

## Configurazione dell'SDK server
{: #serversetup}

L'SDK server {{site.data.keyword.amashort}} richiede che siano impostate due variabili di ambiente. Quando stai sviluppando codice lato server su {{site.data.keyword.Bluemix_notm}}, queste variabili vengono fornite dall'infrastruttura {{site.data.keyword.Bluemix_notm}}.

* `VCAP_SERVICES`: contiene informazioni sui servizi associati mediante bind all'applicazione di back-end mobile.
* `VCAP_APPLICATION`: contiene informazioni sull'applicazione di back-end mobile.

Per utilizzare {{site.data.keyword.amashort}} con un ambiente di sviluppo locale, devi aggiungere manualmente queste variabili di ambiente.

1. Apri il dashboard {{site.data.keyword.Bluemix_notm}} della tua applicazione di backend mobile che è protetto con il servizio {{site.data.keyword.amashort}}.

1. Nel tuo ambiente di sviluppo locale, imposta la variabile di ambiente *VCAP_APPLICATION*. La variabile deve contenere un oggetto JSON convertito in stringa con una singola proprietà.
```JavaScript
{
    application_id:"appGUID"
}
```

Sostituisci il valore *appGUID* con il valore `appGUID` ottenuto in [Prima di cominciare](#before-you-begin).

1. Fai clic su **Visualizza credenziali** sul tile del servizio {{site.data.keyword.amashort}} nella tua applicazione di backend mobile sul dashboard {{site.data.keyword.Bluemix_notm}}. Viene visualizzato un oggetto JSON con le credenziali di accesso fornite da {{site.data.keyword.amashort}} alla tua applicazione di back-end mobile.

1. Nel tuo ambiente di sviluppo locale, imposta la variabile di ambiente `VCAP_SERVICES`. Il valore della variabile deve essere un oggetto JSON convertito in stringa che contiene le credenziali {{site.data.keyword.amashort}}.  Per ulteriori informazioni, vedi il seguente esempio.

## Codice server di esempio
{: #local-dev-sample}

Per utilizzare il servizio {{site.data.keyword.amashort}} in un ambiente di sviluppo Node.js locale, aggiungi il seguente codice.  

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
				"tenantId": "tenantId"
			}
		}
	]
};

process.env["VCAP_APPLICATION"] = JSON.stringify(vcapApplication);
process.env["VCAP_SERVICES"] = JSON.stringify(vcapServices);

// Ora puoi richiedere il modulo bms-mca-token-validation-strategy:
var MCABackendStrategy =
	require('bms-mca-token-validation-strategy').MCABackendStrategy;

// Il resto del tuo codice
```

Sostituisci il valore *appGUID* con il valore `appGUID` (consulta [Prima di cominciare](#before-you-begin)).


## Configurazione delle applicazioni {{site.data.keyword.amashort}} per lavorare con un server di sviluppo locale
{: #configuring-local}

Inizializza gli SDK client {{site.data.keyword.amashort}} con l'URL reale della tua applicazione {{site.data.keyword.Bluemix_notm}} e utilizza l'host locale (o l'indirizzo IP) in ciascuna delle tue richieste. Consulta i seguenti esempi.

Sostituisci la regione con la regione appropriata.

Sostituisci i valori *appGUID* e *bluemixAppRoute* con i valori ottenuti in [Prima di cominciare](#before-you-begin).

Nei seguenti esempi, potresti dover modificare `localhost` in un indirizzo IP effettivo del tuo server di sviluppo.

### Android
{: #android}
```Java
String baseRequestUrl = "http://localhost:3000";
String bluemixAppRoute = "http://myapp.mybluemix.net";
String bluemixAppGUID = "your-bluemix-app-guid";
String tenantId = "your-MCA-service-tenantID";

BMSClient.getInstance().initialize(bluemixAppRoute, bluemixAppGUID, BMSClient.REGION_UK);
//  imposta qui la regione della tua applicazione MCA. I valori possibili al momento sono BMSClient.REGION_US_SOUTH, BMSClient.REGION_SYDNEY o BMSClient.REGION_UK
BMSClient.getInstance().setAuthorizationManager(
                 MCAAuthorizationManager.createInstance(this, tenantId));

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



### iOS - Objective C
{: #objc}

```Objective-C
NSString *baseRequestUrl = @"http://localhost:3000";
NSString *bluemixAppRoute = @"http://myapp.mybluemix.net";
NSString *bluemixAppGUID = @"your-bluemix-app-guid";
NSString *tenantId = "your-MCA-service-tenantID";

[[IMFClient sharedInstance]
			initializeWithBackendRoute:bluemixAppRoute
			backendGUID:bluemixAppGUID];

[[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: tenantId];


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
{: #swift}

```Swift

let baseRequestUrl = "http://localhost:3000"
let bluemixAppRoute = "http://myapp.mybluemix.net"
let tenantId = "your-MCA-service-tenantID"
let regionName = BMSClient.Region.usSouth
// imposta qui la regione della tua applicazione MCA. Al momento può essere BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, BMSClient.Region.sydney

BMSClient.sharedInstance.initialize(bluemixAppRoute: bluemixAppRoute, bluemixAppGUID: tenantId, bluemixRegion: regionName)

BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

let requestPath = baseRequestUrl + "/resource/path"               
let request = Request(url: requestPath, method: HttpMethod.GET)

request.send { (response, error) in
	if let error = error {
    			print("Connection failure")
     		print("Error :: \(error)");
     		print("Status :: \(response?.statusCode)");
    	} else {
           print("Connection success")
           print("Response :: \(response?.responseText)")
    }                
}



```


### Cordova
{: #cordova}

```JavaScript
var baseRequestUrl = "http://localhost:3000";
var bluemixAppRoute = "http://myapp.mybluemix.net";
var bluemixAppGUID = "your-bluemix-app-guid";
Var tenantId = "your-MCA-service-tenantID";

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
