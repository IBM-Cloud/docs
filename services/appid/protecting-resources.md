---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Protecting back-end resources
{: #protecting-resources}

The {{site.data.keyword.appid_short}} server SDK provides strategies for protecting two types of resources: APIs and web applications.
{:shortdesc}


## Accessing protected resources from client SDKs
{: #accessing}

Calling a protected resource launches the login widget, if necessary. If a valid token was already obtained, the login widget is not launched, and the resource is accessed directly.


### Using the Swift SDK
{: #requesting-swift notoc}

1. Import BMSCore.

  ```swift
  import BMSCore
  ```
  {:pre}

2. Invoke a protected resource request.

  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //code handling the response here
  })
  ```
  {:pre}


### Using the Android SDK
{: #requesting-android notoc}

1. Invoke a protected resource request.

  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
  public void onSuccess (Response response) {
     //code handling the response here
  }
  @Override
  public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
      //code handling the failure here
  });
  ```
  {:pre}



## Authorization filters
{: #auth-filter}

The API protection strategy returns an HTTP 401 response with a list of scopes to obtain authorization for an unauthenticated client. The web application protection strategy returns an HTTP 302 redirect. The redirect sends an unauthenticated client to the login page that is hosted by the {{site.data.keyword.appid_short_notm}} service, or directly to an identity provider login page, depending on your configuration.



### API strategy
{: #api notoc}

The API strategy expects requests to contain an authorization header with a valid access token. The response can also include an identity token, but it is not required; see [Access and identity tokens](/docs/services/appid/about.html#acess-and-identity).

If a token is invalid or expired, the API strategy returns an HTTP 401 error that contains the following information: Www-Authenticate=Bearer scope="{scope}" error="{error}". The `error` component is optional.

If the request returns a valid token, control is passed to the next middleware and the `appIdAuthorizationContext` property is injected into the request object. This property contains original access and identity tokens, as well as decoded payload information as plain JSON objects.


### Web app strategy
{: #web notoc}

When the web app strategy class detects unauthenticated attempts to access a protected resource, it automatically redirects a user's browser to the authentication page. After successful authentication, the user is returned to the web application's callback URL. The service uses the web app strategy class to obtain access and identity tokens. After obtaining these tokens, the web app strategy class stores them in an HTTP session under `WebAppStrategy.AUTH_CONTEXT`. It is up to the user to decide whether to store access and identity tokens in the application database.

## Authorization header
{: #auth-header}

The authorization header in the incoming request consists of three parts that are separated by white spaces: Bearer, Access Token, and ID Token. Access Token is a mandatory component and ID Token is optional. The expected header structure is: Authorization=Bearer {access_token} [{id_token}]
