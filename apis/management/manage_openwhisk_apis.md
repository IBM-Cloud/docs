---

copyright:
  years: 2017
lastupdated: "2017-04-12"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Create APIs from {{site.data.keyword.openwhisk_short}} actions
{: #manage_openwhisk_apis}

OpenWhisk actions can benefit from being managed by API management.

With API management, you can expose an {{site.data.keyword.openwhisk_short}} action as an API. After you define the API, you can apply security and rate limiting policies, view API usage and response logs, and define API sharing policies.  

To create an {{site.data.keyword.openwhisk_short}} API, complete the following steps:

1. In the {{site.data.keyword.openwhisk_short}} Dashboard, click the **APIs** tab. If you already have {{site.data.keyword.openwhisk_short}} APIs created, then a list of your {{site.data.keyword.openwhisk_short}} APIs is displayed. If you do not have any {{site.data.keyword.openwhisk_short}} APIs, then a Getting Started screen is displayed. 
2. Click **Create an {{site.data.keyword.openwhisk_short}} API**. The Create API for {{site.data.keyword.openwhisk_short}} window is displayed. 
3. Complete the fields in the API Info section, and then click **Create Operation**. The Create Operation window is displayed. You create operations to define the endpoint, https path, and method for your API.
4. In the "Create Operation" window, complete the required fields and select **Create**. The Operation is added to the Operations that invoke {{site.data.keyword.openwhisk_short}} actions table.
5. Complete the remaining information that you want to complete. You can also add or update the remaining information later when you manage your APIs.
6. Click **Save**. The API management overview page for your API opens and all the information that you just defined is displayed.
7. Continue managing your API with [Manage APIs](manage_apis.html).
