---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# MQTT connectivity for applications
{: #mqtt}


## Client connections
{: #client_connections}
Every registered organization has a unique endpoint value, which must be used when connecting MQTT clients for applications in that organization.


```
org_id.messaging.internetofthings.ibmcloud.com
```

### Unencrypted client connections

For unencrypted client connections, connect on port **1883**.

**Important:** Applications in the {{site.data.keyword.iot_full}} submit information as plain text, including the API key and authentication token. To secure the transmission, always use an encrypted connection.

### Encrypted client connections

For encrypted client connections, connect on port **8883**, or for WebSockets, connect on port **443**.

Many client libraries require that you provide the server's public certificate in PEM format. To view the entire certificate chain for
\*.messaging.internetofthings.ibmcloud.com, go to [messaging.pem](https://github.com/ibm-messaging/iot-python/blob/master/src/ibmiotf/messaging.pem).

**Tip:** Some SSL client libraries do not support domains that include a wildcard. If you cannot successfully change libraries, disable certificate checking.

**Prerequisites:** {{site.data.keyword.iot_short_notm}} requires Transport Layer Security (TLS) V1.2 and the following cipher suites:
- ECDHE-RSA-AES256-GCM-SHA384
- AES256-GCM-SHA384
- ECDHE-RSA-AES128-GCM-SHA256
- AES128-GCM-SHA256 *(as of 1 June 2015)*


## MQTT client identifier
{: #mqtt_client_identifier}
For applications to successfully authenticate, define each MQTT client ID in the following format:

```
a:org_id:app_id
```

Where:
- The lowercase character **a** indicates that the client is an application.
- org_id is the unique six character organization ID that was generated when you registered the service alphanumeric string that was assigned when you first registered the service.
- app_id is a user-defined unique string identifier for the client with a maximum length of 36 characters. The string can contain only alpha-numeric characters (a-z, A-Z, 0-9) and the following special characters: dash (-); underscore (\_); dot (.).


**Notes:**
- When connecting to the Quickstart service, authentication is not required.
- You do not need to register an application before connecting.
- **Important:** Only one MQTT client can connect using any given client ID. Simultaneous connections that use the same client ID are not permitted. If you attempt to connect a client in your organization by using an app_id that is already connected, the first connection is disconnected.

## MQTT authentication
{: #mqtt_authentication}

{{site.data.keyword.iot_short_notm}} applications require an API key to connect into an organization. When an API key is registered, a token is generated, which must be used with that API key.

The following is an example of an API key:
```
a-org_id-a84ps90Ajs
```

The following is an example of an API token:

```
MP$08VKz!8rXwnR-Q*
```

When you make an MQTT connection by using an API key, ensure that the following points apply:

- The MQTT client ID is in the format: a:org_id:app_id
- The MQTT user name is the API key: a-org_id-a84ps90Ajs
- The MQTT password is the authentication token: MP$08VKz!8rXwnR-Q*


## Publishing device events
{: #publishing_device_events}

An application can publish events as if they came from any registered device.

-  Publish to topic iot-2/type/**device\_type**/id/**device\_id**/evt/**event\_id**/fmt/**format\_string**

If you would like to migrate existing data from a device into  {{site.data.keyword.iot_short_notm}}, you can create an application to process the bespoke data and publish it into {{site.data.keyword.iot_short_notm}}.

**Important:** The message payload is limited to a maximum of 131072 bytes.  Messages that exceed the limit are rejected.

## Publishing device commands
{: #publishing_device_commands}

An application can publish a command to any registered device.

-  Publish to topic iot-2/type/**device\_type**/id/**device\_id**/cmd/**command\_id**/fmt/**format\_string**

## Subscribing to device events
{: #subscribe_device_events}

An application can subscribe to events from one or more devices.

-  Subscribe to topic iot-2/type/**device\_type**/id/**device\_id**/evt/**event\_id**/fmt/**format\_string**

**Note:**  To subscribe to more than one type of event, or events
from more than a single device, use the MQTT "any" wildcard character (+) for any of the following components:
- device_type
- device_id
- event_id
- format_string


## Subscribing to device commands
{: #subscribe_device_commands}

An application can subscribe to commands that are being sent to one or more devices.

-  Subscribe to topic iot-2/type/**device\_type**/id/**device\_id**/cmd/**command\_id**/fmt/**format\_string**

**Note:** To subscribe to more than one type of event, or events from more than a single device, use the MQTT "any" wildcard character (+) for any of the following components:
- device_type
- device_id
- cmd_id
- format_string



## Subscribing to device status messages
{: #subscribe_device_status}

An application can subscribe to monitor the status of one or more devices.

-  Subscribe to topic iot-2/type/**device\_type**/id/**device\_id**/mon

**Note:** To subscribe to updates from more than one device, use the MQTT "any" wildcard character (+) for any of the following components:

- device_type
- device_id

## Subscribing to application status messages
{: #subscribe_app_status}

An application can subscribe to monitor status of one or more applications.

- Subscribe to topic iot-2/app/app_id/mon

**Note:** To subscribe to updates for all applications, use the MQTT "any" wildcard character (+) for the app_id component.


## Quickstart restrictions
{: #quickstart_restrictions}
If you are planning to create application code for use with the Quickstart service, the following features are not supported in Quickstart:

- Publishing commands
- Subscribing to commands
- Using the MQTT "any" wildcard character (+) in **device\_type** or app_id components
- MQTT connection over SSL

## Scalable applications
{: #scalable_apps}

With a few adjustments to how your applications connect, you can make your {{site.data.keyword.iot_short_notm}} applications more scalable by balancing the load handling of event messages across multiple instances of an application.

The number of clients that are required for optimum load balancing and scalability varies by deployment. To identify the optimum number of clients, you need to stress test your system further.


To enable load balancing, ensure that the application subscription is non-durable and that the client ID in the subscription matches the following format:

```
  A:org_id:app_id
```

Where:
-  The character **A** indicates that the client is a scalable application.
- org_id is the unique six character organization ID that was generated when you registered the service alphanumeric string that was assigned when you first registered the service.
-  app_id is a user-defined unique string identifier for the client. The string can contain only alpha-numeric characters (a-z, A-Z, 0-9) and the following special characters: dash (-); underscore (\_); dot (.).

**Important:**
- Only non-durable subscriptions are supported for scalable applications.
- The client ID must precede with an uppercase **A** character to be correctly designated as a scalable application by {{site.data.keyword.iot_short_notm}}.
- Other clients that are part of the scalable application must use the same client ID.


### How it works

The {{site.data.keyword.iot_short_notm}} service extends the MQTT V3.1.1 messaging protocol specification to support shared subscriptions. Shared subscriptions provide load balancing capabilities for applications. A shared subscription might be needed if a back-end enterprise application cannot cope with the volume of messages that are being published to a specific topic space. For example, when many devices publish messages that are being processed by a single application, it might be necessary to leverage the load balancing capability of a shared subscription. {{site.data.keyword.iot_short_notm}} shared subscription support is limited to
non-durable subscriptions only.


**Example**

The following scenario is one example of how a scalable application works in {{site.data.keyword.iot_short_notm}}:

- Client one connects as **A:abc123:myApplication** and subscribes to all device events, which means that client one receives 100% of the device events that are published.
- Client two connects as **A:abc123:myApplication** and also subscribes to all device events, which means that from this point forward, client one and client two share between them all of the events that get published. The processing load is shared equally between client one and client two.
- Client three connects as **A:abc123:myApplication** and also subscribes to all device events, which means that from this point forward, clients one, two, and three share the processing load for events between all three instances.
- Clients two and three then unsubscribe from all device events, which means that from this point forward, only client one receives all device events that are published. While instances two and three are still connected to the service, instance one receives 100% of the device events that are published.
