---

copyright:
  year: 2016

---

# Enabling Facebook authentication for web applications

Last updated: 28 July 2016
{: .last-updated}

Use Facebook to authenticate users on your web app. Add {{site.data.keyword.amashort}} security functionality. 

## Before you begin
{: #facebook-auth-android-before}
You must have:

* A web app. 
* An instance of a  {{site.data.keyword.Bluemix_notm}} application that is protected by the {{site.data.keyword.amashort}} service. For more information about how to create a {{site.data.keyword.Bluemix_notm}} back-end application, see [Getting started](index.html).
* The URI for the final redirect (after the authorization process completes).


## Configuring a Facebook application for your website
To use Facebook as an identity provider on your website, you must add and configure the website platform on your Facebook application.

1. Log in to the [Facebook Developers Portal](https://developers.facebook.com).
2. Open or create your app.
3. Note the **Application ID**  and **App Secret**. You need these values when you configure your web project for Facebook authentication in the {{site.data.keyword.amashort}} dashboard.
4. Add the **Website** platform, if it does not exist.
5. Add or open the **Facebook Login** from the Products list.
6. Enter the authorization server callback endpoint URI in the **Valid OAuth redirect URIs** box. Find this authorization redirect URI in the {{site.data.keyword.amashort}} dashboard configuration steps that follow.
7. Save changes.




## Configuring {{site.data.keyword.amashort}} for Facebook authentication
After you have your Facebook Application ID and App Secret, and your Facebook Application has been configured to serve web clients, you can enable Facebook authentication in the {{site.data.keyword.Bluemix_notm}}  dashboard.

1. Open the {{site.data.keyword.Bluemix_notm}} dashboard.
2. Click the relevant app tile to load the app.
3. Click the tile for the  {{site.data.keyword.amashort}} service.
4. Click the **Configure** button in the **Facebook** panel.
5. Note the value in the **Mobile Client Access Redirect URI for Facebook Developer Console** text box. You need this value to add to the **Valid OAuth redirect URIs** box in the **Facebook Login** of the Facebook Developers Portal in step six of Configuring a Facebook application for your website.
6. Enter the Facebook **Application ID** and **App Secret**.
7. Enter the redirect URI in the **Your Web Application Redirect URIs**. This value is for the redirect URI to be accessed after the authorization process is completed, and is determined by the developer.
8. Click **Save**.




## Implementing the {{site.data.keyword.amashort}} authorization flow using Facebook as identity provider

The `VCAP_SERVICES` environment variable is created automatically for each {{site.data.keyword.amashort}} service instance and contains properties necessary for the authorization process. It consists of a JSON object and can be viewed by clicking  **Environment Variables**  in <!--the left-side navigator of--> your application.

To start the process of authorization:

1. Retrieve the authorization endpoint (`authorizationEndpoint`) and client id (`clientId`) from the service credentials stored in the `VCAP_SERVICES` environment variable. 

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
2. Build the authorization server URI using `response_type("code")`, `client_id`, and `redirect_uri` as query parameters. 
3. Redirect from your web app to the generated URI.



The following example retrieves the parameters from the `VCAP_SERVICES` variable, building the URL, and sending the redirect request.

  ```Java
  var cfEnv = require("cfenv"); 

  app.get("/protected", checkAuthentication, function(req, res, next){  
      res.send("Hello from protected endpoint"); 
    }
  ); 
  
  function checkAuthentication(req, res, next){
  // Check if user is authenticated 
  
    if (req.session.userIdentity){   
       next()  
     } else {   
  // If not - redirect to authorization server   
        var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;   
        var authorizationEndpoint = mcaCredentials.authorizationEndpoint;   
        var clientId = mcaCredentials.clientId;   
        var redirectUri = "http://some-server/oauth/callback"; 
         // Your web application redirect URI   

        var redirectUrl = authorizationEndpoint + "?response_type=code";
        redirectUrl += "&client_id=" + clientId;   
        redirectUrl += "&redirect_uri=" + redirectUri;   
  
        res.redirect(redirectUrl);  
  
      } 
  }
  
 ```

   The `redirect_uri` parameter is the URI for redirecting, after the successful or unsuccessful authentication with Facebook.
   

 After redirecting to the authorization endpoint, the user will get a login form from 
Facebook. After Facebook authorizes the user's identity the {{site.data.keyword.amashort}} service will call your web application redirect URI, supplying the grant code as a query parameter.  

## Obtaining the tokens

The next step is to obtain the access and identity tokens using the previously received grant code:

 1.  Retrieve token `tokenEndpoint`, `clientId`, and `secret`  from service credentials stored in `VCAP_SERVICES` environment variable. 
 
    **Note:** If you used {{site.data.keyword.amashort}} before web support was added, you might not have a token endpoint in service credentials. Instead, use the following URLs, depending on your Bluemix region: 

    US South: 
    ```
    https://mobileclientaccess.ng.bluemix.net/oauth/v2/token 
     ```
    London: 
      ```
    https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token  
     ```
    Sydney: 
      ```
    https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token 
    ```

 1. Send a post request to the token server URI with grant type ("authorization_code"), `clientId`, and your redirect URI  as form parameters. Send the `clientId` and `secret` as basic HTTP authentication credentials.
 
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
      redirect_uri: "http://some-server/oauth/callback",
     // Your web application redirect uri 
      code: req.query.code 
   } 

 
    request.post({ 
        url: tokenEndpoint, 
        formData: formData 
      }, function (err, response, body){ 
        var parsedBody = JSON.parse(body); 
        req.session.accessToken = parsedBody.access_token; 
        req.session.idToken = parsedBody.id_token; 
        var idTokenComponents = parsedBody.id_token.split("."); 
        // [header, payload, signature] 
        var decodedIdentity= base64url(idTokenComponents[1]);
        req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"]; 
        res.redirect("/"); 
        }
   ).auth(mcaCredentials.clientId, mcaCredentials.secret); 

   }
  ); 
   
  ```
 
 Note that the `redirect_uri` parameter must match the `redirect_uri` used for the previous authorization request. The `code` parameter value should be the grant code received in the response from  the authorization request. The grant code is valid for 10 minutes, after which a new code must be be retrieved.

The response body will contain the access code and token ID in JWT format (https://jwt.io/).

Once you have gained access and received the identity tokens, you can flag web session as authenticated, and optionally persist these tokens.  

##Using obtained access and identity token 

The identity token contains information about user identity. In case of Facebook authentication, the token will contain all the information user agreed to share, such as full name, age group, url of the profile photo, etc.  

The access token enables communications with resources protected by {{site.data.keyword.amashort}} authorization filters, see see [Protecting Resources](protecting-resources.html).


To make requests to protected resources, add an authorization header to requests with the following structure: 

`Authorization=Bearer <accessToken> <idToken>`

#### Tips
{: tips} 

* You must separate the `accessToken` and `idToken` with a white space.

* The `idToken` is optional. If you do not supply the identity token, the protected resource can be accessed, but will not receive any information about the authorized user. 
 



