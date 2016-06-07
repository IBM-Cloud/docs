---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# HTTP API for devices
{: #api}

**Important:** The {{site.data.keyword.iot_full}} HTTP API for devices feature is currently available as part of a limited beta program only. Future updates might include changes that are  incompatible with the current version of this feature. Try it out and [let us know what you think](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html).

## Publishing events
{: #event_publication}

In addition to using the MQTT messaging protocol, you can also configure your devices to submit events to the {{site.data.keyword.iot_short_notm}} over HTTP by using the HTTP API for devices.

The following URL outlines how devices can submit a ``POST`` request:

```
 https://${orgid}.internetofthings.ibmcloud.com/api/v0002/device/types/${typeId}/devices/${deviceId}/events/${eventId}
```

For more information, see the relevant API detail in the [{{site.data.keyword.iot_short_notm}} API documentation](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/).

The request body (event payload) can contain any content, however, the MQTT message payload guidelines must be followed.

**Note:** To connect a device or application to Quickstart, use the following URL instead:

 ```
 http://quickstart.internetofthings.ibmcloud.com/api/v0002/device/types/${typeId}/devices/${deviceId}/events/${eventId}
 ```



**Important:** In the current HTTP API version, you can submit only device events through HTTP messaging. Use the MQTT messaging protocol for more device management and control features.

### Authentication

Requests should include an authorization header. Basic authentication is the only method that is supported. Applications get authenticated by API keys. When an application makes any request to the {{site.data.keyword.iot_short_notm}} API, the following credentials are required:

- username = "use-token-auth"
- password = Authentication token

### Content-Type request headers

A `Content-Type` request header must be provided with the request. The following table shows how the supported types are mapped to the  {{site.data.keyword.iot_short_notm}} internal formats.

  Content-Type header        | Format in {{site.data.keyword.iot_short_notm}}
  -------------------------- | ---------------------
  text/plain                 | text
  application/json           | JSON
  application/xml            | XML
  application/octet-stream   | bin

### Quality of service

The HTTP(S) protocol provides "at most once" best effort delivery, analogous to the QoS0 quality of service that is provided by the MQTT protocol. When you use QoS0 or the HTTP(S) equivalent to deliver event messages, the device or application must implement retry logic to guarantee delivery.


For more information on the MQTT protocol and quality of service levels, see [MQTT for the {{site.data.keyword.iot_short_notm}}](../reference/mqtt/index.html) documentation.
