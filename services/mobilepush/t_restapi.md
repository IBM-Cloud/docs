---

copyright:
 years: 2015, 2016

---

# Using REST APIs
{: #push-api-rest}

You can use a REST (Representational State Transfer) API (application program interface) for push notifications. You can also use the SDK and [Push API](https://mobile.{DomainName}/imfpushrestapidocs/) to further develop your client applications.

With the Push REST API, backend server applications and clients can access Push functions.

- Device registrations
- Registrations
- Messages
- Subscriptions
- Tags

To obtain the base URL for the REST API:

1. Create a backend application in the Boilerplates section Bluemix® catalog, which automatically binds the Push service to this application. If you already created a backend app, make sure that you bind the app to the Push Notification Service. 

1. In the main page of the Bluemix dashboard, go to the **Applications** area and then click your app.

3. Click MOBILE OPTIONS. The route and app GUID values are displayed at the top of the details page for your app.



## Accept language header
{: #push-api-rest-accept}

The "Accept-Language" header specifies which language to use for the error messages that are output by [Push REST API](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}. The following languages are supported for error messages: Chinese (Simplified), Chinese, (Traditional), English (US), German, French, Italian, Japanese, Korean, Portuguese, and Spanish.

## appSecret
{: #push-api-rest-secret}

When an application binds to the Push Notifications, the service generates an appSecret (a unique key) and passes it in the response header. If you are using the IBM® Push Notifications for Bluemix Rest API, use the REST API reference to obtain information on which APIs you need to secure. For information about the REST API, see REST API Reference.

The request header must contain the appSecret. If not, the server returns a 401 Unauthorized Error code. When the Push Notification is added to an application, a specific AppID is created. As part of the response, you get a header called appSecret that is used for creating Tags or sending messages. The operation happens through services in the catalog or the boilerplate.

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
       "appSecret": "8dac71a5-2219-42b3-a9f3-dbb828ba1f04"  
       }
   }
 ]
}
``` 

##Push REST API filters
{: #push-api-rest-filters}

Filters define a search criteria that restrict data that is returned from a GET API of Push. Apply the filters against the result of the Get operation that you want to filter. The filter restricts the number of entries that are included in the result. For example, you can use a filter to search a tag with a starts with "test". You can generate a filter by using the following syntax.

**name**
The field name on which the filter is being applied.

**operator**
Either == (Exact Match) or =@ (Contains Substring) that describes filter match to use.

**expression**
The values to include in the result.

When a comma and a backslash are displayed in an expression, they must be backslash-escaped.

When you are using multiple filters, they can be combined by using AND and OR logic.\

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
