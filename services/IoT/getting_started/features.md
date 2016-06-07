---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Feature overview
{: #features}

## Device registry
{: #device-registry}

Manage your inventory, configure security, and store metadata for millions of unique devices.  Define
device types to represent individual device models and apply default metadata to all devices of that type.


## Connectivity
{: #connectivity}

Securely connect your devices, gateways and applications directly to the {{site.data.keyword.iot_full}} via MQTT.  For more information about the advantages of using
the MQTT protocol, see the [MQTT](../reference/mqtt/index.html) reference information.
Model the data from your device as events and control the flow of events into your applications.


## Gateway support
{: #gateway-support}

In many cases where a direct connection can not be made between the service and a device, the {{site.data.keyword.iot_short_notm}} allows
gateway devices to connect that can provide indirect connectivity for multiple devices.


## Device management
{: #device-management}

Optionally, allow the {{site.data.keyword.iot_short_notm}} to manage the lifecycle of your devices by implementing support for
the {{site.data.keyword.iot_short_notm}}'s device management protocol in your devices.  The means by which the device
connects to the service does not affect the device management protocol, which functions the
same for directly connected, indirectly connected, and gateway devices.


## External service integration
{: #external-service-int}

The {{site.data.keyword.iot_short_notm}} supports integration with external services to bring data and operations supported by
other online services into the platform, allowing your application and device developers to
seamlessly interact with those services without ever leaving the comfort of the {{site.data.keyword.iot_short_notm}} APIs.

**Important:** This feature is currently available as part of a limited beta. Future updates  
may include changes incompatible with the current version of this feature. Try it out and [let us know what you think](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html).


## Historican
{: #historical-event-storage}

Configure the {{site.data.keyword.iot_short_notm}} to store a record of the events your devices generate.

**Warning:** **Message format restrictions apply to the Historian**

The Historian feature supports JSON messages that meet the following criteria:

- The message is a valid JSON object (not an array) with only two top level elements: ``d`` and ``ts``
- The message is UTF-8 encoded
- The message is less than 4KB

**Data**

The **d** element is where you include all data for the event (or command) that is transmitted in the message.

- This element is required for your message to meet the {{site.data.keyword.iot_short_notm}} message specification.
- This must always be a JSON object (not an array)
- In the case where you wish to send no data the **d** element should still be present, but contain an empty object.

**Time stamp**

The **ts** element is optional, and you can use this to associate an event or command with a valid ISO8601 time stamp.

**Example**

```
  {
    "d": {
      "host": "IBM700-R9E683D",
      "mem": 54.9,
      "network": {
        "up": 1.22,
        "down": 0.55
      },
      "cpu": 1.3,
    },
    "ts": "2014-12-30T14:47:36+00:00"
  }
  ```

## Last event cache
{: #last-event-cache}

Using the API you can retrieve the last recorded value of an event ID for a specific device, or the last recorded value for each event-id reported by a specific device. The last event cache only includes data from event IDs that were sent in the previous 30 days.

To request the most recent value for a specific event-id, use the following API request, which returns the last recorded value for the “power” event-id.

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

**Note:** While the API response is JSON, event payloads can be written in any format. Payloads returned by this API will be encoded in base64.

Alternatively, to request the most recent value for each event-id reported by this device, use the following API request.

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events
```

The response will include all event-id’s sent by the device. In this instance, it returns values for the “power” and “temperature” events.

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
