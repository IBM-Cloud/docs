---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Risk and Security Management
{: #RM_security}
Last updated: 15 November 2016
{: .last-updated}

The Risk and Security Management add-on enables organizations to enhance IBM Watson IoT Platform security by creating, enforcing, and reporting on device connection security. With this add-on, certificates and transport layer security (TLS) authentication are used, on top of the user IDs and tokens that are used by Watson IoT Platform to determine how and where devices connect with the platform. During communication between devices and the server, any devices that do not have valid certificates with server access, as configured in the Risk and Security Management add-on, are denied access, even if they use valid user IDs and passwords.

**Note:** To sign up for and enable the IBM Watson IoT Platform Risk and Security Management Beta program, go to https://developer.ibm.com/iotplatform/2016/11/02/experience-the-latest-iot-security-capabilities-sign-up-to-our-november-beta-today/.

## Connection security policy

The Connection Security policy enforces how devices connect to the platform. You can set up default connection policies for all device types, as well as custom settings for specific device types. The policy can be set to allow unencrypted connections, to enforce only transport layer security (TLS) connections, and to enable devices to authenticate with client-side certificates. When client-side certificates are being used, the security policy provides an additional option of using only the certificate for client authentication or using a combination of both a client certificate and client ID and authentication token pair.   

Connection security can also be set up for clients to use their own server-side certificate instead of the default certificate that is provided. This can be useful, for example, if the users’ devices will be authenticating the server during the TLS handshake. In this initial release of Risk and Security Management the domain name of the Watson IoT Platform server cannot not be changed and must be used as-is in the server certificate.

## Client certificates

To configure client certificates and server access for devices, the system operator imports the associated certificate authority (CA) certiﬁcates and messaging server certificates into Watson IoT platform. The security analyst then conﬁgures the connection security policies so that the default connections between devices and the platform use either the Certificates Only or Certificates with Authentication Tokens security levels. The analyst can add different policies for different device types.

## Whitelist and blacklist policies

Whitelist and blacklist policies provide the ability to control the locations from which devices are allowed to connect to the organization’s account. A blacklist identifies all of the IP addresses, CIDRs, or countries that are to be denied server access, while a whitelist gives explicit access to specific IP addresses.

## Risk and Security Management dashboard

Finally, the system operator and the security analyst can use the Risk and Security Management dashboard to view the overall security status. Cards on the dashboard can provide them with a comprehensive compliance overview, as well as the connection status of devices.
