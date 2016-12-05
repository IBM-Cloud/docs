---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Configuring certificates (Beta)
{: #set_up_certificates.md}
Last updated: 30 November 2016
{: .last-updated}

By using the Risk and Security Management add-on, certificates are used for device authentication or to replace the default {{site.data.keyword.iot_full}} server certificate for MQTT messaging. Any devices that do not have valid signed certificates are denied access and cannot communicate with the server.

To configure certificates and server access for devices, the system operator registers the associated certificate authority (CA) certiﬁcates and optionally registers message server certificates into the {{site.data.keyword.iot_short_notm}} platform.

## Certificate requirements
{: #cert_reqs.md}

The certificate that you register must have the the device ID entered as either the Common Name (CN) or SubjectAltName in the certificate. For the the *CN* field, the format is CN=d:devtype:devid. For the SubjectAltName field, the format is: SubjectAltName=d:devtype:devid where devtype is the Device Type of the device and devid is the Client ID of the device.

The use of a certificate revocation list (CRL), to indicate which devices are no longer allowed to connect, is not supported in the beta release.

If you add a CA certificate or replace the messaging server certificate, all devices must connect using an MQTT client that supports Server Name Indication (SNI). With the multi-tenancy architecture, SNI tells the MQTT server which certificates should be used for a each organization/tenant connection.

##Registering Certificate Authority (CA) certificates for device authentication
{: #reg_ca_cert.md}

1. Log in to {{site.data.keyword.iot_short_notm}} and navigate to **General Settings**.
2. In the **Risk Management** section, under **CA Certificates**, click **Add Certificate**.
3. Browse to select a certificate file to upload, or drag and drop a file in the **Add Certificate** window. The file can have only one certificate within it, and the dates of the certificate must be valid. Files that have extensions .pem, .cer, .cert, or .crt are accepted. You can preview the certificate information within the selected file.
4. Enter a description of the certificate file.
5. Confirm that the correct file is selected and click **Save**. The selected certificate is is listed in the
table and it is active by default.

## Registering messaging server certificates
{: #reg_msg_cert.md}

Default server certificates are provided with the platform. You can use one of the default certificates or upload one from your organization. If you do not yet have a certificate to use, you can create a request for a new certificate. After you receive the new certificate, you must have it signed and then upload it back to the platform.

To use one of the default certificates or another certificate that has already been uploaded, select the certificate you want to use from the **Default messaging server certificate** drop-down list in the table under **Messaging Server Certificates**.

### Uploading a certificate from your organization

1. In the **Risk Management** section of **General Settings**, under **Messaging Server Certificates**, click **Add Certificate**.
2. Browse to select a certificate file to upload, or drag and drop a file in the **Add Certificate** window.
3. Browse to select the private key file to upload, or drag and drop a file in the **Add Certificate** window.  
4. Enter the passphrase of the private key, if the private key was encrypted with a passphrase.
5. Confirm that the correct file is selected and click **Save**.
6. Select the newly uploaded certificate from the **Default messaging server certificate** drop-down list. The selected certificate is is listed in the table as the active certificate.


### Requesting a new certificate
{: #request_cert.md}

 If you want to use a new messaging server certificate, you can generate a certificate signing request (CSR) to request a new certificate.

 1. In the **Risk Management** section of **General Settings**, under **Messaging Server Certificates**, click **Generate CSR**.
 2. Enter the details to request a certificate signing request (CSR) for your server, and click **Generate**. The CSR is displayed in the table.
 3. Download the request and submit it to a certification authority for signing.
 4. After you obtain a certificate, you can upload it by following the steps in Uploading a certificate from your organization. After the certificate is uploaded, the CSR in the table is replaced with the uploaded certificate.
