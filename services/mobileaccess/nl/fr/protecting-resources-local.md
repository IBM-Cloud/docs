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


# Utilisation de {{site.data.keyword.amashort}} avec un environnement de développement local
{: #protecting-local}

Vous pouvez configurer votre environnement de développement local pour utiliser le service {{site.data.keyword.amafull}} qui s'exécute sur {{site.data.keyword.Bluemix}}. Plus précisément, vous pouvez développer le code localement à l'aide du SDK serveur {{site.data.keyword.amashort}} et envoyer des requêtes {{site.data.keyword.amashort}} au serveur de développement. Ces requêtes seront protégées par le service {{site.data.keyword.amashort}} qui s'exécute sur {{site.data.keyword.Bluemix}}.

## Avant de commencer
{: #before-you-begin}

Vous devez disposer des éléments suivants :

* Une instance d'une application {{site.data.keyword.Bluemix_notm}} qui est protégée par le service {{site.data.keyword.amashort}}. Pour plus d'informations sur la création d'un système de back end {{site.data.keyword.Bluemix_notm}}, voir [Initiation](index.html).
* Valeur de votre **TenantID**. Ouvrez votre service dans le tableau de bord de {{site.data.keyword.amafull}}. Cliquez sur le bouton **Options pour application mobile**. Les valeurs `tenantId` (qui portent également le nom d'`appGUID`) sont affichées dans la zone **App GUID / TenantId**. Vous aurez besoin de cette valeur pour initialiser le Gestionnaire des autorisations.
* Votre **Application Route**. Il s'agit de l'URL de votre application back end. Vous avez besoin de cette valeur pour envoyer des demandes à ses noeuds finaux protégés.
* Votre **région** {{site.data.keyword.Bluemix_notm}}.  Vous pouvez trouver votre région {{site.data.keyword.Bluemix_notm}} actuelle dans l'en-tête, en regard de l'icône **Avatar**![icône Avatar](images/face.jpg "icône Avatar"). La valeur de la région qui apparaît doit être l'une des suivantes : `US South`,  `Sydney` ou `United Kingdom`. Pour la syntaxe exacte requise par le SDK, voir les commentaires dans les exemples de code. Vous aurez besoin de cette valeur pour initialiser le client {{site.data.keyword.amashort}}.
* Un projet Android Studio, configuré pour fonctionner avec Gradle. Pour plus d'informations sur la configuration de votre environnement de développement Android, accédez au site [Google Developer Tools ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://developer.android.com/sdk/index.html "Icône de lien externe"){: new_window}.

## Configuration du SDK serveur
{: #serversetup}

Le SDK serveur {{site.data.keyword.amashort}} requiert que deux variables d'environnement soient définies. Lorsque vous développez du code côté serveur sur {{site.data.keyword.Bluemix_notm}}, ces variables sont fournies par l'infrastructure {{site.data.keyword.Bluemix_notm}}.

* `VCAP_SERVICES` : contient des informations sur les services liés à l'application de back end mobile.
* `VCAP_APPLICATION` : contient des informations sur l'application de back end mobile.

Pour utiliser {{site.data.keyword.amashort}} avec un serveur de développement local, vous devez ajouter manuellement ces variables d'environnement.

1. Ouvrez le tableau de bord {{site.data.keyword.Bluemix_notm}} de votre application back end mobile protégée par le service {{site.data.keyword.amashort}}.

1. Dans votre environnement de développement local, définissez la variable d'environnement *VCAP_APPLICATION*. Elle doit contenir une représentation d'objet JSON sous la forme d'une chaîne de caractères (stringified) avec une seule propriété.
	```JavaScript
	{
	    application_id: "appGUID"
	}
	```
	{: codeblock}

1. Cliquez sur l'onglet **Afficher les données d'identification** dans le tableau de bord {{site.data.keyword.amashort}}. Un objet JSON s'affiche avec les identifiants d'accès fournis par {{site.data.keyword.amashort}} à votre application de back end mobile.

1. Dans votre environnement de développement local, définissez la variable d'environnement `VCAP_SERVICES`. La valeur de cette variable doit être une représentation d'objet JSON sous la forme d'une chaîne de caractères contenant les données d'identification de {{site.data.keyword.amashort}}.  Voir l'exemple suivant pour plus d'informations.

## Exemple de code serveur
{: #local-dev-sample}

Pour utiliser le service {{site.data.keyword.amashort}} dans un environnement de développement Node.js local, ajoutez le code suivant.  

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

// Now you can require the bms-mca-token-validation-strategy module:
var MCABackendStrategy =
	require('bms-mca-token-validation-strategy').MCABackendStrategy;

// Rest of your code
```
{: codeblock}

Pour plus d'informations sur l'obtention de la valeur *tenantID*, voir [Avant de commencer](#before-you-begin).


## Configuration d'applications {{site.data.keyword.amashort}} pour leur utilisation avec un serveur de développement local
{: #configuring-local}

Initialisez les SDK client {{site.data.keyword.amashort}} avec l'URL réelle de votre application {{site.data.keyword.Bluemix_notm}} en spécifiant l'hôte local (ou l'adresse IP) dans chacune de vos requêtes. Voir l'exemple suivant.

Remplacez la région par la région appropriée. Reportez-vous aux exemples de code pour connaître la syntaxe correcte.

Remplacez les valeurs de *appGUID* et de *bluemixAppRoute*. Pour des informations sur l'obtention de ces valeurs, voir [Avant de commencer](#before-you-begin).

Dans les exemples suivants, il peut être nécessaire de remplacer `localhost` par l'adresse IP réelle de votre serveur de développement.

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
