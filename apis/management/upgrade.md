---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Accessing more API management features
{: #upgrade}

API management allows you to control call rates, OAuth, and view analytics. You can have greater management control over APIs by upgrading to the {{site.data.keyword.apiconnect_full}} service. The {{site.data.keyword.apiconnect_short}} service provides more choices of security policies and greater control over rate limits. In addition to this, you'll be able to configure a fully customizable Developer Portal so that you can socialize your APIs and engage with the developer community. Other benefits include:
* Lifecycle management
* Composite APIs
* Web services integration
* Protocol mediation
* API generation from schema
* Micro services development

Migrating to the {{site.data.keyword.apiconnect_short}} service is easy, and you do not have to recreate any of the APIs that you are managing with API management.

## Migrating APIs to {{site.data.keyword.apiconnect_short}}
{: #migrate_api}

If you decide to upgrade to {{site.data.keyword.apiconnect_full}}, you'll need to migrate your APIs from API management to the {{site.data.keyword.apiconnect_short}} service by completing the following steps for each of your APIs: 

1. Download the Swagger document for the API from API management.
    1. Open your app and select **API Management**.
	2. Select the **API Explorer** tab. A list of your APIs that are related to that project is displayed.
    2. Download the Swagger document for your API by selecting the icon beside the name of the API.
2. Create and prepare the {{site.data.keyword.apiconnect_short}} instance. 
    1. Create an instance of the {{site.data.keyword.apiconnect_short}} service from the {{site.data.keyword.Bluemix_notm}} catalog.
	2. Select your plan.
	3. Select **+Add** to create a catalog.
	4. Enter a Display name and name for your catalog, and select **Add**.
	5. Select the catalog that you created.
3. Import the Swagger document to your {{site.data.keyword.apiconnect_short}} instance by completing the following steps:
	1. From the {{site.data.keyword.apiconnect_short}} service dashboard, select **Navigate to... (>>)** > **Drafts** in the menu.
	2. Select the APIs tab.
	3. Select **+Add** > **Import API from a file or URL**.
	4. Find and select the Swagger file that you downloaded from API management. Select **Open**.
	5. Select **Import** to import your API into the {{site.data.keyword.apiconnect_short}} service.
4. Specify settings for your API.
    1. Select **Create product**.
	2. Select the product that you created to view its settings.
	3. Set the rate limit for the API.
	4. Set the tier for the API.
5. Add the endpoint for the API, if necessary.
    1. Select the API.
	2. Select the Assembly tab.
	3. Add the endpoint, if it is not already specified.
	
 After you migrate your APIs you will be able to access all of the API management features by opening the {{site.data.keyword.apiconnect_short}} service tile and also through the {{site.data.keyword.Bluemix_notm}} Dashboard. 

 
