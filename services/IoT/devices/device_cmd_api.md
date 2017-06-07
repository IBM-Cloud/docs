--

copyright:
 years: 2015, 2017
lastupdated: "2017-05-23"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# HTTP Messaging APIs for devices (Beta)
{: #api}

**Important:** The {{site.data.keyword.iot_full}} HTTP Messaging API for devices feature is available only as part of a limited beta program. Future updates might include changes that are incompatible with the current version of this feature. Try it out and [let us know what you think ![External link icon](../../../icons/launch-glyph.svg)](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html){: new_window}.


## Accessing the HTTP Messaging API documentation for devices
{: #rest_messaging_api}

To access the {{site.data.keyword.iot_short_notm}} HTTP Messaging API documentation, see [{{site.data.keyword.iot_short_notm}} HTTP Messaging API ![External link icon](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}.


## Client connections
{: #client_connections}

For information about client security and how to connect clients to devices in {{site.data.keyword.iot_short_notm}}, see [Connecting applications, devices, and gateways to {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).

## Publishing events
{: #event_publication}

In addition to using the MQTT messaging protocol, you can also configure your devices to publish events to the {{site.data.keyword.iot_short_notm}} over HTTP by using HTTP REST API commands.

Use one of the following URLs to submit a ``POST`` request from a device that is connected to {{site.data.keyword.iot_short_notm}}:

### Non-secure POST request
<pre class="pre"><code class="hljs">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### Secure POST request

<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

**Note:** Port 443, the default SSL port, can also be specified for secure HTTP API calls.

### Authentication

All requests must include an authorization header. Basic authentication is the only method that is supported. When a device makes an HTTP request through the {{site.data.keyword.iot_short_notm}} HTTP REST API, the following credentials are required:

|Credential|Required input|
|:---|:---|
|User name|`use-token-auth`
|Password| The authentication token that was either automatically generated or manually specified when you registered the device.


### Content-Type request headers

A `Content-Type` request header must be provided with the request. The following table shows how the supported types are mapped to the {{site.data.keyword.iot_short_notm}} internal formats.

|Content-Type header|Format in {{site.data.keyword.iot_short_notm}}|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"


## Receiving commands
{: #receive_commands}

In addition to using the MQTT messaging protocol, you can also configure your devices to receive commands from {{site.data.keyword.iot_short_notm}} over HTTP by using HTTP Messaging API commands. A device can receive commands that are directed at itself.

Use one of the following URLs to submit a ``POST`` request from a device that is connected to {{site.data.keyword.iot_short_notm}}:

### Non-secure POST request
<pre class="pre"><code class="hljs">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">command</var>/request</code></pre>

### Secure POST request

<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">command</var>/request</code></pre>

**Note:** Port 443, the default SSL port, can also be specified for secure HTTP API calls.

To receive a command from {{site.data.keyword.iot_short_notm}}, use the following API:

<pre class="pre"><code class="hljs">/device/types/{deviceType}/devices/{deviceId}/commands/{command}/request</var></code></pre>

You can optionally include the parameter *waitTimeSecs* in the body of the HTTP request to specify an integer that represents the maximum number of seconds to wait for a command:
<pre class="pre"><code class="hljs">{"waitTimeSecs": 5} </code></pre>


**Important notes:**
- The value of *waitTimeSecs* must be an integer in the range 0 - 3600 seconds. The default value is 0.
- To receive any command, use the "any" wildcard character (+) for the {command} component. If the wildcard character is used, the command identifier is contained in the response header field *X-commandId*.
- If the HTTP response status code is 200, the command data is contained in the body of the response. Review the response header field *Content-Type* to find the content type.
- If the HTTP response status code is 204, no command data is available.


For information about developing devices, see [Developing devices on {{site.data.keyword.iot_short_notm}}](../devices/device_dev_index.html).
