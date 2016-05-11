---

copyright:
  years: 2015, 2016

---

# {{site.data.keyword.amashort}} mit einer lokalen Entwicklungsumgebung verwenden
{: #protecting-local}

Sie können Ihre lokale Entwicklungsumgebung so konfigurieren, dass sie den {{site.data.keyword.amashort}}-Service verwendet, der in {{site.data.keyword.Bluemix}} ausgeführt wird. Insbesondere können Sie das {{site.data.keyword.amashort}}-Server-SDK verwenden, wenn Sie serverseitigen Code mit einem lokalen Entwicklungsserver wie Node.js entwickeln.

Das {{site.data.keyword.amashort}}-Server-SDK setzt voraus, dass zwei Umgebungsvariablen festgelegt werden. Wenn Sie serverseitigen Code in {{site.data.keyword.Bluemix_notm}} entwickeln, werden diese Variablen von der {{site.data.keyword.Bluemix_notm}}-Infrastruktur bereitgestellt.

* `VCAP_SERVICES`: Enthält Informationen zu Services, die an die mobile Back-End-Anwendung gebunden sind.
* `VCAP_APPLICATION`: Enthält Informationen zur mobilen Back-End-Anwendung.

Zur Verwenden von {{site.data.keyword.amashort}} mit einem lokalen Entwicklungsserver müssen Sie diese Umgebungsvariablen manuell hinzufügen.

1. Öffnen Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard Ihres mobilen Back-Ends, das mit dem {{site.data.keyword.amashort}}-Service geschützt wird.

1. Klicken Sie auf **Mobile Systemerweiterungen** und kopieren Sie den Wert für **AppGUID**.

1. Legen Sie in Ihrer lokalen Entwicklungsumgebung die Umgebungsvariable *VCAP_APPLICATION* fest. Die Variable muss ein in eine Zeichenfolge konvertiertes JSON-Objekt mit einer einzelnen Eigenschaft enthalten.
```JavaScript
{
    application_id: "appGUID"
}
```
Ersetzen Sie die Variable *appGUID* durch den Wert aus dem entsprechenden Feld unter **Mobile Systemerweiterungen**.

1. Klicken Sie auf **Berechtigungsnachweise anzeigen** auf der Kachel für den {{site.data.keyword.amashort}}-Service in Ihrer mobilen Back-End-Anwendung im {{site.data.keyword.Bluemix_notm}}-Dashboard. Es wird ein JSON-Objekt mit Zugriffsberechtigungsnachweisen angezeigt, die {{site.data.keyword.amashort}} für Ihre mobile Back-End-Anwendung bereitstellt.

1. Legen Sie in Ihrer lokalen Entwicklungsumgebung die Umgebungsvariable `VCAP_SERVICES` fest. Der Wert dieser Variablen muss ein in eine Zeichenfolge konvertiertes JSON-Objekt sein, das die {{site.data.keyword.amashort}}-Berechtigungsnachweise enthält.  Weitere Informationen finden Sie im folgenden Beispiel.

## Beispielcode
{: #local-dev-sample}

Zur Verwendung des {{site.data.keyword.amashort}}-Service in einer lokalen Node.js-Entwicklungsumgebung fügen Sie den folgenden Code hinzu, bevor Sie das Modul `bms-mca-token-validation-strategy` benötigen.

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

// Restlicher Code
```
Ersetzen Sie die Vorkommen des Werts *appGUID* im Code durch den Wert für *appGUID* aus Ihrem mobilen Back-End.


## Mobile Anwendungen zur Arbeit mit einem lokalen Entwicklungsserver konfigurieren
{: #configuring-local}

Initialisieren Sie die {{site.data.keyword.amashort}}-Client-SDKs mit der realen URL Ihrer {{site.data.keyword.Bluemix_notm}}-Anwendung und verwenden Sie den lokalen Host (localhost) oder die IP-Adresse in jeder Ihrer Anforderungen. Weitere Informationen finden Sie in den folgenden Beispielen.

Es ist möglich, dass Sie `localhost` in den folgenden Beispielen in die tatsächliche IP-Adresse Ihres Entwicklungsservers ändern müssen.

### Android

```Java
String baseRequestUrl = "http://localhost:3000";
String bluemixAppRoute = "http://myapp.mybluemix.net";
String bluemixAppGUID = "your-bluemix-app-guid";

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
var bluemixAppGUID = "your-bluemix-app-guid";

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
NSString *bluemixAppGUID = @"your-bluemix-app-guid";

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
let bluemixAppGUID = "your-bluemix-app-guid";

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
