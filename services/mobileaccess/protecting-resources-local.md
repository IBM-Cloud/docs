---

copyright:
  years: 2015, 2016

---

# Using {{site.data.keyword.amashort}} with a local development environment
{: #protecting-local}

You can configure your local development environment to use the {{site.data.keyword.amashort}} service that is running on {{site.data.keyword.Bluemix}}. Specifically, you can use the {{site.data.keyword.amashort}} server SDK when you are developing server side code with a local development server, such as Node.js.

The {{site.data.keyword.amashort}} server SDK requires that two environment variables are set. When you are developing server-side code on {{site.data.keyword.Bluemix_notm}}, these variables are supplied by {{site.data.keyword.Bluemix_notm}} infrastructure.

* `VCAP_SERVICES`: Contains information about services that are bound to the mobile backend application.
* `VCAP_APPLICATION`: Contains information about the mobile backend application.

To use {{site.data.keyword.amashort}} with a local development server, you must manually add these environment variables.

1. Open the {{site.data.keyword.Bluemix_notm}} dashboard of your mobile backend that is protected with the {{site.data.keyword.amashort}} service.

1. Click **Mobile Options** and copy the **AppGUID** value.

1. In your local development environment, set the   *VCAP_APPLICATION* environment variable. The variable must contain a stringified JSON object with a single property.
```JavaScript
{
    application_id: "appGUID"
}
```
Replace the *appGUID* variable with the value from the **Mobile Options** field.

1. Click **Show Credentials** on the {{site.data.keyword.amashort}} service tile in your mobile backend application on the {{site.data.keyword.Bluemix_notm}} dashboard. A JSON object displays with access credentials that {{site.data.keyword.amashort}} provides to your mobile backend application.

1. In your local development environment, set the `VCAP_SERVICES` environment variable. The value of this variable must be stringified JSON object that contains the {{site.data.keyword.amashort}} credentials.  See the following sample for more information.

## Sample code
{: #local-dev-sample}

To use the {{site.data.keyword.amashort}} service in a local Node.js development environment, add the following code before you require `bms-mca-token-validation-strategy` module.

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
Replace the occurrences of the *appGUID* value in the code with your mobile backend *appGUID* value.


## Configuring mobile applications to work with a local development server
{: #configuring-local}

Initialize the {{site.data.keyword.amashort}} client SDKs with the real URL of your {{site.data.keyword.Bluemix_notm}} application and use the localhost (or IP address) in each of your requests. See the following samples.

You might need to change `localhost` to an actual IP address of your development server in the following examples.

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
