---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-10"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# HTTP REST API for applications
{: #api}

Use the {{site.data.keyword.iot_full}} HTTP REST API to build and customize applications that interact with your organization on {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Capabilities
{: #capabilities}

The {{site.data.keyword.iot_short_notm}} HTTP REST API supports the following capabilities and functions for applications:

- Organization information retrieval
- Bulk device operations (list, add, and remove)
- Device type operations (list, create, delete, view details, and update)
- Device operations (list, add, remove, view details, update, view location, and view management information)
- Device diagnostic operations (clear logs, retrieve logs, add log information, delete logs, get specific logs, clear error codes, get device error codes, and add error codes)
- Connection problem determination (list device connection log events)
- Last event cache (view the last event for a specific device)
- Device management request operations (list device management requests, initiate requests, clear request status, get details of a request, list all request statuses by device, and get the request status for a specific device)
- Usage management operations (retrieve the total amount of data used)
- Device event publishing (beta)
- Service status querying (retrieve service statuses by organization)

## Accessing the HTTP REST API documentation
{: #api_link}

To access the {{site.data.keyword.iot_short_notm}} HTTP REST API documentation and obtain more information about how to build and customize your applications, see [APIs](../reference/api.html).

The only version of the {{site.data.keyword.iot_short_notm}} HTTP REST API that is supported is version 2. Ensure that your {{site.data.keyword.iot_short_notm}} solutions are using version 2.

# HTTP Messaging APIs for applications
{: #rest_messaging_api}

To access the {{site.data.keyword.iot_short_notm}} HTTP Messaging API documentation and find more information about publishing events and sending commands by using HTTP, see [{{site.data.keyword.iot_short_notm}} HTTP Messaging API ![External link icon](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}.

## Publishing events and commands
{: #event_command_publication}

In addition to using the MQTT messaging protocol, you can also configure your applications to publish events and commands to the {{site.data.keyword.iot_short_notm}} over HTTP by using one of the following HTTP REST API commands:

### Non-secure event POST request
<pre class="pre"><code class="hljs">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### Secure event POST request
<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

**Note:** Port 443, the default SSL port, can also be specified for secure HTTP API calls.

### Non-secure command POST request
<pre class="pre"><code class="hljs">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">eventId</var></code></pre>


### Secure command POST request
<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">eventId</var></code></pre>
{: codeblock}

If you are connecting a device or application to the Quickstart service, replace **orgId** with the string 'quickstart'.

**Notes:**
- While applications can reuse an HTTP connection to post events or commands to different devices, the authorization HTTP header cannot be changed.
- Port 443, the default SSL port, can also be specified for secure HTTP API calls.

### Authentication

All requests must include an authorization header. Basic authentication is the only method that is supported. Applications are authenticated by using API keys. When an application makes any request through the  {{site.data.keyword.iot_short_notm}} HTTP REST API, the following credentials are required:

```
username = API key (for example, a/orgId/a84ps90Ajs)
password = Authentication token
```

### Content-Type request headers

A `Content-Type` request header must be provided with the request. The following table shows how the supported types are mapped to the {{site.data.keyword.iot_short_notm}} internal formats.

|Content-Type header|Format in {{site.data.keyword.iot_short_notm}}|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

### Quality of service

Similar to the MQTT quality of service "at most once" delivery service level 0, HTTP REST messaging provides non-persistent message delivery but it validates that the request is correct and that it can be delivered to the server before it sends the HTTP response. A reply that contains a HTTP status code of 200 confirms that the message was delivered to the server. When you use either the "at most once" MQTT quality of service level or the HTTP equivalent to deliver event messages, the device or application must implement retry logic to guarantee delivery.


For more information about the MQTT protocol and the quality of service levels for {{site.data.keyword.iot_short_notm}}, see [MQTT messaging](../reference/mqtt/index.html).
