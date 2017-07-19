---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# MQTT connectivity for applications
{: #mqtt}

MQTT is the primary protocol that devices and applications use to communicate with the {{site.data.keyword.iot_full}}. Client libraries, information, and samples are provided to help you to connect and integrate your {{site.data.keyword.iot_short_notm}} applications.
{:shortdesc}

## Client connections
{: #client_connections}

For information about client security and how to connect MQTT clients to applications in  {{site.data.keyword.iot_short_notm}}, see [Connecting applications, devices, and gateways to {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).

## MQTT authentication
{: #mqtt_authentication}

{{site.data.keyword.iot_short_notm}} applications require an API key to connect to an organization. When an API key is registered, an authentication token is generated, which must be used with that API key.

The following example shows a typical API key:

<pre class="pre">a-<var class="keyword varname">orgId</var>-a84ps90Ajs</pre>
{: codeblock}


The following example shows a typical authentication token:

```
MP$08VKz!8rXwnR-Q*
```

When you make an MQTT connection by using an API key, ensure that the following guidelines are applied:

- The MQTT client ID is in the format: a:*orgId*:*appId*
- The MQTT user name is the API key (for example, a-*orgId*-a84ps90Ajs)
- The MQTT password is the authentication token (for example, MP$08VKz!8rXwnR-Q*)


## Publishing device events
{: #publishing_device_events}

An application can publish events as if they came from any registered device, for example:

-  Publish to topic iot-2/type/*device_type*/id/*device_id*/evt/*event_id*/fmt/*format_string*

To send existing data from a device into {{site.data.keyword.iot_short_notm}}, you can create an application to process the data and publish it into {{site.data.keyword.iot_short_notm}}.

**Important:** The message payload is limited to a maximum of 131072 bytes.  Messages that exceed the limit are rejected.

### Retained messages
{{site.data.keyword.iot_short_notm}} organizations are not authorized to publish retained MQTT messages. If an application, gateway, or device sends a retained message, the {{site.data.keyword.iot_short_notm}} service overrides the retained message flag when it is set to true and processes the message as if the flag is set to false.

## Publishing device commands
{: #publishing_device_commands}

