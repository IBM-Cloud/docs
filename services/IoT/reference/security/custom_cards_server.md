---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-29"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Securing your custom cards server
{: #securing_custom_cards}

Custom cards servers are standard web servers that host the custom cards javascript code. To ensure the integrity of your {{site.data.keyword.iot_short_notm}} environment you should secure your custom cards server by taking steps to secure the card source as discussed in this topic.
{:shortdesc}

**Important:** Custom cards are currently offered as an experimental feature and the custom cards extension is enabled per browser session. Custom cards connection configuration and card packages are not shared globally across your {{site.data.keyword.iot_short_notm}} organization.

## {{site.data.keyword.Bluemix_notm}} role requirement
{: #roles_requirements}

You must have {{site.data.keyword.iot_short_notm}} administrator rights to create a custom cards server connection.

## Custom cards server security considerations
{: #server_requirements}

The following requirements are set by {{site.data.keyword.iot_short_notm}}:
- The directory that serves the custom card content on the server must not require credentials to access.  
No authentication is provided to the custom card server when connecting to access and load custom cards.
- The server must use the HTTP Secure (HTTPS) protocol.
- The server must support Cross-origin resource sharing (CORS) connections.  

To protect the custom cards code and the card server itself, the card server should be located and secured using defense in depth. This includes firewall protection to restrict access to the custom card server.

Custom card processing is always between a user’s browser and the custom cards server. The {{site.data.keyword.iot_short_notm}} backend is never involved in processing or adjusting the custom cards information and code.

There are no restrictions placed on the JavaScript code that you choose to deploy in your cards on your custom cards server. Javascript code in custom cards has access to all information held in the browser, just as any other cards running in the dashboard.  Make sure that the correct custom card server is supplying the code to the browser to display and process the custom cards.

The cards execute their code in your {{site.data.keyword.iot_short_notm}} browser session exactly as written. Furthermore, the custom cards server connection is created with no credentials supplied to the custom card server. A users's browser can connect to any configured custom cards server.

It is important that you only configure known and secured custom cards servers to supply custom cards to your users’ dashboards.   
