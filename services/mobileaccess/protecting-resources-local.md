---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**Important: The {{site.data.keyword.amafull}} service is replaced with the {{site.data.keyword.appid_full}} service.**

# Using {{site.data.keyword.amashort}} with a local development environment
{: #protecting-local}

You can configure your local development  to use the {{site.data.keyword.amafull}} service that is running on {{site.data.keyword.Bluemix}}. Specifically, you can develop code locally using the {{site.data.keyword.amashort}} server SDK and send {{site.data.keyword.amashort}} requests to the development server. These requests will be protected by the {{site.data.keyword.amashort}} service that is running on {{site.data.keyword.Bluemix}}.

## Before you begin
{: #before-you-begin}

You must have:

* An instance of a  {{site.data.keyword.Bluemix_notm}} application that is protected by {{site.data.keyword.amashort}} service. For more information about how to create a {{site.data.keyword.Bluemix_notm}} back-end application, see [Getting started](index.html).
* Your **TenantID**. Open your service in the  {{site.data.keyword.amafull}} dashboard. Click the **Mobile Options** button. The `tenantId` (also known as `appGUID`)  values are displayed in the  **App GUID / TenantId** field. You will need this value for intializing the Authorization Manager.
* Your **Application Route**. This is the URL of your back-end application. You need this value for for sending requests to its protected endpoints.
* Your {{site.data.keyword.Bluemix_notm}} **Region**.  You can find your current {{site.data.keyword.Bluemix_notm}} region in the header, next to the **Avatar** icon ![Avatar icon](images/face.jpg "Avatar icon"). The region value that appears should be one of the following: `US South`,  `Sydney`, or  `United Kingdom`. For the exact syntax required by the SDK, see the comments in the code samples. You will need this value for initializing the {{site.data.keyword.amashort}} client.
* An Android Studio project, set up to work with Gradle. For more information about how to set up your Android development environment, see [Google Developer Tools ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://developer.android.com/sdk/index.html){: new_window}.

## Setting up the server SDK
{: #serversetup}

The {{site.data.keyword.amashort}} server SDK requires that two environment variables be set. When you are developing server-side code on {{site.data.keyword.Bluemix_notm}}, these variables are supplied by {{site.data.keyword.Bluemix_notm}} infrastructure.

* `VCAP_SERVICES`: Contains information about services that are bound to the mobile back-end application.
* `VCAP_APPLICATION`: Contains information about the mobile back-end application.

To use {{site.data.keyword.amashort}} with a local development server, you must manually add these environment variables.

1. Open the {{site.data.keyword.Bluemix_notm}} dashboard of your mobile back-end application that is protected with the {{site.data.keyword.amashort}} service.

1. In your local development environment, set the *VCAP_APPLICATION* environment variable. The variable must contain a stringified JSON object with a single property.
	```JavaScript
	{
	    application_id: "appGUID"
	}
	```
	{: codeblock}

1. Click **Show Credentials** tab in the {{site.data.keyword.amashort}} dashboard. A JSON object displays with access credentials that {{site.data.keyword.amashort}} provides to your mobile back-end application.

1. In your local development environment, set the `VCAP_SERVICES` environment variable. The value of this variable must be stringified JSON object that contains the {{site.data.keyword.amashort}} credentials.  See the following sample for more information.

## Sample server code
{: #local-dev-sample}

To use the {{site.data.keyword.amashort}} service in a local Node.js development environment, add the following code.  

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

For information on finding the *tenantID* value see [Before you begin](#before-you-begin).


## Configuring {{site.data.keyword.amashort}} applications to work with a local development server
{: #configuring-local}

Initialize the {{site.data.keyword.amashort}} client SDKs with the real URL of your {{site.data.keyword.Bluemix_notm}} application, and use the localhost (or IP address) in each of your requests. See the following samples.

Replace the region with the appropriate region. See the code examples for the correct syntax.

Replace the *appGUID* and *bluemixAppRoute* values. For information on obtaining these values, see [Before you begin](#before-you-begin).

You might need to change `localhost` to an actual IP address of your development server in the following examples.

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

var request = new MFPRequest(baseRequestUrl + "/resource/path", MFPRequest.GET);

request.send(success, failure);
```
{: codeblock}
