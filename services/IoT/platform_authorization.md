---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Application connection
To connect your application to {{site.data.keyword.iot_full}}, you must connect by using API keys and tokens or binding your application directly to {{site.data.keyword.iot_short_notm}} in {{site.data.keyword.Bluemix_notm}}. You use the access dashboard to grant access.
{:shortdesc}

## API key connection
API keys are used when connecting applications to your {{site.data.keyword.iot_short_notm}} organization. Applications require an API key to connect into an organization and a unique authentication token that must be used with that API key.  

For more information about application connections, see [MQTT Connectivity for Applications](https://docs.internetofthings.ibmcloud.com/applications/mqtt.html) in the developer documentation.

To create a new API key and authentication token pair:  
1.	In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Access > API Keys**.  
2.	Click **Generate API Key**.  
**Important:** Make a note of the API key and token pair. Authentication tokens are non-recoverable. If you lose or forget this token, you will need to re-register the API key to generate a new authentication token.
 - An example of an API key is `a-organization_id-a84ps90Ajs`  
 - An example of a token is `MP$08VKz!8rXwnR-Q*`  
3.	Add a comment to identify the API key in the dashboard, for example: Key to connect my application.
4.	Click **Finish**.



## Bluemix binding connection
You can bind applications to your {{site.data.keyword.iot_short_notm}} organization from {{site.data.keyword.Bluemix_notm}}. By binding the application, it can only communicate with service instances in the same space or organization. You can find all the required data for the application to communicate with the service instance in the VCAP_SERVICES environment variable. If your application is bound to multiple services, the VCAP_SERVICES variable includes the connection information for each service instance.  

However, you can use service instances from other spaces or orgs in the same way that an external app does. Instead of creating a binding, use the credentials to directly configure your app instance. For more information, see [Requesting a new service instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance) in the {{site.data.keyword.Bluemix_notm}} documentation.
