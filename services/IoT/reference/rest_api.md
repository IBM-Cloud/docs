---

copyright:

years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# APIs
{: #overview}

Several APIs are available for developing code for devices, gateways, and applications that connect to {{site.data.keyword.iot_full}}.

The HTTP APIs are protected with HTTP basic authentication. When you generate an API key by using the dashboard, you are presented with a key and an authentication token. For more information, see


## HTTP REST APIs

After registering for your own organization you will be provided with a 6 character organization ID. This ID is required in the hostname for any API calls, the base URL for your organization can be accessed at the following address:

https://<**orgId**>.internetofthings.ibmcloud.com/api/v0002/

To authenticate requests to the application API, set the username to the API key and the password to the authentication token.

For Messaging APIs, use the following address: https://<**orgId**>.messaging.internetofthings.ibmcloud.com:/api/v0002


## API links

Use the links in the following table to find out more about the APIs that are provided by {{site.data.keyword.iot_short_notm}}.

### General HTTP APIs

API                     | Use to ...       
------------- | -------------
[Organization Administration ![External link icon](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html){: new_window} | Configure an organization (including creating and deleting devices), check usage, service status and diagnose device connection problems.
[Security ![External link icon](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/security.html){: new_window} | Manage user invitations and authentication, and authorization of users, API keys and devices.
[Information Management ![External link icon](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/info-mgmt.html){: new_window} |  Access device event data, as well as get and update device location and obtain weather information for that location. **Note:** Weather information is dependant on integration of The Weather Company.
[The Weather Company ![External link icon](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/info-mgmt.html#!/Device_Location_Weather){: new_window} | Integrate data from The Weather Company with your existing devices.
[Analytics ![External link icon](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/analytics.html){: new_window} | Create rules, alerts and actions for data coming into {{site.data.keyword.iot_short_notm}} from devices.
[Device Management ![External link icon](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/device-mgmt.html){: new_window} | Interact with managed devices by using the device management protocol.
[Messaging ![External link icon](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}   | Publish events and send commands by using HTTP. **Note:** For Messaging APIs, use the address https://<**orgId**>.messaging.internetofthings.ibmcloud.com:/api/v0002



### Extension HTTP APIs

API                     | Use to ...       
------------- | -------------
[AT&T Extension ![External link icon](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-atnt.html){: new_window} | Administer AT&T devices.
[Jasper Extension  ![External link icon](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-jasper.html){: new_window} | Administer Jasper devices.
[Orange Extension  ![External link icon](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-orange.html){: new_window} | View SIM card data from devices that are connected to your {{site.data.keyword.iot_short_notm}} organization and have an Orange SIM card installed.

### Beta HTTP APIs

API                     | Use to ...       
------------- | -------------
[Gateway Security  ![External link icon](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html){: new_window}   | Check and assign roles to gateway devices.
[ Device Security  ![External link icon](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-devices-beta.html){: new_window} | Check and assign roles to devices.
[Interface Mapping  ![External link icon](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html){: new_window}   |   Map and access device data using interfaces.
