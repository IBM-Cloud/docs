---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}



# Utilisation de {{site.data.keyword.appid_short_notm}} avec un environnement de développement local
{: #protecting-local}

Vous pouvez configurer votre environnement local afin d'utiliser le service {{site.data.keyword.appid_short}}. Plus précisément, vous pouvez développer le code en local à l'aide du SDK serveur d'{{site.data.keyword.appid_short_notm}} et envoyer des demandes au serveur de développement.
{:shortdesc}


## Configuration du SDK serveur
{: #serversetup}

Pour utiliser {{site.data.keyword.appid_short_notm}} avec un serveur de développement local, vous devez transmettre le paramètre d'option avec les attributs suivants lorsque vous créez votre stratégie :

* APIStrategy: `oauthServerUrl`
* WebAppStrategy: tenantId, clientId, secret, oauthServerUrl, redirectUri

Pour votre attribut 'redirectUri', spécifiez votre port d'application sur l'hôte local avec le chemin de rappel. Par exemple : `http://localhost:<port>/callback`. Le noeud final de rappel conclut le processus d'authentification.

Pour obtenir vos données d'identification pour le service, procédez comme suit :

1. Ouvrez votre tableau de bord {{site.data.keyword.Bluemix_notm}} et cliquez sur l'onglet **Données d'identification pour le service**.
2. Cliquez sur **Afficher les données d'identification**. Vos identifiants d'accès sont affichées sous forme d'objet JSON.

Pour consulter des exemples et pour plus d'informations, reportez-vous au <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">référentiel GitHub du SDK serveur<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.


## Configuration d'applications {{site.data.keyword.appid_short_notm}} pour leur utilisation avec un serveur de développement local
{: #configuring-local}

Pour configurer vos applications afin d'utiliser un serveur de développement local, utilisez l'hôte local dans chaque demande.

1. Remplacez l'ID du titulaire par votre ID titulaire {{site.data.keyword.appid_short_notm}}. Vous pouvez localiser cet ID dans le tableau de bord de votre service.
2. Remplacez la région par la région appropriée comme indiqué dans le tableau ci-dessous.

<table> <caption> Tableau 1. Régions {{site.data.keyword.Bluemix_notm}} et régions {{site.data.keyword.appid_short_notm}} correspondantes pour Android et iOS </caption>
<tr>
  <th> Région Bluemix </th>
  <th> Android </th>
</tr>
<tr>
  <td> Sud des Etats-Unis </td>
  <td> AppID.REGION_US_SOUTH </td>
</tr>
<tr>
  <td> Sydney </td>
  <td> AppID.REGION_SYDNEY </td>
</tr>
<tr>
  <td> Royaume-Uni </td>
  <td> AppID.REGION_UK </td>
</tr>
</table>



### Android
{: #android}
```java
String baseRequestUrl = "http://localhost:<port>"; //spécifiez ici le port d'exécution de votre serveur
String tenantId = "your-AppID-service-tenantID";
String region = AppID.REGION_UK; //spécifiez ici la région de votre application App ID. Les valeurs possibles actuellement sont : AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, ou AppID.REGION_UK.

BMSClient bmsClient= BMSClient.getInstance();
bmsClient.initialize(getApplicationContext(), region);
AppID appId = AppID.getInstance();
appId.initialize(getApplicationContext(), tenantId, region);

AppIDAuthorizationManager appIDAuthorizationManager = new AppIDAuthorizationManager(appId);
bmsClient.setAuthorizationManager(appIDAuthorizationManager);

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
{:pre}

### iOS - Swift
{: #swift}
```swift

 let baseRequestUrl = "http://localhost:<port>"; //spécifiez ici le port d'exécution de votre serveur
 let tenantId = "your-AppID-service-tenantID"
 let region = AppID.REGION_UK; //spécifiez ici la région de l'application App ID. Les valeurs possibles actuellement sont : AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, ou AppID.REGION_UK.

BMSClient.sharedInstance.initialize(bluemixRegion: region)
BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)

var request:Request =  Request(url: baseRequestUrl + "/resource/path", method: HttpMethod.GET)
request.send(completionHandler: {(response:Response?, error:Error?) in
    if let error = error {
            print("Connection failure")
     		print("Error :: \(error)");
     		print("Status :: \(response?.statusCode)");
    	} else {
            print("Connection success")
            print("Response :: \(response?.responseText)")
        }
});
```
{:pre}
