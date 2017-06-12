---

copyright:
  years: 2016, 2017
lastupdated: "2017-06-12"
---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Configuring certificates
{: #set_up_certificates}

Certificates are used for device authentication or to replace the default {{site.data.keyword.iot_full}} server certificate for MQTT messaging. Any devices that do not have valid signed certificates are denied access and cannot communicate with the server.

To configure certificates and server access for devices, the system operator registers the associated certificate authority (CA) certiﬁcates and optionally registers message server certificates into the {{site.data.keyword.iot_short_notm}} platform.

For information about using APIs to manage CA certificates and messaging server certificates, see [IBM Watson IoT Platform Authentication and Authorization APIs ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/security.html){: new_window}.

## CA certificates
CA certificates enable the organization to recognize the client certificates on devices as trusted so that devices can connect to the server.

If you add a CA certificate or replace the messaging server certificate, all devices must connect by using an MQTT client that supports Server Name Indication (SNI) so that the server can use the appropriate CAs to authenticate the device.

You can set the connection security level by configuring the connection security policy. For more information about how to do this, see [Configuring security policies](set_up_policies.html).

## Client certificates

Individual client (device or gateway) certificates remain on the devices and are not uploaded to the platform. The CA signing certificate that is used to sign all of the device and gateway certificates is the only certificate that you upload to the platform. If you are using self-signed messaging server certificates, you must upload the Root and intermediates certificates that are used to sign the client certificate (cert.pem).

The individual device or gateway certificate that you sign with the CA certificate must have the device ID or gateway ID entered as either the Common Name (CN) or SubjectAltName in the certificate.

For devices, the **CN** field format is `CN=d:devtype:devid`, and the **SubjectAltName** field format is `SubjectAltName=email:d:*devtype:devid*` where `email:d` is constant and `*devtype*` is the Device Type of the device and `*devid*` is the ID of the device in the platform.

For gateways, the **CN** field format is `CN=g:typeId:deviceId`, and the **SubjectAltName** field format is SubjectAltName=email:g:*devtype:devid*

Note: Do not include the `orgId` in the **CN** or **SubjectAltName** fields for device or gateway certificates. The `orgId` should be provided as part of the SNI information that is provided by the client implementation when connecting to the messaging server.

For more information about client certificates, see [the Connect Raspberry Pi to IBM Watson IoT Platform using Client side Certificates recipe ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-to-ibm-watson-iot-platform-using-client-side-certificates/){: new_window}

## Messaging server certificates

Messaging server certificates accept the default domain, internetofthings.ibmcloud.com. The following format must be followed for the certificate CN or SubjectAltName:

- `orgId.messaging.internetofthings.ibmcloud.com` (IoTP domain)

The following example shows a valid CN for the server certificate:

`mtxpd0.messaging.internetofthings.ibmcloud.com`

For more information about messaging server certificates, see [the Connect Raspberry Pi to IBM Watson IoT Platform using Self-Signed Server Certificate recipe ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-to-ibm-watson-iot-platform-using-selfsigned-server-certificate/){: new_window}

### Custom domains (Beta)
{: #custom_domains}

**Important**: The custom domains feature for messaging server certificates is available only as part of a limited Beta program. To enable custom domains, turn on the **Experimental Features** on the **Settings** page.

As part of the Beta feature, messaging server certificates accept custom domains. The following format must be followed for the certificate CN or SubjectAltName:

- `orgId.messaging.<custom domain>`

The **CN** field accepts wildcard characters for custom domains, as shown in the following example:

- `CN=*.messaging.mywiotpcustomdomain.com`

**Important**: For custom domains, an external DNS service is required to resolve the custom domain to the {{site.data.keyword.iot_full}} messaging server. This DNS service is not provided by the platform.

## Registering Certificate Authority (CA) certificates for device authentication
{: #reg_ca_cert}

1. Log in to {{site.data.keyword.iot_short_notm}} and navigate to **General Settings**.
2. In the **Security** section, under **CA Certificates**, click **Add Certificate**.
3. Browse to select a certificate file to upload or drag a file in to the **Add Certificate** window. The file can have only one certificate within it, and the dates of the certificate must be valid. Only certificates in .pem or. der format are accepted. You can preview the certificate information within the selected file.
4. Enter a description for the certificate file.
5. Confirm that the correct file is selected and click **Save**. The selected certificate is listed in the table and is active by default.

## Registering messaging server certificates
{: #reg_msg_cert}

A default server certificate is provided with the platform. You can use the default certificate or upload one from your organization. If you do not yet have a certificate to use, you can create a request for a new certificate. After you receive the new certificate, you must have it signed and then upload it back to the platform.

**Note:** Platform dashboard pages might do internal connections to the messaging server to retrieve device information. When setting up self-signed server certificates for an organization, dashboard users must add the server certificate as a trusted certificate in their browsers to avoid connection issues, because browsers, by default, will not recognize the messaging server as a trusted server.

## Uploading a messaging server certificate from your organization
{: #upload_cert}
1. In the **Security** section of **General Settings**, under **Messaging Server Certificates**, click **Add Certificate**.
2. Browse to select a certificate file to upload or drag a file in to the **Add Certificate** window.
3. Browse to select the private key file to upload or drag a file in to the **Add Certificate** window.
4. Enter the passphrase of the private key, if the private key was encrypted with a passphrase.
5. Confirm that the correct file is selected and click **Save**.

## Activating a messaging server certificate

To activate the default certificate or another certificate that has already been uploaded, select the certificate that you want to use from the **Default messaging server certificate** drop-down list in the table under **Messaging Server Certificates**. The selected certificate is listed in the table as the active certificate.

## Requesting a new messaging server certificate
{: #request_cert}

If you want to use a new messaging server certificate, you can generate a Certificate Signing Request (CSR) to request a new certificate.

1. In the **Security** section of **General Settings**, under **Messaging Server Certificates**, click **Generate CSR**.
2. Enter the details to request a CSR for your server and click **Generate**. The CSR is displayed in the table.
3. Download the request and submit it to a certificate authority for signing.
4. After you obtain a certificate, return to the CSR entry in the table and upload the new certificate. After the certificate is uploaded, the CSR in the table is replaced with the uploaded certificate.
