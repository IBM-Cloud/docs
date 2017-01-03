---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-17"

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

To port existing data from a device into  {{site.data.keyword.iot_short_notm}}, you can create an application to process the data and publish it into {{site.data.keyword.iot_short_notm}}.

**Important:** The message payload is limited to a maximum of 131072 bytes.  Messages that exceed the limit are rejected.

### Retained messages
{{site.data.keyword.iot_short_notm}} organizations are not authorized to publish retained MQTT messages. If an application, gateway, or device sends a retained message, the {{site.data.keyword.iot_short_notm}} service overrides the retained message flag when it is set to true and processes the message as if the retained message flag is set to false.

## Publishing device commands
{: #publishing_device_commands}

An application can publish a command to any registered device, for example:

-  Publish to topic iot-2/type/*device_type*/id/*device_id*/cmd/*command_id*/fmt/*format_string*

## Subscribing to device events
{: #subscribe_device_events}

An application can subscribe to events from one or more devices, for example:

-  Subscribe to topic iot-2/type/*device_type*/id/*device_id*/evt/*event_id*/fmt/*format_string*

**Note:**  To subscribe to more than one type of event or to events from more than a single device, use the MQTT "any" wildcard character (+) for any of the following components:

- device_type
- device_id
- event_id
- format_string

## Subscribing to device commands
{: #subscribe_device_commands}

An application can subscribe to commands that are being sent to one or more devices, for example:

-  Subscribe to topic iot-2/type/*device_type*/id/*device_id*/cmd/*command_id*/fmt/*format_string*

**Note:** To subscribe to more than one type of event or to events from more than a single device, use the MQTT "any" wildcard character (+) for any of the following components:

-  device_type
-  device_id
-  cmd_id
-  format_string

## Subscribing to device status messages
{: #subscribe_device_status}

An application can subscribe to monitor the status of one or more devices, for example:

-  Subscribe to topic iot-2/type/*device_type*/id/*device_id*/mon

**Note:** To subscribe to updates from more than one device, use the MQTT "any" wildcard character (+) for any of the following components:

- device_type
- device_id

## Subscribing to application status messages
{: #subscribe_app_status}

An application can subscribe to monitor status of one or more applications, for example:

- Subscribe to topic iot-2/app/*appId*/mon

**Note:** To subscribe to updates for all applications, use the MQTT "any" wildcard character (+) for the *appId* component.


## Quickstart restrictions
{: #quickstart_restrictions}
If you are planning to create application code for use with the Quickstart service, the following features are not supported in Quickstart:

- Publishing commands
- Subscribing to commands
- Using the MQTT "any" wildcard character (+) in **deviceType** or **appId** components
- MQTT connection over Transport Layer Security (TLS)
- Scalable applications

## Scalable applications
{: #scalable_apps}

By adjusting the way that your applications connect, you can make your {{site.data.keyword.iot_short_notm}} applications more scalable by balancing the load handling of event messages across multiple instances of an application.

The number of clients that are required for optimum load balancing and scalability varies by deployment. To identify the optimum number of clients, you need to stress test your system.

To enable load balancing, ensure that the application subscription is non-durable and that the client ID in the subscription matches the following format:

<pre class="pre">A:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
{: codeblock}

Where:
-  The character **A** indicates that the client is a scalable application.
-  *orgId* is the unique six-character organization ID that was generated when you registered the service.
-  *appId* is a user-defined unique string identifier for the client. The string can contain only alphanumeric characters (a-z, A-Z, 0-9) and the dash (-), underscore (_), and dot (.) special characters.

**Important:**
- Only non-durable subscriptions are supported for scalable applications.
- The client ID must start with an uppercase **A** character to be correctly designated as a scalable application by {{site.data.keyword.iot_short_notm}}.
- Other clients that are part of the scalable application must use the same client ID.


### Shared subscriptions

The {{site.data.keyword.iot_short_notm}} service extends the MQTT V3.1.1 messaging protocol specification to support shared subscriptions. Shared subscriptions provide load balancing capabilities for applications. A shared subscription might be needed if a back-end enterprise application cannot process the volume of messages that are being published to a specific topic space. For example, when many devices publish messages that are being processed by a single application, it might be necessary to use the load balancing capability of a shared subscription. {{site.data.keyword.iot_short_notm}} shared subscription support is limited to non-durable subscriptions only.

**Example**

The following scenario is one example of how a scalable application works in {{site.data.keyword.iot_short_notm}}:

- Client one connects as **A:abc123:myApplication** and subscribes to all device events, which means that client one receives 100% of the device events that are published.
- Client two connects as **A:abc123:myApplication** and also subscribes to all device events, which means that client one and client two share all of the events that are published. The processing load is shared between client one and client two.
- Client three connects as **A:abc123:myApplication** and also subscribes to all device events, which means that client one, client two, and client three share the processing load for events.
- Client two and client three then unsubscribe from all device events, which means that only client one receives all device events that are published. While client two and client three are still connected to the service, client one receives 100% of the device events that are published.
- When two or more applications share a subscription, messages might not arrive in the order in which they were sent. For example, message B might arrive at client one before message A arrives at client two, even though message A was sent first.
