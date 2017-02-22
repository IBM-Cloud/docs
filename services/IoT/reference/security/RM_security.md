---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-07"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Risk and Security Management
{: #RM_security}

The Risk and Security Management add-on enables organizations to enhance {{site.data.keyword.iot_full}} security by creating, enforcing, and reporting on device connection security. With this add-on, certificates and transport layer security (TLS) authentication are used, on top of the user IDs and tokens that are used by {{site.data.keyword.iot_short_notm}} to determine how and where devices connect with the platform. During communication between devices and the server, any devices that do not have valid certificates with server access, as configured in the Risk and Security Management add-on, are denied access, even if they use valid user IDs and passwords.

## Connection security policy
{: #connect_policy}

The Connection Security policy enforces how devices connect to the platform. You can set up default connection policies for all device types, as well as custom settings for specific device types. The policy can be set to allow unencrypted connections, to enforce only transport layer security (TLS) connections, and to enable devices to authenticate with client-side certificates. When client-side certificates are being used, the security policy provides an additional option of using only the certificate for client authentication or using a combination of both a client certificate and client ID and authentication token pair.

For information about how to configure connection security policies, see [Configuring security policies](set_up_policies.html).

Connection security can also be set up for clients to use their own server-side certificate instead of the default certificate that is provided. This can be useful, for example, if the users’ devices will be authenticating to the server during the TLS handshake. In this initial release of Risk and Security Management the domain name of the {{site.data.keyword.iot_short_notm}} server cannot not be changed and must be used as-is in the server certificate.

## Client certificates
{: #certificates}

To configure client certificates and server access for devices, the system operator imports the associated certificate authority (CA) certiﬁcates and messaging server certificates into {{site.data.keyword.iot_short_notm}}. The security analyst then conﬁgures the connection security policies so that the default connections between devices and the platform use either the Certificates Only or Certificates with Authentication Tokens security levels. The analyst can add different policies for different device types.

For information about how to configure certificates, see [Configuring certificates](set_up_certificates.html).

## Blacklist and whitelist policies
{: #wl_bl}

Blacklist and whitelist policies provide the ability to control the locations from which devices are allowed to connect to the organization’s account. A blacklist identifies all of the IP addresses, CIDRs, or countries that are to be denied server access, while a whitelist gives explicit access to specific IP addresses.

For information about how to configure blacklist and whitelist policies, see [Configuring blacklists and whitelists](set_up_policies.html#config_black_white).

## Risk and Security Management dashboard
{: #dashboard}

Finally, the system operator and the security analyst can use the Risk and Security Management dashboard to view the overall security status. Cards on the dashboard can provide them with a comprehensive compliance overview, as well as the connection status of devices.
