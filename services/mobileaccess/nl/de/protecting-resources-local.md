---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-08"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# {{site.data.keyword.amashort}} mit einer lokalen Entwicklungsumgebung verwenden
{: #protecting-local}

Sie können Ihre lokale Entwicklungsumgebung so konfigurieren, dass sie den {{site.data.keyword.amafull}}-Service verwendet, der in {{site.data.keyword.Bluemix}} ausgeführt wird. Insbesondere können Sie Code mit dem {{site.data.keyword.amashort}}-Server-SDK lokal entwickeln und {{site.data.keyword.amashort}}-Anforderungen an den Entwicklungsserver senden. Diese Anforderungen werden vom {{site.data.keyword.amashort}}-Service geschützt, der in {{site.data.keyword.Bluemix}} ausgeführt wird.

## Vorbereitungen
{: #before-you-begin}

Voraussetzungen:

* Instanz einer {{site.data.keyword.Bluemix_notm}}-Anwendung, die durch den {{site.data.keyword.amashort}}-Service geschützt ist. Weitere Informationen zur Erstellung einer {{site.data.keyword.Bluemix_notm}}-Back-End-Anwendung finden Sie in der [Einführung](index.html).
* Die **Tenant-ID**. Öffnen Sie den Service im {{site.data.keyword.amafull}}-Dashboard. Klicken Sie auf die Schaltfläche **Mobile Systemerweiterungen**. Im Feld **App-GUID/TenantId** wird der Wert `tenantId` (auch als `appGUID` bezeichnet) angezeigt. Sie benötigen diesen Wert für die Initialisierung von Authorization Manager.
* Die **Anwendungsroute**. Dies ist die URL Ihrer Back-End-Anwendung. Sie benötigen diesen Wert zum Senden von Anforderungen an die geschützten Endpunkte der Anwendung.
* Die {{site.data.keyword.Bluemix_notm}}-**Region**.  Ihre aktuelle {{site.data.keyword.Bluemix_notm}}-Region finden Sie im Header neben dem Symbol **Avatar** ![Avatarsymbol](images/face.jpg "Avatarsymbol"). Der angezeigte Regionswert muss einer der folgenden sein: `USA (Süden)`, `Sydney` oder `Vereinigtes Königreich`. Die genaue, für SDK erforderliche Syntax finden Sie bei den Kommentaren in den Codebeispielen. Sie benötigen diesen Wert für die Initialisierung des {{site.data.keyword.amashort}}-Clients.
* Android Studio-Projekt, das für das Arbeiten mit Gradle eingerichtet ist. Weitere Informationen zur Einrichtung Ihrer Android-Entwicklungsumgebung finden Sie in [Google Developer Tools ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://developer.android.com/sdk/index.html "Symbol für externen Link"){: new_window}.

## Server-SDK einrichten
{: #serversetup}

Das {{site.data.keyword.amashort}}-Server-SDK setzt voraus, dass zwei Umgebungsvariablen festgelegt werden. Wenn Sie serverseitigen Code in {{site.data.keyword.Bluemix_notm}} entwickeln, werden diese Variablen von der {{site.data.keyword.Bluemix_notm}}-Infrastruktur bereitgestellt.

* `VCAP_SERVICES`: Enthält Informationen zu Services, die an die mobile Back-End-Anwendung gebunden sind.
* `VCAP_APPLICATION`: Enthält Informationen zur mobilen Back-End-Anwendung.

Zur Verwendung von {{site.data.keyword.amashort}} mit einem lokalen Entwicklungsserver müssen Sie diese Umgebungsvariablen manuell hinzufügen.

1. Öffnen Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard Ihrer mobilen Back-End-Anwendung, die mit dem {{site.data.keyword.amashort}}-Service geschützt wird.

1. Legen Sie in Ihrer lokalen Entwicklungsumgebung die Umgebungsvariable *VCAP_APPLICATION* fest. Die Variable muss ein in eine Zeichenfolge konvertiertes JSON-Objekt mit einer einzelnen Eigenschaft enthalten.
	```JavaScript
	{
	    application_id: "appGUID"
	}
	```
	{: codeblock}

1. Klicken Sie im {{site.data.keyword.amashort}}-Dashboard auf **Berechtigungsnachweise anzeigen**. Es wird ein JSON-Objekt mit Zugriffsberechtigungsnachweisen angezeigt, die {{site.data.keyword.amashort}} für Ihre mobile Back-End-Anwendung bereitstellt.

1. Legen Sie in Ihrer lokalen Entwicklungsumgebung die Umgebungsvariable `VCAP_SERVICES` fest. Der Wert dieser Variablen muss ein in eine Zeichenfolge konvertiertes JSON-Objekt sein, das die {{site.data.keyword.amashort}}-Berechtigungsnachweise enthält.  Weitere Informationen finden Sie im folgenden Beispiel.

## Beispielservercode
{: #local-dev-sample}

Zur Verwendung des {{site.data.keyword.amashort}}-Service in einer lokalen Node.js-Entwicklungsumgebung fügen Sie den folgenden Code hinzu.  

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

// Nun können Sie das Modul bms-mca-token-validation-strategy anfordern:
var MCABackendStrategy =
	require('bms-mca-token-validation-strategy').MCABackendStrategy;

// Restlicher Code
```
{: codeblock}

Informationen zum Suchen nachdem Wert für *tenantID* finden Sie in [Vorbereitungen](#before-you-begin).


## {{site.data.keyword.amashort}}-Anwendungen zur Arbeit mit einem lokalen Entwicklungsserver konfigurieren
{: #configuring-local}

Initialisieren Sie die {{site.data.keyword.amashort}}-Client-SDKs mit der realen URL Ihrer {{site.data.keyword.Bluemix_notm}}-Anwendung und verwenden Sie den lokalen Host (localhost) oder die IP-Adresse in jeder Ihrer Anforderungen. Weitere Informationen finden Sie in den folgenden Beispielen.

Ersetzen Sie die Region durch die richtige Region. Die korrekte Syntax finden Sie in den Codebeispielen.

Ersetzen Sie die Werte *appGUID* und *bluemixAppRoute*. Informationen zum Abrufen dieser Werte finden Sie unter [Vorbereitungen](#before-you-begin).

Es ist möglich, dass Sie `localhost` in den folgenden Beispielen in die tatsächliche IP-Adresse Ihres Entwicklungsservers ändern müssen.

### Android
{: #android}

```Java
String baseRequestUrl = "http://localhost:3000";
String bluemixAppRoute = "http://myapp.mybluemix.net";
String bluemixAppGUID = "your-bluemix-app-guid";
String tenantId = "your-MCA-service-tenantID";


BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

//  MCA-Anwendungsregion hier festlegen. Aktuell mögliche Werte sind: BMSClient.REGION_US_SOUTH, BMSClient.REGION_SYDNEY odr BMSClient.REGION_UK

BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));

Request request = new Request(baseRequestUrl + "/resource/path", Request.GET);

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
 //Mögliche Werte: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom oder BMSClient.Region.sydney
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
