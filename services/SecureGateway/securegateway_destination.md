---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-10"

---

# Adding a Destination

A destination is a definition of how to connect to a specific on-premises or cloud resource. Once the destination has been created, the {{site.data.keyword.SecureGateway}} servers will provide it with a unique public endpoint where it will listen for connections while the gateway is connected.

![Dashboard with no destinations](./images/emptyDestinations.png?raw=true "Dashboard with no destinations")

From within your new gateway and on the Destinations tab, click the Add Destination button to open the Add Destination panel.  There are two methods for creating your destination:  a guided setup that shows how each piece fits into the overall architecture and an advanced setup that provides all fields and options on a single panel.  

The guided setup <b>does not</b> allow for the configuration of proxy information, server name indicators, or the upload of a destination-specific cert/key pair.  After creation, all fields are available via the Edit Destination panel.

## Guided Panel

![Guided Setup](./images/guidedLanding.png?raw=true "Guided Setup landing panel")

## Advanced Panel

![Advanced Setup](./images/advancedLanding.png?raw=true "Advanced Setup landing panel")

## On-premises vs Cloud Destinations
{: #dest-types}

The first question to answer when creating your destination is where the resource resides that you need to connect to.

### On-premises Destination
The on-premises destination is for the use case where an application in the public space needs access to a restricted resource located on-premises.
![On Premises destination](./images/onPremDestination.png?raw=true "On-premises Destination")

### Cloud Destination
The cloud destination is for the use case where an application located in a restricted network needs access to a resource that is available in a public space.
![Reverse Destination](./images/reverseDestination.png?raw=true "Cloud Destination")

## Defining your Destination
For both types of destinations, the following information is required:

- <b>Resource Hostname</b>: This is the IP or hostname of the resource you need to connect to.
- <b>Resource Port</b>: This is the port that your resource is listening on.
- <b>Protocol</b>: This is the type of connection your application will be making.  See the table below for the various [protocol options](#protocols).  For configuring the type of connection your resource is expecting, check the [Resource authentication](#resource-auth) section.

If you have selected a cloud destination you will also need to provide a <b>Client Port</b>.  This is the port that the {{site.data.keyword.SecureGateway}} Client will listen on to allow connections to the associated resource hostname and port.

## Protocol options
{: #protocols}

This table provides all of the available options for how your application can initiate connections/requests with {{site.data.keyword.SecureGateway}}.

Protocol | Description
-- | --
TCP | No authentication. Your application can communicate directly with the {{site.data.keyword.SecureGateway}} servers without requiring any certificates.
TLS: Server Side | Transport Layer Security (TLS) is enabled and the server provides a certificate to prove its authenticity.
TLS: Mutual Auth | The server provides a set of certificates and your application must also provide a certificate as part of its connection.
HTTP | TCP connection where the host header is rewritten to match the on-premises hostname.
HTTPS | TLS: Server Side connection where the host header is rewritten to match the on-premises hostname.
HTTPS: Mutual Auth | TLS: Mutual Auth connection where the host header is rewritten to match the on-premises hostname.


## Configuring Mutual Authentication
{: #mutual-auth}

For protocols enforcing mutual authentication, you will need to upload your own certificate or the server will automatically create a self-signed certificate/key pair for your application to use.  This pair can be downloaded alongside the server certificate.
![Mutual Authentication Panels](./images/mutualAuth.png?raw=true "Mutual Authentication panels")

### User Authentication
{: #user-auth}

The user authentication section is for managing the authorization of your requesting/connecting application with {{site.data.keyword.SecureGateway}}.  This field accepts a single certificate which should be the certificate your application will be presenting alongside any connection/request.

### Resource Authentication
{: #resource-auth}

Resource authentication determines how {{site.data.keyword.SecureGateway}} will attempt to connect to the defined resource.  Three options are available:  None, TLS (server-side), and Mutual Auth.  Depending on your choice, different authentication options become available.

Enabling TLS on the connection to your resource is separate from the TLS used for User Authentication.  TLS for User Authentication secures the access between your initial requesting application and {{site.data.keyword.SecureGateway}} (e.g., between your {{site.data.keyword.Bluemix_notm}} app and the {{site.data.keyword.SecureGateway}} servers) while TLS for Resource Authentication secures the connection between {{site.data.keyword.SecureGateway}} and your defined resource (e.g., between the {{site.data.keyword.SecureGateway}} client and your on-premises database).

#### Cloud/On-Premises Authentication

This option becomes available by selecting TLS or Mutual Auth for your Resource Authentication.  The name of the field will match the [type of destination](#dest-types) you have chosen.  This field allows for up to 6 certificates to be uploaded in order to validate the certificate of the resource you are connecting to.  These files will be added to the CA of connection to the resource and should contain the certificate or certificate chain that your resource will be presenting.

#### Server Name Indicator (SNI)
This option becomes available by selecting TLS or Mutual Auth for your Resource Authentication.  This is used to allow a separate hostname to be provided to the TLS handshake of the resource connection.

### Client Certificate and Key
Where the Client Certificate and Key fields appears depends on the [type of destination](#dest-types) you have chosen.  In both situations, the files provided here will be used by the SG Client to identify itself for TLS connections.  If no files are uploaded, the {{site.data.keyword.SecureGateway}} servers will automatically generate a self-signed pair with a CN of `localhost`.  For instructions on how to generate a certificate/key pair, [click here](./securegateway_keygen.html).

For an on-premises destination, it will appear under Resource Authentication if Resource Authentication: Mutual Auth has been selected.  In this case, the client will use this certificate/key pair for its outbound connection to the defined resource.  The CA of this connection will contain the certificates provided in the [Cloud/On-prem Authentication](#resource-auth) field.

For a cloud destination, it will appear under User Authentication if a TLS protocol has been selected.  In this case, the client will use this certificate/key pair to establish TLS listeners with the file uploaded to the [User Authentication](#user-auth) in the CA.  

## Configuring Network Security
To prevent all but specific IP addresses from connecting to your cloud host and port, you can choose to enforce iptable rules on your on-premises destination.
![Network Security Panel](./images/networkSecurity.png?raw=true "Network Security panel")

To enforce iptable rules, check the box <b>Restrict cloud access to this destination with iptable rules</b> from the Network Security panel.  Once the box is checked, you can begin adding the IPs that should be allowed to connect.  If no IPs are provided, all connections to this cloud host and port will be rejected as long as the <b>Restrict cloud access</b> box is checked.

<b>Note</b>: The IPs or ports provided must be the external IP address that the {{site.data.keyword.SecureGateway}} servers will see, not the local IP address of the machine making the request.

### Adding iptable rules
When adding rules to iptables, you can provide individual IPs or an IP range along with either a single port or a port range.  All ranges provided are inclusive.  The following table has some examples as well as how they will resolve within iptables:

IP Addresses | Ports | Results
-- | -- | --
1.2.3.4 | 5000 | Only IP 1.2.3.4 from port 5000 will be allowed.
1.2.3.4-2.3.4.5 | 5000 | All IPs between 1.2.3.4 and 2.3.4.5 from port 5000 will be allowed.
1.2.3.4 | 5000:10000 | Only IP 1.2.3.4 from ports 5000 to 10000 will be allowed.
1.2.3.4-2.3.4.5 | 5000:10000 | All IPs between 1.2.3.4 and 2.3.4.5 from ports 5000 to 10000 will be allowed.
1.2.3.4 | | Only IP 1.2.3.4 from any port will be allowed.
| 5000 | Any IP from port 5000 will be allowed.

Specific rules can also be associated with an application.  For more information on creating associated rules, see [how to create iptable rules for your app](./iptables.html).

## Configuring Proxy Options
If your on-premises destination is located behind a SOCKS proxy, you can configure the proxy settings for your destination in the Proxy Options panel.
![Proxy Options Panel](./images/proxyOptions.png?raw=true "Proxy Options panel")

To configure the proxy settings, you only need to provide the hostname and port that the proxy is listening on as well as the SOCKS protocol that is being used (4, 4a, 5).

## Destination Settings
Once your destination has been created, click the settings icon to see the following information:

- The destination ID required to use the API.
- <b>On-premises destinations will have a cloud host and port.  This information is required by your application in order to connect to your on-premises resource.</b>
- <b>Cloud destinations will have a client port.  This is the port the {{site.data.keyword.SecureGateway}} Client will be listening on in order to connect your on-premises application to your cloud resource.</b>
- The resource host and port this destination is pointed to.
- When the destination was created as well as the user who created it.
- When the destination was last modified as well as the user who modified it.
