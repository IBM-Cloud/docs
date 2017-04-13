---

copyright:
  years: 2017
lastupdated: "2017-04-11"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Manage APIs
{: #manage_apis}

After you integrate your API so it is managed and monitored by the API management system, you can view and modify the API settings. If you have not integrated your API, you must integrate one by completing the procedure in [Creating APIs from {{site.data.keyword.openwhisk_short}} actions](manage_openwhisk_apis.html). 

To manage the settings for your API, complete the following steps:

If you created a new API, and it is already opened in the interface, you can skip the first three steps.

1. Select the API that you want to manage by selecting an action on the {{site.data.keyword.openwhisk_short}} service Dashboard, if the information for your API is not already displayed.
2. Select the **APIs** tab, if necessary.
3. Select the API that you want to manage, if necessary. When a connection is established, the following selections are available for you to view and update:
    * Summary
    * Definition
    * Sharing
    * API Explorer
4. Select the Expose Managed API slider to activate it and expose your API. Note: Some of the settings cannot be set when the API is not exposed.  

## Summary of settings for APIs
{: #overview_api}

The Summary tab is selected by default when you select an API, and is split into two sections:
* Properties - In the Properties section you can view the following information:
    * Basic information about your API
	* Security policies
	* Rate limit information
    * Sharing details
* Analytics and Logging section - In the Analytics and Logging section, you can view the following statistics:
	* Number of responses and average response time during the last specified time interval
    * Number of API calls per minute in graph format
    * Last 100 responses in the Response Log table
	
The *Responses* graph shows a quick representation of how many responses your API received, and the breakdown of the status of the responses. This can help you determine if you are receiving a majority of error responses. A majority of error responses can indicate that you have more traffic than you allowed in your rate settings. You can see a numerical breakdown of the responses by response code by hovering over the information icon. The following response codes are common:
* 200  OK
* 201  Created
* 302  Found
* 304  Not Modified
* 400  Bad Request
* 401  Unauthorized
* 403  Forbidden
* 500  Internal Server Error
* 503  Service Unavailable

The Response Log table contains individual details of the last 100 responses. You can sort the information according to the entries in a column by selecting the column heading. You can search for specific entries in the Response Log table by using the *Search responses* bar. More information is available for an event by selecting it, or by selecting **View Details** in the list of options menu (three vertical dots) that is beside the entry.


## Editing API settings
{: #settings_api}

In the **Definition** tab, you can update basic information about your API. This information includes the documentation, name, and base URL. Use the Security and Rate Limiting section to specify a call and interval limit to ensure that only a certain amount of calls are made per second, minute, or hour. You can also require authentication to create API calls to prevent unwanted use of your data or to gather statistics about the API.

To change the settings for an API, complete the following steps:

1. In the API management dashboard, click the **Definition** tab.
2. You can name or update the name of your API and import an API definition in the API Info section.
3. In the Security and Rate Limiting section, you can update the following policies:
    * Require API key - Specifies whether the API call can only be processed when the correct API key is provided. The default setting does not require an additional key.
    * Security method - When the API key option is selected, specifies whether processing the API only requires the API key, or requires both the API key and the API secret.
    * Location of the API key and secret - Depending on your setting for the method, specifies how your API security information is included in the call. The Invocation names specify how the security information is identified.
    * Limit API call rate - Sets the number of API calls that are allowed during a specified time interval, with the option of setting it for each key. Note that a burst-type of rate-limiting method is used. If the rate of the API calls exceeds the average rate of calls that was specified, there could be a period of denied calls up to the time limit that you specified in the rate.  
    * OAuth provider - Ensures that users with the correct security parameters can access your APIs by enforcing OAuth through social login credentials of providers like Google, Facebook, IBM, and GitHub.
4. Enable CORS - Cross-origin requests (CORS) enables some limited requests from a different domain.
5. Click **Save**.

## Sharing APIs
{: #share_api}

You can share APIs with other users inside or outside your {{site.data.keyword.Bluemix_notm}} organization.

When you share your APIs with others, either inside or outside of your {{site.data.keyword.Bluemix_notm}} organization, you can create keys for your APIs. Each managed API supports 5 keys that can be created and assigned that API. By sending a unique key to an individual or company, you can track some statistics about how that API is used. For example, you can track the number or calls to your API by that person or company.

You can also limit the number of calls at the key ledisable a key or limit the calls from a key. This can be helpful during testing, workload balancing, monetizing, or for addressing some security situations.  

1. In the API management dashboard, click the **Sharing** tab.
2. Within the "Sharing within {{site.data.keyword.Bluemix_notm}} Organization" area, select **Share API with all users in my Bluemix organization** if you want your API to be available to others with access to your {{site.data.keyword.Bluemix_notm}} organization. This must be selected to generate a key.
3. Click **Create API Key** to create a unique key for your API. The Create API Key dialog box is displayed. The API key is generated automatically.
4. Use the API key to determine which user is accessing the API by sending a user a unique key. The gateway can determine which key (and customer) is generating the call.
5. Click the the **Menu** icon (three vertical dots) beside the key to Edit or Delete that API key.

In the Sharing Outside of {{site.data.keyword.Bluemix_notm}} Organization section, you can share your API with users who do not have a {{site.data.keyword.Bluemix_notm}} account. This method of sharing provides a direct link to view the information about the API in the API Explorer. The API contains a button to run the API in the API Explorer view. To request a link for your API, complete the following steps:

1. Within the "Sharing Outside of {{site.data.keyword.Bluemix_notm}} Organization" section. Click **Create API Key**. The Create API Key dialog box is displayed.
     Notice that the user has a secret that you cannot control.
2. Provide a unique name for the API key.
3. Select **Create key**. 
4. Send the API Portal Link to the customer without a {{site.data.keyword.Bluemix_notm}} account. The API key and secret (if it is used) is included in the link, so you can still determine which key generatated the link.
  
The API documentation link opens the API in the **API Explorer** tab.

## Viewing and testing with API Explorer
{: #explore_api}

Select the API Explorer tab to view generated html from your Swagger doc. 

The API Explorer shows all of the API actions and documentation that apply to the API. You can view the operations and actions, their descriptions, and test the API from the UI. You can also download the Swagger doc to reuse its content.

To test the API, complete the following steps:
1. *Examples* is selected by default. This shows an example of the code for the selected API.
2. Change the example format, if necessary, by selecting a language from the menu beside the specified language. 
3. Select **Try it**.
4. Select **Call operation**. 

The response to the request is displayed.   
