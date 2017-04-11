---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Risk and security management
{: #RM_security}

You can enhance security to enable creating, enforcing, and reporting on device connection security. With this advanced security, certificates and transport layer security (TLS) authentication are used in addition to the user IDs and tokens that are used by {{site.data.keyword.iot_short_notm}} to determine how and where devices connect with the platform. When certificates are enabled, during communication between devices and the server, any devices that do not have valid certificates, as configured in the security settings, are denied access, even if they use valid user IDs and passwords.

## Client certificates
{: #certificates}

To configure client certificates and server access for devices, the system operator imports the associated certificate authority (CA) certiﬁcates and messaging server certificates into {{site.data.keyword.iot_short_notm}}. The security analyst then conﬁgures the connection security policies so that the default connections between devices and the platform use either the Certificates Only or Certificates with Authentication Tokens security levels. The analyst can add different policies for different device types.

For information about how to configure certificates, see [Configuring certificates](set_up_certificates.html).

## Organization plans and security policies
The enhanced security policies enable organizations to determine how they want devices to connect and be authenticated to the platform, by using connection policies and blacklist and whitelist policies. The security policy options that are available to an organization depend on the organization's plan type, as follows:

**Standard Plan:**
- System operators can configure connection policies with the following options:
    - TLS Optional 
    - TLS with Token Authentication
    - TLS with Token and Client Certificate Authentication

**Advanced Security Plan (ASP) or Lite Plan:** 
- System operators can configure connection policies with the following options:
    - TLS Optional 
    - TLS with Token Authentication
    - TLS with Client Certificate Authentication
    - TLS with Token and Client Certificate Authentication
    - TLS with Client Certificate or Token
- System operators can configure blacklists or whitelists

## Connection policies
{: #connect_policy}

The connection policies enforce how devices connect to the platform. You can set up default connection policies for all device types and create custom settings for specific device types. The policy can be set to allow unencrypted connections, to enforce only transport layer security (TLS) connections, and to enable devices to authenticate with client-side certificates.

For information about how to configure connection security policies, see [Configuring security policies](set_up_policies.html).

Connection security can also be set up so that system operators can use their own messaging server certificate instead of the default certificate that is provided. Using a custom messaging server certificate can be useful if the users’ devices will be authenticating to the server during the TLS handshake. Only custom messaging server certificates that use the same domain that the original IoTP messaging server uses (<orgId>.messaging.internetofthings.ibmcloud.com) are supported.

## Blacklist and whitelist policies
{: #wl_bl}

Blacklist and whitelist policies provide the ability to control the locations from which devices are allowed to connect to the organization’s account. A blacklist identifies all of the IP addresses, CIDRs, or countries that are to be denied server access, while a whitelist gives explicit access to specific IP addresses.

For information about how to configure blacklist and whitelist policies, see [Configuring blacklists and whitelists](set_up_policies.html#config_black_white).

## Risk and Security Management dashboard
{: #dashboard}

Finally, the system operator and the security analyst can use the Risk and Security Management dashboard to view the overall security status. Cards on the dashboard can provide them with a comprehensive compliance overview, as well as the connection status of devices.
