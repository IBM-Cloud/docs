---

copyright:
  years:  2017
lastupdated: "2017-03-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}



# {{site.data.keyword.appid_short_notm}} mit einer lokalen Entwicklungsumgebung verwenden
{: #protecting-local}

Sie können Ihre lokale Umgebung so konfigurieren, dass sie den {{site.data.keyword.appid_short}}-Service verwendet. Insbesondere können Sie Code mit dem {{site.data.keyword.appid_short_notm}}-Server-SDK lokal entwickeln und Anforderungen an den Entwicklungsserver senden.
{:shortdesc}


## Server-SDK einrichten
{: #serversetup}

Zur Verwendung von {{site.data.keyword.appid_short_notm}} mit einem lokalen Entwicklungsserver müssen Sie den Optionsparameter beim Erstellen Ihre Strategie übergeben. Verwenden Sie dazu folgende Attribute:

* APIStrategy: `oauthServerUrl`
* WebAppStrategy: tenantId, clientId, secret, oauthServerUrl, redirectUri

Legen Sie das Attribut 'redirectUri' auf den App-Port des lokalen Hosts mit dem Callback-Pfad fest, d. h.: `http://localhost:<port>/callback`. Der Callback-Endpunkt beendet den Berechtigungsprozess.

Um Ihre Serviceberechtigungsnachweise abzurufen, führen Sie folgende Schritte aus:

1. Öffnen Sie Ihr {{site.data.keyword.Bluemix_notm}}-Dashboard und klicken Sie auf die Registerkarte **Serviceberechtigungsnachweise**.
2. Klicken Sie auf **Berechtigungsnachweise anzeigen**. Ihre Zugriffsberechtigungsnachweise werden als JSON-Objekt angezeigt.

Beispiele und Informationen finden Sie im <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">GitHub-Repository des Server-SDK <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.


## {{site.data.keyword.appid_short_notm}}-Anwendungen zur Arbeit mit einem lokalen Entwicklungsserver konfigurieren
{: #configuring-local}

Um Ihre Apps so zu konfigurieren, dass sie mit einem lokalen Entwicklungsserver arbeiten, verwenden Sie den lokalen Host in jeder Anforderung.

1. Ersetzen Sie die Tenant-ID durch Ihre {{site.data.keyword.appid_short_notm}}-Tenant-ID. Diese ID befindet sich in Ihrem Service-Dashboard.
2. Ersetzen Sie die Region durch die richtige Region, wie in der folgenden Tabelle dargestellt. 

<table> <caption> Tabelle 1: {{site.data.keyword.Bluemix_notm}}-Regionen und entsprechende Android- und iOS-SDK-Regionen </caption>
<tr>
  <th> Bluemix-Region </th>
  <th> Android </th>
  <th> iOS </th>
</tr>
<tr>
  <td> Vereinigte Staaten (Süden) </td>
  <td> AppID.REGION_US_SOUTH </td>
  <td> BMSClient.Region.usSouth </td>
</tr>
<tr>
  <td> Sydney </td>
  <td> AppID.REGION_SYDNEY </td>
  <td> BMSClient.Region.sydney </td>
</tr>
<tr>
  <td> Vereinigtes Königreich </td>
  <td> AppID.REGION_UK </td>
  <td> BMSClient.Region.unitedKingdom </td>
</tr>
</table>



### Android
{: #android}
```java
String baseRequestUrl = "http://localhost:<port>"; //auf Server festgelegt, der Port ausführt
String tenantId = "your-AppID-service-tenantID";
String region = AppID.REGION_UK; //Region der App-ID-Anwendung hier festlegen. Aktuell mögliche Werte sind AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY oder AppID.REGION_UK.

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

 let baseRequestUrl = "http://localhost:<port>"; //auf Server festgelegt, der Port ausführt
 let tenantId = "your-AppID-service-tenantID"
 let region = AppID.Region.unitedKingdom; //Region der App-ID-Anwendung hier festlegen. Aktuell mögliche Werte sind AppID.Region.usSouth, AppID.Region.sydney oder AppID.Region.unitedKingdom.

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
