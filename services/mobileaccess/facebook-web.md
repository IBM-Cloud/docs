---

copyright:
  year: 2016, 2017
lastupdated: "2017-04-06"

---

**Important: The {{site.data.keyword.amafull}} service is replaced with the {{site.data.keyword.appid_full}} service.**

# Enabling Facebook authentication for Web apps
{: #facebook_web}

Use Facebook to authenticate users on your web app.

## Before you begin
{: #facebook-auth-android-before}
You must have:
* A web app.  
* An instance of a  {{site.data.keyword.Bluemix_notm}} application that is protected by {{site.data.keyword.amashort}} service. For more information about how to create a {{site.data.keyword.Bluemix_notm}} back-end, see [Getting started](index.html).
* A Facebook Application ID and App Secret. For more information, see [Obtaining a Facebook application ID from the Facebook Developer Portal](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).


## Configuring a Facebook application for your website
To use Facebook as identity provider on your website, you must add and configure the website platform on your Facebook application.

1. Open your Facebook application in the Facebook Developer Portal.
1. Take note of the Application ID for your app and App Secret. You need this value when you configure your web project for Facebook authentication.
1. From the **Settings** page click **Add Platform** and choose **Website**.
1. Save changes.
1. Click on **Facebook Login** in the side bar.
1. Enter the authorization server callback end-point in the **Valid OAuth redirect URIs** box: https://imf-newauthserver.bluemix.net/oauth/{bluemix_app_guid}/callback. Save changes.




# Configuring {{site.data.keyword.amashort}} for Facebook authentication
After you have your Facebook Application ID and App Secret, and your Facebook Application has been configured to serve web clients, you can enable Facebook authentication in the  {{site.data.keyword.Bluemix_notm}}  dashboard.

1. Open your app in the  {{site.data.keyword.Bluemix_notm}} dashboard.
1. Click the {{site.data.keyword.amashort}} tile. The {{site.data.keyword.amashort}} dashboard loads.
1. Click the Facebook tile.
1. Enter the Facebook Application ID and App Secret, and save.




## Using Mobile Client Access for Facebook web authentication

To start the process of authorization:

1. Redirect from your web app to the following end-point of the authorization server:  https://imf-newauthserver.bluemix.net/oauth/v2/authorization.

1. Add the following query parameters:
   ```
    response_type='authorization_code'
    client_id= <bluemix_app_guid>
    redirect_uri= <uri for redirecting after receiving the authorization code>
    scope= 'openid'
    state= <state>
    ```


  The `state` parameter is not in use for now and can remain empty.
  The `redirect_uri` parameter is the uri for redirecting after successful or failed authentication with Facebook.

1. After redirecting to the authorization end-point you will get a login form from      
   Facebook. Enter the username and password to redirect to the `redirect_uri`.
   The response you get after redirecting  contains the authorization code in the request query parameters.

1. Make a `POST` request to the authorization server's token end-point:

  https://imf-newauthserver.bluemix.net/oauth/v2/token

  using the following query parameters:
  ```
  grant_type='authorization_code'
  client_id= <bluemix_app_guid>
  code= <authorization code>
  ```
The `redirect_uri` parameter must match the `redirect_uri` from step 2.
The `code` value is the authorization code received in the response at the end of end of step 3.
Make sure to send this `POST` request within 10 min since the authorization code is valid for 10 min max.

  The `POST` response body should contain the `access_token` and the `id_token` encoded in base64.

## Testing the authentication
Now you can start making requests to your protected resources.
All request to protected resources should contain the `access_token` in the Authorization request header field.
