---

copyright:
  years:  2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}



# Using {{site.data.keyword.appid_short_notm}} with a local development environment
{: #protecting-local}

You can configure your local environment to use the {{site.data.keyword.appid_short}} service. Specifically, you can develop code locally by using the {{site.data.keyword.appid_short_notm}} server SDK and send requests to the development server.
{:shortdesc}


## Setting up the server SDK
{: #serversetup}

To use {{site.data.keyword.appid_short_notm}} with a local development server, you must pass the option parameter when you are creating your strategy, with the following attributes:

* APIStrategy: `oauthServerUrl`
* WebAppStrategy: tenantId, clientId, secret, oauthServerUrl, redirectUri

Set your 'redirectUri' attribute to your localhost app port with the callback path, i.e.: `http://localhost:<port>/callback`. The callback endpoint finishes the authorization process.

To get your service credentials, complete the following steps:

1. Open your {{site.data.keyword.Bluemix_notm}} dashboard and click the **Service Credentials** tab.
2. Click **Show Credentials**. Your access credentials are displayed as a JSON Object.

For samples and more information, see <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">the server SDK GitHub repository <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.


## Configuring {{site.data.keyword.appid_short_notm}} applications to work with a local development server
{: #configuring-local}

To configure your apps to work with a local development server, use the local host in each of your requests.

1. Replace the tenant ID with your {{site.data.keyword.appid_short_notm}} tenant ID. You can find this ID in your service dashboard.
2. Replace the region with the appropriate region as shown in the following table.

<table> <caption> Table 1. {{site.data.keyword.Bluemix_notm}} regions and corresponding Android and iOS SDK regions </caption>
<tr>
  <th> Bluemix Region </th>
  <th> Android </th>
  <th> iOS </th>
</tr>
<tr>
  <td> US South </td>
  <td> AppID.REGION_US_SOUTH </td>
  <td> BMSClient.Region.usSouth </td>
</tr>
<tr>
  <td> Sydney </td>
  <td> AppID.REGION_SYDNEY </td>
  <td> BMSClient.Region.sydney </td>
</tr>
<tr>
  <td> United Kingdom </td>
  <td> AppID.REGION_UK </td>
  <td> BMSClient.Region.unitedKingdom </td>
</tr>
</table>



### Android
{: #android}
```java
String baseRequestUrl = "http://localhost:<port>"; //set to your server running port
String tenantId = "your-AppID-service-tenantID";
String region = AppID.REGION_UK; //set your App ID application region here. Currently possible values are AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, or AppID.REGION_UK.

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

 let baseRequestUrl = "http://localhost:<port>"; //set to your server running port
 let tenantId = "your-AppID-service-tenantID"
 let region = BMSClient.Region.unitedKingdom; //set your App ID application region here. Currently possible values are BMSClient.Region.usSouth, BMSClient.Region.sydney, or BMSClient.Region.unitedKingdom.

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
