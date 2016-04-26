---

copyright:
  years: 2015, 2016

---

# Using Google to authenticate users
{: #google-auth}
You can configure the {{site.data.keyword.amashort}} service to protect resources, using Google as identity provider. Your mobile application users can then use their Google credentials for authentication.

**Important:** You do not need to separately install the Google SDK. The Google SDK is installed automatically by dependency managers when you configure the {{site.data.keyword.amashort}} client SDK.

## {{site.data.keyword.amashort}} flow
{: #google-auth-overview}

See the following simplified diagram to understand how {{site.data.keyword.amashort}} integrates with Google for authentication.

![image](images/mca-sequence-google.jpg)

1. Use the {{site.data.keyword.amashort}} SDK to make a request to your backend resources that are protected  with the {{site.data.keyword.amashort}} server SDK.
* The {{site.data.keyword.amashort}} server SDK detects the unauthorized request and returns an HTTP 401 code and authorization scope.
* The {{site.data.keyword.amashort}} client SDK automatically detects the HTTP 401 code and starts the authentication process.
* The {{site.data.keyword.amashort}} client SDK  contacts the {{site.data.keyword.amashort}} service and asks to issue an authorization header.
* The {{site.data.keyword.amashort}} service asks the client to authenticate with Google first by supplying an authentication challenge.
* The {{site.data.keyword.amashort}} client SDK uses the Google SDK to start the authentication process. After successful authentication, the Google SDK returns a Google access token.
* The Google access token is considered an authentication challenge answer. The token is sent to the {{site.data.keyword.amashort}} service.
* The service validates the authentication challenge answer with Google servers.
* If validation is successful, the {{site.data.keyword.amashort}} service generates an authorization header and returns it to the {{site.data.keyword.amashort}} client SDK. The authorization header contains two tokens: an access token that contains access permissions information, and ID token that contains information about the current user, device, and application.
* From this point on, all requests that are made through the {{site.data.keyword.amashort}} client SDK  have a newly obtained authorization header.
* The {{site.data.keyword.amashort}} client SDK automatically resends the original request that triggered the authorization flow.
* The {{site.data.keyword.amashort}} server SDK extracts the authorization header from the request, validates it with the {{site.data.keyword.amashort}} service, and grants access to a backend resource.

## Next steps
{: #google-auth-nextsteps}

* [Enabling Google authentication in Android apps](google-auth-android.html)
* [Enabling Google authentication in iOS apps (Swift SDK)](google-auth-ios-swift-sdk.html)
* [Enabling Google authentication in iOS apps (Objective-C SDK)](google-auth-ios.html)
* [Enabling Google authentication in Cordova apps](google-auth-cordova.html)
