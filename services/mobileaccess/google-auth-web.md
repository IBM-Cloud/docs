---

copyright:
  year: 2016

---

# Enabling Google authentication for web applications
{: #google-auth-web}

*Last updated: 20 July 2016*
{: .last-updated}

Use Google Sign-In to authenticate users on your web application. Add {{site.data.keyword.amashort}} security functionality.


## Before you begin
{: #before-you-begin}

You must have:
* A web app.
* An instance of a  {{site.data.keyword.Bluemix_notm}} application that is protected by {{site.data.keyword.amashort}} service. For more information about how to create a {{site.data.keyword.Bluemix_notm}} back-end application, see [Getting started](index.html).
* The URI for the final redirect (after the authorization process completes).



## Configuring a Google application for your website
To start using Google as an identity provider, create a project in the [Google Developer Console](https://console.developers.google.com). Part of creating a project is to obtain a **Google Client ID** and **Secret**. The Google Client ID and Secret are the unique identifiers for your application used by Google authentication, and are needed for setting up the {{site.data.keyword.amashort}} dashboard.


1. Open your Google application in the Google Developer Console. 
3. Add the Google+ API. 
3. Create credentials using OAuth. Select Web application in application type. Enter the {{site.data.keyword.amashort}} redirect URI in the Authorized redirect URIs
box. The {{site.data.keyword.amashort}} redirect authorization URI can be obtained from the Google configuration screen of the {{site.data.keyword.amashort}} dashboard (see steps below). 
6. Save changes. Take note of the Google Client ID and Application Secret.


## Configuring {{site.data.keyword.amashort}} for Google authentication
After you have a Google Application ID and Secret, you can enable Google authentication in the {{site.data.keyword.amashort}}  dashboard.

1. Open your app in the  {{site.data.keyword.Bluemix_notm}}  dashboard.
1. Click the {{site.data.keyword.amashort}} tile. The {{site.data.keyword.amashort}}  dashboard loads.
1. Click the button on the Google panel.
1. In the **Configure for Web** section:   
    * Note the value in the **Mobile Client Access Redirect URI for Google Developer Console** textbox. This is the value you need to add to the **Authorized redirect URIs**  box under **Restrictions in the Client ID for Web application**  of the **Google Developers Portal** in step 3 above.
    * Enter the **Google Client ID** and **Client Secret**.
    * Enter the redirect URI in the **Your Web Application Redirect URIs**. This value is for the redirect URI to be accessed after the authorization process is completed, and is determined by the developer.
1. Click **Save**.


## Implementing the {{site.data.keyword.amashort}} authorization flow using Google as identity provider

The `VCAP_SERVICES` environment variable is created automatically for each {{site.data.keyword.amashort}} service instance and contains properties necessary for the authorization process. It consists of a JSON object and can be viewed by clicking  **Enviroment Variables**  in the left-side navigator of your application.

To start the process of authorization:

1. Retrieve the authorization endpoint (`authorizationEndpoint`) and clientId (`clientId`) from the service credentials stored in the `VCAP_SERVICES` environment variable. 

    **Note:** In case you created the {{site.data.keyword.amashort}} service before web support was added, you may not have authorization endpoints in the service credentials. In this case use the following authorization endpoints depending on your Bluemix region:


 	US South: 
 	```
 	https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization
 	```
 	London: 
 	```
 	https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization
  	```
  	Sydney: 
  	```
  	https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization
  	```
1. Build the authorization server URI using the `response_type("code")`, `client_id`, and `redirect_uri` as query parameters.
1. Redirect from your web app to the generated URI.
  
The example below retrieves the parameters from the `VCAP_SERVICES` variable, building the URL, and sending the redirect request.
  
```Java
 var cfEnv = require("cfenv"); 
 app.get("/protected", checkAuthentication, function(req, res, next){ 
 	res.send("Hello from protected endpoint"); 
 }); 

 app.get("/protected", checkAuthentication, function(req, res, next){ 
 	res.send("Hello from protected endpoint"); 
 	function checkAuthentication(req, res, next){ 

	// Check if user is authenticated 
 	if (req.session.userIdentity){ 
		next() 
	} else { 
		// If not - redirect to authorization server 
		var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials; 
		var authorizationEndpoint = mcaCredentials.authorizationEndpoint; 
		var clientId = mcaCredentials.clientId; 
		var redirectUri = "http://some-server/oauth/callback"; // Your web application redirect URI 
		var redirectUrl = authorizationEndpoint + "?response_type=code";
		redirectUrl += "&client_id=" + clientId; 
		redirectUrl += "&redirect_uri=" + redirectUri; 
		res.redirect(redirectUrl); 
	} 
} 

  ```

Note that the `redirect_uri` parameter represents your web application redirect URI and must be equal to the one defined in the {{site.data.keyword.amashort}} dashboard.
After redirecting to the authorization end-point the user will get a login form from Google. After user grants permissions to be logged in using his Google identity the {{site.data.keyword.amashort}} service will call your web application redirect URI supplying the grant code as a query parameter.

## Obtaining the tokens
The next step is to obtain access token and identity tokens using the previously received grant code. In order to do so: 

1. Retrieve token `tokenEndpoint`, `clientId`, and `secret` from service credentials stored in `VCAP_SERVICES` environment variable. 
  
    **Note:** In case you created the {{site.data.keyword.amashort}} service before web support was added, you may not have authorization endpoints in the service credentials. In this case use the following authorization endpoints depending on your Bluemix region:
 
 	US South: 
 	```
 	https:// mobileclientaccess.ng.bluemix.net/oauth/v2/token 
  	```
 	London: 
  	```
  	https:// mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token  
   	```
   	Sydney: 
  	```
   	https:// mobileclientaccess.au-syd.bluemix.net/oauth/v2/token 
  	```

2. Send a post request to the token server URI with grant_type ("authorization_code"), client_id, redirect_uri, and code as form parameters. Send the `clientId` and `clientSecret` as Basic HTTP authentication credentials.
 
The following code retrieves the necessary values, and sends them with a post request.
    
   ```Java    
  var cfEnv = require("cfenv");
  var base64url = require("base64url ");
  var request = require('request');

   app.get("/oauth/callback", function(req, res, next){ 
	var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials; 
	var tokenEndpoint = mcaCredentials.tokenEndpoint; 
	var formData = { 
		grant_type: "authorization_code", 
		client_id: mcaCredentials.clientId, 
		redirect_uri: "http://some-server/oauth/callback",// Your web application redirect uri 
		code: req.query.code 
	} 

	request.post({ 
		url: tokenEndpoint, 
		formData: formData 
		}, function (err, response, body){ 
			var parsedBody = JSON.parse(body); 
			req.session.accessToken = parsedBody.access_token; 
			req.session.idToken = parsedBody.id_token; 
			var idTokenComponents = parsedBody.id_token.split("."); // [header, payload, signature] 
			var decodedIdentity= base64url(idTokenComponents[1]);
			req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"]; 
			res.redirect("/"); 
			}
	).auth(mcaCredentials.clientId, mcaCredentials.secret); 
  }
); 
  ```

  The `redirect_uri` parameter is the URI for redirecting, after the successful or failed authentication with Google+, and must match the `redirect_uri` from step 1.  
   
Make sure to send this POST request within 10 min after which the grant code expires. After 10 minutes a new code is required.

The POST response body will contain the `access_token` and the `id_token` encoded in base64.

Once you have received access, and identity the tokens, you can flag web session as authenticated and optionally persist these tokens.  


##Using obtained access and identity token 

The identity token contains information about user identity. In case of Google authentication, the token will contain all the information user agreed to share, such as full name,  url of the profile photo, etc.  

The access token enables communications with resources protected by {{site.data.keyword.amashort}} authorization filters, see see [Protecting Resources](protecting-resources.html).


In order to make requests to protected resources, add an Authorization header to requests with the following structure: 

`Authorization=Bearer <accessToken> <idToken>`

**Note:** 

* The `accessToken` and `idToken` must be separated by a white space.

* The `idToken` is optional. In the case where you do not supply the identity token, the protected resource can be accessed, but will not receive any information about the authorized user. 



