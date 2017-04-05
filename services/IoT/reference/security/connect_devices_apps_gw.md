---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-05"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Connecting applications, devices, and gateways using the API
{: #connect_devices_apps_gw}

You can connect applications, devices, and gateways to {{site.data.keyword.iot_full}} through the MQTT protocol. You can also use the HTTP REST API to connect devices to {{site.data.keyword.iot_short_notm}}.
{: shortdesc}


## Client connection URLs
{: #client_connect_url}

To connect device, application, and gateway clients to your {{site.data.keyword.iot_short_notm}} instance, use the following connection URLs:

### Messaging address

<pre class="pre"><var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com</pre>
{: codeblock}

### HTTP REST API connection URL

<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.internetofthings.ibmcloud.com/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>
{: codeblock}

**Notes**
- Where *orgId* is the unique organization ID that was generated when you registered the service instance.
- If you are connecting a device or application to the Quickstart service, specify 'quickstart' as the *orgId* value.

## Port security
{: #client_port_security}

Ensure that the required ports are open and enabled for communication. Ports 8883 and 443 support secure connections using TLS with the MQTT and HTTP protocol. Port 1883 supports non-secure connections with the MQTT and HTTP protocol. Information about connection type and associated port numbers is summarized in the following table:   

|Connection type |Port number|
|:---|:---|
|Non-secure|1883|
|Secure|8883|
|Secure|443|

MQTT is supported over TCP and WebSockets. MQTT clients connect by using appropriate credentials, such as device authentication tokens for devices and API keys and tokens for applications. Because MQTT messaging to the insecure port 1883 sends these credentials in plain text, always use the secure alternatives 8883 or 443 instead. The TLS credentials are always encypted when sent over secure ports. Be aware that you must enable TLS in the application by using the tls_set() method that is in the Python MQTT library. Otherwise, the data might be sent insecurely.

When you use secure MQTT messaging on ports 8883 or 443, newer client libraries automatically trust the certificate that is presented by {{site.data.keyword.iot_short_notm}}. If this is not the case for your client environment, you can download and use the full certificate chain from [messaging.pem](https://github.com/ibm-messaging/iot-python/blob/master/src/ibmiotf/messaging.pem).


## TLS requirements
{: #tls_requirements}

Some Transport Layer Security (TLS) client libraries do not support domains that include a wildcard. If you cannot successfully change libraries, disable certificate checking.

Your TLS requirements depend on whether you are connecting to {{site.data.keyword.iot_short_notm}} with the MQTT or HTTP protocol. The following sections show the cipher suites that are supported if the default server certificate is used. If you are using your own client
certificate, the cipher suites that are supported depend on the certificate that is used.

### TLS requirements for MQTT connections

{{site.data.keyword.iot_short_notm}} requires TLS v1.2 and the following cipher suites:


- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384

### TLS requirements for HTTP connections

If you are using the default server certificate, {{site.data.keyword.iot_short_notm}} requires TLS v1, TLS v1.1, or TLS v1.2 and the following cipher suites:


- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_256_GCM_SHA384


## MQTT client authentication
{: #mqtt_authentication}

**Important:** Each MQTT client requires a unique client ID. If you attempt to connect a client in your organization by using a client ID that is already connected, the first connection is disconnected.

Devices and gateways that are connected directly to the {{site.data.keyword.iot_short_notm}} display a status icon on the dashboard to indicate that they are connected. Devices that are connected indirectly through a gateway are shown as disconnected because the dashboard is unaware of devices that are connected through a gateway.

### MQTT client identifiers

For devices, applications, and gateways to successfully authenticate, define each MQTT client by using the following client identifiers and format:

|Client type |ID|MQTT ID format|
|:---|:---|:---|
|Applications|a|<pre class="pre">a:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
|Scalable Applications|A|<pre class="pre">A:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
|Devices|d|<pre class="pre">d:<var class="keyword varname">orgId</var>:<var class="keyword varname">deviceType</var>:<var class="keyword varname">deviceId</var></pre>|
|Gateways|g|<pre class="pre">g:<var class="keyword varname">orgId</var>:<var class="keyword varname">typeId</var>:<var class="keyword varname">deviceId</var></pre>|

Where
- *orgId* is the unique six-character organization ID that was generated when you registered the service.
- *appId* is a user-defined unique string identifier for the client.
- *deviceId* uniquely identifies a device or gateway across all types and is analogous to a serial number.
- *device_type* is the identifier for the type of device that is connecting and is analogous to a model number.
- *typeId* is an identifier of the type of gateway that is connecting and is analogous to a model number.

The *appId*, *type_id*, *device_type*, and *device_id* values must be no more than 36 characters and can contain only:
- Alpha-numeric characters (a-z, A-Z, 0-9)
- Dashes ( - )
- Underscores ( _ )
- Dots ( . )

**Notes:**
- When you connect to the Quickstart service, authentication is not required.
- You do not need to register an application before you connect.


### Connecting applications by using MQTT

{{site.data.keyword.iot_short_notm}} applications require an API key to connect into an organization. When an API key is registered, a token is generated, which must be used with that API key.

The following code provides an example of an API key:

<pre class="pre">a-<var class="keyword varname">orgId</var>-a84ps90Ajs</pre>
{: codeblock}

The following example shows a typical authentication token:

```
 MP$08VKz!8rXwnR-Q*
```

When you make an MQTT connection by using an API key, ensure that you meet the following requirements:

- The MQTT client ID is in the following format: a:*orgId*:*appId*
- The MQTT user name is the API key, for example, a-*orgId*-a84ps90Ajs
- The MQTT password is the authentication token, for example, *MP$08VKz!8rXwnR-Q*

For more information, see [MQTT connectivity for applications](../../applications/mqtt.html).

### Device authentication

#### User names
The {{site.data.keyword.iot_short_notm}} service supports only token-based authentication for devices; therefore, each device has only one valid user name.
A value of `use-token-auth` indicates to the service that the authentication token for the gateway or device is used as the password for the MQTT connection.

For more information, see [MQTT connectivity for devices](../../devices/mqtt.html).

#### Passwords
If the client is using token based authentication, submit the device authentication token as the password for all MQTT connections.
