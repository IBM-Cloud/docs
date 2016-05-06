---

Copyright : 2015, 2016

---

# Utilisation de {{site.data.keyword.amashort}} avec un environnement de développement local
{: #protecting-local}

Vous pouvez configurer votre environnement de développement local pour qu'il utilise le service {{site.data.keyword.amashort}} qui s'exécute sur {{site.data.keyword.Bluemix}}. En particulier, vous pouvez utiliser le SDK serveur de {{site.data.keyword.amashort}} lorsque vous développez du code côté serveur avec un serveur de développement local, comme Node.js.

Le SDK serveur de {{site.data.keyword.amashort}} requiert la définition de deux variables. Lorsque vous développez du code côté serveur sur {{site.data.keyword.Bluemix_notm}}, ces variables sont fournies par l'infrastructure {{site.data.keyword.Bluemix_notm}}.

* `VCAP_SERVICES` : Contient des informations sur les services liés à l'application de back end mobile.
* `VCAP_APPLICATION` : Contient des informations sur l'application de back end mobile.

Pour utiliser {{site.data.keyword.amashort}} avec un serveur de développement local, vous devez ajouter manuellement ces variables d'environnement.

1. Ouvrez le tableau de bord {{site.data.keyword.Bluemix_notm}} de votre système de back end mobile qui est protégé avec le service {{site.data.keyword.amashort}}.

1. Cliquez sur **Options pour application mobile** et copiez la valeur de **AppGUID**.

1. Dans votre environnement de développement local, définissez la variable d'environnement *VCAP_APPLICATION*. Elle doit contenir une représentation d'objet JSON sous la forme d'une chaîne de caractères (stringified) avec une seule propriété.
```JavaScript
{
    application_id: "appGUID"
}
```
Remplacez la variable *appGUID* par la valeur trouvée dans **Options pour application mobile**.

1. Cliquez sur **Afficher les données d'identification** sur la vignette {{site.data.keyword.amashort}} de votre application de back end mobile dans le tableau de bords {{site.data.keyword.Bluemix_notm}}. Un objet JSON s'affiche avec les identifiants d'accès fournis par {{site.data.keyword.amashort}} à votre application de back end mobile.

1. Dans votre environnement de développement local, définissez la variable d'environnement `VCAP_SERVICES`. La valeur de cette variable doit être une représentation d'objet JSON sous la forme d'une chaîne de caractères contenant les données d'identification de {{site.data.keyword.amashort}}.  Voir l'exemple suivant pour plus d'informations.

## Exemple de code
{: #local-dev-sample}

Pour utiliser le service {{site.data.keyword.amashort}} dans un environnement de développement Node.js, ajoutez le code suivant avant d'avoir besoin du module
`bms-mca-token-validation-strategy`.

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

// Rest of your code
```
Remplacez les occurrences de la valeur *appGUID* dans le code par celle de la valeur *appGUID* de votre application de back end mobile.


## Configuration des applications mobiles en vue de leur fonctionnement avec un serveur de développement local
{: #configuring-local}

Initialisez les SDK client de {{site.data.keyword.amashort}} avec l'URL réelle de votre application {{site.data.keyword.Bluemix_notm}} et utilisez localhost (ou l'adresse IP) dans vos demandes. Voir l'exemple suivant.

Dans les exemples suivants, il peut être nécessaire de replacer `localhost` par l'adresse IP réelle de votre serveur de développement.

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

IMFResourceRequest* request = [IMFResourceRequest
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
