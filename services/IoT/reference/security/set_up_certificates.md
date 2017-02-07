---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-02"
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

## Certificate requirements
{: #cert_reqs}

### CA certificates
CA certificates enable the organization to recognize the client certificates on devices as trusted so that devices can connect to the server. A CA certificate can use a certificate revocation list (CRL). The CRL must be reachable at the moment that the CA is added to the platform, or the CA certificate will be rejected.

If you add a CA certificate or replace the messaging server certificate, all devices must connect using an MQTT client that supports Server Name Indication (SNI) so that the server can use the appropriate CAs to authenticate the device.

If you add a CA certificate, but do not have the Risk and Security Management add-on enabled, all devices connect with the TLS with Token and Client Certificate Authentication connection policy. If you do have Risk and Security Management add-on enabled, you can configure different connection policies. For information about how to configure connection security policies, see [Configuring security policies](set_up_policies.html).

### Client or device certificates
Individual client, or device, certificates remain on the devices and are not uploaded to the platform. The CA signing certificate that is used to sign all of the device certificates is the only certificate that you upload to the platform. If you are using self-signed server certificates, you must upload the Root and intermediate CA (ca.pem) that is used to sign the client certificate (cert.pem).

The individual device certificate that you sign with the CA certificate must have the device ID entered as either the Common Name (CN) or SubjectAltName in the certificate. For the the *CN* field, the format is 'CN=d:devtype:devid'. For the SubjectAltName field, the format is 'SubjectAltName=email:d:devtype:devid' where 'devtype' is the Device Type of the device and 'devid' is the Client ID of the device.

## Registering Certificate Authority (CA) certificates for device authentication
{: #reg_ca_cert}

1. Log in to {{site.data.keyword.iot_short_notm}} and navigate to **General Settings**.
2. In the **Security** section, under **CA Certificates**, click **Add Certificate**.
3. Browse to select a certificate file to upload, or drag and drop a file in the **Add Certificate** window. The file can have only one certificate within it, and the dates of the certificate must be valid. Only certificates in .pem or. der format are accepted. You can preview the certificate information within the selected file.
4. Enter a description for the certificate file.
5. Confirm that the correct file is selected and click **Save**. The selected certificate is listed in the table and is active by default.

## Registering messaging server certificates
{: #reg_msg_cert}

A default server certificate is provided with the platform. You can use the default certificate or upload one from your organization. If you do not yet have a certificate to use, you can create a request for a new certificate. After you receive the new certificate, you must have it signed and then upload it back to the platform.

To use the default certificate or another certificate that has already been uploaded, select the certificate you want to use from the **Default messaging server certificate** drop-down list in the table under **Messaging Server Certificates**.

**Note:** Platform dashboard pages might do internal connections to the messaging server to retrieve device information. When setting up self-signed server certificates for an organization, dashboard users must add the server certificate as a trusted certificate in their browsers to avoid connection issues because browsers, by default, will not recognize the messaging server as a trusted server.

### Uploading a certificate from your organization
{: #upload_cert}
1. In the **Security** section of **General Settings**, under **Messaging Server Certificates**, click **Add Certificate**.
2. Browse to select a certificate file to upload, or drag and drop a file in the **Add Certificate** window.
3. Browse to select the private key file to upload, or drag and drop a file in the **Add Certificate** window.  
4. Enter the passphrase of the private key, if the private key was encrypted with a passphrase.
5. Confirm that the correct file is selected and click **Save**.
6. Select the newly uploaded certificate from the **Default messaging server certificate** drop-down list. The selected certificate is listed in the table as the active certificate.

### Requesting a new certificate
{: #request_cert}

If you want to use a new messaging server certificate, you can generate a Certificate Signing Request (CSR) to request a new certificate.

 1. In the **Security** section of **General Settings**, under **Messaging Server Certificates**, click **Generate CSR**.
 2. Enter the details to request a CSR for your server, and click **Generate**. The CSR is displayed in the table.
 3. Download the request and submit it to a certification authority for signing.
 4. After you obtain a certificate, you can upload it by following the steps in [Uploading a certificate from your organization](#upload_cert). After the certificate is uploaded, the CSR in the table is replaced with the uploaded certificate.
