---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-07"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# HTTP REST APIs for gateway devices
{: #api_link}


To access the {{site.data.keyword.iot_short_notm}} HTTP REST API documentation and find more information about creating, updating, deleting, and listing devices, see [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html).

The only version of the {{site.data.keyword.iot_short_notm}} HTTP REST API that is supported is version 2. Ensure that your {{site.data.keyword.iot_short_notm}} solutions are using version 2.

## Client connections
{: #client_connections}

For information about client security and how to connect clients to gateway devices in {{site.data.keyword.iot_short_notm}}, see [Connecting applications, devices, and gateways to {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).


### Authentication

All requests must include an authorization header. Basic authentication is the only method that is supported. When a device makes an HTTP request by using the {{site.data.keyword.iot_short_notm}} HTTP REST API, the following credentials are required:

|Credential|Required input|
|:---|:---|
|User name| `g/{orgId}/{gwType}/{gwDevId}`
|Password| The authentication token that was either automatically generated or manually specified when you registered the gateway device.

where:

<dl>
<dt>orgId</dt>  
<dd>The organization name, which must match the name that is specified in the host header.</dd>

<p></p>
<dt>gwType</dt>  
<dd>The type of gateway. </dd>
<p></p>
<dt>gwDevId</dt>  
<dd>The device identifier of gateway. </dd>
</dl>


### Content-Type request headers

A `Content-Type` request header must be provided with the request. The following table shows how the supported types are mapped to the {{site.data.keyword.iot_short_notm}} internal formats:

|Content-Type header|Format in {{site.data.keyword.iot_short_notm}}|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

## Last event cache
{: #last-event-cache}

By using the {{site.data.keyword.iot_short_notm}} Last Event Cache API, you can retrieve the last event that was sent by a device. This API works whether the device is online or offline, which allows you to retrieve device status regardless of the device's physical location or use status. You can retrieve the last recorded value of an event ID for a specific device, or you can retrieve the last recorded value for each event ID that was reported by a specific device. Last event data of a device can be retrieved for any specific event that occurred up to 365 days ago.

To request the most recent value for a specific event ID, use the following API request, which returns the last recorded value for the “power” event ID:

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

The response includes all event IDs that were sent by the device. In the following example, values are returned for the “power” and “temperature” events.

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
