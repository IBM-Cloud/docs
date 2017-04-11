---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# About {{site.data.keyword.appid_short_notm}}
{: #about}

With {{site.data.keyword.appid_full}} developers can secure and add authentication to their {{site.data.keyword.Bluemix}} apps, with a few lines of code. Developers can also manage user-specific data to build personalized app experiences.
{:shortdesc}


You can use the service in the following ways:

* To add authentication to your mobile and web applications
* To grant access to protected back-end resources and web apps
* To protect Node.js and Swift applications that are hosted on {{site.data.keyword.Bluemix_notm}}
* To store user data, such as app preferences or information from their public social profiles
* To use stored data to build personalized app experiences
* To protect resources for both authenticated and anonymous users

**Note**: The implemented protocols are fully compliant with OpenID Connect (OIDC).


## Components
{: #components}

* Dashboard - Download onboarding samples, see activity logs, configure various authentication types and identity providers
* Client SDK - Build mobile and web apps that use the service to implement user authentication
    * Prerequisites for Android: API 25 or higher, Java 8.x, Android SDK tools 25.2.5 or higher, Android SDK Platform Tools 25.0.3 or higher, Android Build Tools version 25.0.2
    * Prerequisites for iOS: iOS9 or higher, MacOS 10.11.5, Xcode 8.2
* Server SDK - Protect resources that are hosted on {{site.data.keyword.Bluemix_notm}}
    * Supported runtimes are Node.js and Swift

## Architecture overview

![{{site.data.keyword.appid_short_notm}} architecture diagram](/images/appid_architecture.png)

Figure 1. {{site.data.keyword.appid_short_notm}} architecture diagram

You can protect your cloud resources with the {{site.data.keyword.appid_short_notm}} server SDK. Use the request class that is provided by the {{site.data.keyword.appid_short_notm}} client SDK to communicate with your protected cloud resources.

* The server SDK detects an unauthorized request and returns HTTP 401 authorization challenge.
* The client SDK detects an HTTP 401 Authorization challenge and automatically starts the authentication process based on configuration of the identity providers.
* Authentication is attempted according to currently configured identity providers.
* After successful authentication, the service returns authorization and identity tokens.
* The client SDK automatically adds the authorization token to the original request, and resends the request to the cloud resource.
* The server SDK extracts the access token from the request and validates it with {{site.data.keyword.appid_short_notm}}.
Access is granted and the response is returned to the application.


## Request flow
{: #request}

The following diagram describes how a request flows from the client SDK to your back-end application and identity providers.

![{{site.data.keyword.appid_short_notm}} request flow](/images/appidflow.png)


* Use the {{site.data.keyword.appid_short_notm}} client SDK to make a request to your back-end resources that are protected with the {{site.data.keyword.appid_short_notm}} server SDK.
* The {{site.data.keyword.appid_short_notm}} server SDK detects an unauthorized request and returns an HTTP 401 and authorization scope.
* The client SDK automatically detects the HTTP 401 and starts the authentication process.
* When the client SDK contacts the service, the server SDK returns the login widget if more than one identity provider is configured. {{site.data.keyword.appid_short_notm}} calls the identity provider and presents the login form for that provider, or returns a grant code that allows them to authenticate if no identity providers are configured.
* {{site.data.keyword.appid_short_notm}} asks the client app to authenticate by supplying an authentication challenge.
* If Facebook or Google are configured, and the user logs in, the authentication is handled by the respective identity provider OAuth Flow.
* If the authentication ends with the same grant code, the code is sent to the token endpoint. The endpoint returns two tokens: an access token and an identity token. From this point on, all requests made with the client SDK have a newly obtained authorization header.
* The client SDK automatically resends the original request that triggered the authorization flow.
* The server SDK extracts the authorization header from the request, validates the header with the service, and grants access to a back-end resource.

## Access and identity tokens
{: #access-and-identity}

{{site.data.keyword.appid_short}} uses two types of tokens: access and identity. The tokens are formatted as <a href="https://jwt.io/introduction/" target="_blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.


### Access token
{: #access-tokens notoc}

The access token enables communication with resources that are protected by {{site.data.keyword.appid_short_notm}} authorization filters, see [Protecting back-end resources](/docs/services/appid/protecting-resources.html).
The token conforms to JavaScript Object Signing and Encryption (JOSE) specifications and has the following format:

```
Header: {

    "typ": "JOSE", // header type, according to spec

    "alg": "RS256", // algorithm, according to spec

}
Payload: {

    "iss": "", // issuer, the AppID server that issued this token. StringOrURL

    "sub": "", // subject, who this token was issued to. Most probably userId

    "aud": "", // audience, who is this token intended for. OAuth2 client_id.

    "exp: "", // expiration timestamp, epoch time

    "iat": "", // issued at timestamp, epoch time

    "tenant": "xxx", the AppID tenantId the token was issued for

    "auth_by": "appid_anon / appid_facebook / appid_google",

    "scope": "", // the scope[s] this token was issued for

}
```
{:screen}

### Identity token
{: #identity-tokens notoc}

The identity token contains information about the user, including name, email, gender, picture, and location.

```
Header: {

    "typ": "JOSE", // header type, according to spec

    "alg": "RS256", // algorithm, according to spec

}
Payload: {

    "iss": "", // issuer, the AppID server that issued this token. StringOrURL

    "sub": "", // subject, who this token was issued to. AppID userid.

    "aud": "", // audience, who is this token intended for. OAuth2 client_id.

    "exp: "", // expiration timestamp, epoch time

    "iat": "", // issued at timestamp, epoch time

    "tenant": "xxx", // the AppID tenantId the token was issued for

    "name": "John Smith", // user's full name as reported by IDP, mandatory,

    "email": "js@mail.com", // user's email as reported by IDP, only if available,

    "gender", "male", // user's gender as reported by IDP, only if available,

    "locale": "en", // user's locale as reported by IDP, only if available

    "picture": "https://url.to.photo", // URL to user's picture, only if available

    "auth_by": "appid_facebook/appid_google", // the name of IDP used for authentication, mandatory

    "identities": [

        "provider: "appid_facebook/appid_google", // mandatory

        "id": "unique user id as reported by IDP", // mandatory

        "profile": { ... } // JSON object returned by IDP,  mandatory

      },

      {...}, {...} // more linked identities

    ],

    "oauth_client":{

      "type": "serverapp/mobileapp from client registration", // mandatory

      "name": "client_name as reported during client registration", // mandatory

      "software_id": "software_id as reported during client registration", // mandatory

      "software_version": "software_version as reported during client registration", // mandatory

      "device_id": "device_id from client registration", //mobile only

      "device_model": "device_model from client registration", //mobile only

      "device_os": "device_os from client registration", //mobile only

    }

}
```
{:screen}


## Identity providers overview
{: #identity-providers-overview}

You can use the following identity providers in your mobile and web applications:

* **Facebook** - Your users log in to the mobile or web app with their Facebook credentials.
* **Google** -  Your users log in to the mobile or web app with their Google+ credentials.
<!--* **Custom** - Bring your own identity provider. The identity providers should be compliant with OIDC. -->

## Using the default configuration
{: #default-configuration}

{{site.data.keyword.appid_short_notm}} provides a default configuration when you initially set up your identity providers. You can use the default configuration in development mode only. For each identity provider, these credentials are limited to 100 uses per {{site.data.keyword.appid_short_notm}} instance, per day. Before you publish your application, update the default configuration to your own credentials. To update your configuration, see [Configuring identity providers](/docs/services/appid/identity-providers.html).
