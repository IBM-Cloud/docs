---

copyright:
  year: 2016, 2017
lastupdated: "2017-04-06"

---

**Important: The {{site.data.keyword.amafull}} service is replaced with the {{site.data.keyword.appid_full}} service.**

# Enabling Google authentication for web apps
{: #google-auth-web}

Use Google Sign-In to authenticate users on your web app.


## Before you begin
{: #before-you-begin}

You must have:
* A web app.
* An instance of a  {{site.data.keyword.Bluemix_notm}} application that is protected by {{site.data.keyword.amashort}} service. For more information about how to create a {{site.data.keyword.Bluemix_notm}} back-end, see [Getting started](index.html).

## Configuring a Google application for your website
To start using Google as an identity provider, create a project in the [Google Developer Console](https://console.developers.google.com). Part of creating a project is to obtain a Google Client ID and Secret. The Google Client ID and Secret are the unique identifiers for your application used by Google authentication, and are needed for setting up the {{site.data.keyword.Bluemix_notm}} application.

1. Create a project using the Google+ API.
1. Create credentials using  **OAuth**. To create the credentials you need to:
    * Select **Web application**  application type.
    * Provide the **Authorized redirect URIs** value:

     https://imf-newauthserver.bluemix.net/oauth/{bluemix_app_guid}/callback
1. Complete the credentials creation and take note of the Google Client ID and Secret.


## Configuring Mobile Client Access for Google authentication
After you have a Google Application ID and Secret, you can enable Google authentication in the {{site.data.keyword.amashort}}  dashboard.

1. Open your app in the  {{site.data.keyword.Bluemix_notm}}  dashboard.
1. Click the {{site.data.keyword.amashort}} tile. The {{site.data.keyword.amashort}}  dashboard loads.
1. Click the Google tile.
1. Enter the Google Client ID and Secret, and save.


## Using Mobile Client Access for Google web authentication
To start the process of authorization:

1. Redirect from your web app to the following end-point of the authorization server:  
  https://imf-newauthserver.bluemix.net/oauth/v2/authorization

  using the following query parameters:
	```
   response_type='authorization_code'
   client_id= <bluemix_app_guid>
   redirect_uri= <uri which you want to return to after getting a grant code>
   scope= ‘openid’
   state= <state>
	```

  The `state` parameter is not in use for now and can remain empty.

  The `redirect_uri` parameter uri is the redirect after successful or failed authentication with Google.
  The response you get after redirect  contains the authorization code in the request query parameters.
1. Make a `POST` request to the authorization server token end-point:

 https://imf-newauthserver.bluemix.net/oauth/v2/token


  using the following query parameters:

	```
  	grant_type=’authorization_code’
    client_id= < bluemix_app_guid >
    redirect_uri= <redirect_uri >
    code= <authorization code>
	```
  The `redirect_uri` parameter must match the `redirect_uri` from step 1 and the`<authorization code>` value is received from the response.
  Make sure to send this `POST` request within 10 min since the grant code is valid for 10 min max.

The `POST` response body should contain the `access_token` and the `id_token` encoded in base64.

## Testing the authentication

Now you can start making requests to your protected resources.
All request to protected resources should contain the access token in the authorization request header field.
