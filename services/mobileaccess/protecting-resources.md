---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-27"

---

{:shortdesc: .shortdesc} {:codeblock:.codeblock}

# Protecting back-end resources with the {{site.data.keyword.amashort}} service
{: #protecting-resources}


With the {{site.data.keyword.amafull}} service, you can protect your Node.js and Java-based back-end applications that are running on {{site.data.keyword.Bluemix_notm}} with mobile-enabled OAuth security and monitoring.
{:shortdesc}

## Before you begin
{: #before-you-begin}
Before you begin, ensure that the Node.js service exists in your {{site.data.keyword.Bluemix_notm}} back-end application.


## Authorization filter
{: #auth-filter}
The {{site.data.keyword.amashort}} server SDK has authorization filters that you can use to protect your back-end applications.  The authorization filter intercepts incoming requests and validates whether an authorization header is present. If the authorization header is not present or is invalid, the filter returns a response with HTTP 401. The {{site.data.keyword.amashort}} client SDK knows how to intercept an HTTP 401 response that is returned by the {{site.data.keyword.amashort}} server SDK, and triggers the authentication flow.
## Authorization header
{: #auth-header}
The authorization header in the incoming request consists of three parts: Bearer, Access Token, and ID Token that are separated by white spaces. `Access Token` is a mandatory component while `ID Token` is optional.

The incoming authorization header is processed by respective authorization filter. The filter validates the access token and ID token signatures, expiration date, and structural integrity. After validation has passed, a security context object is added to the request object. You can get a reference to the security context by using the relevant API.

The security context contains the subject, user, device, and the application information stored with a following structure:
```JSON
{
    "imf.sub":"myclientid",
    "imf.user": {
        "id":"user-name",
        "authBy":"myrealm",
        "displayName":"display-name"
    },
    "imf.device": {
        "id":"device-id",
        "platform":"iOSnative",
        "model":"device-model",
        "osVersion":"device-os"
    },
    "imf.application": {
        "id":"ios.bundle.id",
        "version":"1.0"
    }
}
```
{: codeblock}

* `imf.sub`: Specifies the subject of the ID token or the unique ID of the client if no ID token exists.
* `imf.user`: Specifies the user identity that is extracted from the ID token. If no ID token exists, this field holds an empty object.
* `imf.device`: Specifies the device identity that is extracted from the ID token. If no ID token exists, this field holds an empty object.
* `imf.application`: Specifies the application identity that is extracted from the ID token. If no ID token exists, this field holds a blank object.

## Next steps
{: #next-steps}
* [Protecting Node.js resources](protecting-resources-nodejs.html)
* [Protecting Liberty for Java&trade; resources](protecting-resources-java.html)
* [Local development](protecting-resources-local.html)
