---

copyright:
  years: 2015, 2016, 2017

lastupdated: "2017-02-20"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# HTTP REST API for devices
{: #api}

**Important:** The {{site.data.keyword.iot_full}} HTTP REST API for devices feature is available only as part of a limited beta program. Future updates might include changes that are incompatible with the current version of this feature. Try it out and [let us know what you think](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html).

## Accessing the HTTP REST API documentation
{: #api_link}

To access the {{site.data.keyword.iot_short_notm}} HTTP REST API documentation and obtain more information about how to integrate devices into your organization, go to the following URL:  [https://docs.internetofthings.ibmcloud.com/swagger/v0002.html](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html)

The only version of the {{site.data.keyword.iot_short_notm}} HTTP REST API that is supported is version 2. Ensure that your {{site.data.keyword.iot_short_notm}} solutions are using version 2.

## Client connections
{: #client_connections}

For information about client security and how to connect clients to devices in {{site.data.keyword.iot_short_notm}}, see [Connecting applications, devices, and gateways to {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).

# HTTP REST messaging API for devices
{: #rest_messaging_api}

## Publishing events
{: #event_publication}

In addition to using the MQTT messaging protocol, you can also configure your devices to publish events to the {{site.data.keyword.iot_short_notm}} over HTTP by using HTTP REST API commands.

Use one of the following URLs to submit a ``POST`` request from a device that is connected to {{site.data.keyword.iot_short_notm}}:

### Non-secure POST request
<pre class="pre"><code class="hljs">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### Secure POST request

<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></class></pre>

**Note: **Port 443, the default SSL port, can also be specified for secure HTTP API calls.

If you are connecting a device or application to the Quickstart service, use one of the following URLs instead:

### Non-secure POST request to Quickstart
<pre class="pre"><code class="hljs">http://quickstart.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### Secure POST request to Quickstart
<pre class="pre"><code class="hljs">https://quickstart.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

**Important notes:**
- In the current HTTP REST API version, you can submit device events only by using HTTP messaging. Use the MQTT messaging protocol to submit requests for other device management and control features.
- HTTP connections can be reused to publish events for the same device only as the authorization HTTP header cannot be changed.
- Port 443, the default SSL port, can also be specified for secure HTTP API calls.

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

### Quality of service

Similar to the MQTT quality of service "at most once" delivery service level 0, HTTP REST messaging provides non-persistent message delivery but it validates that the request is correct and that it can be delivered to the server before it sends the HTTP response. A reply that contains a HTTP status code of 200 confirms that the message was delivered to the server. When you use either the "at most once" MQTT quality of service level or the HTTP equivalent to deliver event messages, the device or application must implement retry logic to guarantee delivery.

For more information about the MQTT protocol and the quality of service levels for {{site.data.keyword.iot_short_notm}}, see [MQTT messaging](../reference/mqtt/index.html).

## Last event cache
{: #last-event-cache}

By using the {{site.data.keyword.iot_short_notm}} Last Event Cache API, you can retrieve the last event that was sent by a device. This works whether the device is online or offline, which allows you to retrieve device status regardless of the device's physical location or use status. You can retrieve the last recorded value of an event ID for a specific device, or the last recorded value for each event ID that was reported by a specific device. Last event data of a device can be retrieved for any specific event that occurred up to 365 days ago.

To request the most recent value for a specific event ID, use the following API request, which returns the last recorded value for the “power” event ID.

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events/power
```

The response is returned in the following JSON format:

```
{
    "deviceId": "<device-id>",
    "eventId": "power",
    "format": "json",
    "payload": "eyJzdGF0ZSI6Im9uIn0=",
    "timestamp": "2016-03-14T14:12:06.527+0000",
    "typeId": "<device-type>"
}
```

**Note:** While the API response is in JSON format, event payloads can be written in any format. Payloads returned by Last Event Cache API are encoded in base64.

To request the most recent value for each event ID that was reported by a device, use the following API request:

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events
```

The response will include all event IDs that were sent by the device. In the following example, values are returned for the “power” and “temperature” events.

```
[
    {
        "deviceId": "<device-id>",
        "eventId": "power",
        "format": "json",
        "payload": "eyJzdGF0ZSI6Im9uIn0=",
        "timestamp": "2016-03-14T14:12:06.527+0000",
        "typeId": "<device-type>"
    },
    {
        "deviceId": "<device-id>",
        "eventId": "temperature",
        "format": "json",
        "payload": "eyJpbnRlcm5hbCI6MjIsICJleHRlcm5hbCI6MTZ9",
        "timestamp": "2016-03-14T14:17:44.891+0000",
        "typeId": "<device-type>"
    }
]
```
