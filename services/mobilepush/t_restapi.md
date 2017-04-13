---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Using REST APIs
{: #push-api-rest}
Last updated: 28 February 2017
{: .last-updated}

You can use a REST (Representational State Transfer) API (application program interface) for {{site.data.keyword.mobilepushshort}}. You can also use the SDK and [Push API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://mobile.{DomainName}/imfpush/){: new_window} to further develop your client applications.

With the Push REST API, backend server applications and clients can access {{site.data.keyword.mobilepushshort}} functions.

- Device registrations
- Registrations
- Messages
- Subscriptions
- Tags
- Webhooks

To obtain the base URL for the REST API, complete the steps:

1. Create a back end application in the Boilerplates section Bluemix® catalog by choosing the MobileFirst Services Starter. This binds the {{site.data.keyword.mobilepushshort}} service to the application. You can also create a service instance of Push and leave it unbounded. 
1. In the main page of the Bluemix dashboard, go to the **Applications** area and then select your app.
3. Click **MOBILE OPTIONS**. The route and app GUID values are displayed at the start of the details page for your app. The Show Credentials screen shows information about the AppSecret. You can get the application secret from Mobile Options and also client secret for some of the API's.

You can also use the command line to get the service credentials:

```
    cf create-service-key {push_instance_name} {key_name}
    cf service-key {push_instance_name} {key_name}
```
	{: codeblock}

## Accept language header
{: #push-api-rest-accept}

The "Accept-Language" header specifies which language to use for the error messages that are output by [Push REST API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://mobile.{DomainName}/imfpush/){: new_window}. The following languages are supported for error messages: Chinese (Simplified), Chinese, (Traditional), English (US), German, French, Italian, Japanese, Korean, Portuguese, and Spanish.

## appSecret 
{: #push-api-rest-secret}

When an application binds to the {{site.data.keyword.mobilepushshort}}, the service generates an appSecret (a unique key) and passes it in the response header. If you are using the IBM {{site.data.keyword.mobilepushshort}} for Bluemix Rest API, use the REST API reference to obtain information on which APIs you need to secure. For information, see the [Push REST API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://mobile.{DomainName}/imfpush/){: new_window}.

The request header must contain the appSecret. If not, the server returns a 401 Unauthorized Error code. When the {{site.data.keyword.mobilepushshort}} is added to an application, a specific AppID is created. As part of the response, you get a header called appSecret that is used for creating tags or sending messages. The operation happens through services in the catalog or the boilerplate.

To get the appSecret value:

1. Click the *app-name* that is bound to the push service.
2. Click the **Show Credentials** link to display the appSecret (AppID).

The **Show Credentials** screen shows information about the AppSecret:
```
	{
    "imfpush_Dev": [
    {
     "name": "testapp1",
     "label": "imfpush_Dev",
     "plan": "Basic",
     "credentials": {
       "url": "http://imfpush.ng.bluemix.net/imfpush/v1/apps/b615b280-b37e-4042-8815-38a758f234e2",
       "admin_url": "//mobile.ng.bluemix.net/imfpushdashboard/?appGuid=b615b280-b37e-4042-8815-38a758f234e2",
       "appSecret": "8dac71a5-2219-42b3-a9f3-dbb828ba1f04",
       }
     }
    ]
    }
```
	{: codeblock} 


## Push REST API filters
{: #push-api-rest-filters}

Filters define a search criteria that restrict data that is returned from a GET API of {{site.data.keyword.mobilepushshort}}. Apply the filters against the result of the Get operation that you want to filter. The filter restricts the number of entries included in the result. For example, you can use a filter to search for tags that start with "test". 

Filters can be generated using the following syntax:

**name**: The field name on which the filter is being applied.

**operator**: Either == (Exact Match) or =@ (Contains Substring) that describes filter match to use.

**expression**: The values to include in the result.

When a comma and a backslash are displayed in an expression, they must be backslash-escaped.

When you are using multiple filters, they can be combined by using AND and OR logic.

- For AND logic, use multiple filters in the query.
- For OR logic, use a comma(,) inside of the filter expression.
- For both AND and OR logic: A single query can have both AND and OR logic. Each filter is evaluated individually before the filters are combined in an AND expression.

For the device GET API the following combinations are supported:
-The name is the platform field.
- Except for the platform, the operator can be == or =@
- For the platform, the operator must be ==. If operator =@ is used, the value can be a sub string.
- If == is used, the value must be an exact matching string.

For the subscription GET API the following combinations are supported:

- The name can be one of these fields: tagName or deviceId
- Except for the platform, the operator can be == or =@
- For the platform, the operator must be ==
- If the =@ operator is used, the value can be a sub string. If the == operator is used, the value must be an exact matching string.
- For the tag GET API the following combinations are supported:
- The name can be one of these fields: “name” or “description”
- If operator =@ is used, the value can be a sub string.
- If == is used, the value must be an exact matching string.


## Push Notifications service response codes
{: #push-api-response-codes}

Status: 405 Method Not Allowed - Appropriate method expected.
