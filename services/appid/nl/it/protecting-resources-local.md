---

copyright:
  years:  2017
lastupdated: "2017-03-30"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}



# Utilizzo {{site.data.keyword.appid_short_notm}} con un ambiente di sviluppo locale
{: #protecting-local}

Puoi configurare il tuo ambiente locale per utilizzare il servizio {{site.data.keyword.appid_short}}. Nello specifico, puoi sviluppare il codice localmente utilizzando l'SDK server {{site.data.keyword.appid_short_notm}} e inviare le richieste al server di sviluppo.
{:shortdesc}


## Configurazione dell'SDK server
{: #serversetup}

Per utilizzare {{site.data.keyword.appid_short_notm}} con un ambiente di sviluppo locale, devi passare il parametro dell'opzione quando crei la tua strategia, con i seguenti attributi:

* APIStrategy: `oauthServerUrl`
* WebAppStrategy: tenantId, clientId, secret, oauthServerUrl, redirectUri

Imposta il tuo attributo 'redirectUri' nella tua porta dell'applicazione localhost con il percorso di callback, ad es.: `http://localhost:<port>/callback`. L'endpoint di callback termina con il processo di autorizzazione.

Per ottenere le tue credenziali del servizio, completa la seguente procedura:

1. Apri il tuo dashboard {{site.data.keyword.Bluemix_notm}} e fai clic sulla scheda **Service Credentials**.
2. Fai clic su **Show Credentials**. Le tue credenziali di accesso vengono visualizzate come un oggetto JSON.

Per gli esempi e ulteriori informazioni, consulta <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">the server SDK GitHub repository <img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a>.


## Configurazione delle applicazioni {{site.data.keyword.appid_short_notm}} per lavorare con un server di sviluppo locale
{: #configuring-local}

Per configurare le tue applicazioni in modo che utilizzino un server di sviluppo locale, utilizza l'host locale in ognuna delle tue risposte.

1. Sostituisci l'ID tenant con il tuo ID tenant {{site.data.keyword.appid_short_notm}}. Puoi trovare questo ID nel tuo dashboard del servizio
2. Sostituisci la regione con la regione appropriata come descritto nella seguente tabella.

<table> <caption> Tabella 1. Regioni {{site.data.keyword.Bluemix_notm}} e regioni SDK Android e iOS {{site.data.keyword.appid_short_notm}} corrispondenti </caption>
<tr>
  <th> Regione Bluemix </th>
  <th> Android </th>
</tr>
<tr>
  <td> Stati Uniti Sud </td>
  <td> AppID.REGION_US_SOUTH </td>
</tr>
<tr>
  <td> Sydney </td>
  <td> AppID.REGION_SYDNEY </td>
</tr>
<tr>
  <td> Regno Unito </td>
  <td> AppID.REGION_UK </td>
</tr>
</table>



### Android
{: #android}
```java
String baseRequestUrl = "http://localhost:<port>"; //imposta la tua porta di esecuzione del server
String tenantId = "your-AppID-service-tenantID";
String region = AppID.REGION_UK; //imposta la tua regione dell'applicazione ID Applicazione qui. I valori al momento possibili sono AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY o AppID.REGION_UK.

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

 let baseRequestUrl = "http://localhost:<port>"; //imposta la tua porta di esecuzione del server
 let tenantId = "your-AppID-service-tenantID"
 let region = AppID.REGION_UK; //imposta la tua regione dell'applicazione ID Applicazione qui. I valori al momento possibili sono AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY o AppID.REGION_UK.

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
