---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**Importante: il servizio {{site.data.keyword.amafull}} è stato sostituito con il servizio {{site.data.keyword.appid_full}}.**

# Utilizzo {{site.data.keyword.amashort}} con un ambiente di sviluppo locale
{: #protecting-local}

Puoi configurare il tuo sviluppo locale per utilizzare il servizio {{site.data.keyword.amafull}} che è in esecuzione su {{site.data.keyword.Bluemix}}. Nello specifico, puoi sviluppare il codice localmente utilizzando l'SDK server {{site.data.keyword.amashort}} e inviare le richieste {{site.data.keyword.amashort}} al server di sviluppo. Queste richieste saranno protette dal servizio {{site.data.keyword.amashort}} in esecuzione in {{site.data.keyword.Bluemix}}.

## Prima di cominciare
{: #before-you-begin}

È necessario disporre di:

* Un'istanza di un'applicazione  {{site.data.keyword.Bluemix_notm}} che è protetta da un servizio {{site.data.keyword.amashort}}. Per ulteriori informazioni su come creare un'applicazione di back-end {{site.data.keyword.Bluemix_notm}}, vedi [Introduzione](index.html).
* Il tuo **TenantID**. Apri il tuo servizio nel dashboard {{site.data.keyword.amafull}}. Fai clic sul pulsante **Opzioni per dispositivi mobili**. I valori `tenantId` (noti anche come `appGUID`)  vengono visualizzati nel campo **GUID applicazione / TenantId**. Avrai bisogno di questo valore per inizializzare il gestore autorizzazione.
* La tua **Rotta applicazione**. Questa è l'URL della tua applicazione di back-end. Hai bisogno di questo valore per inviare le richieste agli endpoint protetti correlati.
* La tua **Regione** {{site.data.keyword.Bluemix_notm}}.  Puoi trovare la tua regione {{site.data.keyword.Bluemix_notm}} corrente nell'intestazione, accanto all'icona **Avatar** ![Icona Avatar](images/face.jpg "Icona Avatar"). Il valore della regione visualizzato deve essere uno dei seguenti: `Stati Uniti Sud`,  `Sydney` o  `Regno Unito`. Per la sintassi esatta richiesta dall'SDK, vedi i commenti negli esempi di codice. Avrai bisogno di questo valore per inizializzare il client {{site.data.keyword.amashort}}.
* Un progetto Android Studio, configurato per lavorare con Gradle. Per ulteriori informazioni su come configurare il tuo ambiente di sviluppo Android, vedi gli [strumenti per sviluppatori Google  ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://developer.android.com/sdk/index.html){: new_window}.

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
	    application_id: "appGUID"
	}
	```
	{: codeblock}

1. Fai clic sulla scheda **Visualizza credenziali** nel dashboard {{site.data.keyword.amashort}}. Viene visualizzato un oggetto JSON con le credenziali di accesso fornite da {{site.data.keyword.amashort}} alla tua applicazione di back-end mobile.

1. Nel tuo ambiente di sviluppo locale, imposta la variabile di ambiente `VCAP_SERVICES`. Il valore della variabile deve essere un oggetto JSON convertito in stringa che contiene le credenziali {{site.data.keyword.amashort}}.  Per ulteriori informazioni, vedi il seguente esempio.

## Codice server di esempio
{: #local-dev-sample}

Per utilizzare il servizio {{site.data.keyword.amashort}} in un ambiente di sviluppo Node.js locale, aggiungi il seguente codice.  

```JavaScript
var vcapApplication = {
	application_id:"tenantID"
};

var vcapServices = {
	"AdvancedMobileAccess": [
		{
			"credentials": {
				"admin_url": "https://mobile.ng.bluemix.net/imfmobileplatformdashboard/?appGuid=appGUID",
				"clientId": "tenantID",
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
{: codeblock}

Per informazioni su come trovare il valore *tenantID*, vedi [Prima di cominciare](#before-you-begin).


## Configurazione delle applicazioni {{site.data.keyword.amashort}} per lavorare con un server di sviluppo locale
{: #configuring-local}

Inizializza gli SDK client {{site.data.keyword.amashort}} con l'URL reale della tua applicazione {{site.data.keyword.Bluemix_notm}} e utilizza l'host locale (o l'indirizzo IP) in ciascuna delle tue richieste. Consulta i seguenti esempi.

Sostituisci la regione con la regione appropriata. Vedi gli esempi di codice per conoscere la sintassi corretta.

Sostituisci i valori *appGUID* e *bluemixAppRoute*. Per informazioni su come ottenere questi valori, consulta [Prima di cominciare](#before-you-begin).

Nei seguenti esempi, potresti dover modificare `localhost` in un indirizzo IP effettivo del tuo server di sviluppo.

### Android
{: #android}

```Java
String baseRequestUrl = "http://localhost:3000";
String bluemixAppRoute = "http://myapp.mybluemix.net";
String bluemixAppGUID = "your-bluemix-app-guid";
String tenantId = "your-MCA-service-tenantID";


BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

//  set your MCA application region here. Currently possible values are BMSClient.REGION_US_SOUTH, BMSClient.REGION_SYDNEY, or BMSClient.REGION_UK

BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));

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
{: codeblock}


### iOS - Swift
{: #swift}

```Swift

 let baseRequestUrl = "http://localhost:3000";
 let tenantId = "<serviceTenantID>"
 let regionName = <applicationBluemixRegion>
 //possible values: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney
 let mcaAuthManager = MCAAuthorizationManager.sharedInstance
 mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
 BMSClient.sharedInstance.authorizationManager = mcaAuthManager


 let requestPath = baseRequestUrl + "/protectedResource"
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
{: codeblock}


### Cordova
{: #cordova}

```JavaScript
var baseRequestUrl = "http://localhost:3000";
var bluemixAppRoute = "http://myapp.mybluemix.net";
var bluemixAppGUID = "your-bluemix-app-guid";
Var tenantId = "your-MCA-service-tenantID";

BMSClient.initialize(<applicationBluemixRegion>);

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
{: codeblock}
