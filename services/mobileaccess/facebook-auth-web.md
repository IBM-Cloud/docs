---

copyright:
  year: 2016, 2017
lastupdated: "2017-03-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

The {{site.data.keyword.amafull}} service is replaced with the {{site.data.keyword.appid_full}} service.

# Enabling Facebook authentication for Web applications
{: #facebook-auth-web}

Use Facebook to authenticate users on your {{site.data.keyword.amafull}}  Web application. Add {{site.data.keyword.amashort}} security functionality.

## Before you begin
{: #facebook-auth-android-before}
You must have:

* A Web app.
* An {{site.data.keyword.amashort}} service. For more information, see [Getting started](index.html).
* The URI for the final redirect (after the authorization process completes).


## Configuring an application on the  Facebook for Developers site
{: #facebook-auth-config}

To use Facebook as an identity provider on your website, you must add and configure the website platform on your Facebook application.

1. Log in to your account on the [Facebook for Developers](https://developers.facebook.com) site.
	For information on creating a new app, see [Creating an application on the Facebook for Developers website](facebook-auth-overview.html#facebook-appID).
1. Note the **App ID** and **App Secret**. You need these values when you configure your Web project for Facebook authentication in the Mobile Client Access dashboard.
1. From the **Products List**, choose **Facebook Login**.
4. Add the **Web** platform, if it does not exist.
6. Enter the authorization server callback endpoint URI in the **Valid OAuth redirect URIs** box. You can add this value after you have configured your {{site.data.keyword.amashort}} service in the steps that follow.
7. Save changes.


## Configuring {{site.data.keyword.amashort}} for Facebook authentication
{: #facebook-auth-config-ama}

After you have your Facebook App ID and App Secret, and your Facebook for Developers application has been configured to serve Web clients, you can enable Facebook authentication in the {{site.data.keyword.amashort}}  dashboard.

1. Open the {{site.data.keyword.amashort}} service dashboard.
1. From the **Manage** tab, toggle **Authorization** on.
1. Expand the **Facebook** section.
1. Select **Add Facebook to a Web App**.
5. Note the value in the **Mobile Client Access Redirect URI for Facebook for Developers** text box. You need this value to add to the **Valid OAuth redirect URIs** box in the **Facebook Login** of the Facebook Developers Portal.
6. Enter the Facebook **App ID** and **App Secret** obtained from the Facebook for Developers website.
7. Enter the redirect URI in the **Your Web Application Redirect URIs**. This value is for the redirect URI to be accessed after the authorization process is completed, and is determined by the developer.
8. Click **Save**.


## Implementing the {{site.data.keyword.amashort}} authorization flow using Facebook as identity provider
{: #facebook-auth-flow}

The `VCAP_SERVICES` environment variable is created automatically for each {{site.data.keyword.amashort}} service instance and contains properties necessary for the authorization process. It consists of a JSON object and can be viewed in the  **Service Credentials** tab on the {{site.data.keyword.amashort}} service dashboard.

To start the process of authorization:

1. Retrieve the authorization endpoint (`authorizationEndpoint`) and client id (`clientId`) from the service credentials stored in the `VCAP_SERVICES` environment variable.

	`var cfEnv = require("cfenv");`

	**Note:** If you added the {{site.data.keyword.amashort}} service to your application prior to adding Web support, you might not have token endpoint in the **Service Credentials**. Instead, use the following URLs, depending on your {{site.data.keyword.Bluemix_notm}} region:

	US South:

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization`

	London:

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization`

	Sydney:

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization`

2. Build the authorization server URI using `response_type("code")`, `client_id`, and `redirect_uri` as query parameters.

3. Redirect from your Web app to the generated URI.

	The following example retrieves the parameters from the `VCAP_SERVICES` variable, building the URL, and sending the redirect request.

	```Java
	var cfEnv = require("cfenv");

	app.get("/protected", checkAuthentication, function(req, res, next) {  
		res.send("Hello from protected endpoint");
		}
	);

	function checkAuthentication(req, res, next) {
		// Check if user is authenticated

		if (req.session.userIdentity) {   
			next()  
		} else {   
			// If not - redirect to authorization server   
			var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;   
			var authorizationEndpoint = mcaCredentials.authorizationEndpoint;   
			var clientId = mcaCredentials.clientId;   
			var redirectUri = "http://some-server/oauth/callback";
			// Your Web application redirect URI   

			var redirectUrl = authorizationEndpoint + "?response_type=code";
			redirectUrl += "&client_id=" + clientId;   
			redirectUrl += "&redirect_uri=" + redirectUri;   

			res.redirect(redirectUrl);  

		}
	}
	```
	{: codeblock}

	The `redirect_uri` parameter is the URI for redirecting, after the successful or unsuccessful authentication with Facebook.   

	After redirecting to the authorization endpoint, the user will get a login form from Facebook. After Facebook authorizes the user's identity the {{site.data.keyword.amashort}} service will call your web application redirect URI, supplying the grant code as a query parameter.  


## Obtaining the tokens
{: #facebook-auth-tokens}

The next step is to obtain the access and identity tokens using the previously received grant code:

1.  Retrieve token `tokenEndpoint`, `clientId`, and `secret`  from service credentials stored in `VCAP_SERVICES` environment variable.

	**Note:** If you used {{site.data.keyword.amashort}} before web support was added, you might not have a token endpoint in service credentials. Instead, use the following URLs, depending on your Bluemix region:

	US South:

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/token`

	London:

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token`

	Sydney:

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token`

2. Send a POST request to the token server URI with grant type ("authorization_code"), `clientId`, and your redirect URI  as form parameters. Send the `clientId` and `secret` as basic HTTP authentication credentials.

	The following code retrieves the necessary values, and sends them with a POST request.

	```Java
	var cfEnv = require("cfenv");
	var base64url = require("base64url");
	var request = require('request');

	app.get("/oauth/callback", function(req, res, next) {
		var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
		var tokenEndpoint = mcaCredentials.tokenEndpoint;
		var formData = {
			grant_type: "authorization_code",
			client_id: mcaCredentials.clientId,
			redirect_uri: "http://some-server/oauth/callback",
			// Your web application redirect uri
			code: req.query.code
		}

		request.post( {
			url: tokenEndpoint,
			formData: formData
		}, function (err, response, body) {
			var parsedBody = JSON.parse(body);
			req.session.accessToken = parsedBody.access_token;
			req.session.idToken = parsedBody.id_token;
			var idTokenComponents = parsedBody.id_token.split(".");
			// [header, payload, signature]
			var decodedIdentity= base64url.decode(idTokenComponents[1]);
			req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"];
			res.redirect("/");
		}
		).auth(mcaCredentials.clientId, mcaCredentials.secret);
		}
	);
	```
	{: codeblock}

	Note that the `redirect_uri` parameter must match the `redirect_uri` used for the previous authorization request. The `code` parameter value should be the grant code received in the response from  the authorization request. The grant code is valid for 10 minutes, after which a new code must be be retrieved.

	The response body will contain the access code and token ID in JWT format (see the [JWT website ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://jwt.io/){: new_window}.

	Once you have gained access and received the identity tokens, you can flag web session as authenticated, and optionally persist these tokens.  

##Using obtained access and identity token
{: #facebook-auth-using-token}

The identity token contains information about user identity. In case of Facebook authentication, the token will contain all the information user agreed to share, such as full name, age group, url of the profile photo, etc.  

The access token enables communications with resources protected by {{site.data.keyword.amashort}} authorization filters, see [Protecting Resources](protecting-resources.html).

To make requests to protected resources, add an authorization header to requests with the following structure:

`Authorization=Bearer <accessToken> <idToken>`

#### Tips
{: #tips}

* You must separate the `accessToken` and `idToken` with a white space.

* The `idToken` is optional. If you do not supply the identity token, the protected resource can be accessed, but will not receive any information about the authorized user.
