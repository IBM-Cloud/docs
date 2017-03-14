---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Configuring identity providers
{: #setting-up-idp}

You can configure Facebook, Google, or both to authenticate your applications and authorize access to protected back-end resources.
{:shortdesc}


## Facebook
{: #facebook}

Configure the {{site.data.keyword.appid_short}} service to use Facebook as an identity provider.

<!--- ### Sequence diagram
{: #facebook-sequence-diagram}--->

### Getting an app ID and secret from Facebook
{: #getting-facebook-appid}

To use Facebook as an identity provider on your mobile or web apps, you must add and configure the website platform on your Facebook application.

1. Log in to your account on the Facebook for Developers site. For information about creating a new Facebook app, see <a href="https://developers.facebook.com/docs/apps/register" target="_blank">Creating an application <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
2. Make note of the Facebook app ID and secret. You need these values to configure your web project for authentication in your service dashboard.
3. Add the web platform and enter the site URL.
4. From the products list, select **Facebook Login**.
5. In the Valid OAuth redirect URLs field, enter the authorization server callback endpoint URL. You can add this value after you have configured your {{site.data.keyword.appid_short_notm}} service in the steps that follow.
6. Click **Save Changes**.

### Configuring {{site.data.keyword.appid_short_notm}} for Facebook authentication
{: #configuring-facebook-appid}

When you have your Facebook app ID and secret, and your Facebook for Developers app is configured to serve web clients, you can edit the Facebook authentication in your service dashboard.

1. From the **Manage** tab of your service dashboard, select **Facebook** and click **Edit**.
2. Enter the Facebook app ID and secret that you obtained from the Facebook for Developers website.
3. Copy the URI that is in the **Redirect URI for Facebook for Developers** field. Paste the URI in to the **Valid OAuth redirect URIs** field in the **Facebook Login** section of the Facebook Developers Portal.
4. Click **Save**.
5. Optional: To configure authentication for web apps, enter the redirect URI in the your Web Application Redirect URIs. This value is determined by the developer and used to access the redirect URI after the authorization process is completed.


## Google
{: #google}

Configure the {{site.data.keyword.appid_short_notm}} service to use Google as an identity provider.

<!--- ### Sequence diagram
{: #google-sequence-diagram}--->

### Getting a client ID and secret from Google
{: #google-client-id}

To use Google as an identity provider, obtain a Google client ID and secret and create a project in the Google Developer Console.

1. Open your Google application in the Google Developer Console.
2. Add the Google+ API.
3. Create credentials by using OAuth. In the **Application Type** field, select **Web application**. In the **Authorized redirect URIs** field, enter the App ID redirect URI. You can obtain the App ID redirect authorization URI from the Google configuration screen of the service dashboard.
4. Save your changes. Make note of the Google client ID and secret.




### Configuring {{site.data.keyword.appid_short_notm}} for Google authentication
{: #google-client-appid}

When you have your Google client and secret, and your Google Developers console is configured to serve web clients, you can edit the Google authentication in your service dashboard.

1. From the **Manage** tab of your service dashboard, select **Google** and click **Edit**.
3. Enter the Google Client ID and Secret that you obtained from the Google Developers console.
4. Copy the URI that is in the **Redirect URI for Google for Developers** field. Paste the URI in to the **Authorized redirect URIs** field that is under **Restrictions** in the **Client ID for Web application** section of the Google Developers Portal.
5. Click **Save**.
6. Optional: To configure authentication for web apps, enter the redirect URI in the Web Application Redirect URIs field. This value is determined by the developer and used to access the redirect URI after the authorization process completes.



<!---[## Bring your own OAuth2/OIDC identity provider
{: #oauth2}

### About
{: #oauth2-about}
### Sequence diagram
{: #oauth2-sequence-diagram}
### Configuring AppID for BYOIDP OAuth2 authentication
{: #oauth2-appid} SHAWNA: Is this Interconnect?]--->
