---

copyright:
  years: 2017
lastupdated: "2017-05-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# How it works
{: #about}

You can learn about the components, architecture, and request flow that {{site.data.keyword.appid_full}} uses.
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
{: #architecture}

With {{site.data.keyword.appid_short_notm}} you can add a level of security to your applications by requiring users to sign in. You can also use the server SDK to protect your back end resources.

The following diagram shows an overview of how the {{site.data.keyword.appid_short_notm}} service works.

![{{site.data.keyword.appid_short_notm}} architecture diagram](/images/appid_architecture2.png)

Figure 1. {{site.data.keyword.appid_short_notm}} architecture diagram

<dl>
  <dt> Client SDK </dt>
    <dd> The client SDK provides a request class to communicate with your cloud resources. The client SDK automatically starts the authentication process when it detects an authorization challenge. </dd>
  <dt> Bluemix </dt>
    <dd>  The server SDK extracts the access token from the request and validates it with {{site.data.keyword.appid_short_notm}}. After successful authentication, {{site.data.keyword.appid_short_notm}} returns authorization and identity tokens to your application. </dd>
  <dt> Identity Providers </dt>
    <dd> You can configure Facebook, Google, or both to authenticate your apps.  </dd>
</dl>


## Request flow
{: #request}

The following diagram describes how a request flows from the client SDK to your back-end application and identity providers.

![{{site.data.keyword.appid_short_notm}} request flow](/images/appidflow.png)

Figure 2. App ID request flow

* Use the {{site.data.keyword.appid_short_notm}} client SDK to make a request to your back-end resources that are protected with the {{site.data.keyword.appid_short_notm}} server SDK.
* The {{site.data.keyword.appid_short_notm}} server SDK detects an unauthorized request and returns an HTTP 401 and authorization scope.
* The client SDK automatically detects the HTTP 401 and starts the authentication process.
* When the client SDK contacts the service, the server SDK returns the login widget if more than one identity provider is configured. {{site.data.keyword.appid_short_notm}} calls the identity provider and presents the login form for that provider, or returns a grant code that allows them to authenticate if no identity providers are configured.
* {{site.data.keyword.appid_short_notm}} asks the client app to authenticate by supplying an authentication challenge.
* If Facebook or Google are configured, and the user logs in, the authentication is handled by the respective identity provider OAuth Flow.
* If the authentication ends with the same grant code, the code is sent to the token endpoint. The endpoint returns two tokens: an access token and an identity token. From this point on, all requests that are made with the client SDK have a newly obtained authorization header.
* The client SDK automatically resends the original request that triggered the authorization flow.
* The server SDK extracts the authorization header from the request, validates the header with the service, and grants access to a back-end resource.
