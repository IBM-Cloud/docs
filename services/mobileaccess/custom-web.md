---

copyright:
  years: 2016
lastupdated: "2016-06-16"

---

# Web app custom authentication
{: #custom-web}

Add custom authentication to your web app

## Before you begin
{: #before-you-begin}

You must have:
* A web app with a  `/apps/:Guid/<RealmName>/handleChallengeAnswer` endpoint, which
returns a user identity upon authentication success. The user identity JSON structure should be as follows:

   ```json
  userIdentity: {
  userName: <username>,
  displayName: <displayName>;
 };
```
* An instance of a  {{site.data.keyword.Bluemix_notm}} application that is protected by {{site.data.keyword.amashort}} service. For more information about how to create a {{site.data.keyword.Bluemix_notm}} back-end, see [Getting started](index.html).



## Configuring a {{site.data.keyword.amashort}} app for custom authentication


1. Open your app in the  {{site.data.keyword.Bluemix_notm}} dashboard.
1. Click the {{site.data.keyword.amashort}} tile. The {{site.data.keyword.amashort}}
dashboard loads.
1. Click the Custom tile.
1. Enter the **custom realm**, **custom identity provider url** and **redirect_uri**. Click save.

## Using {{site.data.keyword.amashort}} for custom web authentication

To start the process of authorization:

1. Redirect from your web app to
 the following end-point of the authorization server:

    https://imf-newauthserver.bluemix.net/oauth/v2/authorization

  using the following query parameters:
   ```
   response_type=’authorization_code’
   client_id= <bluemix\_app\_guid>
   redirect_uri= <uri for the redirect after getting an authorization code>
   scope= ‘openid’
   state= <state>
   ```

    The `state` parameter is not currently in use and you can leave it empty.

    The `redirect_uri` parameter determines the redirect after the successful or failed authentication of your custom identity provider.

1. After redirecting to the authorization end-point you get a login
form. Enter the username and password to initiate authentication
against your identity provider, and a redirect to the `redirect_uri`.
The response returned after a successful authentication contains the authorization code in the request query parameters.

4. Make a `POST` request to the authorization server token end-point:

 https://imf-newauthserver.bluemix.net/*oauth/v2/token

 using the following query parameters:
 ```
 grant_type = 'authorization_code'
 client_id = <bluemix_app_guid>
 redirect_uri = <redirect_uri>
 code = <authorization code>
 ```
  The `redirect_uri` parameter must match the `redirect_uri` from step 1. The authorization code was returned by the request in the step 2.

  Make sure to send this `POST` request within 10 min since the grant code is valid for 10 min max.

The `POST` response body contains the *access_token* and the
*id_token* encoded in base64.

## Testing the authentication


Now you can start making requests to your protected resources.
All requests to protected resources should contain the `access_token`.
Send the access token in `the-Authorization-request` header field.
