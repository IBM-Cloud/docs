---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# HTTP REST API for devices
{: #api}
Last updated: 09 September 2016
{: .last-updated}

**Important:** The {{site.data.keyword.iot_full}} HTTP REST API for devices feature is available only as part of a limited beta program. Future updates might include changes that are incompatible with the current version of this feature. Try it out and [let us know what you think](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html).

## Accessing the HTTP REST API
{: #api_link}

To access the {{site.data.keyword.iot_short_notm}} HTTP REST API and obtain more information about how to integrate devices into your organization, go to  https://docs.internetofthings.ibmcloud.com/swagger/v0002.html.

The only version of the {{site.data.keyword.iot_short_notm}} HTTP REST API that is supported is version 2. Ensure that your {{site.data.keyword.iot_short_notm}} solutions are using version 2.

# HTTP REST messaging API for devices
{: #rest_messaging_api}

## Publishing events
{: #event_publication}

In addition to using the MQTT messaging protocol, you can also configure your devices to publish events to the {{site.data.keyword.iot_short_notm}} over HTTP by using HTTP REST API commands.

Use one of the following URLs to submit a ``POST`` request from a device that is connected to {{site.data.keyword.iot_short_notm}}:

### Non-secure POST request
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### Secure POST request
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

If you are connecting a device or application to the Quickstart service, use one of the following URLs instead:

### Non-secure POST request to Quickstart
<pre class="pre">http://quickstart.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### Secure POST request to Quickstart
<pre class="pre">https://quickstart.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**Important notes:**
- In the current HTTP REST API version, you can submit device events only by using HTTP messaging. Use the MQTT messaging protocol to submit requests for other device management and control features.
- HTTP connections can be reused to publish events for the same device only as the authorization HTTP header cannot be changed.

### Authentication

All requests must include an authorization header. Basic authentication is the only method that is supported. When a device makes an HTTP request through the {{site.data.keyword.iot_short_notm}} HTTP REST API, the following credentials are required:

```
username = "use-token-auth"
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
