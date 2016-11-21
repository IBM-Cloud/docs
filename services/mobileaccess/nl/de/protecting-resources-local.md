---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-10"
---
{:shortdesc: .shortdesc} 

# {{site.data.keyword.amashort}} mit einer lokalen Entwicklungsumgebung verwenden
{: #protecting-local}

Sie können Ihre lokale Entwicklungsumgebung so konfigurieren, dass sie den {{site.data.keyword.amafull}}-Service verwendet, der in {{site.data.keyword.Bluemix}} ausgeführt wird. Insbesondere können Sie Code mit dem {{site.data.keyword.amashort}}-Server-SDK lokal entwickeln und {{site.data.keyword.amashort}}-Anforderungen an den Entwicklungsserver senden. Diese Anforderungen werden vom {{site.data.keyword.amashort}}-Service geschützt, der in {{site.data.keyword.Bluemix}} ausgeführt wird.

## Vorbereitungen
{: #before-you-begin}
Voraussetzungen:

* Instanz einer {{site.data.keyword.Bluemix_notm}}-Anwendung, die durch den {{site.data.keyword.amashort}}-Service geschützt ist. Weitere Informationen zur Erstellung einer {{site.data.keyword.Bluemix_notm}}-Back-End-Anwendung finden Sie in der [Einführung](index.html).
* Die Parameterwerte Ihres Service. Öffnen Sie den Service im {{site.data.keyword.Bluemix_notm}}-Dashboard. Klicken Sie auf **Mobile Systemerweiterungen**. In den Feldern **Route** und **App-GUID/TenantId** werden die Werte `applicationRoute` und `appGUID` (auch als `tenantId` bezeichnet) angezeigt. Diese Werte benötigen Sie für die Initialisierung des SDK und zum Senden von Anforderungen an die Back-End-Anwendung.
*  Suchen Sie die Region, in der Ihre {{site.data.keyword.Bluemix_notm}}-Anwendung gehostet wird. Klicken Sie zur Anzeige der {{site.data.keyword.Bluemix_notm}}-Region auf das Symbol **Avatar** ![Avatarsymbol](images/face.jpg "Avatarsymbol") in der Menüleiste, um das Widget **Konto und Unterstützung** zu öffnen. Der Regionswert muss einer der folgenden sein: **USA (Süden)**, **Sydney** oder **Vereinigtes Königreich**. Die genauen konstanten Werte des SDK, die diesen Namen entsprechen, sind in den Codebeispielen angegeben. 

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

Ersetzen Sie den Wert *appGUID* durch den Wert `appGUID`, den Sie im Schritt [Vorbereitungen](#before-you-begin) abgerufen haben. 

1. Klicken Sie auf **Berechtigungsnachweise anzeigen** auf der Kachel für den {{site.data.keyword.amashort}}-Service in Ihrer mobilen Back-End-Anwendung im {{site.data.keyword.Bluemix_notm}}-Dashboard. Es wird ein JSON-Objekt mit Zugriffsberechtigungsnachweisen angezeigt, die {{site.data.keyword.amashort}} für Ihre mobile Back-End-Anwendung bereitstellt.

1. Legen Sie in Ihrer lokalen Entwicklungsumgebung die Umgebungsvariable `VCAP_SERVICES` fest. Der Wert dieser Variablen muss ein in eine Zeichenfolge konvertiertes JSON-Objekt sein, das die {{site.data.keyword.amashort}}-Berechtigungsnachweise enthält.  Weitere Informationen finden Sie im folgenden Beispiel.

## Beispielservercode
{: #local-dev-sample}

Zur Verwendung des {{site.data.keyword.amashort}}-Service in einer lokalen Node.js-Entwicklungsumgebung fügen Sie den folgenden Code hinzu.  

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

// Nun können Sie das Modul bms-mca-token-validation-strategy anfordern:
var MCABackendStrategy =
	require('bms-mca-token-validation-strategy').MCABackendStrategy;

// Restlicher Code
```

Ersetzen Sie den Wert *appGUID* durch den Wert `appGUID`, den Sie im Schritt [Vorbereitungen](#before-you-begin) abgerufen haben. 


## {{site.data.keyword.amashort}}-Anwendungen zur Arbeit mit einem lokalen Entwicklungsserver konfigurieren
{: #configuring-local}

Initialisieren Sie die {{site.data.keyword.amashort}}-Client-SDKs mit der realen URL Ihrer {{site.data.keyword.Bluemix_notm}}-Anwendung und verwenden Sie den lokalen Host (localhost) oder die IP-Adresse in jeder Ihrer Anforderungen. Weitere Informationen finden Sie in den folgenden Beispielen.

Ersetzen Sie die Region durch die richtige Region.

Ersetzen Sie die Werte *appGUID* und *bluemixAppRoute* durch die Werte, die Sie im Schritt [Vorbereitungen](#before-you-begin) abgerufen haben. 

Es ist möglich, dass Sie `localhost` in den folgenden Beispielen in die tatsächliche IP-Adresse Ihres Entwicklungsservers ändern müssen.

### Android
{: #android}
```Java
String baseRequestUrl = "http://localhost:3000";
String bluemixAppRoute = "http://myapp.mybluemix.net";
String bluemixAppGUID = "your-bluemix-app-guid";
String tenantId = "your-MCA-service-tenantID";

BMSClient.getInstance().initialize(bluemixAppRoute, bluemixAppGUID, BMSClient.REGION_UK);
//  MCA-Anwendungsregion hier festlegen. Aktuell mögliche Werte sind: BMSClient.REGION_US_SOUTH, BMSClient.REGION_SYDNEY oder BMSClient.REGION_UK
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

IMFResourceRequest *request =  [IMFResourceRequest requestWithPath:requestPath
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
// MCA-Anwendungsregion hier festlegen. Aktuell mögliche Werte sind: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, BMSClient.Region.sydney

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

