---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---

{:codeblock:.codeblock}


The {{site.data.keyword.amafull}} service is replaced with the {{site.data.keyword.appid_full}} service.


# Creating a custom identity provider
{: #custom-create}


To create a custom identity provider, develop a web application that exposes a RESTful API:

`POST <base_url>/apps/<tenant_id>/<realm_name>/<request_type>`

* `base_url`: Specifies the base URL of the custom identity provider web application. The base URL is the URL to be registered in the {{site.data.keyword.amashort}} dashboard.
* `tenant_id` : Specifies the unique identifier of the tenant. When the {{site.data.keyword.amashort}} invokes this API, it always supplies the {{site.data.keyword.Bluemix}} app GUID (`applicationGUID`).
* `realm_name` : Specifies the custom realm name that is defined in the {{site.data.keyword.amashort}} dashboard.
* `request_type` : Specifies one of these:
	* `startAuthorization`: Specifies a first step of authentication process. The custom identity provider must respond with either "challenge", "success", or "failure" status.
	* `handleChallengeAnswer`: Handles an authentication challenge response from the mobile client.

## `startAuthorization` API
{: #custom-startauthorization}

`POST <base_url>/apps/<tenant_id>/<realm_name>/startAuthorization`
{: codeblock}

The `startAuthorization` API is used as a first step of authentication process. A custom identity provider must respond with either "challenge", "success", or "failure" status.

To allow for a maximum flexibility of the authentication process, a custom identity provider has access to all HTTP headers that are sent by a mobile client in the request body. The headers are provided in following format:

```JavaScript
{
    "headers" : {
    	"header1": "value1",  
    	"header2" : "value2"
    }
}
```
{: codeblock}

A custom identity provider might respond with an authentication challenge, or immediate success or failure. The response HTTP status must be `HTTP 200`, and the response JSON must contain following properties:

* `status` : Specifies `success`, `challenge`, or `failure` of the request.
* `stateId` (optional): Specifies a randomly generated string identifier to identify the authentication session with the mobile client. This attribute can be omitted if the custom identity provider does not store any state.
* `challenge` : Specifies a JSON object that represents an authentication challenge to be sent back to the mobile client. This attribute is only sent to client if status is set to `challenge`.
* `userIdentity` : Specifies a JSON object that represents a user identity.  The user identity consists of properties such as `userName`, `displayName`, and attributes.  For more information, see [User Identity Object](#custom-user-identity). This property is only sent to the mobile client if the status is set to `success`.

For example:

```
{
	"status":"challenge",
	"stateId":"some-random-guid"
	"challenge":{
		message:"Enter username and password",
		attemptsLeft: 3
	}
}
```
{: codeblock}

## `handleChallengeAnswer` API
{: #custom-handleChallengeAnswer}

`POST <base_url>/apps/<tenant_id>/<realm_name>/handleChallengeAnswer`
{: codeblock}

The `handleChallengeAnswer` API handles an authentication challenge response from the mobile client. Like the `startAuthorization` API, the `handleChallengeAnswer` API respond with either `challenge`, `success`, or `failure` status.

Similarly to `startAuthorization` request, the custom identity provider has access to all HTTP headers that are sent by the mobile client in the request body. In addition to the mobile client request headers, the body of `handleChallengeAnswer` request also includes the `stateId` and `challengeAnswer` properties.

### Example of `handleChallengeAnswer` request body
{: #custom-handleChallengeAnswer-example}

```JavaScript
{
    "headers" : {
    	"header1": "value1",  
    	"header2" : "value2"
	},
    "stateId" : "123123123",
    "challengeAnswer" : {
    	"pinCode":12345
 	}
}
```
{: codeblock}

The response from a `handleChallengeAnswer` API must have the same structure as the response of the `startAuthorization` API.

## User identity object
{: #custom-user-identity}

A response to a successful authentication request must include a user identity object, with the following attributes:
* `userName` : Specifies a unique user name.
* `displayName` : Specifies the display name of the user.
* `attributes` (optional) : Specifies a JSON object that contains custom user attributes.

### User identity object example
{: #custom-user-identity-example}
```JavaScript
{
    "userName" : "janesmith",
    "displayName" : "Jane Smith",
    "attributes" : {
        "Language" : "French",
        "Country" : "Canada"
    }
}
```
{: codeblock}

The user identity object is used by the {{site.data.keyword.amashort}} service to generate an ID token that is sent to the mobile client as a part of authorization header. After successful authentication, the mobile client has full access to the user identity object.

## Security considerations
{: #custom-security}

Each request from the {{site.data.keyword.amashort}} service to a custom identity provider contains an authorization header so that the custom identity provider can verify that the request is coming from an authorized source. While not strictly mandatory, consider validating the authorization header by instrumenting your custom identity provider with a {{site.data.keyword.amashort}} server SDK. To use this SDK, your custom identity provider application must implemented with Node.js or Liberty for Java&trade; and run on {{site.data.keyword.Bluemix_notm}}.

The authorization header contains information about the mobile client and mobile app that triggered the authentication process. You can use the security context to retrieve this data. For more information, see [Protecting resources](protecting-resources.html).

## Sample implementation of custom identity provider
{: #custom-sample}
You can use any of the following Node.js sample implementations of a custom identity provider as a reference when you develop your custom identity provider. Download the full application code from the GitHub repositories.

* [Simple sample](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
* [Advanced sample](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

<!---
 ### JSON structure (simple sample)
{: #custom-sample-json}
This implementation assumes that the supplied authentication challenge answer is a JSON object with the following structure:

```
{
 	username: "my.username",
 	password: "my.password"
 }
 ```

### Custom identity provider sample code (simple sample)
{: #custom-sample-code}
```JavaScript
var express = require('express');
var cfenv = require('cfenv');
var log4js = require('log4js');
var jsonParser = require('body-parser').json();

// Using hardcoded user repository
var userRepository = {
	"john.lennon":      { password: "12345", displayName:"John Lennon", dob:"October 9, 1940"},
	"paul.mccartney":   { password: "67890", displayName:"Paul McCartney", dob:"June 18, 1942"},
	"ringo.starr":      { password: "abcde", displayName:"Ringo Starr", dob: "July 7, 1940"},
	"george.harrison":  { password: "fghij", displayName: "George Harrison", dob:"Feburary 25, 1943"}
}

var app = express();
var logger = log4js.getLogger("CustomIdentityProviderApp");
logger.info("Starting up");

app.post('/apps/:tenantId/:realmName/startAuthorization', jsonParser, function(req, res){
	var tenantId = req.params.tenantId;
	var realmName = req.params.realmName;
	var headers = req.body.headers;

	logger.debug("startAuthorization", tenantId, realmName, headers);

	var responseJson = {
		status: "challenge",
		challenge: {
			text: "Enter username and password"
		}
	};

	res.status(200).json(responseJson);
});

app.post('/apps/:tenantId/:realmName/handleChallengeAnswer', jsonParser, function(req, res){
	var tenantId = req.params.tenantId;
	var realmName = req.params.realmName;
	var challengeAnswer = req.body.challengeAnswer;


	logger.debug("handleChallengeAnswer", tenantId, realmName, challengeAnswer);

	var username = req.body.challengeAnswer["username"];
	var password = req.body.challengeAnswer["password"];

	var userObject = userRepository[username];

	var responseJson = { status: "failure" };

	if (userObject && userObject.password == password ){
		logger.debug("Login success for userId ::", username);
		responseJson.status = "success";
		responseJson.userIdentity = {
			userName: username,
			displayName: userObject.displayName,
			attributes: {
				dob: userObject.dob
			}
		}
	} else {
		logger.debug("Login failure for userId ::", username);
	}

	res.status(200).json(responseJson);
});

app.use(function(req, res, next){
	res.status(404).send("This is not the URL you're looking for");
});

var server = app.listen(cfenv.getAppEnv().port, function () {
	var host = server.address().address;
	var port = server.address().port;
	logger.info('Server listening at %s:%s', host, port);
});
```
--->

## Next steps
{: #next-steps}
* [Configuring {{site.data.keyword.amashort}} for custom authentication](custom-auth-config-mca.html)
* [Configuring custom authentication for Android](custom-auth-android.html)
* [Configuring custom authentication for iOS](custom-auth-ios.html)
* [Configuring custom authentication for Cordova](custom-auth-cordova.html)
