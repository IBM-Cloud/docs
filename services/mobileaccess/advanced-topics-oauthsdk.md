---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---

{:codeblock:.codeblock}

The {{site.data.keyword.amafull}} service is replaced with the {{site.data.keyword.appid_full}} service.

# Communicating between back-end applications and services
{: #backend-comm}

In some scenarios, you might need to send requests from your back-end application that is running on {{site.data.keyword.Bluemix}} to another back-end service that is protected by the {{site.data.keyword.amafull}} service (for example the {{site.data.keyword.cloudant}} service). In these cases, you must add an OAuth token to the request.

Use the `bms-mca-oauth-sdk npmjs` module to obtain and inject OAuth tokens into requests.

## Installing the bms-mca-oauth-sdk module
{: #sdk}

On a command line, open the Node.js application directory and run the following command:

```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## Using the bms-mca-oauth-sdk module
{: #using-sdk}

The following code demonstrates how to use the `bms-mca-oauth-sdk` module.


``` JavaScript
var oauthSDK = require('bms-mca-oauth-sdk');

var options = {

	// You can cache tokens to avoid extra roundtrips on every request
	// This property defines the number of tokens to be cached

	cacheSize: 100,

	// The following properties are retrieved automatically when your Node.js
	// runs on {{site.data.keyword.Bluemix_notm}} and bound to an instance of {{site.data.keyword.amashort}} Service.
	// Alternatively, you can get these property values by clicking Show Credentials
	// on the {{site.data.keyword.amashort}} Service tile in your {{site.data.keyword.Bluemix_notm}} application dashboard

	appId: "tenantID",				// a.k.a. Bluemix applicationGUID
	clientId: "clientId",			
	secret: "secret",
	serverUrl: "serverUrl"
};

oauthSDK.getAuthorizationHeader(options).then(function(authHeader){

	// In the request that you want to send to the protected resource,
	// add the authHeader value.

	request.headers.Authorization = authHeader;

	// Send request

});

```
{: codeblock}
