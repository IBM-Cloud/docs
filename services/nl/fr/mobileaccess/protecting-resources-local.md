---

copyright:
  years: 2015, 2016

---

# Utilisation de {{site.data.keyword.amashort}} avec un environnement de développement local
{: #protecting-local}

*Dernière mise à jour : 17 juillet 2016*
{: .last-updated}

Vous pouvez configurer votre environnement de développement local pour utiliser le service {{site.data.keyword.amashort}} qui s'exécute sur {{site.data.keyword.Bluemix}}. Plus précisément, vous pouvez développer le code localement à l'aide du SDK serveur {{site.data.keyword.amashort}} et envoyer des requêtes {{site.data.keyword.amashort}} au serveur de développement. Ces requêtes seront protégées par le service {{site.data.keyword.amashort}} qui s'exécute sur {{site.data.keyword.Bluemix}}.

## Configuration du SDK serveur
{: #serversetup}

Le SDK serveur {{site.data.keyword.amashort}} requiert que deux variables d'environnement soient définies. Lorsque vous développez du code côté serveur sur {{site.data.keyword.Bluemix_notm}}, ces variables sont fournies par l'infrastructure {{site.data.keyword.Bluemix_notm}}.

* `VCAP_SERVICES` : contient des informations sur les services liés à l'application de back end mobile.
* `VCAP_APPLICATION` : contient des informations sur l'application de back end mobile.

Pour utiliser {{site.data.keyword.amashort}} avec un serveur de développement local, vous devez ajouter manuellement ces variables d'environnement.

1. Ouvrez le tableau de bord {{site.data.keyword.Bluemix_notm}} de votre application back end mobile protégée par le service {{site.data.keyword.amashort}}.

1. Cliquez sur **Mobile Options** et copiez la valeur de **AppGUID**.

1. Dans votre environnement de développement local, définissez la variable d'environnement *VCAP_APPLICATION*. Elle doit contenir une représentation d'objet JSON sous la forme d'une chaîne de caractères (stringified) avec une seule propriété.
```JavaScript
{
    application_id: "appGUID"
}
```
Remplacez la variable *appGUID* par la valeur de la zone **Options pour application mobile** **Identificateur global unique de l'application**.
1. Cliquez sur **Afficher les données d'identification** sur la vignette du service {{site.data.keyword.amashort}} dans votre application back end mobile sur le tableau de bord {{site.data.keyword.Bluemix_notm}}. Un objet JSON s'affiche avec les identifiants d'accès fournis par {{site.data.keyword.amashort}} à votre application de back end mobile.

1. Dans votre environnement de développement local, définissez la variable d'environnement `VCAP_SERVICES`. La valeur de cette variable doit être une représentation d'objet JSON sous la forme d'une chaîne de caractères contenant les données d'identification de {{site.data.keyword.amashort}}.  Voir l'exemple suivant pour plus d'informations.

## Exemple de code serveur
{: #local-dev-sample}

Pour utiliser le service {{site.data.keyword.amashort}} dans un environnement de développement Node.js local, ajoutez le code suivant.  

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

// Vous pouvez à présent réclamer le module bms-mca-token-validation-strategy :
var MCABackendStrategy =
	require('bms-mca-token-validation-strategy').MCABackendStrategy;

// Rest of your code
```
Remplacez les occurrences de la valeur de *Identificateur global unique de l'application* dans le code par celle de votre *Identificateur global unique d'application* de back end mobile.

## Configuration d'applications {{site.data.keyword.amashort}} pour leur utilisation avec un serveur de développement local
{: #configuring-local}

Initialisez les SDK client {{site.data.keyword.amashort}} avec l'URL réelle de votre application {{site.data.keyword.Bluemix_notm}} en spécifiant l'hôte local (ou l'adresse IP) dans chacune de vos requêtes. Voir l'exemple suivant.

Remplacez `BMSClient.REGION_UK` par la région appropriée.


Dans les exemples suivants, il peut être nécessaire de remplacer `localhost` par l'adresse IP réelle de votre serveur de développement.

### Android
{: #android}
```Java
String baseRequestUrl = "http://localhost:3000";
String bluemixAppRoute = "http://myapp.mybluemix.net";
String bluemixAppGUID = "your-bluemix-app-guid";

BMSClient.getInstance().initialize(bluemixAppRoute, bluemixAppGUID, BMSClient.REGION_UK);

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

[[IMFClient sharedInstance]
			initializeWithBackendRoute:bluemixAppRoute
			backendGUID:bluemixAppGUID];

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

### Cordova
{: #cordova}

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
